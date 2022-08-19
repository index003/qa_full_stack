# Python Knowledge Summary



## 第一部分 字符串

```python
name = 'wu victor'

# 首字母大写
print(name.title())

# 切换大小写
print(name.upper())
print(name.lower())

# 合并字符串
first_name = 'wu'
last_name = 'victor'
print((first_name +' ' + last_name).title())

# 删除空白
contain_spaces = ' abcd '
print(contain_spaces.strip())
print(contain_spaces.rstrip())
print(contain_spaces.lstrip())

# 数字转换为字符串
age = 18
print("happy birthday ".title() + str(age))
print("happy birthday".title(), age)

# f格式 在字符串里可以引用变量

first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"
print(full_name)
print(f"Hello {full_name.title()}")

# 字符串
str_join = " ".join(["join", "puts", "spaces", "between", "elements"])
print(str_join)

str_join_01 = "::".join(["join", "puts", "spaces", "between", "elements"])
print(str_join_01)

str_join_02 = "".join(["He", "ll", "o"])
print(str_join_02)

x = 'a b c d'
x_split = x.split()
print(x_split)

x_1 = 'vssisstssossr'
x_1_split = x_1.split('ss')
print(x_1_split)

y = 'a b c d'
y_split = y.split(' ', 1)
print(y_split)

y_2 = 'a b c d'
y_2_split = y_2.split(' ', 2)
print(y_2_split)

str_test = "this is a test"
str_test_join = "-".join(str_test.split())
print(str_test_join)

strip_test = " hello, world! "
print(strip_test.lstrip())
print(strip_test.rstrip())
print(strip_test.strip())

url_test = "www.python.org"
print(url_test.strip("w"))
print(url_test.strip("gor"))
print(url_test.strip(".grow"))


x_2 = 'vssisstssossr'
x_3 = x_2.replace("ss", "-")
print(x_3)

# 运行结果
"""
join puts spaces between elements
join::puts::spaces::between::elements
Hello
['a', 'b', 'c', 'd']
['v', 'i', 't', 'o', 'r']
['a', 'b c d']
['a', 'b', 'c d']
this-is-a-test
hello, world! 
 hello, world!
hello, world!
.python.org
www.python.
python
v-i-t-o-r
"""

# ord()函数获取字符的整数表示，chr()函数把编码转换为对应的字符
print(ord("A"))
print(chr(65))

```

## 第二部分 列表

```python
temp_lists = ['a', 'b', 13]

# 列表长度
length = len(temp_lists)
print(length)

# 尾部插入
temp_lists.append(14)
print(temp_lists)

# 插入
temp_lists.insert(0, 15)
print(temp_lists)

# 修改
temp_lists[0] = 'aa'
print(temp_lists)

# pop() 和del都会将列表中的数据删除
# 如果删除了后不用了，用del
# 如果删除了后还要用，用pop（）
# 删除
del temp_lists[0]
print(temp_lists)

# 删除末尾的元素
temp_lists.pop()
print(temp_lists)

# 删除指定位置的元素
temp_lists.pop(2)
print(temp_lists)

# 按值删除
temp_lists.remove('a')
print(temp_lists)
print(len(temp_lists))

# 创建列表
numbers = list(range(1, 6))
print(numbers)

# range步长
even_numbers = list(range(2, 11, 2))
print(even_numbers)
print(min(even_numbers))
print(max(even_numbers))
print(sum(even_numbers))

squares = []
for value in range(1, 10):
    squares.append(value ** 2)
print(squares)

# 推导式
squares_tmp1 = [value for value in range(1, 10)]	# [1, 2, 3, 4, 5, 6, 7, 8, 9]
squares_tmp2 = [value for value in range(3)] # [0, 1, 2]

# 复制列表
private_squares = squares[:]
print(private_squares)

# 复制列表，慎用
x = [1, 2, 3, 4]
# y = x引用的是同一个对象
# y = x
# print(id(x))
# print(id(y))
# 切片赋值
x[len(x):] = [5, 6, 7]
print(x)
x[:0] = [-1, 0]
print(x)
x[1:-1] = []
print(x)

# 排序
# sorted不改变原有列表顺序
list_tmp = [[1, 2, 3], [2, 1, 3], [4, 0, 1]]

def mid_sort(lists):
    return lists[len(lists) // 2]

list_tmp_sorted = sorted(list_tmp, key=mid_sort)
print(list_tmp)
print(list_tmp_sorted)

list_tmp_sorted = sorted(list_tmp, key=mid_sort, reverse=True)
print(list_tmp)
print(list_tmp_sorted)

# list.sort改变了列表顺序
list_tmp.sort(key=mid_sort)
print(list_tmp)

list_tmp.sort(key=mid_sort, reverse=True)
print(list_tmp)

# 列表常用的三个函数
aaa = [1, 2, 3] + [4, 5]
print(aaa)

print(max(aaa))
print(min(aaa))
print(sum(aaa))

# 某个元素是否在列表中
if 6 in aaa:
    print(aaa.index(6))
else:
    print('6 is not in list')

# 某个元素在列表中出现的次数 
bbb = [1, 1, 2, 2, 2, 3, 3, 3, 3, 4, 4, 4, 4, 4, 5]
print(bbb.count(3))
print(bbb)

# 多元列表
xxx = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
# 浅复制
yyy = xxx[:]
yyy[0][0] = 0
print(xxx)
print(yyy)

# 深复制
zzz = copy.deepcopy(xxx)
zzz[0][0] = 100
print(xxx)
print(zzz)

```

