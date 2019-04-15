# python解析式、生成器
## 标准库datetime
    * datetime模块
        * 对日期、时间、时间戳的处理
        * datetime类
            * 类方法  (构造时间对象)
                today():  返回本地时区当前时间的datetime对象
                now(tz=None) ：   返回当前时间的datetime对象，时间到微秒，如果tz为None，返回和today()一样
                utcnow()：  没有时区的当前时间
                fromtimestamp(timestamp,tz=None) : 从一个时间戳返回一个datetime对象

            * datetime对象 (的方法)
                * timestamp() ：  返回一个到微秒的时间戳 （浮点数）
                    时间戳：格林威治时间1970年1月1日0点到现在的秒数
                * 构造方法 datetime.datetime(2016,12,6,16,29,43,79043)

                * year、month、day、hour、minute、second、microsecond,取datetime对象的年月日时分秒及微秒
                * weekday() 返回星期的天，周一：0，周日：6
                * isoweekday() 返回星期的天，周一：1，周日：7
                * date()   返回日期date对象
                * time()  返回时间time对象
                * replace()  修改并返回新的时间
                * isocalendar()   返回一个三元组(年，周数，周的天)



```python
#example
In [15]: datetime.datetime.now()    #返回当前时区时间的对象                                                                 
Out[15]: datetime.datetime(2019, 4, 1, 0, 36, 28, 755929)

In [18]: datetime.datetime.utcnow()      #utc的                                                             
Out[18]: datetime.datetime(2019, 4, 10, 7, 28, 8, 371072)

In [25]: d1.timestamp()     #返回一个时间戳      全世界的同一个时间点的时间戳肯定是一样的        ，时间戳是没有时区的概念的                                                           
Out[25]: 1554881468.872571

In [26]: datetime.datetime.fromtimestamp(d1.timestamp())        #根据时间戳返回一个datetime对象  ，他又返回了我们这个时区的时间，因为他在构造时间的时候，又构造成了跟我们时区相关的时间                                   
Out[26]: datetime.datetime(2019, 4, 10, 15, 31, 8, 872571)

In [27]: datetime.datetime.fromtimestamp(1554881468)                                                 
Out[27]: datetime.datetime(2019, 4, 10, 15, 31, 8

#example  构造时间
In [28]: d4 = datetime.datetime(2017,1,1)                                                            

In [29]: d4                                                                                          
Out[29]: datetime.datetime(2017, 1, 1, 0, 0)

In [30]: d4 = datetime.datetime(2017,1,1,12,1,3)                                                     

In [31]: d4                                                                                          
Out[31]: datetime.datetime(2017, 1, 1, 12, 1, 3)

In [33]: datetime.datetime(2019,04,12,21,32,30)  #这样写就是错误的，因为有无意义的0了
#example 属性
In [32]: d4.year,d4.month,d4.day                                                                     
Out[32]: (2017, 1, 1)

#example 方法
In [34]: d4.weekday()                                                                                
Out[34]: 6

In [35]: d4.isoweekday()                                                                             
Out[35]: 7

In [36]: d4.date()           #返回日期                                                                        
Out[36]: datetime.date(2017, 1, 1)

In [37]: d4.time()           #返回时间                                                                        
Out[37]: datetime.time(12, 1, 3)

In [38]: d4.replace(2019)                                                                            
Out[38]: datetime.datetime(2019, 1, 1, 12, 1, 3)  #返回时间对象，原有时间对象并未改变   #这个方法有时会用

In [40]: d4.replace(d4.year - 3)   #灵活处理                                                                  
Out[40]: datetime.datetime(2014, 1, 1, 12, 1, 3)
```


### 时间格式化

        * 日期格式化 *
            * 类方法 strptime(date_string,format),返回datetime对象  #解析str ----> datetime对象
            * 对象方法strftime(format),返回字符串                   #datetime对象----> str
            * 字符串format函数格式化
