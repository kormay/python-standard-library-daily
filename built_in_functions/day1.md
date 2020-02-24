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
all([])
all(1,2,3)
all([0, 7, 9])
all([False, True, True])
```