## 第三部分 元组

```python
tuple_x = (1, 2, 3, 4)
print(tuple_x)
# 元组数据不可变，所以下列方法执行会报错的
# tuple_x.append(1)
# tuple_x[1] = 'hello'
# del tuple_x[2]
tuple_y = (3, 1, 4, 2)
print(tuple_y)
print("=====")
tuple_y = tuple(sorted(tuple_y))
print(tuple_y)

somelist = [(1, 2), (3, 7), (9, 5)]
result = 0

for t in somelist:
    result += t[0] * t[1]
print(result)

# 元组自动拆包
for x, y in somelist:
    result += x * y
print(result)

# enumerate不但能返回值，还能返回对应的索引
x = [1, 3, -7, 4, 9, -5, 4]
for i, n in enumerate(x):
    if n < 0:
        print(n, "position is => ", i)

xx = [1, 2, 3, 4]
yy = ['a', 'b', 'c']
zz = zip(xx, yy)
print(list(zz))

# 运行结果
"""
68
136
-7 position is =>  2
-5 position is =>  5
[(1, 'a'), (2, 'b'), (3, 'c')]
"""

```

## 第四部分 字典

```python
alien_0 = {
    'color': 'green',
    'points': 5
}

print(alien_0['color'])
print(alien_0['points'])

# 新增键值
alien_0['x_position'] = 0
alien_0['y_position'] = 25
print(alien_0)

# 修改
alien_0['color'] = 'yellow'
print(alien_0)

# 删除
del(alien_0['points'])
print(alien_0)

# 统计字符串中单词的个数
sample_string = "To be or not to be"
occurrences = {}

for word in sample_string.split():
    occurrences[word] = occurrences.get(word, 0) + 1
print(occurrences)

for word in occurrences:
    print("The word", word, "occurs", occurrences[word], "times in the string")

# 访问字典
dict_1 = {
    'a': 1,
    'b': 2,
    'c': 3
}

print(dict_1['a'])
print(dict_1.keys())
print(dict_1.values())
print(dict_1.items())

# get判断key是否存在，如果不存在返回后面内容
alien_0 = {
    'color': 'green',
    'points': 5
}

speed_value = alien_0.get('speed', "No speed value assigned.")
print(speed_value)

# 遍历字典
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python'
}
for name, language in favorite_languages.items():
    print(f"{name.title()}'s favorite language is {language}")

for name in favorite_languages.keys():
    print(f"\t{name.title()}")

friends = ['phil', 'sarah']

for name in favorite_languages.keys():
    print(f"\tHi {name.title()}")
    if name in friends:
        language = favorite_languages[name].title()
        print(f"\t{name.title()}, I see you love {language.title()}")

if 'erin' not in favorite_languages.keys():
    print("Erin, please take our poll!")

# sorted排序并且不改变原有顺序
for name in sorted(favorite_languages.keys()):
    print(f"\t{name.title()}, thank you for taking the poll!")

for language in favorite_languages.values():
    print(language.title())

# set去重
for language in set(favorite_languages.values()):
    print(f"\t{language.title()}")

# 字典中存储列表
pizza = {
    'crust': 'thick',
    'toppings': ['mushroom', 'extra cheese']
}

print(f"You ordered a {pizza['crust']} - crust pizza "
      "with the following toppings:")
for topping in pizza['toppings']:
    print("\t" + topping)

favorite_languages = {
    'jen': ['python', 'ruby'],
    'sarah': 'c',
    'edward': ['go', 'ruby'],
    'phil': ['python', 'haskell']
    }

for name, languages in favorite_languages.items():
    if len(languages) == 1:
        print(f"\n{name.title()}'s favorite languages is:")
    else:
        print(f"\n{name.title()}'s favorite languages are:")
    for language in languages:
        print(f"\t{language.title()}")

# 列表中存储字典
alien_0 = {
    'color': 'green',
    'points': 5
}
alien_1 = {
    'color': 'yellow',
    'points': 10
}
alien_2 = {
    'color': 'red',
    'points': 15
}

aliens = [alien_0, alien_1, alien_2]

for alien in aliens:
    print(alien)

# 字典中存储字典
users = {
    'aeinstein': {
        'first': 'albert',
        'last': 'einstein',
        'location': 'princeton'
    },
    'mcurie': {
        'first': 'marie',
        'last': 'cuire',
        'location': 'paris'
    }
}

for username, userinfo in users.items():
    print(f"\nUsername: {username}")
    full_name = f"{userinfo['first']} {userinfo['last']}"
    location = userinfo['location']
    print(f"\tFullname: {full_name.title()}")
    print(f"\tLocation: {location.title()}")

```

