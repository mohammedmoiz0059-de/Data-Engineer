## Collections 
It is high frequency module.

#### Counter -  To count Occurrences
``` python
from collections import Counter
statuses = ["success", "failed", "success", "running", "success", "failed"]

c = Counter(statuses)
print(c)
#Most Common 2
print(c.most_common(2))
```

#### Defaultdict - Dictionary with Default value

```python
from collections import defaultdict
# Group job_ids by status
jobs = [
    {"job_id": 1, "status": "success"},
    {"job_id": 2, "status": "failed"},
    {"job_id": 3, "status": "success"},
]
grouped = defaultdict(list)  # default value is empty list

for job in jobs:
    grouped[job["status"]].append(job["job_id"])

print(dict(grouped))
# {'success': [1, 3], 'failed': [2]}
```

#### OrderedDict - Dictionary that remembers insertion Order
```python
from collections import OrderedDict

# In modern Python 3.7+ regular dicts maintain order too
# But OrderedDict has one special power:

d1 = OrderedDict([("a", 1), ("b", 2)])
d2 = OrderedDict([("b", 2), ("a", 1)])

print(d1 == d2)  # False — order matters in OrderedDict
```

#### Deque - Fast Queue for streaming data

``` python
from collections import deque

# Regular list — slow for adding/removing from left
# deque — very fast from both ends

buffer = deque(maxlen=3)  # sliding window of size 3

buffer.append(100)
buffer.append(200)
buffer.append(300)
print(buffer)  # deque([100, 200, 300], maxlen=3)

buffer.append(400)  # 100 gets dropped automatically!
print(buffer)  # deque([200, 300, 400], maxlen=3)

```
