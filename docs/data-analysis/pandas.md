![](../img/pandas.jpeg)
#### Pandas初识
<hr>

##### 1. Pandas简介
Pandas 由 WesMcKinney 开发，是一种专门用于数据挖掘的库。其以 NumPy 库为基础，借力 NumPy 模块在计算方面性能高的优势来增强性能。也基于 matplotlib 库，能够简便绘图，并且有着独特的数据结构。
<hr>

##### 2. Pandas优势
NumPy 已近可以帮助我们解决问题，能够结合 Matplotlib 解决部分数据的展示等问题，那为什么要使用 Pandas，使用它的优势主要有以下几个部分：

( 1 ) 增强图表的可读性

( 2 ) 便捷的数据处理能力

( 3 ) 读取文件特别方便

( 4 ) 封装了 Matplotlib 的画图和 NumPy 的计算
<hr>

#### Pandas数据结构
Pandas 一共有三种数据结构，分别是 Series、DataFrame 和M ultiIndex。<font>三者分别是一维数据结构、二维数据结构和三维数据结构</font>。

<hr>

##### 1. Series结构

Series 是一个类似于一维数组结构，它能够保存任何数据类型的数据，如整数、字符串、浮点数等，<font color='red'>**主要由一组数据和与之相关联的数组两部分组成**</font>。

( 1 ) Series 的创建，通过已有数据创建
```py
import pandas as pd
# data：传入的数据，可以是ndarray、list等
# index：索引，必须是唯一且与数据的长度相等，如果没有传入索引参数，则默认会自动创建一个从0～N的整数索引
# dtype：数据类型
pd.Series(data=None, index=None, dtype=None)
```
( 2 ) 指定内容默认索引创建
```py
import pandas as pd
import numpy as np
pd.Series(data=np.arange(10))
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226220243343.png)

( 3 ) 指定索引创建
```py
import pandas as pd
pd.Series(data=[6, 7, 8, 9, 10], index=[0, 1, 2, 3, 4])
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226220206520.png)

( 4 ) 通过字典数据创建
```py
import pandas as pd
pd.Series(data={'name': 'thanlon', 'age': 24, 'address': '中国上海'})
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226220147808.png)

( 5 ) Series 的两个属性

为更方便地操作 Series 对象中的索引和数据，<font>Series 中提供两个属性，分别是 index 和 values</font>。

① index
```py
import pandas as pd
staff = pd.Series(data={'name': 'thanlon', 'age': 24, 'address': '中国上海'})
print('职员的姓名：',staff[0])
print('职员的年龄：',staff['age'])
print(staff.index)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226220123755.png)

② values
```py
import pandas as pd
staff = pd.Series(data={'name': 'thanlon', 'age': 24, 'address': '中国上海'})
print(staff.values) # <class 'numpy.ndarray'>
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226220033836.png)

<hr>

##### 2. DataFrame结构
DataFrame 是一个类似于二维数组或表格的对象，既有行索引和列索引。

( 1 ) DataFrame 的创建
```py
import pandas as pd
# index：行标签，如果没有传入索引参数，则默认会自动创建一个从0～N的整数索引
# columns：列标签，如果没有传入索引参数，则默认会自动创建一个从0～N的整数索引
pd.DataFrame(data=None, index=None, columns=None)
```
`例一：`
```py
import pandas as pd
import numpy as np
pd.DataFrame(data=np.random.randn(2, 3))
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226220012790.png)

`例二：`
```py
# 分别使用numpy和pandas生成学生的成绩表，生成10个同学的6个科目的成绩
import numpy as np
score = np.random.randint(0, 100, (10, 6))
print(score)
score_df = pd.DataFrame(score)
score_df
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226215940943.png)

( 2 ) 增加行列索引
```py
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
print(score)
score_df = pd.DataFrame(score)
print(score_df)
# 构建行索引序列
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
# 构建列索引序列
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
# 添加行索引
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226215857988.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

( 3 ) DataFrame 的属性

① shape：查看几行几列
```py
'''
查看几行几列
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
print(data.shape)
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226221157145.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

② index：获取行索引列表
```py
'''
获取行索引列表
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
print(data.index)
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226221304861.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

③ columns：获取列索引列表
```py
'''
获取列索引列表
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
print(data.columns)
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226221350659.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

④ values：获取数组的值
```py
'''
获取数组的值
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
print(data.values)
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226223102602.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

⑤ T：转置
```py
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
data.T
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226225156343.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

⑥ head(n)：查看前n行，<font color='red'>**如果不传入n，默认是5行。如果数据没有5行，则默认查看所有行。**</font>
```py
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
data.head(4)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226225418173.png)

⑦ tail(n)：查看后n行，<font color='red'>**如果不传入n，默认是5行。如果数据没有5行，则默认查看所有行。**</font>
```py
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
data.tail(2)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226225603674.png)

