# python函数
    * python函数
        * 有若干语句组成的语句块、函数名称、参数列表构成，它是组织代码的最小单元
        * 完成一定的功能
    * 函数的作用
        * 结构化编程对代码的最基本的封装，一般按照功能组织一段代码
        * 封装的目的为了复用，减少冗余代码     (总结：代码封装、复用)
        * 代码更加简洁美观、可读易懂
    * 函数的分类
        * 内建函数，如max()、reversed()等
        * 库函数，如math.ceil()等
        * 自定义函数，使用def关键字定义

### 函数定义
```python
def 函数名(参数列表)：  #创建了一个标识符，即函数名字，  函数名指向 函数对象
    函数体(代码块)
    [return 返回值]
```
    * 函数名就是标识符，命名要求一样
    * 语句块必须缩进，约定4个空格
    * python的函数若没有return语句，会隐式返回一个None值
    * 定义中的参数列表称为形式参数，只是一种符号表达式(标识符)，简称形参

### 函数调用     
    * 函数定义，只是声明了一个函数，它不能被执行，需要调用执行
    * 调用的方式，就是函数名后加上小括号，如有必要在括号内填写上参数
    * 调用时写的参数是实际参数，是实实在在传入的值，简称实参
```python
def add(x, y):#函数定义   创建一个标识符  add  指向 函数对象
    result = x +  y #函数体
    return result #返回值

out = add(4, 5) #函数调用，可能有返回值，使用变量接收这个返回值
print(out)  #print函数加上括号也是调用
#---------------------------------------------------
#代码解释：
#定义一个函数add，及函数名是add，接受2个参数
#该函数计算的结果，通过返回值返回，需要return语句
#调用时，通过函数名add后加2个参数，返回值可使用变量接收
#函数名也是标识符，返回值也是值
#定义需要在调用前，也就是说调用时，已经被定义过了，否则抛NameError异常
#函数是可调用的对象，callable()
#看看这个函数是不是通用的？体会一下函数的好处
```
### 函数参数
* 函数在定义时要约定好形式参数，调用时也提供足够的实际参数，一般来说，形参和实参个数要一致(可变参数除外)。

#### 传参方式
* 1、位置传参
    * 定义时def f(x,y,z),调用使用f(1,3,5),按照参数定义顺序传入实参
* 2、关键字传参     (关键字传参，按照形参的名字对应)
    * 定义时def f(x,y,z),调用使用f(x=1,y=3,z=5),使用形参的名字来传入实参的方式，如果使用了形参名字，那么传参顺序就可和定义顺序不同

> 要求位置参数必须在关键字参数之前传入，位置参数是按位置对应的

```python
def f(x, y, z):
    pass

f(z=None, y=10, x=[1])
f((1,), z=6, y=4.1)
f(y=5, z=6, 2)  #错误传参
```

#### 参数缺省值
* 缺省值也称为默认值，可以在函数定义时，为形参增加一个缺省值。其作用：
    * 参数的默认值可以在未传入足够的实参的时候，对没有给定的参数赋值为默认值
    * 参数非常多的时候，并不需要用户每次都输入所有的参数，简化函数调用
```python
def add(x=4, y=5):
    return x + y

#测试调用 add()、 add(x=5)、 add(y=7)、 add(6, 10)、add(6, y=7)、add(x=5, y=6)、add(y=5, x=6)、add(x=5, 6)、add(y=8, 4)、add(11, x=20)
#能否这样定义 def add(x, y=5) 或 def add(x=4, y)?  第二个错误的，因为无缺省参数放在了有缺省参数后面
```

```python
#定义一个函数login，参数名称为host、port、username、password
def login(host='127.0.0.1', port='8080', username='wayne', password='magedu'):
    print('{}:{}@{}/{}'.format(host,port,username,password))

login()
login('192.168.100.3', 80, 'tom', 'tom')
login('192.168.100.3', username='root')
login('192.168.100.3', port=80, password='com')
login('localhost', port=80, password='com')
login(port=80, password='tom', host='www')
```



### 可变参数  
`需求：写一个函数，可以对多个数累加求和`  
```python
def sum(iterable):
    sum = 0
    for x in iterable:
        sum += x
    return sum

print(sum([1,3,5]))
print(sum(range(4)))
#上例，传入可迭代对象，并累加每一个元素
#也可以使用可变参数完成上面的函数。
```
```python
def sum(*nums):
    sum = 0
    for x in nums:
        sum += x
    return sum

print(sum(1,3,5)) #这里的sum(1,3,5)传入的是三个实参，并不是传入的元组哦
print(sum(1,2,3))
```

