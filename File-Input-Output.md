File Input/Output / 关于类的更多内容
===
以上，我们已经学习了Python的符号语法还有一些实例，现在我们还要学习一下实际应用中一个重要的部分：将数据写入文件。

## 1. Introduction to File I/O  / 文件输入输出 (I/O)的介绍

### 1.1 See It to Believe It / 眼见为实

目前，我们写的Python代码都是从一个来源输入然后只输出到一个地方：所有代码都是从键盘输入，然后结果都是输出到屏幕的控制台。但是如果希望从文件读出输入信息，或者是将信息写入到另外的文件，该怎么办呢？

这个过程称为文件输入输出 **file I/O** ，Python提供了很多内建函数以处理这些工作。

浏览并学习下面的代码。

**指南**

运行下列代码，检查输出的文件。

```python
my_list = [i**2 for i in range(1,11)]
# Generates a list of squares of the numbers 1 - 10

f = open("output.txt", "w")

for item in my_list:
    f.write(str(item) + "\n")

f.close()
```


### 1.2 The open() Function / open() 函数

我们来一步步学习整个写入文件操作的过程。

在之前的代码中，运行的第一个新代码是：
```python
f = open("output.txt", "w")
```

这句代码告诉Python以 `"w"` 模式(w表示write)打开一个名为 `output.txt` 的文件。我们将这个操作的结果保存在一个文件对象 `f` 中。

执行以上的语句，将以写入模式打开一个文件，并且使Python准备好将文件写入该文件。

**指南**

创建一个变量，`my_file`，将其赋值为以 `output.txt` 调用 `open()` 函数。在这个例子中，将 `"r+"` 作为第二个输入声明，这将允许我们读取及写入文件。

```python
my_file = open("output.txt", "r+")
```

### 1.3 Writing / 写入

很好！现在我们来学习将一些数据写入我们的 `output.txt` 文件中。

我们在前面的例子前面加入了第一个例子中的 *列表表达式*。我们在这个练习中的目的是将列表中的每个元素写入我们的 `output.txt` 文件中，每个元素位于单独的一行。

我们可以这样写入Python文件：
```python
my_file.write("Data to be written")
```

其中，`write()` 函数接受一个字符串输入，所以我们需要在这做一些操作：

01. 遍历 `my_list` 以获取列表中每个元素的值
02. 使用 `write()` 函数将每个值写入 `output.txt`
03. 确保通过对数据使用 `str()` 函数将其转换为 `write()` 可接受的字符串输入
04. 确保在每个元素后增加一个换行 ("\n") 保证每个元素都在单独的一行  

最后，当完成写入操作后，**必须**关闭文件。这个工作只需要调用 `my_file.close()`。如果不关闭文件，Python将无法正确的写入。

**指南**

遍历 `my_list` ，将其中的每个元素写入到 `output.txt` 文件，每个元素一行。写入完后，关闭文件。

```python
my_list = [i**2 for i in range(1,11)]

my_file = open("output.txt", "r+")

# Add your code below!
for n in my_list:
    my_file.write(str(n) + "\n")

my_file.close()
```

### 1.4 Reading / 读取

最后，我们还需要学习如何从我们的 `output.txt` 中读取数据。我们，通过 `read()` 函数完成这个：
```python
my_file.read()
```

**指南**

01. 声明一个变量，`my_file`，然后为其赋值为`output.txt` 和 `open()`返回的文件变量。 （output.txt文件中已经有内容、数据了）
02. 用 `read()` 函数从中读取数据。当前一步使用open函数时采用"r"模式。使用 `print` 语句这样可以看到读取的结果。
03. 确保完成所有的操作后关闭文件。如果没有做这一步可能发生各种错误。

```python
my_file = open("output.txt","r")

s = my_file.read()
print s

my_file.close()
```

## 2. The Devil's in the Details   / 细节中的问题

### 2.1 Reading Between the Lines / 逐行读取

