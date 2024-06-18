

## Python内置方法

### 1.range()

`range()` 是 Python 中的一个内置函数，用于创建一个整数序列。它常用于 `for` 循环中，可以生成一系列连续的整数。

`range()` 函数可以接受一个、两个或三个参数：

- 如果只提供一个参数，`range(stop)` 会生成从 0 开始到 `stop-1` 结束的整数序列。
- 如果提供两个参数，`range(start, stop)` 会生成从 `start` 开始到 `stop-1` 结束的整数序列。
- 如果提供三个参数，`range(start, stop, step)` 会生成从 `start` 开始到 `stop-1` 结束的整数序列，步长为 `step`。

例如：

```
# 生成一个整数序列：0, 1, 2, 3, 4
for num in range(5):
    print(num)

# 生成一个整数序列：2, 4, 6, 8
for num in range(2, 10, 2):
    print(num)
```

在这个例子中，第一个 `for` 循环使用了一个参数，生成了从 0 到 4 的整数序列。第二个 `for` 循环使用了三个参数，生成了从 2 开始到 9 结束、步长为 2 的整数序列。

需要注意的是，`range()` 函数生成的是一个序列，如果你想要查看这个序列的具体内容，需要将它转换为列表：

```
pythonCopy code
sequence = list(range(5))  # 生成一个列表：[0, 1, 2, 3, 4]
```

这样就可以得到一个包含 `range()` 函数生成的整数序列的列表。

### 2.strip()

`strip()` 是 Python 字符串对象的一个方法，用于去除字符串两端（开头和结尾）的空白字符（包括空格、制表符和换行符）。这个方法返回去除空白字符后的新字符串，不会修改原始字符串。

具体来说，`strip()` 方法会去除字符串两端的空格（空格字符）、制表符（`\t`）和换行符（`\n`）。

例如：

```
pythonCopy codetext = "  hello, world!  \t\n"
stripped_text = text.strip()
print(stripped_text)  # 输出："hello, world!"
```

在这个例子中，`strip()` 方法去除了字符串 `text` 两端的空格、制表符和换行符，得到了新的字符串 `"hello, world!"`。

`strip()` 方法的变体还有 `lstrip()` 和 `rstrip()`：

- `lstrip()` 方法去除字符串开头（左侧）的空白字符。
- `rstrip()` 方法去除字符串结尾（右侧）的空白字符。

```
pythonCopy codetext = "  hello, world!  \t\n"
left_stripped_text = text.lstrip()
right_stripped_text = text.rstrip()
print(left_stripped_text)  # 输出："hello, world!  \t\n"
print(right_stripped_text)  # 输出："  hello, world!"
```

在这个例子中，`lstrip()` 方法去除了字符串开头的空格、制表符和换行符，而 `rstrip()` 方法去除了字符串结尾的空格和制表符。

### 3.input()

**input()** 是 Python 内置函数，它用于从用户输入中获取数据。当程序执行到 `input()` 时，程序会暂停执行，等待用户输入，直到用户按下回车键为止。然后，`input()` 函数会将用户输入的内容作为字符串（string）返回。

例如，以下代码会提示用户输入名字，然后将用户输入的名字存储在变量 `name` 中：

```
name = input("请输入你的名字: ")
print("你好, " + name + "!")
```

在这个例子中，`input("请输入你的名字: ")` 会显示提示信息 `"请输入你的名字: "`，等待用户输入。用户输入的内容被存储在变量 `name` 中，然后被用来构建输出的字符串。

需要注意的是，`input()` 函数总是返回字符串类型。如果你需要处理其他类型的输入（比如整数或浮点数），你需要使用 `int()` 或 `float()` 函数将输入的字符串转换为相应的类型。例如：

```
age = int(input("请输入你的年龄: "))  # 将用户输入的字符串转换为整数
print("你的年龄是: " + str(age))  # 将整数转换为字符串后输出
```

在这个例子中，`input()` 函数首先获取用户输入的字符串，然后 `int()` 函数将其转换为整数，最后用 `str()` 函数将整数转换为字符串以便输出。

`input()` 函数在编写需要用户交互的程序时非常有用，例如用户输入密码、选择菜单项等等。

### 4.enumerate()

在Python中，`enumerate()` 是一个内置函数，它用于将一个可迭代对象（例如列表、元组、字符串等）转换为一个枚举对象，这个枚举对象包含了原可迭代对象中的元素以及对应的索引。`enumerate()` 函数的基本语法如下：

```
enumerate(iterable, start=0)
```

- `iterable`：需要枚举的可迭代对象。
- `start`：枚举的起始值，默认为0。

`enumerate()` 函数返回一个枚举对象，其中每个元素是一个包含两个值的元组，第一个值是索引，第二个值是原可迭代对象中的元素。

下面是一个示例，演示了如何使用 `enumerate()` 函数：

```
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(f"Index {index} : {fruit}")
```

在这个例子中，`enumerate()` 函数将 `fruits` 列表转换为一个枚举对象。在 `for` 循环中，`index` 是索引，`fruit` 是列表中的元素。输出将会是：

```
Index 0: apple
Index 1: banana
Index 2: cherry
```

你也可以指定 `enumerate()` 函数的第二个参数 `start`，用于设置枚举的起始值。例如：

```
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits, start=1):
    print(f"Index {index} : {fruit}")
```

这将输出：

```
index 1: apple
Index 2: banana
Index 3: cherry
```

在这个例子中，枚举的起始值被设置为1。

### 5.get()

`get()`是一个字典（dictionary）对象的方法。在Python中，字典是一种可变的无序集合，用于存储键-值对。字典中的`get()`方法用于获取指定键的值。

这是`get()`方法的基本语法：

```
dictionary.get(key, default_value)
```

- `key`: 指定要查找的键。
- `default_value`: 如果键存在于字典中，则返回键对应的值；如果键不存在，则返回`default_value`（默认为`None`）。





## 练习

1.可以被3除了输出“Fizz” 被5整除的输出"Buzz" 被3和5全部整除输出"FizzBuzz" 其他输入本身

```
def fizz_buzz(input):

  if input%3==0 and input%5==0:

     return "FizzBuzz"

  if input%3 == 0 :

     return "Fizz"

  elif input%5 ==0 :

     return "Buzz"

  else:

     return input

print(fizz_buzz(7))


```





## Python特性

### 1.可变类型和不可变类型

在Python中，数据类型可以分为可变（Mutable）类型和不可变（Immutable）类型。

不可变类型（Immutable Types）：

不可变类型的对象在创建之后无法被修改。每当你尝试修改不可变对象时，Python 会创建一个新的对象。以下是Python中的不可变类型：

1. **整数（int）**
2. **浮点数（float）**
3. **字符串（str）**
4. **元组（tuple）**
5. **冻结集合（frozenset）**

例如，当你对字符串进行拼接时，实际上会创建一个新的字符串对象：

```python
s = "Hello"
s += " World"  # 创建一个新的字符串对象 "Hello World"，而不是修改原始字符串对象
```

可变类型（Mutable Types）：

可变类型的对象在创建之后可以被修改。当你对可变对象进行操作时，它的内容可以被改变，而不会创建新的对象。以下是Python中的可变类型：

1. **列表（list）**
2. **集合（set）**
3. **字典（dictionary）**

例如，当你向列表中添加或删除元素时，列表对象的内容会被修改，而不会创建新的列表对象：

```python
my_list = [1, 2, 3]
my_list.append(4)  # 修改现有的列表对象，在列表末尾添加元素 4
```

这种区分可变和不可变类型在Python中非常重要。了解一个对象的类型是否可变决定了你在代码中如何处理它，以及你是否需要考虑对象的副本（copy）和引用（reference）的问题。

### 2.缩进

在Python中，缩进是一种代码块的表示方式。与许多其他编程语言使用大括号 `{}` 或者关键词 `begin` 和 `end` 来表示代码块不同，Python使用缩进来定义代码的层次结构。

具体来说，缩进用于：

1. **表示代码块：** 缩进将一组语句组织成一个代码块。在条件语句、循环、函数、类等控制结构中，缩进用来表示这些语句属于同一个代码块。

   ```
   pythonCopy codeif condition:
       print("This is inside the if block")
   print("This is outside the if block")
   ```

   在这个例子中，`print("This is inside the if block")` 是缩进的，表示它属于 `if` 语句的代码块。

2. **提高可读性：** 缩进使得代码更易读、易理解。通过缩进，你可以清晰地看到代码的逻辑结构，哪些语句属于哪个代码块。

   ```
   pythonCopy codefor i in range(5):
       print(i)
       if i % 2 == 0:
           print("Even")
       else:
           print("Odd")
   ```

   在这个例子中，`for` 循环内的语句以及 `if-else` 语句内的语句都有不同级别的缩进，清晰地表示了它们之间的嵌套关系。

3. **避免使用大括号：** Python中不使用大括号 `{}` 来表示代码块的开始和结束。缩进代替了大括号，使得代码更简洁、更符合直觉。

   ```
   pythonCopy codedef greet(name):
       print("Hello, " + name)
       print("Welcome to Python!")
   ```

   在这个例子中，`def` 关键词定义了一个函数，函数体内的语句使用缩进来表示属于函数体的范围。

请注意，缩进的数量必须保持一致，通常使用空格或制表符（tab）来表示缩进。Python 的官方建议是使用四个空格作为每一级别的缩进。不一致的缩进会导致 `IndentationError`，因此保持正确的缩进非常重要。

### 3.迭代器

迭代器（Iterator）是一个对象，它能够在遍历一个可迭代对象（例如列表、元组、字典、字符串等）时，记录遍历的位置，并且能够提供一个方法来逐个访问该可迭代对象的元素，而不需要知道该对象的内部结构。

# Python基础内容

## 一.字符串

### 1.转义字符

\n  换行

```
`message = """`

`programmer`

`Python` 

`"""`

`print(message)`
```

多行字符串使用三个连续的引号（单引号或双引号）来定义，允许你在字符串中包含多行文本。

### 2.格式化字符串

```
first = "wang"

last = "xu"

print(f"{first} {last}")
```

在这个例子中，`f"{first} {last}"` 是一个 f-string，其中 `first` 和 `last` 会被替换为相应的变量值。`f-string` 提供了一种方便的方式来格式化字符串，使得字符串中的变量值更容易插入。

### 3.没有x++自增

在python中没有x++

只能用  x += 1   来自增

### 4.input方法

```
x =input("x : ")

print(str(x))

print(bool(x))

print(float(x))
```

无论用户输入什么内容，`input()` 函数始终返回一个字符串。因此，你需要先将用户输入的字符串转换为其他类型，然后再进行输出。在大部分编程场景下，用户输入的数据通常以字符串的形式传递给程序。然而，有时候我们需要对用户输入的数据进行数学计算、逻辑操作或其他操作，这就需要将字符串转换为其他数据类型。

## 二.条件语句和循环

### 1.条件语句if

