


# enumerator

```python
[print(index,val) for index,val in  enumerate(range(5))]
{index:val for index,val in enumerate(range(5))}
```
# tupple, set and list


```python
tup1=("abc","def","fgh") # Immutable
arryOrList=["abc","def","fgh"] # mutable and not Hashable
# only tuple can be keys in Dict or elements in set
set2={"abc","def","fgh"} # mutable and harshable
#Adding List to set
set2.add(tuple(["x","y","z"]))

set2.add(tuple(sorted(["x","y","z"])))

set1={val for val in range(5)}

list1=[val for val in range(5)]
list2=("abc","de","fgh")
list2.sort(key=lambda x:len(x),reverse=True)
```


# Import classes

```python
from collections import deque

import heapq
# heappush heappop heapify
```