[TOC]

# Python (Learn X in Y Minutes)

## 笔记

### 注释

| 类型 | 符号 |
| --- | :---: |
| 单行注释 | # |
| 多行注释 | """ |

### 运算

| 运算 | 符号 | 备注 |
| --- | :---: | --- |
| 地板除 | // | integer division |
| 幂运算 | ** | exponentiation |
| 优先运算 | () | enforce precedence with parentheses |
| 布尔值 | True False | True为1(**不是非0**) False为0 |
| 与或非 | and or not | `0 and 2` 为0 `0 or -1` 为-1 |
| 布尔函数 | bool(ints) | `bool(0)` 为False `bool(-1)` 为True |
| 指针与值 | is vs. == | is为指针 ==为值 |
| 空 | None | None是一个对象，用is不用==判断 |
    
### 字符串

| String | | |
| --- | --- | --- |
| 字符串拼接 | `"Hello " + "world!"` | `"Hello world!"` |
| 字符串取某个字符 | `"This is a string"[0]` | `T` |
| 字符串格式化 | `"{} can be {}".format("Strings", "interpolated")`  | `"Strings can be interpolated"` |
| | `"{0} be nimble, {0} be quick, {0} jump over the {1}".format("Jack", "candle stick")` | `"Jack be nimble, Jack be quick, Jack jump over the candle stick"` |
| | `"{name} wants to eat {food}".format(name="Bob", food="lasagna")` | `"Bob wants to eat lasagna"` |
| 2.5 below | `"%s can be %s the %s way" % ("Strings", "interpolated", "old")` | `"Strings can be interpolated the old way"` |
| 3.6 above | `name = "Reiko" f"She said her name is {name}."` | `"She said her name is Reiko"` |
| | `name = "Reiko" f"{name} is {len(name)} characters long."` | `"Reiko is 5 characters long."` |

### 常用函数

| 函数 | | |
| --- | --- | --- |
| 打印 `print()`| `print("Hello, World", end="!")` | 默认有回车，添加end参数可自定义 |
| 输入 `input()` | `input_string_var = input("Enter some data: ")` | 低版本为`raw_input()` |
| 类型 | `type()` | |

### 条件

`"yahoo!" if 3 > 2 else 2`

### List

| List | | |
| --- | --- | --- |
| 末尾添加元素 | `li.append()` | |
| 指定序号添加元素 | `li.insert(1, 2)` | 在序号1的位置添加元素2 |
| 删除末尾元素 | `li.pop()` | |
| 删除指定序号元素 | `del li[2]` | |
| 删除第一个指定元素 | `li.remove(2)` | |
| 取元素`li[start:end:step]` | `li[0]` `li[-1]`| 序号0的元素 末尾元素 |
| | `li[1:3]` | 前闭后开 |
| | `li[2:]` | 从序号2的元素取到末尾 |
| | `li[:3]` | 从开始取到序号2的元素 |
| | `li[::2]` | 每两个元素取一个 |
| | `li[::-1]` | 倒序 |
| 复制list元素 | li2 = li[:] | 不是同一个对象 |
| 第一个指定元素的序号 | `li.index(2)` | 第一个2的序号 |
| List拼接 | `l1+l2` | l1与l2未变 |
| | `l1.extend(l2)` | l1改变 |
| 判断元素存在 | `1 in li` | |
| List元素个数 | `len(li)` | |

### Tuple 不可变List

| Tuple | | |
| --- | --- | --- |
| 类型 | `type((1)) type((1,)) type(())` | `int tuple tuple` |
| 赋值 | `a, b, c = (1, 2, 3)` | a=1 b=2 c=3 |
| | `a, *b, c = (1, 2, 3, 4)` | a=1 b=[2, 3] c=4 |
| 交换 | `d, e, f = 4, 5, 6` `e, d = d, e` | d=5 e=4 |

### Dictionary

key不可变，可以是整数、浮点数、字符串、元组

| Dict | | |
| --- | --- | --- |
| 取keys作为List | `list(di.keys())` | |
| 取values作为List | `list(di.values())` | |
| 取指定key的value | `di.get("a", 1)` | 若不存在时返回1 |
| 设置指定key的value | `di.setdefault("a", 5)` | 若已存在则不赋值 |
| 赋值 | `di["b"] = 2` | |
| | `di.update({"b" : 2})` | |
| 删除 | `del di["a"]` | |
| 新增 | `{'a':1, **{'b':2}}` | |
| 修改 | `{'a':1, **{'a':2}}` | |

### Set

元素需为不可变类型，即整数、浮点数、字符串、元组，不可为List、Dict

| Set | | |
| --- | --- | --- |
| 声明 | `empty_set = set()` | |
| 赋值 | `some_set = {1, 1, 2, 2, 3, 4}` | `{1, 2, 3, 4}` |
| & | `other_set = {3, 4, 5, 6} filled_set & other_set` | `{3, 4, 5}` |
| \| | `filled_set | other_set` | `{1, 2, 3, 4, 5, 6}` |
| - | `{1, 2, 3, 4} - {2, 3, 5}` | `{1, 4}` |
| ^ | `{1, 2, 3, 4} ^ {2, 3, 5}` | `{1, 4, 5}` |
| > | `{1, 2} >= {1, 2, 3}` | `False` |
| < | `{1, 2} <= {1, 2, 3}` | `True` |

### 异常处理

```
try:
    # Use "raise" to raise an error
    raise IndexError("This is an index error")
except IndexError as e:
    pass                 # Pass is just a no-op. Usually you would do recovery here.
except (TypeError, NameError):
    pass                 # Multiple exceptions can be handled together, if required.
else:                    # Optional clause to the try/except block. Must follow all except blocks
    print("All good!")   # Runs only if the code in try raises no exceptions
finally:                 #  Execute under all circumstances
    print("We can clean up resources here")
```

### 读取文件

```
with open("py3.py") as f:
	for line in f:
	   print(line)
```

### 迭代器

```
filled_dict = {"one": 1, "two": 2, "three": 3}
our_iterable = filled_dict.keys()
print(our_iterable)  # => dict_keys(['one', 'two', 'three']). This is an object that implements our Iterable interface.

# We can loop over it.
for i in our_iterable:
    print(i)  # Prints one, two, three

# However we cannot address elements by index.
our_iterable[1]  # Raises a TypeError

# An iterable is an object that knows how to create an iterator.
our_iterator = iter(our_iterable)

# Our iterator is an object that can remember the state as we traverse through it.
# We get the next object with "next()".
next(our_iterator)  # => "one"

# It maintains state as we iterate.
next(our_iterator)  # => "two"
next(our_iterator)  # => "three"

# After the iterator has returned all of its data, it raises a StopIteration exception
next(our_iterator)  # Raises StopIteration
```

### 函数

```
# Use "def" to create new functions
def add(x, y):
    print("x is {} and y is {}".format(x, y))
    return x + y  # Return values with a return statement

# Calling functions with parameters
add(5, 6)  # => prints out "x is 5 and y is 6" and returns 11

# Another way to call functions is with keyword arguments
add(y=6, x=5)  # Keyword arguments can arrive in any order.

# You can define functions that take a variable number of
# positional arguments
def varargs(*args):
    return args

varargs(1, 2, 3)  # => (1, 2, 3)

# You can define functions that take a variable number of
# keyword arguments, as well
def keyword_args(**kwargs):
    return kwargs

# Let's call it to see what happens
keyword_args(big="foot", loch="ness")  # => {"big": "foot", "loch": "ness"}

# You can do both at once, if you like
def all_the_args(*args, **kwargs):
    print(args)
    print(kwargs)
"""
all_the_args(1, 2, a=3, b=4) prints:
    (1, 2)
    {"a": 3, "b": 4}
