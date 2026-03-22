# 3.4 函数与模块化

> 理解如何组织和复用代码

---

## 🎯 学习目标

学完本课后，你将能够：

- [ ] 理解函数的概念和用途
- [ ] 读懂带参数和返回值的函数
- [ ] 理解变量作用域
- [ ] 识别常见内置函数

---

## 💭 从一个问题开始

**为什么需要函数？**

想象你要做 100 次同样的计算：
- 每次都重新写代码？
- 还是定义一次，调用 100 次？

**函数 = 可复用的代码块**

就像：
- 食谱：写好一次，可以做多次菜
- 公式：学会一次，可以解很多题

---

## 💡 核心概念

### 什么是函数？

> **函数 = 命名的代码块，执行特定任务**

```python
# 定义函数
def greet(name):
    """向用户打招呼"""
    message = f"Hello, {name}!"
    return message

# 调用函数
result = greet("Alice")
print(result)  # 输出：Hello, Alice!
```

**组成部分**：
- `def`: 定义函数的关键字
- `greet`: 函数名
- `name`: 参数（输入）
- `return`: 返回值（输出）
- `"""..."""`: 文档字符串（说明函数用途）

### 函数的 Anatomy

```python
def function_name(parameter1, parameter2):
    """文档字符串：说明函数做什么"""
    # 函数体
    result = parameter1 + parameter2
    return result  # 返回值
```

---

## 📊 参数与返回值

### 参数类型

```python
# 1. 必需参数
def add(a, b):
    return a + b

add(3, 5)  # 8

# 2. 默认参数
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

greet("Alice")           # "Hello, Alice!"
greet("Alice", "Hi")     # "Hi, Alice!"

# 3. 多个返回值
def get_stats(numbers):
    return min(numbers), max(numbers), sum(numbers)

min_val, max_val, total = get_stats([1, 2, 3, 4, 5])
```

### 返回值

```python
# 有返回值
def square(x):
    return x * x

result = square(5)  # 25

# 没有返回值（返回 None）
def print_square(x):
    print(x * x)

result = print_square(5)  # 输出 25
print(result)  # 输出：None

# 条件返回
def absolute(x):
    if x >= 0:
        return x
    return -x  # 可以多个 return
```

---

## 🔍 深入理解

### 变量作用域

```python
# 全局变量
global_var = "I'm global"

def my_function():
    # 局部变量
    local_var = "I'm local"
    print(global_var)  # 可以访问全局变量
    print(local_var)   # 可以访问局部变量

print(global_var)  # 可以访问
# print(local_var)  # 错误！局部变量只在函数内有效

# 修改全局变量（一般不推荐）
def modify_global():
    global global_var
    global_var = "Modified"
```

**规则**：
- **局部变量**：函数内部定义，只在函数内有效
- **全局变量**：函数外定义，整个文件有效
- 优先使用局部变量

### 函数是"黑盒子"

```
       输入（参数）
          ↓
    ┌─────────────┐
    │   函数      │ ← 内部实现细节对外隐藏
    │  (黑盒子)   │
    └─────────────┘
          ↓
       输出（返回值）
```

**好处**：
- 你不需要知道内部怎么实现
- 只要知道输入什么、输出什么
- 可以独立测试和修改

---

## 🧪 常见内置函数

### 你可能已经用过的函数

```python
# 类型转换
int("25")
str(123)
float("3.14")
bool(1)

# 获取信息
len([1, 2, 3])      # 3
type("hello")       # <class 'str'>
max([1, 5, 3])      # 5
min([1, 5, 3])      # 1
sum([1, 2, 3])      # 6

# 输入输出
print("Hello")
# name = input("Enter name: ")

# 范围
range(5)            # 0, 1, 2, 3, 4
range(1, 6)         # 1, 2, 3, 4, 5
```

### 字符串方法（也是函数）

```python
text = "  Hello World  "

text.upper()        # "  HELLO WORLD  "
text.lower()        # "  hello world  "
text.strip()        # "Hello World"
text.replace("World", "Python")  # "  Hello Python  "
text.split()        # ['Hello', 'World']
text.startswith("H")  # True
text.endswith("d")    # True
```

