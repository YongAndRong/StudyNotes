## 字典dict
* key-value键值对的数据的集合
* 可变的、无序的、key不重复  (python中要求key可hash)

### 字典dict定义  初始化
    * d = dict()  或者 d = {}
    * dict(**kwargs) 使用 name=value  #kv对  初始化一个字典  #name是标识符格式，不能打引号，或者必须满足标识符的条件
    * dict(iterable,**kwarg) 使用可迭代对象和name=value对 构造字典，不过可迭代对象的元素必须是一个二元结构  #可迭代的二元组？
        d = dict(((1,'a'),(2,'b'))) 或者 d = dict(([1,'a'],[2,'b'])) #集合做为二元组结构时，并不知道那个作为key，那个作为value，因为是无序的，但是key必须可hash

    * dict(mapping,**kwarg) 使用一个字典构建另一个字典

    * d = {'a':10,'b':20,'c':None,'d':[1,2,3]}

    类方法dict.fromkeys(iterable,value)
        d = dict.fromkeys(range(5))
        d = dict.fromkeys(range(5),0)
> 常用的dict定义    
d = {}  
dict(**kwargs)  
d = {'a':10,'b':20,'c':None,'d':[1,2,3]}  

```python
#example
In [103]: d1 = dict(a=1,b=2)     #d1 = dict(**kwargs) 键值对嘛      #较常用   这种定义一定要注意 = 前面必须是标识符，否则出错                                                                            
In [104]: d1                                                                                                          
Out[104]: {'a': 1, 'b': 2}
In [105]: d2 = {'a': 1, 'b': 2}   #和上面定义方式等价的  较常用

In [107]: d1 = dict([],a=1,b=2)    #  dict(iterable,**kwarg),前面是这种方式的定义，前面是一个可迭代对象，这里是空列表，d1显示出来的没有这个列表的                                                                               

In [108]: d1                                                                                                          
Out[108]: {'a': 1, 'b': 2}
#
##ERROR  错误的，前面的可迭代对象必须是二元组
In [109]: d1 = dict(['c'=3,'d'=4],a=1,b=2)                                                                            
  File "<ipython-input-109-6b156f12821e>", line 1
    d1 = dict(['c'=3,'d'=4],a=1,b=2)
                  ^
SyntaxError: invalid syntax

##正确的方式，如下：
In [111]: d1 = dict([('c',3),['d',4]],a=1,b=2)   #二元组可以是列表，元组等，但是比较麻烦，还不如上面的键值对了                                                                      

In [112]: d1                                                                                                          
Out[112]: {'c': 3, 'd': 4, 'a': 1, 'b': 2}  

In [6]: d2 = dict(([1,2],))  #如果这个样子的话，第二个括号当作元组了，所以需要加个逗号                                                                        

In [7]: d2                                                                                           
Out[7]: {1: 2}

In [8]: d3 = dict([[1,2]])                                                                           

In [9]: d3                                                                                           
Out[9]: {1: 2}

In [24]: d7 = dict([{1,100},{'b',[200]}])        #二元组为set时，里面的元素要求可hash哦，所以有列表报错了                                                      
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-24-48fc033b18fd> in <module>
----> 1 d7 = dict([{1,100},{'b',[200]}])

TypeError: unhashable type: 'list'


In [3]: d = dict([{1,2},{'b',200}])    #在将set作为二元组的时候，谁作为key是不知道的，因为set无序                                                               

In [4]: d                                                                                            
Out[4]: {1: 2, 'b': 200}

In [5]: d2 = dict([(1,2),{'asd',0}])                                                                 

In [6]: d2                                                                                           
Out[6]: {1: 2, 0: 'asd'}
#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
#
##example
In [113]: d2 = {'a': 1, 'b': 2,1:'abc'}     #注意 这个键值对：1:'abc'  ，这里是对的                                                                     

In [114]: d2                                                                                                          
Out[114]: {'a': 1, 'b': 2, 1: 'abc'}

##example
In [115]: d1 = dict([('c',3),['d',4]],a=1,b=2,2=300)     ##这里错了，因为2=300，这里的2是标识符，不符合标识符的规定了                                                              
  File "<ipython-input-115-60506fd42bc1>", line 1
    d1 = dict([('c',3),['d',4]],a=1,b=2,2=300)
                                       ^
SyntaxError: keyword can't be an expression



In [116]: d1 = dict([('c',3),['d',4]],a=1,b=2,a2=300)  #这样a2就符合标识符的规定了

##example
In [117]: d1 = dict([('c',3),['d',4],(1,1)],a=1,b=2,a2=300)     #(1,1)这里就是正确的，因为检查的是key  1在这里是可hash的了，这里的 1 不是标识符了                                                        

In [118]: d1                                                                                                          
Out[118]: {'c': 3, 'd': 4, 1: 1, 'a': 1, 'b': 2, 'a2': 300}


#要求key必须可hash，不重复
In [119]: d1 = dict([('c',3),['d',4],(1,[1])],a=1,b=2,a2=300)   #这样也是对的                                                       

In [120]: d1                                                                                                          
Out[120]: {'c': 3, 'd': 4, 1: [1], 'a': 1, 'b': 2, 'a2': 300}

#****说明，要求key必须是可hash的，value没所谓的

In [121]: d1 = dict([('a',3),['d',4],(1,[1])],a=1,b=2,a2=300)   #这里定义了a两次，a是key，必须不重复，所以会被后面的覆盖，因为这个定义的格式固定了，可迭代对象必须写前面，所以这样了                                                      

In [122]: d1                                                                                                          
Out[122]: {'a': 1, 'd': 4, 1: [1], 'b': 2, 'a2': 300}  #去重了先计算可迭代，而后面的**kwargs必须写在最后，所以最后计算，所以后面计算的覆盖前面的。得此结果
#
#   dict(mapping,**kwarg)   方式构造dict
In [124]: d2 = dict(d1,a=15)                                                               

In [126]: d2                                                                                                          
Out[126]: {'a': 15, 'd': 4, 1: [1], 'b': 2, 'a2': 300}  #前面的被覆盖了

##example
In [127]: d2[1].append(21)   #d2[1] ，根据key 找到该值是一个列表，对列表是可以append的                                                                                         

In [128]: d2                                                                                                          
Out[128]: {'a': 15, 'd': 4, 1: [1, 21], 'b': 2, 'a2': 300}

In [129]: d1                                                                                                          
Out[129]: {'a': 1, 'd': 4, 1: [1, 21], 'b': 2, 'a2': 300}  #但是根据d1构造的字典d2，这种引用类型的值变动了，都变动了，所以如果有引用类型，再次强调，注意使用，别人是拿的地址啊，要拿里面的值得用深拷贝

##    类方法dict.fromkeys(iterable,value)
##        d = dict.fromkeys(range(5))
##        d = dict.fromkeys(range(5),0)
In [130]: dict.fromkeys(range(5))                                                                                     
Out[130]: {0: None, 1: None, 2: None, 3: None, 4: None}  #value默认是None

In [134]: d1 = dict.fromkeys(range(5),'a')                                                                            

In [135]: d1                                                                                                          
Out[135]: {0: 'a', 1: 'a', 2: 'a', 3: 'a', 4: 'a'}

In [136]: d1[1] = 'b'          #只改一个哦                                                                                       
In [137]: d1                                                                                                          
Out[137]: {0: 'a', 1: 'b', 2: 'a', 3: 'a', 4: 'a'}

In [138]: d1 = dict.fromkeys(range(5),[1])                                                                            

In [139]: d1[1].append(2)    #看清楚哦 ，这个效果是不是你想要的  ，一改全改                                                                                        

In [140]: d1                                                                                                          
Out[140]: {0: [1, 2], 1: [1, 2], 2: [1, 2], 3: [1, 2], 4: [1, 2]}

##d1 = dict.fromkeys(range(5),'a')  #但是这种，因为value是字符串的，所以没法像上面那样使用append。还可以是元组哦，但是可以重新赋值撒
In [145]: d1 = dict.fromkeys(range(5),'a')                                                                            

In [146]: d1[1] = 34                                                                                                  

In [147]: d1                                                                                                          
Out[147]: {0: 'a', 1: 34, 2: 'a', 3: 'a', 4: 'a'}  #看，key为1的值改为了34

###
In [149]: dict.fromkeys(range(10),0)     #0为设置默认值为0，本来是None的，现在改为了0                                                                             
Out[149]: {0: 0, 1: 0, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0, 7: 0, 8: 0, 9: 0}  

```
### 字典元素的访问
    * d[key]    #key唯一
        返回key对应的值value   #根据key的hash值，通过这个值去找它对应的value咯
        key不存在抛出KeyError异常

    * get(key[,default])
        返回key对应的值value
        key不存在返回缺省值，如果没有设置缺省值就返回None

    * setdefault(key[,default])
        返回key对应的值value
        key不存在，添加kv对，value设置为default，并返回default，如果default没有设置，缺省为None
