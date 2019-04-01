## 字符串

* 一个个字符组成的有序的序列，是字符的集合
* 使用单引号、双引号、三引号引住的字符序列

* 字符串是不可变对象
* python3起，字符串就是Unicode类型

### 字符串定义 初始化
```python
#example 
s1 = 'string'
s2 = "string2"
s3 = '''this's a "String" '''
s4 = 'hello \n magedu.com'
s5 = r"hello \n magedu.com"
s6 = 'c:\windows\nt'
s7 = R"c:\windows\nt"  #这里会转义哦 有问题的这样
s8 = 'c:\windows\\nt'  #这里需要转义
name = 'tom';age=20
s9 = f'{name},{age}' #3.6支持f前缀
sql = """ select * from user where name='tom'"""
```
> 可迭代未必可索引  
可索引说明是有序序列，按顺序排放的  
可迭代指可用for循环从里面拿出来  


```python   
In [125]: sql = "hello"  
  
In [126]: lst = list(sql)    #将sql里的字符搞成字符串存到列表中去

In [127]: lst    
Out[127]: ['h', 'e', 'l', 'l', 'o']    

In [128]: tuple(lst)    
Out[128]: ('h', 'e', 'l', 'l', 'o')   #临时创造了一个元组，原来的lst并未改变，只是改了个类型，生产环境中这样做要注意内存

In [129]: lst
Out[129]: ['h', 'e', 'l', 'l', 'o']


```
### 字符串元素访问-----下标
    * 字符串支持使用索引访问
    sql = " select * from user where name='tom'"
    sql[4] #字符串'c'
    sql[4] = 'o' #error  不可改变

    * 有序的字符集合，字符序列
    for c in sql:
        print(c)
        print(type(c))  #什么类型？  答案str
     #type('')  --- > str  即使没有字符，这种也是str类型   

    * 可迭代
        lst = list(sql)

```python
In [125]: sql = "hello"

In [126]: lst = list(sql)

In [127]: lst
Out[127]: ['h', 'e', 'l', 'l', 'o']
```

### 字符串join连接 *
    * "string".join(iterable) ---->str
        * 使用string作为分隔符，将可迭代对象连接起来。
        * 可迭代对象本身元素都是字符串
        * 返回一个新的字符串
```python
lst = ['1','2','3']
print("\"".join(lst)) #分隔符是双引号
print(" ".join(lst))
print("\n".join(lst))
lst = ['1',['a','b'],'3'] #这个大列表只有三个元素，所以只拼接三次
print(" ".join(lst))
```

### 字符串+连接
    * + -----> str
        * 将两个字符串连接在一起
        * 返回一个新的字符串

### 字符串分割
    * split系
        * 将字符串按照分隔符分割成若干字符串，并返回列表
    * partition系
        * 将字符串按照分隔符分割成2段，返回这2段和分隔符的元组


#### 字符串分割 * 
    * split(sep=None,maxsplit=-1)   -----> list of strings 字符串列表，分割完后，立即返回一个列表
        * 从左至右
        * sep 指定分割字符串，缺省的情况下空白字符串作为分隔符
        * maxsplit 指定分割的次数，-1表示遍历整个字符串

```python
s1 = "I'm \ta super student."
s1.split()
s1.split('s')
s1.split('super')
s1.split('super ')
s1.split(' ')
s1.split(' ',maxsplit=2)
s1.split('\t',maxsplit=2)
#example
In [157]: s5 = "I  \r\n \tam \tsuper \rman"
In [159]: s5
Out[159]: 'I  \r\n \tam \tsuper \rman'

In [160]: s5.split()  #默认使用空白字符分割，立即返回一个列表，缺省的情况下，空白字符是贪婪模式的。尽量长的将空白字符作为一个整体
Out[160]: ['I', 'am', 'super', 'man']  

In [162]: s5.split(' ') #知道空格作为分割符，其他的保留下来了
Out[162]: ['I', '', '\r\n', '\tam', '\tsuper', '\rman']

In [163]: s5.split('\t') #以\t为分隔符，s5中有两个\t，所以切两刀
Out[163]: ['I  \r\n ', 'am ', 'super \rman']

In [164]: s5.split(' \t\r\n') #注意这不是正则表达式，它是这样搞的：先找空格，空格后面是\t，再后面是\r，再后面是\n，结果这样的分割符没有，就没切
Out[164]: ['I  \r\n \tam \tsuper \rman']

In [165]: s5.split(' \r\n') #这样的分隔符有，就切了一刀，分隔符是作为一个整体来的
Out[165]: ['I ', ' \tam \tsuper \rman']

In [166]: s5.split('*') #没找打* 分隔符，就返回个单值的列表
Out[166]: ['I  \r\n \tam \tsuper \rman']

In [174]: s5.split(maxsplit=2) # 切2刀，两刀就是三段了。
Out[174]: ['I', 'am', 'super \rman']
```

    * rsplit(sep=None,maxsplit=-1) ----->list of strings
        * 从右向左
        * sep指定分割字符串，缺省的情况下空白字符串作为分隔符
        * maxsplit指定分割的次数，-1表示遍历整个字符串 #maxsplit 大于应该切的次数的话，就和-1一样了，不会报错的