#### **(1)if elif else**

```
age = 22 

if age>=18:

  print("Adult")

elif age>=16:

  print("tennager")

else:

  print("child")

print("ALL done!")
```

#### **(2). 特殊写法 18<=age <56**

```
name = " "

if not name.strip(): 

  print("Name is empty")

age = 22

if 18<=age<56:

  print("Eligible") 

\#这里的strip()为用于去除字符串两端（开头和结尾）的空白字符（包括空格、制表符和换行符）。

\#这个方法返回去除空白字符后的新字符串，不会修改原始字符串。
```

#### **(3).三元运算符**

```
message = "eliggible" if age >= 18 else "Not eligible"   
```

#### **(4).if not 语句**

```
if not expression:
    # 如果expression为False，执行这里的代码 
else:    
    # 如果expression为True，执行这里的代码
```

举个例子，假设我们有一个布尔变量`is_sunny`，表示天气是否晴朗，我们想要检查如果天气不是晴朗，就带上雨伞。我们可以使用`if not`语句：

```
pythonCopy codeis_sunny = False

if not is_sunny:
    print("带上雨伞")
else:
    print("不需要雨伞")
```

在这个例子中，`if not is_sunny` 检查 `is_sunny` 是否为 `False`。由于 `is_sunny` 的值是 `False`，所以执行 `if` 语句下面的代码块，输出 "带上雨伞"。



### 2.循环

#### **(1)遍历**

```

for x in "Python":

  print(x) 出现p y t h o n

for x in ["a","b","c"]:

  print(x)

for x in range(0,10,2):

  print(x) 
```

#### **(2).for...else**

```
names = ["Jhon","Mary"]
for name in names:
  if name.startswith("J"):

     print("Found")
     break

else:

  print("Not found")
```

#### **(3).while循环**

```
guess = 0
answer = 5

while answer != guess:
  guess = int(input("Guess: "))
else:
  pass
```

### 3.函数

#### (1).基本写法

```
def increment(number:int , by:int =1) -> tuple:

  return (number,number+by)

print(increment(2))
```

这里的 -> tuple 表示返回一个元组类型数据

increment()是一个函数，它返回了一个元组。在Python中，函数可以返回元组或其他数据类型。当一个函数返回多个值时，Python 实际上会将这些值封装到一个元组中，然后返回这个元组。

#### (2).接受多个参数 *args

```
def multiply (*list):

  total =1

  for number in list :

     total *= number

  return total

print(multiply(2,3,4,5))
```

**这里的(*list)表示在可以传递多个参数**

函数定义中，`*` 号（星号）在参数前面表示可变数量的位置参数，也称为可变位置参数或*args。它允许函数接受任意数量的位置参数。当你不确定用户会传递多少个参数给函数时，你可以使用这个特性。

在函数定义时，如果你在参数列表中加入了一个星号 `*`，它会告诉Python解释器这个函数可以接受任意数量的位置参数。这些参数会被收集到一个元组中，该元组可以在函数体内部使用。

#### (3).接受任意关键字参数的函数   **args

```
def save_user(**user):

  print(user)

save_user(id=1, name = "admin")


```

这些参数被收集到一个字典中，其中键是参数的名字，对应的值是参数的值。

## 三.列表

### 1.基本写法

```
letters = ["a","b","c"]

matrix = [[0,1],[2,3]]

zeros = [0] * 5

combined = zeros + letters

numbers = list (range(20))

chars = list("Hello World")

print(len(chars))
```

### 2.访问列表项

```
letters = ["a","b","c","d"]

letters[0] = "A"

print(letters[0:3])

print(letters[:])#获得列表副本

print(letters[::2])#列表切片 list[start:stop:step]

numbers = list(range(20))

print(letters[::-1]) #可以得到倒过来的列表
```

### 3.拆包列表

```
numbers = [1,2,3,4,5,6,7,8,9]

first, *other, last = numbers

print(first, last)

print(other)
```

### 4.遍历列表

```
letters = ["a","b","c"]

for index,letter in enumerate(letters):

  print(index,letter)
```

当你使用 `for letter in enumerate(letters)` 时，`letter` 变量接收到的是 `(索引, 元素)` 形式的元组。在你的 `print(letter[0])` 语句中，你输出了这个元组的第一个元素，也就是索引。

如果你想要获取元素本身而不是索引，你可以这样修改你的代码：

```
pythonCopy codeletters = ["a", "b", "c"]
for index, letter in enumerate(letters):
    print(letter)
```

这样，`letter` 变量将直接接收到列表中的元素，而不是元组，然后你可以直接打印出元素。如果你想同时获取索引和元素，可以使用 `index` 和 `letter` 两个变量，就像我在上面的代码中所示。

### 5.向列表添加/删除项

```
letters = ["a","b","c"]

#Add

letters.append("d")  #到最后面添加

letters.insert(0,"-") #指定索引位置添加

#Remove

letters.pop(0)    #如果里面不填删最后一个，填索引删索引位置的东西

letters.remove("b") #指定删除里面的东西

del letters[0:3]   #删除0到2的索引

letters.clear()   #全部删除
```

### 6.搜索列表项

```
letters = ["a","b","c"]

print(letters.count("d")) 

if "d" in letters:

  print(letters.index("d"))

#letters.index("d")  搜索在列表中d字符的索引位置

#letters.count("d")  搜索在列表中d字符出现的次数
```

### 7.列表排序

```
numbers = [3,51,2,6,8,1]

numbers.sort(reverse=True)

sorted(numbers) #它重新正序排列numbers 并且创建一个新列表不会改变源列表 

print(numbers)

#numbers.sort()       可以数字正序排序

#numbers.sort(reverse=True) 可以数字倒序排序
```

```
items = [

  ("Product1",10),

  ("Product2",12),

  ("Product3",4)

]

def sort_item(item):

  return item[1]

items.sort(key=sort_item)

print(items)
```

#### **匿名函数**

```
items = [

  ("Product1",10),

  ("Product2",12),

  ("Product3",4)

]

items.sort(key=lambda item:item[1]) #lambda 参数列表: 返回值表达式

print(items)
```

#### **key关键字**

在Python中，你可以使用 `sorted()` 函数或者列表的 `sort()` 方法来对一个列表进行排序。通常，排序是按照列表元素的默认顺序进行的。但有时候，你希望根据元素的某个特定属性来排序，而不是按照元素本身的顺序。

这时，你就可以使用 `key` 参数。`key` 参数是一个函数，它定义了排序时用哪个属性作为依据。举个例子，如果你有一个由元组组成的列表，每个元组包含姓名和年龄，你可以使用 `key` 参数来指定排序时按照年龄进行排序。

以下是一个例子：

```
pythonCopy codepeople = [("Alice", 30), ("Bob", 25), ("Charlie", 35)]

# 按照年龄进行排序，key 参数是一个函数，用于提取元组中的年龄
sorted_people = sorted(people, key=lambda person: person[1])

print(sorted_people)
# 输出: [('Bob', 25), ('Alice', 30), ('Charlie', 35)]
```

在这个例子中，`lambda person: person[1]` 是一个小函数，它告诉Python在排序时应该用每个元组的第二个元素（即年龄）作为排序的依据。这样，排序就会按照年龄从小到大的顺序排列列表中的人。

#### **映射函数**

```
items = [

  ("Product1",10),

  ("Product2",12),

  ("Product3",4)

]

prices = list(map( lambda item:item[1],items))

print(prices)
```

**注意:**

```
items = [

  ("Product1",10),

  ("Product2",12),

  ("Product3",4)

]

x = map( lambda item:item[1],items)

print(x)

for item in x:

  print(item) 
```

当你打印 `x` 的时候，实际上是打印了一个迭代器对象的内存地址。迭代器是一种特殊的可迭代对象，它是按需计算的，这意味着它不会立即计算所有的结果。这是为了在处理大量数据时节省内存。

如果你想要获取实际的列表，你需要将迭代器对象转换为列表。使用 `list()` 函数将迭代器对象转换为列表(如上面那代码)

#### 过滤函数

```
items = [

 ("Product1",10),

 ("Product2",12),

 ("Product3",4)

]

filtered  =  list(filter(lambda item: item[1]>=10 , items))

print(filtered)
```

#### 列表推导式

```
items = [

 ("Product1",10),

 ("Product2",12),

 ("Product3",4)

]

prices = list(map( lambda item:item[1],items))
prices = [item[1] for item in items ] #列表推导式


filtered =list(filter(lambda item: item[1]>=10 , items))
filtered =[item for item in items if item[1] >= 10] #列表推导式
```

#### Zip函数

`zip()` 函数是一个内置函数，它接受多个可迭代对象作为参数，并将这些可迭代对象中的对应元素打包成元组。具体来说，`zip()` 函数会返回一个新的可迭代对象，其中每个元素是原可迭代对象中对应位置的元素构成的元组。

这个函数的基本语法如下：

```
pythonCopy code
zip(iterable1, iterable2, ...)
```

- `iterable1`, `iterable2`, ... 是一个或多个可迭代对象，比如列表、元组、字符串等。

以下是一个示例，演示了如何使用 `zip()` 函数：

```
names = ["Alice", "Bob", "Charlie"]
ages = [30, 25, 35]

# 使用 zip() 函数将两个可迭代对象打包成元组
zipped_data = zip(names, ages)

# 将 zip 对象转换为列表并打印
print(list(zipped_data))
# 输出: [('Alice', 30), ('Bob', 25), ('Charlie', 35)]
```

在这个例子中，`zip(names, ages)` 将 `names` 列表和 `ages` 列表的对应元素打包成元组，形成了一个包含元组的可迭代对象。你可以通过 `list()` 函数将这个可迭代对象转换为列表，得到包含元组的列表。

需要注意的是，如果传入的可迭代对象的长度不一致，`zip()` 函数会以最短的可迭代对象为准，多余的元素会被忽略。如果你希望处理不等长的可迭代对象，并保留所有元素，你可以使用 `itertools.zip_longest()` 函数。

## 四.数组

在处理大数据时，可以用数组来处理可以提升效率

```
from array import array

numbers = array("i",[1,2,3]) # 这里的"i"表示指定整数类型

numbers[0] = 1.0 #会报错,数组只能储存一种数据类型数据
```

## 五.集合

集合是Python中的一种**无序**、可变的且**不含重复元素**的数据类型，它具有以下特点：

1. **无序性（Unordered）**：集合中的元素是无序的，你无法通过索引来访问集合中的元素。集合中的元素没有固定的顺序，每次遍历集合可能得到不同的顺序。
2. **唯一性（Uniqueness）**：集合中的元素是唯一的，不允许重复元素。如果试图将重复的元素添加到集合中，集合会自动去重，只保留一个。
3. **可变性（Mutable）**：集合是可变的，可以通过添加（`add()`方法）、删除（`remove()`方法）等操作来修改集合。
4. **不可哈希性（Unhashable）**：集合本身是不可哈希的，也就是说集合不能作为字典的键（字典中的键必须是可哈希的），但集合内的元素必须是可哈希的。
5. **数学集合运算**：集合支持各种数学集合运算，如并集（`|`或`union()`方法）、交集（`&`或`intersection()`方法）、差集（`-`或`difference()`方法）、对称差集（`^`或`symmetric_difference()`方法）等。