```python
#example
In [155]: d1[1]                                                                                                       
Out[155]: 34

In [156]: d1                                                                                                          
Out[156]: {0: 'a', 1: 34, 2: 'a', 3: 'a', 4: 'a'}

In [151]: d1[10]     #key不存在。报异常哦                                                                                                 
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-151-a7f4eba52d3e> in <module>
----> 1 d1[10]

KeyError: 10
###
In [152]: d1.get(1)                                                                                                   
Out[152]: 34

In [153]: d1.get(10)  #key10不存在，但是没有报错 ，实际上返回了None的，但是ipython不会给你看的，cpython会显示                                                                                               
#None可以做为判断依据的哦
In [154]: d1.get(10,-1)      #由于这里key不存在的话，返回值None不给你看，所以我们设置一个-1，告诉他，key不存在的话，返回-1                                                                                         
Out[154]: -1

######testsing
In [157]: d1[1] = None  #将key1的值改为None，但是取它的值是没有显示的，实际上是拿到了的                                                                                              

In [158]: d1[1]                                                                                                       

In [159]: d1                                                                                                          
Out[159]: {0: 'a', 1: None, 2: 'a', 3: 'a', 4: 'a'}
In [160]: print(d1[1])      #这样是可以显示出来的                                                                                          
None  #但是这个值就是None，返回的是None，只是ipython没有out出来而已

In [163]: d1.get(1,-1)  #为什么没有返回显示呢，为什么不是返回的-1呢， 因为d1[1]的value有值，是None，所以这里不理你，不会给你返回-1

####
In [162]: print(d1.get('a'))                                                                                          
   >None  #由于不存在返回的None
### 所以为了区分这两种情况，到底None是什么意思，怎么用的，所以给‘d1.get(10,-1)’ get方法设置了默认的返回值-1

#setdefault(key[,default])  设置缺省值
In [165]: d1.setdefault('a')  #这个更牛了，先看key里有没有值，没有的话，给加进去啊 缺省的value默认为None  。                                                                                      

In [166]: d1                                                                                                          
Out[166]: {0: 'a', 1: None, 2: 'a', 3: 'a', 4: 'a', 'a': None}

In [167]: d1.setdefault('b',1000)   #这个函数是有返回值的，由于上面那个是None，所以ipython没有给你看而已                                                                                  
Out[167]: 1000

In [168]: d1.setdefault('b','bbbbbbb')     #由于刚才有值了，所以这里不会添加了，而是把key ‘b’的值给显示出来 ，缺省值，没用了没用了没用了                                                                          
Out[168]: 1000

In [42]: d.get('f','not existes.')      #这个感觉还可以哦                                                               
Out[42]: 'not existes.'
```
        
