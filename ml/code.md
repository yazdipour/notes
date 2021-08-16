# ML In Code

## Split and Read Large Files

```py
# Split big file
! split -1 250000 hi_deduo.txt hindi_
# read splitted files
import glob
file_list = glob.glob('../hindi_*')
```

## Read one Row of a big DF

```py
data = next(iter(df))
```

## Saving results in pickle

```py
save_classifier = open("naivebayes.pickle","wb")
pickle.dump(classifier, save_classifier)
save_classifier.close()


classifier_f = open("naivebayes.pickle", "rb")
classifier = pickle.load(classifier_f)
classifier_f.close()
```

# huggingface

## Dataset

```py
from transformers import AutoModelForSequenceClassification, AutoTokenizer
model = AutoModelForSequenceClassification.from_pretrained('bert-base-cased')
tokenizer = AutoTokenizer.from_pretrained('bert-base-cased')
print(tokenizer(dataset[0]['sentence1'], dataset[0]['sentence2']))
# {'input_ids': [101, 7277, 2180, 5303, 4806, 1117, 1711, 117, 2292, 1119, 1270, 107, 1103, 7737, 107, 117, 1104, 9938, 4267, 12223, 21811, 1117, 2554, 119, 102, 11336, 6732, 3384, 1106, 1140, 1112, 1178, 107, 1103, 7737, 107, 117, 7277, 2180, 5303, 4806, 1117, 1711, 1104, 9938, 4267, 12223, 21811, 1117, 2554, 119, 102],
#  'token_type_ids': [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
#  'attention_mask': [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]
# }
def encode(examples):
    return tokenizer(examples['sentence1'], examples['sentence2'], truncation=True, padding='max_length')
dataset = dataset.map(encode, batched=True)
dataset[0]
# {'sentence1': 'Amrozi accused his brother , whom he called " the witness " , of deliberately distorting his evidence .',
#  'sentence2': 'Referring to him as only " the witness " , Amrozi accused his brother of deliberately distorting his evidence .', 'label': 1,  'idx': 0,
#  'input_ids': array([  101,  7277,  2180,  5303,  4806,  1117,  1711,   117,  2292, 1119,  1270,   107,  1103,  7737,   107,   117,  1104,  9938, 4267, 12223, 21811,  1117,  2554,   119,   102, 11336,  6732, 3384,  1106,  1140,  1112,  1178,   107,  1103,  7737,   107, 117,  7277,  2180,  5303,  4806,  1117,  1711,  1104,  9938, 4267, 12223, 21811,  1117,  2554,   119,   102]),
#  'token_type_ids': array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]),
#  'attention_mask': array([1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1])}


#The first modification is just a matter of renaming the column as follows
dataset = dataset.map(lambda examples: {'labels': examples['label']}, batched=True)


# Here is how we can apply the right format to our dataset using datasets.Dataset.set_format() and wrap it in a torch.utils.data.DataLoader or a tf.data.Dataset:
import torch
dataset.set_format(type='torch', columns=['input_ids', 'token_type_ids', 'attention_mask', 'labels'])
dataloader = torch.utils.data.DataLoader(dataset, batch_size=32)
next(iter(dataloader))


# The two splits are returned as a dictionary of datasets.Dataset.
dataset.train_test_split(test_size=0.1)
```
