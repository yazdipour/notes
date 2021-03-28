# ML In Code

## Split and Read Large Files

```py
# Split big file
! split -1 250000 hi_deduo.txt hindi_
# read splitted files
import glob
file_list = glob.glob('../hindi_*')
```