## 第五部分 推导式及生成器

```python
# 推导式
x = [1, 2, 3, 4]

x_squared_1 = [item * item for item in x]
print(x_squared_1)

x_squared_2 = [item * item for item in x if item > 2]
print(x_squared_2)

x_squared_dict = {item: item * item for item in x}
print(x_squared_dict)

# 交换key和value
alien_0 = {
    'color': 'green',
    'points': 5
}

alien_tmp = {m: n for n, m in alien_1.items()}
print(alien_tmp)

# 生成器
x_squared_generator = (item * item for item in x)
print("---------------")
print(x_squared_generator)
for i in x_squared_generator:
    print(i)

xx = [1, 0, -1, 2, -3, 4]
print(xx)
xx = [item for item in xx if item > 0]
print(xx)

xxx = [item for item in range(1, 101) if item % 2 == 1]
print(xxx)

yyy = {item: item ** 3 for item in range(12, 15)}
print(yyy)

# 运行结果
"""
[1, 4, 9, 16]
[9, 16]
{1: 1, 2: 4, 3: 9, 4: 16}
{'green': 'color', 5: 'points'}
---------------
<generator object <genexpr> at 0x000000000A0184A0>
1
4
9
16
[1, 0, -1, 2, -3, 4]
[1, 2, 4]
[1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29, 31, 33, 35, 37, 39, 41, 43, 45, 47, 49, 51, 53, 55, 57, 59, 61, 63, 65, 67, 69, 71, 73, 75, 77, 79, 81, 83, 85, 87, 89, 91, 93, 95, 97, 99]
{12: 1728, 13: 2197, 14: 2744}
"""

```

## 第六部分 集合

```python
# set去重
x = set([1, 2, 3, 1, 3, 5])
print(x)

# 新增
x.add(6)
print(x)

# 删除
x.remove(5)
print(x)

# 是否存在
print(3 in x)
print(9 in x)

# 关系运算
y = set([1, 7, 8, 9])
print(x | y)	# 并集
print(x & y)	# 交集
print(x ^ y)	# 异或

# 不可变集合frozenset
xx = set([1, 2, 3, 1, 3, 5])
print(xx)
zz = frozenset(xx)
print(zz)
xx.add(zz)
print(xx)

xxx = set([1, 2, 5, 1, 0, 2, 3, 1, 1, (1, 2, 3)])
print(xxx)

# 运行结果
"""
{1, 2, 3, 5}
{1, 2, 3, 5, 6}
{1, 2, 3, 6}
True
False
{1, 2, 3, 6, 7, 8, 9}
{1}
{2, 3, 6, 7, 8, 9}
{1, 2, 3, 5}
frozenset({1, 2, 3, 5})
{1, 2, 3, 5, frozenset({1, 2, 3, 5})}
{0, 1, 2, 3, 5, (1, 2, 3)}
"""

```

## 第七部分 函数