由于集合具有唯一性和无序性，它们在需要存储一组唯一元素的场景下非常有用。例如，你可以使用集合来去重一个列表中的元素，或者检查两个数据集之间的差异。

```
numbers = {1,1,2,3,4,3,5} 简化为 numbers = {1,2,3,4,5}
first = set(numbers)  #定义集合 first = {1,2,3,4,5}
second = {1,5,7}
second.add(5)
second.remove(5)
len(second)
print(first)

print(first | second) #并集 {1,2,3,4,5,7}
print(first & second) #交集 {1,5}
print(first - second) #差集 {2,3,4}
print(first ^ second) #对称差集 {2,3,4,7}

if 1 in first:
  print("yes")
```

1. `first = set(numbers)`：将列表`numbers`转换为集合`first`，自动去除重复元素，`first`包含了1、2、3、4、5这些元素。
2. `print(first | second)`：输出`first`和`second`的并集，即包含两个集合中所有不重复元素的集合。输出为 `{1, 2, 3, 4, 5, 7}`。
3. `print(first & second)`：输出`first`和`second`的交集，即两个集合中共有的元素。输出为 `{1, 5}`，因为1和5是两个集合中都有的元素。
4. `print(first - second)`：输出`first`相对于`second`的差集，即在`first`中但不在`second`中的元素。输出为 `{2, 3, 4}`。

   5.`first ^ second` 表示两个集合的对称差集，即包含在 `first` 或者 `second` 中，但不同时属于二者的元素。在你的例子中，`first`       和 `second` 的对称差集将包含除了交集 `{1, 5}` 之外的所有元素。

## 六.字典

```
point = {"x":1, "y":2}
point = dict(x=1,y=2)
point["x"] = 10  #修改一个键值对
point["y"] = 20  #添加一个键值对
if "a" in point:
  print(point["a"])
print(point.get("a", 0))  #查找a字符
del point["x"]  #删除元素
print(point)

#遍历字典
for key in point:
  print(key,point[key])

#会组成元组,里面保存了键和值 也可以进行拆包 把 x 变为 key value
for x in point.items():
  print(x)
```


在Python中，遍历字典时可以使用`items()`方法，该方法返回一个包含字典键值对的元组列表。在`for key, value in point.items():`这样的语句中，Python会自动将元组的第一个元素（键）赋值给`key`变量，将第二个元素（值）赋值给`value`变量。这种语法称为**序列解包**（sequence unpacking）。

这个特性依赖于Python的迭代器协议。当你迭代一个字典时，它会返回字典的键，因此在遍历`point.items()`时，每次迭代会返回一个包含键值对的元组。通过序列解包，你可以将这个元组拆分成两个独立的变量：`key`和`value`。

这种语法的便利性使得遍历字典变得非常简洁和易读。这也是Python中许多内置数据类型和函数的灵活性和易用性之一。

### 字典推导式

```
#集合推导式
values = {x*2 for x in range(5)}

#字典推导式
values = {}
for x in range(5):
  values[x] = x*2
#下面就是简写
values = {x : x*2 for x in range(5)}
print(values)
```

### 生成器

在Python中，生成器（Generator）是一种用于惰性计算（lazy evaluation）的迭代器，它允许你逐步生成值，而不是一次性生成并存储所有的值。这样可以节省内存空间，并且能够更高效地处理大数据集或者无限序列。

生成器的创建通常使用生成器表达式（Generator Expression）或者生成器函数（Generator Function）。

#### 生成器表达式（Generator Expression）：

生成器表达式是一种类似于列表推导式的语法结构，但是它生成的是一个生成器对象，而不是列表。生成器表达式使用圆括号 `()` 来定义，而不是方括号 `[]`。生成器表达式的语法和列表推导式非常相似，但它使用的是惰性计算，只在需要的时候生成值。

```
pythonCopy code
generator = (x * 2 for x in range(10))
```

在这个例子中，`generator` 是一个生成器对象，它可以生成从0到18的偶数。

#### 生成器函数（Generator Function）：

生成器函数是一种使用 `yield` 关键字的函数，它在函数体内使用 `yield` 语句产生一个值，暂停函数的执行，然后在下一次调用时从上次暂停的地方继续执行，直到函数结束或者遇到 `return` 语句。

```
pythonCopy codedef my_generator():
    for i in range(10):
        yield i * 2

generator = my_generator()
```

在这个例子中，`my_generator` 是一个生成器函数，`generator` 是一个生成器对象，它可以生成从0到18的偶数。

通过生成器，你可以逐步产生数据，而不需要一次性将所有数据存储在内存中，这对于处理大量数据或者需要无限生成数据的场景非常有用。

### 拆包操作符

```
#简单拆包
numbers = [1,2,3]
print(*numbers)
print(1,2,3)


values = list(range(5))
values = [*range(5),*"hello"]  # *拆分操作符可以拆分任何可迭代的对象
print(values)


#字典拆包
first = {"x":1}
second = {"y":2,"z":3}
combined = {**first , **second,"z":1}
print(combined)
```

### 练习题

```
#写一个程序，找到这个字符串里面出现最多的字符

sentence = "This is a common interview question"

char_frequency = {}
for char in sentence:
  if char in char_frequency:
     char_frequency[char] += 1
  else:
     char_frequency[char] =1
print(char_frequency)


char_frequency_sorted = sorted(
  char_frequency.items(),
  key=lambda kv: kv[1],
  reverse=True
)

print(char_frequency_sorted[0])
```

# 异常

### 1.处理异常

```
try:

  age = int(input("Age: "))

except ValueError as ex:

  print("你没有输入一个有效的年龄")

  print(ex) #解释哪个对象引起了异常

  print(type(ex))

else:

  print("没有任何异常")
```

### 2.处理不同的异常

```
try:

  age = int(input("Age: "))

  xfactor = 10 /age

except (ValueError,ZeroDivisionError) :

  print("你没有输入一个有效的年龄")

else:

  print("没有任何异常")
```

### 3.清除

```
try:
  file = open("app.py")
  age = int(input("Age: "))
  xfactor = 10 /age
  
except (ValueError,ZeroDivisionError) :
  print("你没有输入一个有效的年龄")
else:
  print("没有任何异常")

finally: #释放资源
  file.close()
```

### 4.with语句

```
try:

  with open("app.py") as file: #更简明的一种释放外部资源的一种写法，它用完会自动释放外部资源

     print("File opened.")

  age = int(input("Age: "))

  xfactor = 10 /age

except (ValueError,ZeroDivisionError) :

  print("你没有输入一个有效的年龄")

else:

  print("没有任何异常")
```

`with`语句是Python中一种用于管理资源的控制结构。它提供了一种简洁的方式来确保在代码块执行完毕后资源（如文件、网络连接等）被正确关闭，即便在发生异常的情况下也能正确关闭资源。`with`语句的基本语法是：

```
with expression as variable:
    # 代码块
```

在这里，`expression`通常是一个返回上下文管理器（context manager）的表达式，而`variable`是一个变量，用来存储这个上下文管理器的实例。

当进入`with`代码块时，Python会调用上下文管理器的`__enter__()`方法，它可以用来初始化资源或者执行一些必要的操作。当代码块执行完成后，无论是正常退出还是发生异常，Python都会调用上下文管理器的`__exit__()`方法，这个方法可以用来做一些清理工作，比如关闭文件、释放资源等。

使用`with`语句的主要优势是，它保证了在离开`with`代码块时资源会被正确释放，即便在代码块中发生了异常。这样能够提高代码的可读性和可维护性，避免了忘记关闭资源而导致的资源泄露问题。

以下是一个打开文件并读取内容的例子，使用了`with`语句：

```
# 使用with语句打开文件
with open("example.txt", "r") as file:
    content = file.read()
    # 在这里，文件已经被正确关闭，不需要手动调用file.close()

# 在这里，不需要再担心文件关闭的问题，文件已经在with代码块内被正确关闭
print(content)
```

在上面的例子中，`open("example.txt", "r")`返回一个文件对象，它是一个上下文管理器。使用`with`语句，我们确保了文件在代码块结束时会被正确关闭，不需要手动调用`file.close()`。



### 5.抛出异常(自定义异常)

```
def calculate_xfactor(age):
  if age <= 0:
     raise ValueError("Age cannot be 0 of less.")
  return 10/age


try:
  calculate_xfactor(-1)
except ValueError as error:
  print(error)
```

不要手工抛出异常(非常的耗资源)

# 类

类：是用来创建对象的蓝图  

对象：是类的实例

例子(类与对象的区别)：  类：人类     对象：张三，李四，王五





## 1.创建类

```
class Point:
  def draw(self):
     print("draw")
point = Point() #创建对象
point.draw()
```



**在类当中定义方法必须至少需要一个参数**

在Python中，在类中定义方法时，第一个参数必须是`self`。`self` 是一个指向类实例的引用，它表示方法是针对该类的特定实例进行操作。

当你调用一个类的方法时，解释器会自动将该方法的调用者（即类的实例）传递给`self`参数。通过`self`参数，方法可以访问该实例的属性和其他方法。这种方式允许类的方法操作对象的状态，并且使得在类的内部能够正确地引用对象的属性和其他方法。

例如，考虑一个简单的`Person`类：

```
pythonCopy codeclass Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def say_hello(self):
        print(f"Hello, my name is {self.name} and I am {self.age} years old.")
```

在上面的例子中，`__init__`方法是类的构造函数，它用来初始化对象的属性。`say_hello`方法是一个普通方法，它使用`self`参数来访问对象的属性`name`和`age`。当你创建一个`Person`类的实例并调用`say_hello`方法时，`self`参数会被自动传递，使得方法可以正确地引用实例的属性。

```
pythonCopy codeperson = Person("Alice", 30)
person.say_hello()  # 输出: Hello, my name is Alice and I am 30 years old.
```

因此，`self`参数的存在使得类的方法能够正确地操作类的实例，访问对象的属性和调用其他方法，确保了类的方法能够正确地与其对应的实例进行交互。

## 2.构造函数

```
class Point:
  def __init__(self,x,y):
     self.x= x
     self.y= y


  def draw(self):
     print("draw")
     print(f"Point (x:{self.x}, y:{self.y})")


point = Point(1,2) #创建对象
point.draw()
```

## 3.类字段与实例字段 

**(类属性和实例属性)**

在面向对象编程中，类字段（class fields）和实例字段（instance fields）是两种不同类型的属性，它们属于类和类的实例（对象）的属性，有着不同的作用和使用方式。

### 类字段（Class Fields）：