( 4 ) DataFrame索引的设置

① 修改行列索引值
```py
'''
必须整体全部修改，不能使用索引方式改局部，如data.index[0] = '学生_1'
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
stu1 = ['学生_'+str(i+1) for i in range(score_df.shape[0])]
data.index = stu1
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226235552359.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

② 重设索引
```py
'''
使用reset_index(drop=False)，可以用来设置新的下标索引，drop：默认是False，不删除原来的索引，如果为True，删除原来的索引值
不删除原来的索引
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
data = data.reset_index()
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227000425781.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

```py
'''
使用reset_index(drop=False)，可以用来设置新的下标索引，drop：默认是False，不删除原来的索引，如果为True，删除原来的索引值
删除原来的索引
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
data = data.reset_index(drop=True)
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227000436682.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

- 以某列值设置为新的索引
```py
'''
设置新的索引：set_index(keys, drop=True)
keys：列索引名称或列索引名称的列表
drop：boolean类型，默认是True，当做新的索引，删除原来的列
以月份设置新的索引
'''
import pandas as pd
df = pd.DataFrame({
    'month': [1, 2, 3, 4],
    'year': [2017,2018, 2019, 2020],
    'sale': [66, 77, 88, 99]
})
df = df.set_index('month') # 设置单个索引
df
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227092651430.png)

```py
'''
设置新的索引：set_index(keys, drop=True)
keys：列索引名称或列索引名称的列表
drop：boolean类型，默认是True，当做新的索引，删除原来的列
以年份和月份设置新的索引
'''
import pandas as pd
df = pd.DataFrame({
    'month': [1, 2, 3, 4],
    'year': [2017, 2018, 2019, 2020],
    'sale': [66, 77, 88, 99]
})
df = df.set_index(['year', 'month']) # 设置多个索引，要使用列表
df
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227092707450.png)
>**DataFrame通过修改可以变成MultiIndex结构。**

##### 3. MultiIndex结构

MultiIndex 是三维的数据结构，即多级索引，也称为层次化的索引。<font>层次化索引是 pandas 的重要功能，可以在 Series、DataFrame 对象上拥有 2 个及其以上的索引</font>。除了通过修改 DataFrame 数据结构变成 MulitiIndex 结构，还可以直接创建。
 
( 1 ) MultiIndex的创建
```py
import pandas as pd
arrays = [['thanlon', 'kiku', 'kili'], [22, 23, 24]]
pd.MultiIndex.from_arrays(arrays=arrays, names=('name', 'age'))
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227104914950.png)

( 2 ) MultiIndex的特性
```py
'''
index
'''
import pandas as pd
df = pd.DataFrame({
    'month': [1, 2, 3, 4],
    'year': [2017, 2018, 2019, 2020],
    'sale': [66, 77, 88, 99]
})
df = df.set_index(['year', 'month'])
df.index
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227105622126.png)

```py
'''
index.names
'''
import pandas as pd
df = pd.DataFrame({
    'month': [1, 2, 3, 4],
    'year': [2017, 2018, 2019, 2020],
    'sale': [66, 77, 88, 99]
})
df = df.set_index(['year', 'month'])
df.index.names
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227105702906.png)

```py
import pandas as pd
df = pd.DataFrame({
    'month': [1, 2, 3, 4],
    'year': [2017, 2018, 2019, 2020],
    'sale': [66, 77, 88, 99]
})
df = df.set_index(['year', 'month'])
df.index.levels
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227105730475.png)

```py
import pandas as pd
df = pd.DataFrame({
    'month': [1, 2, 3, 4],
    'year': [2017, 2018, 2019, 2020],
    'sale': [66, 77, 88, 99]
})
df = df.set_index(['year', 'month'])
df.index.codes
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227105805806.png)

##### 4. Panel结构
Panel已被废弃，这里只作了解。Panel 是 MultiIndex 的前身。

( 1 ) Panel 的创建
```py
'''
pandas.Panel(data-None, items=None, major_axis=None, minor_axis=None)：存储3维数组的Panel结构
data：ndarray或者DataFrame，表示整体的数据
items：索引或类似数组的对象，axis=0
major_axis：索引或类似数组的对象，axis=1
minor_axis：索引或类似数组的对象，axis=2
'''
import pandas as pd
import numpy as np
# 24个数，第一个维度是4，第二个维度是3，第三个维度是2，三维
data = np.arange(24).reshape(4, 3, 2)
items = list('ABCD')  # ['A', 'B', 'C', 'D']
major_axis = pd.date_range('20200227', periods=3) # DatetimeIndex(['2020-02-27', '2020-02-28', '2020-02-29'], dtype='datetime64[ns]', freq='D')
minor_axis = ['first', 'second']
pd.Panel(data=data, items=items, major_axis=major_axis, minor_axis=minor_axis)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227130454778.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

