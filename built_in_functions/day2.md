# 内置函数

## bool(x)  

略

## breakpoint(*args, **kwargs)  

python3.7版本新增
相当于pdb.set_trace()
略

## class bytearray([source[, encoding[, errors]]])

bytearray() 方法返回一个新字节数组。这个数组里的元素是可变的，并且每个元素的值范围: 0 <= x < 256。

参数source为整数，那么返回一个长度为source的空字节数组。  
>示例

```python
In [1]: bytearray(5)
Out[1]: bytearray(b'\x00\x00\x00\x00\x00')

In [2]: list(bytearray(5))
Out[2]: [0, 0, 0, 0, 0]
```

如果source为字符串，encoding字段是必须的，按照指定的encoding将字符串转换为字节序列。
>示例

```python
In [1]: bytearray('gengleiming', 'utf-8')
Out[1]: bytearray(b'gengleiming')

In [2]: bytearray('耿雷明', 'utf-8')
Out[2]: bytearray(b'\xe8\x80\xbf\xe9\x9b\xb7\xe6\x98\x8e')
```

如果 source 为可迭代类型，则元素必须为[0 ,255] 中的整数；
>示例

```python
In [4]: bytearray([1,2,3])
Out[4]: bytearray(b'\x01\x02\x03')
```

如果没有输入任何参数，默认就是初始化数组为0个元素。
>示例

```python
In [5]: bytearray()
Out[5]: bytearray(b'')
```

如果 source 为与 buffer 接口一致的对象，则此对象也可以被用于初始化 bytearray。
>示例
略
