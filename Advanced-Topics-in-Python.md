Advanced Topics in Python
===
## 1. Iteration Notions / 关于遍历
我们已经学习了如何遍历 **表 (list)** 中的元素，现在我们将学习以下三个点内容：
- 遍历更复杂的数据结构中的元素（如：dictionary）
- 动态的修改表(list)，通过（list comprehensions）
- 切分表(list)，通过表划分（slicing）

### 1.1 Iterators for Dictionarys / 遍历 Dictionary 中元素
先从*遍历 dictionary* 中的元素讲起，回想一下 dictionary 其实就是 *key（键）* 和 *value（值）* 的集合。Python的 `items()` 函数可以遍历 dictionary 中的各个元素，并且返回其 key/value 对。用法就是 `dictionary.tiems()` 。注意：*这个函数遍历dictionary时并不按照特定的顺序。*


**练习**

可以尝试运行下面的例子：

```python
my_dict = {
         "Name": "Stefan",
         "Age": 28,
         "Height": 175,
         "Weight": 62
}

print my_dict.items()
```


### 1.2 keys( ) and values( ) / 键和值
从上面的操作可以看出 `items()` 函数返回一个 *tuple* 的序列(array)，其中每个 tuple 包含了 dictionary 中的一个 key/value 对。同理：

- `keys()`函数，返回一个包含了dictionary中键key的序列(array)，  
- `values()`函数，返回一个由dictionary中值value组成的序列(array)，  

同样，上述两个函数也不能以指定的顺序返回 dictionary 中的 key 或 value

- 可以暂且将 **tuple** 理解为一个 *不可改变的表* *immutable list* 。（当然这只是过于简化的比较）tuple 由一对圆括号 `()` 包围，可以包含任意数据类型。
 
**练习** 

可以将前面例子中的 `print` 语句改为 `print my_dict.keys()` 和 `print my_dict.values()` 从而分别输出 dictionary 中的 键(keys) 和 值(values)。


### 1.3 The 'in' Operator / 'in' 操作符
为了逐项遍历 lists, tuples, dictionaries, strings 中的元素，Python 提供了一个特殊的关键字：`in` 。你可以非常直观的 (`in`tuitively) 使用 `in`,例如：

```python
for number in range(5):
    print number,
# => 0 1 2 3 4

d = { "name": "Eric", "age": 26 }
for key in d:
    print key, # note the comma!
# => age name

for letter in "Eric":
    print letter,  # note the comma!
# => "E" "r" "i" "c"
```

**练习** 

接前面的练习，使用 `in` 操作符，遍历 `my_dict` 中的各个元素并用 `print` 将其输出到屏幕。将 key 和 value 用一个空格分开（使用 `print key, value` 来进行输出，避免使用 `print key + " " + value` 这样的语句）。
注意，`print key, value` 语句中，逗号的使用，使得输出时在两个变量间插入了一个空格，并且使两个变量输出在同一行。
```python
for key in my_dict:  # my_dict was defined previously
    print key, value
```

## 2. List Comprehensions 
### 2.1 Building Lists / 创建列表
如果你想建立一个由 0~50 的数字组成的 列表(list)，可以很容易通过下列语句得到：
```python
my_list = range(51)
```
但如果我们要根据某些逻辑条件来创建一个列表(list)，例如建立一个由 0~50 的偶数组成的列表(list)那又该如何定义呢？

当然可以通过 `for` 语句和 `if` 语句的联合使用来实现上述目的。但是，Python提供了更为便捷的方式，那就是 **List Comprehension** 。 List comprehensions 是一个非常强大的定义列表的方式，通过我们已经学过的 `for`/`in` 以及 `if` 关键字来定义列表(list)。

**例子**

可以运行下面的语句看看是什么效果：
```python
evens_to_50 = [i for i in range(51) if i % 2 == 0]
print evens_to_50
```

### 2.2 List Comprehension Syntax / List Comprehension 语句
通过前面的例子，我们已经见识到了 list comprehension 的强大。那么这个语句具体如何使用呢。下面就详细的介绍一下。

首先，是一个简单的例子：
```python
new_list = [x for x in range(1,6)]
# 这个其实等价于 new_list = range(1,6)
# => [1, 2, 3, 4, 5]
```
上面的表达式定义了一个 1~5 的列表(list)。如果我们想把每个数都乘以2，也很容易，只要：
```python
doubles = [x*2 for x in range(1,6)]
# => [2, 4, 6, 8, 10]
```
更进一步，如果希望生成能被3整除的数的2倍：
```python
doubles_by_3 = [x*2 for x in range(1,6) if (x*2)%3 == 0]
# => [6]
```

