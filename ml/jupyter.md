# Jupyter Tricks

- Multicursor support with `ALT`
- Big data analysis
  - [ipyparallel](https://github.com/ipython/ipyparallel) is a good option for simple map-reduce operations in python. We use it in rep to train many machine learning models in parallel
  - [pyspark](http://www.cloudera.com/documentation/enterprise/5-5-x/topics/spark_ipython.html)
  - spark-sql magic [%%sql](https://github.com/jupyter-incubator/sparkmagic)

```py
# To show Help/Man
?str.replace()
# IPython Magic Commands
# Full list https://ipython.readthedocs.io/en/stable/interactive/magics.html
%env: Set Environment Variables
# %env without any arguments lists all environment variables
%env OMP_NUM_THREADS
# The line below sets the environment variable
%env OMP_NUM_THREADS=4
# %run will execute and show the output from all code cells of the specified notebook or Python file
%run ./two-histograms.ipynb
%run ./two-histograms.py
# %load will replace the contents of the cell with an external script. You can either use a file on your computer as a source, or alternatively a URL.
%load ./hello_world.py
# %store: Pass variables between notebooks
data = 'this is the string I want to pass to different notebook'
%store data
del data # This has deleted the variable
# Now, in a new notebook…
%store -r data
print(data)
# %who: List all variables of global scope.
one = "for the money"
two = "for the show"
%who str #prints one two
# %%time will give you information about a single run of the code in your cell.
%%time
import time
for _ in range(1000): time.sleep(0.01) # sleep for 0.01 seconds
>> CPU times: user 21.5 ms, sys: 14.8 ms, total: 36.3 ms Wall time: 11.6 s
# %%timeit uses the Python timeit module which runs a statement 100,000 times (by default) and then provides the mean of the fastest three times.
import numpy
%timeit numpy.random.normal(size=100)
>> The slowest run took 7.29 times longer than the fastest. This could mean that an intermediate result is being cached.
100000 loops, best of 3: 5.5 µs per loop
# %%writefile magic saves the contents of that cell to an external file.
# %pycat does the opposite, and shows you (in a popup) the syntax highlighted contents of an external file.
%%writefile pythoncode.py
import x
...# saves in pythoncode.py
%pycat pythoncode.py # will load the file in the cell
# `%prun statement_name` will give you an ordered table showing you the number of times each internal function was called within the statement, the time each call took as well as the cumulative time of all runs of the function.
%prun some_useless_slow_function()
# Debugging with %pdb
%pdb
code here
# $Using LaTeX for forumlas
$P(A \mid B) = \frac{P(B \mid A)P(A)}{P(B)}$
```
