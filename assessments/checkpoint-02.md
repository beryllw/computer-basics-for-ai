# Checkpoint 02 - 模块 2-3 评估

> 评估你对 Linux 工具和编程概念的理解

---

## 📋 评估说明

- **覆盖内容**: 模块 2（Linux 工具）、模块 3（编程概念）
- **建议时间**: 45-60 分钟
- **通过标准**: 70% 正确率
- **允许使用**: notes、资源文档、命令速查表
- **不允许使用**: AI 助手、搜索引擎、实际运行命令

---

## 第一部分：Linux 命令选择题（每题 5 分，共 25 分）

### 1. 如何列出当前目录下所有文件（包括隐藏文件）？

A. `ls -l`
B. `ls -a`
C. `ls -la`
D. `ls -al`

### 2. 如何复制一个目录及其所有内容？

A. `cp dir1 dir2`
B. `cp -r dir1 dir2`
C. `mv dir1 dir2`
D. `mkdir dir2`

### 3. 如何查找文件中包含 "error" 的行？

A. `find "error" file.txt`
B. `search "error" file.txt`
C. `grep "error" file.txt`
D. `cat "error" file.txt`

### 4. 管道符号 `|` 的作用是什么？

A. 重定向输出到文件
B. 将一个命令的输出作为另一个命令的输入
C. 同时执行两个命令
D. 注释

### 5. 如何给脚本添加执行权限？

A. `run script.sh`
B. `exec script.sh`
C. `chmod +x script.sh`
D. `bash script.sh`

---

## 第二部分：Python 编程选择题（每题 5 分，共 25 分）

### 6. 以下哪个是有效的 Python 变量名？

A. `1st_name`
B. `my-name`
C. `my_name`
D. `my name`

### 7. 以下代码的输出是什么？

```python
x = 10
if x > 5:
    print("A")
elif x > 8:
    print("B")
else:
    print("C")
```

A. A
B. B
C. C
D. AB

### 8. 以下代码的输出是什么？

```python
for i in range(3):
    print(i, end=" ")
```

A. 1 2 3
B. 0 1 2
C. 0 1 2 3
D. 1 2

### 9. 如何定义一个函数？

A. `function my_func():`
B. `def my_func():`
C. `define my_func():`
D. `func my_func():`

### 10. 以下代码的输出是什么？

```python
def greet(name="World"):
    return f"Hello, {name}!"

print(greet())
```

A. `Hello, !`
B. `Hello, None!`
C. `Hello, World!`
D. 错误

---

## 第三部分：命令/代码写作题（每题 10 分，共 30 分）

### 11. Linux 命令组合

写出完成以下任务的命令：

a) 进入目录 `documents`
b) 列出其中所有 `.txt` 文件
c) 统计这些文件的总行数

```bash
# 你的答案：

```

### 12. 文本处理

有一个日志文件 `app.log`，写出命令：

a) 找出所有包含 "ERROR" 的行
b) 统计错误数量
c) 将错误保存到新文件 `errors.txt`

```bash
# 你的答案：

```

### 13. Python 函数

编写一个函数 `is_even(n)`，判断一个数字是否为偶数：

```python
# 你的答案：

```

---

## 第四部分：代码阅读题（20 分）

### 14. 阅读以下代码，回答问题

```python
def process_data(data):
    result = []
    for item in data:
        if item > 0:
            result.append(item * 2)
    return result

numbers = [1, -2, 3, 0, 5, -1]
output = process_data(numbers)
print(output)
```

**问题**：

a) 这个函数的作用是什么？（5 分）

b) 输出结果是什么？（5 分）

c) 如果输入是空列表 `[]`，输出是什么？（5 分）

d) 如何用一行代码实现同样的功能？（5 分）

---

## 第五部分：综合应用题（20 分）

### 15. 文件处理脚本

**场景**：你有一个包含学生成绩的 CSV 文件 `grades.csv`：

```csv
name,math,english,science
Alice,85,90,88
Bob,78,82,75
Charlie,92,88,95
```

**任务**：编写一个 Python 脚本，完成以下功能：

1. 读取 CSV 文件
2. 计算每个学生的平均分
3. 输出平均分最高的学生姓名

```python
# 你的代码：

```

---

## 📝 答案纸

```
姓名：__________  日期：__________

### 选择题
1. ___  2. ___  3. ___  4. ___  5. ___
6. ___  7. ___  8. ___  9. ___  10. ___

### 命令/代码写作题
11.


12.


13.


### 代码阅读题
14a.
14b.
14c.
14d.

### 综合应用题
15.
```

---

## ✅ 参考答案

<details>
<summary>点击展开答案</summary>

### 选择题
1. C (或 D，-la 和 -al 等价)
2. B
3. C
4. B
5. C
6. C
7. A (先满足 x>5，不会继续判断 elif)
8. B
9. B
10. C

### 命令/代码写作题
11.
```bash
cd documents
ls *.txt
wc -l *.txt
```

12.
```bash
grep "ERROR" app.log | wc -l
grep "ERROR" app.log > errors.txt
```

13.
```python
def is_even(n):
    return n % 2 == 0
```

### 代码阅读题
14a. 过滤出正数并乘以 2
14b. [2, 6, 10]
14c. []
14d. `[x * 2 for x in data if x > 0]`

### 综合应用题
```python
import csv

with open("grades.csv") as f:
    reader = csv.DictReader(f)
    best_student = None
    best_avg = 0

    for row in reader:
        avg = (int(row["math"]) + int(row["english"]) + int(row["science"])) / 3
        if avg > best_avg:
            best_avg = avg
            best_student = row["name"]

print(f"Best student: {best_student} (avg: {best_avg:.1f})")
```

</details>

---

**完成 Checkpoint 02 后**，继续学习 模块 4
