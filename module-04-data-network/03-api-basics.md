# 4.3 API 基础概念

> 理解应用程序如何相互通信

---

## 🎯 学习目标

学完本课后，你将能够：

- [ ] 理解 API 是什么
- [ ] 理解 REST API 的概念
- [ ] 识别 API 的组成部分
- [ ] 理解 API 认证的基础

---

## 💭 从一个问题开始

**App 之间如何"对话"？**

想象两个场景：

1. **天气预报 App** 如何获取天气数据？
   - 从气象局的服务器获取

2. **微信登录** 为什么能用 QQ 账号？
   - QQ 提供了登录 API

**API = 应用程序之间的桥梁**

---

## 💡 核心概念

### API 是什么？

> **API = Application Programming Interface**

应用程序之间通信的规则和方式。

### 类比：餐厅点餐

```
你（客户端）    服务员（API）    厨房（服务器）
     │              │              │
     │  点餐        │              │
     │ ───────────> │              │
     │              │  下单        │
     │              │ ───────────> │
     │              │              │ 做菜
     │              │  上菜        │
     │ <─────────── │              │
     │  用餐        │              │
```

**API 就像服务员**：
- 你不需要知道厨房怎么做菜
- 你只需要知道如何点餐
- 服务员传递你的请求和厨房的响应

---

## 🌐 Web API

### Web API 是什么？

通过 HTTP 协议提供的 API，也叫 **Web Service**。

```
你的程序  ──HTTP 请求──>  API 服务器
              │
              └── JSON 响应
```

### 常见用途

| 用途 | 例子 |
|------|------|
| 获取数据 | 天气、股票、新闻 |
| 提交数据 | 发布微博、发送邮件 |
| 调用服务 | AI 模型、翻译、支付 |
| 第三方登录 | 微信登录、Google 登录 |

---

## 🔧 REST API

### REST 是什么？

> **REST = Representational State Transfer**

一种 API 设计风格，最常用。

### REST 的核心原则

```
1. 资源用 URL 表示
   /users, /posts, /comments

2. 用 HTTP 方法表示操作
   GET = 读取
   POST = 创建
   PUT = 更新
   DELETE = 删除

3. 数据通常用 JSON 格式
   {"id": 1, "name": "Alice"}

4. 无状态
   每个请求包含所有必要信息
```

### RESTful URL 设计

```
GET    /users          # 获取所有用户
POST   /users          # 创建新用户
GET    /users/123      # 获取 ID 为 123 的用户
PUT    /users/123      # 更新用户 123
DELETE /users/123      # 删除用户 123

GET    /users/123/posts    # 获取用户 123 的所有帖子
GET    /posts/456/comments # 获取帖子 456 的评论
```

---

## 📋 API 的组成部分

### 1. 端点（Endpoint）

API 的 URL 地址。

```
https://api.github.com/users/octocat
│                    │
│                    └─ 端点路径
└─ 基础 URL
```

### 2. 请求方法

```
GET    /users    # 获取用户列表
POST   /users    # 创建用户
```

### 3. 请求头（Headers）

```
Authorization: Bearer xxxxx
Content-Type: application/json
```

### 4. 请求体（Body）

```json
{
  "name": "Alice",
  "email": "alice@example.com"
}
```

### 5. 响应

```json
{
  "id": 123,
  "name": "Alice",
  "created_at": "2026-03-22T10:30:00Z"
}
```

---

## 🔐 API 认证

### 为什么需要认证？

- 确认你是谁
- 控制访问权限
- 防止滥用

### 常见认证方式

| 方式 | 说明 | 例子 |
|------|------|------|
| API Key | 简单的密钥 | `?api_key=xxxx` |
| Bearer Token | JWT 令牌 | `Authorization: Bearer xxx` |
| Basic Auth | 用户名密码 | `Authorization: Basic xxx` |
| OAuth | 第三方授权 | 微信登录 |

### API Key 示例