"""

# When calling functions, you can do the opposite of args/kwargs!
# Use * to expand tuples and use ** to expand kwargs.
args = (1, 2, 3, 4)
kwargs = {"a": 3, "b": 4}
all_the_args(*args)            # equivalent to all_the_args(1, 2, 3, 4)
all_the_args(**kwargs)         # equivalent to all_the_args(a=3, b=4)
all_the_args(*args, **kwargs)  # equivalent to all_the_args(1, 2, 3, 4, a=3, b=4)

# Returning multiple values (with tuple assignments)
def swap(x, y):
    return y, x  # Return multiple values as a tuple without the parenthesis.
                 # (Note: parenthesis have been excluded but can be included)

x = 1
y = 2
x, y = swap(x, y)     # => x = 2, y = 1
# (x, y) = swap(x,y)  # Again parenthesis have been excluded but can be included.

# Function Scope
x = 5

def set_x(num):
    # Local var x not the same as global variable x
    x = num    # => 43
    print(x)   # => 43

def set_global_x(num):
    global x
    print(x)   # => 5
    x = num    # global var x is now set to 6
    print(x)   # => 6

set_x(43)
set_global_x(6)

# Python has first class functions
def create_adder(x):
    def adder(y):
        return x + y
    return adder

add_10 = create_adder(10)
add_10(3)   # => 13

# There are also anonymous functions
(lambda x: x > 2)(3)                  # => True
(lambda x, y: x ** 2 + y ** 2)(2, 1)  # => 5

# There are built-in higher order functions
list(map(add_10, [1, 2, 3]))          # => [11, 12, 13]
list(map(max, [1, 2, 3], [4, 2, 1]))  # => [4, 2, 3]

list(filter(lambda x: x > 5, [3, 4, 5, 6, 7]))  # => [6, 7]

# We can use list comprehensions for nice maps and filters
# List comprehension stores the output as a list which can itself be a nested list
[add_10(i) for i in [1, 2, 3]]         # => [11, 12, 13]
[x for x in [3, 4, 5, 6, 7] if x > 5]  # => [6, 7]

# You can construct set and dict comprehensions as well.
{x for x in 'abcddeef' if x not in 'abc'}  # => {'d', 'e', 'f'}
{x: x**2 for x in range(5)}  # => {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

## Learn X in Y Minutes 练习

```
#!/usr/bin/python

print(-5.0 // 3.0) # => -2.0

print(2**3)        # => 8

print(True + True) # => 2

print(True * 8)    # => 8

print(False - 5)   # => -5

print(bool(4))     # => True

print(bool(-6))    # => True

print(0 and 2)     # => 0

print(-5 or 0)     # => -5

print("This is a string.")

print('This is also a string.')

print("Hello " + "world!")

print("Hello " "world!")

print("This is a string"[0])

print(len("This is a string"))

print("{} can be {}".format("Strings", "interpolated"))

print("{0} be nimble, {0} be quick, {0} jump over the {1}".format("Jack", "candle stick"))

print("{name} wants to eat {food}".format(name="Bob", food="lasagna"))

print("%s can be %s the %s way" % ("Strings", "interpolated", "old"))

name = "Reiko"

print(f"She said her name is {name}.")

print(f"{name} is {len(name)} characters long.")

print("etc" is None)  # => False
print(None is None)   # => True

print(bool(0))   # => False
print(bool(""))  # => False
print(bool([]))  # => False
print(bool({}))  # => False
print(bool(()))  # => False

print("Hello, World", end="!")

#input_string_var = input("Enter some data: ")

#print(input_string_var)

print("yahoo!" if 3 > 2 else 2)

l1 = [1, 2, 3]
l2 = [4, 5, 6]
l1.extend(l2)
print(l1)

print(type((1)))   # => <class 'int'>
print(type((1,)))  # => <class 'tuple'>
print(type(()))    # => <class 'tuple'>

a, b, c = (1, 2, 3)

print(a, b, c)

b, c = c, b

print(a, b, c)

a, *b, c = (1, 2, 3, 4, 5)

print(a, b, c)

a = (1, 2, (3,), [4, 5], "a", {"b":2})

print(a)

print(type(a))

di = {"a":1, "b":2, "c":3}
print(di.keys())
print(list(di.keys()))
print("a" in di)
print(di.get("d", 4))
print(di)
di.setdefault("a", 5)
di.setdefault("d", (4,))
print(di)
del di["d"]
print(di)
print({'a':1, **{'b':2}})
print({'a':1, **{'a':2}})

s = set()
print(s)
s = {1, 2, (3,)}
print(s)

ss = s
print(ss)
ss.add(4)
print(s)

#with open("py3.py") as f:
	#for line in f:
		#print(line)

filled_dict = {"one": 1, "two": 2, "three": 3}
our_iterable = filled_dict.keys()
print(our_iterable)  # => dict_keys(['one', 'two', 'three']). This is an object that implements our Iterable interface.

# We can loop over it.
for i in our_iterable:
	print(i)  # Prints one, two, three

# However we cannot address elements by index.
# our_iterable[1]  # Raises a TypeError

# An iterable is an object that knows how to create an iterator.
our_iterator = iter(our_iterable)

# Our iterator is an object that can remember the state as we traverse through it.
# We get the next object with "next()".
print(next(our_iterator))  # => "one"

# It maintains state as we iterate.
print(next(our_iterator))  # => "two"
print(next(our_iterator))  # => "three"

def add(x, y):
	print("x is {} and y is {}".format(x, y))
	return x + y
	
add(y=6, x=5)

def varargs(*args):
	return args

print(varargs(1, 2, 3))

def keyword_args(**kwargs):
	return kwargs

# Let's call it to see what happens
print(keyword_args(big="foot", loch="ness"))

# You can do both at once, if you like
def all_the_args(*args, **kwargs):
	print(args)
	print(kwargs)

all_the_args(1, 2, a=3, b=4)

args = (1, 2, 3, 4)
kwargs = {"a": 3, "b": 4}
all_the_args(*args)            # equivalent to all_the_args(1, 2, 3, 4)
all_the_args(**kwargs)         # equivalent to all_the_args(a=3, b=4)
all_the_args(*args, **kwargs)  # equivalent to all_the_args(1, 2, 3, 4, a=3, b=4)

# Python has first class functions
def create_adder(x):
	def adder(y):
		return x + y
	return adder

add_10 = create_adder(10)
print(add_10(3))   # => 13

# There are also anonymous functions
print((lambda x: x > 2)(3))                  # => True
print((lambda x, y: x ** 2 + y ** 2)(2, 1))  # => 5

# There are built-in higher order functions
print(list(map(add_10, [1, 2, 3])))          # => [11, 12, 13]
print(list(map(max, [1, 2, 3], [4, 2, 1])))  # => [4, 2, 3]

print(list(filter(lambda x: x > 5, [3, 4, 5, 6, 7])))  # => [6, 7]

# We can use list comprehensions for nice maps and filters
# List comprehension stores the output as a list which can itself be a nested list
print([add_10(i) for i in [1, 2, 3]])         # => [11, 12, 13]
print([x for x in [3, 4, 5, 6, 7] if x > 5])  # => [6, 7]

# You can construct set and dict comprehensions as well.
print({x for x in 'abcddeef' if x not in 'abc'})  # => {'d', 'e', 'f'}
print({x: x**2 for x in range(5)})  # => {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