### 字典增加和修改
    * d[key] = value
        将key对应的值修改为value  #有则覆盖，没有则添加
        key不存在添加新的kv对

    * update([other])   ---> None
        使用另一个字典的kv对更新本字典
        key不存在，就添加
        key存在，覆盖已经存在的key对应的值
        就地修改
```python
#example
In [170]: d1['1'] = 1    #‘1’ 和1的hash值是不一样的，所以这里区别对待了                                                                                             
In [171]: d1                                                                                                          
Out[171]: {0: 'a', 1: None, 2: 'a', 3: 'a', 4: 'a', 'a': None, 'b': 1000, '1': 1}
###
In [172]: d2                                                                                                          
Out[172]: {'a': 15, 'd': 4, 1: [1, 21], 'b': 2, 'a2': 300}

#In [174]: d2.update('1')  error
#In [175]: d2.update('1':1) error  需要二元组
#In [176]: d2.update('1'=2)  error

In [178]: d2.update(a=2)   #正确的                                                                                  

In [179]: d2                                                                                                          
Out[179]: {'a': 2, 'd': 4, 1: [1, 21], 'b': 2, 'a2': 300}  #覆盖了

In [185]: d2.update([(1,2222)])  #这种可以改 1 哦                                                                                    

In [186]: d2                                                                                                          
Out[186]: {'a': 2, 'd': 4, 1: 2222, 'b': 2, 'a2': 300}

In [188]: d2.update({'e':5000})          #ok的    必须加引号，否则表示变量标识符                                                                         

In [189]: d2                                                                                                          
Out[189]: {'a': 2, 'd': 4, 1: 2222, 'b': 5000, 'a2': 300, 'e': 5000}

In [190]: d2.update({'j':5000,'k':6666})    #ok的，就地更新                                                                           

In [191]: d2                                                                                                          
Out[191]: 
{'a': 2,
 'd': 4,
 1: 2222,
 'b': 5000,
 'a2': 300,
 'e': 5000,
 'j': 5000,
 'k': 6666}

In [43]: d                                                                                           
Out[43]: {'a': 1, 'b': 'b', 'd': None, 'e': 100}

In [44]: d.update({'a':111,'b':222})           #用字典进行更新 ，有的就覆盖掉                                                    

In [45]: d                                                                                           
Out[45]: {'a': 111, 'b': 222, 'd': None, 'e': 100}

In [46]: d.update(([1,2],))          #使用二元组进行更新  ，没有的就新增                                                                

In [47]: d                                                                                           
Out[47]: {'a': 111, 'b': 222, 'd': None, 'e': 100, 1: 2}

d.update(red=1)
d.update((('red',2),))
d.update({'red':3})
```
#*****************************************************************
### 字典删除
    * pop(key[,default])
        key存在，移除它，并返回它的value   #pop(key,"no exists") 试试
        key不存在，返回给定的default
        default未设置，key不存在则抛出KeyError异常
    * popitem()
        移除并返回一个任意的键值对   ---------> 元组的kv对
        字典为empty，抛出KeyError异常
    * clear()

    * del语句
        a = True
        b = [6]
        d = {'a':1,'b':b,'c':[1,3,5]}
        del a
        del d['c'] #删除了一个对象[1,3,5]?
        del b[0]
        c = b
        del c
        del b
    * del a['c'] 看着像删除了一个对象，本质上减少了一个对象的引用，del实际上删除的是名称，而不是对象
    #只是将引用计数减一而已，如果引用计数不为0的话，它 还是存在的，对象的清理时垃圾回收干的





