## 计算机的组成  
###  1、计算机的五大部件  
    * 运算器，完成各种算数运算、逻辑运算、数据传输等数据加工处理
    * 控制器，控制程序的执行
    * 存储器，用于记忆程序和数据，例如内存
    * 输入设备，将数据或者程序输入到计算机中，如键盘、鼠标
    * 输出设备，将数据或程序的处理结果展示给用户，如显示器、打印机等

    * cpu由运算器和控制器组成，cpu当中还有寄存器和多级缓冲cache
cpu内部大概图
![github.com](https://github.com/YongAndRong/StudyNotes/blob/master/pics/CPUin.png)
> 注意：  
1、CPU只能和内存打交道，除此以外不与任何其他设备打交道。  
2、cpu中的寄存器和cpu是同频的。(频率即晶体震荡的频率)  
3、其中我们所熟知的L1、L2缓存是每个CPU核心独占的，而L3缓存则是所有核心共享的，缓存的速度依次降低，新版的CPU还会把北桥芯片集成在CPU中。 写程序如果能多注意缓存复用的情况，可以大大的提高所写程序的效率  

### 2、语言的分类  
* 编译语言，把源代码转换成目标机器的cpu指令
* 解释语言，解释后转换成字节码，运行在虚拟机上，解释器执行中间代码

### 3、高级语言的发展  
* 非结构化语言：编号或标签、GOTO，子程序可以有多个入口和出口，有分支、循环
* 结构化语言：任何基本结构只允许是唯一入口和唯一出口，有顺序、分支、循环，废弃GOTO
* 面向对象语言：更接近人类认知世界的方式，所有事物抽象成对象，对象间关系抽象成类和继承；封装、继承、多态；
* 函数式语言：古老的编程范式，应用在数学计算、并行处理的场景。函数是"一等公民"，高阶函数

### 4、什么是程序
    * 程序 = 算法 + 数据结构  
    * 数据时一切程序的核心
    * 数据结构是数据在计算机中的类型和组织方式
    * 算法是处理数据的方式，算法有优劣之分

## Python 概述
&ensp;&ensp;Python是Guido van Rossum在1989年圣诞节期间，为了打发无聊的圣诞节而编写的一个编程语言。
&ensp;python的优点：   

    * 为我们提供了非常完善的基础代码库，覆盖了网络、文件、GUI、数据库、文本等大量内容，被形象地称作“内置电池（batteries included）”。用Python开发，许多功能不必从零编写，直接使用现成的即可，除了内置的库外，Python还有大量的第三方库，供你直接使用。当然，如果你开发的代码通过很好的封装，也可以作为第三方库给别人使用。  
&ensp;python的缺点：  

    * 运行速度慢，和C程序相比非常慢，因为Python是解释型语言，你的代码在执行时会一行一行地翻译成CPU能理解的机器码，这个翻译过程非常耗时，所以很慢。而C程序是运行前直接编译成CPU能执行的机器码，所以非常快。  

    * 代码不能加密。如果要发布你的Python程序，实际上就是发布源代码，这一点跟C语言不同，C语言不用发布源代码，只需要把编译后的机器码（也就是你在Windows上常见的xxx.exe文件）发布出去。要从机器码反推出C代码是不可能的，所以，凡是编译型的语言，都没有这个问题，而解释型的语言，则必须把源码发布出去。
## python解释器  

官方CPython：C语言开发，最广泛的python解释器  
IPython：一个交互式、功能增强的CPyhton  
PyPY：Python语言写的python解释器，JIT技术，动态编译python代码。(JIT-->just in time，即动态调整)  
Jython：python的源代码编译成Java的字节码，跑在JVM上  
IronPython：与Jython类似，运行在.Net平台上的解释器，Python代码被编译成.Net的字节码。

## python的语言类型  
`Python是动态编译语言、强类型语言`  
静态编译语言  
&ensp;&ensp;&ensp;&ensp;1、 事先声明变量类型，类型不能在程序执行过程中改变  
&ensp;&ensp;&ensp;&ensp;2、编译时检查错误  
动态编译语言  
&ensp;&ensp;&ensp;&ensp;不用事先声明变量类型，随时可以赋值为其他类型  
&ensp;&ensp;&ensp;&ensp;编程时不知道变量是什么类型，很难推断(唯一的弊端)  
强类型语言  
&ensp;&ensp;&ensp;&ensp;不同类型之间操作，必须先强制类型转换为同一类型。如print('a' + 1)  --->会报错  
弱类型语言  
&ensp;&ensp;&ensp;&ensp;不同类型间可以操作，自动隐式转换，如：javascript中console.log(1+'a')  --->正确的  

## python版本区别  
&ensp;&ensp;&ensp;&ensp;Python是很多Linux系统默认安装的语言，以Centos为例由于其yum包管理工具使用的是Python开发，所以其内置了Python2.x版本，但是Python目前已经发展到了3.7版本了，并且Python官方对2.x的支持也快到期，所以建议学习ython的3.x版本。  
&ensp;&ensp;&ensp;&ensp;Python 3.x的在本质上和Python 2.x有很大的变化，2.x的程序是不能直接在3.x的版本上运行的，它们的主要区别有：  

* 语句函数化。例如print的打印，在3.x中是个函数，要打印的内容会被当作参数传递进入，而2.x中的含义是print语句打印元祖  
* 整除。在3.x中，/为自然除，//为整除。2.x中/和//都为整除。  
* input函数。3.x中把2.x中的raw_input舍去，功能合并到input函数中去。
* round函数。在3.x中的取整变为距离最近的偶数
* 字符串统一使用unicode。2.x中如果想要输入中文，还需要在文件头显示声明(_*_coding:utf-8 _*_)
* 异常的捕获、抛出的语法改变


## python的基础语法
* 注释-----#标注的文本  
* 数字  
    整数：  
    &ensp;&ensp;&ensp;&ensp;1、python3开始不区分long和int，long被重命名为int，所以只有int了  
    &ensp;&ensp;&ensp;&ensp;2、进制0xa、0o11、0b10  
    &ensp;&ensp;&ensp;&ensp;3、bool，只有2个值,True、False (注：bool类型是int类型的子类)   

    浮点数：  
    &ensp;&ensp;&ensp;&ensp;1、1.2、3.1415、-0.12、1.46e9等价于1.46*10^9  
    &ensp;&ensp;&ensp;&ensp;2、本质上使用了C语言的double类型  

    复数：  
    &ensp;&ensp;&ensp;&ensp;1+2j等等  

    字符串：  
    &ensp;&ensp;&ensp;&ensp;使用'、"单双引号引用的字符的序列    
    &ensp;&ensp;&ensp;&ensp;'''和"""单双三引号，可以跨行、可以在其中自由的使用单双引号  
    &ensp;&ensp;&ensp;&ensp;r前缀：在字符串前面加上r和R前缀，表示该字符串不做特殊的处理  
    &ensp;&ensp;&ensp;&ensp;f前缀：3.6版本开始，新增f前缀，格式化字符串  
    > 举例：  
    `a = '''`  #error,因为 ' 作为界定符，这样写python不知道哪里是边界，为了让a表示为一个单引号，这时我们可以将中间的单引号使用转义符进行转义，让其做回自己；也可以使用双引号" ' " 将单引号放中间，使用双引号作为界定符  
    " '''''''''''' "#双引号中存多少个单引号都是可以的，因为是将双引号做为了界定符。 

    转义序列：  
    &ensp;&ensp;&ensp;&ensp;1、\\  \t  \r  \n  \'  \"  
    &ensp;&ensp;&ensp;&ensp;2、前缀r，把里面的所有字符当普通字符对待   

    缩进：  
    &ensp;&ensp;&ensp;&ensp;未使用C等语言的花括号，而是采用缩进的方式表示层次关系  
    &ensp;&ensp;&ensp;&ensp;约定使用4个空格缩进  

    续行：  
    &ensp;&ensp;&ensp;&ensp;在行尾使用\  
    &ensp;&ensp;&ensp;&ensp;如果使用各种括号，认为括号内是一个整体，内部跨行不用\  

    > 说明：  
    1、\r在某些场景下是换行符；  
    2、续行符后面不能存有任何其他的字符，只能是回车；    
    3、\t&ensp;&ensp;[tab]字符有字符宽度的，不是每次有\t都会前进4个空格，因为如果光标所处的位置在这个字符宽度的第二个位置，那么\t只会前进2个空格，到下一个字符宽度处停止；  
    4、path = "c:\nt"  #这里的路径会将\n进行转义，而不是当作路径了，这时可以在字符串前加前缀r，path=r"c:\nt" 表示c盘下的名为nt的目录  

    标识符：  
    &ensp;&ensp;&ensp;&ensp;1、一个名字，用来指代一个值  
    &ensp;&ensp;&ensp;&ensp;2、只能是字母、数字和下划线  
    &ensp;&ensp;&ensp;&ensp;3、只能以字母或下划线开头  
    &ensp;&ensp;&ensp;&ensp;4、不能是python的关键字，如def、class就不能作为标识符  
    &ensp;&ensp;&ensp;&ensp;5、python是大小写敏感的  
    约定：  
    &ensp;&ensp;&ensp;&ensp;不允许使用中文  
    &ensp;&ensp;&ensp;&ensp;不要使用歧义单词，如class_  
    &ensp;&ensp;&ensp;&ensp;在python中不要随便使用下划线开头的标识符  

    > 注：  
    &ensp;&ensp;&ensp;&ensp;1、每个标识符被使用前都必须进行赋值  
    &ensp;&ensp;&ensp;&ensp;2、因为赋值即定义  (如果再次赋值的话，我们就认为重新赋值，重新定义了)  
    &ensp;&ensp;&ensp;&ensp;3、标识符跟一个值建立关联关系，以便以后使用该标识符时代表该值  

    常量：  
    &ensp;&ensp;&ensp;&ensp;一旦赋值就不能改变值的标识符  
    &ensp;&ensp;&ensp;&ensp;python中无法定义常量

    字面常量  
    &ensp;&ensp;&ensp;&ensp;一个单独的量，如12、'abc'等  

    变量  
    &ensp;&ensp;&ensp;&ensp;赋值后，可以改变值的标识符  
    > 注：  
    &ensp;&ensp;1、所谓的常量定义指a = 100，然后将a锁死，a的值不能再改变了，比如再进行a = 200时，这个赋值不会成功，而是报错  
    &ensp;&ensp;2、python没有常量定义，但是有常量的，比如100，'a' 等等，这叫字面常量  
    &ensp;&ensp;3、python中无常量，什么都可以改，只要你拿到一个标识符就可以改，但是后果自负哦。  
    &ensp;&ensp;4、x = 'abc' # 这叫变量定义，赋值即定义
## 运算符 Operator    

算数运算符  
&ensp;&ensp;&ensp;&ensp;+ - * / % **  
&ensp;&ensp;&ensp;&ensp;自然除/结果是浮点数，//是整除。注：2.x中/和//都是整除  

位运算符  
&ensp;&ensp;&ensp;&ensp;& | ~ ^ <<  >>    
&ensp;&ensp;&ensp;&ensp;常用方式：乘除2的倍数，32//8  相当于  32>>3  
&ensp;&ensp;&ensp;&ensp;12、0xc、0o14、0b1100  
> 注：  
&ensp;&ensp;&ensp;&ensp;//  是向下取整数(不是截取整数) 如：     
&ensp;&ensp;&ensp;&ensp;-5//2  ---  -3  
&ensp;&ensp;&ensp;&ensp;5//2   ---  2  
&ensp;&ensp;&ensp;&ensp;divmod(5,2) 得商和余数---(2,1)  
&ensp;&ensp;&ensp;&ensp;num & 1 == 1 ----判断num是否是奇数  
&ensp;&ensp;&ensp;&ensp;~  是按位取反  
&ensp;&ensp;&ensp;&ensp;^  异或--相同为0、不同为1  
&ensp;&ensp;&ensp;&ensp;同或  相同为1  
&ensp;&ensp;&ensp;&ensp;计算机中存放的都是补码  ，但是原码才是给人看的  

比较运算符  
&ensp;&ensp;&ensp;&ensp;==  !=  >  <  >=  <=   
&ensp;&ensp;&ensp;&ensp;返回一个bool值  
&ensp;&ensp;&ensp;&ensp;链式比较操作  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;4 > num > 2   但我们一般不这样操作，可以这样4 > num   and  num > 2  中间使用逻辑运算符  

逻辑运算符  
&ensp;&ensp;&ensp;&ensp;与或非 and or not
&ensp;&ensp;&ensp;&ensp;短路运算符  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;and如果第一个表达式为False,后面就没有必要计算了，这个逻辑表达式一定是False  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;or如果第一个表达式True，后面没有必要计算了，这个逻辑表达式一定是True  
> 注：  
&ensp;&ensp;&ensp;&ensp;1 == 1  -----True  
&ensp;&ensp;&ensp;&ensp;1 == '1'  -----False #这个是可以比较的，意思是1 等于 '1' 吗？ 不等于就是False了  
&ensp;&ensp;&ensp;&ensp;1 > '1' #这里程序会报错，因为类型不匹配，比较大小需要同类型比较，不然就没意义了。后期可以自己实现不同类型的比较，一般同类型比较安全些；  
* 短路思想很重要：把最常频繁计算的表达式，而且一旦计算出来就能决定整个表达式的值的，往前放，这样的话一旦计算出来，后面的表达式(包括函数等)就不用计算了，提前计算完了，可以大大的提高效率；比如：b>10 and fn(b)>3  #一旦前面短路了，后面的函数就没必要继续下去了  

赋值运算符  
&ensp;&ensp;&ensp;&ensp;a = min(3,5)  
&ensp;&ensp;&ensp;&ensp;+= -= *= /= %= 等  
&ensp;&ensp;&ensp;&ensp;x = y = z = 10 #不建议这样做  

成员运算符  
&ensp;&ensp;&ensp;&ensp;in、not in  

身份运算符  
&ensp;&ensp;&ensp;&ensp;is、is not  

> 注：   
1、 赋值一定先算右边  
2、 赋值即定义  ，再次赋值就是重新定义
3、 not b>10 -----> b<=10  



|运算符|描述|
|-----|----|
|-**-|-指数 (最高优先级)-|
|~ + -|	按位翻转, 一元加号和减号 (最后两个的方法名为 +@ 和 -@)
|* / % //|乘、除、取余、向下取整|
|+ -|	加法减法|
|>> <<|	右移，左移运算符
|&|	位 'AND'
|^ \||	位运算符|
|<= < > >=|	比较运算符
|<> == !=|	等于运算符
|= %= /= //= -= += *= **=|	赋值运算符
|is、is not|	身份运算符
|in、not in|	成员运算符
|not、and、or|	逻辑运算符
> 小结：  
1、算数运算符 > 位运算符 > 身份运算符 > 成员运算符 > 逻辑运算符  
2、记不住就用括号  
3、单目运算符 > 多目运算符  
4、长表达式，多用括号  

## 表达式 Expression  
&ensp;&ensp;由数字、符号、括号、变量等的组合  
&ensp;&ensp;&ensp;&ensp;算数表达式  
&ensp;&ensp;&ensp;&ensp;逻辑表达式  
&ensp;&ensp;&ensp;&ensp;赋值表达式  
> 注：python中，赋值即定义，如果一个变量已经定义，赋值相当于重新定义  

## 内存管理  
&ensp;&ensp;&ensp;&ensp;变量无须事先声明，也不需要指定类型，这是动态语言的特性  
&ensp;&ensp;&ensp;&ensp;python编程中一般无须关心变量的存亡，一般也不用关心内存的管理  
&ensp;&ensp;&ensp;&ensp;python使用引用计数记录所有对象的引用数  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;当对象引用数变为0，它就可以被垃圾回收GC  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;计数增加：  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;赋值给其他变量就增加引用计数，如x=3；y=x;z=[x,1]  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;实参传参，如foo(y)  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;计数减少  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;函数运行结束时，局部变量就会被自动销毁，对象引用计数减少  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;变量被赋值给其他对象。如x=3;y=x;x=4  
> 在有关性能的时候，就需要考虑变量的引用问题，但是该释放内存还是尽量不释放内存，看需求  

> 注：  
为什么使用引用计数机制：  
1、怕你不释放内存啊，它自己来释放，这样内存就有空间了，解决了内存空间问题  
2、解决内存碎片问题，内存是线性编址的，如果出现大量的零散的内存，不利于那种需要大量连续空间的数据结构使用；  
垃圾回收解决了什么问题？  
1、谁是垃圾  
2、怎么规整内存  
3、引用计数的互相引用问题，还能发现循环引用的问题，并能清理  

垃圾回收，在引用计数为0时，GC会在适当的时候，将引用计数为0的对象清除掉，规整好内存，给我们开辟出连续的内存空间，以防我们使用，但是在做垃圾清理时，这个规整的过程，应用程序是不能随便使用内存的，相当于应用程序不能动了，所以垃圾回收不能频繁的做。影响性能  
```python
import sys

x = []
print(sys.getrefcount(x))  #这里引用了2次，但是过了这一行代码，引用计数就减了1，因为退出了函数
print(sys.getrefcount([])) # 这里引用计数就又成1了
-----------------------------------------------------------------------
import sys

x = 1
print(sys.getrefcount(x))   #由于1是字面常量，所以没人知道被引用了多少次了
b = [x,1]
print(sys.getrefcount(x)) # 但是这里可以得出他增加了几次引用计数，2次

```
