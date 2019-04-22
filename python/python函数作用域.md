## 函数作用域
### 函数返回值
```python
#先看几个例子
#return 语句之后可以执行吗？
def showplus(x):
    print(x)
    return x+1
    print('~~end~~') # return 之后会执行吗？

showplus(5)

#多条return语句都会执行吗
def showplus(x):
    print(x)
    return x + 1
    return x + 2

showplus(5)


#下例多个return可以执行吗？
def guess(x):
    if x >3:
        return ">3"
    else:
        return "<3"
print(guess(10))


#下面函数执行的结果是什么
def fn(x):
    for i in range(x):
        if i > 3:
            return i
    else:
        print("{} is not greater than 3".format(x))
print(fn(5))
print(fn(3))
```
> 总结：
    * python函数使用return语句返回“返回值”
    * 所有函数都有返回值，如果没有return语句，隐式调用return None
    * return语句并不一定是函数的语句块的最后一条语句
    * 一个函数可以存在多个return语句，但是只有一条可以被执行。如果没有一条return语句被执行到，隐式调用return None
    * 如果有必要，可以显示调用return None，可以简写为return
    * 如果函数执行了return语句，函数就会返回，当前被执行的return语句之后的其他语句就不会被执行了
    * 返回值的作用： 结束函数调用、返回“返回值”

```python
#能够一次返回多个值吗？
def showvalues():
    return 1,3,5

showvalues()  #返回了多个值吗

```
> 小计：
    * 函数不能同时返回多个值
    * return 1,3,5 看似返回多个值，隐式的被python封装成了一个元组
    * x, y, z = showlist() 使用解构提取返回值更为方便




## 函数作用域 ***
### 作用域
* 一个标识符的可见范围，这就是标识符的作用域。一般常说的是变量的作用域
```python
def foo():
    x = 100

print(x) #可以访问到吗
```
> 分析：
上例中x不可以访问到，会抛出异常(NameError:name 'y' is not defined), 原因在于函数是一个封装，它会开辟一个作用域，x变量被限制在这个作用域中，所以在函数外部x变量不可见。  
注意：每一个函数都会开辟一个作用域

### 作用域分类
* 全局作用域
    * 在整个程序运行环境中都可见
    * 全局作用域中的变量称为全局变量
* 局部作用域
    * 在函数、类等内部可见
    * 局部作用域中的变量称为局部变量，其使用范围不能超过其所在局部作用域
```python
# 局部变量
def fn1():
    x = 1  #局部作用域，x 为局部变量，使用范围在fn1内

def fn2():
    print(x) #x能打印吗？可见吗？why？
print(x)  #x能打印吗？可见吗？why？
```
```python
#全局变量
x = 5 #全局变量，也在函数外定义
def foo():
    print(x) #可见吗？why？

foo()
```
> 一般来讲外部作用域变量在函数内部可见，可以使用  
反过来，函数内部的局部变量，不能在函数外部看见  
(标识符就是变量，函数名也是标识符，所以函数名也是变量，函数名指向函数对象)

### 函数嵌套
* 在一个函数中定义了另外一个函数

```python
def outer():
    def inner():
        print("inner")
    print("outer")
    inner()
outer()
inner()
```
> 内部函数inner不能再外部直接使用，会抛NameError异常，因为它在函数外部不可见。
其实，inner不过就是一个标识符，就是一个函数outer内部定义的变量而已。

### 嵌套结构的作用域
* 对比下面嵌套结构， 代码执行的效果
```python
def outer1():
    o = 65
    def inner():
        print("inner {}"format(o))
        print(chr(o))

    inner()
    print("outer {}".format(o))
outer1()  #执行后，打印什么
```
```python
def outer2():
    o = 65
    def inner():
        o = 97
        print("inner {}"format(o))
        print(chr(o))

    inner()
    print("outer {}".format(o))
outer2()  #执行后，打印什么
```
> 从执行的结果来看：
* 外层变量在你内部作用域可见
* 内层作用域inner中，如果定义了o=97,相当于在当前函数inner作用域中重新定义了一个新的变量o，但是，这个O并不能覆盖掉外部作用域outer2中的变量o.只不过对于inner函数来说，其只能可见自己作用域中定义的变量o了。


### 一个赋值语句的问题

```python
#函数1
x = 5
def foo():
    print(x)

foo()
#正常执行，函数外部的变量在函数内部可见


#函数2
x = 5
def foo():
    y = x + 1 #报错吗
    #x += 1 #打开这句报错吗？why？换成x=1可以不？
    print(x)

foo()
#执行错误吗？
```
> 仔细观察函数2返回的错误指向 x += 1，原因是什么呢？

