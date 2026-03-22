# Checkpoint 03 - 模块 4 评估

> 评估你对数据格式和网络 API 的理解

---

## 📋 评估说明

- **覆盖内容**: 模块 4（数据与网络）
- **建议时间**: 45-60 分钟
- **通过标准**: 70% 正确率
- **允许使用**: notes、资源文档、命令速查表
- **不允许使用**: AI 助手、搜索引擎、实际运行代码

---

## 第一部分：数据格式选择题（每题 5 分，共 25 分）

### 1. JSON 中如何表示对象？

A. `[ ]`
B. `{ }`
C. `( )`
D. `< >`

### 2. 以下哪个是有效的 JSON？

A. `{'name': 'Alice', 'age': 25}`
B. `{"name": "Alice", "age": 25}`
C. `{"name": Alice, "age": 25}`
D. `{name: "Alice", age: 25}`

### 3. CSV 文件最适合存储什么类型的数据？

A. 嵌套的树状数据
B. 表格数据
C. 图像数据
D. 音频数据

### 4. 在 Python 中，如何解析 JSON 字符串？

A. `json.parse()`
B. `json.loads()`
C. `json.read()`
D. `json.decode()`

### 5. JSON 中的 `null` 对应 Python 中的什么？

A. `null`
B. `None`
C. `nil`
D. `undefined`

---

## 第二部分：网络基础选择题（每题 5 分，共 25 分）

### 6. URL 中 `https` 表示什么？

A. 超文本标记语言
B. 超文本传输协议安全版
C. 主机传输系统
D. 混合传输标准

### 7. HTTP 状态码 200 表示什么？

A. 请求失败
B. 服务器错误
C. 请求成功
D. 未授权

### 8. 以下哪个 HTTP 方法用于获取数据？

A. POST
B. PUT
C. GET
D. DELETE

### 9. HTTP 状态码 404 表示什么？

A. 服务器错误
B. 未授权
C. 请求格式错误
D. 资源未找到

### 10. 哪个 HTTP 方法通常用于创建新资源？

A. GET
B. POST
C. PUT
D. DELETE

---

## 第三部分：API 理解题（每题 10 分，共 30 分）

### 11. API 是什么的缩写？解释其作用。

### 12. 为什么 API 通常需要认证？列举两种常见的认证方式。

### 13. 解释 REST API 的核心特点。

---

## 第四部分：代码阅读题（20 分）

### 14. 阅读以下代码，回答问题

```python
import requests

def fetch_user(user_id):
    url = f"https://api.example.com/users/{user_id}"

    try:
        response = requests.get(url)
        response.raise_for_status()
        return response.json()
    except requests.exceptions.HTTPError as e:
        if response.status_code == 404:
            return {"error": "User not found"}
        return {"error": f"HTTP error: {e}"}
    except requests.exceptions.RequestException as e:
        return {"error": f"Request failed: {e}"}

# 使用
result = fetch_user(123)
if "error" in result:
    print(f"Error: {result['error']}")
else:
    print(f"User: {result['name']}")
```

**问题**：

a) 这个函数的作用是什么？（5 分）

b) 如果用户不存在（返回 404），会输出什么？（5 分）

c) `response.raise_for_status()` 的作用是什么？（5 分）

d) 如果网络断开，会输出什么？（5 分）

---

## 第五部分：实践题（20 分）

### 15. 设计 API 调用

**场景**：你需要调用一个天气 API 获取某个城市的天气数据。

**API 文档**：
- 端点：`https://api.weather.com/v1/current`
- 参数：`city`（城市名）、`units`（单位：metric 或 imperial）
- 返回：JSON 格式，包含 `temperature`、`humidity`、`condition` 字段

**任务**：

1. 写出调用这个 API 的 Python 代码（10 分）
2. 添加错误处理（5 分）
3. 提取并打印温度（5 分）

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

### 简答题
11.


12.


13.


### 代码阅读题
14a.
14b.
14c.
14d.

### 实践题
15.
```

---

## ✅ 参考答案

<details>
<summary>点击展开答案</summary>

### 选择题
1. B
2. B
3. B
4. B
5. B
6. B
7. C
8. C
9. D
10. B

### 简答题
11. API = Application Programming Interface。作用是让不同的应用程序可以相互通信。

12. 认证用于：确认用户身份、控制访问权限、防止滥用。
    认证方式：API Key、Bearer Token、Basic Auth、OAuth 等。

13. REST 特点：
    - URL 表示资源
    - HTTP 方法表示操作（GET/POST/PUT/DELETE）
    - 通常使用 JSON 格式
    - 无状态

### 代码阅读题
14a. 获取用户信息，带有错误处理
14b. Error: User not found
14c. 如果 HTTP 状态码是错误（4xx/5xx），抛出异常
14d. Error: Request failed: [错误信息]

### 实践题
```python
import requests

def get_weather(city):
    url = "https://api.weather.com/v1/current"
    params = {"city": city, "units": "metric"}

    try:
        response = requests.get(url, params=params)
        response.raise_for_status()
        data = response.json()
        print(f"Temperature in {city}: {data['temperature']}°C")
        return data
    except requests.exceptions.RequestException as e:
        print(f"Error: {e}")
        return None

get_weather("Beijing")
```

</details>

---

**完成 Checkpoint 03 后**，继续学习 模块 5