( 2 ) Panel 数据的查看
```py
 import pandas as pd
import numpy as np
# 24个数，第一个维度是4，第二个维度是3，第三个维度是2，三维
data = np.arange(24).reshape(4, 3, 2)
items = list('ABCD')  # ['A', 'B', 'C', 'D']
major_axis = pd.date_range('20200227', periods=3) # DatetimeIndex(['2020-02-27', '2020-02-28', '2020-02-29'], dtype='datetime64[ns]', freq='D')
minor_axis = ['first', 'second']
p = pd.Panel(data=data, items=items,
             major_axis=major_axis, minor_axis=minor_axis)
p[:, :, 'first']  # :表示取所有
p['A', :, :]
```
<hr>

#### 基本数据操作
<hr>

#### DataFrame运算
<hr>

#### Pandas绘图
<hr>

##### 1. 绘制折线图
```py
import pandas as pd
import numpy as np
import random
data = []
for i in np.arange(0, 100, 10):
    data.append(random.randint(10, 20))
s = pd.Series(data=data)
print(s)
s.plot(kind='line')  # s.plot.line()，s.plot()函数的参数kind默认是'line'
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228205458917.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

<hr>

##### 2. 绘制柱状图
```py
import pandas as pd
import numpy as np
import random
data = []
for i in np.arange(0, 100, 10):
    data.append(random.randint(10, 20))
s = pd.Series(data=data)
print(s)
s.plot(kind='bar')
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020022821033337.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

```py
import pandas as pd
import numpy as np
import random
data = []
for i in np.arange(0, 100, 10):
    data.append(random.randint(10, 20))
s = pd.Series(data=data)
print(s)
s.plot(kind='barh')
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228210426563.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

<hr>

##### 3. 绘制直方图
```py
import pandas as pd
import numpy as np
import random
data = []
for i in np.arange(0, 100, 10):
    data.append(random.randint(10, 20))
data = np.random.normal(1.75, 1, 10000) 
s = pd.Series(data=data)
print(s)
s.plot(kind='hist')
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228213939462.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

<hr>

##### 4. 绘制折线图
```py
import pandas as pd
import numpy as np
data = np.random.randn(10, 2)  # 从标准动态分布中返回一个或多个样本值
print(data)
df = pd.DataFrame(data=data)
print(df)
df.plot(kind='line')  # df.plot()函数的参数kind默认是'line'
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228201352644.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

##### 5. 绘制柱状图
```py
import pandas as pd
import numpy as np
data = np.random.randn(10, 3)  # 从标准动态分布中返回一个或多个样本值
print(data)
df = pd.DataFrame(data=data)
print(df)
df.plot(kind='bar')  # df.plot.line()，df.plot()函数的参数kind默认是'line'
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228212151840.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

```py
import pandas as pd
import numpy as np
data = np.random.randn(10, 3)  # 从标准动态分布中返回一个或多个样本值
df = pd.DataFrame(data=data)
df.plot(kind='barh')  # df.plot()函数的参数kind默认是'line'
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228212400359.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

##### 6. 绘制直方图
```py
import pandas as pd
import numpy as np
data = np.random.randn(10, 3)  # 从标准动态分布中返回一个或多个样本值
print(data)
df = pd.DataFrame(data=data)
print(df)
df.plot(kind='hist')  # df.plot()函数的参数kind默认是'line'
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228215053951.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

<hr>

#### 文件读取与存储
<hr>

##### 1. CSV文件的读取与存储
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200229102432375.png)

( 1 ) CSV文件的读取：
```py
'''
读取数据，并且指定只获取age和addr指标
'''
import pandas as pd
pd.read_csv(filepath_or_buffer='test.csv')
# filepath_or_buffer：文件路径；usecols：指定读取的列名；sep：默认是以逗号分割
pd.read_csv(filepath_or_buffer='test.csv', usecols=['name', 'age'], sep=',')
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200229102523441.png)

( 2 ) CSV文件的存储：
```py
'''
存储数据
'''
import pandas as pd
data = pd.read_csv(filepath_or_buffer='test.csv', usecols=['name', 'age'], sep=',')
# to_csv的参数，columns：选择需要的列索引；header：是否写进列索引值，默认是True；index：是否写进索引，默认是True。mode：重写(w)与追加(a)
data.to_csv(path_or_buf='tmp.csv', columns=['name'], header=True, index=None, mode='w')
data = pd.read_csv(filepath_or_buffer='tmp.csv')
data
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200229104113394.png)

