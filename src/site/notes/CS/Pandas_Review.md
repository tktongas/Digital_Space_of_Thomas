---
{"dg-publish":true,"permalink":"/cs/pandas-review/"}
---


# 0. pandas简介
- 专门的数据分析开源python包，基础工具
- 基于numpy开发 [Numpy_Review](Numpy_Review.md)
- 数据结构：series，dataframe，index

特点如下：
- 处理浮点数精度处理方法，大数据处理，准确处理数据队列，转换不规则数据和差异数据，从CSV/Excel中导入数据，智能合并和连接数据集等。

# 1. Series 一维的数组
> 基本的结构包含index和value，其相互关联。

## 1.1声明Series():
```python
import pandas as pd
a = pd.Series([1,2,3,4]) #该处S为大写。index默认从0开始。
b = pd.Series([5,6,7,8],index=['a','b','c','d']) #设置index
b.index #查看index
b.values #查看value

#通过字典生成Series
sdata = {'xiaoming':14,'xiaohong':15,'xiaolan':16}
c = pd.Series(sdata)

#用numpy或其他Series定义新的Series对象

#numpy一维数组转化为pandas series
Arr = np.array([1,2,3,4,5])
S = pd.Series(Arr)
#用Series创建Series
S1 = pd.Series(s) #是引用关系，非副本关系。如果改变某一个对象里的值，另一个也会改变
#深拷贝函数 copy(deep=true/false)
S1=s.copy()
```

## 1.2 选择Series内部元素
```python
Q['xiaoming'] #标签元素选择
Q[0] #索引元素选择
Q[1:2] #选取索引为第二的元素，不包含第三的数据
Q[1:] #选取索引为第二的一直包含到最后
Q[['xiaohong','xiaolan']]
```
## 1.3 元素的赋值
```python
Q['xiaohong'] = 15
```
## 1.4 Series元素筛选和运算
```python
s[s>12] #元素筛选
s/10 #元素运算
s+10
s-1
```
## 1.5 Series对象组成元素及判断
```python
# unique() 返回未排序list
S.unique() # 直接使用unique会对value去重复
S.index.unique() # 去除index重复值
S.value_counts() # 统计元素重复次数
S.isin([0,3,5]) # 判断从属关系，返回bool判断
S[S.isin([0,3,5])] # 返回重复值
S.dropna() # 删除空值
```
## 1.6 Series对象间的运算
> 能够通过识别标签对应不一致的数据，例如元素个数不一致，pandas自动根据对应标签进行计算，对同样标签的数据进行计算。
```python
S1+S2 #对应的标签相加，不一致的会显示成NaN
```

# 2. Dataframe
- pandas核心功能之一，为了将Series使用场景扩展到多维。列表式数据结构，按照**一定数据排列的列组成**，各列的数据类型可以不一样。
- Series组成的字典，每一列称为字典的键，形成dataframe的列的series作为字典的值。
![400](Pasted%20image%2020220312143124.png)

## 2.1 Dataframe和numpy对比
```python
Stock = np.random.normal(0,1,(10,5))
Stock = pd.Dataframe(stock) #自动添加了行索引和列索引，默认从0开始
stcok_name = ['股票{}'.format(i) for i in range(1,11)] #生成新行索引名
Stock = pd.Dataframe(Stock.index=stock_name) #自定义行索引

#自定义列索引
date_range() #起始时间20191201，产生数量5，B表示每个工作日
date = pd.date_range(start='20191201',period=5,freq='B')
Stock = pd.Dataframe(Stock.index=stock_name,columns=date)
```
## 2.2 创建DataFrame对象
```python
Df = pd.DataFrame(data) #从字典中创建
Df = pd.DataFrame(data,column=('color','price')) #指定列创建
Df = pd.DataFrame(data,column=('color','price'),index=('one','two','three','four')) #指定行索引，即将行索引变更成了one two three four
```

## 2.3 DataFrame的主要属性
- shape
- column
- index
- value
- T(矩阵转置)

```python
df['color'] #选取特定的列


#选取行
df.iloc[1:3] #即选取了第2,3行。共两行。  i表示index的意思
df.iloc[[0,3]] #选取间隔行，即选取了第1和第4行
df.loc['four'] #loc函数传入行的标签值
df.loc[['one','four']] #即选取了行标签为one和four的值
df['length'][2] #第一个值为列，第二个为行
```

