# 实验 LAB-06：代码阅读练习

> 通过阅读和理解代码来巩固编程概念

---

## 🎯 实验目标

- [ ] 能够读懂 AI 生成的 Python 代码
- [ ] 能够追踪代码的执行流程
- [ ] 能够识别和修改代码中的问题
- [ ] 能够向 AI 提出改进代码的请求

---

## 📋 准备工作

```bash
# 创建实验目录
mkdir -p ~/computer-basics/module-03/lab06
cd ~/computer-basics/module-03/lab06
```

---

## 第一部分：理解简单函数 (20 分钟)

### 任务 1.1：阅读代码

阅读以下 AI 生成的函数：

```python
# temperature.py

def celsius_to_fahrenheit(celsius):
    """Convert Celsius to Fahrenheit"""
    return celsius * 9/5 + 32

def fahrenheit_to_celsius(fahrenheit):
    """Convert Fahrenheit to Celsius"""
    return (fahrenheit - 32) * 5/9

# 测试
print(f"0°C = {celsius_to_fahrenheit(0)}°F")
print(f"32°F = {fahrenheit_to_celsius(32)}°C")
```

**问题**：
1. 这个文件定义了几个函数？
2. `celsius_to_fahrenheit` 函数的输入是什么？输出是什么？
3. 如果输入 100°C，输出是多少？（可以先猜，然后运行验证）
4. 第 3 行的 `"""Convert Celsius..."""` 是什么？有什么用？

### 任务 1.2：运行验证

```bash
# 创建文件
nano temperature.py

# 输入代码并保存

# 运行
python3 temperature.py
```

**预期输出**：
```
0°C = 32.0°F
32°F = 0.0°C
```

### 任务 1.3：修改代码

修改 `temperature.py`，添加以下功能：

1. 添加一个新函数 `celsius_to_kelvin(celsius)`，返回 `celsius + 273.15`
2. 添加测试代码，调用新函数
3. 运行验证结果

**完成后代码应该像**：

```python
def celsius_to_kelvin(celsius):
    """Convert Celsius to Kelvin"""
    return celsius + 273.15

print(f"100°C = {celsius_to_kelvin(100)}K")
# 预期输出：100°C = 373.15K
```

---

## 第二部分：理解条件逻辑 (25 分钟)

### 任务 2.1：阅读代码

```python
# grade_checker.py

def get_grade(score):
    """Return letter grade based on score"""
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    elif score >= 60:
        return "D"
    else:
        return "F"

def get_comment(grade):
    """Return comment based on grade"""
    if grade == "A":
        return "Excellent!"
    elif grade == "B":
        return "Good job!"
    elif grade == "C":
        return "Keep trying"
    else:
        return "Needs help"

# 测试
scores = [95, 82, 75, 68, 55]

for score in scores:
    grade = get_grade(score)
    comment = get_comment(grade)
    print(f"Score: {score}, Grade: {grade}, Comment: {comment}")
```

**问题**：
1. `get_grade(85)` 返回什么？
2. `get_comment("A")` 返回什么？
3. 如果 `score = 70`，`grade` 是什么？
4. 为什么有两个函数而不是写在一起？

### 任务 2.2：追踪执行

手动追踪以下调用的执行过程：

```python
get_grade(82)
```

**填写**：
```
1. 检查 82 >= 90?  ____ (True/False)
2. 检查 82 >= 80?  ____ (True/False)
3. 返回 ____
```

### 任务 2.3：运行验证

```bash
nano grade_checker.py
# 输入代码
python3 grade_checker.py
```

**预期输出**：
```
Score: 95, Grade: A, Comment: Excellent!
Score: 82, Grade: B, Comment: Good job!
Score: 75, Grade: C, Comment: Keep trying
Score: 68, Grade: D, Comment: Needs help
Score: 55, Grade: F, Comment: Needs help
```

### 任务 2.4：修改代码

**新需求**：
1. 添加一个函数 `is_passing(grade)`，如果等级是 A/B/C/D 返回 True，否则返回 False
2. 修改测试代码，也输出是否及格

**提示**：

```python
def is_passing(grade):
    """Return True if grade is passing"""
    # 你的代码在这里
    pass  # 这行要删掉，替换成你的代码
```

---

## 第三部分：理解循环和列表 (30 分钟)

### 任务 3.1：阅读代码

