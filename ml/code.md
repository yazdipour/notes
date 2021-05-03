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

<!-- tabs:start -->

#### ** English **

Hello!

#### ** French **

Bonjour!

#### ** Italian **

Ciao!

<!-- tabs:end -->
