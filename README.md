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
  next(fib)
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
#####The @contextmanager decorator
ex
```
form contextlib import contextmanager

@contextmanager  #must have this line to call __exit__
def simple_manager(obj):
  try:
    obj.prop+=1
    yield
  finally:
    obj.prop-=1

class K(object):
  def __init__(self,arg):
    self.prop=arg
```

tests:
```
obj=K(1)
obj.prop  #1
```
call contextmanager:
```
with simple_manager(obj):
  print (obj.prop) #2

obj.prop #1
```

#####Use the yielded value in contextmanager(not intuitive, needs memorize)
```
@contextmanager
def create_file(name):
  try:
    logname=name
    f=open(logname,'w')
    f.write('a')
    yield f
  finally:
    f.write('c')
    f.close()
```
call:
```
with create_file('filename.txt') as file:
  file.write('b')
```
then
```
cat filename.txt  #a b c 
```
####3. Coroutines
#####Coroutine overview
coroutines: 
- receive values. 
- may not return anything. 
- not for iteration  
- repeatedly receives input
- precess input
- stops at yield statement  

In coroutine, the yield statement is used to capture the value of whatever is passed to the send method.  
In the case of coroutines, the yield statement is not only in charge of pausing the flow, but also capturing values.  

#####Create a coroutine
```
def co():
  while True:
    x=yield
    print(x)
```
call
```
c = co()
next(c)
c.send(1)
```

ex2
```
def conuter(s):
  count=0
  try:
    while True:
      item=yield
      if instance(item,str):
        if item in s:
          count+=1
          print(item)
        else:
          pass
      else:
        print("not a string")
  except GeneratorExit:
    print (count)
```
test
```
c =counter('abc')
next(c)
c.send('a')
c.send('d')
```