```python
#几个坑
x = 100

def fn():
    print(x)   #执行到这句的时候，发现x在本函数中有赋值，是local的，作用域是当前函数，所以就拿local x来打印，但是打印时发现x没有值，所以还是报错。注意，这个x并不会去外面拿值来打印哦 。。切记
    x += 200

print(x)
fn()
print(x)


##example

x = 100

def fn():
    print(x)   #这种情况的话，虽然x有值了，但是在使用的时候，x并未定义，所以还是报错
    x = 200

print(x)
fn()
print(x)
```


```python
x = 5
def foo():
    x += 1
foo()  #报错如下：
#——————————————————————————————————————————
---------------------------------------------------------------------------
UnboundLocalError                         Traceback (most recent call last)
<ipython-input-1-36430bfdfe1a> in <module>
      2 def foo():
      3     x += 1
----> 4 foo()

<ipython-input-1-36430bfdfe1a> in foo()
      1 x = 5
      2 def foo():
----> 3     x += 1
      4 foo()

UnboundLocalError: local variable 'x' referenced before assignment

```
> 原因分析：
* x += 1 其实是 x = x + 1
* 相当于在foo内部定义一个局部变量x， 那么foo内部所有x都是这个局部变量x了
* x = x + 1 相当于使用了局部变量x， 但是这个x还没有完成赋值，就被右边拿来做加1操作了
* 如何解决这个常见问题？

### global 语句

```python
x = 5
def foo():
    global x #全局变量
    x += 1
    print(x)
foo() 
```
> 分析：
* 使用globa关键字的变量，将foo内的x声明为使用外部的全局作用域中定义的x
* 全局作用域中必须有x的定义

`如果全局作用域中没有x定义会怎么样？`
* 注意，下面实验如果在ipython、jupyter中做，上下文运行环境中有可能有x的定义，稍微不注意，就测试不出效果
```python
#有错不？
def foo():
    global x
    x += 1
    print(x)

foo()


#有错不？
def foo():
    global x
    x = 10
    x += 1
    print(x)

foo()
print(x) #可以吗？ 可以，因为已经将x申明为了全局变量了
###
def fn():
    global x
    x = 100

fn()
print(x)  #---->x=100了哦，因为申明为了global。赋值即重新定义，但是赋值即定义只针对标识符，不对列表中的元素哦。了解下
#这里是不是意味着函数内的变量在外可见了呢？不是，因为申明为了global了，相当于在对外部变量操作了。
#注意全局变量一般在函数内只是读一下，而不是操作它，改变它。

##
def fn():
    global x
    x += 100

fn()
print(x)   #--->这里是错的，因为x申明为了global，但是在做x +=100时，x没有值，所以错误
```
> 使用global关键字定义的变量，虽然在foo函数中声明，但是这将告诉当前foo函数作用域，这个x变量将使用外部全局作用域中的x。
即使是在foo中又写了x=10，也不会在foo这个局部作用域中定义局部变量x了。
使用了global，foo中的x不再是局部变量了，它是全局变量。
总结：
* x += 1这种特殊形式产生的错误的原因？先引用后赋值，而python动态语言是赋值才算定义，才能被引用。解决办法，在这条语句前增加x=0之类的赋值语句，或者使用global告诉内部作用域，去全局作用域查找变量定义
* 内部作用域使用x=10之类的赋值语句会重新定义局部作用域使用的变量x，但是，一旦这个作用域中使用globa声明x为全局的，那么x=5相当于在为全局作用域的变量x赋值

### global使用原则

* 外部作用域变量会在内部作用域可见，但也不要在这个内部的局部作用域中直接使用，因为函数的目的就是为了封装，尽量与外界隔离
* 如果函数需要使用外部全局变量，请尽量使用函数的形参定义，并在调用传实参解决
* 一句话：不用global。学习它就是为了深入理解变量作用域
```python
y = []

def inc_one():
    y.append(1)
    return y

inc_one()
inc_one()
inc_one()
print(y)
#这种也是使用y的情况也是全局的，尽量不要这样用

#应该传参进去，函数的功能就是处理数据的
y = []

def inc_one(y): #形参y是标识符，就是变量，就是本地变量，是变量就可以改变的
    y.append(1)
    return y

inc_one(y) #这里的y是引用类型，把列表的地址传过去了
inc_one(y)
inc_one(y)
print(y)
```







