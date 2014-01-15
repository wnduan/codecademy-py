Introduction to Classes / 类
===

类(Classes) 是面向对象编程(OOP) 中的一个非常重要的部分。在本节课中我们会学习什么是类，他们为什么重要，以及如何有效使用他们。

## 1. Class Basics / 关于类的基本概念
### 1.1 Why Use Classes? / 为什么要使用类 

Python是一个面向对象 (object-oriented programming) 的编程语言，这意味着他通过操作 **对象(objects)** 来构件程序。可以把对象看作是一个单独的数据结构，他包含了数据 (data) 和函数 (function) ；对象(object) 的函数(function) 称之为 **方法(method)** 。例如，当你调用：
```python
len("Eric")
```

Python 会检查传递给 `len()` 的字符串对象是否有一个长度，如果有，则返回与之相关的 **属性值(attribute)**。当调用：
```python
my_dict.items()
```

Python 会检查 `my_dict` 是否有 `items()` 方法（所有的 dictionary 变量都有这个方法），如果找到了就会执行这个方法。

但到底是什么将 `"Eric"` 定义为字符串而将 `my_dict` 定义为一个dictionary呢？实际上他们就分别是 `str` 和 `dict` 类的实例(instances)。 类(classes)只是将相似的属性(attributes) 和方法(methods) 组织起来并且产生对象(objects) 的一个途径。

**指导**

学习下面的代码，我们定义了一个类，`Fruit`，然后创建了一个 `lemon` 实例，大致了解了之后就运行一下，看看结果，然后进入下一课。
```python
class Fruit(object):
    """A class that makes various tasty fruits."""
    def __init__(self, name, color, flavor, poisonous):
        self.name = name
        self.color = color
        self.flavor = flavor
        self.poisonous = poisonous
    
    def description(self):
        print "I'm a %s %s and I taste %s." % (self.color, self.name, self.flavor)
        
    def is_edible(self):
        if not self.poisonous:
            print "Yep! I'm edible."
        else:
            print "Don't eat me! I am super poisonous."

lemon = Fruit("lemon", "yellow", "sour", False)

lemon.description()
lemon.is_edible()
```

### 1.2 Class Syntax / 声明类的语法规则 

一个基本的类可以仅包括 `class` 关键字、类的名字、以及括号中被继承的类（新定义的类将继承这个类）。（这个继承(inheritance) ）之后会提到。现在，我们的类将继承 `object` 类，像这样：
```python
class NewClass(object):
    # Class magic here
```

这使他们有了一个 Python 对象的属性和能力。一般约定，用户自定义的 Python 类，类名以大写字母开头。

**指导**

创建一个名为 `Animal` 的类。现在，在类的内部，加上一个 `pass` 语句。（ `pass` 什么都不做，但是起到一个占位符的作用）
```python
class Animal(object):
    pass
```

### 1.2 Classier Classes / 更像是类的类

在做了上面的例子之后，当然我们会希望我们创建了类会更有用，所以我们需要把那里的 pass 语句变成其他的什么东西。

之前，在最开始的第一个例子，可能已经注意到了在我们定义了我们的类之后，紧接着出现了一个看起来很奇怪的函数：`__init__()`。类需要用这个函数来 **初始化(initialize)** 其创建的对象。`__init__()` 包含至少一个声明（输入参数），`self`，指向被创建的对象自己。可以认为 `__init__()` 启动了类创建的每个对象。

**指导**

移除上一小节的练习中的 `pass` 语句。在 `Animal` 类中定义一个 `__init__()` 函数。现在先将 `self` 声明传给这个函数，我们之后再详细解释。最后，在 `__init__()` 函数体中加上 `pass` 语句
```python
class Animal(object):
    def __init__(self):
        pass
```

### 1.3 Let's Not Get Too Selfish / 不要太自私

现在进一步调整我们的类的定义，然后我们将实例化(instantiate)/创建 我们的第一个对象(object)。