- **定义位置：** 类字段是定义在类级别的属性，它们不属于任何特定的实例，而是属于整个类。它们在类的定义中，方法之外声明。
- **作用范围：** 类字段是类的属性，对所有该类的实例共享。如果一个实例修改了类字段的值，该值会影响所有该类的实例。
- **访问方式：** 可以通过类名直接访问类字段，也可以通过类的实例访问。

例如：

```
class MyClass:
    class_field = "I am a class field"

# 访问类字段
print(MyClass.class_field)  # 输出: I am a class field

obj1 = MyClass()
obj2 = MyClass()

print(obj1.class_field)  # 输出: I am a class field
print(obj2.class_field)  # 输出: I am a class field

# 修改类字段的值
MyClass.class_field = "Updated class field"
print(obj1.class_field)  # 输出: Updated class field
print(obj2.class_field)  # 输出: Updated class field
```

### 实例字段（Instance Fields）：

- **定义位置：** 实例字段是定义在类的方法中，通常在类的构造方法（通常是`__init__`方法）中声明，用`self`关键字指定。
- **作用范围：** 实例字段属于类的实例（对象），每个对象都有一份独立的实例字段副本。修改一个对象的实例字段不会影响其他对象的实例字段。
- **访问方式：** 只能通过对象实例访问实例字段。

例如：

```
class MyClass:
    def __init__(self, instance_field):
        self.instance_field = instance_field

# 创建对象并访问实例字段
obj1 = MyClass("I am an instance field")
obj2 = MyClass("I am another instance field")

print(obj1.instance_field)  # 输出: I am an instance field
print(obj2.instance_field)  # 输出: I am another instance field

# 修改实例字段的值
obj1.instance_field = "Updated instance field"
print(obj1.instance_field)  # 输出: Updated instance field
print(obj2.instance_field)  # 输出: I am another instance field
```

总结来说，类字段是类的属性，对所有实例共享；而实例字段是每个实例（对象）独有的属性，每个对象都有自己的实例字段副本。

## 4.类方法和实例方法

在面向对象编程中，类方法（class methods）和实例方法（instance methods）是两种不同类型的方法，它们可以在类中定义，并用于操作类的属性和实例的属性。

### 类方法（Class Methods）：

- **定义方式：** 类方法使用`@classmethod`装饰器定义，第一个参数通常是`cls`，表示类本身。
- **作用范围：** 类方法属于类，而不是类的实例。类方法可以访问和修改类的属性，但不能直接访问实例的属性。
- **调用方式：** 可以通过类名或者类的实例调用类方法。

```
class MyClass:
    class_field = "I am a class field"
    
    @classmethod
    def class_method(cls):
        print(f"This is a class method of {cls}")
        
# 调用类方法
MyClass.class_method()  # 输出: This is a class method of <class '__main__.MyClass'>
obj = MyClass()
obj.class_method()  # 输出: This is a class method of <class '__main__.MyClass'>
```

### 实例方法（Instance Methods）：

- **定义方式：** 实例方法是最常见的方法类型，没有特殊的装饰器，第一个参数通常是`self`，表示对象实例。
- **作用范围：** 实例方法属于类的实例，可以访问和修改实例的属性，也可以访问类的属性。
- **调用方式：** 只能通过类的实例调用实例方法。

```
class MyClass:
    def __init__(self, instance_field):
        self.instance_field = instance_field
        
    def instance_method(self):
        print(f"This is an instance method of {self}")
        
# 创建对象并调用实例方法
obj = MyClass("I am an instance field")
obj.instance_method()  # 输出: This is an instance method of <__main__.MyClass object at 0x...>
```

**总结来说，类方法用于操作类级别的属性，可以通过类名或者类的实例调用；而实例方法用于操作实例级别的属性，只能通过类的实例调用。类方法的第一个参数是`cls`，实例方法的第一个参数是`self`，它们分别表示类和实例本身。**

## 5.魔法方法

魔法方法（Magic methods），也被称为特殊方法或双下划线方法（dunder methods），在Python中是具有特殊名称和功能的方法。它们以双下划线开头和结尾，例如`__init__`、`__str__`等。这些方法允许你定义对象在特定操作中的行为。当你使用内置函数（例如`print()`、`len()`、`+`等）或者进行特定操作（例如迭代、比较等）时，这些方法会被自动调用。

以下是一些常见的魔法方法及其功能：

- **`__init__(self, ...)`:** 构造函数，用于初始化对象的属性。
- **`__str__(self)`:** 返回对象的字符串表示，通常用于`print()`函数和`str()`函数。
- **`__repr__(self)`:** 返回对象的字符串表示，通常用于交互式环境中直接输入对象名。
- **`__len__(self)`:** 返回对象的长度，通常用于内置函数`len()`。
- **`__getitem__(self, key)`:** 获取对象的元素，用于支持索引操作。
- **`__setitem__(self, key, value)`:** 设置对象的元素，用于支持索引赋值操作。
- **`__delitem__(self, key)`:** 删除对象的元素，用于支持删除索引操作。
- **`__iter__(self)`:** 返回一个迭代器对象，用于支持对象的迭代。
- **`__next__(self)`:** 返回下一个迭代器值，用于支持迭代器的迭代。
- **`__eq__(self, other)`:** 定义对象相等的比较规则（==）。
- **`__lt__(self, other)`:** 定义对象小于的比较规则（<）。
- **`__gt__(self, other)`:** 定义对象大于的比较规则（>）。

这些魔法方法可以让你自定义对象的行为，使得你的类实例可以像内置类型一样被操作，提供了更好的灵活性和控制性。你可以根据需要实现这些魔法方法，以满足你的具体需求。

## 6.比较对象

```
class Point:
  def __init__(self,x,y):
     self.x= x
     self.y= y

  def __eq__(self,other):
     return self.x ==other.x and self.y ==other.y

  def __gt__(self,other):
     return self.x >other.x and self.y >other.y

  def __lt__(self,other):
     return self.x <other.x and self.y <other.y


point = Point(10,3) 
other = Point(1,2)
print(point>other)
```

如果你想要比较两个对象是否相等，你需要在对象的类中定义 `__eq__(self, other)` 方法。`__eq__` 方法是用于定义对象相等性的魔法方法，在进行对象之间的相等性比较时（使用 `==` 操作符），Python 会自动调用这个方法。

在 `__eq__` 方法中，你需要定义两个参数：`self` 表示当前对象，`other` 表示与之比较的对象。然后，你可以在该方法中根据你自己的逻辑来确定两个对象是否相等，并返回 `True` 或 `False`。

## 7.数学运算

```
class Point:
  def __init__(self,x,y):
     self.x= x
     self.y= y
  def __add__(self,other):
     return Point(self.x + other.x,self.y + other.y)


point = Point(10,3) 
other = Point(1,2)
combined = point + other
print(combined.y)
```

## 8.创建自定义容器

```python
class tagCloud:
  def __init__(self) :
     self.tags = {}
  def add (self,tag):
     self.tags[tag.lower()] = self.tags.get(tag.lower(), 0) + 1  #解决大小写问题
  def __getitem__(self, tag):
     return self.tags.get(tag.lower(),0)
  def __setitem__(self,tag,count):
    self.tags[tag.lower()] = count
  def __len__(self):
     return len(self.tags)
  def __iter__(self):
     return iter(self.tags)
 
 
cloud = tagCloud()
cloud["python"] = 10
cloud.add("Python")
cloud.add("python")
cloud.add("Python")
print(cloud.tags)
```

## 9.私有成员

**前缀双下划线，就会被认定为私有**

目的:为了防止意外访问对象属性

```
class tagCloud:
  def __init__(self) :
     self.__tags = {}
  def add (self,tag):
     self.__tags[tag.lower()] = self.__tags.get(tag.lower(), 0) + 1  #解决大小写问题
  def __getitem__(self, tag):
     return self.__tags.get(tag.lower(),0)
  def __setitem__(self,tag,count):
     self.__tags[tag.lower()] = count
  def __len__(self):
     return len(self.__tags)
  def __iter__(self):
     return iter(self.__tags)

cloud = tagCloud()
cloud["python"] = 10
cloud.add("Python")
cloud.add("python")
cloud.add("Python")
print(cloud.__dict__) #通过这个可以查看cloud对象的属性

print(cloud._tagCloud__tags)
```

## 10.属性

使用这些装饰器可以定义属性

```
class Product:
  def __init__(self,price):
     self.price = price
     
  @property #只读
  def price(self):
     return self.__price
     
  @price.setter   #在赋值的时候进行校准,确保属性的值符合你的规定
  def price(self,value):
     if value < 0 :
       raise ValueError("Price cannot be negative")
     self.__price =value
     
     
product = Product(-10)
print(product.price)
```

当你使用`@property`装饰器时，你可以将一个方法转换为一个只读的属性。在你的代码中，你定义了一个名为`price`的方法，并使用了`@property`装饰器，这样这个方法就可以被像一个属性一样访问，而不需要使用括号调用它。

```
pythonCopy code@property
def price(self):
    return self.__price
```

上述代码中的`price`方法是一个getter方法。这个方法返回了一个私有属性`__price`的值。由于使用了`@property`装饰器，你可以像访问属性一样使用`product.price`来获取`__price`的值，而不需要使用括号调用这个方法。

接下来，你使用了`@price.setter`装饰器，定义了一个名为`price`的setter方法：

```
pythonCopy code@price.setter
def price(self, value):
    if value < 0:
        raise ValueError("Price cannot be negative")
    self.__price = value
```

这个setter方法负责设置私有属性`__price`的值，并且在设置值之前进行了检查。如果传入的`value`小于0，那么会抛出一个`ValueError`异常，指示价格不能为负数。如果`value`合法，setter方法将`value`赋给`__price`属性。

使用这两个装饰器，你创建了一个可读写的属性`price`。你可以通过`product.price`读取属性的值，也可以通过`product.price = new_value`来设置属性的值。在设置属性的值时，会自动调用setter方法，确保属性的值符合你的规定。这种方式提供了一种更加优雅和安全的方式来操作类的属性。

## 11.继承

```
class animal:
  def __init__(self,age):
     self.age = age
  def eat(self):
     print("eat")

class Mammal(animal):
  def walk(self):
     print("walk")

class Fish(animal):
  def swim(self):
     print("swim")

m = Mammal(1)
m.eat()
print(m.age)
```

## 12.Object基类

在Python中，所有的类都直接或间接地继承自一个基类，即`object`类。`object`类是Python中所有类的基类（父类）。这意味着所有的类在Python中都是`object`类的子类。`object`类提供了Python中所有对象的基本功能，包括属性、方法、特殊方法（如`__init__`、`__str__`等），以及一些基本的魔法方法（magic methods）。

在Python 2中，`object`类并不是必须的，但在Python 3中，所有的类都隐式地继承自`object`类。如果你创建一个新类，即使你不显式地指定它的父类，它仍然会隐式地继承自`object`类。例如：

