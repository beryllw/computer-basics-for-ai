# 实验 LAB-05：Python 初体验

> 第一次编写和运行 Python 代码

---

## 🎯 实验目标

- [ ] 能够运行 Python 代码
- [ ] 理解 Python 交互式环境
- [ ] 练习变量和基本数据类型
- [ ] 编写简单的 Python 脚本

---

## 📋 准备工作

```bash
# 检查 Python 是否安装
python3 --version

# 创建实验目录
mkdir -p ~/computer-basics/module-03
cd ~/computer-basics/module-03
```

---

## 第一部分：Python 交互式环境 (15 分钟)

### 步骤 1：启动 Python

```bash
python3
```

你会看到类似输出：
```
Python 3.10.12 (main, Nov 20 2023, 15:14:05) [GCC 11.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

### 步骤 2：尝试基本运算

```python
# 在 >>> 提示符后输入

>>> 1 + 1
2

>>> 10 * 5
50

>>> 100 / 3
33.333333333333336

>>> 2 ** 10
1024
```

### 步骤 3：使用变量

```python
>>> name = "Alice"
>>> age = 25
>>> height = 1.65

>>> print(name)
Alice

>>> print(f"{name} is {age} years old")
Alice is 25 years old
```

### 步骤 4：退出 Python

```python
>>> exit()
# 或者按 Ctrl+D
```

---

## 第二部分：编写第一个脚本 (20 分钟)

### 步骤 1：创建文件

```bash
# 用文本编辑器创建文件
nano hello.py
```

### 步骤 2：输入代码

```python
# hello.py
# 我的第一个 Python 程序

# 定义变量
name = input("What is your name? ")
age = int(input("How old are you? "))

# 输出问候
print(f"\nHello, {name}!")
print(f"You are {age} years old.")
print(f"In 10 years, you will be {age + 10}.")
```

### 步骤 3：保存并运行

```bash
# 保存文件（nano: Ctrl+O, Enter, Ctrl+X）

# 运行脚本
python3 hello.py
```

### 步骤 4：测试程序

```
What is your name? Alice
How old are you? 25

Hello, Alice!
You are 25 years old.
In 10 years, you will be 35.
```

---

## 第三部分：变量练习 (20 分钟)

创建文件 `variables.py`：

```python
# variables.py
# 变量和数据类型练习

# 1. 创建变量存储你的信息
first_name = "Your"      # 改成你的名字
last_name = "Name"       # 改成你的姓氏
age = 25                 # 改成你的年龄
height = 1.70            # 改成你的身高（米）
is_student = True        # 改成 True 或 False

# 2. 使用 f-string 输出
print(f"Name: {first_name} {last_name}")
print(f"Age: {age}")
print(f"Height: {height}m")
print(f"Is student: {is_student}")

# 3. 类型转换练习
birth_year = 2026 - age
print(f"\nYou were born in {birth_year}")

# 4. 检查类型
print(f"\nType of age: {type(age)}")
print(f"Type of height: {type(height)}")
print(f"Type of is_student: {type(is_student)}")
```

**任务**：
1. 修改变量值为你自己的信息
2. 运行程序查看输出
3. 添加一个新的变量（比如你的城市）
4. 再次运行程序

---

## 第四部分：简单计算器 (25 分钟)

创建文件 `calculator.py`：

```python
# calculator.py
# 简单计算器

# 定义两个数字
a = 10
b = 3

# 输出各种运算结果
print(f"Numbers: {a} and {b}\n")

print(f"Addition:       {a} + {b} = {a + b}")
print(f"Subtraction:    {a} - {b} = {a - b}")
print(f"Multiplication: {a} * {b} = {a * b}")
print(f"Division:       {a} / {b} = {a / b:.2f}")  # 保留 2 位小数
print(f"Integer div:    {a} // {b} = {a // b}")
print(f"Remainder:      {a} % {b} = {a % b}")
print(f"Power:          {a} ** {b} = {a ** b}")
```

**运行并验证结果**：
```bash
python3 calculator.py
```

**预期输出**：
```
Numbers: 10 and 3

Addition:       10 + 3 = 13
Subtraction:    10 - 3 = 7
Multiplication: 10 * 3 = 30
Division:       10 / 3 = 3.33
Integer div:    10 // 3 = 3
Remainder:      10 % 3 = 1
Power:          10 ** 3 = 1000
```

---

## 📝 实验报告

完成以下内容：

```markdown
# LAB-05 实验报告

姓名：__________  日期：__________

## 1. 运行 Python 交互式环境
- [ ] 成功启动 Python
- [ ] 尝试了基本运算
- [ ] 创建了变量

## 2. 第一个脚本
- [ ] 创建了 hello.py
- [ ] 成功运行并接受输入
- [ ] 输出正确结果

## 3. 变量练习
- [ ] 创建了 variables.py
- [ ] 填写了自己的信息
- [ ] 添加了新变量

## 4. 计算器
- [ ] 创建了 calculator.py
- [ ] 验证了所有运算结果
- [ ] 理解了每种运算符

## 遇到的问题

（记录你遇到的问题和解决方法）

## 收获与疑问

（记录你的收获和还不懂的地方）
```

---

## 🔗 相关资源

- [3.2 变量与数据类型](./02-variables-data-types.md)
- [resources/glossary.md](../resources/glossary.md)
- [resources/common-errors.md](../resources/common-errors.md)

---

**完成 LAB-05 后**，继续学习下一课或开始 [LAB-06](./LAB-06-code-reading.md)
