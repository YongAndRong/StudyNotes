## 集 set

    * 约定
        * set 翻译为集合
        * collection翻译为集合类型,是一个大概念
    * set
        * 可变的、无序的、不重复的 元素的集合

### set定义  初始化
    * set() ---> new empty set object
    * set(iterable)  ---> new set object

```python
#example 
s1 = set()
s2 = set(range(5))
s3 = set(list(range(10))) #ok的
s4 = {}  #这个是字典的符号dict
s5 = {9,10,11}  #set
s6 = {(1,2),3,'a'}
s7 = {[1],(1,),1}  #error,可变类型无法存到set中去的

In [41]: s7 = {1,2,(1,),(3,[4])}        #error                                                                               
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-41-d8a74fa6ecd2> in <module>
----> 1 s7 = {1,2,(1,),(3,[4])}

TypeError: unhashable type: 'list'

#__________________________________________________s
In [42]: hash(1)                                                                                                      
Out[42]: 1

In [43]: hash('abc')                                                                                                  
Out[43]: 1925617888116319093

In [44]: hash([1,2,])                                                                                                 
---------------------------------------------------------------------------
TypeError  

####*****************************
In [40]: s2 = set(b'abcd')       #bytes type, so get int set                                                                                      
In [41]: s2                                                                                                           
Out[41]: {97, 98, 99, 100}

In [42]: s3 = set(bytearray(b'hello'))    #no repeat                                                                             

In [43]: s3                                                                                                           
Out[43]: {101, 104, 108, 111} #get four elem

##如下顶进去的是十进制整数，而append的进去的是bytes类型
In [88]: l1                                                                                                           
Out[88]: [0, 2, b'hji', b'cde', 'c', 'b']

In [89]: l1[1:2] = b'abcd'                                                                                            

In [90]: l1                                                                                                           
Out[90]: [0, 97, 98, 99, 100, b'hji', b'cde', 'c', 'b']

In [91]: l1.append(b'hi')                                                                                             

In [92]: l1                                                                                                           
Out[92]: [0, 97, 98, 99, 100, b'hji', b'cde', 'c', 'b', b'hi']
```

### set的元素
    * set的元素要求必须可以hash
    * 目前学过的不可hash的类型有list、set
    * 元素不变可以使用索引
    * set可以迭代

### set增加
    * add(elem)
        * 增加一个元素到set中
        * 如果元素存在,什么都不做

    * update(*others)   #并集  
        * 合并其他元素到set集合中来
        * 参数others必须是可以迭代对象  *other表示可以多个可迭代对象
        * 就地修改
```python
In [48]: s6.add(1)            #   一次只能加进来一个元素，里面有的元素，不再加进来                                                                                     
In [49]: s6.add('1')                                                                                                  
In [50]: s6                                                                                                           
Out[50]: {1, '1', 2, 3}

In [51]: s6.add('abc')                                                                                                
In [52]: s6.add('abc',5,6)      #   一次只能加进来一个元素                                                                                       
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-52-01c7330046fe> in <module>
----> 1 s6.add('abc',5,6)

TypeError: add() takes exactly one argument (3 given)

#example update
In [57]: s6.update(range(6))      #返回值None，就地修改  这个叫并集                                                                                    

In [58]: s6                                                                                                           
Out[58]: {0, 1, '1', 2, 3, 4, 5, 'abc'}

In [59]: s6.update(range(6),range(8))                                                                                 

In [60]: s6                                                                                                           
Out[60]: {0, 1, '1', 2, 3, 4, 5, 6, 7, 'abc'}

```

### set删除
    * remove(elem)
        * 从set中移除一个元素
        * 元素不存在,抛出KeyError异常,为什么是KeyError?  
    * discard(elem)
        * 从set中移除一个元素
        * 元素不存在,什么都不做   (比较温和的一种操作)
    * pop() --->item
        * 移除并返回任意的元素,为什么是任意元素?
        * 空集返回KeyError异常
    * clear()
        * 移除所有元素   #慎重，这只是标记一下，所以很快的
```python
# remove
In [80]: s6                                                                                                           
Out[80]: {(1, 2, 3), (1, 2, 3, 4, 5), (1,), 0, 1, '1', 2, 3, 4, 5, 6, 7, 'abc'}
In [81]: s6.remove((1,2,3,4,5))       #移除这个元组                                                                                
In [82]: s6                                                                                                           
Out[82]: {(1, 2, 3), (1,), 0, 1, '1', 2, 3, 4, 5, 6, 7, 'abc'}

In [83]: s6.remove(8)    #没有8 报错keyerror，#因为里面不会有重复的元素， key唯一的                                                                                           
---------------------------------------------------------------------------
KeyError 

#discard
In [86]: s6.discard(7)                                                                                                

In [87]: s6                                                                                                           
Out[87]: {(1, 2, 3), (1,), 0, 1, '1', 2, 3, 4, 5, 6, 'abc'}
#pop 方法
In [88]: s6.pop()  #随机出一个，没有规律的                                                                                                   
Out[88]: 0

In [90]: s7                                                                                                           
Out[90]: set()

In [91]: s7.pop()    #不能从空集里面弹出元素，否则报错                                                                                                   
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-91-295bfc69c181> in <module>
----> 1 s7.pop()

KeyError: 'pop from an empty set'

#clear
In [92]: s6.clear()                                                                                                   

In [93]: s6                                                                                                           
Out[93]: set()

```