``python
#定义
In [9]: def sum(*iterable): 
   ...:     result = 0 
   ...:     print(type(iterable),iterable) 
   ...:     for x in iterable: 
   ...:         result += x 
   ...:     return result 
   ...:      
   ...:                                                                                                                          

In [10]: sum (1,3,5)      #将1,3,5  三个实参传到了iterable这个容器里面，这个容器将实参包装成了元组，然后进行遍历加，最后返回                                                                                                        
<class 'tuple'> (1, 3, 5)   #返回的是tuple
Out[10]: 9
```


1. 可变位置参数
    * 在形参前使用 * 表示该形参是可变位置参数，可以接受多个实参
    * 它将收集来的实参组织到一个tuple中  #为什么是tuple呢？因为1、传入的参数不能变；2、传参时的顺序不变，这个参数序是固定的，不能乱
2. 可变关键字参数
    * 在形参前使用 ** 表示该形参是可变关键字参数，可以接受多个关键字参数
    * 它将收集来的实参的名称和值，组织到一个dict中

```python
def showconfig(**kwargs):
    for k,v in kwargs.items():
        print('{}={}'.format(k,v),end=',')

showconfig(host='127.0.0.1',port=8080,username='wayne',password='magedu')

####
In [12]: def showconfig(**kwargs): 
    ...:     print(type(kwargs)) 
    ...:     print(kwargs) 
    ...:                                                                                                                         

In [13]: showconfig(a=1,b=2)                                                                                                     
<class 'dict'>
{'a': 1, 'b': 2}   #还是会把a变为字符串

showconfig(a=1,b=2,1=200) #error  因为传进去后别人都是把a变成了字符串的，且1不能作为标识符的
showconfig(a=1,a=2)   #error  重复传入了
#。。。。。。。。。。。。。。。。。


```
* 混合使用
    * 可否定义为下列方式？
    `def showconfig(username, password, **kwargs)`
    `def showconfig(username, *args, **kwargs)`
    `def showconfig(username, password, **kwargs, *args)` #?

> 总结：  
    * 有可变位置参数和可变关键字参数
    * 可变位置参数在形参前使用一个星号*
    * 可变关键字参数在形参前使用两个星号**
    * 可变位置参数和可变关键字参数都可以收集若干个实参，可变位置参数收集形成一个tuple，可变关键字参数收集形成一个dict
    * 混合使用参数的时候，普通参数需要放到参数列表前面，可变参数要放到参数列表的后面，可变位置参数需要在可变关键字参数之前

```python
#使用举例
def fn(x, y, *args, **kwargs):
    print(x, y, args, kwargs, sep='\n', end='\n\n')

fn(3,5,7,9,10, a=1, b='abc')
fn(3, 5)
fn(3, 5, 7)
fn(3, 5, a=1, b='abc')
fn(x=3, y=8, 7, 9, a=1, b='abc') #?   错在位置传参必须在关键字传参前
fn(7, 9, y=5, x=3, a=1, b='abc') #?   错在7和9已经按照位置传参了，x=3,y=5有重复传参了

```



### keyword-only参数
```python
#先来一段代码
def fn(*args, x, y, **kwargs):
    print(x, y, args, kwargs, sep='\n', end='\n\n')

fn(3,5)
fn(3,5,7)
fn(3,5,a=1,b='abc')
fn(3,5,y=6,x=7,a=1,b='abc')


```
* 在python3之后，新增了keyword-only参数
    * keyword-only参数：在形参定义时，在一个*星号之后，或一个可变位置参数之后，出现的普通参数，就已经不是普通的参数了，称为keyword-only参数

```python
def fn(*args, x):
    print(x, args, sep='\n', end='\n\n')

fn(3,5)
fn(3,5,7)
fn(3,5,x=7)

```
* keyword-only参数，言下之意就是这个参数必须采用关键字传参。
    * 可以认为，上例中，args可变位置参数已经截获了所有位置参数，其后的变量x不可能通过位置传参传入了。

```python
思考：def fn(**kwargs,x) 可以吗?
def fn(**kwargs, x):
    print(x, kwargs, sep='\n', end='\n\n')