```python
s1 = "I'm \ta super student."
s1.rsplit()
s1.rsplit('s')
s1.rsplit('super')
s1.rsplit('super ')
s1.rsplit(' ')
s1.rsplit(' ',maxsplit=2)
s1.rsplit('\t',maxsplit=2)
```


    * splitlines([keepends]) -----> list of strings
        * 按照行来切分字符串
        * keepends 指的是是否保留分隔符
        * 行分隔符包括\n、\r\n、\r等

```python
In [177]: s5 =  'I  \r\n \tam \t\n super \rman'

In [178]: s5.splitlines()   #按行切
Out[178]: ['I  ', ' \tam \t', ' super ', 'man']

In [179]: s5.splitlines(True)  #保留换行符，缺省情况下是False  #一般不保留
Out[179]: ['I  \r\n', ' \tam \t\n', ' super \r', 'man']
```

    * partition(sep) -----> (head,sep,tail)
        * 从左至右，遇到分隔符就把字符串分割成两部分，返回头、分隔符、尾三部分的三元组；如果没有找到分隔符，就返回头、2个空元素的三元组
        * sep分割字符串，必须指定
    * rpartition(sep) ---->(head,sep,tail)
        * 从右至左，遇到分隔符就把字符串分割成两部分，返回头、分隔符、尾三部分的三元组；如果没有找到分隔符，就返回2个空元素和尾的三元组
```python
#example partition --- 必须得有一个分隔符作为参数，必须指定分隔符
In [190]: s4
Out[190]: 'a,b,c,d,e,f'

In [193]: s4.partition('.')  #立即返回一个三元组，因为没有切到，所有后面连个是空的，分隔符没了
Out[193]: ('a,b,c,d,e,f', '', '')

In [192]: s4.partition(',')
Out[192]: ('a', ',', 'b,c,d,e,f') #切到了，只切了一刀   等价于split(maxsplit=1)
#但是split返回的是列表，列表中不带分隔符；partition把分割符给带上了，返回的是元组；简化版的split
In [194]: s4.rpartition('.') #从右边向左切，没切到，前面两个是空，分隔符没了
Out[194]: ('', '', 'a,b,c,d,e,f')

In [196]: s4.partition('d')  #只要是字符都可以作为分隔符
Out[196]: ('a,b,c,', 'd', ',e,f')

In [197]: s4.split('d')  #这个才真正的叫一刀两段，d没了
Out[197]: ['a,b,c,', ',e,f']

#一般切多次用split
#切一刀，一般用partition ，其实split都可以搞的
```

### 字符串大小写
    * upper()
        * 全大写
    * lower()
        * 全小写
    * 大小写，做判断的时候用
    * swapcase()
        * 交换大小写

### 字符串排版
    * title() ---->str
        * 标题的每个单词都大写
    * capitalize()  -----> str
        * 首个单词大写
    * center(width[,fillchar]) ----> str
        * width 打印宽度
        * fillchar 填充的字符
    * zfill(width) ----> str
        * width 打印宽度，居右，左边用0填充
    * ljust(width[,fillchar]) ----> str 左对齐
    * rjust(width[,fillchar]) ----> str 右对齐
```python
In [205]: 'a title of news'.capitalize()
Out[205]: 'A title of news'

In [206]: s10 = 'a title of news'
In [207]: s10.center(20)
Out[207]: '  a title of news   '

In [208]: s10.center(20,'*') #默认使用的空格填充，如果需要，只能一个字符
Out[208]: '**a title of news***'
In [213]: s10.center(30,'0') #记得是字符，整数0的话会报错的
Out[213]: '0000000a title of news00000000'

In [211]: s10.zfill(30) #用0填充，左对齐
Out[211]: '000000000000000a title of news'

In [214]: str(1).zfill(10)
Out[214]: '0000000001'  #一般补0，可以这样写

In [215]: '1'.ljust(10)
Out[215]: '1         '

In [216]: '1'.ljust(10,'0')
Out[216]: '1000000000'

In [217]: '1'.rjust(10,'0')
Out[217]: '0000000001'  #类似zfill。。。
```