---

## 🧪 代码示例

### 示例 1：实用工具函数

```python
# 工具函数集合

def celsius_to_fahrenheit(c):
    """摄氏度转华氏度"""
    return c * 9/5 + 32

def fahrenheit_to_celsius(f):
    """华氏度转摄氏度"""
    return (f - 32) * 5/9

def calculate_bmi(weight, height):
    """计算 BMI 指数"""
    return weight / (height ** 2)

# 使用
print(f"25°C = {celsius_to_fahrenheit(25)}°F")
print(f"BMI: {calculate_bmi(70, 1.75)}")
```

### 示例 2：数据处理函数

```python
def process_scores(scores):
    """处理成绩列表，返回统计信息"""
    if not scores:  # 空列表
        return None

    average = sum(scores) / len(scores)
    highest = max(scores)
    lowest = min(scores)

    return {
        "average": average,
        "highest": highest,
        "lowest": lowest,
        "count": len(scores)
    }

# 使用
scores = [85, 92, 78, 90, 88]
stats = process_scores(scores)
print(f"Average: {stats['average']}")
print(f"Highest: {stats['highest']}")
```

### 示例 3：验证函数

```python
def is_valid_email(email):
    """简单验证邮箱格式"""
    if "@" not in email:
        return False
    if "." not in email:
        return False
    if email.startswith("@"):
        return False
    return True

def is_adult(age):
    """检查是否成年"""
    return age >= 18

# 使用
emails = ["test@example.com", "invalid", "@no.com"]
for email in emails:
    if is_valid_email(email):
        print(f"{email} is valid")
    else:
        print(f"{email} is invalid")
```

---

## 💡 实践技巧

### 好的函数设计

```python
# ✅ 好的函数
def calculate_area(width, height):
    """计算矩形面积"""
    return width * height

# 特点：
# - 名字清晰描述功能
# - 参数少（2-3 个）
# - 做一件事
# - 有文档字符串

# ❌ 不好的函数
def calc(a, b, c=None):
    """做一些计算"""
    # ... 一堆代码
    return something

# 问题：
# - 名字不清晰
# - 参数无意义
# - 可能做太多事
```

### 函数命名规范

```python
# ✅ 好名字
def get_user_name():
    pass

def calculate_total():
    pass

def is_valid():
    pass

# ❌ 坏名字
def do_stuff():
    pass

def func1():
    pass

def my_function():
    pass
```

**规则**：
- 用动词开头（表示动作）
- 描述清楚做什么
- 用小写和下划线

### 调试函数

```python
def debug_add(a, b):
    result = a + b
    print(f"DEBUG: {a} + {b} = {result}")
    return result

# 或者用更正式的方式
def add(a, b):
    """
    Add two numbers.

    Args:
        a: First number
        b: Second number

    Returns:
        Sum of a and b
    """
    return a + b
```

---

## 📝 关键术语

| 术语 | 英文 | 解释 |
|------|------|------|
| 函数 | Function | 命名的可复用代码块 |
| 参数 | Parameter | 函数的输入 |
| 返回值 | Return Value | 函数的输出 |
| 调用 | Call | 执行函数 |
| 作用域 | Scope | 变量有效的范围 |
| 局部变量 | Local Variable | 函数内的变量 |
| 全局变量 | Global Variable | 函数外的变量 |
| 模块化 | Modularization | 用函数组织代码 |

---

## ✅ 本课小结

```
核心要点：

1. 函数 = 可复用的代码块

2. 函数结构：
   def 函数名 (参数):
       """文档字符串"""
       函数体
       return 返回值

3. 参数类型：
   - 必需参数
   - 默认参数
   - 多个返回值

4. 变量作用域：
   - 局部变量：函数内有效
   - 全局变量：整个文件有效

5. Python 有很多内置函数
   - len(), type(), print(), etc.
```

---

## 🤔 思考题

1. 为什么函数应该有返回值而不是直接 print？
2. 函数名为什么重要？什么样的名字是好的？
3. 什么情况下应该把代码写成函数？

---

**下一步**: [3.5 读懂 AI 生成的代码](./05-reading-ai-code.md)