## 闭包 ***
* 自由变量： 未在本地作用域中定义的变量。例如定义在内层函数外的外层函数的作用域中的变量
* 闭包： 就是一个概念，出现在嵌套函数中，指的是内层函数引用到了外层函数的自由变量，就形成了闭包。很多语言都有这个概念，最熟悉就是JavaScript
```python
def counter():
    c = [0]
    def inc():
        c[0] += 1
        return c[0]
    return inc
foo = counter()
print(foo(), foo())
c = 100
print(foo())

```
> 上面代码有几个问题：
* 第4行会报错吗？为什么
* 第8行打印什么结果
* 第10行打印什么结果

> 代码分析
* 第7行会执行counter函数并返回inc对应的函数对象，注意这个函数对象并不释放，因为有foo记着
* 第4行会报错吗？为什么
    * 不会报错，c已经在counter函数中定义过了。而且inc中的使用方式是为c的元素修改值，而不是重新定义c变量
* 第8行打印什么结果
    * 打印 1 2
* 第10行打印什么结果
    * 打印3
    * 第九行的c和counter中的c不一样，而inc引用的是自由变量正式counter中的变量。
* 这是python2中实现闭包的方式，python3还可以使用nonlocal关键字
```python
#这段代码会报错吗？使用global能解决吗？

def counter():
    count = 0
    def inc():
        count += 1
        return count
    return inc   #返回inc对应的函数对象
foo = counter()
print(foo(), foo())
```
```python
#上面的一定错
def counter():
    global count
    count = 0
    def inc():
        global count
        count += 1
        return count
    return inc
foo = counter()
print(foo(), foo())
#这里使用global解决，这是全局变量的实现，而不是闭包
#如果要对这个普通变量使用闭包，python3中可以使用nonlocal关键字

#######
def counter():
    #global count   将这句注释了的话会出错的额，因为inc里面将count申明成了global，结果在执行count+=1时，却发现没有global的全局变量count，所以出错。如果这句添上，就在counter函数里面申明了count为全局变量，虽然counter外面没有，但是接下来的count=0，将count赋值为了0，所以还是对的
    count = 0
    def inc():
        global count
        count += 1
        return count
    return inc
foo = counter()
print(foo(), foo())


#####
count = 100
def counter():
    count = 0
    def inc():
        global count
        count += 1
        return count
    return inc

m = counter()
m()
m()
print(m())  #返回多少？

#######
count = 100
def counter():
    global count
    count = 0  #这句不要和在这里，最后的返回结果是多少？
    def inc():
        global count
        count += 1   #这里用到了闭包了么？因为都申明成了global，所以不存在闭包的
        return count
    return inc

m = counter()
m()
m()
print(m())


#######
count = 100
def counter():
    x = 123
    count = 0
    def inc():
        nonlocal count
        count += 1
        print(x)  #这里也使用了闭包哦，为什么这里的x不用申明为nonlocal也可以呢？因为这个里面的函数并未对他进行操作改变值啊，看上面的一个赋值引发的血案。。，这里打印的是counter函数下的x=123
        #如果将print(x)注释掉，则counter下的x由于没有人记住他了，所以随着counter的结束，它也会消亡的
        return count
    return inc

m = counter()
m()
m()
print(m())
```

### nonlocal 语句
* nonlocal： 将变量标记为不在本地作用域定义，而是在上级的某一级局部作用域中定义，但不能是全局作用域中定义。
```python
def counter():
    count = 0
    def inc():
        nonlocal count   #声明变量count不是本地变量
        count += 1
        return count
    return inc
foo = counter()
print(foo(), foo())
```
> count是外层函数的局部变量，被内部函数引用
内部函数使用nonlocal关键字声明count变量在上级作用域而非本地作用域中定义。
代码中内层函数引用外部局部作用域中的自由变量，形成闭包。

```python
a = 50
def counter():
    nonlocal a
    a += 1
    print(a)
    count = 0
    def inc():
        nonlocal count   
        count += 1
        return count
    return inc
foo = counter()
foo()
foo()
#错误的，nonlocal声明变量a不在当前作用域，但是往外就是全局作用域了，所以错误
```







### 默认值的作用域

```python
def foo(xyz=1):
    print(xyz)

foo()
foo()
print(xyz)
```