### 字符串修改 *
    * replace(old, new[, count]) ----> str 
        * 字符串中找到匹配替换为新子串，返回新字符串
        * count表示替换几次，不指定就是全部替换，从左到右的替换
    #低级的替换，不能模糊的替换，使用正则表达式来搞


```python
'www.magedu.com'.replace('w','p')
'www.magedu.com'.replace('w','p',2)
'www.magedu.com'.replace('w','p',3)
'www.magedu.com'.replace('ww','p',2)
'www.magedu.com'.replace('www','python',2)


In [218]: s10
Out[218]: 'a title of news'

In [219]: s10.replace('a','the')  #将a替换为了the
Out[219]: 'the title of news'

In [220]: s10.replace(' ','\n')
Out[220]: 'a\ntitle\nof\nnews'

In [221]: s10.replace(' ','\n',1)  #替换1次
Out[221]: 'a\ntitle of news'

In [226]: s1 = 'a b'

In [227]: s1.replace(',',' ') #将逗号替换为空格，由于没有逗号，所以还是原样的返回一个新的字符串
Out[227]: 'a b'
#搞个好玩的，看下面的
In [228]: s1
Out[228]: 'a b'

In [229]: s1.replace(' ','    \t').split().append('c')  #这种叫链式编程，但是没有返回。因为最后append返回的是None

In [230]: s1
Out[230]: 'a b'

In [231]: s2 = s1.replace(' ','    \t').split().append('c')  #所以我做了这一步，但是s2还是没有东西，这是为什么呢？首先s1.replace(' ','    \t').split()，返回的是一个临时的列表，在临时列表后面再追加一个值，并返回了None，并将None赋值给了s2，所以s2啥都没有

In [232]: s2
###最后还是得像下面这样做，才能得到你想要的，这种做法没啥意思，因为append返回None，急死你
In [234]: tmp = s1.replace(' ','    \t').split()

In [235]: tmp.append('c')

In [236]: tmp
Out[236]: ['a', 'b', 'c']

```

    * strip([chars]) ----> str
        * 从字符串两端去除指定的字符集chars中的所有字符
        * 如果chars没有指定，去除两端的空白字符

    #chars --->意思可以写多个
```python
#example strip
s = "\r\n\thello python \n \t"
s.strip()
s = " I am very very very sorry "
s.strip('Iy')
s.strip('Iy ')
###*********
In [238]: s11
Out[238]: '   \t  I am very very very sorry  \r\n '

In [239]: s11.strip()  #默认去除字符串两端的空白字符(空白字符包括空格、换行符、tab、换页符)
Out[239]: 'I am very very very sorry'

In [245]: s11.strip(' ')  #两头的空格拿掉，遇到第一个非空格停止
Out[245]: '\t  I am very very very sorry  \r\n'

In [249]: s11.strip(' \t')  #在两端碰到第一个不在这里面的字符集就停止
Out[249]: 'I am very very very sorry  \r\n'

In [250]: s11.strip(' \t\nmaI')  #这里面是可以有多个的，chars嘛
Out[250]: 'very very very sorry  \r'

In [251]: s11.lstrip(' \t\nmaI')  #左边
Out[251]: 'very very very sorry  \r\n  '
```


    * lstrip([chars]) ----> str
        * 从左开始
    * rstrip([chars]) ----> str
        * 从右开始


### 字符串查找 * 
    * find(sub[,start[,end]]) ----> int
        * 在指定的区间[start,end),从左至右，查找子串sub。找到返回索引，没找到返回-1
    * rfind(sub[,start[,end]]) ----> int
        * 在指定的区间[start,end),从右至左，查找子串sub。找到返回索引，没找到返回-1
        #sub是作为一个整体的，找到了返回索引，没找到返回-1
        #时间复杂度O(n)

```python
s = "I am very very very sorry"
s.find('very')
s.find('very',5)
s.find('very',6,13)
s.find('very',10)
s.find('very',10,15)
s.find('very',-10,-1)
```

    * index(sub[, start[, end]]) ---->int
        * 在指定的区间[start, end),从左至右，查找子串sub，找到返回索引，没找到抛出异常ValueError
    * rindex(sub[, start[, end]]) ---->int
        * 在指定的区间[start, end),从右至左，查找子串sub，找到返回索引，没找到抛出异常ValueError