**练习**

用 list comprehension 建立一个名为 `even_squares` 的列表变量。这个列表应该包括1~10的数中能被2整除的数的平方。（包括10）
```python
even_squares = [i**2 for i in range(1,11) if i%2 == 0]
print even_squares
```

### 2.3 Now You Try / 现在来做些练习
现在，尝试自己来使用list comprehension。

**练习**

创建一个名为 `cubes_by_four` 的列表。由1~10的数的立方中能被4整除的数组成。然后将他们显示出来。
```python
cubes_by_four = [x**3 for x in range(1,11) if (x**3)%4 == 0]
print cubes_by_four
```

## 3. List Slicing / 列表片段（划分）

### 3.1 List Slicing Syntax / 列表片段的基本语法
有时候，我们只需要列表(list)中的一部分元素。可能仅需要前一部分或后一部分或者需要间隔分布的元素，

这时候就需要列表片段的帮助，他可以使我们以一种更准确的方式获取列表中的元素。其语法形式如下：
```python
[start:end:stride]
```

其中 `start` 是片段开始的指数(index)（包括 start 本身，即片段中的元素大于等于 start，注意第一项的index是0），`end` 是片段结束的指数(index)（和 `range()` 一样，end 本身是不包括的，即片段中的元素小于 end）`stride` 定义了列表片段中项目间的间距（步长）。例如，stride 步长为 `2` 时，将在原列表中每隔一个选取一个元素形成列表片段。

**例子**

可以运行如下代码，看看代码片段的机制是如何工作的：
```python
l = [i ** 2 for i in range(1, 11)]
# Should be [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

print l[2:9:2]
```

### 3.2 Omitting Indices / 省略指数
如果用户没有指定列表片段中的三个指数(index)，Python会为其选择默认值。默认的起始 index 是列表中的第一个元素，即 `0` ；默认的结束 index 是列表中的最后一个元素， 即 `len(list) + 1` ；而默认的步长(stride)为 `1` 。例如：
```python
to_five = [1, 2, 3, 4, 5]
print to_five[3::]
# prints [4, 5] 
```

上面例子中，列表 `to_five` 在指数 `3` 处的元素是 `4`，由于后面两个指数都省略了，Python 认为你需要取到列表的最后一项，且计数每次增加1。

**练习**

学习了以上内容，现在练习使用代码片段输出 `my_list` 中从开始到结束间隔的元素，即输奇数（实际上是偶数index）。
```python
my_list = range(1, 11) # List of numbers 1 - 10

# Add your code below!
print my_list[::2]
```

### 3.3 Reversing a List / 倒序输出列表
步长 (stride) 为正值时，将按从左到右的顺序遍历列表；相反，一个负数的步长，将从右至左遍历列表。

**练习**

定义一个列表变量 `backwards` 并使其等于 `my_list` 的倒序。使用列表片段中负的步长来实现list元素的反向。在这个练习中不必指定第一个和第二个指数。
```python
my_list = range(1, 11)

# Add your code below!
backwards = my_list[::-1]
```

### 3.4 Stride Length / 步长
前面已经了解了，正的步长将从左至右遍历列表，负的步长从右至左遍历列表。更进一步，步长为1时，将以1为间隔遍历列表；步长为2时将以2为间隔遍历列表。这很简单了。

**练习**

一个简单的练习：定义一个列表变量 `backwards_by_tens` ，以 `10` 为步长遍历 `to_one_hundred` 并且将结果赋给 `backwards_by_tens`。用 `print` 将新的变量输出到屏幕。
```python
to_one_hundred = range(101)
# Add your code below!
backwards_by_tens = to_one_hundred[::10]
print backwards_by_tens
```

### 3.5 Practice Makes Perfect / 练习
以上就学习了列表片段的相关内容。下面来做一个练习：

**练习**

1. 定义一个列表 `to_21` ，包括1~21的数字（包括21）
2. 定义第二个列表 `odds` ，由 `to_21` 中的奇数组成。用 list slicing 而非 list comprehension 语句实现
3. 最后，定义第三个列表 `middle_third` ，由 `to_21` 的中间三分之一元素构成
```python
to_21 = range(1,22)
odds = to_21[::2]
middle_third = to_21[(len(to_21)/3):(len(to_21)*2/3)]
print to_21
print odds
print middle_third
```