```python
import datetime
dt = datetime.datetime.strptime("21/11/06 16:30", "%d/%m/%y %H:%M")
print(ds.strftime("%Y-%m-%d %H:%M:%S"))
print("{0:%Y}/{0:%m}/{0:%d}{0:%H}::{0:%S}".format(dt))
print('{:%Y-%m-%d %H:%M:%S}'.format(dt))
```
```python
#example
In [41]: dt = datetime.datetime.strptime('21/11/06 16:30', '%d/%m/%y %H:%M')  #这个操作需要注意到， （ '%d/%m/%y %H:%M'   ）它的格式必须和前面的数字对应，连空格都必须一致                  

In [42]: dt                                                                                          
Out[42]: datetime.datetime(2006, 11, 21, 16, 30)

In [43]: dn = datetime.datetime.strptime("2009, 5, 2, 16, 29, 39", "%Y, %m, %d, %H, %M, %S")         

In [44]: dn                                                                                          
Out[44]: datetime.datetime(2009, 5, 2, 16, 29, 39)

#example 
In [47]: d1                                                                                          
Out[47]: datetime.datetime(2019, 4, 10, 15, 31, 8, 872571)

In [48]: d1.strftime("%y-%m-%d %H:%M:%S")                                                            
Out[48]: '19-04-10 15:31:08'
#日常中，为了方便存储或者传输，我们都要将时间转换为字符串，当我们在文本文件中年拿到这些个字符串后再将其转换为时间对象，然后用时间对象的方法对其进行操作。++--等

```
        * timedelta 对象
            * datetime2 = datetimie1 + timedelta
            * datetime2 = datetime1 - timedelta
            * timedelta = datetime1 - datetime2
        构造方法：
            datetime.timedelta(days=0,seconds=0,microseconds=0,milliseconds=0,minutes=0,hours=0,weeks=0)
            year = datetime.timedelta(days=365)
        * total_seconds() 返回时间差的总秒数
```python
#example
In [54]: d2 + datetime.timedelta(days=365)    #增加365天                                                       
Out[54]: datetime.datetime(2020, 4, 9, 16, 11, 0, 312422)

In [55]: d2                                                                                          
Out[55]: datetime.datetime(2019, 4, 10, 16, 11, 0, 312422)

In [56]: d2 + datetime.timedelta(days=365,hours=12)                                                  
Out[56]: datetime.datetime(2020, 4, 10, 4, 11, 0, 312422)


In [57]: datetime.timedelta(days=365,hours=12).total_seconds()     #时间差对象，有一个   total_seconds() 方法                               
Out[57]: 31579200.0

```



    ### time标准库
    * time
        time.sleep(secs)   将调用线程挂起指定的秒数    #多线程用的较多



## 列表解析式

    * 举例
        生成一个列表，元素0-9，对每一个元素自增1后求平方返回新列表
        l1 = list(range(10))
        l2 = []
        for i in l1:
            l2.append((i+1)**2)
        print(l2)
    * 列表解析式
        l1 = list(range(10))
        l2 = [(i+1)**2 for i in l1]
        print(l2)
        print(type(l2))

    * 语法
        * [返回值 for  元素  in 可迭代对象 if 条件]
        * 使用中括号[]，内部是for循环，if条件语句可选
        * 返回一个新的列表
    * 列表解析式是一种语法糖
        * 编译器会优化，不会因为简写而影响效率，反而因优化提高了效率
        * 减少程序员工作量，减少出错
        * 简化了代码，但可读性增强
```python
#example
#获取10以内的偶数，比较执行效率
even = []
for x in range(10):
    if x%2 == 0:
        even.append(x)

#2
even = [x for x in range(10) if x%2 == 0]
even = [x for x in range(10) if not x%2]

```
    * 思考：
        * 有这样的赋值语句newlist = [print(i) for i in range(10)],请问newlist的元素打印出来是什么？
        * 获取20以内的偶数，如果同时3的倍数也打印[i for i in range(20) if i%2 == 0 elif i%3 == 0]行吗？