### 字典遍历
    * 遍历不管是根据key还是value，都不高效，因为遍历根据元素量来算的，所以别经常遍历
    for ... in dict  

        遍历key
        for k in d:
            print(k)
        
        for k in d.keys():
            print(k)

        遍历value:
        for k in d:
            print(d[k])

        for k in d.keys():
            print(d.get(k))

        for v in d.values():
            print(v)

        遍历item，即kv对
            for item in d.items():
                print(item)            ------>元组的二元组

            for item in d.items():
                print(item[0],item[1])

            for k,v in d.items():
                print(k,v)

            for k,_ in d.items():
                print(k)

            for _,v in d.items():
                print(v)
```python
#example
In [17]: d2                                                                                                           
Out[17]: {0: 1000, 1: 0, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0, 7: 0}

In [14]: list(d2.items())        #返回一个二元组的列表                                                                                     
Out[14]: [(0, 1000), (1, 0), (2, 0), (3, 0), (4, 0), (5, 0), (6, 0), (7, 0)]

#还可以这样玩
In [64]: d                                                                                           
Out[64]: {'a': 111, 'b': 222, 'd': None, 'e': 100}

In [65]: for item in d.items(): 
    ...:     print(item[0] ,'~~~~~~~',item[1]) 
    ...:                                                                                             
a ~~~~~~~ 111
b ~~~~~~~ 222
d ~~~~~~~ None
e ~~~~~~~ 100
#--------还不如用for k,v in d.items()

In [15]: list(d2.values())                                                                                            
Out[15]: [1000, 0, 0, 0, 0, 0, 0, 0]

In [16]: list(d2.keys())                                                                                              
Out[16]: [0, 1, 2, 3, 4, 5, 6, 7]

#--------------------------------------------
In [48]: a,b = {'x':1,'y':4}                                                                         

In [49]: a,b                                                                                         
Out[49]: ('x', 'y')  #这种情况a,b的值是不确定的，因为字典是无序的嘛，所以a可能是x，也可能是y

In [70]: type(d.keys())    #这些都是可迭代对象                                                                            
Out[70]: dict_keys

In [71]: type(d.values())                                                                            
Out[71]: dict_values

In [72]: type(d.items())                                                                             
Out[72]: dict_items
#
In [76]: 'a' in d.keys()       #时间复杂度是O(1)                                                                       
Out[76]: True

In [77]: 111 in d.values()    #时间复杂度O(n)                                                                       
Out[77]: True

In [78]: ('a',111) in d.items()      #时间复杂度是O(n)                                                                
Out[78]: True

```