```
class MyClass:
    pass

# 在Python 3中，MyClass隐式地继承自object类
print(isinstance(MyClass, object))  # 输出: True
```

在Python 3中，你也可以显式地指定`object`类作为父类：

```
class MyClass(object):
    pass
```

`object`类为所有的Python对象提供了一些通用的方法，例如`__init__`用于初始化对象，`__str__`用于返回对象的字符串表示，等等。由于所有的类都继承自`object`类，因此它们都具有这些通用的方法。

使用`object`类作为所有类的基类，使得Python的类体系结构更加统一，并且确保了所有的类都共享了一些基本的行为和特性。

## 13.方法重写

**方法重写就是覆盖或者改写基类中的方法**

```
class Animal:
  def __init__(self):
     print("Animal constructor")
     self.age = 1
  def eat(self):
     print("eat")
     
     
class Mammal(Animal):
  def __init__(self):
     print("Mammal constructor")
     self.weigth = 2
     super().__init__() #你希望除了执行Mammal类的初始化操作外，
                        #还能执行Animal类的初始化操作。这时就可以使用super()来实现。
  def walk(self):
     print("walk")
     
     
class Fish(Animal):
  def swim(self):
     print("swim")
     
     
m = Mammal() 
print(m.weigth)
```

## 14.多级继承

**尽量建一两级继承关系就行，不要继承多了，容易遭罪**

## 15.多重继承

**进行多重继承时，不要有重复的方法名**

```
class Flyer:
  def fly(self):
     print("Employee greet")
     
class Swimmer:
  def swim(self):
     print("Person")
     
class Flyingfish(Flyer,Swimmer):
  pass
```

## 16.一个良好的继承关系例子

```
class InvalidOperationError(Exception):
    pass


class Stream:
    def __init__(self):
        self.opened = False

    def open(self):
        if self.opened:
            raise InvalidOperationError("Stream is alread open")
        self.opened = True
    def close(self):
        if self.opened:
            raise InvalidOperationError("Stream is alread close")
        self.opened = False

class FileStream(Stream):
    def read(self):
        print("FileStream date from a file ")
class NetworkStream(Stream):
    def read(self):
        print("NetworkStream date from a network ")

```

## 17.抽象基类

抽象类是一种在面向对象编程中常用的概念。在Python中，抽象类通过`abc`模块来定义。抽象类不能被实例化，只能被继承，并且子类必须实现抽象类中定义的抽象方法。抽象方法是在抽象类中声明但没有提供具体实现的方法。抽象类和抽象方法的存在主要是为了规范子类的行为，确保子类实现了特定的方法。

下面是一个简单的抽象类的例子：

```
pythonCopy codefrom abc import ABC, abstractmethod

class Shape(ABC):  # 定义抽象类
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):  # Circle类继承自抽象类Shape
    def __init__(self, radius):
        self.radius = radius

    def area(self):  # 实现抽象方法
        return 3.14 * self.radius * self.radius

class Square(Shape):  # Square类继承自抽象类Shape
    def __init__(self, side):
        self.side = side

    def area(self):  # 实现抽象方法
        return self.side * self.side

# 创建Circle对象
circle = Circle(5)
print("Circle Area:", circle.area())  # 输出: Circle Area: 78.5

# 创建Square对象
square = Square(4)
print("Square Area:", square.area())  # 输出: Square Area: 16
```

在这个例子中，`Shape` 是一个抽象类，它包含一个抽象方法 `area`。`Circle` 和 `Square` 类都继承自 `Shape` 抽象类，并实现了 `area` 方法。因此，它们可以被实例化，并且可以调用 `area` 方法计算各自的面积。

如果子类没有实现抽象类中定义的抽象方法，或者试图实例化一个抽象类，Python 将抛出 `TypeError` 异常。抽象类和抽象方法为程序提供了一种规范和约束，确保了继承关系中的一致性和可靠性。

## 18.多态

多态（Polymorphism）是面向对象编程中的一个重要概念，指的是在不同的对象类型上执行相同的操作，但可能会产生不同的行为。多态性允许你使用统一的接口来处理不同类的对象，使得代码更加灵活和可扩展。

在Python中，多态性是通过方法的重载和动态绑定实现的。方法的重载指的是在不同的类中可以定义相同名字的方法，但这些方法的具体实现可以不同。动态绑定是指在运行时确定调用的方法，而不是在编译时确定。下面是一个简单的多态性示例：

```
pythonCopy codeclass Animal:
    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        return "Woof!"

class Cat(Animal):
    def sound(self):
        return "Meow!"

# 多态性的应用
def make_sound(animal):
    return animal.sound()

# 创建不同的对象
dog = Dog()
cat = Cat()

# 调用相同的方法，但产生不同的行为
print(make_sound(dog))  # 输出: Woof!
print(make_sound(cat))  # 输出: Meow!
```

在这个例子中，`Animal` 是基类，它定义了一个抽象方法 `sound`。`Dog` 和 `Cat` 类是 `Animal` 的子类，它们分别实现了 `sound` 方法。函数 `make_sound` 接受一个 `Animal` 类型的参数，并调用其 `sound` 方法。在调用 `make_sound` 函数时，可以传入不同的对象（`Dog` 或 `Cat` 的实例），产生不同的行为，这就是多态性的体现。

多态性使得代码更加灵活，可以轻松地扩展和修改程序，同时也提高了代码的可读性和可维护性。

## 19.鸭子类型

鸭子类型（Duck Typing）是一种动态类型的概念，它关注的不是对象的类型本身，而是对象的行为和能力。鸭子类型的核心思想是：如果某个对象走起路来像鸭子、叫起来像鸭子，那么它就可以被视为鸭子。换句话说，对象的类型是由它的行为决定的，而不是由它的类或类型声明决定的。

这个概念常常用于动态语言（例如Python）中，不要求一个对象严格地继承自某个特定的类或接口，只要对象具有特定的行为和属性，就可以被视为满足特定类型的要求。这种特性使得代码更加灵活，可以处理各种不同结构和类型的对象。

例如，在Python中，可以定义一个接受任何拥有`quack`方法的对象的函数，而无需关心对象的具体类型：

```
class Duck:
    def quack(self):
        print("Quack!")

class Person:
    def quack(self):
        print("I'm quacking like a duck!")

def make_quack(object_with_quack_method):
    object_with_quack_method.quack()

duck = Duck()
person = Person()

make_quack(duck)    # 输出: Quack!
make_quack(person)  # 输出: I'm quacking like a duck!
```

在这个例子中，`make_quack` 函数接受任何具有`quack`方法的对象作为参数。`Duck` 类和 `Person` 类都具有`quack`方法，因此它们都可以被传递给 `make_quack` 函数，这就是鸭子类型的体现。这种方式使得函数的参数更加灵活，可以接受多种类型的对象，只要它们具有特定的行为。

## 20.扩展内建类型

在Python中，你可以扩展内建类型（如`list`、`dict`、`str`等），给它们添加额外的方法或者修改现有的方法。这可以通过继承内建类型并添加自定义方法，或者通过使用装饰器来实现。

### 继承内建类型并添加自定义方法：

```python
class MyList(list):
    def custom_method(self):
        return "This is a custom method for MyList"

# 创建自定义列表对象
my_list = MyList([1, 2, 3, 4, 5])

# 使用自定义方法
print(my_list.custom_method())  # 输出: This is a custom method for MyList

# 使用内建列表方法
my_list.append(6)
print(my_list)  # 输出: [1, 2, 3, 4, 5, 6]
```

在这个例子中，我们定义了一个继承自内建列表类型的`MyList`类，并添加了一个自定义方法`custom_method`。实例化后，`my_list`对象就拥有了`custom_method`方法。

### 使用装饰器扩展内建类型：

```
# 装饰器函数，接受一个列表作为参数，返回一个新的列表
def custom_decorator(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return [x * 2 for x in result]  # 将列表中的每个元素乘以2
    return wrapper

# 使用装饰器扩展内建列表类型的方法
@custom_decorator
def modify_list(input_list):
    return input_list

# 调用扩展后的方法
original_list = [1, 2, 3, 4, 5]
modified_list = modify_list(original_list)
print(modified_list)  # 输出: [2, 4, 6, 8, 10]
```

在这个例子中，`custom_decorator` 是一个装饰器函数，它将传入的列表中的每个元素乘以2。`modify_list` 函数使用了这个装饰器，并将其应用于传入的列表。最终，`modified_list`中的元素被扩展了。

请注意，扩展内建类型可能导致代码的可读性降低和意外的副作用。因此，在使用这种技术时，确保你了解代码的行为，并且小心不要覆盖或破坏内建类型的核心行为。

## 21.数据类

在Python中，"数据类"通常指的是具有一些特定特征的类，这些特征使得它们更适合用于存储数据的目的。通常来说，数据类应该主要用于存储数据而不包含太多的业务逻辑。Python的`dataclasses`模块提供了一个简单的方式来定义数据类。

在Python 3.7及以上版本中，你可以使用`@dataclass`装饰器来定义数据类。数据类会自动为你生成`__init__`、`__repr__`等特殊方法，省去了手动编写这些方法的麻烦。

以下是一个使用`dataclasses`模块定义数据类的示例：

```
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int

# 创建数据类的实例
p = Point(1, 2)
print(p)  # 输出: Point(x=1, y=2)

# 数据类自动具有__eq__方法
p2 = Point(1, 2)
print(p == p2)  # 输出: True

# 数据类自动具有__hash__方法
print(hash(p))  # 输出: 384307168202284039

# 数据类自动具有__repr__方法
print(repr(p))  # 输出: Point(x=1, y=2)
```

在这个例子中，`Point` 是一个数据类，它有两个字段`x`和`y`，分别表示点的横坐标和纵坐标。使用`@dataclass`装饰器，你无需手动编写`__init__`、`__repr__`等方法，它们会被自动创建。

数据类在许多场景下非常有用，例如在处理配置、传递简单的数据结构等情况下，可以让你更容易地创建和维护类。但需要注意，数据类主要用于存储数据，不应该包含太多的业务逻辑。



### 命名元组（namedtuple）：

- **轻量级：** 命名元组是轻量级的数据结构，它比普通的类或`dataclasses`更简单。
- **不可变性：** 命名元组是不可变的，一旦创建就不能修改它的属性值。如果你需要不可变的数据结构，命名元组是一个好选择。
- **性能：** 由于不可变性，命名元组在某些情况下可能比可变的数据结构（如`dataclasses`生成的类）更快，因为不需要考虑内部状态的变化。

**示例：**

```
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])
p = Point(x=1, y=2)
```

### 数据类（dataclasses） :

- **可变性：** `dataclasses`生成的类是可变的，你可以修改它的属性值。
- **默认方法：** `dataclasses`会自动生成`__init__`、`__repr__`等特殊方法，减少了手动编写这些方法的工作量。
- **更多的功能：** 如果你需要定制类的行为，例如定义自定义的`__eq__`、`__lt__`等方法，`dataclasses`提供了更多的选项。

