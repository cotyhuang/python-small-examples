### Python 小例子

告别枯燥，60秒学会一个Python小例子。Python基础、Web开发、数据科学、机器学习的精简小例子都在这里。

#### 欢迎贡献

比如github账号为`lhxon`的小伙伴，fork此库后，按照如下步骤提交到此库：

```markdown
1. git clone https://github.com/lhxon/python-small-examples
2. git add . 
3. git commit -m "xiugai"
4. git push
5. 界面点击：pull requests，根据操作即可。如遇问题，欢迎联系我。
```
#### 基本操作

1. 环境搭建基本概念
pycharm，python解释器，conda安装，pip安装，详情点击：[Python新手环境搭建时容易混淆的概念](Python新手环境搭建时容易混淆的概念.md)
2. 修改为国内镜像 
[conda国内镜像修改(最新版)](conda国内镜像修改(最新版).md)
3. 链式比较
```python
i = 3
print(1 < i < 3)  # False
print(1 < i <= 3)  # True
```
4. 不用else和if实现计算器
```python
from operator import *

def calculator(a, b, k):
    return {
        '+': add,
        '-': sub,
        '*': mul,
        '/': truediv,
        '**': pow
    }[k](a, b)

calculator(1, 2, '+')  # 3
calculator(3, 4, '**')  # 81
```
5. 函数链
```python
from operator import (add, sub)

def add_or_sub(a, b, oper):
    return (add if oper == '+' else sub)(a, b)

add_or_sub(1, 2, '-')  # -1
```
6. 求字符串的字节长度
```python
def str_byte_len(mystr):
    return (len(mystr.encode('utf-8')))

str_byte_len('i love python')  # 13(个字节)
str_byte_len('字符')  # 6(个字节)
```
7. 寻找第n次出现位置
```python
def search_n(s, c, n):
    size = 0
    for i, x in enumerate(s):
        if x == c:
            size += 1
        if size == n:
            return i
    return -1

print(search_n("fdasadfadf", "a", 3))# 结果为7，正确
print(search_n("fdasadfadf", "a", 30))# 结果为-1，正确
```
8. 去掉最高最低求平均
```python
def score_mean(lst):
    lst.sort()
    lst2=lst[1:(len(lst)-1)]
    return round((sum(lst2)/len(lst2)),2)

score_mean([9.1, 9.0,8.1, 9.7, 19,8.2, 8.6,9.8]) # 9.07
```
9.  交换元素
```python
def swap(a, b):
    return b, a

swap(1, 0)  # (0,1)
```

#### 基础算法

1. 二分搜索
```python
def binarySearch(arr, left, right, x):
    while left <= right:
        mid = int(left + (right - left) / 2); # 找到中间位置。求中点写成(left+right)/2更容易溢出，所以不建议这样写

        # 检查x是否出现在位置mid
        if arr[mid] == x:
            print('found %d 在索引位置%d 处' %(x,mid))
            return mid

            # 假如x更大，则不可能出现在左半部分
        elif arr[mid] < x:
            left = mid + 1 #搜索区间变为[mid+1,right]
            print('区间缩小为[%d,%d]' %(mid+1,right))

        elif x<arr[mid]:
            right = mid - 1 #搜索区间变为[left,mid-1]
            print('区间缩小为[%d,%d]' %(left,mid-1))

    return -1
```
更多细节查看：[二分搜索](二分搜索.md)

2. [距离矩阵](距离矩阵.md)
```python
x,y = mgrid[0:5,0:5]
list(map(lambda xe,ye: [(ex,ey) for ex, ey in zip(xe, ye)], x,y))
[[(0, 0), (0, 1), (0, 2), (0, 3), (0, 4)],
 [(1, 0), (1, 1), (1, 2), (1, 3), (1, 4)],
 [(2, 0), (2, 1), (2, 2), (2, 3), (2, 4)],
 [(3, 0), (3, 1), (3, 2), (3, 3), (3, 4)],
 [(4, 0), (4, 1), (4, 2), (4, 3), (4, 4)]]
```