## 2.4 对数据增删改查
```python
df['new'] = 99 #增加一列，值都为99
df['new'] = [i for i in range(4)] #指定新增列值
df.loc['four'] = ['test',5,6,7,8] #修改行数据
df.loc['five'] = ['test',7,8,9,10] #新增加了一行
rawdata.loc[i, "LOT TYPE"] = "MP" # 修改某格数据

# 在指定位置插入列，insert函数
fablist=list(data["Fab"])
data.insert(0,"FAB",fablist)

#drop() 函数，接收axis.axis =1 为列删除，axis = 0为行删除
df.drop(['color','price'],axis =1) #删除了color和price列
# drop函数不会对原对象进行更改，而是返回一个副本
df.drop('one',axis=0) #即删除了one行

del() #del只能删除列数据，会对原始数据行更改。实际操作中一般会对原始数据进行修改
del df['color'] #删除了列数据
```

## 2.5 判断元素的从属关系
```python
isin() #判断从属
df.isin(['pencil',3.4]) #判断两者是否在dataframe里，返回整个frame的True/False
df[df.isin(['pencil',3.4])] #返回整个frame的真值
```
## 2.6 DataFrame转置操作
- 转置：行和列的对换
df.T
![](Pasted%20image%2020220312150148.png)

## 2.7 pandas中的index对象
- index属性
数据中的轴标签。index对象不可改变(不能单独修改index对象里面的具体值)。不同数据公用index时，能保证数据安全。
```python
df.index[2] = '999' #该操作是错误的，不可单独进行修改
df.index =['one','two','999','four'] #可以。能够进行整体修改
```
- index重新索引
```python
reset_index() #重置索引，帮助重新生成以0为开始的索引值。只能接受一个参数：设置是否保留之前的索引值。
df.reset_index() #默认保留之前的index
df.reset_index(drop=True)
```
- 以某列作为新的索引
```python
set_index() #将任意列的值作为dataframe的新索引。两个参数：新索引的key(dataframe列名)，drop(是否删除索引列)
df.set_index('price') #默认删除原来的列
df.set_index('price',drop=False) 
```
![](Pasted%20image%2020220312151108.png)

- 识别并过滤重复索引
```python
df.index.is_unique #识别数据结构中是否存在重复索引项目
```
- 算术和数据对齐
> 在index和value都不同的两个Series中，pandas自动将相同的index进行对齐后计算。对于只在一个series中的index，会将value设置成NaN。
- 根据索引、内容进行排序
```python
#返回元素相同但顺序不同的新对象。
#如果索引是数字的话，按照数字的顺序排列。如果为字母，则按照字母进行排序。dataframe分别对两条轴中的任意一条排序。对行进行排序，直接使用sort_index,对列进行排序需要指定axis=1
S.sort_index()
Df.sort_index(axis=1)

sort_values() #按照元素内容进行排序。接受两个参数by(根据哪一列排序)，asscending(默认为True/升序，False为降序)
Df.sort_values(by='price',asscending=False)

# 对dataframe中的列顺序进行调整
df=df.reindex(columns=['b','c','a']) # 指定出新的列顺序，只会出现指定顺序的列。默认是副本。如需替换，则重新赋值给原来的df
df=df[['c','a','b']] # 该方法也可以转变列顺序

```
- groupby函数：分组排序
![Pandas_groupby](Pandas_groupby.md)

## 2.8. 算术与逻辑计算
- 算术运算：加减乘除
```python
#series之间
s1+s2
s1.add(s2)

#dataframe之间，需要指定列axis
Df['price']+3
df['price'].add(3).head(2) #显示前2行
df['price']+df['length']
df['price'].add(df['length'])
```
- 逻辑运算
> 筛选符合条件的元素

```python
df[df['price']>1.2]
df[(df['price']>1.2)&(df['length']<3.4)] #多条件筛选，用()隔开各个条件

#query函数
df.query('price'>1.2&'length'<3.4)
```

# 3. 统计函数与自定义运算
## 3.1 统计函数
```python
df.describe() #返回函数的最大，最小，均值，中位数等
sum() #求和
count() #统计个数
mean()
median()
min()
max()
std()
argmax() #返回最大值的索引
argmin()
# 参数里指定axis=0/1表示按行还是按列统计
# 有些统计函数只适合统计数值型，不适合字符型
```
## 3.2累计统计函数
统计量的累计。
```python
cumsum() #累计和
cumprod() #累计乘积
cummax() #累计最大值
cummin() #累计最小值

df.cumsum() #针对字符串类型的字段进行拼接。数值型进行累计值。
```
![](Pasted%20image%2020220312161155.png)