```python
"""
要注意定义可变参数和关键字参数的语法：
*args是可变参数，args接收的是一个tuple；
**kw是关键字参数，kw接收的是一个dict。
以及调用函数时如何传入可变参数和关键字参数的语法：
可变参数既可以直接传入：func(1, 2, 3)，又可以先组装list或tuple，再通过*args传入：func(*(1, 2, 3))；
关键字参数既可以直接传入：func(a=1, b=2)，又可以先组装dict，再通过**kw传入：func(**{'a': 1, 'b': 2})。
使用*args和**kw是Python的习惯写法，当然也可以用其他参数名，但最好使用习惯用法。
命名的关键字参数是为了限制调用者可以传入的参数名，同时可以提供默认值。
定义命名的关键字参数在没有可变参数的情况下不要忘了写分隔符*，否则定义的将是位置参数

参数组合
Python中定义函数，可以用必选参数、默认参数、可变参数、关键字参数和命名关键字参数，这5种参数都可以组合使用。
但是请注意，参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数。
"""
# 位置参数
def power_1(x, y):
    r = 1
    while y > 0:
        r = r * x
        y = y - 1
    return r

# 有默认值
def power_2(x, y=2):
    r = 1
    while y > 0:
        r = r * x
        y = y - 1
    return r

print(power_1(3, 3))
print(power_2(3, 3))
print(power_2(3))

# 收集不定的位置参数
def maximum(*numbers):
    if len(numbers) == 0:
        return None
    else:
        maxnum = numbers[0]
        for n in numbers[1:]:
            if n > maxnum:
                maxnum = n
    return maxnum

print(maximum(2, 3, 8, 10))

# 收集不定的关键字参数
def example_fun(x, y, **other):
    print("x:{0}, y:{1}, keys in 'other':{2}".format(x, y, list(other.keys())))
    other_total = 0
    for k in other.keys():
        other_total += other[k]
    print("The total of values in 'other' is {0}".format(other_total))

example_fun(1, 2, a=3, b=4, c=5, d=6)


def f(n, list1, list2):
    list1.append(3)
    list2 = [4, 5, 6]

x = 5
y = [1, 2]
z = [4, 5]
f(x, y, z)
print(x)
print(y)
print(z)

# 装饰器，用函数作为了参数传入，用@关键字
def decorate(func):
    print("in decorate function, decorating", func.__name__)

    def wrapper_func(*args):
        print("Executing", func.__name__)
        return func(*args)

    return wrapper_func

@decorate
def my_function(parameter):
    print(parameter)

my_function("hello")

# 运行结果
"""
27
27
9
10
x:1, y:2, keys in 'other':['a', 'b', 'c', 'd']
The total of values in 'other' is 18
5
[1, 2, 3]
[4, 5]
in decorate function, decorating my_function
Executing my_function
hello
"""

# 递归函数
def fact(n):
    if n == 1:
        return 1
    return n * fact(n-1)

m = fact(5)
print(m)

# 汉诺塔
def move(n, a, b, c):
    if n == 1:
        print('move', a, '-->', c)  # 直接搬过去
    else:
        move(n-1, a, c, b)          # 先把a上面的n-1个盘子搬到b
        move(1, a, b, c)            # 然后把最后1个盘子搬到c
        move(n-1, b, a, c)          # 最后再把b上的n-1个盘子搬到c
        
move(4, 'A', 'B', 'C')

# filter函数
def is_odd(n):
    return n % 2 == 1

l = filter(is_odd,[1,2,3,4,5,6,7,8,9])
for i in l:
    print(i)
    
# map函数
def f(x):
    return x * x

r = map(f,[1,2,3,4,5,6,7,8,9])
lr = list(r)
print(lr)

# reduce函数
# reduce把一个函数作用在一个序列[x1, x2, x3, ...]上，
# 这个函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积计算，其效果就是：
# reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)

from functools import reduce

def add(x,y):
    return x + y
sum0 = reduce(add,[1,2,3,4,5,6])
print(sum)

# 但是如果要把序列[1, 3, 5, 7, 9]变换成整数13579，reduce就可以派上用场

def fn(x,y):
    return 10 * x + y
mul = reduce(fn,[1,3,5,7,9])
print(mul)

# 这个例子本身没多大用处，但是，如果考虑到字符串str也是一个序列，
# 对上面的例子稍加改动，配合map()，我们就可以写出把str转换为int的函数

def char2num(s):
    digits = {'0':0,'1':1,'2':2,'3':3,'4':4,'5':5,'6':6,'7':7,'8':8,'9':9}
    return digits[s]
char2 = reduce(fn,map(char2num,'13579'))
print(char2)

# 整理成一个str2int的函数就是

DIGITS = {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}

def str2int(s):
    def fn(x, y):
        return x * 10 + y
    def char2num(s):
        return DIGITS[s]
    return reduce(fn, map(char2num, s))
char3 = str2int('13579')
print(char3)

# 还可以用lambda函数进一步简化成
DIGITS = {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}

def char2num(s):
    return DIGITS[s]

def str2int(s):
    return reduce(lambda x, y: x * 10 + y, map(char2num, s))
char4 = str2int('13579')
print(char4)

# 也就是说，假设Python没有提供int()函数，你完全可以自己写一个把字符串转化为整数的函数，而且只需要几行代码！

# lambda表达式
def f(x):
    return x * x
l1 = list(map(f, [1, 2, 3, 4, 5, 6, 7]))
print(l1)

l2 = list(map(lambda x: x * x, [1, 2, 3, 4, 5, 6, 7]))
print(l2)
# 匿名函数lambda x: x * x实际上就是：f(x)
# 关键字lambda表示匿名函数，冒号前面的x表示函数参数。
# 匿名函数有个限制，就是只能有一个表达式，不用写return，返回值就是该表达式的结果。
# 用匿名函数有个好处，因为函数没有名字，不必担心函数名冲突。
# 此外，匿名函数也是一个函数对象，也可以把匿名函数赋值给一个变量，再利用变量来调用该函
f = lambda x: x * x
print(f(5))

# 同样，也可以把匿名函数作为返回值返回，比如：
def build(x,y):
    return lambda:x * x + y * y

```

