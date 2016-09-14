### lapythongenerators
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