## 3.3 相关性分析统计
> 对两个或多个具备相关性的变量元素进行分析，从而衡量两个变量因素相关密切程度。
- pearson相关系数：也被成为皮尔森积矩相关系数，线性相关系数衡量相似度的方法。输出范围为[-1,1]。0表示不相关，-1表示负相关，1表示正相关。当相关性r符合-1<r<1，两个向量存在不同程度的相关性。r绝对值小于0.3，认为不存在相关性；r绝对值在0.3~0.5，为低度相关。0.5~0.8，显著相关;0.8~1高度相关。
- sperman相关系数：用于服从正态分布的连续变量。不服从正态分布变量或分类关联性也可以使用该相关系数，被称为等级相关系数。
- corr()：相关性分析函数 df.corr() 默认使用pearson相关系数，如需使用sperman传入参数(method='spearman')

## 3.4 自定义函数
- map()：将自定义函数作用于series对象的每个元素。参数：函数名
```python
Def addsomething(e):
	Return str(e)+'元'
Df['price'].map(addsomething)

lambda#可以使用lambda函数简化 
df['price'].map(lambda e:str(e)+'元')
```
- apply()：将自定义的函数作用于dataframe上的行列。需要指定axis参数，默认列。
```python
Df[['length','price']].apply(lambda e:e.max()-e.min()) #按列计算，price列和length列各自最大值和最小值的差值

Df[['length','price']].apply(lambda e:e.max()-e.min(),axis=1) #按行计算
```
![](Pasted%20image%2020220312162308.png)
- applymap()将自定义函数作用于dataframe的每一个元素。用于处理全局的元素。
```python
df.applymap(lambda e:e*2)
```

# 4. pandas中文件的读写
数据分析主要以pandas操作为主。
## 4.1 csv文件的读写
- csv文件的读取
```python
read_csv() #csv文件的读取，默认将第一行作为列名
df=pd.read_csv('test.csv')

df = pd.read_csv('test.csv',usecol=['price','length']) #指定读取某些列

#为数据增加列名(加入原始数据没有列名)
df = pd.read_csv('test.csv',names=['price','length']) 
df = pd.read_csv('test.csv',header=None) #或指定header为None,pandas会从0开始索引出列名

#省略或限定读取行数
df = pd.read_csv('test.csv',skiprows=2,names=['price','length']) #即省略了前2行，并添加了列名
df = pd.read_csv('test.csv',skiprows[7,10],names=['price','length']) #即省略了第8,11行，并添加了列名

#指定读取行
df = pd.read_csv('test.csv',nrows=5) #读取前5行
df = pd.read_csv('test.csv')
df.iloc[4:5] #进行切片，读取的是文件的第5行

#指定某列为索引index
index_col='issued'

```
- csv文件的保存
```python
to_csv() #默认保存当前位置
df.to_csv('test.csv',index=False) # index=False，即保存的文件中不含行号。

#保存特定行数据
df[:10].to_csv('test.csv',columns=['列1'，'列2']) #原来的index保存为unnamed
df[:10].to_csv('test.csv',columns=['列1'，'列2'],index=False)
```
![](Pasted%20image%2020220312163825.png)

## 4.2 HDF5文件读写
> 是存储分发科学数据的一种自我描述，多对象文件格式。主要特征：1自述性 2通用性 3灵活性 4扩展性 5跨平台。读取写入hdf需要两个参数：路径和key

```python
df = pd.read_hdf('test.h5') #如提示缺少tables模块，需要安装该模块
df.to_hdf("test2.h5",key='key2') #需定义key
```

## 4.3 JSON文件读写
> javascript object notation。  HTTP在浏览器和其他应用程序间发送数据的标准格式。

```python
Data = pd.read_json('sample.json')
data.to_json('sample1.json')
#实际存储成json，最好加上各种参数
orient='records' #按行写入json文件
lines=True #按行写入
data.to_json('sample2.json',orient='records',line=True)
```

## 4.4 从数据库中读写
SQL:mysql,SQL server
```python
to_sql()
read_sql()

import sqlite3 as lite
```
![](Pasted%20image%2020220312165522.png)

## 4.5 从Excel中读写
xlrd,openpyxl：pandas处理excel依赖的库
```python
read_excel:默认打开第一个表单
df=pd.read_excel('test.xlsx')
df=pd.read_excel('test.xlsx',sheet_name='test1') #指定表单名

df.to_excel('test2.xlsx',sheet_name='test2')
```
