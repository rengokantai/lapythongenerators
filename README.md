### lapythongenerators
####1. Generator Functions and Expressions
#####Build a generator function
create function return even numbers  
old school function way
```
def even(n):
  result =[]
  for i in range(n):
    if i%2==0:
      result.append(i)
  return result
```

generator way
```
def even(n):
  for i in range(n):
    if i%2==0:
      yield i
```

#####Use a generator expression
compare:  
list comprehension
```
ke = [i.upper() for i in coll]
```
generator
```
(i.upper() for i in coll)
```
for the previous lession,
```
def even(n):
  for i in range(n):
    if i%2==0:
      yield i
```
same as
```
even = (n for n in range(10) if n%2==0)
```

For complex generator better to break multiple generator
```
reverse_upper = (i[::-1] for i in (i.upper() for i in coll))
```
can break to
```
upper =  (i.upper() for i in coll)
reverse_upper = (i[::-1] for i in upper)
```
#####Use a generator object
call max on generator
```
max(i for i in range(10))   #9
```
######Fibonacci sequence fenerator
```
def fib(n):
  i =0
  trail,start=0,1
  while True:
    yield start  #start from 1   #initially I wrote yield trail
    trail,start = start,trail+start
```    
call
```
for _ in range(10):
  fib.next()
```
#####Build a generator pipeline
example file
```
def seperate_name(names):
  for full_name in names:
    for name in full_name.split(' '):
      yield name

def get_longest(namelist):
  full_names = (name.strip() for name in open(namelist))
  names = seperate_name(full_names)
  lengths =((name,len(name) for name in names
  return max(langths, key=lambda x:x[1])
```
####2. Using Generators as Context Managers
