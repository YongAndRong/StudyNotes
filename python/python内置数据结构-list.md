## 分类 
### 数值型  
    * int、float、 complex、 bool
### 序列对象  
    * 字符串 str  
    * 列表 list  
    * 元组 tuple  
### 键值对  
    * 集合 set
    * 字典 dict

### 数值型  
    * int、float、complex、bool、都是class，1、5.0、2+3j都是对象；记住：对象即实例
    * int：python3的int都是长整型，且没有大小限制，受限于内存区域的大小
    * float：由整数部分和小数部分组成，支持十进制和科学计数法表示。C的双精度型实现
    * complex：有实数和虚数部分组成，实数和虚数部分都是浮点数，3+4.2j
    * bool:int的子类，仅有2个实例True、False对应1和0，可以和整数直接运算
### 类型转换 (built-in)
    * int(x) 返回一个整数
    * float(x) 返回一个浮点数
    * complex(x)、complex(x,y) 返回一个复数
        In [11]: complex(2,3)                                                                               
        Out[11]: (2+3j)
    * bool(x) 返回布尔值；
        In [13]: bool(0)                                                                                        
        Out[13]: False

        In [14]: bool('a')                                                                                      
        Out[14]: True

### 数字的处理函数
    * round()：四舍六入，五取偶
    * floor()：向下取整
    * ceil()： 向上取整
    * int():取整数部分，截取效果
    * //: 整除且向下取整
```python
#example  ----  ceil() #向上取整
In [19]: math.ceil(2.1),math.ceil(2.4999),math.ceil(2.5000),math.ceil(2.6)                              
Out[19]: (3, 3, 3, 3)


In [20]: math.ceil(2.00000001)                                                                          
Out[20]: 3


In [21]: math.ceil(-2.1),math.ceil(-2.4999),math.ceil(-2.5000),math.ceil(-2.6)                          
Out[21]: (-2, -2, -2, -2)

#example ------- floor() #向下取整
In [24]: math.floor(2.1),math.floor(2.4999),math.floor(2.5000),math.floor(2.6)                          
Out[24]: (2, 2, 2, 2)


In [25]: math.floor(-2.1),math.floor(-2.4999),math.floor(-2.5000),math.floor(-2.6)                      
Out[25]: (-3, -3, -3, -3)

#example ------ // 整除，向下取整
In [26]: 1//2,2//2,3//2,4//2,5//2                                                                       
Out[26]: (0, 1, 1, 2, 2)

In [27]: -1//2,-2//2,-3//2,-4//2,-5//2                                                                  
Out[27]: (-1, -1, -2, -2, -3)

#example  ------ int()  #整型的截取，实际上就是对一个数字进行截取
In [29]: int(1//2),int(2//2),int(3//2),int(4//2),int(5//2)          #这种注意下，因为int()里面是个式子了，不是一个数字，所以一对比效果不对。看下面的实验吧                                    
Out[29]: (0, 1, 1, 2, 2)

In [30]: int(-1//2),int(-2//2),int(-3//2),int(-4//2),int(-5//2)                                         
Out[30]: (-1, -1, -2, -2, -3)

In [32]: int(3.6)                                                                                       
Out[32]: 3

In [33]: int(-3.6),int(-3.4),int(-3.5)                                                                 
Out[33]: (-3, -3, -3)

#example   ----round()  #四舍六入，五取偶
In [37]: round(2.1),round(2.4999),round(2.5000),round(2.51),round(2.9)                                  
Out[37]: (2, 2, 2, 3, 3)

In [38]: round(-2.1),round(-2.4999),round(-2.5000),round(-2.51),round(2.9)                              
Out[38]: (-2, -2, -2, -3, 3)

In [40]: round(0.5),round(1.5),round(2.5),round(3.5)                                                    
Out[40]: (0, 2, 2, 4) 
```

    * min()
    * max()
    * pow(x,y)  ----> x ** y
    * math.sqrt() ----> x ** 0.5
    * math.pi  --->π
    * math.e 自然常数 2.718281828459045