## 4. Lambdas
### 4.1 Anonymous Functions / 匿名函数
Python 一个很强大的功能就是他允许采用 *函数化编程 (functional programming)* ，这就意味着可以把函数当作变量或值一样的传递。（这个可以类比MATLAB中的函数句柄的使用）。我们常常认为这本应该是理所当然的功能，但实际上，并非所有的语言都允许这样。

我们先看一个例子：
```python
my_list = range(16)
print filter(lambda x: x % 3 == 0 , my_list)
```

这里有两个新的内容：
- `filter()` 函数
- `lambda` 语句

我们先看下面这个，`lambda` 语句:
```python
lambda x: x % 3 == 0
```
就等等于下面的函数：
```python
def by_three(x):
    return x % 3 == 0
```

区别在于我们不需要给定函数名，他就可以完成其工作并返回值。这就是为什么说 **lambda** 定义的是一个 *匿名函数*

关于 `filter` 函数的，第一部分，当我们将 lambda 传递给 `filter()` 时，`filter` 用 lambda 返回的结果作为过滤的条件，来决定要过滤掉的内容；而第二部分 `my_list` 是一个将要被过滤的列表；

`filter` 最终将会输出判断为真值时对应的列表元素。

### 4.2 Lambdas Syntax / lambda 函数的语法
Lambda 函数按照下列规则定义：
```python
lambda variable: expression
```

当需要一个简单的函数临时完成某项工作时可以采用 lambda 函数。否则，你需要建立一个需要反复使用的函数，那么最好还是用 `def` 来定义一个有函数名的函数。

**练习**

使用 lambda 完成调用 `filter()` 函数，使得下面的 language list 中只输出 "Python"。
```python
languages = ["HTML", "JavaScript", "Python", "Ruby"]
print filter(lambda s: s == "Python", languages)
```

### 4.3 Try it / 练习
现在练习独自使用 `filter` 和 `lambda` ：

**练习**

1. 定义并创建一个列表，`squares` 包含了 1~10 的数的平方。提示：可以用 list comprehension
2. 用 `filter()` 和 `lambda` 表达式输出 `square` 中介于30到70的数
```python
squares = [x**2 for x in range(1,11)]
print filter(lambda n : n>30 and n<70, squares)
```

## 5. Review / 回顾
### 5.1 Iterating Over Dictionaries
首先来复习遍历 dictionary。

**练习**

调用合适的方法，输出 `movies` 中的所有项目
```python
movies = {
    "Monty Python and the Holy Grail": "Great",
    "Monty Python's Life of Brian": "Good",
    "Monty Python's Meaning of Life": "Okay"
}
print movies.items()
```

### 5.2 Comprehending Comprehensions
接着练习 list comprehension 的使用

**练习**

用 list comprehension 建立一个列表(list)，`threes_and_fives`，由1~15的数中能被3或5整除的数。
```python
threes_and_fives = [n for n in range(1,16) if (n%3 == 0 or n%5 ==0)]
```

### 5.3 List Slicing
接下来练习 list slicing

在 Python 中可以将字符串(string)看作一个字母(character)的列表(list)。（这样理解有点过于简化了，很明显一点不同字符串是不可变的immutable而列表是可变的mutable，更详细的参考注释）。这意味着，之前学习的 list slicing 操作可同样用于字符串！

> 注：要始终记住在Python中列表(list)是可变的(mutable/changeable)，但字符串(string)则不是。当你切分(slice)一个字符串时，将会获得一个新的字符串。原有的字符串并不发生改变。

**练习**

现在给出的 string 是混乱的。使用 list slicing 提取出信息并将其保存在 名为 `message` 的变量
```python
garbled = "!XeXgXaXsXsXeXmX XtXeXrXcXeXsX XeXhXtX XmXaX XI"
message = garbled[::-2]
```

### 5.4 Lambda Expressions
最后再来复习一下 `lambda` 表达式，直接进入一个练习

**练习**

现在给定了另一个（和之前有些不同）的混乱的字符串 `garbled`。定义一个 `message` 变量，用 `filter()` 和适合的 `lambda` 表达式过滤掉"X"，赋值给 `message`。最后将结果输出到屏幕。
```python
garbled = "IXXX aXXmX aXXXnXoXXXXXtXhXeXXXXrX sXXXXeXcXXXrXeXt mXXeXsXXXsXaXXXXXXgXeX!XX"
message = filter(lambda c: c!="X" , garbled)
```





