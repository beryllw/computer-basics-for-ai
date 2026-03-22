# Final Assessment - 课程综合评估

> 综合评估你对整个课程的掌握程度

---

## 📋 评估说明

- **覆盖内容**: 全部 5 个模块
- **建议时间**: 90-120 分钟
- **通过标准**: 75% 正确率
- **允许使用**: 课程文档、命令速查表、资源文件
- **不允许使用**: AI 助手、搜索引擎、他人帮助

---

## 第一部分：综合选择题（每题 4 分，共 40 分）

### 1. 以下哪项最好地描述了"计算"的本质？

A. 执行数学运算
B. 运行计算机程序
C. 按规则处理信息得到新信息
D. 解决复杂问题

### 2. 十进制数字 15 的二进制表示是？

A. 1110
B. 1111
C. 1011
D. 1101

### 3. 在 Linux 中，如何将文件 `a.txt` 复制到目录 `backup/` 并重命名为 `b.txt`？

A. `cp a.txt backup/`
B. `cp a.txt backup/b.txt`
C. `mv a.txt backup/b.txt`
D. `copy a.txt backup/b.txt`

### 4. 以下 Python 代码的输出是什么？

```python
x = [1, 2, 3]
y = x
y.append(4)
print(x)
```

A. [1, 2, 3]
B. [1, 2, 3, 4]
C. [4, 1, 2, 3]
D. 错误

### 5. 以下哪个是有效的 JSON 格式？

A. `{"name": "Alice", "skills": ["Python", "AI"]}`
B. `{'name': 'Alice', 'skills': ['Python', 'AI']}`
C. `{"name": Alice, "skills": [Python, AI]}`
D. `{name: "Alice", skills: ["Python", "AI"]}`

### 6. HTTP 状态码 500 表示什么？

A. 请求成功
B. 未授权
C. 资源未找到
D. 服务器内部错误

### 7. 调用 REST API 获取资源，应该使用哪个 HTTP 方法？

A. GET
B. POST
C. PUT
D. DELETE

### 8. 关于 AI 大模型，以下说法正确的是？

A. AI 完全理解它生成的内容
B. AI 是下一个词预测器
C. AI 永远不会犯错
D. AI 有自我意识

### 9. Token 在 AI 上下文中的含义是？

A. 登录凭证
B. 加密货币
C. AI 处理文本的单位
D. 数据加密密钥

### 10. 以下哪种人机协作模式最有效？

A. AI 生成，人类直接使用
B. 人类设定目标，AI 生成，人类审查
C. 完全依赖 AI
D. 完全不用 AI

---

## 第二部分：命令和代码写作（每题 10 分，共 40 分）

### 11. Linux 命令组合

写出完成以下任务的命令：

有一个目录 `logs/` 包含多个 `.log` 文件：

a) 找出所有包含 "ERROR" 的行
b) 统计错误总数
c) 将错误按时间排序后保存到 `errors_sorted.txt`
d) 显示前 10 个错误

```bash
# 你的答案：

```

### 12. Python 数据处理

编写一个函数，完成以下功能：

```python
def analyze_numbers(numbers):
    """
    分析数字列表

    参数：numbers - 整数列表

    返回：字典，包含：
        - total: 总和
        - count: 数量
        - average: 平均值
        - max: 最大值
        - min: 最小值

    如果列表为空，返回 None
    """
    # 你的代码

# 测试
print(analyze_numbers([1, 2, 3, 4, 5]))
# 应输出：{'total': 15, 'count': 5, 'average': 3.0, 'max': 5, 'min': 1}
```

### 13. API 调用

编写代码调用 API 并处理响应：

```python
import requests

def get_user_posts(user_id):
    """
    从 API 获取用户的所有帖子

    参数：user_id - 用户 ID

    返回：帖子列表（只包含 title 字段）

    API: https://jsonplaceholder.typicode.com/posts?userId={user_id}
    """
    # 你的代码

# 测试
titles = get_user_posts(1)
for title in titles[:3]:
    print(title)
```

### 14. JSON 处理

编写代码处理 JSON 数据：

```python
import json

def process_user_data(json_string):
    """
    解析 JSON 字符串，提取信息

    参数：json_string - 包含用户数据的 JSON

    返回：格式化字符串 "姓名 (邮箱): 技能数量"

    示例输入：
    '{"name": "Alice", "email": "alice@example.com", "skills": ["A", "B", "C"]}'

    示例输出：
    "Alice (alice@example.com): 3 skills"
    """
    # 你的代码
```

