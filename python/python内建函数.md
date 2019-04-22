## python内建函数
### 内建函数
`内建函数名不是关键字，所以可以被覆盖的，，覆盖后就在该程序内就无法使用了，请注意使用，比如写了sum=1，这后面这个sum内建函数就不以使用了`
`有的内建函数看起来像函数，但是是class，比如int等`
    * 标识id
        * 返回对象的唯一标识，CPython返回内存地址
    * 哈希 hash()
        * 返回一个对象的哈希值
        `hash函数里面实现了一个hash算法，这个hash算法可以帮助将这个可hash对象经过hash算法，计算出一个值`
        `幂等性，在同一次运行时，对同一个内容的值反复求hash的话，得到的hash值是一致的`
        `一个函数不一定要返回一个确定的值哦，比如一个函数返回当前时间。`
    * 类型 type()
        * 返回对象的类型
        * 获取一个类型的类型
    * 类型转换
        * float() int() bin() hex() oct() bool() list() tuple() dict() set() complex() bytes() bytearray()
        `int(3//2)  int(3/2) 还记得吗？`
    * 输入input([prompt])
        * 接收用户输入，返回一个字符串
    * 打印print(*objects,sep='',end='\n',file=sys.stdout,flush=False)
        * 打印输出，默认使用空格分割，换行结尾，输出到控制台
    * 对象长度 len(s)
        * 返回一个集合类型的元素个数 （盒子里面的元素个数不代表盒子的大小，所以len函数并不能求的这个数据结构在内存中的实际大小，我们往往关心的是元素个数，不关心数据结构的大小，但是在做优化时就很重要了）
    * isinstance()
        * 判断对象obj是否属于某种类型或者元组中列出的某个类型
        * isinstance(True,int)
    * issubclass(cls,class_or_)
        * 判断类型cls是否是某种类型的子类或元组中列出的某个类型的子类
        * issubclass(bool,int)  ---> True

    * 绝对值abs(x) x为数值
    * 最大值max()  最小值min()   ：(一般情况下不同类型间不能比较大小,所以 max(1,range(2))  ---> error )
        * 返回可迭代对象中最大或最小值
        * 返回多个参数中最大或最小值
