Advanced Topics in Python
===
---
## Iteration Notions
我们已经学习了如何遍历 **表 (list) ** 中的元素，现在我们将学习以下三个点内容：
- 遍历更复杂的数据结构中的元素（如：dictionary）
- 动态的修改表（list），通过（list comprehensions）
- 切分表(list），通过表划分（slicing）

### Iterators for Dictionarys
先从*遍历 dictionary* 中的元素讲起，回想一下 dictionary 其实就是 *key（键）* 和 *value（值）* 得集合。Python的 `items()` 函数可以遍历 dictionary 中的各个元素，并且返回其 key/value 对。用法就是 `dictionary.tiems()` 。注意：*这个函数遍历dictionary时并不按照特定的顺序。*

可以尝试运行下面的例子：

``` python
my_dict = {
         "Name": "Stefan",
         "Age": 28,
         "Height": 175,
         "Weight": 62
}

print my_dict.items()

```


### keys( ) and values( )
从上面的操作可以看出 `items()` 函数返回一个 *tuple* 的序列（array），其中每个tuple包含了dictionary中的一个key/value对。同理：

- `keys()`函数，返回一个包含了dictionary中键key的序列，  
- `values()`函数，返回一个由dictionary中值value的序列，  

同样，上述两个函数也不能以指定的顺序返回 dictionary 中的 key 或 value

- 可以暂且将 **tuple** 理解为一个 *不可改变的表* *immutable list* 。（当然这只是过于简化的比较）tuple 有一对圆括号 `()` 包围，可以包含任意数据类型
 
可以将前面例子中的 `print` 语句改为 `print my_dict.keys()` 和 `print my_dict.values()`


### The 'in' Operator
