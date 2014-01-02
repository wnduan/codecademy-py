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
### 3.1 List Slicing Syntax
### 3.2
### 3.3
### 3.4
### 3.5
