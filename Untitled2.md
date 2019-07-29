

```python
states = [' alabama','geregial','south','tanshiyu iloveyou#%%$','funy']
```


```python
import re
def clean_strings(strings):
    result = []
    for value in strings:
        value = value.strip()
        value = re.sub('[!#%$?]','',value)
        value = value.title()
        result.append(value)
    return result
```


```python
clean_strings(states)
```




    ['Alabama', 'Geregial', 'South', 'Tanshiyu Iloveyou', 'Funy']




```python
def short_function(x):
    return x * 2
equiv_anon = lambda x:x * 2
```


```python
def apply_to_list(some_list,f):
    return [f(x) for x in some_list]
ints = [1,3,5,6]
print(apply_to_list(ints,lambda x:x * 2))
```

    [2, 6, 10, 12]
    


```python
strings = ['tan','shi','yu','wo','xi','huan','ni']
strings.sort(key=lambda x:len(set(list(x))))
strings
```




    ['yu', 'wo', 'xi', 'ni', 'tan', 'shi', 'huan']




```python
some_dict = {'a':1,'b':2,'c':3}
for key in some_dict:
    print(key)
```

    a
    b
    c
    


```python
dict_iterator = iter(some_dict)
dict_iterator
```




    <dict_keyiterator at 0x2768c1b9c78>




```python
list(dict_iterator)
```




    ['a', 'b', 'c']




```python
some_list = [1,2,45,6,7,8,]
list_iterator = iter(some_list)
set(list_iterator)
```




    {1, 2, 6, 7, 8, 45}




```python
def squares(n=10):
    print('Generating squares from 1 to{0}'.format(n ** 2))
    for i in range(1,n + 1):
          yield i ** 2
```


```python
gen = squares()
gen
```




    <generator object squares at 0x000002768C26B840>




```python
for x in gen:
    print(x,end='')
```

    Generating squares from 1 to100
    149162536496481100


```python
import itertools
first_letter = lambda x:x[0]
names = ['tan','shi','yu','tong','xue']
for letter,names in itertools.groupby(names,first_letter):
    print(letter,list(names))
```

    t ['tan']
    s ['shi']
    y ['yu']
    t ['tong']
    x ['xue']
    


```python
from itertools import groupby
test = [(1,5),(1,4),(1,3),(1,2),(2,4),(2,3),(2,4)]
temp = groupby(test,key=lambda x:x[0])
for a,b in temp:
    print(a,list(b))
```

    1 [(1, 5), (1, 4), (1, 3), (1, 2)]
    2 [(2, 4), (2, 3), (2, 4)]
    