## 第八部分 面向对象

```python
class Circle:
    all_circles = []
    all_circles_c = []
    # 类变量
    pi = 3.14159

    def __init__(self, r=1):
        self.radius = r
        self.__class__.all_circles.append(self)
        self.__class__.all_circles_c.append(self)

    def area(self):
        return self.__class__.pi * self.radius ** 2

    def circumference(self):
        return self.__class__.pi * self.radius * 2

    @staticmethod
    def total_area():
        total = 0
        for c in Circle.all_circles:
            total += c.area()
        return total

    @classmethod
    def total_c(cls):
        total = 0
        for c in cls.all_circles_c:
            total += c.circumference()
        return total


class Rectangle:
    def __init__(self, length=4, width=2):
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width


if __name__ == '__main__':
    # # 静态方法
    # c1 = Circle(1)
    # c2 = Circle(2)
    # c3 = Circle(3)
    # print("静态方法的结果")
    # print(Circle.total_area())

    # 类方法
    c1 = Circle(1)
    c2 = Circle(2)
    c3 = Circle(3)
    print("类方法的结果")
    print(Circle.total_c())

    # 类变量不依赖与实例
    print(Circle.pi)
    Circle.pi = 4
    print(Circle.pi)
    c = Circle()

    s1 = c.area()
    print(s1)
    c.radius = 3
    s2 = c.area()
    print(s2)

    c2 = Circle(4)
    s3 = c2.area()
    print(s3)

    # 类实例字段不需要提前声明，可以在运行时创建
    c.tmp_radius = 2
    print(2 * 3.14 * c.tmp_radius)

    r1 = Rectangle()
    rs1 = r1.area()
    print(rs1)

# 运行结果
"""
# 静态方法的结果
# 43.98226
类方法的结果
37.699079999999995
3.14159
4
4
36
64
12.56
8   
"""

class Temperature:
    # 变量前面两个下划线，表示私有变量
    def __init__(self):
        self.__temp_fahr = 0
        
    @property
    def temp(self):
        return (self.__temp_fahr - 32) * 5 / 9

    @temp.setter
    def temp(self, new_temp):
        self.__temp_fahr = new_temp * 9 / 5 + 32


if __name__ == '__main__':
    t = Temperature()
    print(t.temp)

    t.temp = 34
    print(t.temp)

# 运行结果
"""
-17.77777777777778
34.0
"""

class Car:
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0

    def get_descriptive_name(self):
        long_name = f"{self.year} {self.make} {self.model}"
        return long_name.title()

    def read_odometer(self):
        print(f"This car has {self.odometer_reading} miles on it.")

    def update_odometer(self, mileage):
        if mileage >= self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back odometer!")

    def increment_odometer(self, miles):
        if miles >= 0:
            self.odometer_reading += miles
        else:
            print("You can't roll back odometer!")

    def fill_gas_tank(self):
        print("This car have a gas tank!")


class ElectricCar(Car):
    def __init__(self, make, model, year):
        # 继承父类属性
        super().__init__(make, model, year)
        # 自己的属性
        self.battery_size = 75

    # 子类自己的方法
    def describe_battery(self):
        print(f"This car has a {self.battery_size}-kWh battery.")

    # 子类重写父类方法
    def fill_gas_tank(self):
        print("ElectricCar doesn't need a gas tank!")


my_tesla = ElectricCar('tesla', 'model s', 2019)
print(my_tesla.get_descriptive_name())
my_tesla.describe_battery()
my_tesla.fill_gas_tank()

# 运行结果
"""
2019 Tesla Model S
This car has a 75-kWh battery.
ElectricCar doesn't need a gas tank!
"""

```

