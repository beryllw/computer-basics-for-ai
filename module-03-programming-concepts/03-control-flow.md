# 3.3 控制流：条件与循环

> 理解程序如何做决定和重复执行

---

## 🎯 学习目标

学完本课后，你将能够：

- [ ] 理解条件语句（if/else）
- [ ] 理解循环（for/while）
- [ ] 读懂包含控制流的代码
- [ ] 理解嵌套的控制结构

---

## 💭 从一个问题开始

**程序如何做决定？**

生活中我们不断做决定：
- 如果下雨，就带伞
- 如果饿了，就吃饭
- 否则，继续工作

程序也需要做决定，这就是**条件语句**。

**程序如何重复做事？**

- 检查每封邮件
- 处理每个文件
- 等待用户输入

这就是**循环**。

---

## 💡 核心概念

### 条件语句：if/elif/else

```python
# 基本结构
age = 18

if age >= 18:
    print("You are an adult")
else:
    print("You are a minor")

# 多个条件
score = 85

if score >= 90:
    grade = "A"
elif score >= 80:  # else if 的缩写
    grade = "B"
elif score >= 70:
    grade = "C"
else:
    grade = "F"

print(f"Your grade: {grade}")
```

**关键点**：
- `if` 后面是条件（返回 True/False）
- 冒号 `:` 表示代码块开始
- **缩进**表示哪些代码属于条件块
- `elif` 可以多个，`else` 最多一个

### 比较运算符

| 运算符 | 含义 | 例子 | 结果 |
|--------|------|------|------|
| `==` | 等于 | `5 == 5` | `True` |
| `!=` | 不等于 | `5 != 3` | `True` |
| `>` | 大于 | `5 > 3` | `True` |
| `<` | 小于 | `5 < 3` | `False` |
| `>=` | 大于等于 | `5 >= 5` | `True` |
| `<=` | 小于等于 | `5 <= 3` | `False` |

---

### 循环：for 循环

```python
# 遍历列表
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(f"I like {fruit}")

# 输出：
# I like apple
# I like banana
# I like cherry

# 使用 range() 遍历数字
for i in range(5):  # 0 到 4
    print(i)

for i in range(1, 6):  # 1 到 5
    print(i)

for i in range(0, 10, 2):  # 0, 2, 4, 6, 8（步长为 2）
    print(i)
```

### 循环：while 循环

```python
# while：当条件为 True 时继续
count = 0

while count < 5:
    print(f"Count: {count}")
    count += 1  # 重要：改变条件，否则会无限循环！

# 输出：Count: 0, 1, 2, 3, 4

# 等待用户输入
password = ""
while password != "secret":
    password = input("Enter password: ")
print("Access granted!")
```

### for vs while

| 场景 | 用 for | 用 while |
|------|--------|----------|
| 已知次数 | ✅ | ⚠️ |
| 遍历列表/字符串 | ✅ | ❌ |
| 条件满足前重复 | ❌ | ✅ |
| 等待某事发生 | ❌ | ✅ |

---

## 🔍 深入理解

### 布尔逻辑

```python
# and: 两个条件都为 True
age = 25
has_license = True

if age >= 18 and has_license:
    print("You can drive")

# or: 任一条件为 True
day = "Saturday"

if day == "Saturday" or day == "Sunday":
    print("Weekend!")

# not: 取反
is_raining = False

if not is_raining:
    print("No umbrella needed")
```

### 嵌套结构

```python
# 嵌套 if
score = 85
is_bonus = True

if score >= 60:
    if is_bonus:
        score += 5
    print(f"Final score: {score}")

# 嵌套循环
for i in range(3):
    for j in range(3):
        print(f"({i}, {j})", end=" ")
    print()

# 输出：
# (0, 0) (0, 1) (0, 2)
# (1, 0) (1, 1) (1, 2)
# (2, 0) (2, 1) (2, 2)
```

### 循环控制

```python
# break: 跳出循环
for i in range(10):
    if i == 5:
        break  # 找到 5 就停止
    print(i)  # 输出：0, 1, 2, 3, 4

# continue: 跳过本次
for i in range(5):
    if i == 2:
        continue  # 跳过 2
    print(i)  # 输出：0, 1, 3, 4

# else: 循环正常结束（没有被 break）
for i in range(5):
    if i == 10:
        break
else:
    print("Loop completed without break")
```

