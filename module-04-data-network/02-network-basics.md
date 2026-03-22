# 4.2 网络基础：HTTP 与 URL

> 理解互联网如何工作

---

## 🎯 学习目标

学完本课后，你将能够：

- [ ] 理解 URL 的结构
- [ ] 理解 HTTP 请求和响应
- [ ] 识别常见的 HTTP 方法
- [ ] 理解状态码的含义

---

## 💭 从一个问题开始

**当你在浏览器输入网址时，发生了什么？**

```
你输入：https://www.example.com
        ↓
    浏览器发送请求
        ↓
    服务器处理请求
        ↓
    服务器返回网页
        ↓
    浏览器显示网页
```

这就是**网络通信**的基本过程。

---

## 💡 核心概念

### URL：统一资源定位符

> **URL = 网络资源的地址**

```
https://www.example.com:8080/path/to/file?name=value#section
│      │              │     │              │           │
│      │              │     │              │           └─ 片段
│      │              │     │              └─ 查询参数
│      │              │     └─ 路径
│      │              └─ 端口
│      └─ 域名
└─ 协议
```

### URL 的组成部分

| 部分 | 例子 | 说明 |
|------|------|------|
| 协议 | `https` | 通信规则 |
| 域名 | `www.example.com` | 服务器地址 |
| 端口 | `:8080` | 通信端口（可省略） |
| 路径 | `/path/to/file` | 资源位置 |
| 查询 | `?name=value` | 额外参数 |
| 片段 | `#section` | 页面内位置 |

### 常见协议

| 协议 | 用途 |
|------|------|
| `http` | 普通网页浏览（不安全） |
| `https` | 安全网页浏览（加密） |
| `ftp` | 文件传输 |
| `mailto` | 发送邮件 |

---

## 🌐 HTTP 协议

### HTTP 是什么？

> **HTTP = HyperText Transfer Protocol**

浏览器和服务器通信的规则。

### 请求 - 响应模型

```
客户端（浏览器）         服务器
      │                    │
      │   HTTP 请求        │
      │ ─────────────────> │
      │                    │ 处理请求
      │                    │
      │   HTTP 响应        │
      │ <───────────────── │
      │                    │
```

### HTTP 请求

```http
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html
```

**组成部分**：
- 请求行：`GET /index.html HTTP/1.1`
- 请求头：`Host: ...`, `User-Agent: ...`
- 请求体：（可选，POST 请求时有数据）

### HTTP 响应

```http
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234

<html>...</html>
```

**组成部分**：
- 状态行：`HTTP/1.1 200 OK`
- 响应头：`Content-Type: ...`
- 响应体：HTML 内容

---

## 🔢 HTTP 状态码

### 常见状态码

| 状态码 | 含义 | 说明 |
|--------|------|------|
| **200** | OK | 请求成功 |
| **201** | Created | 资源创建成功 |
| **301** | Moved Permanently | 永久重定向 |
| **302** | Found | 临时重定向 |
| **400** | Bad Request | 请求格式错误 |
| **401** | Unauthorized | 未授权 |
| **403** | Forbidden | 禁止访问 |
| **404** | Not Found | 资源不存在 |
| **500** | Internal Server Error | 服务器错误 |
| **503** | Service Unavailable | 服务不可用 |

### 状态码分类

```
1xx: 信息（很少见）
2xx: 成功（200, 201, 204...）
3xx: 重定向（301, 302, 304...）
4xx: 客户端错误（400, 401, 403, 404...）
5xx: 服务器错误（500, 502, 503...）
```

---

## 🔄 HTTP 方法

### 常见方法

| 方法 | 用途 | 例子 |
|------|------|------|
| `GET` | 获取资源 | 浏览网页 |
| `POST` | 提交数据 | 提交表单 |
| `PUT` | 更新资源 | 修改资料 |
| `DELETE` | 删除资源 | 删除文章 |
| `PATCH` | 部分更新 | 修改部分字段 |

### 类比：CRUD 操作

```
CREATE（创建） → POST
READ（读取）   → GET
UPDATE（更新） → PUT/PATCH
DELETE（删除） → DELETE
```

### 示例

```http
# GET 请求：获取用户信息
GET /users/123 HTTP/1.1

# POST 请求：创建新用户
POST /users HTTP/1.1
Content-Type: application/json

{"name": "Alice", "email": "alice@example.com"}

# DELETE 请求：删除用户
DELETE /users/123 HTTP/1.1
```

---

## 🧪 用 curl 测试 HTTP

### 基本用法

```bash
# GET 请求
curl https://www.example.com

# 显示响应头
curl -I https://www.example.com

# 显示详细信息
curl -v https://www.example.com

# 保存响应到文件
curl -o page.html https://www.example.com
```

### 查看状态码

```bash
curl -I https://www.example.com
# HTTP/1.1 200 OK

curl -I https://www.example.com/nonexistent
# HTTP/1.1 404 Not Found
```

### 带参数请求

```bash
# 查询参数
curl "https://api.example.com/users?id=123"

# POST 请求
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name": "Alice"}'
```

---

## 🧪 代码示例

### 示例 1：Python 发送 HTTP 请求

```python
import requests

# GET 请求
response = requests.get("https://api.github.com")

print(f"Status: {response.status_code}")  # 200
print(f"Headers: {response.headers}")
print(f"Body: {response.text}")
```

### 示例 2：处理 API 响应

```python
import requests

response = requests.get("https://api.github.com/users/octocat")

if response.status_code == 200:
    data = response.json()
    print(f"Username: {data['login']}")
    print(f"Name: {data['name']}")
    print(f"Public repos: {data['public_repos']}")
else:
    print(f"Error: {response.status_code}")
```

---

## 💡 实践技巧

### URL 编码

```
特殊字符需要编码：
空格 → %20
中文 → %E4%B8%AD%E6%96%87
& → %26
```

### HTTPS 的重要性

```
HTTP:  数据明文传输，可能被窃听
HTTPS: 数据加密传输，更安全

🔒 浏览器地址栏的锁图标表示 HTTPS
```

### 调试网络请求

```bash
# 浏览器开发者工具
# F12 → Network 标签

# 或用 curl 测试
curl -v https://api.example.com
```

---

## 📝 关键术语

| 术语 | 英文 | 解释 |
|------|------|------|
| URL | URL | 统一资源定位符 |
| HTTP | HTTP | 超文本传输协议 |
| HTTPS | HTTPS | 安全的 HTTP |
| 请求 | Request | 客户端发给服务器 |
| 响应 | Response | 服务器返回客户端 |
| 状态码 | Status Code | 响应状态代码 |
| 方法 | Method | GET, POST, PUT, DELETE |
| 头 | Header | 请求/响应的元数据 |

---

## ✅ 本课小结

```
核心要点：

1. URL 结构：
   协议://域名：端口/路径？参数#片段

2. HTTP 模型：
   - 请求 - 响应
   - 无状态协议

3. HTTP 方法：
   - GET: 获取
   - POST: 提交
   - PUT: 更新
   - DELETE: 删除

4. 状态码：
   - 200: 成功
   - 404: 未找到
   - 500: 服务器错误
```

---

## 🤔 思考题

1. HTTP 和 HTTPS 有什么区别？
2. 为什么 DELETE 请求不常用于浏览器地址栏？
3. 404 和 500 错误有什么区别？

---

**下一步**: [4.3 API 基础概念](./03-api-basics.md)