```py
'''
存储数据，不保存索引
'''
import pandas as pd
data = pd.read_csv(filepath_or_buffer='test.csv', usecols=['name', 'age'], sep=',') # 
data.to_csv(path_or_buf='tmp.csv',columns=['name'],index=False)
data = pd.read_csv(filepath_or_buffer='tmp.csv')
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200229104147504.png)

<hr>

##### 2. HDF5文件的读取与存储
( 1 ) 创建 HDF5 文件

首先安装 h5py 模块：
```python
$ sudo pip3 install h5py -i https://pypi.tuna.tsinghua.edu.cn/simple
```
```py
import h5py
f = h5py.File('hd.h5', 'w')
lst1 = ['thanlon', 'kiku', 'kili']
column_01 = []
for i in lst1:
    column_01.append(i.encode())
f['name'] = column_01
f['age'] = [11,22,23]
print(f.keys())
print(f['name'][:])
print(f['age'][:])
f.close()
```
( 2 ) HDF5 格式文件的读取：
```py
# 安装tables模块，sudo pip3 install tables -i https://pypi.tuna.tsinghua.edu.cn/simple
import pandas as pd
data = pd.read_hdf('hd.h5')
data.head()
```
( 3 ) HDF5格式文件的存储
```py
import pandas as pd
data = pd.read_hdf('hd.h5')
data.to_hdf('hd.h5', key='data')  # 注意这里必须有要有key
pd.read_hdf('hd.h5', key='data')
```
>**HDF5 在存储的时候，使用的方式blosc。这种方式是速度读取快，使用压缩提高磁盘利用率节省空间，也是 pandas 默认支持的。HDF5 还是跨平台的，可以轻松迁移到 adoop 上。**

<hr>

##### 3. JSON文件的读取与存储
<hr>
( 1 ) JSON格式文件的读取：
```py
# 
```

( 2 ) JSON格式文件的存储：
```py
# 
```
<!--回到顶部 start-->
<div style="width: 60px;height: auto;z-index: 99;bottom: 30%;position: fixed;right: 0px" id="plug-ins">
    <div style="position: relative;float: right">
        <a target="" href="javascript:;" id="weibo"
           style="display: block;width: 40px;height: 40px;background-color: #c4351b;margin-top: 1px;">
            <img width="22" height="20" src="../img/weibo.png" alt=""
                 style="margin-top: 10px;margin-left: 9px">
        </a>
        <a target="_blank" href="http://wpa.qq.com/msgrd?v=3&uin=3330447288&site=qq&menu=yes" id="qq" style="display: block;width: 40px;height: 40px;background-color:#0e91e8;margin-top: 1px">
            <img width="20" height="20" src="../img/qq.png" 
                 style="margin-top: 10px;margin-left: 10px" alt="点击这里给我发消息" title="点击这里给我发消息">
        </a>
        <a href="javascript:" id="wechat"
           style="display: block;width: 40px;height: 40px;background-color:#01b901;margin-top:1px">
            <img width="22" height="20" src="../img/wechat.png"
                 style="margin-top: 10px;margin-left: 9px">
        </a>
        <a href="javascript:" id="go_top"
           style="display: none;width: 40px;height: 40px;background-color: #b5b5b5;margin-top: 1px">
            <img width="22" height="20" src="../img/top.png" alt=""
                 style="margin-top: 10px;margin-left: 9px">
        </a>
    </div>
</div>
<!--回到顶部 start-->
<!--左侧广告 start-->
<div style="width: auto;height: auto;z-index: 99;position: fixed;left: 0;top: 70px;" id="google_ads">
        <div>
            <div style="width: 180px;height: auto"></div>
            <!-- Vertical -->
            <ins class="adsbygoogle"
                 style="display:block"
                 data-ad-client="ca-pub-6937898095875663"
                 data-ad-slot="2927491642"
                 data-ad-format="auto"
                 data-full-width-responsive="true"></ins>
            <script>
                (adsbygoogle = window.adsbygoogle || []).push({});
            </script>
        </div>
</div>
<!--左侧广告 stop-->
<!--右侧广告 start-->
<div style="width: auto;height: auto;z-index: 99;position: fixed;right: 0;top: 70px;" id="google_ads">
        <div>
            <div style="width: 180px;height: auto"></div>
            <!-- Vertical -->
            <ins class="adsbygoogle"
                 style="display:block"
                 data-ad-client="ca-pub-6937898095875663"
                 data-ad-slot="2927491642"
                 data-ad-format="auto"
                 data-full-width-responsive="true"></ins>
            <script>
                (adsbygoogle = window.adsbygoogle || []).push({});
            </script>
        </div>
</div>
<!--右侧广告 stop-->