

```python
##本章主要涉及Python内建数据操作工具的拔高，他们与pandas和numpy协同处理数据。
##主要包括元组、列表、字典和集合，以及创建可复用函数
```


```python
#3、数据结构和序列
##3.1.1、元组
###元组是一种固定长度、不可变的python对象序列，以逗号分隔序列值。
###元组函数为tuple()
```


```python
tup_1 = 1,2,3,4,5
tup_2 = (1,2,3),(4,5,6)
print(tup_1,tup_2)
```

    (1, 2, 3, 4, 5) ((1, 2, 3), (4, 5, 6))
    


```python
##元组拆包
###可以运用于任何迭代类型，要求就是数量对应
```


```python
tup = (1,2,3)
a,b,c = tup
c
```




    3




```python
tup = (1,2,3,(4,5,6))
a,b,c,(d,e,f) = tup
e
```




    5




```python
seq = [(1,2,3),(4,5,6),(7,8,9)]
for a,b,c in seq:
    print('a={0},b={1},c={2}'.format(a,b,c))
```

    a=1,b=2,c=3
    a=4,b=5,c=6
    a=7,b=8,c=9
    


```python
##3.1.2、列表
###[]或者list()定义列表
###list()在数据处理中常用于将迭代器或生成器转换为列表。
```


```python
###如果已经定义了一个列表，使用extend()向该列表添加多个元素
everything = [10]
lists = str(range)
for i in lists:
    everything.extend(i)
everything
```




    [10, '<', 'c', 'l', 'a', 's', 's', ' ', "'", 'r', 'a', 'n', 'g', 'e', "'", '>']




```python
##3.1.3内建序列函数
```


```python
###1、enumerate()
###遍历序列时追踪元素的索引——构造字典
```


```python
some_list = ['foo','bar','baz']
mopping = {}
for i,v in enumerate(some_list):
    mopping[v] = i
mopping
```




    {'foo': 0, 'bar': 1, 'baz': 2}




```python
###zip()
###将列表、元组等序列的元素配对，新建一个元组构成的列表
###多用于同时遍历多个序列
```


```python
seq_1 = ['foo','bar','baz']
seq_2 = ['one','tow','three']
zipped = zip(seq_1,seq_2)
list(zipped)
```




    [('foo', 'one'), ('bar', 'tow'), ('baz', 'three')]




```python
seq_1 = ['foo','bar','baz']
seq_2 = ['one','tow','three']
for i,(a,b) in enumerate(zip(seq_1,seq_2)):
    print('{0}:{1},{2}'.format(i,a,b))
```

    0:foo,one
    1:bar,tow
    2:baz,three
    


```python
###3、reversed()将序列元素倒序排列
###reversed是一个生成器
```


```python
##3.1.4、字典（dict）
###又名哈希表或关联数组
```


```python
###使用update()将两个字典合并
```


```python
dict_1 = {'a':1,'b':2}
dict_2 = {'c':3,'d':4}
dict_1.update(dict_2)
dict_1
```




    {'a': 1, 'b': 2, 'c': 3, 'd': 4}




```python
key_list = ['a','b','c']
value_list = range(3)
mapping = {}
for k,v in zip(key_list,value_list):
    mapping[k] = v
mapping
```




    {'a': 0, 'b': 1, 'c': 2}




```python
##3.1.5、集合
###类似字典，但只有键没有值
###使用set()或字面集与大括号的语法创建
###数学上集合的操作都可以完成
```


```python
set([1,2,3,4,3,1])
```




    {1, 2, 3, 4}




```python
##3.1.6、列表、集合和字典的推导式
###他允许过滤一个容器的元素，同一种简明的表达式传递给过滤器的元素，从而生成一个新的列表
```


```python
###1.列表推导式：
###list_mapping = [for value in collection if condition]  
###即：
result = []
for i in collection:
    if condition:
        result.append(expr)
```


```python
strings = ['a','as','bat','car','dove','python']
###遍历列表，如果长度大于二，就将其大写
new = [x.upper() for x in strings if len(x) > 2]
new
```




    ['BAT', 'CAR', 'DOVE', 'PYTHON']




```python
###2.字典推导式：
###dict_mapping = {key_expr:value_eapr for value in collection if condition }
loc_mapping = {val:index for index,val in enumerate(strings)}
loc_mapping
```




    {'a': 0, 'as': 1, 'bat': 2, 'car': 3, 'dove': 4, 'python': 5}




```python
###3.集合推导式：
###set_comp = {expr for value in collection if condition}
```


```python
unique_lengths = {len(x) for x in strings}
unique_lengths
```




    {1, 2, 3, 4, 6}




```python
###上述其实讲的是，在一个迭代中对元素进行某种运算的格式
```


```python
###map()将更加函数化、简洁化的进行表达
###它接收一个函数 f 和一个 list，并通过把函数 f 依次作用在 list 的每个元素上，得到一个新的 list 并返回。
```


```python
set(map(len,strings))
```




    [1, 2, 3, 3, 4, 6]




```python
list(map(len,strings))
```




    [1, 2, 3, 3, 4, 6]




```python
###4.嵌套列表推导式：
###假设有一个包含列表的列表
```


```python
###想要得到文件中有两个或以上e的数据
all_data = [['john','emily','michael','mary','steven'],
            ['maria','juan','javier','natalia','pilar','eee']]
names_of_interest = []
for names in all_data:
    enough_es = [name for name in names if name.count('e') >= 2 ]
    names_of_interest.extend(enough_es)
names_of_interest
```




    ['steven', 'eee']




```python
###这里使用嵌套列表表达式，等价于上述方法
###在all_data中取出names，再在names中取出符合name，最后输出name
result = [name for names in all_data for name in names if name.count('e') >= 2]
result
```




    ['steven', 'eee']




```python
some_tuples = [(1,2,3),(4,5,6),(7,8,9)]
re_1 = [x for a in some_tuples for x in a ]
re_1
```




    [1, 2, 3, 4, 5, 6, 7, 8, 9]




```python
###以上就是一些Python数据结构基础内容的拔高，出于为后面数据处理的学习铺垫而编写。
```