### 总结
    * python3中，keys、values、items方法返回一个类似一个生成器的可迭代对象，不会把函数的返回结果复制到内存中
        * 返回Dictionary view对象，可以使用len()、iter()、in操作
        * 字典的entry的动态的视图，字典变化，视图将反映出这些变化
        * keys返回一个类set对象，也就是可以看做一个set集合
        * 如果values都可以hash，那么items也可以看做是类set对象
    * python2中，上面的方法会返回一个新的列表，占据新的内存空间。所以python2建议使用iterkeys、itervalues、iteritems版本，返回一个迭代器，而不是返回一个copy

### 字典遍历和移除
    * 如何在遍历的时候移除元素
    错误的做法：
        d = dict(a=1,b=2,c='abc')
        for k,v in d.items():
            d.pop(k) #异常，在迭代的过程中改变了字典的大小 #其实第一个kv对是被删除了的？    新增也是会加进去的，只是在加第二个kv的时候，由于size变了，会报错

        while len(d):   #相当于情况，不如直接clear()
            print(d.popitem())

        while d:
            print(d.popitem())
    正确的做法：
        d = dict(a=1,b=2,c='abc')
        keys = []

        for k,v in d.items():
            if isinstance(v,str):
                keys.append(k)
        
        for k in keys:
            d.pop(k)
        print(d)
> 对列表的增删，使用while循环
  对字典的增删，请使用上面的方法
```python
#
In [88]: d                                                                                           
Out[88]: {'b': 222, 'd': None}

In [89]: while d: 
    ...:     d.popitem()   #这样ok的，清空列表。类似clear() 
    ...:                                                                                             

In [90]: d                                                                                           
Out[90]: {}

 ```

### 字典的key
    * key的要求和set的元素要求一致
        set的元素可以就是看做key，set可以看做dict的简化版
        hashable可哈希才可以作为key，可以使用hash()测试
        d = {1:0,2.0:3,"abc":None,('hello','world','python'):"string",b'abc':'135'}

### defaultdict
    * collections.defaultdict([default_factory[,...]]) #缺省工厂
        * 第一个参数是default_factory,缺省是None，它提供一个初始化函数。当key不存在的时候，会调用这个工厂函数来生成key对应的value
        * 构造一个字典，values是列表，为其添加随机个元素
            import random
            d1 = {}
            for k in 'abcdef':
                for v in range(random.randint(1,5)):
                    if  v not  in d1.keys():
                        d1[k] = []
                    d1[k].append(v)
                    #d1.setdefault(k,[]).append(v)
                print(d1)


            from collections import defaultdict
            import random

            d1 = defaultdict(list)  #括号里面是函数名称，我们称其为构造器,还可以是set，如果是set的话，就必须是add方法了，不应该是append方法了。如果函数后面跟一个()的话就叫函数调用了
            for k in 'abcdef':
                for v in range(random.randint(1,5)):
                    d1[k].append(v)  #defaultdict会自动给你创建一个list，所以这里就可以用append方法了
                print(d1)

```python
In [9]: d                                                                                            
Out[9]: 
defaultdict(list,
            {'a': [0, 1, 2, 3, 4],
             'b': [0, 1, 2, 3],
             'c': [0, 1, 2],
             'd': [0, 1, 2],
             'e': [0, 1, 2]})

In [11]: d1 = defaultdict(set)                                                                       

In [12]: for k in 'xyz': 
    ...:     for v in range(random.randint(1,5)): 
    ...:         d1[k].add(v) 
    ...:                                                                                             

In [13]: d1                                                                                          
Out[13]: defaultdict(set, {'x': {0, 1}, 'y': {0, 1, 2, 3}, 'z': {0}})
```


### OrderedDict
    * collections.OrderedDict([items])
        * key并不是按照加入的顺序排列，可以使用OrderedDict 记录顺序
```python
from collections import OrderedDict
import random

d = {'banana':3,'apple':4,'pear':1,'orange':2}
print(d)
keys = list(d.keys())
random.shuffle(keys)
print(keys)

od = OrderedDict()  #定义一个有序字典

for key in keys:
    od[key] = d[key]
print(od)
print(od.keys())

```
    * 有序字典可以记录元素插入的顺序，打印的时候也是按照这个顺序输出打印
    * 3.6 版本的python的字典就是记录key插入的顺序(IPython不一定有效果)

    * 应用场景
        * 假如使用字典记录了N个产品，这些产品使用ID由小到大加入到字典中
        * 除了使用字典检索的遍历，有时候需要取出ID，但是希望是按照输入的顺序，因为输入顺序是有序的
        * 否则还需要把遍历到的值排序