#### 列表

1. [打印乘法表](打印乘法表.md)
```python
for i in range(1,10):
    for j in range(1,i+1):
        print('{0}*{1}={2}'.format(j,i,j*i),end="\t")
    print()
```
结果：
```markdown
1*1=1
1*2=2   2*2=4
1*3=3   2*3=6   3*3=9
1*4=4   2*4=8   3*4=12  4*4=16
1*5=5   2*5=10  3*5=15  4*5=20  5*5=25
1*6=6   2*6=12  3*6=18  4*6=24  5*6=30  6*6=36
1*7=7   2*7=14  3*7=21  4*7=28  5*7=35  6*7=42  7*7=49
1*8=8   2*8=16  3*8=24  4*8=32  5*8=40  6*8=48  7*8=56  8*8=64
1*9=9   2*9=18  3*9=27  4*9=36  5*9=45  6*9=54  7*9=63  8*9=72  9*9=81
```
2. [嵌套数组完全展开](嵌套数组完全展开.md)
```python
from collections.abc import *

def flatten(input_arr, output_arr=None):
    if output_arr is None:
        output_arr = []
    for ele in input_arr:
        if isinstance(ele, Iterable): # 判断ele是否可迭代
            flatten(ele, output_arr)  # 尾数递归
        else:
            output_arr.append(ele)    # 产生结果
    return output_arr

flatten([[1,2,3],[4,5]], [6,7]) # [6, 7, 1, 2, 3, 4, 5]
```
3. [将list等分为子组](./将list等分为子组.md)
```python
from math import ceil

def divide(lst, size):
    if size <= 0:
        return [lst]
    return [lst[i * size:(i+1)*size] for i in range(0, ceil(len(lst) / size))]

r = divide([1, 3, 5, 7, 9], 2) # [[1, 3], [5, 7], [9]]
```
4. [生成fibonacci序列前n项](生成fibonacci序列前n项.md)
```python
def fibonacci(n):
    if n <= 1:
        return [1]
    fib = [1, 1]
    while len(fib) < n:
        fib.append(fib[len(fib) - 1] + fib[len(fib) - 2])
    return fib

fibonacci(5)  # [1, 1, 2, 3, 5]
```
5. [过滤掉各种空值](过滤掉list中的各种空值.md)
```python
def filter_false(lst):
    return list(filter(bool, lst))

filter_false([None, 0, False, '', [], 'ok', [1, 2]])# ['ok', [1, 2]]
```
6. [返回列表头元素](返回列表头元素.md)
```python
def head(lst):
    return lst[0] if len(lst) > 0 else None

head([])  # None
head([3, 4, 1])  # 3
```
7. [返回列表尾元素](返回列表尾元素.md)
```python
def tail(lst):
    return lst[-1] if len(lst) > 0 else None
    
print(tail([]))  # None
print(tail([3, 4, 1]))  # 1
```
8. [对象转换为可迭代类型](./对象转换为可迭代类型.md)
```python
from collections.abc import Iterable

def cast_iterable(val):
    return val if isinstance(val, Iterable) else [val]

cast_iterable('foo')# foo
cast_iterable(12)# [12]
cast_iterable({'foo': 12})# {'foo': 12}
```
9. [求更长列表](求更长列表.md)
```python
def max_length(*lst):
    return max(*lst, key=lambda v: len(v))

r = max_length([1, 2, 3], [4, 5, 6, 7], [8])# [4, 5, 6, 7]
```
10. [出现最多元素](统计出现次数最多的元素.md)
```python
def max_frequency(lst):
    return max(lst, default='列表为空', key=lambda v: lst.count(v))

lst = [1, 3, 3, 2, 1, 1, 2]
max_frequency(lst) # 1 
```
11. [求多个列表的最大值](求多个列表的最大值.md)
```python
def max_lists(*lst):
    return max(max(*lst, key=lambda v: max(v)))

max_lists([1, 2, 3], [6, 7, 8], [4, 5]) # 8
```
12. [求多个列表的最小值](求多个列表的最小值.md)
```python
def min_lists(*lst):
    return min(min(*lst, key=lambda v: max(v)))

min_lists([1, 2, 3], [6, 7, 8], [4, 5]) # 1
```
13. [检查list是否有重复元素](检查list是否有重复元素.md)
```python
def has_duplicates(lst):
    return len(lst) == len(set(lst))

x = [1, 1, 2, 2, 3, 2, 3, 4, 5, 6]
y = [1, 2, 3, 4, 5]
has_duplicates(x)  # False
has_duplicates(y)  # True
```
14. [求列表中所有重复元素](求列表中所有重复元素.md)
```python
from collections import Counter

def find_all_duplicates(lst):
    c = Counter(lst)
    return list(filter(lambda k: c[k] > 1, c))

find_all_duplicates([1, 2, 2, 3, 3, 3])  # [2,3]
```
16. [列表反转](列表反转.md)
```python
def reverse(lst):
    return lst[::-1]

reverse([1, -2, 3, 4, 1, 2])# [2, 1, 4, 3, -2, 1]
```
18. [浮点数等差数列](浮点数等差数列.md)
```python
def rang(start, stop, n):
    start,stop,n = float('%.2f' % start), float('%.2f' % stop),int('%.d' % n)
    step = (stop-start)/n
    lst = [start]
    while n > 0:
        start,n = start+step,n-1
        lst.append(round((start), 2))
    return lst

rang(1, 8, 10) # [1.0, 1.7, 2.4, 3.1, 3.8, 4.5, 5.2, 5.9, 6.6, 7.3, 8.0]
```

