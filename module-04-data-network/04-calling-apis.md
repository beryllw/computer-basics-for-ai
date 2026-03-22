# 4.4 调用 API 获取数据

> 动手实践：使用 API 获取真实数据

---

## 🎯 学习目标

学完本课后，你将能够：

- [ ] 调用公开的 API 获取数据
- [ ] 处理 API 响应
- [ ] 理解并处理常见错误
- [ ] 将 API 数据用于实际场景

---

## 💭 从一个问题开始

**如何用程序获取实时数据？**

- 天气预报
- 股票价格
- 新闻文章
- AI 模型响应

答案：**调用 API**

---

## 🧪 公开 API 推荐

### 无需认证的 API（适合练习）

| API | 用途 | URL |
|-----|------|-----|
| JSONPlaceholder | 模拟数据 | `https://jsonplaceholder.typicode.com` |
| Cat Facts | 猫咪事实 | `https://catfact.ninja/fact` |
| Dad Jokes | 冷笑话 | `https://icanhazdadjoke.com` |
| PokeAPI | 宝可梦数据 | `https://pokeapi.co` |
| Chuck Norris | 名人名言 | `https://api.chucknorris.io` |

### 需要认证的 API（进阶）

| API | 用途 | 认证 |
|-----|------|------|
| GitHub API | 代码仓库 | Token |
| OpenWeatherMap | 天气数据 | API Key |
| Twitter API | 社交媒体 | OAuth |
| Google Maps | 地图服务 | API Key |

---

## 🔧 准备工作

### 安装 requests 库

```bash
pip install requests
```

### 测试连接

```python
import requests

response = requests.get("https://httpbin.org/get")
print(response.status_code)  # 应该是 200
```

---

## 📚 实战示例

### 示例 1：获取随机猫咪事实

```python
import requests

# API 端点
url = "https://catfact.ninja/fact"

# 发送请求
response = requests.get(url)

# 检查响应
if response.status_code == 200:
    data = response.json()
    print(f"Cat Fact: {data['fact']}")
    print(f"Length: {data['length']}")
else:
    print(f"Error: {response.status_code}")
```

**响应示例**：
```json
{
  "fact": "Cats have 32 muscles in each ear.",
  "length": 36
}
```

---

### 示例 2：获取用户列表（分页）

```python
import requests

# 获取第一页用户
url = "https://jsonplaceholder.typicode.com/users"
params = {"page": 1}

response = requests.get(url, params=params)
users = response.json()

# 打印用户信息
for user in users[:3]:
    print(f"Name: {user['name']}")
    print(f"Email: {user['email']}")
    print(f"City: {user['address']['city']}")
    print("---")
```

**响应示例**：
```json
[
  {
    "id": 1,
    "name": "Leanne Graham",
    "email": "Sincere@april.biz",
    "address": {
      "city": "Gwenborough"
    }
  },
  ...
]
```

---

### 示例 3：获取帖子并过滤

```python
import requests

# 获取所有帖子
url = "https://jsonplaceholder.typicode.com/posts"
response = requests.get(url)
posts = response.json()

# 过滤：只看 userId 为 1 的帖子
user1_posts = [p for p in posts if p["userId"] == 1]

print(f"User 1 has {len(user1_posts)} posts")

# 显示前 3 个
for post in user1_posts[:3]:
    print(f"\nTitle: {post['title']}")
    print(f"Body: {post['body'][:50]}...")
```

---

### 示例 4：创建新资源（POST）

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"

# 要创建的数据
new_post = {
    "title": "My First Post",
    "body": "This is the content of my post.",
    "userId": 1
}

# 发送 POST 请求
response = requests.post(url, json=new_post)

# 检查响应
print(f"Status: {response.status_code}")
created = response.json()
print(f"Created post with ID: {created['id']}")
```

**注意**：JSONPlaceholder 是模拟 API，不会真正保存数据。

---

### 示例 5：更新资源（PUT）

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

# 更新的数据
updated_post = {
    "id": 1,
    "title": "Updated Title",
    "body": "Updated content",
    "userId": 1
}

# 发送 PUT 请求
response = requests.put(url, json=updated_post)

print(f"Status: {response.status_code}")
print(f"Response: {response.json()}")
```

---

### 示例 6：删除资源（DELETE）

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

# 发送 DELETE 请求
response = requests.delete(url)

print(f"Status: {response.status_code}")
# 200 表示删除成功
```

---

## 🛠️ 错误处理

### 常见错误及处理

```python
import requests

