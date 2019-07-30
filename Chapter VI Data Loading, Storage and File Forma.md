

```python
#第六章 数据载入、储存及文件格式
###访问数据是第一步，本章重点在于使用pandas进行数据输入与输出。
###输入与输出通常有：读取文本格式文件、数据库载入以及网络资源交互。
```


```python
##一、文本格式数据的读写
##1、csv文件
###将表格型数据读取为DataFrame对象是pandas的重要特性。
```


```python
import pandas as pd
file = r'C:\Users\WS\Desktop\exl.csv'
df = pd.read_csv(file)
df
###首先尝试使用read_csv()将文件读入DataFrame
###这里csv文件要自己创建（创建方式百度），书上例子好像是不太实用的，需要其他知识的投入。
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
      <th>message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>hello</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>world</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9</td>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>foo</td>
    </tr>
  </tbody>
</table>
</div>




```python
import pandas as pd
file = r'C:\Users\WS\Desktop\exl.csv'
df = pd.read_table(file,sep=',')
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
      <th>message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>hello</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>world</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9</td>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>foo</td>
    </tr>
  </tbody>
</table>
</div>




```python
import pandas as pd
file = r'C:\Users\WS\Desktop\exl.csv'
name = ['9','8','7','6','message']
df = pd.read_csv(file,names=name,index_col='message',header=None)
df
###对照上一个输出结果理解参数：
###names指定一个列索引，index_col从列索引指定一个参数成为行索引，header指定行列都为序数标签这里没有生效。
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>9</th>
      <th>8</th>
      <th>7</th>
      <th>6</th>
    </tr>
    <tr>
      <th>message</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>message</th>
      <td>a</td>
      <td>b</td>
      <td>c</td>
      <td>d</td>
    </tr>
    <tr>
      <th>hello</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>world</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
    </tr>
    <tr>
      <th>foo</th>
      <td>9</td>
      <td>10</td>
      <td>11</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
import pandas as pd
file = r'C:\Users\WS\Desktop\ex5.csv'
data = pd.read_csv(file)

file_1 = r'C:\Users\WS\Desktop\ex6.txt'
data.to_csv(file_1)
###使用to_csv()可以将文件保存，这里保存地址、文件名及格式都是自己指定。
```


```python
##2、json文件
obj = """
{"name":"wen",
"lives":["China,chongqing","China,sichuan,chengdu"],
"pet":null,
"friends":[{"name":"ergou","age":18},
{"name":"shan","age":20},
{"name":"wu","age":21}]
}
"""
import json
result = json.loads(obj)
result
###创建一个json文件，loads（）将json字符串转换为python形式（load与loads是不一样的）。
###这里null是空值的意思。
```




    {'name': 'wen',
     'lives': ['China,chongqing', 'China,sichuan,chengdu'],
     'pet': None,
     'friends': [{'name': 'ergou', 'age': 18},
      {'name': 'shan', 'age': 20},
      {'name': 'wu', 'age': 21}]}