#### 字典

1. [字典值最大的键值对列表](返回字典值最大的键值对列表.md)
```python
def max_pairs(dic):
    if len(dic) == 0:
        return dic
    max_val = max(map(lambda v: v[1], dic.items()))
    return [item for item in dic.items() if item[1] == max_val]

max_pairs({'a': -10, 'b': 5, 'c': 3, 'd': 5})# [('b', 5), ('d', 5)]
```
2. [字典值最小的键值对列表](返回字典值最小的键值对列表.md)
```python
def min_pairs(dic):
    if len(dic) == 0:
        return []
    min_val = min(map(lambda v: v[1], dic.items()))
    return [item for item in dic.items() if item[1] == min_val]


min_pairs({}) # []

r = min_pairs({'a': -10, 'b': 5, 'c': 3, 'd': 5})
print(r)  # [('b', 5), ('d', 5)]
```
3. [合并两个字典](合并两个字典.md)
```python
def merge_dict2(dic1, dic2):
    return {**dic1, **dic2}  # python3.5后支持的一行代码实现合并字典

merge_dict({'a': 1, 'b': 2}, {'c': 3})  # {'a': 1, 'b': 2, 'c': 3}
```
4. [求字典前n个最大值](求字典前n个最大值.md)
```python
from heapq import nlargest

# 返回字典d前n个最大值对应的键
def topn_dict(d, n):
    return nlargest(n, d, key=lambda k: d[k])

topn_dict({'a': 10, 'b': 8, 'c': 9, 'd': 10}, 3)  # ['a', 'd', 'c']
```
5. [求最小键值对](求最小键值对.md)
```python
d={'a':-10,'b':5, 'c':3,'d':5}
min(d.items(),key=lambda x:x[1]) #('a', -10)
```

#### 集合

1. [互为变位词](是否相同字母但顺序不同.md)
```python
from collections import Counter
# 检查两个字符串是否 相同字母异序词，简称：互为变位词
def anagram(str1, str2):
    return Counter(str1) == Counter(str2)

anagram('eleven+two', 'twelve+one')  # True 这是一对神器的变位词
anagram('eleven', 'twelve')  # False
```

