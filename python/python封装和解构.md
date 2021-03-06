## 封装和解构

    * 封装(装箱)
        * 将多个值使用逗号分割,组合在一起
        * 本质上,返回一个元组,只是省掉了小括号

        t1 = (1,2)  #定义为元组
        t2 = 1,2    #将1和2封装成元组

        type(t1)  
        type(t2)  
    * 交换 (封装、解构)
        a = 4
        b = 5
        
        tmp = a
        a = b
        b = tmp
        等价于a,b = b,a   #等号右边使用了封装,而左边使用了解构
    * 解构(拆箱)
        * 把线性结构的元素解开,并顺序的赋给其他变量
        * 左边接纳的变量数要合右边解开的元素个数一致
```python
#example 1
lst = [3,5]
first,second = lst
print(first,second)
#example 2
a,b = 1,2
a,b = (1,2)
a,b = [1,2]
a,b = [10,20]
a,b = {1,2}
a,b = {'a':10,'b':20}  #非线性结构也可以解构
a,b = {1,2,3}
a,*b = {1,2,3}
[a,b] = (1,2)
[a,b] = 1,2
(a,b) = {3,4}


```
## python3 的解构
    * 使用 *变量名 接收,但不能单独使用
    * 被 *变量名 收集后组成一个列表

```python
#example 
lst = list(range(1,21,2))
head,*mid,tail = lst
*lst2 = lst
*body,tail = lst
head,*tail = lst
head,*m1,*m2,tail = lst
head,*mid,tail = "abcdefghijklmln"
type(mid)


```

## 丢弃变量
    * 这是一个惯例,是一个不成文的约定,不是标准
    * 如果不关心一个变量,就可以定义改变量的名字为_
    * _是一个合法的标识符,也可以作为一个有效的变量使用,但是定义成下划线就是希望不要被使用,除非你明确的知道这个数需要使用

```python
#example 1
lst = [9,8,7,20]
first,*second = lst
head,*_,tail = lst
print(head)
print(tail)
# _是合法的标识符,看到下划线就知道这个变量就是不想被使用
print(_)

#example 2
lst = [9,8,7,20]
first,*second = lst
_,*_,tail = lst
print(_)
print(tail)
print(_)

```

    * 总结
        * _这个变量本身无任何语义,没有任何可读性,所以不是用来给人使用的
        * python中很多库,都使用这个变量,使用十分广泛.请不要在不明确变量作用域的情况下,使用_导致和库中_冲突