## 第九部分 文件处理

```python
# 文本文件
pi_digits.txt
3.1415926535 
  8979323846 
  2643383279
# read file
with open('pi_digits.txt') as file_object:
    contents = file_object.read()

print(contents)
print(contents.rstrip())

filename = 'pi_digits.txt'
with open(filename) as file_object:
    for line in file_object:
        print(line.rstrip())
        # print(line)

with open(filename) as file_object:
    lines = file_object.readlines()
for line in lines:
    print(line.rstrip())

pi_string = ''
for line in lines:
    pi_string += line.strip()
print(pi_string)
print(len(pi_string))

# 运行结果
"""
3.1415926535 
  8979323846 
  2643383279

3.1415926535 
  8979323846 
  2643383279
3.1415926535
  8979323846
  2643383279
3.1415926535
  8979323846
  2643383279
3.141592653589793238462643383279
32
"""

# write file

filename = "programming.txt"

# 每次都覆盖之前的内容
with open(filename, 'w') as file_object:
    # 要让输入的内容，一行一行的写入，需要加上换行符 \n
    file_object.write("I love programming. \n")
    file_object.write("I love creating new games. \n")

# 在文件之后追加内容
with open(filename, 'a') as file_object:
    file_object.write("I also love finding meaning in large datasets. \n")
    file_object.write("I love creating apps that can run in a browser. \n")

# json文件
numbers.json
[2, 3, 5, 7, 11, 13]

# read json
import json

filename = 'numbers.json'
with open(filename) as f:
    numbers = json.load(f)
print(numbers)

# write json
import json

numbers = [2, 3, 5, 7, 11, 13]
filename = 'numbers.json'
with open(filename, 'w') as f: 
    json.dump(numbers, f)

# excel文件 xlrd，xlwt
import xlrd
import xlwt

# 利用xlrd和xlwt进行excel读写（xlwt不支持xlsx）
book = xlrd.open_workbook('data_xlrd.xls')
# sheet1 = book.sheets()[0]
# sheet1 = book.sheet_by_index(0)
sheet1 = book.sheet_by_name('Sheet1')

# 返回行数
n_rows = sheet1.nrows
print(n_rows)

# 返回列数
n_cols = sheet1.ncols
print(n_cols)

# 返回第三行数据
row3_values = sheet1.row_values(2)
print(row3_values)

# 返回第三列数据
col3_values = sheet1.col_values(2)
print(col3_values)

# 返回第三行，第三列的数据
cell_3_3 = sheet1.cell(2, 2).value
print(cell_3_3)

# 写入数据到excel——write.xls表格中去
work_book = xlwt.Workbook()
work_sheet = work_book.add_sheet('test')
work_sheet.write(0, 0, 'A1data')
work_book.save('excel_write.xls')

# excel openpyxl
import openpyxl

# 利用openpyxl读写excel，注意这里只能是xlsx类型的excel
work_book = openpyxl.load_workbook('data_openpyxl.xlsx')
work_sheet = work_book.get_sheet_by_name('Sheet1')
row3 = [item.value for item in list(work_sheet.rows)[2]]
print(row3)

col3 = [item.value for item in list(work_sheet.columns)[2]]
print(col3)

cell_2_3 = work_sheet.cell(row=2, column=3).value
print(cell_2_3)

max_row = work_sheet.max_row
print(max_row)

# 写入内容进入new.xlsx中
work_book_write = openpyxl.Workbook()
write_sheet = work_book_write.active
write_sheet['A1'] = 'hi,wwu'
work_book_write.save('new.xlsx')

# excel pandas

import pandas as pd
from pandas import DataFrame

# pandas是一个数据处理的包，本身提供了许多读取文件的函数，像read_csv（读取csv文件），
# read_excel（读取excel文件）等，只需一行代码就能实现文件的读取
df = pd.read_excel(r'name_data.xls', sheet_name=0)
# df = pd.read_excel(r'name_data.xls', sheet_name='Sheet1')
print(type(df.head))
print(df.head())

# 写入数据
data = {
   'name': ['张三', '李四', '王五'],
   'age': [11, 12, 13],
   'sex': ['男', '女', '男']
}
df = DataFrame(data)
df.to_excel('new1.xlsx')

```

