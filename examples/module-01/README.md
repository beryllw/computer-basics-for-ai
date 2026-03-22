# Module 01 Examples

> 模块 1 的示例和练习代码

---

## 示例 1：二进制转换

```python
# binary_convert.py
# 十进制和二进制互相转换

def decimal_to_binary(n):
    """十进制转二进制"""
    if n == 0:
        return "0"
    result = ""
    while n > 0:
        result = str(n % 2) + result
        n = n // 2
    return result

def binary_to_decimal(binary_str):
    """二进制转十进制"""
    result = 0
    for i, digit in enumerate(reversed(binary_str)):
        result += int(digit) * (2 ** i)
    return result

# 测试
print("=== 十进制转二进制 ===")
for i in range(10):
    print(f"{i} -> {decimal_to_binary(i)}")

print("\n=== 二进制转十进制 ===")
for b in ["0", "1", "10", "101", "1111"]:
    print(f"{b} -> {binary_to_decimal(b)}")
```

---

## 示例 2：文本的二进制表示

```python
# text_to_binary.py
# 将文本转换为二进制表示（ASCII）

def text_to_binary(text):
    """将文本转换为二进制"""
    result = []
    for char in text:
        # 获取 ASCII 码，然后转为二进制
        ascii_code = ord(char)
        binary = bin(ascii_code)[2:].zfill(8)  # 补足 8 位
        result.append(binary)
    return " ".join(result)

def binary_to_text(binary_str):
    """将二进制转换回文本"""
    bytes_list = binary_str.split()
    result = ""
    for b in bytes_list:
        ascii_code = int(b, 2)
        result += chr(ascii_code)
    return result

# 测试
message = "Hello"
print(f"原文：{message}")
binary = text_to_binary(message)
print(f"二进制：{binary}")

# 解码
decoded = binary_to_text(binary)
print(f"解码：{decoded}")
```

---

## 示例 3：简单算法演示

```python
# algorithm_demo.py
# 演示常见算法

def linear_search(arr, target):
    """线性搜索"""
    for i, item in enumerate(arr):
        if item == target:
            return i
    return -1

def bubble_sort(arr):
    """冒泡排序"""
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

def find_max(arr):
    """找最大值"""
    if not arr:
        return None
    max_val = arr[0]
    for item in arr[1:]:
        if item > max_val:
            max_val = item
    return max_val

# 测试
numbers = [64, 34, 25, 12, 22, 11, 90]

print("原始数组:", numbers)
print("最大值:", find_max(numbers.copy()))

print("\n排序过程:")
print("排序前:", numbers)
print("排序后:", bubble_sort(numbers.copy()))

print("\n搜索演示:")
print(f"25 在索引 {linear_search(numbers, 25)}")
print(f"100 在索引 {linear_search(numbers, 100)}")
```

---

## 示例 4：抽象层次演示

```python
# abstraction_demo.py
# 演示抽象层次

# 底层：直接操作
def add_numbers_low_level(a, b):
    # 模拟底层加法
    result = 0
    carry = 0
    # ... 复杂的位运算
    return a + b  # 简化

# 中层：函数封装
def calculate_sum(numbers):
    """计算列表总和"""
    total = 0
    for num in numbers:
        total += num
    return total

# 高层：使用内置函数
def calculate_sum_high_level(numbers):
    """计算列表总和（高级方式）"""
    return sum(numbers)

# 使用
numbers = [1, 2, 3, 4, 5]

print("底层方式:", add_numbers_low_level(2, 3))
print("中层方式:", calculate_sum(numbers))
print("高层方式:", calculate_sum_high_level(numbers))

# 用户不需要知道内部实现
print(f"总和是：{calculate_sum_high_level(numbers)}")
```

---

## 运行示例

```bash
# 进入示例目录
cd examples/module-01

# 运行示例
python3 binary_convert.py
python3 text_to_binary.py
python3 algorithm_demo.py
python3 abstraction_demo.py
```
