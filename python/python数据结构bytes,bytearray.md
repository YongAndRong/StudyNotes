## bytes、bytearray
* Python3 引入两个新类型  
* bytes
    不可变字节序列
* bytearray
    字节数组
    可变的

    * 字符串与bytes
        * 字符串是字符组成的有序序列，字符可以使用编码来理解  
        * bytes是字节组成的有序的不可变序列  
        * bytearray是字节组成的有序的可变序列  
    * 编码与解码  
        * 字符串按照不同的字符集编码encode返回字节序列bytes  
            encode(encoding='utf-8',errors='strict')  ---- > bytes  
            字符串用encode()方法只能转为bytes，不能转为bytearray，需要特殊构造   

        * 字节序列按照不同的字符集解码decode返回字符串  
            bytes.decode(encoding='utf-8',errors='strict') ----> str  
            bytearray.decode(encoding='utf-8',errors='strict') ----> str
### bytes定义
    定义
    * bytes()   空bytes
    * bytes(int) 指定字节的bytes，被0填充
    * bytes(iterable_of_ints) --->bytes [0,255]的int组成的可迭代对象
    * bytes(string,encoding[,errors]) ----> bytes 等价于string.encode()  
    * bytes(bytes_or_buffer)  ----> immutable of bytes_or_buffer从一个字节序列或者buffer复制出一个新的不可变的bytes对象  
    * 使用b前缀定义  
        * 指允许基于ASCII使用字符形式b'abc9'  
        * 使用16进制表示b'\x41\x61'  

```python
In [1]: b1 = bytes()  #不可变,那这里这个就永远是空bytes了

In [2]: b1
Out[2]: b''

In [3]: b2 = b''   #定义了一个空bytes

In [4]: b2
Out[4]: b''

In [5]: bytes('XYZ',encoding='utf8')
Out[5]: b'XYZ'

In [318]: bytes('abc','utf8')                                                                                         
Out[318]: b'abc'

In [7]: 'AWK'.encode()
Out[7]: b'AWK'

In [8]: bytes(13)  #bytes(n)  1个int ，指的是bytes的长度，使用‘\x00’填充，这个是ASCii码的零(内存中全零表示)，不是字符串的0(对应的是\x30)，这个要注意区分
Out[8]: b'\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00'  #没啥用

In [9]: bytes([61,62])  #61,62是十进制的
Out[9]: b'=>'

In [10]: bytes([0X61,0X62])  #使用十六进制
Out[10]: b'ab'

In [11]: bytes([97,98])  #里面是可迭代的int对象，单独的一个int就是48行的结果。
Out[11]: b'ab'           #int可以是二进制，八进制，十六进制,十进制等都算

In [15]: b2 = bytes([97,98])

In [16]: b3 = bytes(b2)   #这种情况b2,b3不是同一个对象，但是python3已经优化了

In [17]: b3
Out[17]: b'ab'   #b2、b3不是同一个对象，但是python对某些常量进行了优化，bytes和str一样属于字面常量，所以这里看到的id是一样的。但是对于可变类型没有做优化，对可变类型这样做，就不是这样的了
In [18]: id(b2),id(b3)
Out[18]: (2049251603600, 2049251603600)
#但是我们在用的时候不要这样用，因为61行的b3生成了一个全新的bytes，把b2重新包了一次，所以b2、b3不是同一个对象。

In [19]: b3 = b2 #只有这样才认为是一样的，这样我们可以用，增加引用计数吧

```

### bytes操作
    * 和str类型类似，都是不可变类型，所以方法很多都一样。只不过bytes的方法，输入是bytes，输出是bytes
        * b'abcdef'.replace(b.'f',b'k')  #并非就地修改，注意参数是bytes，返回的也是bytes
        * b'abc'.find(b'b')
    * 类方法 bytes.fromhex( string )   #(类方法，就是类才可以用的方法) ----> bytes
        * string必须是2个字符的16进制的形式，'6162 6a 6b',空格将被忽略
            bytes.fromhex('6162 09 6a 6b00')

    * hex() 
        * 返回16进制表示的字符串
        'abc'.encode().hex()

    * 索引
        b'abcdef'[2]  返回该 字节 对应的数，int类型

```python
In [33]: b'abcd'.replace(b'b',b'aaaa')
Out[33]: b'aaaaacd'     #生成了一个新的bytes

In [34]: b'abcd'.find(b'b')
Out[34]: 1    #look

In [36]: bytes.fromhex('616263')
Out[36]: b'abc'

In [37]: bytes.fromhex('61 62 63')  #可以空格，方便我们自己看
Out[37]: b'abc'

In [38]: b8 = bytes.fromhex('61 62 63')

In [40]: b8.hex()     #b8必须是bytes类型
Out[40]: '616263'  #返回到十六进制  和上面那个是反的 #hex(10) ---- > str

#一般转换为十六进制是为了网络传输

In [43]: '啊'[0]
Out[43]: '啊'

In [44]: b'abc'[2]   #bytes 的索引是字节为单位的，而字符串索引是一个字符的
Out[44]: 99          #看，返回的是十进制的

In [30]: ' '.join(map(str,b'abcde'))         #这么操作合适不?                                                                      
Out[30]: '97 98 99 100 101'

In [31]: ' '.join(map(str,b'abcde')).split()       #这么操作合适不?   感觉多此一举啊                                                                 
Out[31]: ['97', '98', '99', '100', '101']

In [260]: b'*'.join([b'a',b'cd',b'hello'])      #注意分隔符也是bytes类型                                                                      
Out[260]: b'a*cd*hello'


In [80]: list(b'abcdef')    #得到一个十进制整数类型的列表                                                                                            
Out[80]: [97, 98, 99, 100, 101, 102]





```