```python
In [408]: max(*range(10),*range(100,117))                                                                                        
Out[408]: 116
In [409]: max(range(100,117))                                                                                                    
Out[409]: 116
```
    * round(x) 四舍六入五取偶，round(-0.5)
    * pow(x,y) 等价于 x**y
    * range(stop) 从0开始到stop-1的可迭代对象；range(strat,stop[,step])从start开始到stop-1结束步长为step的可迭代对象
    * divmod(x,y) 返回一个tuple   等价于 tuple(x//y,x%y)  
```python
#解构出来得到值，很方便的
In [168]: divmod(13,2)                                                                               
Out[168]: (6, 1)

In [169]: a,b = divmod(13,2)                                                                         

In [170]: a,b                                                                                        
Out[170]: (6, 1)

In [171]: a                                                                                          
Out[171]: 6

In [172]: b                                                                                          
Out[172]: 1
```
    * sum(iterable[,start])对可迭代对象的所有数值元素求和
        * sum(range(1,100,2))
```python
#example
In [176]: sum(range(5),50)   #base + sum    求和值，后面的50类似一个基数                                                                         
Out[176]: 60

sum({range(5)},50)      #error  {}无法构造一个字典
sum(set(range(5)),50)   #right  set() 可以构造一个字典 构造器可以帮我们将一个可迭代对象转化我我们指定的类型
sum(range(1,100,2))   #求100以内奇数和
```
    * chr(i) 给一个一定范围的整数返回对应的字符   #char
        chr(97)    chr(20013)
    * ord(c)  返回字符对应的整数，返回的是Unicode
        ord('a')  ord('中')
```python
In [177]: '啊'.encode()     #bytes utf-8                                                                        
Out[177]: b'\xe5\x95\x8a'

In [178]: '啊'.encode(encoding='gbk')   #gbk                                                             
Out[178]: b'\xb0\xa1'

In [179]: ord('啊')           #unicode                                                                        
Out[179]: 21834

In [180]: hex(21834)                                                                                 
Out[180]: '0x554a'
```

    * str()、repr()、ascii()后面说
 ```python
In [185]: str(123)   #字符串强制类型转换，  > 在python中我们这么理解：获取一个对象的字符串表达形式，给人看的                                                                                
Out[185]: '123'   #由一个字节的数字123，转换成了3个字节的字符串。不划算

In [182]: str(range(10))    #这个可以理解成为，range(10),你有没有字符串的表达形式，给人看的，它说有，然后给出来了，但是应该不是我们希望的                                                                       
Out[182]: 'range(0, 10)'

In [184]: str(list())  #list()你有没有字符串的表达形式呢？                                                                             
Out[184]: '[]'         #有 --- ‘[]’
 ```   

    * sorted(iterable[,key][,reverse])排序  ----> 新列表
        * 立即返回一个新的列表，默认升序
        * reverse是反转
        sorted([1,3,5])
        sorted([1,3,5],reverse=True)
        sorted({'c':1,'b':2,'a':1})
```python
#example
In [196]: l1                                                                                         
Out[196]: [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

In [200]: l2 = sorted(l1,reverse=True)  #立即返回，new出来一个列表，其中待排序数据必须能够比较大小，如果不能比较大小，会出错的

In [199]: id(l1),id(l2)                                                                              
Out[199]: (139803452669704, 139803539985224)

In [206]: l3 = l2 + ['1'] 
In [207]: l3                                                                                         
Out[207]: [9, 8, 7, 6, 5, 4, 3, 2, 1, 0, '1']
In [208]: sorted(l3)   #error
#为了解决不同类型之间非要排序的问题，提供了一个参数，key是函数，这个函数就可以把元素强制类型转换为你指定的类型,但转换后的结果只是用来比较大小的，不改变最后生成的列表中的元素本身
#  sorted(l3,key=str)   sorted(l3,key=int)如果写成int的话，l3里面的元素要能够转换成int才可以，如果不可以转换为int会出错的
In [209]: sorted(l3,key=str)      #1、所有元素转化为str来比较大小  2、只是改变了元素的顺序而已                                                                 
Out[209]: [0, 1, '1', 2, 3, 4, 5, 6, 7, 8, 9]
#看看
In [203]: l3 = (x for x in range(10))                                                                

In [204]: l3                                                                                         
Out[204]: <generator object <genexpr> at 0x7f26873f8990>

In [205]: sorted(l3,reverse=True)                                                                    
Out[205]: [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
##
#构造一个字典看看，什么情况下会去重
In [217]: sorted({x:200 for x in l3},key=str)     #这个key=str只是临时的，生成字典不会去重                                                   
Out[217]: [0, 1, '1', 2, 3, 4, 5, 6, 7, 8, 9]

In [218]: sorted({str(x):200 for x in l3})                   #注意下，这是强制转换成了字符串  构造字典过程中重复的x被去掉                                      
Out[218]: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']

sorted({str(x):200 for x in l3}，key=int)  #这样呢，注意理解   
```

    * 翻转reversed(seq)  #seq意思是序列
        * 返回一个翻转元素的迭代器
        list(reversed("13579"))
        {reversed((2,4))} #有几个元素？  #一个，一般不这样写，使用构造器dict()、set()等等  这里返回 {<reversed at 0x7fae95715b70>}。   set(reversed((2,4))) -->{2, 4}
        for x in reversed(['c','b','a']):
            print(x)
        reversed(sorted({1,5,9}))

 ```python
In [227]: lst                                                                                        
Out[227]: [5, 8, 3, 0, 7, 9, 2, 6, 4, 1]

In [228]: g = (lst[x] for x  in range(-1,-len(lst)-1,-1))     #就是这个技术                                       

In [229]: for i in g: 
     ...:     print(i) 
     ...:                                                                                            
1
4
6
2
9
7
0
3
8
5

In [233]: reversed(set(range(10)))  #error 因为set无序，无法倒转  TypeError: 'set' object is not reversible   字典的返回TypeError: 'dict' object is not reversible
In [232]: reversed(range(10))                                                                        
Out[232]: <range_iterator at 0x7f26871ebc90>  #生成了一个迭代器，惰性的

In [234]: r = reversed(range(10))                                                                    

In [235]: next(r)                                                                                    
Out[235]: 9

#
In [238]: { reversed((2,4))}    #生成一个元素的字典                                                                     
Out[238]: {<reversed at 0x7f26871c5d30>}

In [243]: list( reversed((2, 4)))                                                                    
Out[243]: [4, 2]

In [242]: set( reversed((2, 4)))                                                                     
Out[242]: {2, 4}  #set无序的，所以出来的不是4,2
##
In [244]: g = reversed(sorted({1, 5, 9}))   #sorted返回一个列表升序的，reversed将其倒转过来，返回一个迭代器                                                         

In [245]: next(g)                                                                                    
Out[245]: 9

In [246]: next(g)                                                                                    
Out[246]: 5

In [247]: next(g)                                                                                    
Out[247]: 1

#为了看效果，我们往往在外面再套一个list看看，程序里面一般不这样写 ，写在for循环里面，但是如果又要生成一个的话，就把for写成生成器里了
In [248]: list(reversed(sorted({1, 5, 9})))                                                          
Out[248]: [9, 5, 1]

In [254]: g = (x**2 for x in reversed(sorted({1, 5, 9})))   #我们一般这样写，惰性的，                                         

In [255]: next(g)                                                                                    
Out[255]: 81

In [256]: next(g)                                                                                    
Out[256]: 25

In [262]: for x in (x**2 for x in reversed(sorted({1, 5, 9}))): #经常使用
     ...:     print(x) 
     ...:                                                                                            
81
25
1

 ```   
    
    * 枚举enumerate(seq,start=0)   ----> 二元组
        * 迭代一个序列，返回索引数字和元素构成的二元组
        * start表示索引开始的数字，默认是0
        for x in enumerate([2,4,6,8]):
            print(x)

        for x in enumerate("abcde"):
            print(x,end=" ") 

```python
In [263]: l3                                                                                         
Out[263]: [9, 8, 7, 6, 5, 4, 3, 2, 1, 0, '1']

In [264]: for x in enumerate(l3): 
     ...:     print(x)    
     ...:                                                                                            
(0, 9)
(1, 8)
(2, 7)
(3, 6)
(4, 5)
(5, 4)
(6, 3)
(7, 2)
(8, 1)
(9, 0)
(10, '1')

#
In [267]: e = enumerate(reversed(range(10)))                                                         

In [268]: next(e)                                                                                    
Out[268]: (0, 9)

In [269]: next(e)                                                                                    
Out[269]: (1, 8)

In [270]: for i,x in enumerate(reversed(range(10)),10): 
     ...:     print(i,x) 
     ...:                                                                                            
10 9
11 8
12 7
13 6
14 5
15 4
16 3
17 2
18 1
19 0

In [271]: for i,x in enumerate(reversed(range(10)),-10):   #enumerate可以用来索引
     ...:     print(i,x) 
     ...:                                                                                            
-10 9
-9 8
-8 7
-7 6
-6 5
-5 4
-4 3
-3 2
-2 1
-1 0

#
#比较下面两个
In [275]: l5 = list(range(10))                                                                       

In [276]: [x for x in enumerate(l5, -5)]     # 1                                                         
Out[276]: 
[(-5, 0),
 (-4, 1),
 (-3, 2),
 (-2, 3),
 (-1, 4),
 (0, 5),
 (1, 6),
 (2, 7),
 (3, 8),
 (4, 9)]

In [277]: list(enumerate(l5,-5))    # 2   这两个的效果是一样的，                                                                  
Out[277]: 
[(-5, 0),
 (-4, 1),
 (-3, 2),
 (-2, 3),
 (-1, 4),
 (0, 5),
 (1, 6),
 (2, 7),
 (3, 8),
 (4, 9)]

#两个这里的功能一样的，但是1 的那个可以做复杂计算,比如
[x+1 for x in enumerate(l5, -5)]   #x是个元组哦，试试得行不
或者解构
[x for i,x in enumerate(l5, -5)]
In [278]: [x for i,x in enumerate(l5, -5)]                                                           
Out[278]: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```


    * 迭代器和取元素iter(iterable)、next(iterable[,default])
        * iter 将一个可迭代对象封装成一个迭代器
        * next对一个迭代器取下一个元素。如果全部元素都取过了，再次next会抛StopIteration异常
        it = iter(range(5))
        next(it)

        it=reversed([1,3,5])
        next(it)
`在python中迭代器需要支持迭代器协议，所以next(range(5)) 是错的，需要用iter来封装一下`
### 可迭代对象
    * 可迭代对象
        * 能够通过迭代一次次返回不同的元素的对象 (不同位置的)
            * 所谓相同，不是指 值是否相同，而是元素在容器中是否是同一个，例如列表中值可以重复的，['a','a'],虽然这个列表有2个元素，值一样，但是两个‘a’ 是不同的元素，因为不同的索引
        * 可以迭代，但是未必有序，未必可索引
        * 可迭代对象有：list、tuple、string、bytes、bytearray、range对象、set、dict、生成器、迭代器等
        * 可以使用成员操作符in、not in，in本质上对于线性结构就是在遍历对象，非线性结构求hash
        3 in range(10)    --- O(n)
        3 in (x for x in range(10))   ----- O(n)
        3 in {x:y for x,y in zip(range(4),range(4,10))}   ------O(1)
 
### 迭代器
    * 迭代器
        * 特殊的对象，一定是可迭代对象，具备可迭代对象的特征
        * 通过iter方法把一个可迭代对象封装成迭代器
        * 通过next方法，迭代 迭代器对象
        * 生成器对象，就是迭代器对象
        #迭代器可能无限次的迭代，如生成器。
        for x in iter(range(10))  #这里就没必要再包装一次了，因为range也是可迭代对象
            print(x)

        g = ( x for x in range(10))
        print(type(g))
        print(next(g))
        print(next(g))

### 拉链函数zip(*iterables)
    * 拉链函数zip(*iterables)  
        * 像拉链一样，把多个可迭代对象合并在一起，返回一个迭代器
        * 将每次从不同对象中取到的元素合并成一个元组
        list(zip(range(10),range(10)))
        list(zip(range(10),range(10),range(5),range(10)))

        dict(zip(range(10),range(10)))
        {str(x):y for x,y in zip(range(10),range(10))}
```python
In [282]: zip(range(10))                                                                             
Out[282]: <zip at 0x7f268c011208>

In [284]: z = zip(range(10))                                                                         

In [285]: next(z)                                                                                    
Out[285]: (0,)

In [286]: next(z)                                                                                    
Out[286]: (1,)

In [287]: z = zip(range(10),'abcdefghijk')                                                           

In [288]: next(z)                                                                                    
Out[288]: (0, 'a')

In [289]: next(z)                                                                                    
Out[289]: (1, 'b')

In [290]: {x:y for x,y in zip(range(10),'abcdefjklm')}                                               
Out[290]: 
{0: 'a',
 1: 'b',
 2: 'c',
 3: 'd',
 4: 'e',
 5: 'f',
 6: 'j',
 7: 'k',
 8: 'l',
 9: 'm'}

In [291]: dict(zip('abcdefjklm', range(10)))                                                         
Out[291]: 
{'a': 0,
 'b': 1,
 'c': 2,
 'd': 3,
 'e': 4,
 'f': 5,
 'j': 6,
 'k': 7,
 'l': 8,
 'm': 9}

 In [292]: z = zip(range(5),range(5),range(5),'abcde')                                                

In [293]: for x,y,z,m in z: 
     ...:     print(x,y,z,m) 
     ...:                                                                                            
0 0 0 a
1 1 1 b
2 2 2 c
3 3 3 d
4 4 4 e

In [295]: for item in zip(range(5),range(5),range(5),range(3)):  #木桶原理，最少的那个决定有多少
     ...:     print(item) 
     ...:      
     ...:                                                                                            
(0, 0, 0, 0)
(1, 1, 1, 1)
(2, 2, 2, 2)


In [296]: {item[0]:item for item in zip(range(5),range(5),range(5),range(3))}    #字典解析                     
Out[296]: {0: (0, 0, 0, 0), 1: (1, 1, 1, 1), 2: (2, 2, 2, 2)}
```

### all
    * all(iterable)
        * 可迭代对象所有元素都要等效为True，或空的可迭代对象，all函数返回True
        * 一旦可迭代对象有一个元素等效为False，all函数返回False
    * any(iterable)
        * 可迭代对象任意一个元素等效为True，any函数返回True
        * 空可迭代对象或所有元素都等效False，any函数返回False

        lst = [True,{1},[2,3],5.1,'abc']
        print(all(lst),any(lst))
        print(all([]),any([]))
        print(all(lst+[0]),any(lst+[0]))

```python
In [297]: l3                                                                                         
Out[297]: [9, 8, 7, 6, 5, 4, 3, 2, 1, 0, '1']

In [298]: all(l3)    #所有都为True，才为True                                                                                
Out[298]: False

In [304]: l3.extend((str(i) for i in range(10)))                                                     

In [305]: all(l3)                                                                                    
Out[305]: True

In [306]: l3                                                                                         
Out[306]: [8, 7, 6, 5, 4, 3, 2, 1, '1', '0', '1', '2', '3', '4', '5', '6', '7', '8', '9']

In [307]: all([])  #这也是True哦                                                                                  
Out[307]: True

####
In [308]: any([])                                                                                    
Out[308]: False

In [309]: any([1])                                                                                   
Out[309]: True

In [310]: any([1, 0])                                                                                
Out[310]: True

In [311]: any([0, 0])                                                                                
Out[311]: False

#all
def all(iterable):
    for element in iterable:
        if not element:
            return False
    return True


#any
def any(iterable):
for element in iterable:
    if element:
        return True
return False
```

