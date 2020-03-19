# 逻辑值检测

一个对象在默认情况下均被视为真值，除非当该对象被调用时其所属类定义了 __bool__() 方法且返回 False 或是定义了 __len__() 方法且返回零。  
下面基本完整地列出了会被视为假值的内置对象:

**被定义为假值的常量**: None 和 False。  
**任何数值类型的零**: 0, 0.0, 0j, Decimal(0), Fraction(0, 1)  
**空的序列和多项集**: '', (), [], {}, set(), range(0)

产生布尔值结果的运算和内置函数总是返回 0 或 False 作为假值，1 或 True 作为真值，除非另行说明。 （重要例外：布尔运算 or 和 and 总是返回其中一个操作数。）

# 布尔运算 --- and, or, not

这些属于布尔运算，按优先级升序排列:

|   运算 |                 结果                 | 注释 |
| ------ | ----------------------------------- | --- |
|x or y  | if x is false, then y, else x       | (1) |
|x and y | if x is false, then x, else y       | (2) |
|not x   | if x is false, then True, else False| (3) | 

注释:  
1. 这是个短路运算符，因此只有在第一个参数为假值时才会对第二个参数求值。  
2. 这是个短路运算符，因此只有在第一个参数为真值时才会对第二个参数求值。  
3. not 的优先级比非布尔运算符低，因此 not a == b 会被解读为 not (a == b) 而 a == not b 会引发语法错误。

# 比较
在 Python 中有八种比较运算符。 它们的优先级相同（比布尔运算的优先级高）。 比较运算可以任意串连；例如，x < y <= z 等价于 x < y and y <= z，前者的不同之处在于 y 只被求值一次（但在两种情况下当 x < y 结果为假值时 z 都不会被求值）。

此表格汇总了比较运算:

| 运算 | 含义 |
| -- | -- |
|< |严格小于|
|<= |小于或等于|
|> |严格大于|
|>= |大于或等于|
|== |等于|
|!= |不等于|
|is| 对象标识|
|is not |否定的对象标识|

除不同的数字类型外，不同类型的对象不能进行相等比较。== 运算符总有定义，但对于某些对象类型（例如，类对象），它等于 is 。其他 <、<=、> 和 >= 运算符仅在有意义的地方定义。例如，当参与比较的参数之一为复数时，它们会抛出 TypeError 异常。

具有不同标识的类的实例比较结果通常为不相等，除非类定义了 __eq__() 方法。

一个类实例不能与相同类或的其他实例或其他类型的对象进行排序，除非该类定义了足够多的方法，包括 __lt__(), __le__(), __gt__() 以及 __ge__() (而如果你想实现常规意义上的比较操作，通常只要有 __lt__() 和 __eq__() 就可以了)。

is 和 is not 运算符无法自定义；并且它们可以被应用于任意两个对象而不会引发异常。

还有两种具有相同语法优先级的运算 in 和 not in，它们被 iterable 或实现了 __contains__() 方法的类型所支持。

# 数字类型 --- int, float, complex
存在三种不同的数字类型: 整数, 浮点数和复数。此外，布尔值属于整数的子类型。整数具有无限的精度。     
浮点数通常使用 C 中的 double 来实现；  
有关你的程序运行所在机器上浮点数的精度和内部表示法可在 sys.float_info 中查看。   
复数包含实部和虚部，分别以一个浮点数表示。   
要从一个复数 z 中提取这两个部分，可使用 z.real 和 z.imag。 （标准库包含附加的数字类型，如表示有理数的 fractions.Fraction 以及以用户定制精度表示浮点数的 decimal.Decimal。）

数字是由数字字面值或内置函数与运算符的结果来创建的。 不带修饰的整数字面值（包括十六进制、八进制和二进制数）会生成整数。 包含小数点或幂运算符的数字字面值会生成浮点数。 在数字字面值末尾加上 'j' 或 'J' 会生成虚数（实部为零的复数），你可以将其与整数或浮点数相加来得到具有实部和虚部的复数。