---

## 第三部分：代码阅读和调试（20 分）

### 15. 代码分析（10 分）

阅读以下代码，回答问题：

```python
import requests

def fetch_and_save(url, filename):
    try:
        response = requests.get(url, timeout=10)
        response.raise_for_status()

        data = response.json()

        with open(filename, "w") as f:
            json.dump(data, f, indent=2)

        return {"success": True, "message": f"Saved {len(data)} items"}

    except requests.exceptions.Timeout:
        return {"success": False, "message": "Request timed out"}
    except requests.exceptions.HTTPError as e:
        return {"success": False, "message": f"HTTP error: {e}"}
    except Exception as e:
        return {"success": False, "message": f"Error: {e}"}
```

**问题**：

a) 这个函数的主要功能是什么？（3 分）

b) 列举可能返回的三种错误情况。（3 分）

c) 如果要添加对 JSON 解析错误的处理，应该如何修改？（4 分）

### 16. 调试题（10 分）

以下代码有 bug，请找出并修复：

```python
def calculate_stats(data):
    """计算数据的统计信息"""
    total = 0
    count = 0

    for item in data:
        total += item
        count += 1

    average = total / count

    return {
        "total": total,
        "count": count,
        "average": average
    }

# 测试
print(calculate_stats([1, 2, 3, 4, 5]))  # 正常工作
print(calculate_stats([]))  # 会出什么问题？如何修复？
```

**问题**：
a) 当输入空列表时会发生什么？（2 分）
b) 如何修复？写出完整的修复代码。（8 分）

---

## 第四部分：综合应用题（30 分）

### 17. 完整项目设计

**场景**：你需要构建一个"每日新闻摘要"系统。

**需求**：
1. 从 API 获取新闻数据
2. 过滤出特定类别的新闻
3. 生成摘要
4. 保存到文件
5. 可以用 AI 帮助生成更自然的摘要

**可用资源**：
- 新闻 API: `https://api.news.com/headlines?category={category}`
- AI API（可选）：用于生成摘要
- Python 和 Linux 工具

**任务**：设计并实现这个系统（可以用伪代码）

```
你的设计：

1. 系统架构（5 分）


2. 数据获取模块（5 分）


3. 数据处理模块（5 分）


4. 摘要生成模块（5 分）


5. 文件保存模块（5 分）


6. 错误处理（5 分）
```

---

## 第五部分：反思题（Bonus 20 分）

### 18. 学习反思

a) 通过这门课程，你最大的收获是什么？（5 分）

b) 哪个概念最初最难理解，现在明白了？（5 分）

c) 你计划如何将所学应用于实际工作/学习？（5 分）

d) 给未来学习这门课的学弟学妹一条建议。（5 分）

---

## 📝 答案纸

```
姓名：__________  日期：__________

### 选择题
1. ___  2. ___  3. ___  4. ___  5. ___
6. ___  7. ___  8. ___  9. ___  10. ___

### 命令和代码写作
11.

12.

13.

14.

### 代码阅读和调试
15a.
15b.
15c.

16a.
16b.

### 综合应用题
17.

### 反思题（Bonus）
18a.
18b.
18c.
18d.
```

---

## ✅ 评估完成检查清单

完成评估后，检查：

```
□ 所有选择题已作答
□ 所有代码写作题已完成
□ 代码阅读题已回答
□ 调试题已找出并修复 bug
□ 综合应用题有完整设计
□ 反思题已填写（如选做）
```

---

## 🎓 课程完成证书

**完成本课程所有要求后**：
- ✅ 完成 5 个模块的学习
- ✅ 完成 10 个实验
- ✅ 通过 4 个 Checkpoint 评估
- ✅ 通过 Final Assessment

**恭喜你！** 🎉

你已掌握：
- 计算机思维基础
- Linux 工具使用
- Python 代码阅读
- 数据格式和 API 调用
- AI 协作能力

**下一步**：查看 [resources/next-steps.md](../resources/next-steps.md) 继续学习！

---

## 评分标准

| 部分 | 总分 | 得分 |
|------|------|------|
| 选择题 | 40 | |
| 命令和代码写作 | 40 | |
| 代码阅读和调试 | 20 | |
| 综合应用题 | 30 | |
| 反思题（Bonus） | 20 | |
| **总计** | **150** | |

**通过分数**: 113 分（75%）
**优秀分数**: 135 分（90%）