**示例：**

```
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int
```

**如何选择：**

- 如果你需要一个轻量级的、不可变的数据结构，可以使用命名元组。
- 如果你希望有一个可变的、具有默认特殊方法的类，并且不想手动编写这些方法，可以使用`dataclasses`。



# 标准库

## 一.Path类

在Python中，`Path`类位于内置模块`pathlib`中，它提供了一个面向对象的API来处理文件系统路径。`pathlib`模块引入了`Path`类，使得路径操作更加直观和面向对象。`Path`类可以用来替代`os.path`模块中的函数，提供了更加灵活和易用的方法来操作文件和目录路径。

以下是`Path`类的一些常用方法和属性：

### 创建Path对象：

```
from pathlib import Path

# 创建Path对象
path = Path("/path/to/directory")
```

### 常用属性和方法：

- **`.exists()`:** 判断路径是否存在。
- **`.is_file()`:** 判断路径是否为文件。
- **`.is_dir()`:** 判断路径是否为目录。
- **`.name`:** 返回路径的基本名称（文件名或目录名）。
- **`.parent`:** 返回路径的父目录。
- **`.suffix`:** 返回路径的后缀（文件扩展名）。
- **`.parts`:** 返回路径的各个部分作为元组。
- **`.joinpath()`:** 连接路径的各个部分，返回新的Path对象。
- **`.resolve()`:** 返回绝对路径的规范版本。
- **`.glob(pattern)`:** 根据通配符模式返回一个生成器，用于匹配文件。
- **`.read_text()`:** 读取文件内容为文本。
- **`.write_text(content)`:** 将文本内容写入文件。
- **`.read_bytes()`:** 读取文件内容为字节。
- **`.write_bytes(data)`:** 将字节数据写入文件。

示例用法：

```
from pathlib import Path

# 创建Path对象
path = Path("/path/to/directory")

# 检查路径是否存在
if path.exists():
    # 如果是目录，遍历目录下的文件
    if path.is_dir():
        for file in path.iterdir():
            print(file.name)
    # 如果是文件，读取文件内容
    elif path.is_file():
        content = path.read_text()
        print(content)
else:
    print("路径不存在")
```

使用`Path`类可以使得文件和目录的操作更加简洁和可读，而不需要调用`os.path`模块中的各种函数。

当使用`pathlib`的`Path`类时，可以使用不同的方法执行各种操作。以下是每个方法的一个简单例子：

### 1. 创建和删除：

- **`Path.mkdir()`:** 创建目录。

  ```
  from pathlib import Path
  
  # 创建目录
  new_directory = Path("/path/to/new_directory")
  new_directory.mkdir()
  ```

- **`Path.rmdir()`:** 删除空目录。

  ```
  from pathlib import Path
  
  # 删除目录
  directory_to_delete = Path("/path/to/directory")
  directory_to_delete.rmdir()
  ```

- **`Path.unlink()`:** 删除文件。

  ```
  from pathlib import Path
  
  # 删除文件
  file_to_delete = Path("/path/to/file.txt")
  file_to_delete.unlink()
  ```

### 2. 检查路径和属性：

- **`Path.exists()`:** 判断路径是否存在。

  ```
  from pathlib import Path
  
  # 检查路径是否存在
  path_to_check = Path("/path/to/somefile.txt")
  if path_to_check.exists():
      print("文件存在")
  else:
      print("文件不存在")
  ```

- **`Path.is_file()`:** 判断路径是否为文件。

  ```
  from pathlib import Path
  
  # 检查路径是否为文件
  file_path = Path("/path/to/somefile.txt")
  if file_path.is_file():
      print("这是一个文件")
  else:
      print("这不是一个文件")
  ```

### 3. 目录和文件操作：

- **`Path.iterdir()`:** 返回目录中的所有子目录和文件的迭代器。

  ```
  from pathlib import Path
  
  # 遍历目录中的所有子目录和文件
  directory_path = Path("/path/to/directory")
  for item in directory_path.iterdir():
      print(item)
  ```

- **`Path.glob(pattern)`:** 根据通配符模式返回文件和子目录。

  ```
  from pathlib import Path
  
  # 使用通配符获取所有.txt文件
  directory_path = Path("/path/to/directory")
  txt_files = directory_path.glob("*.txt")
  for file in txt_files:
      print(file)
  ```

### 4. 读写文件内容：

- **`Path.read_text()`:** 读取文件内容为文本。

  ```
  from pathlib import Path
  
  # 读取文本文件内容 返回以字符串方式返回
  file_path = Path("/path/to/somefile.txt")
  content = file_path.read_text(encoding="utf-8")
  print(content)
  ```

- **`Path.write_text(content)`:** 将文本内容写入文件。

  ```
  from pathlib import Path
  
  # 写入文本到文件
  file_path = Path("/path/to/somefile.txt")
  content = "Hello, World!"
  file_path.write_text(content)
  ```

### 5. 路径拼接和转换：

- **`Path.joinpath(\*paths)`:** 连接路径的各个部分，返回新的`Path`对象。

  ```
  from pathlib import Path
  
  # 连接路径的各个部分
  base_path = Path("/path/to")
  file_name = "file.txt"
  full_path = base_path.joinpath(file_name)
  print(full_path)
  ```

- **`Path.as_posix()`:** 将路径转换为字符串，并使用正斜杠 (`/`) 分隔路径部分。

  ```
  from pathlib import Path
  
  # 将路径转换为字符串
  path = Path("/path/to/somefile.txt")
  path_string = path.as_posix()
  print(path_string)
  ```

这些例子演示了如何使用`pathlib`的`Path`类的不同方法进行文件和目录操作。你可以根据需要，选择合适的方法来执行各种操作。

### 6.将文件复制到其他地方

```
# 导入必要的模块
from pathlib import Path
import shutil

# 源文件的路径
source = Path(r"D:\OneDrive\桌面\Python\Text.py")

# 目标文件的路径，位于当前工作目录下的 "text.py"
target = Path() / "text.py"

# 使用 shutil 模块的 copy 函数将源文件复制到目标路径
shutil.copy(source, target)
```

以上代码的操作步骤为：

1. **`source = Path(r"D:\OneDrive\桌面\Python\Text.py")`:** 创建了一个 `Path` 对象，表示了源文件的路径。
2. **`target = Path() / "text.py"`:** 创建了另一个 `Path` 对象，表示了目标文件的路径。在这里，`Path()` 表示当前工作目录，使用 `/` 运算符连接路径，然后文件名为 `"text.py"`，表示目标文件位于当前工作目录下，文件名为 `text.py`。
3. **`shutil.copy(source, target)`:** 使用 `shutil` 模块的 `copy()` 函数将源文件复制到目标文件。这一步将源文件 `Text.py` 复制到当前工作目录下并命名为 `text.py`。

这段代码的功能是将 `D:\OneDrive\桌面\Python\Text.py` 文件复制到当前工作目录下，并命名为 `text.py`，并确保目标文件的内容与源文件相同。请确保源文件路径是正确的，并且目标路径是你希望将文件复制到的地方。

### 7.处理zip文件

#### 1.压缩zip文件

```
from pathlib import Path
from zipfile import ZipFile


with ZipFile("files.zip","w") as zip:
    for path in Path("text.py").rglob("*.*"):
        zip.write(path)
```

1. `with ZipFile("files.zip", "w") as zip:`: 这行代码使用 `with` 语句创建了一个名为 "files.zip" 的 ZIP 文件，并以写入模式打开它。`zip` 是一个 `ZipFile` 对象，你可以使用它来添加文件到 ZIP 文件中。
2. `for path in Path("text.py").rglob("*.*"):`: 这行代码使用 `Path` 对象创建了一个路径对象，表示名为 "text.py" 的目录。然后，`rglob("*.*")` 方法返回了这个目录及其子目录中的所有文件（带有任意扩展名的文件）的路径对象。这个循环会遍历这些文件的路径。
3. `zip.write(path)`: 在每次迭代中，当前的文件路径 `path` 被添加到 ZIP 文件中，`zip.write()` 方法将文件写入 ZIP 文件。

综合起来，这段代码的作用是遍历指定目录 "text.py" 中的所有文件，包括子目录中的文件，将它们逐个添加到名为 "files.zip" 的 ZIP 文件中。最终，你将得到一个包含指定目录中所有文件的 ZIP 归档文件。

#### 2.解压zip文件

```
from pathlib import Path
from zipfile import ZipFile


with ZipFile("files.zip") as zip:
    print(zip.namelist())
    info = zip.getinfo("ecommerce/__init__.py")
    print(info.file_size)
    print(info.compress_size)
    zip.extractall("extract")
```

1. `with ZipFile("files.zip") as zip:`: 这行代码使用`with`语句打开名为"files.zip"的ZIP文件。在这个上下文中，`zip`是一个`ZipFile`对象，你可以使用它来操作ZIP文件。
2. `print(zip.namelist())`: 这行代码打印了ZIP文件中所有文件和目录的名称列表。`namelist()`方法返回ZIP文件中包含的所有文件和目录的名称。
3. `info = zip.getinfo("ecommerce/__init__.py")`: 这行代码获取了ZIP文件中特定文件（在这里是"ecommerce/**init**.py"）的信息。`getinfo()`方法返回一个`ZipInfo`对象，其中包含了文件的元数据，例如文件大小、压缩后的大小等。
4. `print(info.file_size)`: 这行代码打印了"ecommerce/**init**.py"文件在ZIP文件中的原始大小（以字节为单位）。
5. `print(info.compress_size)`: 这行代码打印了"ecommerce/**init**.py"文件在ZIP文件中的压缩后大小（以字节为单位）。
6. `zip.extractall("extract")`: 这行代码将ZIP文件中的所有内容解压缩到当前工作目录下的"extract"子目录中。`extractall()`方法会解压缩ZIP文件中的所有文件和目录，并将它们放置在指定的目录中。

综合起来，这段代码的作用是打开名为"files.zip"的ZIP文件，获取其中指定文件的大小信息，然后将ZIP文件中的所有内容解压缩到"extract"目录中。

### 8.处理csv文件

#### 1.写入csv文件

```
import csv

with open("data.csv","w") as file:
    writer = csv.writer(file)
    writer.writerow(["transaction_id","product_id","price_id"])
    writer.writerow([1000,1,5])
    writer.writerow([1001,2,15])
```

这段代码使用了Python的内置`csv`模块来创建并写入CSV文件。