```python
obj = """
{"name":"wen",
"lives":["China,chongqing","China,sichuan,chengdu"],
"pet":null,
"friends":[{"name":"ergou","age":18},
{"name":"shan","age":20},
{"name":"wu","age":21}]
}
"""
import json
result = json.loads(obj)
ajson = json.dumps(result)
friend = pd.DataFrame(result["friends"])
friend
###dumps（）将python对象转换为json格式，然后又向DataFrame构造器传入字典的列表。
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ergou</td>
      <td>18</td>
    </tr>
    <tr>
      <th>1</th>
      <td>shan</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>wu</td>
      <td>21</td>
    </tr>
  </tbody>
</table>
</div>




```python
obj = """
[{"a":1,"b":2,"c":3},
{"a":4,"b":5,"c":6},
{"a":7,"b":8,"c":9}]
"""
import json
import pandas as pd
data = pd.read_json(obj)
data
###这里使用read_json()将json文件转换为pandas文件。
###值得注意的是，转换条件就是文件必须能构造为这种列表，否则会报错。
###下面是一个示例。
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
obj = """
{"name":"wen",
"lives":["China,chongqing","China,sichuan,chengdu"],
"pet":null,
"friends":[{"name":"ergou","age":18},
{"name":"shan","age":20},
{"name":"wu","age":21}]
}
"""
import json
import pandas as pd
data = pd.read_json(obj)
data
###valueerror格外醒目，哈哈哈。
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-99-dab7a4a16052> in <module>
         10 import json
         11 import pandas as pd
    ---> 12 data = pd.read_json(obj)
         13 data
    

    c:\users\ws\appdata\local\programs\python\python37\lib\site-packages\pandas\io\json\_json.py in read_json(path_or_buf, orient, typ, dtype, convert_axes, convert_dates, keep_default_dates, numpy, precise_float, date_unit, encoding, lines, chunksize, compression)
        590         return json_reader
        591 
    --> 592     result = json_reader.read()
        593     if should_close:
        594         try:
    

    c:\users\ws\appdata\local\programs\python\python37\lib\site-packages\pandas\io\json\_json.py in read(self)
        715             obj = self._get_object_parser(self._combine_lines(data.split("\n")))
        716         else:
    --> 717             obj = self._get_object_parser(self.data)
        718         self.close()
        719         return obj
    

    c:\users\ws\appdata\local\programs\python\python37\lib\site-packages\pandas\io\json\_json.py in _get_object_parser(self, json)
        737         obj = None
        738         if typ == "frame":
    --> 739             obj = FrameParser(json, **kwargs).parse()
        740 
        741         if typ == "series" or obj is None:
    

    c:\users\ws\appdata\local\programs\python\python37\lib\site-packages\pandas\io\json\_json.py in parse(self)
        847 
        848         else:
    --> 849             self._parse_no_numpy()
        850 
        851         if self.obj is None:
    

    c:\users\ws\appdata\local\programs\python\python37\lib\site-packages\pandas\io\json\_json.py in _parse_no_numpy(self)
       1091         if orient == "columns":
       1092             self.obj = DataFrame(
    -> 1093                 loads(json, precise_float=self.precise_float), dtype=None
       1094             )
       1095         elif orient == "split":
    

    c:\users\ws\appdata\local\programs\python\python37\lib\site-packages\pandas\core\frame.py in __init__(self, data, index, columns, dtype, copy)
        408             )
        409         elif isinstance(data, dict):
    --> 410             mgr = init_dict(data, index, columns, dtype=dtype)
        411         elif isinstance(data, ma.MaskedArray):
        412             import numpy.ma.mrecords as mrecords
    

    c:\users\ws\appdata\local\programs\python\python37\lib\site-packages\pandas\core\internals\construction.py in init_dict(data, index, columns, dtype)
        255             arr if not is_datetime64tz_dtype(arr) else arr.copy() for arr in arrays
        256         ]
    --> 257     return arrays_to_mgr(arrays, data_names, index, columns, dtype=dtype)
        258 
        259 
    

    c:\users\ws\appdata\local\programs\python\python37\lib\site-packages\pandas\core\internals\construction.py in arrays_to_mgr(arrays, arr_names, index, columns, dtype)
         75     # figure out the index, if necessary
         76     if index is None:
    ---> 77         index = extract_index(arrays)
         78     else:
         79         index = ensure_index(index)
    

    c:\users\ws\appdata\local\programs\python\python37\lib\site-packages\pandas\core\internals\construction.py in extract_index(data)
        366             lengths = list(set(raw_lengths))
        367             if len(lengths) > 1:
    --> 368                 raise ValueError("arrays must all be same length")
        369 
        370             if have_dicts:
    

    ValueError: arrays must all be same length



```python
obj = """
[{"a":1,"b":2,"c":3},
{"a":4,"b":5,"c":6},
{"a":7,"b":8,"c":9}]
"""
import json
import pandas as pd
data = pd.read_json(obj)
ad = r'C:\Users\WS\Desktop\ex8.json'
print(data.to_json(ad))
###理同to_csv()，to_json()将pandas文件保存为json文件(这里返回了一个None我也不知道什么意思)。
```

    None
    


