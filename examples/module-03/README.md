# Module 03 Examples

> 模块 3 的 Python 代码示例

---

## 示例 1：变量和数据类型

```python
# variables_demo.py
# 变量和数据类型演示

# 基本数据类型
name = "Alice"           # 字符串
age = 25                 # 整数
height = 1.65            # 浮点数
is_student = False       # 布尔值

# 输出
print(f"姓名：{name}")
print(f"年龄：{age}")
print(f"身高：{height}m")
print(f"是学生：{is_student}")

# 类型检查
print(f"\n类型检查:")
print(f"name 的类型：{type(name)}")
print(f"age 的类型：{type(age)}")
print(f"height 的类型：{type(height)}")

# 类型转换
age_str = str(age)
print(f"\nage 转为字符串：'{age_str}'")

height_int = int(height)
print(f"height 转为整数：{height_int}")
```

---

## 示例 2：控制流

```python
# control_flow_demo.py
# 控制流演示

# 条件语句
def check_grade(score):
    """根据分数返回等级"""
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

# 测试
scores = [95, 82, 75, 68, 55]
print("=== 成绩等级 ===")
for score in scores:
    grade = check_grade(score)
    print(f"{score}分 -> {grade}级")

# for 循环
print("\n=== for 循环 ===")
for i in range(1, 6):
    print(f"数字：{i}, 平方：{i**2}")

# while 循环
print("\n=== while 循环 ===")
count = 0
while count < 5:
    print(f"计数：{count}")
    count += 1
```

---

## 示例 3：函数

```python
# functions_demo.py
# 函数演示

def greet(name, greeting="Hello"):
    """打招呼"""
    return f"{greeting}, {name}!"

def calculate_area(width, height):
    """计算矩形面积"""
    return width * height

def get_stats(numbers):
    """计算统计信息"""
    if not numbers:
        return None

    return {
        "sum": sum(numbers),
        "count": len(numbers),
        "average": sum(numbers) / len(numbers),
        "max": max(numbers),
        "min": min(numbers)
    }

# 测试
print("=== 函数调用 ===")
print(greet("Alice"))
print(greet("Bob", "Hi"))

print(f"\n矩形面积：{calculate_area(5, 3)}")

numbers = [1, 2, 3, 4, 5]
stats = get_stats(numbers)
print(f"\n统计信息:")
for key, value in stats.items():
    print(f"  {key}: {value}")
```

---

## 示例 4：列表和字典

```python
# data_structures_demo.py
# 列表和字典演示

# 列表操作
fruits = ["apple", "banana", "cherry"]
fruits.append("orange")
fruits.insert(1, "grape")

print("=== 列表操作 ===")
print(f"水果列表：{fruits}")
print(f"第一个：{fruits[0]}")
print(f"最后两个：{fruits[-2:]}")

# 列表推导式
squares = [x**2 for x in range(1, 6)]
print(f"\n平方列表：{squares}")

# 字典操作
person = {
    "name": "Alice",
    "age": 25,
    "city": "Beijing"
}

print("\n=== 字典操作 ===")
print(f"姓名：{person['name']}")
print(f"年龄：{person['age']}")

# 添加/修改
person["email"] = "alice@example.com"
person["age"] = 26

print(f"更新后：{person}")

# 遍历
print("\n遍历字典:")
for key, value in person.items():
    print(f"  {key}: {value}")
```

---

## 示例 5：文件处理

```python
# file_handling_demo.py
# 文件处理演示

import os

# 创建文件并写入
with open("demo.txt", "w") as f:
    f.write("Hello, World!\n")
    f.write("这是第二行\n")
    f.write("这是第三行\n")

# 读取文件
print("=== 读取整个文件 ===")
with open("demo.txt") as f:
    content = f.read()
    print(content)

# 逐行读取
print("=== 逐行读取 ===")
with open("demo.txt") as f:
    for line in f:
        print(f"  {line.strip()}")

# 读取为列表
print("=== 读取为列表 ===")
with open("demo.txt") as f:
    lines = f.readlines()
    print(lines)

# 清理
os.remove("demo.txt")
print("\n演示完成，临时文件已删除")
```

---

## 示例 6：错误处理

```python
# error_handling_demo.py
# 错误处理演示

def safe_divide(a, b):
    """安全的除法"""
    try:
        result = a / b
        return result
    except ZeroDivisionError:
        return "错误：除数不能为零"
    except TypeError:
        return "错误：请输入数字"

def get_list_item(lst, index):
    """安全地获取列表元素"""
    try:
        return lst[index]
    except IndexError:
        return f"错误：索引 {index} 超出范围 (列表长度：{len(lst)})"

# 测试
print("=== 除法测试 ===")
print(f"10 / 2 = {safe_divide(10, 2)}")
print(f"10 / 0 = {safe_divide(10, 0)}")
print(f"10 / 'a' = {safe_divide(10, 'a')}")

print("\n=== 列表索引测试 ===")
numbers = [1, 2, 3, 4, 5]
print(f"索引 2: {get_list_item(numbers, 2)}")
print(f"索引 10: {get_list_item(numbers, 10)}")
```

---

## 示例 7：综合项目 - 通讯录

```python
# contact_book.py
# 简单的通讯录程序

def create_contact(name, phone, email=""):
    """创建联系人"""
    return {
        "name": name,
        "phone": phone,
        "email": email
    }

def add_contact(contacts, contact):
    """添加联系人"""
    contacts.append(contact)

def find_contact(contacts, name):
    """查找联系人"""
    for contact in contacts:
        if contact["name"].lower() == name.lower():
            return contact
    return None

def list_contacts(contacts):
    """列出所有联系人"""
    if not contacts:
        print("通讯录为空")
        return

    print("=== 通讯录 ===")
    for i, contact in enumerate(contacts, 1):
        print(f"{i}. {contact['name']} - {contact['phone']}")
        if contact["email"]:
            print(f"   Email: {contact['email']}")

# 主程序
def main():
    contacts = []

    # 添加一些示例联系人
    add_contact(contacts, create_contact("Alice", "123-4567", "alice@example.com"))
    add_contact(contacts, create_contact("Bob", "234-5678"))
    add_contact(contacts, create_contact("Charlie", "345-6789", "charlie@example.com"))

    # 列出所有
    list_contacts(contacts)

    # 查找
    print("\n=== 查找联系人 ===")
    result = find_contact(contacts, "Bob")
    if result:
        print(f"找到：{result}")
    else:
        print("未找到")

if __name__ == "__main__":
    main()
```

---

## 运行示例

```bash
# 进入示例目录
cd examples/module-03

# 运行各个示例
python3 variables_demo.py
python3 control_flow_demo.py
python3 functions_demo.py
python3 data_structures_demo.py
python3 file_handling_demo.py
python3 error_handling_demo.py
python3 contact_book.py
```
