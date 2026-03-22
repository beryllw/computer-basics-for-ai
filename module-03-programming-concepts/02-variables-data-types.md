# 3.2 变量与数据类型

> 理解程序如何存储和处理数据

---

## 🎯 学习目标

学完本课后，你将能够：

- [ ] 理解变量的概念和用途
- [ ] 识别 Python 中的基本数据类型
- [ ] 进行简单的数据类型转换
- [ ] 读懂涉及变量和数据的代码

---

## 💭 从一个问题开始

**程序如何"记住"信息？**

就像做菜需要记住食材的数量，程序也需要记住各种信息：
- 用户的名字
- 购物车里的商品
- 游戏的得分

**变量**就是程序的"记忆盒子"。

---

## 💡 核心概念

### 什么是变量？

> **变量 = 带标签的盒子，用来存储数据**

```
     ┌─────────────┐
name │   "Alice"   │  ← 盒子里的值
     └─────────────┘
       ↑
     标签名
```

**关键点**：
- 变量有**名字**（标签）
- 变量有**值**（盒子里的东西）
- 变量的值可以**改变**

### Python 中的变量

```python
# 创建变量（赋值）
name = "Alice"
age = 25
height = 1.65
is_student = False

# 使用变量
print(name)  # 输出：Alice

# 改变变量的值
age = 26  # 年龄增长了
```

**语法**：`变量名 = 值`
- `=` 是赋值符号（不是数学的"等于"）
- 读作"把右边的值赋给左边的变量"

---

## 📊 数据类型

### 为什么需要数据类型？

计算机需要知道数据的"种类"，因为：
- 不同种类的数据，操作方式不同
- `2 + 3 = 5`（数字相加）
- `"2" + "3" = "23"`（字符串拼接）

### Python 的基本数据类型

| 类型 | 名称 | 例子 | 用途 |
|------|------|------|------|
| `int` | 整数 | `42`, `-5`, `0` | 计数、编号 |
| `float` | 浮点数 | `3.14`, `-0.5` | 小数、精度 |
| `str` | 字符串 | `"Hello"`, `'你好'` | 文本 |
| `bool` | 布尔值 | `True`, `False` | 真假判断 |

### 检查数据类型

```python
type(42)      # <class 'int'>
type(3.14)    # <class 'float'>
type("Hi")    # <class 'str'>
type(True)    # <class 'bool'>

# 检查变量的类型
age = 25
type(age)     # <class 'int'>
```

---

## 🔍 深入理解

### 整数 vs 浮点数

```python
# 整数 (int)
count = 100
negative = -5
zero = 0

# 浮点数 (float)
price = 19.99
pi = 3.14159
temperature = -3.5

# 注意：整数运算结果还是整数
10 / 3   # 3.333... (Python 3 中除法返回浮点数)
10 // 3  # 3 (整除，返回整数)
10 % 3   # 1 (取余数)
```

### 字符串详解

```python
# 创建字符串
name = "Alice"
greeting = 'Hello'  # 单引号也可以

# 多行字符串
text = """这是
多行
文本"""

# 字符串操作
first_name = "John"
last_name = "Doe"
full_name = first_name + " " + last_name  # "John Doe"

# 字符串方法
name.upper()    # "ALICE"
name.lower()    # "alice"
len(name)       # 5 (字符串长度)

# f-string 格式化（很常用！）
name = "Alice"
age = 25
message = f"My name is {name} and I am {age} years old"
```

### 布尔值详解

```python
# 布尔值只有两个
is_raining = True
is_sunny = False

# 通常来自比较
x = 10
x > 5      # True
x < 5      # False
x == 10    # True (注意：== 是比较，= 是赋值)
x != 10    # False (!= 表示"不等于")

# 布尔运算
True and False   # False (与)
True or False    # True (或)
not True         # False (非)
```

---

## 🔄 类型转换

### 为什么需要转换？

```python
# 常见场景：用户输入是字符串
age_str = "25"
# 想做数学运算？需要转成整数
age = int(age_str)  # 25

# 或者要把数字显示给人看
price = 19.99
message = "Price: $" + str(price)  # "Price: $19.99"
```

### 类型转换函数

```python
# 转成整数
int("25")       # 25
int(3.14)       # 3 (截断，不是四舍五入)

# 转成浮点数
float("3.14")   # 3.14
float(5)        # 5.0

# 转成字符串
str(42)         # "42"
str(3.14)       # "3.14"
str(True)       # "True"

# 转成布尔值
bool(1)         # True
bool(0)         # False
bool("")        # False (空字符串)
bool("Hi")      # True
```

