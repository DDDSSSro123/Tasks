

# Python的基础学习

## print函数

- Print()函数的使用
  - (1)print()函数输出的内容可以是数字
  - (2)print()函数输出的内容可以是字符串
  - (3)print()函数输出的内容可以是含有运算符的表达式
- print()函数可以将内容输出的目的地
  - (1)显示器
  - (2)文件
- print()函数的输出形式
  - (1)换行
  - (2)不换行

1. 将数据输出文件中：

   ```python
   fp=open('E:/text.txt','a+')#a+如果文件不存在就创建，存在就在文件内容的后面继续追加
   print('helloworld',file=fp)
   fp.close()
   ```

   ##### Attention！

   1. a+（读写的形式打开E盘文件text.txt。如果没有文件text.txt的话，就创建，有文件text.txt的话就在原有基础上进行追加，输入到text.txt文件。）
   2. fp为变量
   3. file不能丢，使用file=所设置的变量
   4. 所指定的盘符要存在

## 转义字符

转义字符概念：反斜杠+想要实现的转义功能首字母

- 转义字符出现的原因：当字符串中包含反斜杠、单引号和双引号等有特殊用途的字符时，必须使用反斜杠对这些字符进行转义(转换一个含义)
  - 反斜杠：\\\	（在输入的时候，输入4个'\\\\\\\',最后输出'\\\\'）							
  - 单引号：\\'
  - 双引号：\\"

- 特殊字符：
  - 换行：\n
  - 回车：\r
  - 水平制表符：\t
  - 退格：\b(退一个格)
    - \r的用法：把前面的字符吃掉（例print('hello\\rworld'),结果为world）即world将hello进行覆盖
    - \\b的用法：`print('hello\rworld')`结果为hellworld（退一个格，将o退没了）
    - \\'   \\'的用法:输入\\'   \\'结果为'   '
    - \t的用法:

```python
print('hello\tworld')
print('helloooo\tworld')
```

运行结果：

```python 
hello	world
helloooo	world
```

##### Attention！

\\t是占四个字符，它是从第一个字符开始计数，所以"hello\\tworld"空了三格，而"helloooo\\tworld"空了四格。

- 原字符，不希望字符串中的转义字符起作用，就使用原字符，就是在字符串之前加上r，或R

  例：

  - ```python
    print(r'hello\nworld')
    ```

  结果：

  - ```
    hello\nworld
    ```

  - 注意：最后一个字符不能是一个反斜杠。例：print(r'hello\nworld\\')就是错的，但print（r'hello\\nworld\\\\'）就是对的哦！

## 七十二变

- 1. 二进制与字符编码

​	8位比特=一个字节

```python
print(chr(0b100111001011000))
print(ord('乘'))
```

```python
乘
20056
```

2. Python中的标识符与保留字

-  保留字

  有些单词被赋予了特定的意义，这些单词在给任何对象起名字的时候都不能用。

  ```python
  import  keyword 
  print(keyword.kwlist) 
  ```

  结果：

  ```python
  ['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
  ```

  以上的单词都不能命名。

- 规则

  变量、函数、类、模块和其他对象的起的名字就叫标识符

  - 字母、数字、下划线
  - 不能以数字开头
  - 不能是保留字
  - 严格区分大小写

3. Python中的变量与数据类型

- 变量（变量是内存中一个带标签的盒子）有三部分组成
  - 标识：表示对象所存储的内存地址，使用内置函数id(obj)来获取
  - 类型：表示的是对象的数据类型，使用内置函数type(obj)来获取
  - 值：表示对象所存储的具体数据，使用print(obj)可以将值进行打印输出。
- 

4. Python中的注释



chap1.4

for循环语句格式：

for 变量 in 列表

range()函数返回在特定的区间的自然数序列

语句格式：range（起点，终点，步长);

起点：默认从0开始，range(5)等价于

range(0,5);

终点：到该点结束但不包括该点，类似i<5步长：默认为1，range(0,5)等价于

range(0,5,1)

sum为内置函数，可直接调用求和，且不用import调用模板



## 注意：

1. #为注释

















