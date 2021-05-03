# Transformers

![](https://raw.githubusercontent.com/thunlp/PLMpapers/master/PLMfamily.jpg)

## ELMo

![](https://miro.medium.com/max/1234/1*8WhXg3oXUC4s-m7F2ePLEA.png)

- Not using Transformers, uses LSTM
- ELMo uses the concatenation of independently trained left-to-right and right-to-left LSTMs to generate features for downstream.

## BERT

- Main source code <https://github.com/google-research/bert>
- Blog https://jalammar.github.io/a-visual-guide-to-using-bert-for-the-first-time/
- Blog https://curiousily.com/posts/sentiment-analysis-with-bert-and-hugging-face-using-pytorch-and-python/

- Useful in Text Translation/Summarization because we have the future words.
- Created by stacking multiple encoders of Transformer.
- **Bidirectional** - to understand the text you’re looking you’ll have to look back (at the previous words) and forward (at the next words)
- **Transformers** - The Attention Is All You Need paper presented the Transformer model. The Transformer reads entire sequences of tokens at once. In a sense, the model is non-directional, while LSTMs read sequentially (left-to-right or right-to-left). The attention mechanism allows for learning contextual relations between words (e.g. in a sentence refers to Jim).his
- **(Pre-trained)** contextualized word embeddings - The ELMO paper introduced a way to encode words based on their meaning/context. Nails has multiple meanings - fingernails and metal nails.

### Input Formatting

- **[SEP], 102**
  - to mark the **end** of a sentence,
  - or the **separation** between two sentences
  - `print(tokenizer.sep_token, tokenizer.sep_token_id)`
- **[CLS], 101**
  - at the **beginning** of our text.
  - This token is used for **classification** tasks, but BERT expects it no matter what your application is.
  - `print(tokenizer.cls_token, tokenizer.cls_token_id)`
- **[PAD], 0**
  - There is also a special token for padding
- **[UNK], 100**
  - BERT understands tokens that were in the training set. Everything else can be encoded using the (unknown) token
- **[MASK]**
- Tokens that conform with the fixed vocabulary used in BERT
- **The Token IDs** for the tokens, from BERT’s tokenizer
- **Mask IDs** to indicate which elements in the sequence are tokens and which are padding elements
- **Segment IDs** used to distinguish different sentences
- **Positional Embeddings** used to show token position within the sequence

BERT was trained by masking 15% of the tokens with the goal to guess them. An additional objective was to predict the next sentence. Let’s look at examples of these tasks:

- Masked Language Modeling (Masked LM)

The objective of this task is to guess the masked tokens. Let’s look at an example, and try to not make it harder than it has to be:

That’s she -> That’s what she said[mask][mask]

- Next Sentence Prediction (NSP)

Given a pair of two sentences, the task is to say whether or not the second follows the first (binary classification). Let’s continue with the example:

Input = That’s she . [SEP] Hahaha, nice! [SEP][cls][mask][mask]

Label = IsNext

Input = That’s she . [SEP] Dwight, you ignorant ! [SEP][cls][mask][mask][mask]

Label = NotNext

The training corpus was comprised of two entries: Toronto Book Corpus (800M words) and English Wikipedia (2,500M words).

While the original Transformer has an encoder (for reading the input) and a decoder (that makes the prediction), BERT uses only the decoder.

BERT is simply a pre-trained stack of Transformer Encoders. How many Encoders? We have two versions - with 12 (BERT base) and 24 (BERT Large).

### Google play review Sentiment Analysis with BERT

```py
# https://curiousily.com/posts/sentiment-analysis-with-bert-and-hugging-face-using-pytorch-and-python/

import transformers
from transformers import BertModel, BertTokenizer, AdamW, get_linear_schedule_with_warmup
import torch
import numpy as np
import pandas as pd
import seaborn as sns
from pylab import rcParams
import matplotlib.pyplot as plt
from matplotlib import rc
from sklearn.model_selection import train_test_split
from sklearn.metrics import confusion_matrix, classification_report
from collections import defaultdict
from textwrap import wrap
from torch import nn, optim
from torch.utils.data import Dataset, DataLoader
%matplotlib inline
%config InlineBackend.figure_format='retina'
sns.set(style='whitegrid', palette='muted', font_scale=1.2)
HAPPY_COLORS_PALETTE = ["#01BEFE", "#FFDD00", "#FF7D00", "#FF006D", "#ADFF02", "#8F00FF"]
sns.set_palette(sns.color_palette(HAPPY_COLORS_PALETTE))
rcParams['figure.figsize'] = 12, 8

RANDOM_SEED = 42
np.random.seed(RANDOM_SEED)
torch.manual_seed(RANDOM_SEED)
# pytorch.seed_everything(RANDOM_SEED) will set seed for all processes

device = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")
# data pre-p
df = pd.read_csv("reviews.csv")
df.shape
df.info()
sns.countplot(df.score)
plt.xlabel('review score');

def to_sentiment(rating): # if r>3:2, r=3:1, else: 0
class_names = ['negative', 'neutral', 'positive']
df['sentiment'] = df.score.apply(to_sentiment)
ax = sns.countplot(df.sentiment)
plt.xlabel('review sentiment')
ax.set_xticklabels(class_names);

# Let’s load a pre-trained BertTokenizer:
PRE_TRAINED_MODEL_NAME = 'bert-base-cased'
tokenizer = BertTokenizer.from_pretrained(PRE_TRAINED_MODEL_NAME)
sample_txt = 'When was I last outside? I am stuck at home for 2 weeks.'
tokens = tokenizer.tokenize(sample_txt) #['When', 'was', 'I', 'last', 'outside', '?',
token_ids = tokenizer.convert_tokens_to_ids(tokens) #[1332, 1108, 146, 1314, 1796, 136, 146, 1821,..

# encoding
encoding = tokenizer.encode_plus(
  sample_txt,
  max_length=32,
  add_special_tokens=True, # Add '[CLS]' and '[SEP]'
  return_token_type_ids=False,
  pad_to_max_length=True,
  return_attention_mask=True,
  return_tensors='pt',  # Return PyTorch tensors
)
encoding.keys() # > dict_keys(['input_ids', 'attention_mask'])
encoding['input_ids'][0]
# tensor([ 101, 1332, 1108,  146, 1314, 1796,  136,  146, 1821, 5342, 1120, 1313, 1111,  123, 2277,  119,  102,    0,    0,    0,    0,    0,    0,    0, 0,    0,    0,    0,    0,    0,    0,    0])
encoding['attention_mask']
# tensor([[1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]])

#We can inverse the tokenization to have a look at the special tokens:
tokenizer.convert_ids_to_tokens(encoding['input_ids'][0]) # ['[CLS]', 'When',
#Choosing Sequence Length
token_lens = []
for txt in df.content:
  tokens = tokenizer.encode(txt, max_length=512)
  token_lens.append(len(tokens))
sns.distplot(token_lens)
plt.xlim([0, 256]);
plt.xlabel('Token count');
#Most of the reviews seem to contain less than 128 tokens, but we’ll be on the safe side and choose a maximum length of 160.
MAX_LEN = 160
#
# ALL IN ONE
#
class GPReviewDataset(Dataset):
  def __init__(self, reviews, targets, tokenizer, max_len):
    self.reviews = reviews
    self.targets = targets
    self.tokenizer = tokenizer
    self.max_len = max_len
  def __len__(self):
    return len(self.reviews)
  def __getitem__(self, item):
    review = str(self.reviews[item])
    target = self.targets[item]
    encoding = self.tokenizer.encode_plus(
      review,
      add_special_tokens=True,
      max_length=self.max_len,
      return_token_type_ids=False,
      pad_to_max_length=True,
      return_attention_mask=True,
      return_tensors='pt',
    )
    return {
      'review_text': review,
      'input_ids': encoding['input_ids'].flatten(),
      'attention_mask': encoding['attention_mask'].flatten(),
      'targets': torch.tensor(target, dtype=torch.long)
    }
def create_data_loader(df, tokenizer, max_len, batch_size):
  ds = GPReviewDataset(
    reviews=df.content.to_numpy(),
    targets=df.sentiment.to_numpy(),
    tokenizer=tokenizer,
    max_len=max_len
  )
  return DataLoader(
    ds,
    batch_size=batch_size,
    num_workers=4
  )

bert_model = BertModel.from_pretrained(PRE_TRAINED_MODEL_NAME)
last_hidden_state, pooled_output = bert_model(
  input_ids=encoding['input_ids'],
  attention_mask=encoding['attention_mask']
)

# The last_hidden_state is a sequence of hidden states
# of the last layer of the model. Obtaining the pooled_output
# is done by applying the BertPooler on last_hidden_state:
# last_hidden_state.shape = torch.Size([1, 32, 768])

# We have the hidden state for each of our 32 tokens (the length of our example sequence). But why 768? This is the number of hidden units in the feedforward-networks. We can verify that by checking the config:
# bert_model.config.hidden_size #768

# You can think of the pooled_output as a summary of the content, according to BERT. Albeit, you might try and do better. Let’s look at the shape of the output:
# pooled_output.shape #torch.Size([1, 768])

class SentimentClassifier(nn.Module):
  def __init__(self, n_classes):
    super(SentimentClassifier, self).__init__()
    self.bert = BertModel.from_pretrained(PRE_TRAINED_MODEL_NAME)
    self.drop = nn.Dropout(p=0.3)
    self.out = nn.Linear(self.bert.config.hidden_size, n_classes)
  def forward(self, input_ids, attention_mask):
    _, pooled_output = self.bert(
      input_ids=input_ids,
      attention_mask=attention_mask
    )
    output = self.drop(pooled_output)
    return self.out(output)

# Our classifier delegates most of the heavy lifting to the BertModel. We use a dropout layer for some regularization and a fully-connected layer for our output. Note that we’re returning the raw output of the last layer since that is required for the cross-entropy loss function in PyTorch to work.

model = SentimentClassifier(len(class_names)).to(device)

# We’ll move the example batch of our training data to the GPU:
input_ids = data['input_ids'].to(device)
attention_mask = data['attention_mask'].to(device)
print(input_ids.shape) # batch size x seq length # torch.Size([16, 160])
print(attention_mask.shape) # batch size x seq length # torch.Size([16, 160])

# To get the predicted probabilities from our trained model, we’ll apply the softmax function to the outputs:
F.softmax(model(input_ids, attention_mask), dim=1) # tensor([[0.5879, 0.0842, 0.3279],.....

# Training

# To reproduce the training procedure from the BERT paper, we’ll use the AdamW optimizer provided by Hugging Face. It corrects weight decay, so it’s similar to the original paper. We’ll also use a linear scheduler with no warmup steps:

EPOCHS = 10
optimizer = AdamW(model.parameters(), lr=2e-5, correct_bias=False)
total_steps = len(train_data_loader) * EPOCHS
scheduler = get_linear_schedule_with_warmup(
  optimizer,
  num_warmup_steps=0,
  num_training_steps=total_steps
)
loss_fn = nn.CrossEntropyLoss().to(device)

# How do we come up with all hyperparameters?
# The BERT authors have some recommendations for fine-tuning:

# Batch size: 16, 32
# Learning rate (Adam): 5e-5, 3e-5, 2e-5
# Number of epochs: 2, 3, 4

# We’re going to ignore the number of epochs recommendation but stick with the rest.
# Note that increasing the batch size reduces the training time significantly, but gives you lower accuracy.

# Helper func for training our model for one epoch

def train_epoch(model, data_loader, loss_fn, optimizer, device, scheduler, n_examples):
  model = model.train()
  losses = []
  correct_predictions = 0
  for d in data_loader:
    input_ids = d["input_ids"].to(device)
    attention_mask = d["attention_mask"].to(device)
    targets = d["targets"].to(device)
    outputs = model(
      input_ids=input_ids,
      attention_mask=attention_mask
    )
    _, preds = torch.max(outputs, dim=1)
    loss = loss_fn(outputs, targets)
    correct_predictions += torch.sum(preds == targets)
    losses.append(loss.item())
    loss.backward()
    nn.utils.clip_grad_norm_(model.parameters(), max_norm=1.0)
    optimizer.step()
    scheduler.step()
    optimizer.zero_grad()
  return correct_predictions.double() / n_examples, np.mean(losses)

# Training the model should look familiar, except for two things. The scheduler gets called every time a batch is fed to the model. We’re avoiding exploding gradients by clipping the gradients of the model using clipgrad_norm.

# Helper func to evaluate the model on a given data loader

def eval_model(model, data_loader, loss_fn, device, n_examples):
  model = model.eval()
  losses = []
  correct_predictions = 0
  with torch.no_grad():
    for d in data_loader:
      input_ids = d["input_ids"].to(device)
      attention_mask = d["attention_mask"].to(device)
      targets = d["targets"].to(device)
      outputs = model(
        input_ids=input_ids,
        attention_mask=attention_mask
      )
      _, preds = torch.max(outputs, dim=1)
      loss = loss_fn(outputs, targets)
      correct_predictions += torch.sum(preds == targets)
      losses.append(loss.item())
  return correct_predictions.double() / n_examples, np.mean(losses)

# Using those two, we can write our training loop. We’ll also store the training history:

%%time
history = defaultdict(list)
best_accuracy = 0
for epoch in range(EPOCHS):
  print(f'Epoch {epoch + 1}/{EPOCHS}')
  print('-' * 10)
  train_acc, train_loss = train_epoch(model, train_data_loader, loss_fn, optimizer, device, scheduler, len(df_train))
  print(f'Train loss {train_loss} accuracy {train_acc}')
  val_acc, val_loss = eval_model(model, val_data_loader, loss_fn, device, len(df_val))
  print(f'Val   loss {val_loss} accuracy {val_acc}')
  print()
  history['train_acc'].append(train_acc)
  history['train_loss'].append(train_loss)
  history['val_acc'].append(val_acc)
  history['val_loss'].append(val_loss)
  if val_acc > best_accuracy:
    torch.save(model.state_dict(), 'best_model_state.bin') #saving
    best_accuracy = val_acc

plt.plot(history['train_acc'], label='train accuracy')
plt.plot(history['val_acc'], label='validation accuracy')
plt.title('Training history')
plt.ylabel('Accuracy')
plt.xlabel('Epoch')
plt.legend()
plt.ylim([0, 1]);

# LOAD from pre-trained model
!gdown --id 1V8itWtowCYnb2Bc9KlK9SxGff9WwmogA
model = SentimentClassifier(len(class_names))
model.load_state_dict(torch.load('best_model_state.bin'))
model = model.to(device)

# Evaluation
test_acc, _ = eval_model(
  model,
  test_data_loader,
  loss_fn,
  device,
  len(df_test)
)
test_acc.item() #0.883248730964467
# The accuracy is about 1% lower on the test set. Our model seems to generalize well.

# helper function to get the predictions

def get_predictions(model, data_loader):
  model = model.eval()
  review_texts = []
  predictions = []
  prediction_probs = []
  real_values = []
  with torch.no_grad():
    for d in data_loader:
      texts = d["review_text"]
      input_ids = d["input_ids"].to(device)
      attention_mask = d["attention_mask"].to(device)
      targets = d["targets"].to(device)
      outputs = model(
        input_ids=input_ids,
        attention_mask=attention_mask
      )
      _, preds = torch.max(outputs, dim=1)
      review_texts.extend(texts)
      predictions.extend(preds)
      prediction_probs.extend(outputs)
      real_values.extend(targets)
  predictions = torch.stack(predictions).cpu()
  prediction_probs = torch.stack(prediction_probs).cpu()
  real_values = torch.stack(real_values).cpu()
  return review_texts, predictions, prediction_probs, real_values
# This is similar to the evaluation function, except that we’re storing the text of the reviews and the predicted probabilities:
y_review_texts, y_pred, y_pred_probs, y_test = get_predictions(model, test_data_loader)
print(classification_report(y_test, y_pred, target_names=class_names))

# show_confusion_matrix
def show_confusion_matrix(confusion_matrix):
  hmap = sns.heatmap(confusion_matrix, annot=True, fmt="d", cmap="Blues")
  hmap.yaxis.set_ticklabels(hmap.yaxis.get_ticklabels(), rotation=0, ha='right')
  hmap.xaxis.set_ticklabels(hmap.xaxis.get_ticklabels(), rotation=30, ha='right')
  plt.ylabel('True sentiment')
  plt.xlabel('Predicted sentiment');
cm = confusion_matrix(y_test, y_pred)
df_cm = pd.DataFrame(cm, index=class_names, columns=class_names)
show_confusion_matrix(df_cm)

# Predicting on Raw Text
review_text = "I love completing my todos! Best app ever!!!"
encoded_review = tokenizer.encode_plus(
  review_text,
  max_length=MAX_LEN,
  add_special_tokens=True,
  return_token_type_ids=False,
  pad_to_max_length=True,
  return_attention_mask=True,
  return_tensors='pt',
)

input_ids = encoded_review['input_ids'].to(device)
attention_mask = encoded_review['attention_mask'].to(device)
output = model(input_ids, attention_mask)
_, prediction = torch.max(output, dim=1)
print(f'Review text: {review_text}')
print(f'Sentiment  : {class_names[prediction]}')
# Review text: I love completing my todos! Best app ever!!!
# Sentiment  : positive
```

## T5

### QA with T5

```py
import argparse
import glob
import os
import json
import time
import logging
import random
import re
from itertools import chain
from string import punctuation

import pandas as pd
import numpy as np
import torch
from pathlib import Path
from torch.utils.data import Dataset, DataLoader
import pytorch_lightning as pl

from sklearn.model_selection import train_test_split
from termcolor import colored
import textwrap

from pytorch_lightning.callbacks import ModelCheckpoint

from transformers import (
    AdamW,
    T5ForConditionalGeneration,
    T5Tokenizer,
    get_linear_schedule_with_warmup
)

# reading from one file
with Path("x/BioASQ-train-factoid-4b.json").open() as json_file:
  data = json.load(json_file)
# reading from multiple files
factoid_paths = sorted(list(Path('x/').glob('BioASQ-train-*'))) # All json files in the path
dfs = []
for factoid_path in factoid_paths:
    encoding = tokenizer(
    sample_par['question'],
    sample_par['context'],
    max_length=396,
    padding='max_length',
    truncation="only_second",
    return_attention_mask=True,
    add_special_tokens=True,
    return_tensors="pt"
)
encoding.keys()#dict_keys(['input_ids', 'attention_mask'])
tokenizer.special_tokens_map # {'additional_special_tokens': "['<extra_id_0>', '<extra_id_1>', '<extra_id_2>', '<extra_id_3>', '<extra_id_4>', '<extra_id_5>', '<extra_id_6>', '<extra_id_7>', '<extra_id_8>', '<extra_id_9>', '<extra_id_10>', '<extra_id_11>', '<extra_id_12>', '<extra_id_13>', '<extra_id_14>', '<extra_id_15>', '<extra_id_16>', '<extra_id_17>', '<extra_id_18>', '<extra_id_19>', '<extra_id_20>', '<extra_id_21>', '<extra_id_22>', '<extra_id_23>', '<extra_id_24>', '<extra_id_25>', '<extra_id_26>', '<extra_id_27>', '<extra_id_28>', '<extra_id_29>', '<extra_id_30>', '<extra_id_31>', '<extra_id_32>', '<extra_id_33>', '<extra_id_34>', '<extra_id_35>', '<extra_id_36>', '<extra_id_37>', '<extra_id_38>', '<extra_id_39>', '<extra_id_40>', '<extra_id_41>', '<extra_id_42>', '<extra_id_43>', '<extra_id_44>', '<extra_id_45>', '<extra_id_46>', '<extra_id_47>', '<extra_id_48>', '<extra_id_49>', '<extra_id_50>', '<extra_id_51>', '<extra_id_52>', '<extra_id_53>', '<extra_id_54>', '<extra_id_55>', '<extra_id_56>', '<extra_id_57>', '<extra_id_58>', '<extra_id_59>', '<extra_id_60>', '<extra_id_61>', '<extra_id_62>', '<extra_id_63>', '<extra_id_64>', '<extra_id_65>', '<extra_id_66>', '<extra_id_67>', '<extra_id_68>', '<extra_id_69>', '<extra_id_70>', '<extra_id_71>', '<extra_id_72>', '<extra_id_73>', '<extra_id_74>', '<extra_id_75>', '<extra_id_76>', '<extra_id_77>', '<extra_id_78>', '<extra_id_79>', '<extra_id_80>', '<extra_id_81>', '<extra_id_82>', '<extra_id_83>', '<extra_id_84>', '<extra_id_85>', '<extra_id_86>', '<extra_id_87>', '<extra_id_88>', '<extra_id_89>', '<extra_id_90>', '<extra_id_91>', '<extra_id_92>', '<extra_id_93>', '<extra_id_94>', '<extra_id_95>', '<extra_id_96>', '<extra_id_97>', '<extra_id_98>', '<extra_id_99>']",
 'eos_token': '</s>',
 'pad_token': '<pad>',
 'unk_token': '<unk>'}
  df = extract_questions_and_answers(factoid_path) #prepairing
  dfs.append(df)
df = pd.concat(dfs) #merge all

# Tokenization
MODEL_NAME ='t5-base'
tokenizer = T5Tokenizer.from_pretrained(MODEL_NAME)
sample_encoding = tokenizer(
    "Would I rather be feared or loved?",
    "Easy. Both. I want people to be afraid of how much they love me. "
)
encoding = tokenizer(
    sample_par['question'],
    sample_par['context'],
    max_length=396,
    padding='max_length',
    truncation="only_second",
    return_attention_mask=True,
    add_special_tokens=True,
    return_tensors="pt"
)
encoding.keys()#dict_keys(['input_ids', 'attention_mask'])
tokenizer.special_tokens_map # *** {'additional_special_tokens': "['<extra_id_0>',... 'eos_token': '</s>', 'pad_token': '<pad>', 'unk_token': '<unk>'}
tokenizer.decode(encoding['input_ids'].squeeze()) # if wanna do reverse
answer_encoding = tokenizer(
    sample_par['answer_text'],
    max_length=32,
    padding='max_length',
    truncation=True,
    return_attention_mask=True,
    add_special_tokens=True,
    return_tensors="pt"
)

class BioQADataset(Dataset):
  def __init__(
      self,
      data:pd.DataFrame,
      tokenizer:T5Tokenizer,
      source_max_token_len: int = 396,
      target_max_token_len: int = 32,

      ):

    self.data =  data
    self.tokenizer =  tokenizer
    self.source_max_token_len =  source_max_token_len
    self.target_max_token_len =  target_max_token_len


  def __len__(self):
    return len(self.data)

  def __getitem__(self, index: int):
    data_row = self.data.iloc[index]

    source_encoding = tokenizer(
      data_row['question'],
      data_row['context'],
      max_length=self.source_max_token_len,
      padding='max_length',
      truncation="only_second",
      return_attention_mask=True,
      add_special_tokens=True,
      return_tensors="pt"
      )

    target_encoding = tokenizer(
      data_row['answer_text'],
      max_length=self.target_max_token_len,
      padding='max_length',
      truncation=True,
      return_attention_mask=True,
      add_special_tokens=True,
      return_tensors="pt"
      )

    labels = target_encoding['input_ids']
    labels[labels==0] = -100
    # All labels set to -100 are ignored (masked), the loss is only computed for labels in [0, ..., config.vocab_size]

    return dict(
        question=data_row['question'],
        context=data_row['context'],
        answer_text=data_row['answer_text'],
        input_ids=source_encoding["input_ids"].flatten(),
        attention_mask=source_encoding['attention_mask'].flatten(),
        labels=labels.flatten()
    )

sample_dataset = BioQADataset(df, tokenizer)
train_df, val_df = train_test_split(df, test_size=0.05)
for data in sample_dataset:
  print("Question: ", data['question'])
  print("Answer text: ", data['answer_text'])
  print("Input_ids: ", data['input_ids'][:10])
  print("Labels: ", data['labels'][:10])
  break

# Question:  What is the inheritance pattern of Li–Fraumeni syndrome?
# Answer text:  autosomal dominant
# Input_ids:  tensor([  363,    19,     8, 28915,  3275,    13,  1414,   104,   371,  6340])
# Labels:  tensor([ 1510, 10348,   138, 12613,     1,  -100,  -100,  -100,  -100,  -100])

class BioDataModule(pl.LightningDataModule):
  def __init__(
      self,
      train_df: pd.DataFrame,
      test_df: pd.DataFrame,
      tokenizer:T5Tokenizer,
      batch_size: int = 8,
      source_max_token_len: int = 396,
      target_max_token_len: int = 32,
      ):
    super().__init__()
    self.train_df = train_df
    self.test_df = test_df
    self.tokenizer = tokenizer
    self.batch_size = batch_size
    self.source_max_token_len = source_max_token_len
    self.target_max_token_len = target_max_token_len

  def setup(self):
    self.train_dataset = BioQADataset(
        self.train_df,
        self.tokenizer,
        self.source_max_token_len,
        self.target_max_token_len
        )

    self.test_dataset = BioQADataset(
    self.test_df,
    self.tokenizer,
    self.source_max_token_len,
    self.target_max_token_len
    )

  def train_dataloader(self):
    return DataLoader(
        self.train_dataset,
        batch_size=self.batch_size,
        shuffle=True,
        num_workers=4
        )
  def val_dataloader(self):
    return DataLoader(
        self.test_dataset,
        batch_size=self.batch_size,
        num_workers=4
        )

  def test_dataloader(self):
    return DataLoader(
        self.test_dataset,
        batch_size=1,
        num_workers=4
        )

BATCH_SIZE = 8
N_EPOCHS = 6

data_module = BioDataModule(train_df, val_df, tokenizer, batch_size=BATCH_SIZE)
data_module.setup()

from transformers import T5ForConditionalGeneration

MODEL_NAME = 'google/mt5-small'

model = T5ForConditionalGeneration.from_pretrained(MODEL_NAME, return_dict=True)

model.config()

input_ids = tokenizer(
    "translate English to German: I talk alot, so I've learned to tune myself out",
    return_tensors='pt'
).input_ids
generated_ids = model.generate(input_ids=input_ids)
preds = [
         tokenizer.decode(gen_id, skip_special_tokens=True, clean_up_tokenization_spaces=True)
         for gen_id in generated_ids
]
"".join(preds)
# Ich rede viel, also habe ich gelernt, mich selbst auszutun.
output = model(input_ids=encoding["input_ids"],
      attention_mask=encoding["attention_mask"],
      labels=labels)
output.loss # 5!

# Model

class BioQAModel(pl.LightningModule):
  def __init__(self):
    super().__init__()
    self.model = T5ForConditionalGeneration.from_pretrained(MODEL_NAME, return_dict=True)


  def forward(self, input_ids, attention_mask, labels=None):
    output = self.model(
        input_ids,
        attention_mask=attention_mask,
        labels=labels)

    return output.loss, output.logits

  def training_step(self, batch, batch_idx):
    input_ids = batch['input_ids']
    attention_mask=batch['attention_mask']
    labels = batch['labels']
    loss, outputs = self(input_ids, attention_mask, labels)
    self.log("train_loss", loss, prog_bar=True, logger=True)
    return {"loss": loss, "predictions":outputs, "labels": labels}

  def validation_step(self, batch, batch_idx):
    input_ids = batch['input_ids']
    attention_mask=batch['attention_mask']
    labels = batch['labels']
    loss, outputs = self(input_ids, attention_mask, labels)
    self.log("val_loss", loss, prog_bar=True, logger=True)
    return loss

  def test_step(self, batch, batch_idx):
    input_ids = batch['input_ids']
    attention_mask=batch['attention_mask']
    labels = batch['labels']
    loss, outputs = self(input_ids, attention_mask, labels)
    self.log("test_loss", loss, prog_bar=True, logger=True)
    return loss

  def configure_optimizers(self):

    optimizer = AdamW(self.parameters(), lr=0.0001)
    return optimizer

from transformers import T5ForConditionalGeneration
MODEL_NAME='t5-small' #https://huggingface.co/transformers/model_doc/t5.html#transformers.T5ForConditionalGeneration.parallelize

model =  T5ForConditionalGeneration.from_pretrained(MODEL_NAME, return_dict=True)
model = BioQAModel()
checkpoint_callback = ModelCheckpoint(
    dirpath="checkpoints",
    filename="best-checkpoint",
    save_top_k=1,
    verbose=True,
    monitor="val_loss",
    mode="min"
)

#logger = TensorBoardLogger("training-logs", name="bio-qa")
trainer = pl.Trainer(
    #logger = logger,
    checkpoint_callback=checkpoint_callback,
    max_epochs=N_EPOCHS,
    gpus=1,
    progress_bar_refresh_rate = 30
)
# %load_ext tensorboard
# %tensorboard --logdir ./lightning_logs
trainer.fit(model, data_module)
trainer.test()  # evaluate the model according to the last checkpoint

# Predictions
trained_model = BioQAModel.load_from_checkpoint("checkpoints/best-checkpoint.ckpt")
trained_model.freeze() #

def generate_answer(question):
    source_encoding=tokenizer(
        question["question"],
        question['context'],
        max_length = 396,
        padding="max_length",
        truncation="only_second",
        return_attention_mask=True,
        add_special_tokens=True,
        return_tensors="pt"
    )
    generated_ids = trained_model.model.generate(
      input_ids=source_encoding["input_ids"],
      attention_mask=source_encoding["attention_mask"],
      num_beams=1,  # greedy search
      max_length=80,
      repetition_penalty=2.5,
      early_stopping=True,
      use_cache=True)
    preds =[
            tokenizer.decode(generated_id, skip_special_tokens=True, clean_up_tokenization_spaces=True)
            for generated_id in generated_ids
    ]
    return "".join(preds)
# try
sample_question = val_df.iloc[0]
sample_question["question"]
sample_question["answer_text"]
generate_answer(sample_question)
```