```python
##XML和HTML：网络抓取

ex = r'C:\Users\WS\Desktop\ex9.html'
import pandas as pd
tables = pd.read_html(ex)
tables
###这里也是首先要有一个HTML文件，我下载了我们学教务网的一个页面
###然后通过read_html（）将文件输出pandas文件
```




    [                                                   0  \
     0  校外友情链接 ● 国家教育部  ● 四川省教育厅  ● 教育部学信网  ● 学位认证中心  ...   
     1                                                NaN   
     2                                             校外友情链接   
     3              ● 国家教育部  ● 四川省教育厅  ● 教育部学信网  ● 学位认证中心   
     4                                             校内友情链接   
     5                       ● 学生处  ● 招生就业处  ● 人事处  ● 财务处   
     6                                               联系我们   
     7  地址：成都市温江区惠民路211号第一教学楼215室 电话：028-86293029  信箱：...   
     
                                                   1  \
     0                                           NaN   
     1  校外友情链接 ● 国家教育部  ● 四川省教育厅  ● 教育部学信网  ● 学位认证中心   
     2                                           NaN   
     3                                           NaN   
     4                                        校内友情链接   
     5        ● 图书馆  ● 信息与教育技术中心  ● 后勤管理处  ● 后勤服务总公司   
     6                                           NaN   
     7                                           NaN   
     
                                                        2  \
     0                                                NaN   
     1  校内友情链接  ● 学生处  ● 招生就业处  ● 人事处  ● 财务处  ● 图书馆  ●...   
     2                                                NaN   
     3                                                NaN   
     4                                                NaN   
     5                                                NaN   
     6                                                NaN   
     7                                                NaN   
     
                                                        3   4  
     0                                                NaN NaN  
     1  联系我们  地址：成都市温江区惠民路211号第一教学楼215室 电话：028-8629302... NaN  
     2                                                NaN NaN  
     3                                                NaN NaN  
     4                                                NaN NaN  
     5                                                NaN NaN  
     6                                                NaN NaN  
     7                                                NaN NaN  ,
                                                        0  \
     0                                                NaN   
     1                                             校外友情链接   
     2              ● 国家教育部  ● 四川省教育厅  ● 教育部学信网  ● 学位认证中心   
     3                                             校内友情链接   
     4                       ● 学生处  ● 招生就业处  ● 人事处  ● 财务处   
     5                                               联系我们   
     6  地址：成都市温江区惠民路211号第一教学楼215室 电话：028-86293029  信箱：...   
     
                                                   1  \
     0  校外友情链接 ● 国家教育部  ● 四川省教育厅  ● 教育部学信网  ● 学位认证中心   
     1                                           NaN   
     2                                           NaN   
     3                                        校内友情链接   
     4        ● 图书馆  ● 信息与教育技术中心  ● 后勤管理处  ● 后勤服务总公司   
     5                                           NaN   
     6                                           NaN   
     
                                                        2  \
     0  校内友情链接  ● 学生处  ● 招生就业处  ● 人事处  ● 财务处  ● 图书馆  ●...   
     1                                                NaN   
     2                                                NaN   
     3                                                NaN   
     4                                                NaN   
     5                                                NaN   
     6                                                NaN   
     
                                                        3   4  
     0  联系我们  地址：成都市温江区惠民路211号第一教学楼215室 电话：028-8629302... NaN  
     1                                                NaN NaN  
     2                                                NaN NaN  
     3                                                NaN NaN  
     4                                                NaN NaN  
     5                                                NaN NaN  
     6                                                NaN NaN  ,
                                            0
     0                                 校外友情链接
     1  ● 国家教育部  ● 四川省教育厅  ● 教育部学信网  ● 学位认证中心,
                                   0                                       1
     0                        校内友情链接                                  校内友情链接
     1  ● 学生处  ● 招生就业处  ● 人事处  ● 财务处  ● 图书馆  ● 信息与教育技术中心  ● 后勤管理处  ● 后勤服务总公司,
                                                        0
     0                                               联系我们
     1  地址：成都市温江区惠民路211号第一教学楼215室 电话：028-86293029  信箱：...]




```python
ex = r'C:\Users\WS\Desktop\ex9.html'
import pandas as pd
tables = pd.read_html(ex)
###len(tables)
fatures = tables[0]
fatures.head()
###这里我也没懂他的意思，但是照着写是能写出来的（应该是需要涉及HTML的知识，奈何我没学好HTML。。。）。
###另外需要注意的就是pandans对象的输出对数据的匹配要求较高，报错的时候可以检查一下文件值。
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>校外友情链接 ● 国家教育部  ● 四川省教育厅  ● 教育部学信网  ● 学位认证中心  ...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>校外友情链接 ● 国家教育部  ● 四川省教育厅  ● 教育部学信网  ● 学位认证中心</td>
      <td>校内友情链接  ● 学生处  ● 招生就业处  ● 人事处  ● 财务处  ● 图书馆  ●...</td>
      <td>联系我们  地址：成都市温江区惠民路211号第一教学楼215室 电话：028-8629302...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>校外友情链接</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>● 国家教育部  ● 四川省教育厅  ● 教育部学信网  ● 学位认证中心</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>校内友情链接</td>
      <td>校内友情链接</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
###使用lxml.objectify解析XML。
###XML是一种常用的解构花数据格式，它使用元数据支持分层、嵌套数据。
###暂时难以获取XML的文件
```


