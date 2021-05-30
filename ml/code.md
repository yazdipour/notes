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