---

## 🧪 代码示例

### 示例 1：成绩判断系统

```python
# 成绩判断

scores = [95, 82, 67, 45, 78, 88, 91]

for score in scores:
    if score >= 90:
        grade = "A"
        comment = "Excellent!"
    elif score >= 80:
        grade = "B"
        comment = "Good job"
    elif score >= 70:
        grade = "C"
        comment = "Keep trying"
    elif score >= 60:
        grade = "D"
        comment = "Needs improvement"
    else:
        grade = "F"
        comment = "See me after class"

    print(f"Score: {score}, Grade: {grade} - {comment}")
```

### 示例 2：查找最大值

```python
# 在列表中找最大值

numbers = [23, 45, 12, 67, 34, 89, 2]

# 方法 1：用内置函数
max_num = max(numbers)
print(f"Max: {max_num}")

# 方法 2：自己实现
max_num = numbers[0]  # 假设第一个是最大

for num in numbers[1:]:
    if num > max_num:
        max_num = num  # 找到更大的，更新

print(f"Max: {max_num}")
```

### 示例 3：猜数字游戏

```python
# 猜数字游戏（简化版）

secret_number = 42
max_attempts = 5

print("Guess a number between 1 and 100")

for attempt in range(1, max_attempts + 1):
    # 模拟用户输入
    guess = 50  # 实际中用：guess = int(input("Your guess: "))

    if guess == secret_number:
        print(f"Correct! You guessed it in {attempt} attempts")
        break
    elif guess < secret_number:
        print("Too low!")
    else:
        print("Too high!")
else:
    print(f"Game over! The number was {secret_number}")
```

### 示例 4：处理列表

```python
# 列表处理综合示例

items = ["apple", "", "banana", "cherry", ""]

# 过滤空字符串
non_empty = []
for item in items:
    if item:  # 非空字符串为 True
        non_empty.append(item.upper())

print(non_empty)  # ['APPLE', 'BANANA', 'CHERRY']

# 统计
count = 0
for item in items:
    if item:
        count += 1
print(f"Non-empty items: {count}")
```

---

## 💡 实践技巧

### 常见的条件模式

```python
# 检查列表是否为空
items = []

if items:  # 非空列表为 True
    print("Has items")
else:
    print("Empty list")

# 检查值是否在列表中
fruits = ["apple", "banana"]

if "apple" in fruits:
    print("Found apple")

if "orange" not in fruits:
    print("No orange")
```

### 循环最佳实践

```python
# ✅ 好的做法
for i, fruit in enumerate(fruits):  # 同时获取索引和值
    print(f"{i}: {fruit}")

# ❌ 避免无限循环
# while True:
#     print("Help!")  # 永远不会停止

# 正确的无限循环（有退出条件）
while True:
    command = input("> ")
    if command == "quit":
        break
```

### 调试控制流

```python
# 用 print 调试循环
numbers = [1, 2, 3, 4, 5]
total = 0

for num in numbers:
    total += num
    print(f"DEBUG: num={num}, total={total}")

print(f"Final total: {total}")
```

---

## 📝 关键术语

| 术语 | 英文 | 解释 |
|------|------|------|
| 条件 | Condition | 返回 True/False 的表达式 |
| 分支 | Branch | if/else 的不同执行路径 |
| 循环 | Loop | 重复执行代码 |
| 迭代 | Iteration | 循环的一次执行 |
| 缩进 | Indentation | Python 用缩进表示代码块 |
| 嵌套 | Nesting | 在...内部再放... |

---

## ✅ 本课小结

```
核心要点：

1. 条件语句：
   - if: 如果...
   - elif: 否则如果...
   - else: 否则...

2. 循环：
   - for: 遍历序列
   - while: 条件满足时重复

3. 布尔逻辑：
   - and: 与（都真才真）
   - or: 或（一真就真）
   - not: 非（取反）

4. 循环控制：
   - break: 跳出循环
   - continue: 跳过本次

5. Python 用缩进表示代码块
```

---

## 🤔 思考题

1. for 循环和 while 循环有什么区别？各适合什么场景？
2. 如果没有缩进，Python 代码会有什么问题？
3. 如何避免无限循环？

---

**下一步**: [3.4 函数与模块化](./04-functions.md)