#直接语法错误了
#可以认为，kwargs会截获所有关键字传参，就算写了x=5， x也没有机会得到这个值，所以这种语法不存在。
```

* keyword-only 参数另一种形式
    * '*' 星号后所有的普通参数都成了keyword-only参数

```python
def fn(*, x, y):   #这种一个星号的情况，传实参时就不能有多的位置实参传入了，否则报错，比如fn(1,2,3,x=11, y=22)，因为前面的1，2,3没有标识符接
    print(x,y)

fn(x=6, y=7)
fn(y=8, x=9)
```

### 参数的混合使用
```python
#可变位置参数、keyword-only参数、缺省值
def fn(*args, x=5):   
    print(x)
    print(args)
fn()  #等价于fn(x=5)
fn(5)
fn(x=6)
fn(1,2,3,x=10)
```

```python
#普通参数、可变位置参数、keyword-only参数、缺省值
def fn(y, *args, x=5)
    print('x={}, y={}'.format(x, y))
    print(args)

fn() #
fn(5)
fn(5,6)
fn(x=6)#
fn(1,2,3,x=10)
fn(y=17, 2,3,x=10)#
fn(1,2,y=3,x=10)#

```
```python
#普通参数、缺省值、可变关键字参数
def fn(x=5, **kwargs):
    print('x={}'.format(x))
    print(kwargs)
fn()
fn(5)
fn(x=6)
fn(y=3, x=10)
fn(3, y=10)
fn(y=3, z=20)

```
> 参数规则：  
参数列表参数一般顺序是：普通参数、缺省参数、可变位置参数、keyword-only参数(可带缺省值)、可变关键字参数。
注意：
    * 代码应该易读易懂，而不是为难别人
    * 请按照书写习惯定义函数参数


```python
def fn(x, y, z=3, *arg, m=4, n, **kwargs):  #这种比较特殊，是可以的额，m是keyword-only，m,n 带不带缺省值都可以，没用
    print(x, y, z, m, n)
    print(args)
    print(kwargs)

def connect(host='localhost', port='3306', user='admin', password='admin', **kwargs):  #工作中经常干的
    print(host,port)
    print(user,password)
    print(kwargs)
connect(db='cmdb')
connect(host='192.168.1.123', db='cmdb')
connect(host='192.168.1.123', db='cmdb', password='mysql')
```
* 定义最常用参数为普通参数，可不提供缺省值，必须由用户提供。注意这些参数的顺序，最常用的先定义
* 将必须使用名称的才能使用的参数，定义为keyword-only参数，要求必须使用关键字传参
* 如果函数有很多参数，无法逐一定义，可使用可变参数。如果需要知道这些参数的意义，则使用可变关键字参数收集。







### 参数解构

```python
def add(x, y):
    print(x, y)
    return x + y

add(4, 5)
add((4, 5))#
t = 4, 5
add(t[0], t[1])
add(*t)
add(*(4, 5))  #把(4,5)这个结构给解构了
add(*[4, 5])
add(*{4, 5})  #这个解开后那个是4，那个是5 不知道
add(*range(4, 6))  #这样也可以？是的  把那个结构给解构了

add(*{'a':10, 'b':11})   #可以的，相当于add(*{'a':10, 'b':11}.keys())   #add(*{'a':1,'b':2}.items()) --> ('a', 1, 'b', 2)  这也是可以的。！！！最后得到元组
add(*{'a':10, 'b':11}.values()) #这样也是可以的
add(**{'a':10, 'b':11})  #error 因为它解构成了add(a=10,b=11)
add(**{'x':100, 'y':110}) #这个是对的 解构为这样子了add(x=100,y=110)

```
> 参数解构：
* 在给函数提供实参的时候，可以在可迭代对象前使用 * 或者 ** 来进行结构的解构，提取出其中所有元素作为函数的实参
* 使用 * 解构成位置传参
* 使用 ** 解构成关键字传参
* 提取出来的元素数目要和参数的要求匹配

```python
def add(*iterable):
    result = 0
    for x in iterable:
        result += x
    return result

add(1,2,3)
add(*[1,3,5])
add([1,3,5]) #
add(*range(5))
add(range(5))
add((x for x in range(10)))
add(*(x for x in range(10)))
add(1,2,3,*{x for x in range(10)})  #去重吗？
add(1,2,3,*{x for x in range(10)},10)  #对吗？
```