1. `import csv`: 这行代码导入了Python标准库中的`csv`模块，该模块提供了处理CSV（逗号分隔值）文件的功能。
2. `with open("data.csv", "w") as file:`: 这行代码使用`open()`函数以写入模式打开名为"data.csv"的文件。`with`语句用于确保在操作完成后文件会被正确关闭，即使发生异常也会被处理。
3. `writer = csv.writer(file)`: 这行代码创建了一个`csv.writer`对象，该对象与打开的文件关联，用于写入CSV格式的数据。
4. `writer.writerow(["transaction_id","product_id","price_id"])`: 这行代码使用`writerow()`方法将包含列名的列表写入CSV文件。在CSV文件的第一行中，会包含"transaction_id"、"product_id"和"price_id"这三个列名。
5. `writer.writerow([1000,1,5])`: 这行代码使用`writerow()`方法将一个包含数据的列表写入CSV文件。这行代码会在CSV文件的第二行中写入数据：1000, 1, 5。
6. `writer.writerow([1001,2,15])`: 这行代码类似于上一行，它将另一个包含数据的列表写入CSV文件。这行代码会在CSV文件的第三行中写入数据：1001, 2, 15。

最终，运行这段代码会在当前目录下创建一个名为"data.csv"的CSV文件，内容如下：

```
yamlCopy codetransaction_id,product_id,price_id
1000,1,5
1001,2,15
```

CSV文件中的每一行代表一个数据行，逗号分隔了不同的列。

#### 2.读取csv文件

```
import csv

with open("data.csv") as file:
    reader = csv.reader(file)
    print(list(reader))
    for row in reader:
        print(row)
```

这段代码使用了Python的内置`csv`模块来读取CSV文件。

1. `import csv`: 这行代码导入了Python标准库中的`csv`模块，该模块提供了处理CSV文件的功能。
2. `with open("data.csv") as file:`: 这行代码打开了名为"data.csv"的CSV文件，并使用`with`语句确保在操作完成后文件会被正确关闭。
3. `reader = csv.reader(file)`: 这行代码创建了一个`csv.reader`对象，该对象与打开的CSV文件关联，用于从文件中读取CSV格式的数据。
4. `print(list(reader))`: 这行代码将`csv.reader`对象转换为列表，并将其打印出来。在这里，`list(reader)`会返回一个包含CSV文件所有行的列表。注意，在此之后，文件指针会在文件的末尾，因此后续的`for row in reader:`循环将不会读取到任何数据。
5. `for row in reader:`: 这行代码尝试迭代`csv.reader`对象，逐行读取CSV文件的内容。但由于在前面已经将`reader`对象转换为列表，所以在此处`reader`对象已经为空，循环内的代码不会执行。

因此，这段代码的输出将会是：

```
cssCopy code
[['transaction_id', 'product_id', 'price_id'], ['1000', '1', '5'], ['1001', '2', '15']]
```

第一个`print(list(reader))`语句打印了整个CSV文件的内容，而`for row in reader:`循环没有输出任何内容，因为`reader`对象已经在前面的`list(reader)`转换中被消耗完了。

### 9.处理JSON文件

在Python中，你可以使用内置的`json`模块来处理JSON文件。这个模块提供了方法来解析JSON数据（从JSON字符串到Python数据结构）和将Python数据结构转换为JSON格式。以下是一些基本的JSON文件处理操作：

#### 1. 读取JSON文件：

```
import json

# 从JSON文件中读取数据
with open("data.json", "r") as json_file:
    data = json.load(json_file)
    print(data)  # data是一个Python数据结构，包含了从JSON文件中读取的数据
```

#### 2. 写入JSON文件：

```
import json

# 要写入的数据，可以是Python字典、列表等数据结构
data = {
    "name": "Alice",
    "age": 30,
    "city": "New York",
    "isEmployed": True,
    "skills": ["Python", "JavaScript", "SQL"]
}

# 将数据写入JSON文件
with open("output.json", "w") as json_file:
    json.dump(data, json_file)
```

#### 3. 将Python数据结构转换为JSON字符串：

```
import json

# Python数据结构
data = {
    "name": "Alice",
    "age": 30,
    "city": "New York",
    "isEmployed": True,
    "skills": ["Python", "JavaScript", "SQL"]
}

# 将数据转换为JSON字符串
json_string = json.dumps(data)
print(json_string)
```

在这些示例中，`json.load()` 用于从JSON文件中读取数据，`json.dump()` 用于将数据写入JSON文件，`json.dumps()` 用于将Python数据结构转换为JSON字符串。请确保在读取和写入文件时使用正确的文件路径和文件名。

## 二.处理SQList数据库

​                                                                          **学完数据库再回来看**

## 三.时间

### 1.测试性能

在Python中，`time.time()` 函数返回当前的系统时间（从1970年1月1日午夜到现在的秒数）。通常，程序员使用 `time.time()` 函数来计算代码段的执行时间，例如：

```
import time

# 记录开始时间
start = time.time()

# 在这里执行你的代码

# 记录结束时间
end = time.time()

# 计算代码执行时间
execution_time = end - start
print(f"Code executed in {execution_time} seconds")
```

在这个示例中，`start` 变量存储了代码开始执行的时间戳，然后在代码执行结束后，**通过 `time.time()` 获取当前时间戳**，将两者相减得到代码执行时间。这个方法通常用于性能测试或者优化代码，以便了解代码执行所需的时间。

在Python中，你可以使用`datetime`模块来处理日期和时间。`datetime`模块提供了多个类来操作日期和时间，包括`datetime`、`date`、`time`等。以下是一些常见的日期时间处理操作：

### 2.获取当前日期和时间：

```
from datetime import datetime

current_datetime = datetime.now()
print(current_datetime)
```

### 3.格式化日期时间为字符串：

```
from datetime import datetime

current_datetime = datetime.now()
formatted_date = current_datetime.strftime("%Y-%m-%d %H:%M:%S")
print(formatted_date)
```

在这个例子中，`strftime()` 方法将`datetime`对象格式化为字符串。`%Y`、`%m`、`%d`、`%H`、`%M`和`%S`是格式化字符串中的格式码，代表年、月、日、小时、分钟和秒。

### 4.将字符串解析为日期时间对象：

```
from datetime import datetime

date_string = "2023-10-26 14:30:00"
parsed_date = datetime.strptime(date_string, "%Y-%m-%d %H:%M:%S")
print(parsed_date)
```

在这个例子中，`strptime()` 方法将一个字符串解析为`datetime`对象。第一个参数是待解析的字符串，第二个参数是字符串的格式。

### 5.执行日期时间计算：

```
from datetime import datetime, timedelta

current_datetime = datetime.now()
future_datetime = current_datetime + timedelta(days=7, hours=3)
print(future_datetime)
```

在这个例子中，`timedelta` 类被用来表示时间间隔。在这里，我们将当前日期时间加上7天3小时，并打印结果。

这些只是`datetime`模块提供的一些基本操作。你可以使用这些工具进行各种日期时间的处理，包括计算、比较、格式化等。

## 四.创建随机数

在Python中，你可以使用`random`模块来生成随机数。`random`模块提供了许多用于生成随机数的函数。以下是一些常见的随机数生成方法：

### 1.生成随机整数：

```
import random

# 生成一个在范围 [a, b] 内的随机整数
random_integer = random.randint(a, b)
print(random_integer)
```

这里，`random.randint(a, b)` 生成的随机整数在 `a` 和 `b` 之间（包括 `a` 和 `b`）。

### 2.生成随机浮点数：

```
import random

# 生成一个在范围 [a, b) 内的随机浮点数
random_float = random.uniform(a, b)
print(random_float)
```

这里，`random.uniform(a, b)` 生成的随机浮点数在 `a` 和 `b` 之间（不包括 `b`）。

### 3.从列表中随机选择元素：

```
import random

my_list = [1, 2, 3, 4, 5]
random_element = random.choice(my_list)
print(random_element)
```

这里，`random.choice(my_list)` 从列表 `my_list` 中随机选择一个元素。

### 4.打乱列表中元素的顺序：

```
import random

my_list = [1, 2, 3, 4, 5]
random.shuffle(my_list)
print(my_list)
```

这里，`random.shuffle(my_list)` 将列表 `my_list` 中的元素随机打乱顺序。



**请注意，这些随机数生成函数的结果是伪随机的，即它们基于初始种子生成，种子相同的情况下，生成的随机数序列也相同。你可以使用 `random.seed(seed)` 来设置随机数生成的种子，以便获得可预测的随机数序列。**

当我们说随机数是“伪随机”的时候，意味着这些随机数是通过计算机算法生成的，而不是通过真正的随机过程（例如硬件随机数生成器）产生的。这些算法需要一个初始值，称为“种子”（seed），以便产生随机数序列。如果你使用相同的种子，这些算法将生成相同的随机数序列。

例如，考虑以下的代码：

```
import random

random.seed(42)  # 设置种子为42
print(random.randint(1, 100))  # 输出一个1到100之间的随机整数
```

在这个例子中，我们使用 `random.seed(42)` 来设置随机数生成器的种子为42。无论何时你运行这段代码，它都会生成相同的随机整数，因为种子是固定的。

种子的主要作用是在调试和测试中创建可重复的结果。如果你需要在每次运行程序时得到不同的随机数，就不需要设置种子。但是，如果你希望在调试时得到相同的结果，可以设置相同的种子，这样每次运行程序时就会得到相同的随机数序列。

要强调的是，伪随机数生成器的随机性依赖于种子的选择。如果你使用不同的种子，将会得到不同的随机数序列。在实际应用中，常常使用当前系统时间戳作为种子，以确保每次运行时都得到一个不同的种子，从而生成不同的随机数序列。

### 5.扩展内容

```
import random
import string


print(random.random())  #它会生成 [0,1) 的随机小数 
print(random.choices([1,2,3,4],k=2))  #参数k=2表示选择2个元素
print(",".join(random.choices("abcdefgh",k=4)))


print(string.ascii_letters) # 这是string模块中包含所有字母的字符串，即包括小写字母和大写字母。你可以用它来生成随机字母。
print("".join(random.choices(string.ascii_letters + string.digits, k=4))) #里面包含大小写字母和数字可以生成4个数据数
print(string.digits) #这是string模块中包含所有数字的字符串，你可以用它来生成随机数字。
```

## 五.自动打开浏览器

`webbrowser` 模块是Python的一个内置模块，可以用来在默认的Web浏览器中打开一个网址。

```
import webbrowser

url = "https://www.example.com"
webbrowser.open(url)
```

这会在默认的Web浏览器中打开指定的URL。

## 六.发送邮件