## 第十部分 异常

```python
# try ... except ...
try:
    print(5/0)
except ZeroDivisionError:
    print("You can't divide by Zero!")

print("Give me two numbers, and I'll divide them.")
print("Enter 'q' to quit.")

while True:
    first_number = input("\nFirst number: ")
    if first_number == 'q':
        break
    second_number = input("\nSecond number: ")
    if second_number == 'q':
        break
    try:
        answer = int(first_number) / int(second_number)
    except ZeroDivisionError:
        print("You can't divide by Zero!")
        
# try ... except ... else ...

filename = "alice.txt"
try:
    with open(filename, encoding="utf-8") as f:
        contents = f.read()
except FileNotFoundError:
    print(f"Sorry,the file {filename} does not exist. ")
else:
    words = contents.split()
    num_words = len(words)
    print(f"The file {filename} has about {num_words} words. ")

# 综合运用
def count_word(filename):
    try:
        with open(filename, encoding="utf-8") as f:
            contents = f.read()
    except FileNotFoundError:
        # print(f"Sorry,the file {filename} does not exist. ")
        with open('missing_files.txt', 'a', encoding='utf-8') as f:
            f.write(filename)
    else:
        words = contents.split()
        num_words = len(words)
        print(f"The file {filename} has about {num_words} words. ")


filename = 'alice.txt'
count_word(filename)

filenames = ['alice.txt', 'siddhartha1.txt', 'moby_dick.txt', 'little_women.txt']
for filename in filenames:
    count_word(filename)

```

## 第十一部分 连接数据库