目前为止，`__init__()` 只接受一个参数：`self`。这只是一个 Python 的惯例，`self` 这个词并没有什么神奇的。但是，绝大多数常见的情况下都会使用 `self` 作为 `__init__()` 的第一个参数，所以你也应该这样做，这样别人才能够更容易读懂你的代码。

真正神奇的部分是，`self` 是 *第一个* 传递给 `__init__()` 的参数。Python 将会用 `__init__()` 接收到的第一个参数指向创建的对象；这就是为什么总是调用self，因为这个参数定义了被创建的对象的特性。

**指导**

我们接前面的练习，做两件事：

**01.** 向 `__init__()` 传递第二个参数 `name`

**02.** 在 `__init__()` 内，让函数知道，上面的 `name` 指向创建的对象的名字用 `self.name = name` 语句实现 （在下一个小节就会变得清晰透彻）

```python
class Animal(object):
    def __init__(self, name):
        self.name = name
```

### 1.4 Instantiating Your First Object / 实例化一个对象

有了之前的基础，我们可以创建对象了。

我们现在要做两件事：

**01.** 创建一个名为 `"Jeffrey"` 的 `zebra`，他将是我们的 `Animal` 类的一个实例 

**02.** 在屏幕上 `print` 出我们的 `zebra` 的名字。

我们可以通过 `.` **点符号(dot notation)** 访问我们的对象的属性。例如，我们定义了一个对象的 `age` ，当我们需要获得这个属性时，可以输入：
```python
our_object.age
```

**指导**

根据上面的要求，完成这个练习。

**01.** 在类定义的外部，创建一个名为 `zebra` 的变量，使他等于 `Animal()` 。在括号内，传递字符串 `"Jeffrey"`

**02.** 在屏幕 `print` 出 `zebra` 的名字

```python
class Animal(object):
    def __init__(self, name):
        self.name = name

zebra = Animal("Jeffrey")
print zebra.name
```

## 2. Member Variables and Functions / 成员变量和函数
### 2.1 More on __init__() and self / 关于 __init__() 和 self 的更多内容

现在我们已经初步了解了类和对象是如何工作的，现在我们来进一步的钻研一下 `__init__()` 和 `self` 。 很容易让人糊涂的两个概念。

之前提过，可以将 `__init__()` 看成一个用来启动由类实例化成的对象的方法：init 本来就是 初始化("initialize") 的缩写。

传统上，`__init__()` 方法获得的第一个声明(argument) 【这个声明其实也就是传递进来的参数】用于指向实例对象，这个声明就是 `self`。如果需要增加其他的声明，例如你的animal的 `name` 和 `age` ，则在 `__init__()` 函数内另他们等于`self.name` 和 `self.age` ，这样当你创建一个 `Animal` 类的实例对象时，你需要给每个实例指定一个名字和年龄，这些变量将与特定的实例相关联。

**指导**

根据上面的内容，和已经给出的代码，看看 `__init__()` 如何启动每一个对象接收一个名字和年龄的输入，然后用 `self.name` 和 `self.age` 把这些名字赋给每一个对象。

之后，增加第三个属性，`is_hungry` ，之后查看代码运行的结果

```python
# Class definition
class Animal(object):
    """Makes cute animals."""
    # For initializing our instance objects
    def __init__(self, name, age, is_hungry):
        self.name = name
        self.age = age
        self.is_hungry = is_hungry

# Note that self is only used in the __init__()
# function definition; we don't need to pass it
# to our instance objects.

zebra = Animal("Jeffrey", 2, True)
giraffe = Animal("Bruce", 1, False)
panda = Animal("Chad", 7, True)

print zebra.name, zebra.age, zebra.is_hungry
print giraffe.name, giraffe.age, giraffe.is_hungry
print panda.name, panda.age, panda.is_hungry
```

### 2.2 Class Scope / 类的作用域

