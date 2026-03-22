# 4.1 数据格式：JSON 与 CSV

> 理解计算机如何组织和存储数据

---

## 🎯 学习目标

学完本课后，你将能够：

- [ ] 理解 JSON 格式的结构
- [ ] 理解 CSV 格式的结构
- [ ] 读懂和编写简单的 JSON
- [ ] 理解不同数据格式的用途

---

## 💭 从一个问题开始

**数据如何组织？**

生活中我们组织信息：
- 通讯录：姓名、电话、地址
- 购物清单：商品、数量、价格
- 课程表：时间、地点、课程

计算机也需要组织数据，这就是**数据格式**。

---

## 💡 核心概念

### 什么是数据格式？

> **数据格式 = 数据的组织方式**

就像：
- 表格：行和列
- 表单：字段和值
- 清单：项目和数量

计算机有多种数据格式，最常用的是 **JSON** 和 **CSV**。

---

## 📊 JSON 格式

### JSON 是什么？

> **JSON = JavaScript Object Notation**

一种轻量级的数据交换格式，用于：
- 存储数据
- 在程序间传递数据
- API 通信

### JSON 的基本结构

```json
{
  "name": "Alice",
  "age": 25,
  "is_student": false,
  "hobbies": ["reading", "coding", "hiking"]
}
```

**特点**：
- 用 `{}` 表示对象
- 用 `[]` 表示数组（列表）
- 键值对用 `:` 分隔
- 键必须用双引号 `""`
- 多个键值对用 `,` 分隔

### JSON 的数据类型

| JSON 类型 | 例子 | 对应 Python |
|-----------|------|------------|
| 对象 | `{"name": "Alice"}` | dict |
| 数组 | `[1, 2, 3]` | list |
| 字符串 | `"Hello"` | str |
| 数字 | `42`, `3.14` | int/float |
| 布尔值 | `true`, `false` | True/False |
| null | `null` | None |

### JSON 示例

```json
{
  "user": {
    "id": 123,
    "name": "Alice",
    "email": "alice@example.com"
  },
  "posts": [
    {"id": 1, "title": "Hello World"},
    {"id": 2, "title": "My Second Post"}
  ],
  "active": true
}
```

---

## 📋 CSV 格式

### CSV 是什么？

> **CSV = Comma-Separated Values**

用逗号分隔值的格式，用于：
- 表格数据
- 导入/导出数据
- Excel 可以打开

### CSV 的基本结构

```csv
name,age,city
Alice,25,Beijing
Bob,30,Shanghai
Charlie,28,Guangzhou
```

**特点**：
- 第一行通常是标题（列名）
- 每行是一条记录
- 用逗号分隔字段
- 简单、易读

### CSV 示例

```csv
id,product,price,quantity
1,Apple,1.50,10
2,Banana,0.75,20
3,Orange,2.00,15
```

**对应的表格**：

| id | product | price | quantity |
|----|---------|-------|----------|
| 1 | Apple | 1.50 | 10 |
| 2 | Banana | 0.75 | 20 |
| 3 | Orange | 2.00 | 15 |

---

## 🔍 深入理解

### JSON vs CSV

| 特点 | JSON | CSV |
|------|------|-----|
| 结构 | 树状（嵌套） | 表格（扁平） |
| 可读性 | 好 | 很好 |
| 适合场景 | 复杂数据、API | 表格数据、导出 |
| 大小 | 稍大 | 较小 |
| 支持类型 | 多种类型 | 只有字符串 |

### 何时用哪个？

```
用 JSON：
- 嵌套数据（对象里有对象）
- API 通信
- 配置文件

用 CSV：
- 简单的表格数据
- 需要 Excel 打开
- 大量数据的导出
```

---

## 🧪 Python 中处理 JSON 和 CSV

### 处理 JSON

```python
import json

# JSON 字符串 → Python 对象
json_str = '{"name": "Alice", "age": 25}'
data = json.loads(json_str)
print(data["name"])  # Alice

# Python 对象 → JSON 字符串
python_dict = {"name": "Bob", "age": 30}
json_str = json.dumps(python_dict)
print(json_str)  # {"name": "Bob", "age": 30}

# 读取 JSON 文件
with open("data.json") as f:
    data = json.load(f)

# 写入 JSON 文件
with open("output.json", "w") as f:
    json.dump(data, f, indent=2)
```

### 处理 CSV

```python
import csv

# 读取 CSV 文件
with open("data.csv") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row["name"], row["age"])

# 写入 CSV 文件
with open("output.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["name", "age"])
    writer.writerow(["Alice", 25])
    writer.writerow(["Bob", 30])
```

---

## 🧪 代码示例

### 示例 1：JSON 配置文件

```json
{
  "app_name": "My App",
  "version": "1.0.0",
  "settings": {
    "theme": "dark",
    "language": "zh-CN",
    "notifications": true
  },
  "features": ["search", "share", "comment"]
}
```

### 示例 2：API 响应

```json
{
  "status": "success",
  "data": {
    "user_id": 123,
    "username": "alice",
    "profile": {
      "avatar": "https://example.com/avatar.jpg",
      "bio": "Hello World"
    }
  },
  "timestamp": "2026-03-22T10:30:00Z"
}
```

### 示例 3：CSV 数据导出

```csv
date,product,quantity,revenue
2026-01-01,Widget A,100,1500.00
2026-01-02,Widget B,50,1250.00
2026-01-03,Widget A,75,1125.00
```

---

## 💡 实践技巧

### JSON 格式化

**问题**：JSON 挤在一起很难读

**解决**：使用格式化工具

```python
# Python 格式化
import json

ugly_json = '{"name":"Alice","age":25,"hobbies":["reading","coding"]}'
pretty = json.loads(ugly_json)
print(json.dumps(pretty, indent=2))
```

**在线工具**：
- jsonlint.com
- jsonformatter.org

### 处理特殊字符

```csv
# CSV 中包含逗号怎么办？用引号包裹
name,description,price
"Widget, Deluxe","High-quality, long-lasting",29.99
```

```json
// JSON 中的引号需要转义
{
  "quote": "He said \"Hello\"",
  "path": "C:\\Users\\Alice"
}
```

---

## 📝 关键术语

| 术语 | 英文 | 解释 |
|------|------|------|
| JSON | JSON | JavaScript 对象表示法 |
| CSV | CSV | 逗号分隔值 |
| 对象 | Object | JSON 的键值对集合 |
| 数组 | Array | JSON 的列表 |
| 键值对 | Key-Value Pair | 键和值的组合 |
| 解析 | Parse | 把字符串转成数据结构 |
| 序列化 | Serialize | 把数据结构转成字符串 |

---

## ✅ 本课小结

```
核心要点：

1. JSON 格式：
   - 用 {} 表示对象，[] 表示数组
   - 键值对用 "key": value 表示
   - 适合复杂数据和 API

2. CSV 格式：
   - 用逗号分隔字段
   - 每行一条记录
   - 适合表格数据

3. Python 处理：
   - JSON: json.loads(), json.dumps()
   - CSV: csv.reader(), csv.writer()

4. 选择依据：
   - 复杂数据 → JSON
   - 表格数据 → CSV
```

---

## 🤔 思考题

1. 为什么 JSON 的键要用双引号？
2. CSV 和 Excel 的表格有什么区别？
3. 如果你要设计一个 API，你会用 JSON 还是 CSV 返回数据？为什么？

---

**下一步**: [4.2 网络基础：HTTP 与 URL](./02-network-basics.md)