### 常见错误

```python
# 错误：不能转成数字
int("hello")    # ValueError!

# 错误：混淆赋值和比较
x = 5           # 赋值（正确）
x == 5          # 比较（返回 True 或 False）
x = 5 == 6      # x 变成 False！(容易出错)
```

---

## 🧪 代码示例

### 示例 1：个人信息卡片

```python
# 变量和数据类型综合示例

# 定义变量
name = "Alice"
age = 25
height = 1.65
is_student = True
hobbies = ["reading", "coding", "hiking"]

# 使用变量
print(f"Name: {name}")
print(f"Age: {age}")
print(f"Height: {height}m")
print(f"Is student: {is_student}")
print(f"Hobbies: {', '.join(hobbies)}")

# 类型转换示例
next_age = age + 1
print(f"Next year, {name} will be {next_age}")
```

### 示例 2：简单计算器

```python
# 简单计算器

# 定义数字
a = 10
b = 3

# 各种运算
print(f"Addition: {a} + {b} = {a + b}")
print(f"Subtraction: {a} - {b} = {a - b}")
print(f"Multiplication: {a} * {b} = {a * b}")
print(f"Division: {a} / {b} = {a / b}")
print(f"Integer division: {a} // {b} = {a // b}")
print(f"Remainder: {a} % {b} = {a % b}")
print(f"Power: {a} ** {b} = {a ** b}")
```

### 示例 3：用户输入处理

```python
# 模拟用户输入（实际中用 input() 函数）

# 假设用户输入
user_input = "25"

# 类型转换
age = int(user_input)

# 验证
print(f"You are {age} years old")
print(f"In 10 years, you will be {age + 10}")

# 检查类型
print(f"Type of user_input: {type(user_input)}")  # str
print(f"Type of age: {type(age)}")  # int
```

---

## 💡 实践技巧

### 变量命名规范

```python
# ✅ 好的命名
user_name = "Alice"  # 小写，下划线分隔
total_count = 100
is_valid = True

# ❌ 不好的命名
a = "Alice"          # 没有意义
UserName = "Alice"   # 不符合 Python 惯例
1st_name = "Alice"   # 不能用数字开头

# 规则：
# 1. 只能用字母、数字、下划线
# 2. 不能用数字开头
# 3. 不能用 Python 关键字（if, for, True 等）
# 4. 要有意义，让人能看懂
```

### 调试技巧

```python
# 不确定变量的值？打印出来！
x = 10
y = 20
result = x + y

print(f"DEBUG: x = {x}")
print(f"DEBUG: y = {y}")
print(f"DEBUG: result = {result}")
print(f"DEBUG: type of result = {type(result)}")
```

---

## 📝 关键术语

| 术语 | 英文 | 解释 |
|------|------|------|
| 变量 | Variable | 存储数据的命名容器 |
| 赋值 | Assignment | 给变量设置值 |
| 数据类型 | Data Type | 数据的分类 |
| 整数 | Integer | 不带小数的数字 |
| 浮点数 | Float | 带小数的数字 |
| 字符串 | String | 文本数据 |
| 布尔值 | Boolean | True 或 False |
| 类型转换 | Type Conversion | 改变数据的类型 |

---

## ✅ 本课小结

```
核心要点：

1. 变量 = 带标签的盒子，存储数据

2. Python 基本数据类型：
   - int: 整数 (42, -5)
   - float: 浮点数 (3.14, -0.5)
   - str: 字符串 ("Hello")
   - bool: 布尔值 (True, False)

3. 类型转换：
   - int() 转整数
   - float() 转浮点数
   - str() 转字符串
   - bool() 转布尔值

4. 变量命名要有意义，遵循规范

5. 用 print() 调试，查看变量值和类型
```

---

## 🧪 练习

```python
# 练习 1：创建变量存储你的信息
# - 姓名（字符串）
# - 年龄（整数）
# - 身高（浮点数）
# - 是否学生（布尔值）

# 练习 2：计算
# 给定 a = 10, b = 3
# 计算并打印：a+b, a-b, a*b, a/b, a%b

# 练习 3：类型转换
# 给定字符串 "123"
# 转成整数后加 100，结果再转回字符串
```

---

## 🤔 思考题

1. 为什么 `2 + "2"` 会出错？如何修复？
2. 变量命名为什么重要？什么样的名字是好的？
3. 在什么场景下需要进行类型转换？

> 💡 可以把你的思考告诉 AI，让它帮你深化理解

---

**下一步**: [3.3 控制流：条件与循环](./03-control-flow.md)