关于Python类的另一个重要方面是范围(scope)。一个变量的范围(scope)是一个对程序可见的环境？？。(The scope of a variable is the context in which it's visible to the program.)

可能你会觉得惊讶，并不是所有的变量都能在任意时刻被Python程序访问。当处理类时，你可以定义在哪都可以被访问的变量 **（全局变量(global variables)）**，只能被某些类的成员访问的变量 **（成员变量(member variables)）**，以及只能被类的某些特殊实例访问的变量 **（实例变量(instance variables)）**。

对函数(function)也是一样：有些在哪都可以访问，有些只能被某个类的成员访问，其他的一些只能被特殊的实例对象访问。

**指导**

阅读并学习下面的代码。注意每个单独的animal都有他自己的 `name` 和 `age` （因为他们都是各自独立初始化的）。但是每个单独的对象都可以访问成员变量(member variable) `is_alive` ， 因为他们都是 `Animal` 类的成员。执行代码看看结果。

```python
class Animal(object):
    """Makes cute animals."""
    is_alive = True
    def __init__(self, name, age):
        self.name = name
        self.age = age

zebra = Animal("Jeffrey", 2)
giraffe = Animal("Bruce", 1)
panda = Animal("Chad", 7)

print zebra.name, zebra.age, zebra.is_alive
print giraffe.name, giraffe.age, giraffe.is_alive
print panda.name, panda.age, panda.is_alive
```

### 2.3 A Methodical Approach / 一个有条理的方法

当一个类有其自己的函数时，这些函数称为方法（即类的函数称为方法）。前面已经见过类似：`__init__()` 这样的方法。但是，除此之外还可以定义你自己的方法。

**指导**

为你的 `Animal` 类增加一个 `description` 方法。使用两个单独的 `print` 语句，在屏幕输出动物的名字和年龄。然后，创建一个 `Animal` 的实例，`hippo` ，为他起一个名字和定义他的年龄，然后调用他的 `description` 方法。
```python
class Animal(object):
    """Makes cute animals."""
    is_alive = True
    def __init__(self, name, age):
        self.name = name
        self.age = age
    # Add your method here!
    def description(self):
        print self.name
        print self.age

hippo = Animal("tiger", 5)
hippo.description()
```

### 2.4 They're Multiplying! / 

一个类可以有任意数量的 *成员变量* 。这些是可以被类的所有成员访问的：例如我们的 `Animal` 类的 `is_alive` 成员变量。

**指导**

为 `Animal` 类增加一个成员变量，`health` ，为其赋值字符串 `"good"` 。然后，创建两个新的 `Animals` ：`sloth` 和 `ocelot` 。（为其指定任意的名字和年龄）。最后，在屏幕上输出 `hippo` ，`sloth` 和 `ocelot` 的 `health` 。
```python
class Animal(object):
    """Makes cute animals."""
    is_alive = True
    health = "good"
    def __init__(self, name, age):
        self.name = name
        self.age = age
    # Add your method here!
    def description():
        print self.name
        print self.age

hippo = Animal("Ann", 5)
sloth = Animal("Bobby", 2)
ocelot = Animal("Duan", 10)

print hippo.health
print sloth.health
print ocelot.health
```

### 2.5 It's Not All Animals and Fruits / 

前面介绍的 `Animal` 和 `Fruit` 类，可以帮助我们理解类和实例的概念，但是实际的编程中你可能很少会见到zebras或lemons这类东西。

但是，类和对象确经常用来描述真实世界中的事物。下面的代码更接近真实世界中使用的类和对象。在这里，我们有一个基本的 `ShoppingCart` 类，用于为网络购物创建购物车对象。尽管很基本，但这和你在真实的程序中见到的是很相似的。

**指导**

创建一个 `ShoppingCart` 的实例，名为 `my_cart` 。为其定义任意初始值，之后调用 `add_item` 方法为购物车增加一个商品。
```python
class ShoppingCart(object):
    """Creates shopping cart objects
    for users of our fine website."""
    items_in_cart = {}
    def __init__(self, customer_name):
        self.customer_name = customer_name
        
    def add_item(self, product, price):
        """Add product to the cart."""
        if not product in self.items_in_cart:
            self.items_in_cart[product] = price
            print product + " added."
        else:
            print product + " is already in the cart."
        
    def remove_item(self, product):
        """Remove product from the cart."""
        if product in self.items_in_cart:
            del self.items_in_cart[product]
            print product + " removed."
        else:
            print product + " is not in the cart."

my_cart = ShoppingCart("Stefan")
my_cart.add_item("Nike", 68.5)
```

## 3. Inheritance  / 继承
### 3.1 Warning: Here Be Dragons / 

**继承(inheritance)** 是一个有点复杂的概念，我们一步步来看。

通过继承(inheritance)，一个类可以获得另外一个类的属性（变量）和方法。继承表示了一种 **什么是什么(is-a)** 的关系。例如，熊猫是熊(a Panda **is a** bear)，所以，熊猫(Panda)类可以从熊(Bear)类继承而来。但丰田汽车不是拖拉机(a Toyota is not a Tractor)，尽管他们有很多共同之处，Toyota 不能从 Taractor 继承而来。Toyota 和 Tractor 都可以从 Vehicle 类继承来。

**指导**

浏览下面的代码。我们定义了一个类，`Customer`，和另一个继承自 `Customer` 的 `ReturningCustomer` 类。我们并没有在 `ReturningCustomer` 的内部定义 `display_cart` 方法，但是仍然可以通过继承来访问这个方法。运行代码看看结果。
```python
class Customer(object):
    """Produces objects that represent customers."""
    def __init__(self, customer_id):
        self.customer_id = customer_id
    
    def display_cart(self):
        print "I'm a string that stands in for the contents of your shopping cart!"

class ReturningCustomer(Customer):
    """For customers of the repeat variety."""
    def display_order_history(self):
        print "I'm a string that stands in for your order history!"

monty_python = ReturningCustomer("ID: 12345")
monty_python.display_cart()
monty_python.display_order_history()
```

### 3.2 Inheritance Syntax / 

在 Python 中，继承用下面的方式实现：
```python
class DerivedClass(BaseClass)
```

其中派生类(derived class)，是要创建的新类。新的类继承自基础类(base class)。

**指导**

已经给出的代码，建立了一个 `Shape` 类。创建你自己的类 `Triangle` ，继承自 `Shape`。

新的类应该有自己的 `__init__()` 函数，应该接受四个输入：`self`, `side1`, `side2` 和 `side3`。
```python
class Shape(object):
    """Makes shapes!"""
    def __init__(self, number_of_sides):
        self.number_of_sides = number_of_sides

# Add your Triangle class below!
class Triangle(Shape):
    def __init__(self, side1, side2, side3):
        self.side1 = side1
        self.side2 = side2
        self.side3 = side3
```

### 3.3 Override / 改写

有时候当一个对象继承自另一个对象时，我们不仅希望新的对象可以继承到父对象的属性和方法，而且希望能够 **改写(override)** 其中的一个或一些。

例如，你有一个 `PartTimeEmployee` 类，继承自 `Employee` 类。这两个类都有一个 `calculate_wage` 方法用于计算双周的薪水，但对小时雇员和其他雇员的计算方法不同。这时候，与其在派生类增加一个 `calculate_part_time_wage` 方法，同时又继承了一个永远也用不到的 `calculate_wage` 方法，就不如直接在派生类显式的声明创建一个 `calculate_wage` 方法返回适合的小时雇员的薪水，这个新的计算就会覆盖(override) 继承来的方法。

**指导**

创建一个新的类，`PartTimeEmployee`，继承自 `Employee` 类。为你的派生类定义一个 `calculate_wage` 方法，覆盖原有的 `Employee` 类的；新的方法返回小时雇员的的薪资按每小时$12.00计算。
```python
class Employee(object):
    """Models real-life employees!"""
    def __init__(self, employee_name):
        self.employee_name = employee_name
    
    def calculate_wage(self, hours):
        self.hours = hours
        return hours * 20.00

# Add your code below!
class PartTimeEmployee(Employee):
    def calculate_wage(self, hours):
        self.hours = hours
        return hours * 12.00
```

### 3.4 This Looks Like a Job For... / 

另一方面，有时候你在一个派生类（子类）**(subclass)** 中进行开发时，发现需要用到某个基类（或称为父类）**(parent or superclass)** 中定义的属性或方法，而该方法已经被你改写过了。这时候，不必担心，可以通过Python内置的 `super` 调用直接调用父类中的属性和方法。

其使用的语法如下：
```python
class DerivedClass(Base):
   def some_method(self):
       super(DerivedClass, self).meth()
```

其中 `meth()` 是基类中定义的一个方法。

**指导**

为 `PartTimeEmployee` 增加一个 `full_time_wage` 方法。令其返回 `super` call 调用 `PartTimeEmployee` 父类的 `calculate_wage` 方法的结果。

最后，创建一个 `PartTimeEmployee` 的实例 `milton` ，然后输出调用 `full_time_wage` 方法的结果。（这个结果应该是以$20.00每小时计算，输出10个小时的计算结果）。

```python
class Employee(object):
    """Models real-life employees!"""
    def __init__(self, employee_name):
        self.employee_name = employee_name
    
    def calculate_wage(self, hours):
        self.hours = hours
        return hours * 20.00

# Add your code below!
class PartTimeEmployee(Employee):
    def calculate_wage(self, hours):
        self.hours = hours
        return hours * 12.00

    def full_time_wage(self, hours):
        return super(PartTimeEmployee, self).calculate_wage(hours)

milton = PartTimeEmployee("Milton")
print milton.full_time_wage(10)

```

## 4. Review / 回顾

### 4.1 Class Basics / 类基础

首先，创建一个类。

**指导**

创建一个类，`Triangle` 。 他的 `__init__()` 方法接受 `self`, `angle1`, `angle2`, 和 `angle3` 作为输入声明。确保在 `__init__()` 方法内进行正确的设置。

```python
class Triangle(object):
    def __init__(self, angle1, angle2, angle3):
        self.angle1 = angle1
        self.angle2 = angle2
        self.angle3 = angle3
        print "A Triangle have been created."
```

### 4.2 Class It Up / 

接下来，为我们的类创建一个成员变量和方法。

**指导**

为 `Triangle` 类定义一个成员变量，`number_of_sides` ，为其赋值 `3`。

为 `Triangle` 类定义一个 `check_angles` 方法。返回一个逻辑值，如果三个角的和为180度则返回 `True` 否则返回 `False`。

```python
class Triangle(object):
    number_of_sides = 3
    def __init__(self, angle1, angle2, angle3):
        self.angle1 = angle1
        self.angle2 = angle2
        self.angle3 = angle3
        print "A Triangle have been created."

    def check_angles(self):
        total = self.angle1 + self.angle2 + self.angle3
        nonnegative = self.angle1 > 0 and self.angle2 > 0 and self.angle3 > 0
        if total == 180 and nonnegative:
            return True
        else:
            return False
```

### 4.2 Instantiate an Object / 创建一个实例

创建一个 `Triangle` 类的实例。

**指导**

创建一个 `Triangle` 类的实例， `my_triangle` 。为他赋予有效的角度。然后输出 `number_of_sides` 属性和调用 `check_angles()` 方法的结果。

```python
"""接上例..."""
my_triangle = Triangle(30,45,105)
print my_triangle.number_of_sides
print my_triangle.check_angles()
```

### 4.3 Inheritance / 继承

最后，我们来建立一个 `Equilateral` 类，继承自 `Triangle` 类。（equilateral 等边三角形）

**指导**

定义一个 `Equilateral` 类，继承自 `Triangle` 类。他应该包含一个成员变量，`angle` ，为其赋值 `60`。最后，仅用参数 `self` 初始化， 并且将 `self.angle1` 到 `self.angle3` 赋值为成员变量 `self.angel`。

```python
"""接上例..."""
class Equilateral(Triangle):
    angle = 60
    def __init__(self):
        self.angle1 = self.angle
        self.angle2 = self.angle
        self.angle3 = self.angle
```