def safe_api_call():
    url = "https://api.example.com/data"

    try:
        response = requests.get(url, timeout=5)

        # 检查 HTTP 状态码
        if response.status_code == 200:
            return response.json()
        elif response.status_code == 404:
            print("Resource not found")
            return None
        elif response.status_code == 401:
            print("Unauthorized - check your API key")
            return None
        else:
            print(f"Error: {response.status_code}")
            return None

    except requests.exceptions.Timeout:
        print("Request timed out")
        return None
    except requests.exceptions.ConnectionError:
        print("Connection error - check your internet")
        return None
    except requests.exceptions.RequestException as e:
        print(f"Request failed: {e}")
        return None

# 使用
data = safe_api_call()
if data:
    print("Got data successfully")
```

### 错误码速查

| 状态码 | 含义 | 如何处理 |
|--------|------|----------|
| 200 | 成功 | 正常处理数据 |
| 400 | 请求错误 | 检查请求参数 |
| 401 | 未授权 | 检查 API Key/Token |
| 403 | 禁止访问 | 检查权限 |
| 404 | 未找到 | 检查 URL |
| 429 | 请求太多 | 等待后重试 |
| 500 | 服务器错误 | 稍后重试 |
| 503 | 服务不可用 | 稍后重试 |

---

## 🧪 综合项目：天气查询器

```python
"""
简单天气查询器
使用 Open-Meteo API（免费，无需认证）
"""

import requests

def get_weather(city_name, lat, lon):
    """获取天气数据"""

    url = "https://api.open-meteo.com/v1/forecast"
    params = {
        "latitude": lat,
        "longitude": lon,
        "current_weather": True
    }

    response = requests.get(url, params=params)

    if response.status_code == 200:
        data = response.json()
        weather = data["current_weather"]

        print(f"\n🌤️  {city_name} 天气")
        print(f"温度：{weather['temperature']}°C")
        print(f"风速：{weather['windspeed']} km/h")
        print(f"天气代码：{weather['weathercode']}")
    else:
        print(f"获取天气失败：{response.status_code}")

# 一些城市的坐标
cities = {
    "北京": (39.9042, 116.4074),
    "上海": (31.2304, 121.4737),
    "广州": (23.1291, 113.2644),
    "深圳": (22.5431, 114.0579),
}

# 查询北京天气
get_weather("北京", *cities["北京"])
```

---

## 💡 实践技巧

### 1. 限制请求频率

```python
import time

for i in range(10):
    response = requests.get("https://api.example.com/data")
    # 处理数据...

    time.sleep(1)  # 每秒最多 1 次请求
```

### 2. 使用会话复用连接

```python
import requests

session = requests.Session()

# 多次请求
for i in range(5):
    response = session.get(f"https://api.example.com/data/{i}")
```

### 3. 缓存响应

```python
import requests
import json

def get_with_cache(url, cache_file="cache.json"):
    # 尝试从缓存读取
    try:
        with open(cache_file) as f:
            cache = json.load(f)
            if url in cache:
                print("Using cached data")
                return cache[url]
    except:
        pass

    # 从 API 获取
    response = requests.get(url)
    data = response.json()

    # 保存到缓存
    cache[url] = data
    with open(cache_file, "w") as f:
        json.dump(cache, f)

    return data
```

---

## 📝 关键术语

| 术语 | 英文 | 解释 |
|------|------|------|
| 端点 | Endpoint | API 的 URL |
| 参数 | Parameter | 传递给 API 的值 |
| 响应体 | Response Body | API 返回的数据 |
| 超时 | Timeout | 请求等待时间 |
| 认证 | Authentication | 验证身份 |
| 速率限制 | Rate Limit | 每秒请求次数限制 |

---

## ✅ 本课小结

```
核心要点：

1. 调用 API 的步骤：
   - 确定端点 URL
   - 准备参数
   - 发送请求
   - 处理响应

2. 错误处理：
   - 检查状态码
   - 处理网络异常
   - 合理重试

3. 最佳实践：
   - 限制请求频率
   - 缓存响应数据
   - 保护 API Key

4. 练习资源：
   - JSONPlaceholder
   - Cat Facts
   - 其他公开 API
```

---

## 🧪 练习

1. 用 JSONPlaceholder 获取一个用户的所有帖子
2. 获取一只随机猫咪的图片（使用 TheCatAPI）
3. 创建一个函数，根据用户 ID 获取用户信息

---

## 🤔 思考题

1. 为什么要限制 API 请求频率？
2. 如果 API 返回的数据格式变了，你的代码会怎样？
3. 如何保护你的 API Key 不被泄露？

---

**下一步**: [LAB-07: 处理 JSON 数据](./LAB-07-json-data.md)

---

**Module 4 完成！** 🎉

继续学习 [模块 5：系统与 AI 准备](../module-05-systems-ai-prep/README.md)