### set修改、查询
    * 修改
        * 要么删除，要么加入新的元素
        * 为什么没有修改？  #因为本来里面就是不重复的，set修改就意味着要先移除元素，然后没有的元素，才添加进来
    * 查询
        * 非线性结构，无法索引
    * 遍历
        * 可以迭代所有元素
    * 成员运算符
        * in和not in 判断元素是否在set中
        * 效率呢？  #非常高O(1)，它不是遍历找出元素是否在set中的，而是根据给定值，算出它的hash值，然后根据hash值去set里面看看，这个hash值对应的位置有没有值，如果有，就代表该元素在set中，否则该元素不在set中。

        # 散列值意思是一个小小的变化都可以引发很大的改变
        # 幂等性，在本次程序运行过程中，同一个值的hash值始终是一样的
    * 遍历 就效率不高了，遍历只和元素个数相关

### set成员运算符的比较
    * list 和 set的比较
### set和线性结构
    * 线性结构的查询时间复杂度是O(n),即随着数据的规模的增大而增加耗时
    * set、dict等结构，内部使用hash值作为key，时间复杂度可以做到O(1)，查询时间和数据规模无关

    * 可hash
        数值型int、float、complex
        布尔型True、False
        字符串string、bytes
        tuple
        None
        以上都是不可变类型，是可哈希类型，hashable
    * set的元素必须是可hash的


## 集合
    * 基本概念
    * 全集
        * 所有元素的集合。例如实数集，所有实数组成的集合就是全集
    * 子集subset 和超集superset
        * 一个集合A所有元素都在另一个集合B内，A是B的子集，B是A的超集
    * 真子集和真超集
        * A是B的子集，且A不等于B，A就是B的真子集,B是A的真超集
    * 并集：多个集合合并的结果
    * 交集：多个集合的公共部分
    * 差集：集合中除去和其他集合公共部分
```python

```
### 集合运算
    * 并集
        * 将两个集合A和B的所有的元素合并到一起，组成的集合称作集合A和集合B的并集
        * union(*others)
            * 返回和多个集合合并的新的集合
        * | 运算符重载
            等同union
        * update(*others)
            和多个集合合并，就地修改
        |= 
            等同update
    *交集
        * 集合A和B，由所有属于A且属于B的元素组成的集合
        * intersection(*others)
            * 返回和多个集合的交集
        * & 
            等同intersection
        * intersection_update(*others)
            获取和多个集合的交集，并就地修改
        * &= 等同intersection_update

    * 差集
        * 集合A和集合B，由所有属于A且不属于B的元素组成的集合
        * difference(*others)
            返回和多个集合的差集
        - 
            等同difference
        * difference_update(*others)
            获取和多个集合的差集并就地修改
        -=   等同difference_update

    * 对称差集
        * 集合A和B，由所有不属于A和B的交集元素组成的集合，记作(A-B) U (B-A)
        * symmetric_difference(other)    #注意 这个other可不是多个哦，单个的一个计算完了再计算下一个
            返回和另一个集合的差集
        * ^ 等同symmetric_difference
        * symmetric_difference_update(other)
            获取和另一个集合的差集并就地修改
        *^=  等同symmetric_difference_update

    * issubset(other) 、 <=
        判断当前集合是否是另一个集合的子集
    * set1 < set2
        判断set1 是否是set2的真子集
    * issuperset(other) 、>=
        判断当前集合是否是other的超集
    * set1 > set2
        判断set1是否是set2的真超集
    * isdisjoint(other)
        当前集合和另一个集合没有交集
        没有交集，返回True
```python
#example 
In [195]: sa                                                                                                          
Out[195]: {1, 2, 3, 5}

In [196]: sb                                                                                                          
Out[196]: {1, 2, 3, 4}

In [197]: sc                                                                                                          
Out[197]: {1, 2, 3, 7}

In [198]: sd                                                                                                          
Out[198]: {1, 2, 3}
#*****************************************************
In [193]: sd.issubset(sa)    #sds是sa的子集                                                                                          
Out[193]: True

In [194]: sa.issubset(sd)         #sa不是sd的子集                                                                                    
Out[194]: False

In [199]: sa <= sa      #sa是sa的子集                                                                                              
Out[199]: True

In [200]: sa <= sd   #sa不是sd的子集                                                                                                 
Out[200]: False

In [201]: sd <= sa      #sd是sa的子集                                                                                              
Out[201]: True


