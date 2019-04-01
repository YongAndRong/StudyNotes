## python 语法  

### 程序控制  
* 顺序  
    * 按照事先顺序一条条执行
* 分支
    * 根据不同的情况判断，条件满足执行某条件下的语句
* 循环
    * 条件满足就反复执行，不满足就不执行或不再执行

`真值表`
|对象/常量|值|
|:-------|:--------|
|""|假|
|"string"|真|
|0|假|
|>=1|真|
|<=-1|真|
|()空元组|假|
|[]空列表|假|
|{}空字典|假|
|None|假|
> 注:0、False、''、""、[]、()、{}、set()、None对象 都是假

```python
if [0,None]:
    print('true')
else:
    print('false')
#out---->true
if [0]:
    print('true')
else:
    print('false')
#out---->true
#if后面有东西，即为非空，所以进入if语句里面，打印true
```
> 注意:  
```python
#1：
if condition:
    代码块
#condition必须是一个bool类型，这个地方有一个隐式转换bool(condition)
#2：
for element in iterable: 
    block
#当可迭代对象中有元素可以迭代，进入循环体，执行block
#意思从箱子拿，箱子有东西就可以进去拿，

*************小技巧*************************
In [1]: int(10.5)   #int() 取整                                                                                    
Out[1]: 10

In [10]: int ('123')    #这样是没问题的                                                                                
Out[10]: 123

In [3]: int('10.5')      #对字符串使用int()会报错                                                                                
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-3-6cc59efdcec3> in <module>
----> 1 int('10.5')

ValueError: invalid literal for int() with base 10: '10.5'

In [4]: float('10.5')        #float()可以对字符串进行处理，取得float                                                                            
Out[4]: 10.5

In [2]: int(float('10.5'))      #所以这样是可以的                                                                         
Out[2]: 10
```
### range()函数  
    range()函数生成一个序列
```python
for i in range(10):  #计数器 i= 从range内取一个元素赋值 (range就是一个容器)，感觉是一个隐式赋值
    print(i)         #从箱子里拿东西就是遍历，不会重复拿
    i += 10          #这个语句有点意思，因为在这里改变了i的值，但是打印出来的i却不受这个影响，不像c语言的，因为它是从容器里面拿数据，每循环一次拿一次，随便你在语句里面改的

out：0 1 2 3 4 5 6 7 8 9 
****************************************************
In [5]: range(1,11,2)    #可迭代对象，惰性的，这家伙很懒，你不去拿，他就不会出对象                                        
Out[5]: range(1, 11, 2)   #这个返回的叫range对象,这个range对象称为可迭代对象
#可迭代对象不遍历不出对象，遍历才出对象，所以这种叫惰性对象
In [7]: for i in range(9,-1,-1):   #打印10-1  倒序打印   注意range()里面的顺序
   ...:     print(i+1) 
```
### 循环else子句  
```python
while condition:
    block
else:
    block

for element in iterable:
    block
else:
    block
#如果循环正常的执行结束，就执行else子句，即使循环都没有进去
#如果使用break终止循环，则else子句不会执行
#example 1
for i in range(0):  #range容器里面没有，是空的，但是for循环是正常结束的，所以'else'还是正常打印了的
    print(i)
else:
    print('else')
#example 2
for i in []:     # 这个同上面一个道理
    print(i)
else:
    print('else')
#example 3
for i in range(5):  
    print(i)
    if i > 3:
        break
else:
    print('else')
#这个循环在i==4时，虽然也是打印了i的值，但是在打印完后就执行了if语句，结果造成了break，所以是非正常结束的，即便for循环遍历的最后一个数字是4，但是非正常退出，所以else子句未执行的。
#如果这个循环没有if语句，正常情况下，i从容器里面取出4后，并打印了，程序执行下次循环，i还想从容器里取数字，结果发现不能取了，所以就正常结束。然后才执行else子句
#注意非正常退出，即便你已经遍历完了，但是循环是非正常退出的话，那就不会执行else子句
```