```python
##二、二进制格式
###使用python的pickle序列化模块进行二进制格式操作是储存数据（也称序列化）的方式之一。
###同时pandas也有一个to_pickle（）可以将数据以pickle格式写入硬盘。

import pandas as pd
file = r'C:\Users\WS\Desktop\exl.csv'
df = pd.read_csv(file)
ad = r'C:\Users\WS\Desktop\frame_pickle'
df.to_pickle(ad)
frame = pd.read_pickle(ad)
frame
###这里直接引用了之前创建的csv文件，通过to_pickle()将其储存在了电脑上，然后又通过read_oickle()将文件读取为了pandas对象。
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
      <th>message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>hello</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>world</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9</td>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>foo</td>
    </tr>
  </tbody>
</table>
</div>




```python
##Web API交互
###这里我跳过了HDF5的内容（因为二进制还搞不懂。。。）
###API交互中requests是一个非常重要的库

import requests
url = 'https://api.github.com/repos/pandas-dev/pandas/issues'
response = requests.get(url)
response
###这里的话基本是一个固定的格式。
###使用get（）函数，传入url，获取response值，返回值一定要是200才代表成功了，否则的话多检查url（之前做爬虫吃过亏，哈哈哈）。
```




    <Response [200]>




```python
import requests
url = 'https://api.github.com/repos/pandas-dev/pandas/issues'
response = requests.get(url)
data = response.json()
issues = pd.DataFrame(data)
issues
###用json（）将文件解析为python对象的json字典，再使用dataframe（）将其转换为pandas对象
###（我的天！这也太美了吧！这个dataframe真的是看了又看，其实之前一直比较抗拒jupyter，现在却被深深折服了！棒！）
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>url</th>
      <th>repository_url</th>
      <th>labels_url</th>
      <th>comments_url</th>
      <th>events_url</th>
      <th>html_url</th>
      <th>id</th>
      <th>node_id</th>
      <th>number</th>
      <th>title</th>
      <th>...</th>
      <th>assignee</th>
      <th>assignees</th>
      <th>milestone</th>
      <th>comments</th>
      <th>created_at</th>
      <th>updated_at</th>
      <th>closed_at</th>
      <th>author_association</th>
      <th>body</th>
      <th>pull_request</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/issues/27654</td>
      <td>474416717</td>
      <td>MDU6SXNzdWU0NzQ0MTY3MTc=</td>
      <td>27654</td>
      <td>BUG: pandas.cut should optionally allow overla...</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>0</td>
      <td>2019-07-30T07:19:40Z</td>
      <td>2019-07-30T07:19:40Z</td>
      <td>None</td>
      <td>NONE</td>
      <td>Due to #23980 the following code now raises a ...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27653</td>
      <td>474339784</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAyMzAyNzE4</td>
      <td>27653</td>
      <td>BUG: Fix dir(interval_index), closes #27571</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>0</td>
      <td>2019-07-30T02:31:56Z</td>
      <td>2019-07-30T03:33:53Z</td>
      <td>None</td>
      <td>MEMBER</td>
      <td>- [x] closes #27571\r\n- [x] tests added / pas...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/issues/27652</td>
      <td>474339308</td>
      <td>MDU6SXNzdWU0NzQzMzkzMDg=</td>
      <td>27652</td>
      <td>API: Meta-issue for making consistent API's to...</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>0</td>
      <td>2019-07-30T02:29:40Z</td>
      <td>2019-07-30T02:29:40Z</td>
      <td>None</td>
      <td>CONTRIBUTOR</td>
      <td>I would like to propose that any pandas API th...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27651</td>
      <td>474292683</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAyMjY1Mzg3</td>
      <td>27651</td>
      <td>improve warnings for Series.{real,imag}</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>0</td>
      <td>2019-07-29T22:57:10Z</td>
      <td>2019-07-29T23:31:39Z</td>
      <td>None</td>
      <td>CONTRIBUTOR</td>
      <td>- [x] closes #27610\r\n- [x] tests added / pas...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27650</td>
      <td>474267830</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAyMjQ1MDI5</td>
      <td>27650</td>
      <td>issue #27642 - timedelta merge asof with toler...</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
      <td>2</td>
      <td>2019-07-29T21:35:20Z</td>
      <td>2019-07-30T07:04:43Z</td>
      <td>None</td>
      <td>NONE</td>
      <td>- [X] closes #27642 \r\n- [ ] tests added / pa...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/issues/27649</td>
      <td>474264934</td>
      <td>MDU6SXNzdWU0NzQyNjQ5MzQ=</td>
      <td>27649</td>
      <td>Add a "scope" document</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>0</td>
      <td>2019-07-29T21:27:50Z</td>
      <td>2019-07-29T21:30:49Z</td>
      <td>None</td>
      <td>CONTRIBUTOR</td>
      <td>e.g. https://numpy.org/neps/scope.html\r\n\r\n...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27646</td>
      <td>474222967</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAyMjA4MDU2</td>
      <td>27646</td>
      <td>TYPING: add some type hints to core.generic</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>0</td>
      <td>2019-07-29T19:42:47Z</td>
      <td>2019-07-29T19:42:47Z</td>
      <td>None</td>
      <td>MEMBER</td>
      <td>pre-cursor to #27527</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27645</td>
      <td>474219196</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAyMjA0OTYw</td>
      <td>27645</td>
      <td>BUG: Add mapping for pyqt for successful packa...</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>0</td>
      <td>2019-07-29T19:32:54Z</td>
      <td>2019-07-30T02:28:22Z</td>
      <td>None</td>
      <td>CONTRIBUTOR</td>
      <td>- [ ] closes #26838 \r\n- [ ] tests added / pa...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27644</td>
      <td>474208770</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAyMTk2NjE4</td>
      <td>27644</td>
      <td>Add Pandas-Bokeh to pandas ecosystem page</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>0</td>
      <td>2019-07-29T19:07:27Z</td>
      <td>2019-07-29T19:07:27Z</td>
      <td>None</td>
      <td>NONE</td>
      <td>This PR adds Pandas-Bokeh reference to Pandas ...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/issues/27642</td>
      <td>474183308</td>
      <td>MDU6SXNzdWU0NzQxODMzMDg=</td>
      <td>27642</td>
      <td>merge_asof(): cannot use tolerance flag when t...</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>4</td>
      <td>2019-07-29T18:03:54Z</td>
      <td>2019-07-29T19:16:25Z</td>
      <td>None</td>
      <td>NONE</td>
      <td>#### Code Sample\r\n\r\n```python\r\nimport pa...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27640</td>
      <td>474155847</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAyMTU0MDI1</td>
      <td>27640</td>
      <td>Backport PR #27631 on branch 0.25.x (BUG: rais...</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
      <td>0</td>
      <td>2019-07-29T16:56:15Z</td>
      <td>2019-07-29T16:56:16Z</td>
      <td>None</td>
      <td>NONE</td>
      <td>Backport PR #27631: BUG: raise when wrong leve...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/issues/27639</td>
      <td>474096038</td>
      <td>MDU6SXNzdWU0NzQwOTYwMzg=</td>
      <td>27639</td>
      <td>Max recursion limit on pd.eval</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>0</td>
      <td>2019-07-29T14:50:29Z</td>
      <td>2019-07-29T14:50:29Z</td>
      <td>None</td>
      <td>NONE</td>
      <td>#### Code Sample\r\n\r\nAfter some hypothesis ...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/issues/27637</td>
      <td>473993909</td>
      <td>MDU6SXNzdWU0NzM5OTM5MDk=</td>
      <td>27637</td>
      <td>Add comment char parameter to to_csv method</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>2</td>
      <td>2019-07-29T11:17:50Z</td>
      <td>2019-07-29T17:08:39Z</td>
      <td>None</td>
      <td>NONE</td>
      <td>#### Code Sample\r\n```\r\nimport pandas as pd...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/issues/27636</td>
      <td>473930501</td>
      <td>MDU6SXNzdWU0NzM5MzA1MDE=</td>
      <td>27636</td>
      <td>Operators between DataFrame and Series fail on...</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>2</td>
      <td>2019-07-29T08:54:57Z</td>
      <td>2019-07-30T01:48:48Z</td>
      <td>None</td>
      <td>NONE</td>
      <td>#### Code Sample\r\n\r\n```python\r\nimport pa...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/issues/27634</td>
      <td>473897551</td>
      <td>MDU6SXNzdWU0NzM4OTc1NTE=</td>
      <td>27634</td>
      <td>pandas.ExcelWriter has abstract methods</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>3</td>
      <td>2019-07-29T07:37:42Z</td>
      <td>2019-07-29T14:57:51Z</td>
      <td>None</td>
      <td>NONE</td>
      <td>#### Code Sample, a copy-pastable example if p...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27633</td>
      <td>473823816</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAxODg3Mzcx</td>
      <td>27633</td>
      <td>EA: implement+test EA.view</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>1</td>
      <td>2019-07-29T02:44:22Z</td>
      <td>2019-07-29T19:16:06Z</td>
      <td>None</td>
      <td>MEMBER</td>
      <td>Broken off from #27142, plus some type annotat...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27630</td>
      <td>473731294</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAxODIyMzg2</td>
      <td>27630</td>
      <td>Validate docstring directives</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>1</td>
      <td>2019-07-28T10:58:57Z</td>
      <td>2019-07-29T05:30:29Z</td>
      <td>None</td>
      <td>CONTRIBUTOR</td>
      <td>- [X] closes #27629\r\n- [ ] tests added / pas...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/issues/27629</td>
      <td>473731146</td>
      <td>MDU6SXNzdWU0NzM3MzExNDY=</td>
      <td>27629</td>
      <td>DOC: Validate reST directives in docstrings</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>0</td>
      <td>2019-07-28T10:57:02Z</td>
      <td>2019-07-29T15:56:57Z</td>
      <td>None</td>
      <td>CONTRIBUTOR</td>
      <td>#### Code Sample, a copy-pastable example if p...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>18</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27628</td>
      <td>473693489</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAxNzk2NDY0</td>
      <td>27628</td>
      <td>Make interpolate_2d handle datetime64 correctly</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>2</td>
      <td>2019-07-28T01:11:51Z</td>
      <td>2019-07-29T19:04:33Z</td>
      <td>None</td>
      <td>MEMBER</td>
      <td>Broken off from #27626 because I decided that ...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27627</td>
      <td>473693256</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAxNzk2Mjkz</td>
      <td>27627</td>
      <td>CLN: de-kludge Block.quantile</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>2</td>
      <td>2019-07-28T01:07:25Z</td>
      <td>2019-07-29T21:20:19Z</td>
      <td>None</td>
      <td>MEMBER</td>
      <td>Broken off from #27626 since I decided that is...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27625</td>
      <td>473670899</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAxNzgwODQz</td>
      <td>27625</td>
      <td>remove undesired values kwarg</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>0</td>
      <td>2019-07-27T19:38:45Z</td>
      <td>2019-07-29T18:19:01Z</td>
      <td>None</td>
      <td>MEMBER</td>
      <td>- [ ] closes #xxxx\r\n- [ ] tests added / pass...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27624</td>
      <td>473632641</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAxNzU1NDM3</td>
      <td>27624</td>
      <td>BUG: cells are missing in the excel file when ...</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>1</td>
      <td>2019-07-27T12:15:59Z</td>
      <td>2019-07-30T01:18:54Z</td>
      <td>None</td>
      <td>NONE</td>
      <td>- [x] closes #15392\r\n- [ ] tests added / pas...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>22</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27623</td>
      <td>473627597</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAxNzUxOTY1</td>
      <td>27623</td>
      <td>Fix AttributeError in scripts/validate_docstri...</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>5</td>
      <td>2019-07-27T11:06:45Z</td>
      <td>2019-07-28T06:30:01Z</td>
      <td>None</td>
      <td>CONTRIBUTOR</td>
      <td>- [X] closes #27622\r\n- [ ] tests added / pas...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/issues/27622</td>
      <td>473627272</td>
      <td>MDU6SXNzdWU0NzM2MjcyNzI=</td>
      <td>27622</td>
      <td>BUG: AttributeError in scripts/validate_docstr...</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>0</td>
      <td>2019-07-27T11:02:26Z</td>
      <td>2019-07-27T14:21:05Z</td>
      <td>None</td>
      <td>CONTRIBUTOR</td>
      <td>#### Code Sample, a copy-pastable example if p...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>24</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27620</td>
      <td>473585891</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAxNzI0ODU2</td>
      <td>27620</td>
      <td>DEPR: remove ix</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
      <td>2</td>
      <td>2019-07-27T01:45:51Z</td>
      <td>2019-07-29T13:56:06Z</td>
      <td>None</td>
      <td>MEMBER</td>
      <td>- [ ] Needs release note\r\n- [ ] Needs geopan...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27618</td>
      <td>473570458</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAxNzEzNTg5</td>
      <td>27618</td>
      <td>Remove Encoding of values in char** For Labels</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>7</td>
      <td>2019-07-26T23:35:30Z</td>
      <td>2019-07-27T03:52:04Z</td>
      <td>None</td>
      <td>MEMBER</td>
      <td>In reviewing this module there is a shared fun...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>26</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27617</td>
      <td>473560779</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAxNzA1NjYx</td>
      <td>27617</td>
      <td>DEPR: Deprecate NDFrame.filter</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>0</td>
      <td>2019-07-26T22:43:26Z</td>
      <td>2019-07-27T14:18:28Z</td>
      <td>None</td>
      <td>CONTRIBUTOR</td>
      <td>- [ ] xref #26642\r\n- [x] tests added / passe...</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>27</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/issues/27616</td>
      <td>473549993</td>
      <td>MDU6SXNzdWU0NzM1NDk5OTM=</td>
      <td>27616</td>
      <td>to_dict() on a boolean series sometimes return...</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>6</td>
      <td>2019-07-26T21:55:33Z</td>
      <td>2019-07-28T20:30:43Z</td>
      <td>None</td>
      <td>NONE</td>
      <td>#### Problem description\r\n\r\nI construct a ...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>28</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/pull/27615</td>
      <td>473455400</td>
      <td>MDExOlB1bGxSZXF1ZXN0MzAxNjE5NDAx</td>
      <td>27615</td>
      <td>Move json_normalize to pd namespace</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>9</td>
      <td>2019-07-26T17:12:09Z</td>
      <td>2019-07-29T15:04:05Z</td>
      <td>None</td>
      <td>NONE</td>
      <td>- Added a whatsnew entry\r\n- Imported pandas....</td>
      <td>{'url': 'https://api.github.com/repos/pandas-d...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://api.github.com/repos/pandas-dev/pandas...</td>
      <td>https://github.com/pandas-dev/pandas/issues/27614</td>
      <td>473454626</td>
      <td>MDU6SXNzdWU0NzM0NTQ2MjY=</td>
      <td>27614</td>
      <td>GroupBy(axis=1) Does Not Offer Implicit Select...</td>
      <td>...</td>
      <td>None</td>
      <td>[]</td>
      <td>None</td>
      <td>5</td>
      <td>2019-07-26T17:09:54Z</td>
      <td>2019-07-27T10:04:36Z</td>
      <td>None</td>
      <td>CONTRIBUTOR</td>
      <td>#### Code Sample, a copy-pastable example if p...</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>30 rows × 24 columns</p>
</div>




```python
###与数据库的交互
###使用python内建库sqlite3驱动生成SQLite数据库

# import sqlite3
# query = """
# create table test
# (a varchar(20),b varchar(20),
# c real,
# d integer)"""
# con = sqlite3.connect('mydaata.sqlite')
con.execute(query)
###我完全是照着代码瞎敲的，不能理解这个逻辑过程（还没上过数据库的内容），但是居然能运行。
```




    <sqlite3.Cursor at 0x2c167580490>




```python
import sqlite3
query = """
create table test
(a varchar(20),b varchar(20),
c real,
d integer)"""
con = sqlite3.connect('mydaata.sqlite')
data = [('Atlanta', 'Georgia', 1.25, 6),
('Tallahassee', 'Florida', 2.6, 3),
('Sacramento', 'California', 1.7, 5)]
stmt = "insert into test values(?,?,?,?)"
con.executemany(stmt,data)
con.commit()

###这个照着敲的，本来第一次是可以了的，但是后面就运行不了了，但介于我数据库的缺乏我决定不管了（嘻嘻）。
```


    ---------------------------------------------------------------------------

    OperationalError                          Traceback (most recent call last)

    <ipython-input-141-8cbb4224f96b> in <module>
         10 ('Sacramento', 'California', 1.7, 5)]
         11 stmt = "insert into test values(?,?,?,?)"
    ---> 12 con.executemany(stmt,data)
         13 con.commit()
         14 
    

    OperationalError: database is locked



```python
###这样的话，数据载入这一章节就算完了，中间有一些我跳过了，多半是我操作不了且认为无关紧要的内容
```
