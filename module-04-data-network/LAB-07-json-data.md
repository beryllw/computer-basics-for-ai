# 实验 LAB-07：处理 JSON 数据

> 动手练习 JSON 数据的读取、解析和写入

---

## 🎯 实验目标

- [ ] 能够读取和解析 JSON 数据
- [ ] 能够操作 JSON 数据
- [ ] 能够将数据写入 JSON 文件
- [ ] 理解嵌套 JSON 结构

---

## 📋 准备工作

```bash
# 创建实验目录
mkdir -p ~/computer-basics/module-04/lab07
cd ~/computer-basics/module-04/lab07
```

---

## 第一部分：解析 JSON 数据 (20 分钟)

### 任务 1.1：创建示例 JSON 文件

创建文件 `users.json`：

```json
{
  "users": [
    {
      "id": 1,
      "name": "Alice",
      "email": "alice@example.com",
      "age": 25,
      "city": "Beijing",
      "skills": ["Python", "JavaScript", "SQL"]
    },
    {
      "id": 2,
      "name": "Bob",
      "email": "bob@example.com",
      "age": 30,
      "city": "Shanghai",
      "skills": ["Java", "Python", "DevOps"]
    },
    {
      "id": 3,
      "name": "Charlie",
      "email": "charlie@example.com",
      "age": 28,
      "city": "Guangzhou",
      "skills": ["Python", "Data Science", "ML"]
    }
  ]
}
```

### 任务 1.2：编写解析代码

创建 `parse_json.py`：

```python
import json

# 读取 JSON 文件
with open("users.json") as f:
    data = json.load(f)

# 访问数据
print(f"Total users: {len(data['users'])}")

# 遍历用户
for user in data["users"]:
    print(f"\nName: {user['name']}")
    print(f"Email: {user['email']}")
    print(f"Skills: {', '.join(user['skills'])}")
```

### 任务 1.3：运行验证

```bash
python3 parse_json.py
```

**预期输出**：
```
Total users: 3

Name: Alice
Email: alice@example.com
Skills: Python, JavaScript, SQL

Name: Bob
Email: bob@example.com
Skills: Java, Python, DevOps

Name: Charlie
Email: charlie@example.com
Skills: Python, Data Science, ML
```

---

## 第二部分：过滤和查询 (25 分钟)

### 任务 2.1：按条件过滤

在 `parse_json.py` 中添加：

```python
# 找出所有会 Python 的用户
print("\n=== Python Developers ===")
for user in data["users"]:
    if "Python" in user["skills"]:
        print(f"- {user['name']} ({user['email']})")

# 找出年龄大于 27 的用户
print("\n=== Age > 27 ===")
for user in data["users"]:
    if user["age"] > 27:
        print(f"- {user['name']}: {user['age']} years old")
```

### 任务 2.2：数据转换

创建 `transform.py`：

```python
import json

with open("users.json") as f:
    data = json.load(f)

# 转换为新格式
simple_list = []
for user in data["users"]:
    simple_list.append({
        "name": user["name"],
        "skill_count": len(user["skills"])
    })

# 输出新格式
print(json.dumps(simple_list, indent=2))
```

**预期输出**：
```json
[
  {
    "name": "Alice",
    "skill_count": 3
  },
  {
    "name": "Bob",
    "skill_count": 3
  },
  {
    "name": "Charlie",
    "skill_count": 3
  }
]
```

---

## 第三部分：创建和写入 JSON (25 分钟)

### 任务 3.1：创建数据

创建 `create_json.py`：

```python
import json

# 创建数据
new_user = {
    "id": 4,
    "name": "Diana",
    "email": "diana@example.com",
    "age": 26,
    "city": "Shenzhen",
    "skills": ["Python", "Frontend", "Design"]
}

# 读取现有数据
with open("users.json") as f:
    data = json.load(f)

# 添加新用户
data["users"].append(new_user)

# 写回文件
with open("users.json", "w") as f:
    json.dump(data, f, indent=2)

print("User added successfully!")
```

### 任务 3.2：验证结果

```bash
# 运行脚本
python3 create_json.py

# 查看更新后的文件
cat users.json
```

**验证**：
- 文件中应该有 4 个用户
- Diana 的信息应该正确

---

## 第四部分：综合练习 (30 分钟)

### 任务：分析 API 响应

创建 `api_response.json`：

```json
{
  "status": "success",
  "data": {
    "repos": [
      {
        "name": "project-a",
        "stars": 150,
        "forks": 30,
        "language": "Python",
        "updated_at": "2026-03-20"
      },
      {
        "name": "project-b",
        "stars": 89,
        "forks": 12,
        "language": "JavaScript",
        "updated_at": "2026-03-21"
      },
      {
        "name": "project-c",
        "stars": 234,
        "forks": 45,
        "language": "Python",
        "updated_at": "2026-03-19"
      }
    ]
  },
  "total_count": 3
}
```

创建 `analyze.py`，完成以下任务：

```python
import json

# 1. 读取 JSON 文件
with open("api_response.json") as f:
    data = json.load(f)

# 2. 检查状态
if data["status"] != "success":
    print("Error: Request failed")
    exit(1)

# 3. 统计信息
repos = data["data"]["repos"]
total_stars = sum(r["stars"] for r in repos)
total_forks = sum(r["forks"] for r in repos)
avg_stars = total_stars / len(repos)

print(f"=== Repository Analysis ===")
print(f"Total repos: {len(repos)}")
print(f"Total stars: {total_stars}")
print(f"Total forks: {total_forks}")
print(f"Average stars: {avg_stars:.1f}")

# 4. 按语言分组
print(f"\n=== By Language ===")
languages = {}
for repo in repos:
    lang = repo["language"]
    if lang not in languages:
        languages[lang] = {"count": 0, "stars": 0}
    languages[lang]["count"] += 1
    languages[lang]["stars"] += repo["stars"]

for lang, stats in languages.items():
    print(f"{lang}: {stats['count']} repos, {stats['stars']} stars")

# 5. 找出最 starred 的项目
most_starred = max(repos, key=lambda r: r["stars"])
print(f"\n=== Most Popular ===")
print(f"{most_starred['name']}: {most_starred['stars']} stars")
```

**预期输出**：
```
=== Repository Analysis ===
Total repos: 3
Total stars: 473
Total forks: 87
Average stars: 157.7

=== By Language ===
Python: 2 repos, 384 stars
JavaScript: 1 repos, 89 stars

=== Most Popular ===
project-c: 234 stars
```

---

## 📝 实验报告

```markdown
# LAB-07 实验报告

姓名：__________  日期：__________

## 任务完成情况

### 第一部分：解析 JSON
- [ ] 创建了 users.json
- [ ] 编写了解析代码
- [ ] 正确输出结果

### 第二部分：过滤和查询
- [ ] 实现了条件过滤
- [ ] 实现了数据转换

### 第三部分：创建和写入
- [ ] 添加了新用户
- [ ] 验证了结果

### 第四部分：综合练习
- [ ] 完成了 API 响应分析
- [ ] 输出了正确统计

## 遇到的问题

## 最大的收获
```

---

## 🔗 相关资源

- [4.1 数据格式：JSON 与 CSV](./01-data-formats.md)
- [resources/glossary.md](../resources/glossary.md)

---

**完成 LAB-07 后**，继续 [LAB-08: API 调用练习](./LAB-08-api-calls.md)