如果想从文件中逐行读取数据而不是一次读入整个文件的内容该怎么处理呢？Python提供了 `readline()` 函数，这个函数正好满足了上述功能。如果打开了一个文件然后对这个文件对象调用 `readline()` 函数，你将读取到文件的第一行，之后继续调用 `readline()` 函数将依次返回后续的行。

**指南**

以只读 `"r"` 模式打开 `text.txt` 文件，然后将其赋给文件对象 `my_file`。在三个不同的行，输出调用 `readline()` 的结果。看看该函数是如何工作的。（最后别忘了关闭文件）

```python
my_file = open("text.txt", "r")
for i in range(0,3):
    print my_file.readline()

my_file.close()
```

### 2.2 PSA: Buffering Data / 

前面我们一直强调当完成文件操作的工作后要关闭文件，这里来说明一下原因。

在 I/O 过程中，数据是受保护(**buffered**)的：这意味着他们在被写入文件之前保存在一个临时的地方。在关闭文件之前，Python不会清除这些缓存(**flush the buffer**)的数据。

**指南**

阅读我们的糟糕的代码，并且运行他。你会发现没有在我们的read_file.read()文件中读取到任何数据！

增加一个 `write_file.close()` 在第九行以及 `read_file.close()` 在第13行。然后再执行一遍代码，这回就会看到数据读出来了。

```python
# Open the file for reading
read_file = open("text.txt", "r")

# Use a second file handler to open the file for writing
write_file = open("text.txt", "w")
# Write to the file
write_file.write("Not closing files is VERY BAD.")

write_file.close()

# Try to read from the file
print read_file.read()
read_file.close()
```

### 2.3 The 'with' and 'as' Keywords / with 和 as 关键字

编程的目的在于让电脑为我们工作。是否有什么办法让Python自动帮我们关闭我们的文件呢？

答案当然是肯定的，因为这是Python。

文件对象包含一对特殊的内置方法：`__enter__()` 和 `__exit__()`。细节在这里并不重要，重要的是当一个文件对象执行到 `__exit__()` 方法时，会自动关闭文件，如何调用这个方法呢？使用 `with` 和 `as` 。

语法示例如下：
```python
with open("file", "mode") as variable:
    # Read or write to the file
```

**指南**

浏览下面的代码。注意，我们并没有显示的 `close()` 关闭我们的文件，记住如果我们没有关闭文件，我们的数据会卡住。运行代码看看执行的结果如何。

```python
with open("text.txt", "w") as textfile:
    textfile.write("Success!")
```


### 2.4 Try It Yourself / 

上面的方法是有效的，我们的Python程序成功的在text.txt中写入了数据。

**指南**

现在我们自己来尝试一下：在`text.txt`中写入任何你喜欢的数据使用 `with...as` 。为文件对象指定一个通常使用的名字：`my_file`。

```python
with open("text.txt", 'w') as my_file:
    my_file.write("Happy")
```

### 2.5 Case Closed? / 

最后，我们希望有个方法可以测试我们打开过的文件是否已经关闭。有时我们打开了大量的文件对象，如果不注意，他们可能没有全部被关闭。我们该如何进行测试？

Python的文件对象有一个 `closed` 属性，当文件关闭时，该属性值为 `True` 否则为 `False` 。通过检查 `fileobject.closed` 属性，我们可以知道文件是否关闭，如果还开着则可以调用 `close()` 方法。

**指南**

在前例 `with...as` 代码的下面，做以下两件事：

01. 创建一个 `if` 语句，对 `.closed` 为 `False` 的文件显式调用 `close()` 方法。（这个if语句块不需要else）
02. 用 `print` 输出 `my_file.closed` 的值，确保文件确实关闭了

```python
with open("text.txt", 'w') as my_file:
    my_file.write("Happy")

if my_file.closed == False:
    my_file.close()

print my_file.closed
```
