# Hadoop

- Data distrubutes between nodes and "NameNode" reserve the addresses of those partitioned data.
- Can have clone of data "DataNode" on other nodes.
- Can have another NameNode called "StandBy" to have another clone of "Active" Namenode for high availablity.
- Mappers categorize data by their tag/group.
- Reducers recieve these grouped data and process.
- Daemons on node = task trackers
- job tracker is a node which handle map and recude between nodes.

```sh
hadoop fs -ls
hadoop fs -put local.txt #upload to hadoop
hadoop fs -get local.txt #dl from hadoop
hadoop fs -rm x.txt

hadoop jar /usr/lib/hadoop-g.20-mapreduce/contrib/streaming/hadoop-streaming-2 -mrl-cdh4.1.1.jar -mapper mapper.py -reducer reducer.py -file mapper.py -file reducer.py -input myinput -out joboutput

hs mapper.py reducer.py indir outdir
```

## Patterns

- Filtering: like, sampling and top-N
- Summerization: Counting, Min/Max, Statistic, Index
- Structural: Combining data sets

## Sample

mapper.py

```py
import sys
def mapper():
    # read standard input line by line
    for line in sys.stdin:
        # strip off extra whitespace, split on tab and put the data in an array
        data = line.strip().split("\t")
        if len(data) != 6:
            continue
        date, time, store, item, cost, payment = data
        print "{0}\t{1}".format(store, cost)
test_text = """2013-10-09\t13:22\tMiami\tBoots\t99.95\tVisa
2013-10-09\t13:22\tNew York\tDVD\t9.50\tMasterCard
2013-10-09 13:22:59 I/O Error
^d8x28orz28zoijzu1z1zp1OHH3du3ixwcz114<f
1\t2\t3"""
# This function allows you to test the mapper with the provided test string
def main():
    import StringIO
    sys.stdin = StringIO.StringIO(test_text)
    mapper()
    sys.stdin = sys.__stdin__
```

Reducer.py

```py
import sys
salesTotal = 0
oldKey = None

for line in sys.stdin:
    data = line.strip().split("\t")
    if len(data) != 2:
        continue

    thisKey, thisSale = data
    if oldKey and oldKey != thisKey:
      print oldKey, "\t", salesTotal
      oldKey = thisKey
      salesTotal = 0

     oldKey = thisKey
     salesTotal += float(thisSale)

 if oldKey != None:
   print oldKey, "\t", salesTotal
```

## Run cdh(Cloudera Data Platform) on docker

```sh
# STEP 1:
docker pull cloudera/quickstart:latest
# STEP 2:
docker run --hostname=quickstart.cloudera --privileged=true -t -i -p 8888:8888 -p 80:80 cloudera/quickstart /usr/bin/docker-quickstart
# STEP 3:
browse hue localhost:8888 user/pass: cloudera/cloudera
```