### 进制函数，返回值是字符串
    * bin()    #返回的是字符串
    * oct()
    * hex()
```python
# example 
In [58]: bin(10)                                                                                        
Out[58]: '0b1010'  #看清楚哦 ，返回值是字符串,不能做数值运算，这里已经转换类型了

In [63]: bin(10),oct(10),hex(10)                                                                        
Out[63]: ('0b1010', '0o12', '0xa') #看清楚哦 ，返回值是字符串,不能做数值运算，这里已经转换类型了

In [65]: type(bin(10))                                                                                  
Out[65]: str  #看这里
```
### 类型判断  
    * type(obj),   返回类型，而不是字符串
    * isinstance(obj,class_or_tuple)，   返回布尔值

```python
#example 
In [68]: a                                                                                              
Out[68]: 10

In [71]: type(a)                                                                                        
Out[71]: int

In [69]: type(a) == 'int'     #这个比较就不对，type(a) 返回的是类型，类型和字符串比较，虽然==和!=可以比较，但是一定出False    'int'就像人的名字一样，是个字符串，type() 返回类型                                                                     
Out[69]: False

In [70]: type(a) == int     #应该这样比较                                                                            
Out[70]: True

# isinstance
In [90]: isinstance('ab',(int,float,))  #'ab' 你是int吗？你是float吗？依次比较的，如果是就返回True，否则返回False                                                                
Out[90]: False

In [94]: isinstance(False,int)     #bool类型是int子类，所以这个返回True，所以isinstance可以判断子类                                                                     
Out[94]: True

In [95]: type(False) == int     #这样没法测试子类，所以isinstance用的比较多的                                                                         
Out[95]: False

#注意这个：
isinstance(6,(str,bool,int))  #过程是这样的，6是str类型吗？不是。6是bool吗？不是。6是int吗？是的，所以返回True；  
#bool可以是整型，但是整型不是bool   isinstancce(0,bool) -->false;  isinstance(1,bool) -->false。知道了吧

In [98]: type(1 + True)     #bool是int的子类，所以可以加的，不会报错                                                                            
Out[98]: int

In [99]: type (1+True+2.0)        # 这里有隐式转换，所以不会报错 ，类似c语言                                                                  
Out[99]: float

In [102]: 1+False+2.5                                                                                   
Out[102]: 3.5
```

## 列表  list

    * 一个队列，一个排列整齐的队伍
    * 列表内的个体称作元素，由若干元素组成列表
    * 元素可以是任意对象(数字、字符串、对象、列表等)
    * 列表内元素有顺序，可以使用索引
    * 线性的数据结构
    * 使用[]表示
    * 列表是可变的
> 一定注意：列表是可变的，线性的数据结构，有序的，在内存中是连续存放的

### 列表list定义 初始化
    * list()
    * list(iterable)
    * 列表不能一开始就定义大小
>举例：  
lst = list()  
lst = []  
lst = [2,6,9,'ab']  
lst = list(range(5))  
lst = list([2,6,9,'ab'])  #多余

```python
In [102]: range(5)  #  这里返回的是range对象，因为是惰性的，你如果要里面的元素，得用for循环一个一个从里面拿                                                                               
Out[102]: range(0,5)

lst = list(range(5))  #这里实际用了一个for循环，将range内的元素一个一个装入到了列表中，然后将标识符lst与这个列表建立了关联关系，从而可以通过lst操作该列表

l1 = []
l2 = list()  #这两个效果一样，其实[] 最后是用list()搞出来的

lst = [1,'ab',True,None,[4,5,'ab'],str] #一切皆对象，是对象就可以作为元素
for f in lst:
    print(type(f))

<class 'int'>
<class 'str'>
<class 'bool'>
<class 'NoneType'>
<class 'list'>
<class 'type'>    #看看返回的类型都是些什么
```