###bytearray定义
    * 定义
    * bytearray() 空bytearray
    * bytearray(int) 指定字节的bytearray，被0填充
    * bytearray(iterable_of_ints)  ----> bytearray[0,255]的int组成的可迭代对象
    * bytearray(string[,errors]) ----> bytearray近似string.encode()，不过返回可变对象
    * bytearray(bytes_or_buffer) 从一个字节序列或者buffer复制一个新的可变的bytearray对象

    * 注意，b前缀定义的类型是bytes类型

```python
In [39]: b8                                                                                                           
Out[39]: b'abc'

In [40]: b9 = bytearray(b8)                                                                                            

In [41]: b9                                                                                                           
Out[41]: bytearray(b'abc')

In [50]: b9.extend([100])

In [51]: b9
Out[51]: bytearray(b'abcd')

In [52]: b9.extend(range(101,105))

In [53]: b9
Out[53]: bytearray(b'abcdefgh')

In [54]: b9.append(b'i')   #error，这里必须写int类型，且范围在0-255的
---------------------------------- -----------------------------------------
TypeError

In [55]: b9.append(105)

In [56]: b9
Out[56]: bytearray(b'abcdefghi')

In [57]: b9.append(0x41)  #这是一个字节一个字节的添的，由于没有单个字节的东西，所以使用整型

In [58]: b9
Out[58]: bytearray(b'abcdefghiA')

In [59]: b9.pop()
Out[59]: 65      #弹出的还是整型

In [60]: b9.remove(b'a')  #这里还是得写int
---------------------------------------------------------------------------
TypeError

In [61]: b9.remove(97)   #这个还是别用了

In [62]: b9
Out[62]: bytearray(b'bcdefghi')

```

###bytearray 操作
    * 和bytes类型的方法相同
    bytearray(b'abcdef').replace(b'f',b'k')
    bytearray(b'abc').find(b'b')

    * 类方法bytearray.fromhex(string)
    string必须是2个字符的16进制的形式，'6162 6a 6b',空格将被忽略
    bytearray.fromhex('6162 09 6a 6b00')

    * hex()
    返回16进制表示的字符串
    bytearray('abc'.encode()).hex()

    In [42]: bytearray('abc'.encode()).hex()                                                                              
    Out[42]: '616263'

    * 索引
    bytearray(b'abcdef')[2] 返回该字节对应的数，int类型

    * append(int) 尾部追加一个元素
    * insert(index,int) 在指定索引位置插入元素
    * extend(iterable_of_ints) 将一个可迭代的整数集合追加到当前bytearray
    * pop(index=-1) 从指定索引上移除元素，默认从尾部移除
    * remove(velue) 找到第一个value移除，找不到抛ValueError异常  #value 必须是整型，移除后要挪动啊啊，慎用
    * 注意： 上述方法若需要使用int类型，值在[0,255]

    * clear() 清空bytearray
    * reverse()翻转bytearray，就地修改
```python
b = bytearray()
b.append(97)
b.append(99)
b.insert(1,98)

```

### 字节序 
    * 大端模式，big-endian;  小端模式,little-endian  
    * intel x86 CPU 使用小端模式
    * 网络传输更多使用大端模式  
    * windows、linux使用小端模式  
    * max os使用大端模式
    * java虚拟机是大端模式

    低位放在低地址 就是小端模式
    低位放在高地址 就是大端模式

### int和bytes

* int.from_bytes(bytes,byteorder)      #int类的方法   bytearray也可以这样转换的  
    将一个字节数组表示成整数  
```python
In [65]: i = int.from_bytes(b'abcd','big')                                                                                
Out[65]: 1633837924 

In [66]: hex(1633837924)                                                                                              
Out[66]: '0x61626364'
```

* int.to_bytes(length,byteorder)  
    byteorder字节序  
    将一个整数表达成一个指定长度的字节数组  


```python
In [70]: i                                                                                                            
Out[70]: 1633837924

In [71]: i.to_bytes(4,'big')                                                                                          
Out[71]: b'abcd'

In [72]: i.to_bytes(4,'little')   #字节序要对哦                                                                                     
Out[72]: b'dcba'
```
> 分割线--------------------------------------------------------------------------