```python
def foo(xyz=[]):  #这里是引用类型，相当于是地址哦
    xyz.append(1)
    print(xyz)

foo()    #由于没有传参，所以用的是默认值，而默认值是一个引用类型，所以下次进来时，默认值还是一个引用类型，如果每次都要对引用你类型里面操作，则会被记住
foo()
print(xyz)  #NameERror，当前作用域没有xyz变量
```
> 为什么第二次调用foo函数打印的是[1,1]?
* 因为函数也是对象，每个函数定义被执行后， 就生成了一个函数对象和函数名这个标识符关联
* python把函数的默认值放在了函数对象的属性中，这个属性就伴随着这个函数对象的整个生命周期
* 查看foo.__defaults__属性，它是个元组

```python
#这样呢
def bar(x=[]):
    x.append(1)
    print(x)

lst = []
bar(lst)
bar(lst)
bar(lst)
bar(lst)


###
#这样呢？
def bar():
    x = []
    x.append(1)
    print(x)

lst = []
bar()
bar()
bar()
bar()
```



```python
##
# 1 
def foo(x=1, y=2):
    x = 3
    y = 4
    print(x, y)

print(foo.__defaults__)
foo()
print(foo.__defaults__)

# (1, 2)
# 3 4
# (1, 2)

# 2 
def foo(x=1, y=2, *, n='abc', t=[1, 2]): #keyworld-only参数
    x = 3
    y = 4
    t.append(300)
    print(x, y)

print(foo.__defaults__, foo.__kwdefaults__)
foo()
print(foo.__defaults__, foo.__kwdefaults__)

# (1, 2) {'n': 'abc', 't': [1, 2]}
# 3 4
# (1, 2) {'n': 'abc', 't': [1, 2, 300]}  #一样会

####
# 3
def foo(x=1, y=2, *, n='abc', t=[1, 2]):
    x = 3
    y = 4
    t[:].append(300)
    print(x, y, t)

print(foo.__defaults__, foo.__kwdefaults__)
foo()
print(foo.__defaults__, foo.__kwdefaults__)

# (1, 2) {'n': 'abc', 't': [1, 2]}
# 3 4 [1, 2]
# (1, 2) {'n': 'abc', 't': [1, 2]}

#####
# 4
def foo(x=1, y=2, *, n='abc', t=[1, 2]):
    x = 3
    y = 4
    t[:] = t  #
    t.append(300)  #
    print(x, y, t)

print(foo.__defaults__, foo.__kwdefaults__)
foo()
print(foo.__defaults__, foo.__kwdefaults__)

# (1, 2) {'n': 'abc', 't': [1, 2]}
# 3 4 [1, 2, 300]
# (1, 2) {'n': 'abc', 't': [1, 2, 300]}

### 5
def foo(x=1, y=2, *, n='abc', t=[1, 2]):
    x = 3
    y = 4
    t = t[:]  #前面那个t还是上面那个t么？切片是怎么搞的，这里可以新生成了一个t哦，所以打印的是[1,2,300],但是缺省的那个t还是原来那个哦
    t.append(300)
    print(x, y, t)

print(foo.__defaults__, foo.__kwdefaults__)
foo()
print(foo.__defaults__, foo.__kwdefaults__)

# (1, 2) {'n': 'abc', 't': [1, 2]}
# 3 4 [1, 2, 300]
# (1, 2) {'n': 'abc', 't': [1, 2]}

```
```python
###
def x(a=[]):
    a += [5]  #这里相当于a.extend([5])，就地修改，defaults改了
print(x.__defaults__)
x()
x()
print(x.__defaults__)

# ([],)
# ([5, 5],)

######
def x(a=[]):
    a = a + [5]  #返回新的列表，a已经不是原来的a了 a = __defaults__ + [5] 这样理解，defalults没有改变过
print(x.__defaults__)
x()
x()
print(x.__defaults__)

# ([],)
# ([],)

##############
a = 'a'
b = 'b'
c = a + b   
print(id(a), id(b), id(c))
c += 'd'  #这里注意，c是不可变的，这里不存在在原来的c增加一个'd'。但是有可能打印出来的id(c)地址是一样的，因为内存地址复用
print(c, id(c))

#1976091475728 1976091474048 1976092504224
#abd 1976092504224
###########
# 
```





### 变量名解析原则LEGB ***
* Local,本地作用域、 局部作用域的local命名空间。函数调用时创建， 调用结束消亡
* Enclosing， python2.2时引入了嵌套函数， 实现了闭包， 这个就是嵌套函数的外部函数的命名空间
* Global，全局作用域，即一个模块的命名空间。模块被import时创建，解释器退出时消亡
* Build-in,内置模块的命名空间，生命周期从python解释器启动时创建到解释器退出时消亡。例如：print(open),print 和open都是内置的变量
所以一个名词的查找顺序就是LEGB


