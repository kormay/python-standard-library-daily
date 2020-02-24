# 内置函数

## abs(x)

返回整数或浮点数的绝对值

```python
In [1]: abs(-1)
Out[1]: 1

In [2]: abs(-28.9)
Out[2]: 28.99
```

如果对象x定义了__abs__()方法，那么abs(x)返回x.__abs__()

>示例：

```python
In [3]: class X:
   ...:     def __abs__(self):
   ...:         return 10000
   ...:

In [4]: x = X()

In [5]: abs(x)
Out[5]: 10000

In [6]: x.__abs__()
Out[6]: 10000
```

## all(iterable)

如果可迭代对象所有元素都为真，或者可迭代对象没有元素，那么返回True  

相当于：

```python
In [7]: def all(iterable):
   ...:     for element in iterable:
   ...:         if not element:
   ...:             return False
   ...:     return True
```

>示例：

```python
In [10]: all([])
Out[10]: True

In [11]: all([0,7,9])
Out[11]: False

In [12]: all([True, False, True])
Out[12]: False)
```

## any(iterable)

如果可迭代对象任意一个元素为真，那么返回True。如果可迭代对象没有元素，那么返回False

相当于:

```python
In [1]: def any(iterable):
   ...:     for element in iterable:
   ...:         if element:
   ...:             return True
   ...:     return False
```

>示例

```python
In [6]: any([])
Out[6]: False

In [7]: any([0, 0, 0])
Out[7]: False

In [8]: any([True, False, False])
Out[8]: True

In [9]: any([1, 0, 0])
Out[9]: True
```

## ascii(object)

Python ascii()函数和repr() 函数有点类似，返回一个表示对象的字符串, 但是对于字符串中的非 ASCII 字符则返回通过 repr() 函数使用 \x, \u 或 \U 编码的字符。 生成类似 Python2 版本中 repr() 函数返回的字符串。

>示例
```python
In [1]: ascii([1,2])
Out[1]: '[1, 2]'

In [2]: ascii({1:2,'name':5})
Out[2]: "{1: 2, 'name': 5}"

In [3]: ascii("我geng")
Out[3]: "'\\u6211geng'"

In [4]: repr("我geng")
Out[4]: "'我geng'"
```

## bin(x)

bin() 返回一个`'0b'`开头字符串，作为整数int或者长整数long int的二进制表示。

>示例：

```python
In [1]: bin(10)
Out[1]: '0b1010'

In [2]: bin(-5)
Out[2]: '-0b101'

```