## 切片 
* 线性结构
    * 特点：
    * 可迭代 for ... in
    * len()可以获取长度
    * 通过下标访问
    * 可以切片
* 学过的线性结构
    * 列表、元组、字符串、bytes、bytearray

* 切片
    * 通过索引区间访问线性结构的一段数据
    * sequence[start:stop] 表示返回  [start,stop)  区间的子序列
    * 支持负索引
    * start为0，可以省略
    * stop为末尾，可以省略
    * 超过上界(右边界)，就取到末尾；
    * 超过下界(左边界)，取到开头
    * start一定要在stop的左边 (和方向有关)

    * [:] 表示从头到尾，全部元素被取出，等效于copy()方法,浅拷贝过程

```python
#example
In [20]: 'abcdef'[:]  #类似copy
Out[20]: 'abcdef'

In [17]: 'abcdef'[1:1]  #空
Out[17]: ''

In [18]: 'abcdef'[1:2]
Out[18]: 'b'

In [21]: 'abcdef'[-1:3] #方向，start在stop右边了，所以切不出来
Out[21]: ''

In [22]: b'abcdef'[-1:3]  #切片出来的不改变类型的，bytes切出来的还是bytes
Out[22]: b''                #列表切还是列表，不会改变原有类型

In [76]: list('abcdef')[-1:3]                                                                                         
Out[76]: []

In [23]: 'abcdef'[-1:-3]   #方向反了，切不出来
Out[23]: ''

In [24]: 'abcdef'[-1:-3:-1]   #反过来了
Out[24]: 'fe'

In [25]: 'abcdef'[-3:-1]
Out[25]: 'de'

In [26]: 'abcdef'[-3:]   #前包后不包
Out[26]: 'def'

In [28]: b'abcdef'[1:3:2]  #间隔取
Out[28]: b'b'

In [29]: b'abcdef'[1:-1:2]  #记住左包右不包，这样取不包含-1的
Out[29]: b'bd'

In [30]: b'abcdef'[1::2]
Out[30]: b'bdf'

In [31]: b'abcdef'[::2]  #从头开始间隔2
Out[31]: b'ace'

In [32]: b'abcdef'[::-2]  #从尾部开始间隔2个   倒序哦  
Out[32]: b'fdb' 

In [81]: "hello world"[::-1]     #倒着打                                                                                      
Out[81]: 'dlrow olleh'
```


* 切片赋值  
    * 切片操作写在等号左边
    * 被插入值可迭代对象写在等号右边


```python
In [33]: a = list(range(10))

In [34]: a[1:2] = 10   #右边必须是可迭代对象
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-34-b60b39001c44> in <module>
----> 1 a[1:2] = 10

TypeError: can only assign an iterable

In [35]: a[1:2] = {10,11}

In [36]: a
Out[36]: [0, 10, 11, 2, 3, 4, 5, 6, 7, 8, 9]

In [37]: a[1:-1] = ()  #清空

In [38]: b = list()

In [39]: b[:] = a  #这里有两个动作

In [40]: c = a

In [41]: id(a),id(b),id(c)
Out[41]: (2319253188808, 2319248870792, 2319253188808)

In [48]: l1 = list(b'abcdef')
Out[48]: [97, 98, 99, 100, 101, 102]
In [49]: l1[1:2] = (10,)  #将那个位置的元素替换成后面的可迭代对象，就地修改  #这个操作少做，因为这里不光删了，还挪动了

In [50]: l1
Out[50]: [97, 10, 99, 100, 101, 102]

In [51]: l1[1:4] = ()  #相当于remove

In [52]: l1
Out[52]: [97, 101, 102]

In [53]: l1[:] = range(10)  #清空原来的，重新将0-9装进列表去

In [54]: l1
Out[54]: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

l2 = [1,2,3,4]



In [56]: l1[:] = l2  #相当于copy，但是注意，对l1有清空操作，如果l1原来是空的，没什么大的问题，就相当于copy

In [60]: l3 = l2[:]  #这个才是copy  不改变类型  理解成先切片，然后赋给l3

In [57]: l1
Out[57]: [1, 2, 3, 4]

In [58]: l2
Out[58]: [1, 2, 3, 4]

In [59]: id(l1),id(l2)
Out[59]: (2319253180232, 2319252289352)

In [62]: id(l3)
Out[62]: 2319254220040
####
In [65]: l8 = list(range(10))
In [63]: l9 = (1,2,3,4)
In [68]: l8[:] = l9 #切片不改变类型
In [69]: l9
Out[69]: (1, 2, 3, 4)
In [70]: l8
Out[70]: [1, 2, 3, 4]


#切片不改变类型,但是复制会的
In [69]: l9
Out[69]: (1, 2, 3, 4)

In [70]: l8
Out[70]: [1, 2, 3, 4]

In [71]: l8 = l9[:]

In [72]: l8  #l8也成元组了
Out[72]: (1, 2, 3, 4)

In [73]: l9
Out[73]: (1, 2, 3, 4)


```