1. 这段代码使用了 Python 的 `smtplib` 和 `email` 模块发送一封电子邮件，附带了文本消息和一张图片附件。以下是代码的详细解释：

   1. **导入模块：**

   ```
   from email.mime.multipart import MIMEMultipart
   from email.mime.text import MIMEText
   from email.mime.image import MIMEImage
   from pathlib import Path
   import smtplib
   ```

   这里导入了需要用到的模块，包括创建邮件结构的 `MIMEMultipart`、`MIMEText` 用于文本消息、`MIMEImage` 用于图片附件，`Path` 用于处理文件路径，以及 `smtplib` 用于发送邮件。

   1. **创建邮件对象：**

   ```
   message = MIMEMultipart()
   message["from"] = "王旭"
   message["to"] = "wxu743571@gmail.com"
   message["subject"] = "This is a test"
   ```

   这段代码创建了一个 `MIMEMultipart` 对象，并设置了邮件的发送者、接收者和主题。

   1. **添加文本消息和图片附件：**

   ```
   message.attach(MIMEText("Body"))
   message.attach(MIMEImage(Path("mosh.png").read_bytes()))
   ```

   - `message.attach(MIMEText("Body"))` 将文本消息添加到邮件对象中。
   - `message.attach(MIMEImage(Path("mosh.png").read_bytes()))` 从文件路径 `"mosh.png"` 读取图片的字节内容，并将图片附件添加到邮件对象中。

   1. **连接到 SMTP 服务器并发送邮件：**

   ```
   with smtplib.SMTP(host="smtp.gmail.com", port=587) as smtp:
       smtp.ehlo()
       smtp.starttls()
       smtp.login("wxu743571@gmail.com", "xiaoxu512")
       smtp.send_message(message)
       print("Sent...")
   ```

   这段代码连接到 Gmail 的 SMTP 服务器，启用 TLS 加密，登录到邮箱账号，然后使用 `send_message()` 方法发送邮件。邮件中包含了文本消息和附带的图片。最后，打印出 "Sent..." 表示邮件已发送成功。

   请确保代码中的图片文件路径是正确的，并且你的邮箱账号和密码是正确的，否则邮件发送会失败。

## 七.操作模板

**有时候我们发送文件的内容很多，我们需要html文件来写这些内容然后通过方法到python中把它导入**

## 八.命令行参数

**命令行参数提供了一种简单而强大的方式，使得你的程序能够灵活地适应不同的需求和场景，实现更加智能、自动化的处理任务**

在Python中，你可以使用命令行参数（Command Line Arguments）来在运行脚本时传递数据给你的程序。命令行参数是在命令行（或终端）中传递给脚本的额外的输入信息。这些参数可以用来实现很多不同的功能，例如：

1. **传递输入数据：** 你可以通过命令行参数将输入数据传递给脚本。例如，一个计算器程序可以接受两个数字作为命令行参数，并返回它们的和。

   ```
   pythonCopy codeimport sys
   
   num1 = float(sys.argv[1])
   num2 = float(sys.argv[2])
   result = num1 + num2
   print("Sum:", result)
   ```

   在命令行中运行这个脚本：`python script.py 3 5` 将会输出 `Sum: 8`。

2. **配置参数：** 你可以使用命令行参数来配置程序的行为。例如，一个文件处理程序可以接受一个输出目录作为命令行参数。

   ```
   pythonCopy codeimport sys
   import os
   
   output_dir = sys.argv[1]
   files = os.listdir()
   # 处理文件并将结果保存到指定的输出目录
   ```

   在命令行中运行这个脚本：`python script.py output_directory`，它会将处理后的文件保存到指定的输出目录中。

3. **自动化脚本：** 你可以使用命令行参数来自动化脚本的行为。例如，一个备份脚本可以接受源目录和目标目录作为命令行参数。

   ```
   pythonCopy codeimport sys
   import shutil
   
   source_dir = sys.argv[1]
   target_dir = sys.argv[2]
   shutil.copytree(source_dir, target_dir)
   ```

   在命令行中运行这个脚本：`python script.py source_directory target_directory`，它会将源目录的内容复制到目标目录中。

总的来说，命令行参数为你的Python程序提供了一种在运行时接收外部输入的方法，使得你的程序更加灵活和可配置。

命令行参数在实际工作中有很多用途。以下是一些常见的实际应用场景：

1. **自动化脚本和任务调度：** 当你需要在特定的时间或事件发生时运行脚本时，可以使用命令行参数。例如，你可以编写一个定时备份脚本，该脚本在每天晚上运行，将特定文件夹的内容备份到指定位置。
2. **批处理任务：** 在数据处理、文件操作、网络请求等需要批量处理的任务中，你可以使用命令行参数来指定输入文件夹、输出文件夹、处理方式等信息，从而实现自动化批处理。
3. **配置和设置：** 命令行参数可以用来配置程序的行为。例如，一个服务器程序可以通过命令行参数指定监听的端口号、日志级别、数据库连接信息等配置参数。
4. **测试和调试：** 在测试时，你可以使用命令行参数传递测试用例、测试模式等信息。这使得你可以通过命令行方便地运行特定的测试套件。
5. **数据处理和分析：** 在数据处理和分析任务中，你可以使用命令行参数来指定输入文件、输出文件、数据处理方法等。这样，同一个脚本可以用不同的参数执行不同的数据处理任务。
6. **命令行工具：** 命令行参数常用于创建命令行工具。这种工具可以通过命令行接受不同的参数，从而执行不同的操作。例如，版本控制系统（如Git）的命令行工具，可以通过命令行参数执行不同的版本控制操作。

总之，命令行参数提供了一种简单而强大的方式，使得你的程序能够灵活地适应不同的需求和场景，实现更加智能、自动化的处理任务。

## 九.运行外部程序

在Python中，你可以使用`subprocess`模块来运行外部程序。`subprocess`模块允许你生成新的进程，连接到它们的输入/输出/错误管道，并且获取它们的返回值。

以下是使用`subprocess`模块运行外部程序的几种方法：

### 1. **使用`subprocess.run()`函数（Python 3.5及以上）:**

`subprocess.run()`函数用于运行外部命令，等待它完成，并且返回一个`CompletedProcess`实例，包含了命令的返回码等信息。

```
pythonCopy codeimport subprocess

result = subprocess.run(["ls", "-l"], capture_output=True, text=True)
print(result.stdout)
```

在这个例子中，`subprocess.run()`函数运行了`ls -l`命令，并且将命令的输出（标准输出）捕获到`result.stdout`中。

### 2. **使用`subprocess.Popen()`类:**

`subprocess.Popen()`类用于更灵活地管理进程。它允许你更精细地控制输入、输出和错误。

```
pythonCopy codeimport subprocess

process = subprocess.Popen(["ls", "-l"], stdout=subprocess.PIPE, text=True)
output, error = process.communicate()
print(output)
```

在这个例子中，`subprocess.Popen()`打开了一个`ls -l`的进程，并且使用`communicate()`方法获取了命令的输出。

### 3. **使用`os.system()`函数:**

`os.system()`函数可以在操作系统的shell中运行命令。它的返回值是命令的退出状态码。

```
pythonCopy codeimport os

os.system("ls -l")
```

这个方法比较简单，但是不如`subprocess`模块提供的控制和灵活性多。

在选择使用哪种方法时，你需要考虑你的需求。如果你只需要运行一个简单的命令并获取其输出，`subprocess.run()`函数通常是一个不错的选择。如果你需要更多的控制权，可以使用`subprocess.Popen()`类。





# 库索引

**pypi.org ** Python第三方库地址

**pipenv**   就是将pip和虚拟环境结合在一起的程序  相似于（npm依赖管理器）

## 虚拟环境

虚拟环境（Virtual Environment）是Python中的一个概念，它允许你在同一台计算机上同时管理多个独立的Python环境。每个虚拟环境都可以拥有自己独立的Python解释器和安装的库，这样就可以避免不同项目之间的依赖冲突。

使用虚拟环境的主要目的是：

1. **隔离项目依赖**: 不同的项目可能需要不同版本的Python或不同版本的第三方库。使用虚拟环境，你可以为每个项目创建一个独立的环境，确保项目所需的依赖不会互相干扰。
2. **避免权限问题**: 在某些系统中，你可能没有在全局Python环境中安装新库的权限。使用虚拟环境，你可以在用户目录下创建一个环境，无需超级用户权限就可以安装新库。

`Pipfile` 和 `Pipfile.lock` 是 Python 项目中常用的两个文件，用于管理项目的依赖关系和版本。它们的作用有所不同：

## pipenv常见命令

`pipenv` 是一个用于管理Python项目依赖和虚拟环境的工具，它结合了`pip`、`virtualenv`和`Pipfile`，提供了一种更简洁、更强大的依赖管理方式。以下是一些常见的 `pipenv` 命令：

### 创建新项目

在当前目录中创建一个新的 `Pipfile` 文件，并自动初始化虚拟环境：

```
pipenv install
```

### 安装依赖

安装一个包并将其添加到 `Pipfile` 文件中（类似于 `pip install`）：

```
pipenv install package_name
```

### 安装开发依赖

安装一个开发时依赖，并将其添加到 `[dev-packages]` 部分：

```
pipenv install --dev package_name
```

### 卸载包

从虚拟环境和 `Pipfile` 文件中移除一个包：

```
pipenv uninstall package_name
```

### 查看依赖

显示当前项目的依赖（包括开发依赖）：

```
pipenv graph
```

### 进入虚拟环境

激活当前项目的虚拟环境：

```
pipenv shell
```

### 运行Python脚本

在虚拟环境中运行一个Python脚本：

```
pipenv run python script.py
```

### 查看虚拟环境路径

显示当前项目的虚拟环境路径：

```
pipenv --venv
```

### 查看Python解释器信息

显示当前项目的Python解释器信息：

```
pipenv --py
```

### 锁定依赖版本

锁定依赖的版本并生成 `Pipfile.lock` 文件：

```
pipenv lock
```

这些命令涵盖了在使用 `pipenv` 进行Python项目依赖管理时的常见任务。`pipenv` 提供了一种更简单和更现代的方式来创建虚拟环境，安装依赖，以及管理项目的依赖关系。





当你开发Python项目时，你通常会依赖于很多第三方库（比如requests、numpy等）。`Pipfile` 和 `Pipfile.lock` 是用来管理这些依赖关系的文件。

## Pipfile:

- **作用：** `Pipfile` 是一个配置文件，它列出了你的项目所需的所有Python包及其版本号。你可以在这里指定项目所需的依赖包。

- **生成方式：** 你可以手动创建 `Pipfile` 文件，也可以使用 `pipenv` 命令（例如 `pipenv install package_name`）自动生成并安装依赖包。

  

## Pipfile.lock:

- **作用：** `Pipfile.lock` 是 `Pipfile` 的锁定版本，记录了你项目依赖的确切版本号。它确保了在不同环境中安装的依赖包版本一致。
- **生成方式：** 当你运行 `pipenv install` 命令时，`Pipfile.lock` 会被自动生成。它会根据 `Pipfile` 中的依赖信息，包括依赖的依赖，确定每个包的具体版本。
- **示例：** `Pipfile.lock` 是一个复杂的JSON文件，包含了项目的所有依赖关系及其版本信息。

总结来说，`Pipfile` 让你明确列出项目的依赖关系，而 `Pipfile.lock` 则确保了在不同环境中这些依赖包的版本一致性。在开发中，通常使用 `Pipfile.lock` 确保项目在不同的开发、测试和生产环境中都能保持一致。







```
pipenv install --ignore-pipfile    忽略pipfile文件安装依赖，用pipfile.lock文件来安装依赖
```