```python
# data_processor.py

def process_numbers(numbers):
    """Process a list of numbers and return statistics"""
    if not numbers:
        return {"error": "Empty list"}

    total = 0
    count = 0
    largest = numbers[0]
    smallest = numbers[0]

    for num in numbers:
        total += num
        count += 1
        if num > largest:
            largest = num
        if num < smallest:
            smallest = num

    average = total / count

    return {
        "total": total,
        "count": count,
        "average": average,
        "largest": largest,
        "smallest": smallest
    }

# 测试
data = [23, 45, 12, 67, 34, 89, 2]
result = process_numbers(data)

print(f"Data: {data}")
print(f"Statistics: {result}")
```

**问题**：
1. `if not numbers:` 这行检查什么？
2. 为什么 `largest` 和 `smallest` 初始化为 `numbers[0]`？
3. `for num in numbers:` 循环执行了多少次？
4. 返回值是什么类型的？（int, float, str, list, dict?）

### 任务 3.2：手动追踪

对于 `data = [5, 2, 8]`，追踪第一次循环迭代：

```
初始：total = ___, count = ___, largest = ___, smallest = ___

第一次迭代 (num = 5):
- total = ___ + 5 = ___
- count = ___ + 1 = ___
- 5 > 5? ___ → largest = ___
- 5 < 5? ___ → smallest = ___
```

### 任务 3.3：运行验证

```bash
nano data_processor.py
python3 data_processor.py
```

**验证**：
- total = 23+45+12+67+34+89+2 = 272 ✓
- count = 7 ✓
- average = 272/7 ≈ 38.86 ✓
- largest = 89 ✓
- smallest = 2 ✓

### 任务 3.4：重构代码

**任务**：使用 Python 内置函数简化代码

```python
# 原来的代码
total = 0
count = 0
for num in numbers:
    total += num
    count += 1

# 可以简化为
total = sum(numbers)
count = len(numbers)

# 同样，找最大最小也可以简化
largest = max(numbers)
smallest = min(numbers)
```

**修改 `process_numbers` 函数**，使用内置函数简化代码。

**修改后**应该像：

```python
def process_numbers(numbers):
    """Process a list of numbers and return statistics"""
    if not numbers:
        return {"error": "Empty list"}

    return {
        "total": sum(numbers),
        "count": len(numbers),
        "average": sum(numbers) / len(numbers),
        "largest": max(numbers),
        "smallest": min(numbers)
    }
```

---

## 第四部分：综合练习 (25 分钟)

### 任务：分析并修复代码

以下 AI 生成的代码**有 bug**，找出并修复：

```python
# buggy_code.py

def calculate_discount(price, discount_percent):
    """Calculate final price after discount"""
    discount_amount = price * discount_percent
    final_price = price - discount_amount
    return final_price

def main():
    # 原价 100 元，打 8 折（20% 折扣）
    original_price = 100
    discount = 20  # 20%

    final = calculate_discount(original_price, discount)
    print(f"Original: ${original_price}")
    print(f"Discount: {discount}%")
    print(f"Final price: ${final}")

main()
```

**问题**：
1. 运行代码，输出是什么？
2. 预期输出应该是多少？（100 元打 8 折 = 80 元）
3. bug 在哪里？
4. 如何修复？

**提示**：
```
20% 应该表示为 0.2 还是 20？
discount_percent = 20 还是 0.2？
```

**修复后的代码**：

```python
# 方案 1：修改调用时的参数
final = calculate_discount(original_price, discount / 100)

# 方案 2：修改函数内部
discount_amount = price * (discount_percent / 100)
```

---

## 📝 实验报告

```markdown
# LAB-06 实验报告

姓名：__________  日期：__________

## 第一部分：温度转换
- [ ] 理解了函数结构
- [ ] 成功添加了新函数
- [ ] 验证了转换结果

## 第二部分：成绩判断
- [ ] 理解了条件逻辑
- [ ] 手动追踪了执行过程
- [ ] 添加了 is_passing 函数

## 第三部分：数据处理
- [ ] 理解了循环和列表
- [ ] 手动追踪了变量变化
- [ ] 用内置函数简化了代码

## 第四部分：调试练习
- [ ] 找出了 bug
- [ ] 理解了 bug 原因
- [ ] 成功修复

## 遇到的问题

## 最大的收获

## 还不懂的地方
```

---

## 🔗 相关资源

- [3.4 函数与模块化](./04-functions.md)
- [3.5 读懂 AI 生成的代码](./05-reading-ai-code.md)
- [resources/common-errors.md](../resources/common-errors.md)

---

**完成 LAB-06 后**，你已经完成了 module-03 的所有内容！🎉

下一步：[模块 4：数据与网络](../module-04-data-network/README.md)
