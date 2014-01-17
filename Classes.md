Classes / 关于类的更多内容
===
解决一个具体问题，创建一个类并且实现一个实例。

## 1. A Review of Class / 类的回顾

### 1.1 Class basics / 基础内容

类可以用于存储复杂的，包含自己的变量和方法的对象。定义一个类与定义函数相类似，但我们用 `class` 关键字来代替。同时我们用括号中的 `object` 关键字，因为我们希望我们的类由 `object` 继承而来，这是最简单最基础的类。在后面的课程中我们会看到继承其他更复杂类的类。一个空的类，看起来应该是这样的：
```python
class ClassName(object):
    # class statements go here
```

**指南**

定义一个名为 `Car` 的类。现在，因为必须在类的内部写点儿什么，因此先用 `pass` 关键字代替
```python
class Car(object):
    pass
```

### 1.2 Create an instance of a class / 创建一个实例

我们可以用类来创建新的对象，我们称之为这些类的实例。

创建类的一个实例非常简单：
```python
newObject = ClassName()
```

**指南**

在 `Car` 类后面，创建一个 `my_car` 的实例：
```python
class Car(object):
    pass

my_car = Car()
```

### 1.3 Class member variables / 类成员变量

类可以拥有成员变量，存储了类的每个对象都可访问的信息。之所以称其为成员变量，就是因为他们是属于类的对象的信息。

创建成员变量并为其赋予初值，就与创建其他变量一样容易：
```python
class ClassName(object):
    memberVariable = "initialValue"
```

**指南**

在 `Car` 类中，用新的成员变量 `condition` 替代原来的 `pass` 语句，为其赋值字符串 `"new"`.
```python
class Car(object):
    condition = "new"
my_car = Car()
```

### 1.4 Calling class member variables / 调用成员变量

我们创建的类的每个对象都有他自己的一套成员变量。因为我们已经创建了 `Car` 类的实例 `my_car` 对象，`my_car` 也就有了名为 `condition` 的成员变量。这个属性值在 `my_car` 创建的时候就被赋值了。

**指南**

在你代码的最后，用 `print` 语句输出 `my_car` 的 `condition`.
```python
class Car(object):
    condition = "new"
my_car = Car()
print my_car.condition
```

### 1.5 Initializing a class / 类的初始化

有一个 *特殊的* 函数 `__init__()` ，每当创建一个实例时就会调用该函数。一般，默认都存在这个函数，即使我们看到不到他。但是，我们也可以定义我们自己的 `__init__()` 函数，从而覆盖原有的版本。我们可能需要通过定义自己的初始化函数而提供更多的输入变量，就想其他的函数那样。

第一个传给 `__init__()` 的声明变量应该永远是 `self` 关键词 - 这是对象在自己内部访问自己的的方式 - 在其之后还可以定义其他附加的输入变量。

为了赋值给一个类（创建一个成员变量），我们使用 *dot notation* 点符号。例如，如果我们将 `newVariable` 传递给我们的类，那么在 `__init__()` 内部，我们应该用如下语句：
```python
self.new_variable = new_variable
```

**指南**

为 `Car` 类定义一个 `__init__()` 函数，接受四个输入：`self`, `model`, `color`, 和 `mpg`。使用 `self` 将后面三个输入赋值给同名的成员变量。

然后，修改 `my_car` 对象，在初始化时提供下列输入：
```python
model = "DeLorean"
color = "silver"
mpg = 88
```

当创建一个类的实例时，不需要包括 `self` 关键词，因为类定义时会自动把 `self` 增加到输入列表的第一个。
```python
class Car(object):
    condition = "new"
    def __init__(self, model, color, mpg):
        self.model = model
        self.color = color
        self.mpg = mpg

my_car = Car("DeLorean", "silver", 88)
print my_car.condition
```

### 1.6 Referring to member variables / 引用成员变量

使用类的成员变量，不管这些值是在类的代码中创建的还是在新对象初始化时传入的，都是一样的。我们使用 *dot notation* 点符号来访问成员变量，因为这些变量属于对象。

例如，如果我们创建了一个名为 `new_variable` 的成员变量，该类的一个新的实例 `new_object` 可以访问这个变量：
```python
new_object.new_variable
```

**指南**

现在，我们已经创建了 `my_car` 并且为他的成员变量赋值，用 `print` 分三行输出 `my_car` 的 `model`, `color`, 和 `mpg`。
```python
class Car(object):
    condition = "new"
    def __init__(self, model, color, mpg):
        self.model = model
        self.color = color
        self.mpg = mpg

my_car = Car("DeLorean", "silver", 88)
print my_car.condition
print my_car.model
print my_car.color
print my_car.mpg
```

## 2. Using Classes  / 类的使用

### 2.1 Creating class methods / 创建类的方法

除了成员变量，类还可以拥有他们自己的方法。定义这些类的方法与定义其他函数相同，除了他们是在类的内部定义的。与我们定义 `__init__()` 函数一样，定义其他方法时也应该提供 `self` 作为第一个声明变量。

**指导**

为 `Car` 增加一个 `display_car()` 方法，该方法引用 `Car` 的成员变量，返回一个字符串， "This is a [color] [model] with [mpg] MPG." 可以使用 `str()` 函数将 `mpg` 转换为string。