```bash
# 在 URL 中
curl "https://api.weather.com/data?key=YOUR_KEY&city=Beijing"

# 在 Header 中
curl -H "X-API-Key: YOUR_KEY" \
     https://api.example.com/data
```

### Bearer Token 示例

```bash
curl -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIs..." \
     https://api.example.com/protected
```

---

## 🧪 用 curl 调用 API

### GitHub API 示例

```bash
# 获取用户信息（公开 API，无需认证）
curl https://api.github.com/users/octocat

# 响应
{
  "login": "octocat",
  "id": 1,
  "type": "User",
  ...
}
```

### 带参数的请求

```bash
# 查询参数
curl "https://api.github.com/search/repositories?q=python&sort=stars"
```

### 带认证的请求

```bash
# 使用 API Token
curl -H "Authorization: token YOUR_TOKEN" \
     https://api.github.com/user
```

---

## 🧪 Python 调用 API

### 使用 requests 库

```python
import requests

# 简单的 GET 请求
response = requests.get("https://api.github.com/users/octocat")

# 检查状态码
if response.status_code == 200:
    # 解析 JSON 响应
    data = response.json()
    print(f"Username: {data['login']}")
    print(f"Name: {data['name']}")
else:
    print(f"Error: {response.status_code}")
```

### 带参数的请求

```python
import requests

params = {
    "q": "python",
    "sort": "stars",
    "order": "desc"
}

response = requests.get(
    "https://api.github.com/search/repositories",
    params=params
)

data = response.json()
for repo in data["items"][:5]:
    print(f"{repo['name']}: {repo['stargazers_count']} ⭐")
```

### 带认证的请求

```python
import requests

headers = {
    "Authorization": "token YOUR_GITHUB_TOKEN"
}

response = requests.get(
    "https://api.github.com/user",
    headers=headers
)

user = response.json()
print(f"Logged in as: {user['login']}")
```

---

## 💡 实践技巧

### 阅读 API 文档

```
好的 API 文档包含：
1. 基础 URL
2. 端点列表
3. 请求方法
4. 参数说明
5. 响应格式
6. 认证方式
7. 错误码说明
```

### 测试 API

```bash
# 1. 用 curl 测试
curl https://api.example.com/endpoint

# 2. 检查响应
# - 状态码
# - 响应格式
# - 数据内容

# 3. 用 Python 编写代码
```

### 错误处理

```python
import requests

try:
    response = requests.get("https://api.example.com/data")
    response.raise_for_status()  # 如果状态码不是 2xx，抛出异常
    data = response.json()
except requests.exceptions.HTTPError as e:
    print(f"HTTP Error: {e}")
except requests.exceptions.RequestException as e:
    print(f"Request Error: {e}")
```

---

## 📝 关键术语

| 术语 | 英文 | 解释 |
|------|------|------|
| API | API | 应用程序接口 |
| REST | REST | API 设计风格 |
| 端点 | Endpoint | API 的 URL 地址 |
| 请求 | Request | 发给 API 的消息 |
| 响应 | Response | API 返回的消息 |
| 认证 | Authentication | 验证身份 |
| API Key | API Key | API 访问密钥 |
| Token | Token | 访问令牌 |

---

## ✅ 本课小结

```
核心要点：

1. API = 应用程序之间的桥梁

2. REST API 特点：
   - URL 表示资源
   - HTTP 方法表示操作
   - JSON 格式数据

3. API 组成部分：
   - 端点（URL）
   - 方法（GET/POST/PUT/DELETE）
   - 请求头
   - 请求体
   - 响应

4. 认证方式：
   - API Key
   - Bearer Token
   - OAuth
```

---

## 🤔 思考题

1. 为什么 API 要用 HTTP 方法表示操作，而不是都用 GET？
2. API Key 和 Bearer Token 有什么区别？
3. 如果你要设计一个 API，你会如何设计 URL 结构？

---

**下一步**: [4.4 调用 API 获取数据](./04-calling-apis.md)
