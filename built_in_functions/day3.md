# 内置函数

## callable(object)  

如果 object 参数可调用，则返回 True，否则返回 False。如果返回 true，也有可能调用失败，但如果是 false，调用 object 将永远不会成功。请注意，类是可调用的（调用一个类返回一个新的实例）; 如果类有一个 __call __()方法，则实例可以被调用。

>示例
```python
In [1]: a = 1
In [2]: callable(1)
Out[2]: False

In [3]: class A: 
   ...:     pass 
   ...:
In [4]: callable(A)
Out[4]: True

In [5]: a = A()
In [6]: callable(a)
Out[6]: False

In [7]: class B: 
   ...:     def __call__(self, *args, **kwargs): 
   ...:         pass 
   ...:
In [8]: b = B()
In [9]: callable(b)
Out[9]: True
```

## chr(i)  
返回表示 Unicode 代码点为整数 i 的字符的字符串。  
例如，chr(97) 返回字符串 'a'，而 chr(8364) 返回字符串 '€'。这是 ord() 的逆过程。  
参数的有效范围是从 0 到 1,114,111（基于 16 的 0x10FFFF）。如果超出这个范围，将会抛出 ValueError。

> 示例
```python
In [1]: chr(97)                                
Out[1]: 'a'

In [2]: ord('a')                                          
Out[2]: 97

In [3]: chr(0)
Out[3]: '\x00'

In [4]: chr(1114111)
Out[4]: '\U0010ffff'
```

## @classmethod
略

## compile(source, filename, mode[, flags[, dont_inherit]])
它可以把传入的python语句编译成AST（Abstract Syntax Trees）对象，AST是python的抽象语法树，AST可以看成是python代码分析后的中间结果，最后会被编译成python虚拟机代码执行。

```python
In [1]: c = compile('x=1;y=2;print(x+y)','','exec')
In [2]: c
Out[2]: <code object <module> at 0x7f92664706f0, file "", line 1>
In [3]: exec(c)
3
```

作为source参数传入，filename为空，mode是告诉compile编译模式可以选择的有 'exec' ，'eval'， 'single' 我们选择'exec'可以被exec执行，最后使用exec执行AST对象。

## delattr(object, name)
跟setattr()是相对的。name作为字符串，必须是object的属性之一，delattr用来删除对象的属性。 `delattr(x, "foobar")`等价于`del x.foobar`

## dict
`class dict(**kwarg)`  
`class dict(mapping, **kwarg)`  
`class dict(iterable, **kwarg)`  

创建一个字典
> 示例

```python
In [1]: dict(name='gengleiming', gender=1)
Out[1]: {'name': 'gengleiming', 'gender': 1}

In [2]: dict({"name":"gengleiming", "gender":1}, age=18, address="shenzhen")
Out[2]: {'name': 'gengleiming', 'gender': 1, 'age': 18, 'address': 'shenzhen'}

In [3]: dict([("name", "gengleiming"), ("gender", 1), ("age", 1)])
Out[3]: {'name': 'gengleiming', 'gender': 1, 'age': 1}

In [4]: dict([("name","gengleiming"), ("gender", 1)], age=18, address="shenzhen")
Out[4]: {'name': 'gengleiming', 'gender': 1, 'age': 18, 'address': 'shenzhen'}
```

## dir([object])
尝试返回 object 的有效属性列表。如果没有参数，则返回当前本地作用域中的名称列表。  
如果对象具有名为 __dir__() 的方法，则将调用此方法，并且必须返回属性列表。  
这允许实现自定义 __getattr__()或 __getattribute__() 函数的对象自定义 dir() 报告其属性。  
默认的 dir() 机制对不同类型的对象有不同的表现，因为它试图产生最相关的信息，而不是完整的信息：
1. 如果对象是模块对象，则列表包含模块属性的名称。
2. 如果对象是一个类型或类对象，则该列表包含其属性的名称，并递归地显示其基础的属性。
3. 否则，该列表包含对象的属性名称，其类属性的名称以及其类的基类的属性的递归。

结果列表按字母顺序排序。例如：  
```python
In [1]: import struct
In [2]: dir()
Out[2]: 
['In',
 'Out',
 '_',
 '__',
 '___',
 '__builtin__',
 '__builtins__',
 '__doc__',
 '__loader__',
 '__name__',
 '__package__',
 '__spec__',
 '_dh',
 '_i',
 '_i1',
 '_i2',
 '_ih',
 '_ii',
 '_iii',
 '_oh',
 'exit',
 'get_ipython',
 'quit',
 'struct']

In [3]: dir(struct)
Out[3]: 
['Struct',
 '__all__',
 '__builtins__',
 '__cached__',
 '__doc__',
 '__file__',
 '__loader__',
 '__name__',
 '__package__',
 '__spec__',
 '_clearcache',
 'calcsize',
 'error',
 'iter_unpack',
 'pack',
 'pack_into',
 'unpack',
 'unpack_from']

In [4]: class Shape: 
   ...:     def __dir__(self): 
   ...:         return ["area", "perimeter", "location"] 
   ...:

In [5]: dir(Shape)                               
Out[5]: 
['__class__',
 '__delattr__',
 '__dict__',
 '__dir__',
 '__doc__',
 '__eq__',
 '__format__',
 '__ge__',
 '__getattribute__',
 '__gt__',
 '__hash__',
 '__init__',
 '__init_subclass__',
 '__le__',
 '__lt__',
 '__module__',
 '__ne__',
 '__new__',
 '__reduce__',
 '__reduce_ex__',
 '__repr__',
 '__setattr__',
 '__sizeof__',
 '__str__',
 '__subclasshook__',
 '__weakref__']

In [6]: s = Shape()
In [7]: dir(s)
Out[7]: ['area', 'location', 'perimeter']
```

## divmod(a, b)
以两个（非复数）数字作为参数，并在使用整数除法时返回由它们的商和余数组成的一对数字。  
使用混合操作数类型时，适用二元算术运算符的规则。  
对于整数，结果与 (a // b, a % b) 相同。  
对于浮点数，结果是 (q, a % b)，其中 q 通常是 math.floor(a / b)，但可能小于 1。  
在任何情况下， q * b + a % b 都非常接近 a，如果 a % b 不为零，则它具有与 b 相同的符号，并且 0 <= abs(a % b) < abs(b)。
>示例
```python
In [1]: divmod(10, 3)
Out[1]: (3, 1)

In [2]: divmod(10.1, 3)
Out[2]: (3.0, 1.0999999999999996)

In [3]: divmod(1.2, 1)
Out[3]: (1.0, 0.19999999999999996)
```

## enumerate(iterable, start=0)
返回一个枚举对象。   
iterable 必须是一个可迭代对象。  
由 enumerate() 返回的迭代器的 __next__() 方法返回一个元组，该元组包含一个计数（从 start 开始，默认值为 0）以及遍历迭代获得的值。

>示例
```python
In [1]: seasons = ['Spring', 'Summer', 'Fall', 'Winter']
In [2]: list(enumerate(seasons))
Out[2]: [(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]

In [3]: list(enumerate(seasons, start=2))
Out[3]: [(2, 'Spring'), (3, 'Summer'), (4, 'Fall'), (5, 'Winter')]
```