所有数字类型（复数除外）都支持下列运算:

|运算|结果|注释|
| -- | -- | -- | -- |
|x + y |x 和 y 的和
|x - y |x 和 y 的差
|x * y |x 和 y 的乘积
|x / y |x 和 y 的商，结果是浮点数|
|x // y |x 和 y 的商数，整除 |
|x % y |x 和 y 相除的余数 |不可用于复数
|-x |x 取反
|+x |x 不变
|abs(x) |x 的绝对值或大小 |
|int(x) |将 x 转换为整数 | 
|float(x) |将 x 转换为浮点数 | float 也接受字符串 "nan" 和附带可选前缀 "+" 或 "-" 的 "inf" 分别表示非数字 (NaN) 以及正或负无穷。
|complex(re, im) |一个带有实部 re 和虚部 im 的复数。im 默认为0。 
|c.conjugate() |复数 c 的共轭
|divmod(x, y) |(x // y, x % y)x和y相除后的值和余数 
|pow(x, y) |x 的 y 次幂 |pow(0, 0)和0 ** 0定义为1，这是编程语言的普遍做法
|x ** y |x 的 y 次幂 

eg:
```python
In [1]: 1 / 2                                                                                          
Out[1]: 0.5

In [2]: 2 / 2                                                                                          
Out[2]: 1.0

In [3]: 1//2                                                                                           
Out[3]: 0

In [4]: 2//2                                                                                           
Out[4]: 1

In [5]: int(2.0)                                                                                       
Out[5]: 2

In [6]: int("2")                                                                                       
Out[6]: 2

In [7]: int("2.0")                                                                                     
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-7-b8c5cc4be956> in <module>
----> 1 int("2.0")

ValueError: invalid literal for int() with base 10: '2.0'


```


所有 numbers.Real 类型 (int 和 float) 还包括下列运算:

|运算 |结果|
| -- | -- |
|math.trunc(x) |x 截断为 Integral(取整)|
|round(x[, n]) |x 舍入到 n 位小数，半数值会舍入到偶数。 如果省略 n，则默认为 0。|
|math.floor(x) |<= x 的最大 Integral|
|math.ceil(x) |>= x 的最小 Integral|

```ipython
In [1]: import math                                                                                    

In [2]: math.trunc(1.2)                                                                                
Out[2]: 1

In [3]: math.floor(1.2)                                                                                
Out[3]: 1

In [4]: math.trunc(-1.2)                                                                               
Out[4]: -1

In [5]: math.floor(-1.2)                                                                               
Out[5]: -2

In [6]: round(2.6)                                                                                     
Out[6]: 3

In [7]: round(2.6, 1)                                                                                  
Out[7]: 2.6

In [8]: round(2.55, 1)                                                                                 
Out[8]: 2.5

In [9]: math.ceil(1.2)                                                                                
Out[9]: 2

In [10]: math.ceil(-1.2)                                                                               
Out[10]: -1
```

# 整数类型的按位运算
按位运算只对整数有意义。计算按位运算的结果，就相当于使用无穷多个二进制符号位对二的补码执行操作。

二进制按位运算的优先级全都低于数字运算，但又高于比较运算；  
一元运算 ~ 具有与其他一元算术运算 (+ and -) 相同的优先级。

此表格是以优先级升序排序的按位运算列表:

| 运算 | 结果 | 注释 |
| -- | -- | -- |
|x \| y | x 和 y 按位 或 |(4) 
|x ^ y| x 和 y 按位 异或 | (4)
|x & y| x 和 y 按位 与| (4)
|x << n |x 左移 n 位 |负数不可移位，不溢出**乘以**pow(2, n)
|x >> n |x 右移 n 位| 负数不可移位，不溢出**除以**pow(2, n)
|~x| x 逐位取反