* [expr for item in iterable if cond1 if cond2]   
* 等价于  
```python
    ret = []  
    for item in iterable:  
        if cond1:  
            if cond2:  
                ret.append(expr)  
```
```python
#example
#20以内，即能被2整除又能被3整除的数
[ i for i in range(20) if i%2==0 and i%3==0]
[ i for i in range(20) if i%2==0 if i%3==0]
```
* [ expr for i in iterable1 for j in iterable2 ]
等价于  
```python
ret = []
for i in iterable1:
    for j in iterable2:
        ret.append(expr)
```
    * 举例
```python
[ (x,y) for x in 'abcde' for y in range(3) ]
[ [x,y] for x in 'abcde' for y in range(3) ]
[ {x:y} for x in 'abcde' for y in range(3) ]
```
#列表解析式进阶
    * 请问下面3中输出各是什么？为什么
```python
[(i,j) for i in range(7) if i>4 for j in range(20,25) if j>23 ]
[(i,j) for i in range(7) for j in range(20,25) if j>23 if i>4 ]
[(i,j) for i in range(7) for j in range(20,25) if j>23 and i>4 ]
```



# 生成器表达式 Generator expression  
    * 语法
        * (返回值 for 元素 in 可迭代对象  if  条件 )
        * 列表解析式的中括号换成小括号就行了
        * 返回一个生成器  (生成器对象)
    * 和列表解析式的区别
        * 生成器表达式是按需计算(或称惰性求值、延迟计算)，需要的时候才计算值
        * 列表解析式是立即返回值
    * 生成器
        * 可迭代对象
        * 迭代器
    
    * 举例

> 迭代器一定是可迭代对象，但是可迭代对象不一定是迭代器   
生成器和迭代器是不同的对象，但都是可迭代对象  
生成器同时也是个迭代器  迭代器未必是生成器对象  
生成器是特殊的迭代器，它是由生成器表达式和生成器函数生成的迭代器对象，本身也叫生成器对象，它是迭代器  
只要可以用next()去拨一下的都是迭代器    



## 和列表解析式的对比
    * 计算方式
        * 生成器表达式延迟计算，列表解析式立即计算
    * 内存占用
        * 单从返回值本身来说，生成器表达式省内存，列表解析式返回新的列表
        * 生成器没有数据，(当前)内存占用极少，它是使用时一个个返回数据。如果将这些返回的数据合起来占用的内存也和列表解析式差不多。但是，它不需要立即占用这么多内存
        * 列表解析式构造新的列表需要立即占用内存，不管你是否立即使用这么多数据
    * 计算速度
        * 单看计算时间，生成器表达式耗时非常短，列表解析式耗时长
        * 但是生成器本身并没有返回任何值，只返回了一个生成器对象
        * 列表解析式构造并返回了一个新的列表，所以看起来耗时了

### 集合解析式
    语法
        * {返回值  for 元素  in  可迭代对象  if  条件 }
        * 列表解析式的中括号换成了大括号{} 就行了
        * 立即返回一个集合
    用法 
        * {(x,x+1) for x in range(10)}
        * {[x] for x in range(10)}  #error
### 字典解析式
    语法
        * {返回值 for 元素 in 可迭代对象 if 条件 }
        * 列表解析式的中括号换成大括号{}就行了
        * 使用key:value形式
        * 立即返回一个字典
    用法
        {x:(x,x+1) for x in range(10)}
        {x:[x,x+1] for x in range(10)}
        {(x,):[x,x+1] for x in range(10)}
        {[x]:[x,x+1] for x in range(10)}
        {chr(0x41+x):x**2 for x in range(10)}
        {str(x):y for x in range(3) for y in range(4)}  #输出多少个元素？

### 字典解析式
    用法
    {str(x):y for x in range(3) for y in range(4)}
    等价于
        for x in range(3):
            for y in rnage(4):
                ret[str(x)] = y


# 总结
    python2 引入列表解析式
    python2.4 引入生成器表达式
    python3 引入集合、字典解析式，并迁移到了2.7

    一般来说，应该多应用解析式，简短、高效
    如果一个解析式非常复杂，难以读懂，可以考虑拆解成for循环

    生成器和迭代器是不同的对象，但都是可迭代对象
    可迭代对象范围更大，都可以使用for循环遍历






