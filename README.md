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
```