```python
s = "I am very very very sorry"
s.index('very')
s.index('very',5)
s.index('very',6,13)
s.rindex('very',10)
s.rindex('very',10,15)
s.rindex('very',-10,-1)
```

    * count(sub[, start[, end]]) ----> int
        * 在指定的区间[start,end),从左至右，统计子串sub出现的次数
```python
s = "I am very very very sorry"
s.count('very')
s.count('very',5)
s.count('very',10,14)
```
    * 时间复杂度
        * index和count方法都是O(n)
        * 随着数据规模的增大，而效率下降

    * len(string)
        * 返回字符串的长度，即字符的个数
        #时间复杂度O(1)


### 字符串判断 * 
    #前缀后缀
    * endswith(suffix[, start[, end]]) ---->bool
        * 在指定的区间[start, end),字符串是否是suffix结尾
    * startswith(prefix[, start[, end]]) ----> bool
        * 在指定的区间[start, end),字符串是否是prefix开头


```python
s = "I am very very very sorry"
s.statswith('very')
s.statswith('very',5)
s.statswith('very',5,9)
s.endswith('very',5,9)
s.endswith('very',5)
s.endswith('very',5,-1)
s.endswith('very',5,100)

#example 前缀后缀
In [254]: s12 = 'xy.tar.gz'

In [255]: s12.startswith('x')
Out[255]: True

In [256]: s12.endswith('.gz')
Out[256]: True

In [257]: s12.endswith('.tar',0,-2)
Out[257]: False

In [258]: s12.endswith('.tar',0,-3)   #前包后不包
Out[258]: True
```
### 字符串判断is系列
    * isalnum() ----> bool 是否是字母和数字组成
    * isalpha() 是否是字母
    * isdecimal() 是否只包含十进制数字
    * isdigit() 是否全部数字(0~9)
    * isidentifier() 是不是字母和下划线开头，其他都是字母、数字、下划线
    * islower() 是否全部小写
    * isupper() 是否全部大写
    * isspace() 是否只包含空白字符(空格\t\r\n\f,不特指空格)
```python

```


### 字符串格式化
    * 字符串的格式化时一种拼接字符串输出样式的手段，更灵活方便
        * join拼接只能使用分隔符，且要求被拼接的是可迭代对象且其元素使用字符串
        + 拼接字符串还算方便，但是非字符串需要先转换为字符串才能拼接

```python

```


#### format函数格式字符串语法 ------python鼓励使用
    * "{}{xxx}".format(*args, **kwargs) ----> str
    * args 是可变位置参数，是一个元组
    * kwargs 是可变关键字参数，是一个字典
    * 花括号表示占位符
    * {}表示按照顺序匹配位置参数，{n}表示取位置参数索引为n的值
    * {xxx}表示在关键字参数中搜索名称一致的
    * {{}}表示打印花括号

    * 位置参数
    * 关键字参数或命名参数
    * 访问元素
    * 对象属性访问
    * 对齐
    * 进制
    * 浮点数

```python
#example c风格
In [278]: "I am %s" % 20
Out[278]: 'I am 20'


In [281]: "I am %s" % list(range(5))
Out[281]: 'I am [0, 1, 2, 3, 4]'

In [282]: "I am %s" % list(range(5))
Out[282]: 'I am [0, 1, 2, 3, 4]'

In [283]: "I am %s" % 20
Out[283]: 'I am 20'

In [284]: "I am %4s" % 20
Out[284]: 'I am   20'

In [285]: "I am %-4s" % 20
Out[285]: 'I am 20  '

In [288]: 'My name is %s, I am %d' % ('wayne',30)
Out[288]: 'My name is wayne, I am 30'

In [289]: '%10.2f'% 32.2356
Out[289]: '     32.24'

In [290]: '%x' % 127  #hex(127)
Out[290]: '7f'

In [291]: '%#x' % 127
Out[291]: '0x7f'

In [292]: '0x%x' % 127  #自己加的
Out[292]: '0x7f'

#example  python鼓励使用的

In [293]: "{}".format(1)
Out[293]: '1'

In [294]: "{}".format('asb')
Out[294]: 'asb'

In [298]: "{}{}{}".format(1,2,3)
Out[298]: '123'





In [305]: import datetime

In [306]: d = datetime.datetime.now()

In [307]: d
Out[307]: datetime.datetime(2019, 3, 30, 20, 23, 48, 513956)

In [308]: "{}".format(d)
Out[308]: '2019-03-30 20:23:48.513956'

In [309]: "{:%Y-%m-%d %H:%M:%S}".format(d)
Out[309]: '2019-03-30 20:23:48'



```