### 列表索引访问
    * 索引，也叫下标   
    * 正索引：从左至右，从0开始，为列表中每一个元素编号  
    * 负索引：从右至左，从-1开始  
    * 正负索引不可以超界，否则引发异常IndexError  
    * 为了理解方便，可以认为列表是从左至右排列的，左边是头部，右边是尾部，左边是下界，右边是上界  

    * 列表通过索引访问  
        list[index],index就是索引，使用中括号访问  

### 列表查询  
    * index(value,[start,[stop]])
        * 通过值value，从指定区间查找列表内的元素是否匹配
        * 匹配第一个就立即返回索引(从左向右一个一个遍历的找)
        * 匹配不到，抛出异常ValueError
```python
In [1]: lst = [1,2,3,4,5,1,2,3,]

In [2]: lst.index(4)
Out[2]: 3

In [3]: lst.index(6)
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-3-d05f2abc176c> in <module>
----> 1 lst.index(6)

ValueError: 6 is not in list
```   
    * count(value)
        * 返回列表中匹配value的次数，他会遍历整个列表
    * 时间复杂度  
        * index和count方法都是O(n)
        * 随着列表数据规模的增大，而效率下降
    * 如何返回列表元素的个数？如何遍历？如何设计高效？
    count(value)  找里面的值value有几个  没找到就是0，没找到不会报错
    count(）会遍历列表，这个方式非常低效 时间复杂度O(n),所以能不用则不用count

    * len()  
    len()不会遍历列表才知道列表有多长，这个长度就像是列表的属性一样，加元素长度+1，减元素长度-1，所以算列表的长度速度很快的，时间复杂度是O(1)


### 列表元素修改
    * 索引访问修改
        * list[index] = value
        * 索引不要超界,超界一样报错，indexerror


### 列表增加、插入元素
    * append(object) ->None
        * 列表尾部追加元素，返回None
        * 返回None就意味着没有新的列表产生，就地修改
        * 时间复杂度是O(1)
```python
In [7]: lst.append(12).append(13)  #lst.append(12)返回None，所以变成了None.append(13),None不是容器，而是一个单值，所以不允许追加，报错，但是12这个值是追加进列表lst了。
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-7-b12154870e7c> in <module>
----> 1 lst.append(12).append(13)

AttributeError: 'NoneType' object has no attribute 'append'

In [8]: lst
Out[8]: [1, 2, 3, 4, 5, 1, 2, 3, 11, 12]   #看看12这个值是追加进去了的，13由于有问题，未加进去
```



    * insert(index,object) -->None
        * 在指定的索引index处插入元素object
        * 返回None就意味着没有新的列表产生，就地修改
        * 时间复杂度是O(n)
        * 索引能超上下界吗？
            * 超越上界，尾部追加
            * 超越下界，头部追加
```python
In [9]: lst.insert(1000,100)

In [10]: lst
Out[10]: [1, 2, 3, 4, 5, 1, 2, 3, 11, 12, 100]
```

    * extend(iterable) -->None
        * 将可迭代对象的元素追加进来，返回None
        * 就地修改
    注意，1、在尾部扩展，必须是可迭代对象
    2、extend在尾部扩展，如果空间不够的话，垃圾回收就会去规整空间，这样也会有效率下降的风险

    + --> list
        * 连接操作，将两个列表连接起来   #是列表加列表哦，不是数值加列表，否则出错
        * 产生新的列表，原列表不变 
        * 本质上调用的是魔术方法__add__()方法
        #这种操作能不做就不做，因为太耗时间和内存了，它是新建一个list,需要将元素搬到新list中去，而且另外还得开辟一倍连续的空间。
        新产生的列表得用标识符来关联，否则就只是打印下就完了

    * --> list
        * 重复操作，将本列表元素重复n次，返回新的列表
        #需要用标识符来接，否则就只是显示一下就完了,意思就是生成了一个新的列表


### 列表 * 重复的坑
    * `*` --->list
        * 重复操作，将本列表元素重复n次，返回新的列表
        如果其中有引用类型的话，是浅拷贝
### 列表复制  
    * shadow copy
        * 影子拷贝，也叫浅拷贝，遇到引用类型，只是复制了一个引用而已(即地址)
    * 深拷贝
        * copy模块提供了deepcopy
        import copy
        lst0 = [1,[2,3,4],5]
        lst5 = copy.deepcopy(lst0)
        lst5[1][1] = 20
        lst5 == lst0 #不等了,注意 这里的相等比较是里面的值的比较即内容比较

    * id(x) ----> 取内存地址cpython
    #可以使用print(id(x))打印出来看看
```python
#example *
#这里请注意下这个情况：
In [24]: l4 = [0]

In [25]: l5 = [l4] * 3   #这里也相当于是l5 = [[0]]  引用类型啊，得相当注意了，* 对列表进行复制时，对简单类型要好一些！！

In [26]: l4[0] = 1000

In [27]: l5
Out[27]: [[1000], [1000], [1000]]

```


### 列表删除元素
    * remove(value) -->None
        * 从左至右查找第一个匹配value的值，移除元素，返回None
        * 就地修改
        * 效率？    #remove需要遍历，而且在移除后，该元素后面的还得挪动，比index()还差，除非是最后一个，时间复杂度是O(n)。
                    #在remove（value）中的value没有找到的话，会出现异常。


    * pop(index) -->item
        * 不指定索引index，就从列表尾部弹出一个元素   #找到了就是返回值
        * 指定索引index，就从索引处弹出一个元素，索引超界抛出IndexError错误
        * 效率？指定索引的时间复杂度？不指定索引呢？
        #1、pop(index) ---根据索引pop的话，只要不是最后一个，一样会挪动数据，效率和remove一样，但是我们鼓励使用pop()，这样的就是弹出最后一个元素，这个效率就很高
        2、pop()在列表为空时使用会出异常
        3、pop(value) :在没找到这个value时，也会出异常 

        # remove是根据值来弹出，找到了就直接弹出，没找到出异常
        #pop()是根据索引所对应的值来弹出，鼓励使用

    * clear() --> None
        * 清除列表所有元素，剩下一个空列表
        #它不会真的把数据给清理了，只是告诉别人，这些元素我不要了，我把他们的引用计数都减1.
        #并将列表长度设置为0。类似快速格式化
        #清理对象都是垃圾回收干的，只要引用计数为0，垃圾回收都会将其回收了
        #从数据的角度考虑，还是少用这个操作，除非真的没用了

### 列表其他操作
    * reverse() -->None
        * 将列表元素反转，返回None
        * 就地修改
        #对调过程，效率不高的，如果要倒着输出元素的话，可以倒着读！！

    * sort(key=None,reverse=False) -->None
        * 列表元素进行排序，就地修改，默认升序
        * reverse为True，反转，降序
        * key一个函数，指定key如何排序
            * lst.sort(key=function)
```python
#example 
In [4]: r = [3,2,1,4,5]  # 有一个列表，在里面插入了一个字符串6，然后进行sort()方法，因为是字符串，所以用sort时，会报错，我们可以用另一种方法来对这种情况排序
In [5]: r.append('6')

In [6]: r
Out[6]: [3, 2, 1, 4, 5, '6']
In [7]: r.sort()  #error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-7-ee2c9f5de204> in <module>
----> 1 r.sort()

TypeError: '<' not supported between instances of 'str' and 'int'
In [8]: r.sort(key=int)  #将列表中所有的元素用int转换成整型，如果转换失败，也会报异常的。这里的key仅仅用在比较时，并不影响元素本身，默认升序

In [9]: r
Out[9]: [1, 2, 3, 4, 5, '6']  #里面的字符串还是字符串并没有变为整型

In [10]: r.append('a')

In [11]: r.sort(key=str) #看这里

In [12]: r
Out[12]: [1, 2, 3, 4, 5, '6', 'a']  #根据ASCII码来排的
```
            
    * in
        * [3,4] in [1,2,[3,4]]
        * for x in [1,2,3,4]
        *返回bool型，不会报错，所以我们经常用这个，不怎么用index，比较内容，内容一样就返回true，否则返回false
```python
#根据内容进行比较，每一个索引对下来的值必须一样，才返回True
In [13]: 1 in r
Out[13]: True

In [14]: l5 = [1,[3,4],5]

In [15]: 3 in l5
Out[15]: False

In [16]: [3,4] in l5
Out[16]: True

In [17]: [3] in l5
Out[17]: False
```
### 随机数  
* random模块  

* random(a,b) 返回[a,b]之间的整数 

* choice(seq) 从非空序列的元素中随机挑选一个元素，比如random.choice(range(10)),从0到9中随机挑选一个整数。random.choice([1,3,5,7])

* randrange([start,]stop[,step])从指定范围内，按指定基数递增的集合中获取一个随机数，基数缺省值为1.random.randrange(1,7,2)  

* random.shuffle(list) -->None就地打乱列表元素  

* sample(population,k)从样本空间或总体(序列或者集合类型)中随机取出k个不同的元素，返回一个新的列表
    * random.sample(['a','b','c','d'],2)
    * random.sample(['a','a'],2)会返回什么结果

```python
#example  
In [18]: import random

In [19]: random.randint(1,2)  #左包右包[ ]  ,在1到2之间选
Out[19]: 2

In [22]: random.randrange(1,2) #左包右不包[ ) ，在1 到2之前的那个数字之前选
Out[22]: 1

In [28]: random.choice(range(9)) #从非空序列中随机选择一个元素，可能存在重复的
Out[28]: 2

In [29]: random.choice(range(9))
Out[29]: 6
#不只是有choice这个方法可以随机的拿数据哦，你可以用randint生成一个index，通过index所以去一个非空列表中拿一样的，反正都是假随机
In [30]: lst = [1,2,3,4,5,6,7,8,9]

In [31]: for i in range(9):
    ...:     print(random.choice(lst))
    ...:
#
In [32]: for i in range(9):
    ...:     index = random.randint(0,7)
    ...:     print(lst[index])
    ...:
#效果基本一样的随机

#****************8shuffle
In [35]: lst
Out[35]: [1, 2, 3, 4, 5, 6, 7, 8, 9]

In [36]: random.shuffle(lst)

In [37]: lst
Out[37]: [4, 6, 9, 5, 7, 2, 1, 3, 8]

#sample  注意是不同的元素，所谓的不同是不用位置上的，所以想想k大于元素个数了呢
#样本空间不光是列表，还可能是集合呢，样本空间就像是一个大的容器一样
In [38]: lst
Out[38]: [4, 6, 9, 5, 7, 2, 1, 3, 8]

In [39]: random.sample(lst,0)
Out[39]: []

In [40]: random.sample(lst,3)
Out[40]: [5, 8, 1]

In [41]: random.sample(lst,10)  #超界会报错的
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-41-dad093d8c53f> in <module>
----> 1 random.sample(lst,10)

In [44]: random.sample([1,1],2)  #这个比较特殊，所谓不同元素，这里虽然值一样，但是索引不同
Out[44]: [1, 1]

#这个样本空间，虽然都是一样的小球，但是不同的，就像世界上没有一样的一片叶子一个道理

#区别：
In [45]: random.sample([1,2,3,4],2) #执行1次

In [46]: random.choice([1,2,3,4]) #执行2次  这个操作可能把一个元素取了两次，而上面那个不可能把一个元素取两次，因为它不重复

```