```python
#########
# db_config.py
# db 数据库配置信息
def db_base_info(env, db):
    db_info = {
        # fat1 数据库连接信息
        'fat1': {
            'host': '172.16.4.11',
            'port': 3306,
            'user': 'wuchangzheng',
            'passwd': 'JnbbSQj4kW6fLFDfZxlg',
            'db': db,
            'charset': 'utf8'
        },
        # game1 数据库连接信息
        'game1': {
            'host': '172.16.4.81',
            'port': 3306,
            'user': 'wuchangzheng',
            'passwd': 'JnbbSQj4kW6fLFDfZxlg',
            'db': db,
            'charset': 'utf8'
        },
        # pre 数据库连接信息
        'pre': {
            'host': '172.16.4.41',
            'port': 3306,
            'user': 'test',
            'passwd': 'JnbbSQj4kW6fLFDfZxlg',
            'db': db,
            'charset': 'utf8'
        }
    }
    return db_info[env]


def get_lottery_info():
    sport_lottery_db = db_base_info(env_config.env, 'sport-lottery')
    return sport_lottery_db


def get_data_info():
    sport_data_db = db_base_info(env_config.env, 'sport-data')
    return sport_data_db


def get_platform_info():
    platform_db = db_base_info(env_config.env, 'db_platform')
    return platform_db


def get_score_info():
    score_db = db_base_info(env_config.env, 'sport_score')
    return score_db

#########
# db_core.py
import pymysql
from common.config import db_config


class DatabaseRepository(object):

    def __init__(self, conn_info):
        self.conn_info = conn_info

    # 连接数据库
    def get_db_connect(self):
        connections = pymysql.connect(**self.conn_info)
        return connections

    # 增删改数据
    def modify_execute(self, sql):
        connection = self.get_db_connect()
        cursor = connection.cursor()
        print(sql)
        cursor.execute(sql)
        connection.commit()
        print(f"Affected rows: {cursor.rowcount}")
        cursor.close()
        connection.close()

    # 批量增删改
    def modify_execute_list(self, sqls):
        connection = self.get_db_connect()
        cursor = connection.cursor()
        for sql in sqls:
            cursor.execute(sql)
            connection.commit()
            print(f"Affected rows: {cursor.rowcount}")
        cursor.close()
        connection.close()

    # 查询数据
    def query_execute(self, sql, *params):
        connection = self.get_db_connect()
        cursor = connection.cursor()
        cursor.execute(sql, [*params])
        result = cursor.fetchall()
        cursor.close()
        connection.close()
        return result


def get_lottery_db():
    return DatabaseRepository(db_config.get_lottery_info())

#########
# data.py
from common.data.query_core import db_base


# 根据match_id查询指定赛事的信息
def query_match_info_by_id(match_id):
    sql_query = "select * from sport_match_info where id = %s"
    query_result = db_base.get_lottery_db().query_execute(sql_query, match_id)
    return query_result


# 根据category_id获取类别信息
def query_category_info_by_id(category_id):
    sql_query = "select * from sport_category_info where id = %s"
    query_result = db_base.get_lottery_db().query_execute(sql_query, category_id)
    return query_result


# 根据league_id获取联赛基础信息
def query_league_info_by_league_id(league_id):
    sql_query = "select * from sport_league_info where id = %s"
    query_result = db_base.get_lottery_db().query_execute(sql_query, league_id)
    return query_result


# 某个类别下的联赛数据
def query_league_info_by_category_id(category_id):
    sql = ("select * from sport_league_info "
           "where category_id = %s and available=0")
    league_ids = db_base.get_lottery_db().query_execute(sql, category_id)
    return league_ids

#########
# data_api.py
import json

from common.data import sport_data_sql
from common.utils import std_out


# 返回赛事相关信息
def get_match_info_by_id(match_id, info):
    match_info = sport_data_sql.query_match_info_by_id(match_id)
    if info == 'fixture_id':
        fixtureId = std_out.format_sql_result(match_info, [10])
        return fixtureId[0]
    elif info == 'category_id':
        category_id = std_out.format_sql_result(match_info, [1])
        return category_id[0]
    elif info == 'league_id':
        league_id = std_out.format_sql_result(match_info, [2])
        return league_id[0]
    elif info == 'match_time':
        match_time = std_out.format_sql_result(match_info, [11])
        return str(match_time[0])
    elif info == 'team_id':
        team_ids_result = std_out.format_sql_result(match_info, [7, 8])
        team_ids = team_ids_result[0]
        return team_ids
    else:
        print("get_match_info_by_id Wrong")


# 返回category_code
def get_category_info_by_id(match_id, info):
    category_id = get_match_info_by_id(match_id, 'category_id')
    category_info = sport_data_sql.query_category_info_by_id(category_id)
    if info == 'category_code':
        category_code = std_out.format_sql_result(category_info, [2])
        return category_code[0]
    elif info == 'source_category_id':
        source_category_id = std_out.format_sql_result(category_info, [4])
        return source_category_id[0]
    else:
        print("get_category_info_by_id Wrong")


# 根据league_id获取联赛的源id
def get_league_source_id_by_id(match_id):
    league_id = get_match_info_by_id(match_id, 'league_id')
    league_info = sport_data_sql.query_league_info_by_league_id(league_id)
    source_league_id = std_out.format_sql_result(league_info, [6])
    return source_league_id[0]

#########
# util.py
# 处理sql查询的结果，放到列表中
import decimal


# 将sql结果转换为列表
def format_sql_result(sql_results, element_poses):
    final_result = []
    if len(element_poses) == 1:
        for sql_result in sql_results:
            element = sql_result[element_poses[0]]
            final_result.append(element)
    elif len(element_poses) > 1:
        for sql_result in sql_results:
            elements = []
            for element_pos in element_poses:
                element = sql_result[element_pos]
                elements.append(element)
            final_result.append(elements)
    else:
        print("Wrong")
    return final_result


# 将decimal.Decimal数据类型的值，转换为字符
def format_decimal(sql_result):
    rep = []
    for row in sql_result:
        if type(row) is list:
            list_x = []
            for data in row:
                if data is None:
                    list_x.append(' ')
                elif type(data) is decimal.Decimal:
                    list_x.append(float(str(data.quantize(decimal.Decimal('0.000')))))
                else:
                    list_x.append(data)
            rep.append(list_x)
        else:
            rep.append(float(str(row.quantize(decimal.Decimal('0.000')))))
    return rep


# 指定浮点数保留的小数点位数，默认为小数点后12位
def format_float(float_num, length=12):
    format_num = str(float_num).split('.')[0] + '.' + str(float_num).split('.')[1][:length]
    return float(format_num)


# 格式化输出
def format_output(some_list):
    for i in range(len(some_list)):
        print(some_list[i], end=' | ')
        if(i+1) % 10 == 0:
            print("\n")
    print("\n")
    print("=====================================")
```





