用一个 `print` 命令显示调用 `display_car()` 的结果，换掉前面的 `print` 语句
```python
class Car(object):
    condition = "new"
    def __init__(self, model, color, mpg):
        self.model = model
        self.color = color
        self.mpg = mpg
    def display_car(self):
        return "This is a %s %s with %d MPG." % (self.color, self.model, self.mpg)

my_car = Car("DeLorean", "silver", 88)
print my_car.display_car()
```

### 2.2 Modifying member variables / 修改成员变量

我们可以修改属于类的变量就像我们初始化那些成员变量一样。当我们想根据类的方法改变一个变量的值时，这会很有用。

**指导**

为 `Car` 类增加一个 `drive_car()` 方法，他会将 `Car` 的 `condition` 变量变为字符串 `"used"`。 

然后，移除调用 `my_car.display_car()` 方法，改为仅输出 `condition` 。然后，通过调用 `drive_car()` 方法来驾驶一下你的车，之后用 `print` 输出 `condition` 看看结果有什么变化。
```python
class Car(object):
    condition = "new"
    def __init__(self, model, color, mpg):
        self.model = model
        self.color = color
        self.mpg = mpg

    def display_car(self):
        return "This is a %s %s with %d MPG." % (self.color, self.model, self.mpg)

    def drive_car(self):
        self.condition = "used"

my_car = Car("DeLorean", "silver", 88)
print my_car.condition
my_car.drive_car()
print my_car.condition
```

### 2.3 Inheritance / 继承

使用类的一个好处是，我们可以通过继承父类 **(parent classes)** 的变量和方法而创建更加复杂的类。这可以节约大量的开发时间，并且帮助我们建立更复杂的对象，因为这些子类 **(child classes)** 也可以包括额外附加变量和方法。

我们定义一个子类，他从父类继承了所有的变量和函数：
```python
class ChildClass(ParentClass):
    # new variables and functions go here
```

通常，我们用 `object` 作为父类，因为这是最基本的一个类，但是通过指定不同的类，我们可以继承更多复杂的功能。

**指导**

创建一个类 `ElectricCar` 继承自 `Car` 。为你的新类定义一个 `__init__()` 方法增加一个 `"battery_type"` 成员变量。

然后，创建一个电动车实例，`my_car` ，拥有一个 `"molten salt"` 电池类型。并且为其他另外三个输入的参数(model, color and mpg)赋值。

```python
class Car(object):
    condition = "new"
    def __init__(self, model, color, mpg):
        self.model = model
        self.color = color
        self.mpg = mpg

    def display_car(self):
        return "This is a %s %s with %d MPG." % (self.color, self.model, self.mpg)

    def drive_car(self):
        self.condition = "used"

class ElectricCar(Car):
    def __init__(self, model, color, mpg, battery_type):
        self.model = model
        self.color = color
        self.mpg = mpg
        self.battery_type = battery_type

my_car = ElectricCar("DeLorean", "silver", 88, "molten salt")
```

### 2.4 Overriding methods / 覆盖改写方法

因为我们的 `ElectricCar` 是 `Car` 的一种更加特殊的类型，我们可以为 `ElectricCar` 定义他自己的 `drive_car()` 方法，与原始的 `Car` 类的不同。

**指导**

在 `ElectricCar` 中增加一个新的 `drive_car()` 方法，改变 `condition` 变量为字符串 `"like new"`。然后，用`drive_car()` 方法驾驶你的电动车，并且分别在之前和之后用 `print` 输出 `condition` 。 
```python
class Car(object):
    condition = "new"
    def __init__(self, model, color, mpg):
        self.model = model
        self.color = color
        self.mpg = mpg

    def display_car(self):
        return "This is a %s %s with %d MPG." % (self.color, self.model, self.mpg)

    def drive_car(self):
        self.condition = "used"

class ElectricCar(Car):
    def __init__(self, model, color, mpg, battery_type):
        self.model = model
        self.color = color
        self.mpg = mpg
        self.battery_type = battery_type

    def drive_car(self):
        self.condition = "like new"

my_car = ElectricCar("DeLorean", "silver", 88, "molten salt")
print my_car.condition
my_car.drive_car()
print my_car.condition
```

### 2.5 Building useful classes / 建立有用的类

可能你不会马上就在现实生活中设计并使用一个 `Car` 类。通常，类最有用的地方是，可以用于存储和访问抽象的数据集合。

一个可以改写的有用的方法是内置的 `__repr__()` 方法，是 **representation** 的简称。通过在这个方法中提供一个返回值，我们可以告诉Python如何代表类的一个对象（？）（例如当我们用 `print` 语句时）

**指导**

定义一个 `Point3D` 类，继承自 `object` 。包括一个自定义的 `__init__()` 函数，接受三个数（当然还有 `self` 关键词）并且将这些数赋值给成员变量x, y 和 z.
之后，创建一个 `Point3D` 的实例 `my_point` ， 使 x=1, y=2, z=3。

改写 `__repr__()` 方法，使得你可以用 `print` 输出 `my_point` 显示对象用下面的格式：`(1, 2, 3)`。

```python
class Point3D(object):
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z

    def __repr__(self):
        s = "(%s, %s, %s)" % (str(self.x), str(self.y), str(self.z))
        return s

my_point = Point3D(1,2,3)
print my_point
```