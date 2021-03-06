## 元组  tuple
    * 一个有序的元素组成的集合
    * 使用小括号()表示
    * 元组是不可变的对象

### 元组的定义、初始化
    * 定义
        * tuple()  ---->空元组
        * tuple(iterable)    #可迭代。。
```python
#example
t = (1,)  # 定义一个元素的元组，注意有一个逗号
t = (1,) * 5
t = (1,2,3) * 5
t = (1,2,3,4)
t = tuple(range(5))
t = ()   #空元组
t = tuple()#空元组

t = (1)   #不是元组，1使用括号改变优先级 t*3 ---> 3

In [92]: lst
Out[92]: [1, 2, 3, 4, 5]

In [95]: t = tuple(lst)

In [96]: t
Out[96]: (1, 2, 3, 4, 5)  #变了，改为了括号了，改为了元组了
t[1] = 10  ---->  error

In [98]: t
Out[98]: (1, 2, 3, (3, 4, 5), 66)

In [99]: t[3][1]    #改值的话出错
Out[99]: 4

In [100]: t = (1,[2,3],'a',None)   #注意：里面存了一个列表，引用类型，所以列表里面的值是可以改变的哦，重大发现啊，元组里面存放的是列表的地址，反正列表的地址没有改变，所以列表里面的内容是可以改变的

In [101]: t[1][1] = 300

In [102]: t
Out[102]: (1, [2, 300], 'a', None)
#
In [103]: t9 = ([1],) *5  # 一定要注意引用类型啊，里面存放的是地址
In [105]: t9[2][-1] = 100
In [106]: t9
Out[106]: ([100], [100], [100], [100], [100])

```
### 元组元素的访问
    * 支持索引
    * 正索引：从左至右，从0开始，为列表中每一个元素编号
    * 负索引：从右至左，从-1开始
    * 正负索引不可以越界，否则引发异常IndexError

    * 元组通过索引访问
        * tuple[index],index就是索引，使用中括号访问
```python
t[1]
t[-2]
t[1] = 5
```

### 元组查询
* index(value,[start,[stop]])
    * 通过值value，从指定区间查找列表内的元素是否匹配  
    * 匹配第一个就立即返回索引  
    * 匹配不到，抛出异常ValueError  

* count(value)  
    * 返回列表中匹配value的次数  
        #未找到返回0

* 时间复杂度  
    * index 和count方法都是O(n)  
    * 随着列表数据规模的增大，而效率下降  

* len(tuple)
    * 返回元素的个数
    
### 元组其他操作
> 元组是只读的，所以增、改、删方法都没有
如果里面有引用类型，是可以改变的哦 

### 命名元组 namedtuple
    * namedtuple(typename,field_names,verbose=False,rename=False)
        * 命名元组，返回一个元组的子类，并定义了字段
        * field_names可以是空白符或逗号分割的字段的字符串，可以是字段的列表 