#### 文件操作

1. [批量修改后缀名](./批量修改后缀名.md)
2. [返回两个文件的不同行的编号](返回两个文件的不同行的编号.md)
3. [查找指定文件格式文件](查找指定文件格式文件.md)
```python
import os

def find_file(work_dir,extension='jpg'):
    lst = []
    for filename in os.listdir(work_dir):
        print(filename)
        splits = os.path.splitext(filename)
        ext = splits[1] # 拿到扩展名
        if ext == '.'+extension:
            lst.append(filename)
    return lst

find_file('.','md') # 返回所有目录下的md文件
```

#### 正则和爬虫

1. [判断密码是否合法](判断密码是否合法.md)
2. [爬取天气数据并解析温度值](爬取天气数据并解析温度值.md)
3. [批量转化驼峰格式](批量转化为驼峰格式.md)
```python
import re
def camel(s):
    s = re.sub(r"(\s|_|-)+", " ", s).title().replace(" ", "")
    return s[0].lower() + s[1:]

# 批量转化
def batch_camel(slist):
    return [camel(s) for s in slist]

batch_camel(['student_id', 'student\tname', 'student-add']) #['studentId', 'studentName', 'studentAdd']

```
#### 绘图

1. [turtle绘制奥运五环图](turtle绘制奥运五环图.md)
![五环图](./img/turtle1.png)
2. [turtle绘制漫天雪花](turtle绘制漫天雪花.md)
结果：
<img src="https://github.com/jackzhenguo/python-small-examples/blob/master/img/turtlesnow.gif" width="300" height="200" alt="图片名称" align=center>
3. [4种不同颜色的色块，它们的颜色真的不同吗？](4种不同颜色的色块，它们的颜色真的不同吗？.md)
4. [词频云图](词频云图.md)
```python
import hashlib
import pandas as pd
from wordcloud import WordCloud
geo_data=pd.read_excel(r"../data/geo_data.xlsx")
words = ','.join(x for x in geo_data['city'] if x != []) #筛选出非空列表值
wc = WordCloud(
    background_color="green", #背景颜色"green"绿色
    max_words=100, #显示最大词数
    font_path='./fonts/simhei.ttf', #显示中文
    min_font_size=5,
    max_font_size=100,
    width=500  #图幅宽度
    )
x = wc.generate(words)
x.to_file('../data/geo_data.png')
```
![词频云图](./data/geo_data.png)

#### 生成器

1. [求斐波那契数列前n项(生成器版)](求斐波那契数列前n项(生成器版).md)
```python
def fibonacci(n):
    a, b = 1, 1
    for _ in range(n):
        yield a
        a, b = b, a + b

list(fibonacci(5))  # [1, 1, 2, 3, 5]
```
2. [将list等分为子组(生成器版)](将list等分为子组(生成器版).md)
```python
from math import ceil

def divide_iter(lst, n):
    if n <= 0:
        yield lst
        return
    i, div = 0, ceil(len(lst) / n)
    while i < n:
        yield lst[i * div: (i + 1) * div]
        i += 1

list(divide_iter([1, 2, 3, 4, 5], 0))  # [[1, 2, 3, 4, 5]]
list(divide_iter([1, 2, 3, 4, 5], 2))  # [[1, 2, 3], [4, 5]]
```

#### keras

1. [Keras入门例子](
```python
import numpy as np
from keras.models import Sequential
from keras.layers import Dense

data = np.random.random((1000, 1000))
labels = np.random.randint(2, size=(1000, 1))
model = Sequential()
model.add(Dense(32,
                activation='relu',
                input_dim=100))
model.add(Dense(1, activation='sigmoid'))
model.compile(optimize='rmsprop', loss='binary_crossentropy',
              metrics=['accuracy'])
model.fit(data, labels, epochs=10, batch_size=32)
predictions = model.predict(data)
```

[更多小例子，请点击此处](./md/README.md)
















