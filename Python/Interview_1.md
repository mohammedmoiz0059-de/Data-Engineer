#### List vs Tuple
  A list is mutable and ordered — elements can be added, removed, or changed.    
  A tuple is immutable and ordered — once created, it cannot be modified.    
  In a data pipeline, I'd use a list when the data is dynamic — for example, collecting rows from a GCS file chunk by chunk before loading into BigQuery.    
  I'd use a tuple for fixed config values — like a database column schema ('user_id', 'INT64') or GCP project settings — where I don't want anything accidentally modifying them. Tuples are also slightly faster and memory-efficient, which matters in large pipelines.   

#### Can a tuple contain a list inside it? And if so, can that inner list be modified?
A tuple is immutable in terms of its references, not the contents of those references. So if a tuple holds a mutable object like a list, that inner list can still be changed.   
````python
t = ([1, 2, 3], "hello")

# Can we modify the inner list?
t[0].append(4)

print(t)  # ([1, 2, 3, 4], 'hello')   It changed!    
````

#### Write a Python function that takes a list of sales records (each record is a dictionary) and returns only the records where the amount is greater than 1000. Use list comprehension.
``` python
records = [
    {"id": 1, "region": "North", "amount": 1500},
    {"id": 2, "region": "South", "amount": 800},
    {"id": 3, "region": "East",  "amount": 2000},
    {"id": 4, "region": "West",  "amount": 450},
    {"id": 5, "region": "North", "amount": 1100},
]

def filter_1000(records,threshold=1000):
    filtered_records = [record for record in records if record["amount"] > threshold]
    return filtered_records
print(filter_1000(records))


# Extract region
def get_high_value_regions(records,threshold=1000):
    return [record["region"] for record in records if record['amount'] > threshold]

get_high_value_regions(records)
```
#### Difference between global and local variable??
A global variable is accessible to whole code , whereas local variable is only accessible to the function.
In order to use global variable inside a function "global" keyword is used.

#### You have a list of pipeline job records. Group them by status and count how many jobs are in each status.

```python
jobs = [
    {"job_id": 1, "status": "success"},
    {"job_id": 2, "status": "failed"},
    {"job_id": 3, "status": "success"},
    {"job_id": 4, "status": "running"},
    {"job_id": 5, "status": "failed"},
    {"job_id": 6, "status": "success"},
    {"job_id": 7, "status": "running"},
]

def count_by_status(jobs):
    grouped_status = {}
    for job in jobs :
        if job["status"] in grouped_status :
            grouped_status[job["status"]] += 1
        else:
            grouped_status[job["status"]] = 1
    print(grouped_status)

count_by_status(jobs)
```
#### Same above problem with Libraries
```python 


```
#### You are reading a raw CSV file from GCS. Each row comes in as a messy string. Clean it and extract the fields into a dictionary.
```python
aw_rows = [
    "  101 , John Doe , john.doe@email.com , NEW YORK  ",
    "  102 , Jane Smith , jane@email.com , los angeles  ",
]


def parse_row(raw_row):
    splited = raw_row.split(",")
    parsed = {}
    parsed["id"] = splited[0].strip()
    parsed["name"] = splited[1].strip()
    parsed["email"] = splited[2].strip()
    parsed["city"] = splited[3].strip().title()
    return parsed


for row in raw_rows:
    result = parse_row(row)
    print(result)
```

#### Using List Comp

```python
raw_rows = [
    "  101 , John Doe , john.doe@email.com , NEW YORK  ",
    "  102 , Jane Smith , jane@email.com , los angeles  ",
]

def parse_row(raw_row):
    fields = [f.strip() for f in raw_row.split(",")]
    return {
        "id"    : fields[0],
        "name"  : fields[1],
        "email" : fields[2],
        "city"  : fields[3].title()
    }

all_rows = [parse_row(row) for row in raw_rows]

print(all_rows)
```
