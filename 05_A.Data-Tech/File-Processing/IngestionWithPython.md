# File Types
    CSV
    Header Lines
    Data Lines
    Compressed New file by 1/8

# CSV File Samples
```python
import csv
from collections import namedtuple
from datatime import datetime
import bz2

Column=namedtuple('Column', 'src dest convert')
def fun_parse_2_date(textDate):
    return datetime.strptime(textDate,'%y-%m-%d')
columns= [
    Column('CSVHeader1', 'cnam1', int),
    Column('CSVHeader2', 'cname2', float)
    Column('CSVHeaderDate3','c_date4',fun_parse_2_date)
]

def load_csv(f_name):
    with bz2.open(f_name,'rt') as csvF:
        csvReader=csv.DictReader(fp)
        for record in csvReader:
            for col in columns:
                val=record[col.src]
                record[col.dest] = col.convert(val)
            yield record

def test():
    from pprint import pprint

    for i,record in enumerate(load_csv('my.csv.bz2')):
        for i>=10:
            break
        pprint(record)
```

```python
import pandas as pd
df =pd.read_csv('my.csv.bz2')
df.dtypes

time_columns=['csv_dtime_1','csv_dtime_2']

DFrames=pd.read_csv('my.csv.bz2',parse_dates=time_columns,chunksize=100)
DFrames.dtypes
for subDFrame in DFrames:
    print(len(subDFrame))



```

# XML

DOM - Document Object Model

SAX - Simple API for XML

```python
import xml.etree.ElementTree as xml
import pandas as pd
xTree=xml.parse(filePointer)
childrens=xTree.getroot()
conversion =[
    'xmlTag1', int
    'xmlDateTag2', pd.to_datetime,
    'xmlDateTag3', float
]

for child in childrens:
    record={}
    for tag,func in conversion:
        tagValue=child.find(tag).text
        record[tag]=func(tagValue)
    yield record

df=pd.DataFrame.from_records(records) # Array of records {}
df.dtypes
df.head()

```

# Parquet file
(Parquet,avro,ORC)

Apache Arrow -- Parquet

```python

import pyarrow.parquet as pq
my_table = pq.read_table('mytable.parquet')
df=my_table.to_pandas()
df.dtypes
df.head()

```

# Unstructured Data

pythex.org

```python
import re
match=re.search('RegularExpression',line)
c_value1=match.group(index)
c_value2=match.group(index)
c_value3=match.group(index)
```

# JSON
JavaScript Object Notation

Not Serialiable (Date,Object)
```python

```