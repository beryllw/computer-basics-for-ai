# 实验 LAB-08：API 调用练习

> 动手调用真实 API 获取数据

---

## 🎯 实验目标

- [ ] 能够使用 Python 调用 API
- [ ] 能够处理 API 响应
- [ ] 能够处理常见错误
- [ ] 理解 API 的工作流程

---

## 📋 准备工作

```bash
# 创建实验目录
mkdir -p ~/computer-basics/module-04/lab08
cd ~/computer-basics/module-04/lab08

# 确保安装了 requests
pip install requests
```

---

## 第一部分：简单的 GET 请求 (20 分钟)

### 任务 1.1：测试连接

创建 `test_api.py`：

```python
import requests

# 测试 API（无需认证）
url = "https://httpbin.org/get"

response = requests.get(url)

print(f"Status Code: {response.status_code}")
print(f"Headers: {response.headers.get('Content-Type')}")
```

**预期输出**：
```
Status Code: 200
Headers: application/json
```

### 任务 1.2：获取猫咪事实

创建 `cat_facts.py`：

```python
import requests

url = "https://catfact.ninja/fact"

response = requests.get(url)

if response.status_code == 200:
    data = response.json()
    print(f"🐱 Cat Fact: {data['fact']}")
    print(f"Length: {data['length']}")
else:
    print(f"Error: {response.status_code}")
```

**运行多次**，看看不同的猫咪事实！

---

## 第二部分：带参数的请求 (25 分钟)

### 任务 2.1：用户查询

创建 `user_query.py`：

```python
import requests

# JSONPlaceholder - 模拟 API
url = "https://jsonplaceholder.typicode.com/users"

# 获取所有用户
response = requests.get(url)
users = response.json()

print("=== All Users ===")
for user in users[:5]:  # 只显示前 5 个
    print(f"{user['id']}. {user['name']} ({user['email']})")

# 获取单个用户
print("\n=== Single User ===")
user_url = f"{url}/1"
response = requests.get(user_url)
user = response.json()
print(f"Name: {user['name']}")
print(f"Company: {user['company']['name']}")
print(f"Website: {user['website']}")
```

### 任务 2.2：搜索功能

创建 `search_posts.py`：

```python
import requests

# 获取帖子
url = "https://jsonplaceholder.typicode.com/posts"
params = {
    "_limit": 5  # 限制返回数量
}

response = requests.get(url, params=params)
posts = response.json()

print("=== Recent Posts ===")
for post in posts:
    print(f"\nID: {post['id']}")
    print(f"Title: {post['title'][:50]}...")
    print(f"User ID: {post['userId']}")

# 按用户过滤
print("\n=== Posts by User 1 ===")
user1_posts = [p for p in posts if p["userId"] == 1]
print(f"User 1 has {len(user1_posts)} posts")
```

---

## 第三部分：POST 请求 (25 分钟)

### 任务 3.1：创建资源

创建 `create_post.py`：

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"

# 新帖子数据
new_post = {
    "title": "My First Post",
    "body": "This is the content of my post.",
    "userId": 1
}

# 发送 POST 请求
response = requests.post(url, json=new_post)

print(f"Status Code: {response.status_code}")

if response.status_code == 201:
    created = response.json()
    print(f"\nCreated Post:")
    print(f"ID: {created['id']}")
    print(f"Title: {created['title']}")
else:
    print(f"Error: {response.text}")
```

**注意**：JSONPlaceholder 是模拟 API，不会真正保存数据，但会返回成功的响应。

### 任务 3.2：更新资源

创建 `update_post.py`：

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

# 更新的数据
updated = {
    "title": "Updated Title",
    "body": "This is the updated content."
}

# PUT 请求（完整更新）
response = requests.put(url, json=updated)
print("=== PUT Response ===")
print(f"Status: {response.status_code}")
print(f"Response: {response.json()}")
```

---

## 第四部分：错误处理 (30 分钟)

### 任务 4.1：处理错误响应

创建 `error_handling.py`：

```python
import requests

def safe_request(url):
    """安全地发送请求"""
    try:
        response = requests.get(url, timeout=5)

        if response.status_code == 200:
            return {"success": True, "data": response.json()}
        elif response.status_code == 404:
            return {"success": False, "error": "Resource not found"}
        elif response.status_code == 500:
            return {"success": False, "error": "Server error"}
        else:
            return {"success": False, "error": f"HTTP {response.status_code}"}

    except requests.exceptions.Timeout:
        return {"success": False, "error": "Request timed out"}
    except requests.exceptions.ConnectionError:
        return {"success": False, "error": "Connection failed"}
    except Exception as e:
        return {"success": False, "error": str(e)}

# 测试各种情况
urls = [
    "https://jsonplaceholder.typicode.com/users/1",  # 成功
    "https://jsonplaceholder.typicode.com/invalid",   # 404
    "https://invalid-domain-xyz.com/api",             # 连接失败
]

for url in urls:
    print(f"\nRequesting: {url}")
    result = safe_request(url)
    if result["success"]:
        print(f"✓ Success")
    else:
        print(f"✗ Error: {result['error']}")
```

### 任务 4.2：重试机制

创建 `retry_request.py`：

```python
import requests
import time

def request_with_retry(url, max_retries=3):
    """失败时重试"""
    for attempt in range(max_retries):
        try:
            response = requests.get(url, timeout=5)
            if response.status_code == 200:
                return response.json()
        except requests.exceptions.Timeout:
            print(f"Attempt {attempt + 1} timed out, retrying...")
            time.sleep(1)
        except Exception as e:
            print(f"Attempt {attempt + 1} failed: {e}")
            time.sleep(1)

    print("Max retries reached")
    return None

# 测试
data = request_with_retry("https://jsonplaceholder.typicode.com/users/1")
if data:
    print(f"Got data: {data['name']}")
```

---

## 第五部分：综合项目 (40 分钟)

### 任务：天气查询器

创建 `weather_app.py`：

```python
"""
简单天气查询器
使用 Open-Meteo API（免费，无需认证）
"""

import requests

# 城市坐标
CITIES = {
    "1": {"name": "Beijing", "lat": 39.9042, "lon": 116.4074},
    "2": {"name": "Shanghai", "lat": 31.2304, "lon": 121.4737},
    "3": {"name": "Guangzhou", "lat": 23.1291, "lon": 113.2644},
    "4": {"name": "Shenzhen", "lat": 22.5431, "lon": 114.0579},
}

def get_weather(city_key):
    """获取天气数据"""
    city = CITIES[city_key]

    url = "https://api.open-meteo.com/v1/forecast"
    params = {
        "latitude": city["lat"],
        "longitude": city["lon"],
        "current_weather": True
    }

    try:
        response = requests.get(url, params=params, timeout=10)
        response.raise_for_status()

        data = response.json()
        weather = data["current_weather"]

        print(f"\n🌤️  {city['name']} Weather")
        print(f"Temperature: {weather['temperature']}°C")
        print(f"Wind Speed: {weather['windspeed']} km/h")
        print(f"Wind Direction: {weather['winddirection']}°")

    except requests.exceptions.RequestException as e:
        print(f"Error getting weather: {e}")

# 主程序
print("=== Weather Query ===")
print("Select a city:")
for key, city in CITIES.items():
    print(f"  {key}. {city['name']}")

choice = input("\nEnter choice (1-4): ")

if choice in CITIES:
    get_weather(choice)
else:
    print("Invalid choice")
```

**运行**：
```bash
python3 weather_app.py
```

---

## 📝 实验报告

```markdown
# LAB-08 实验报告

姓名：__________  日期：__________

## 任务完成情况

### 第一部分：GET 请求
- [ ] 测试连接成功
- [ ] 获取猫咪事实

### 第二部分：带参数请求
- [ ] 获取用户列表
- [ ] 搜索帖子

### 第三部分：POST 请求
- [ ] 创建资源
- [ ] 更新资源

### 第四部分：错误处理
- [ ] 处理错误响应
- [ ] 实现重试机制

### 第五部分：综合项目
- [ ] 完成天气查询器
- [ ] 能正确显示天气

## 遇到的问题

## 最大的收获

## 还想探索的内容
```

---

## 🔗 相关资源

- [4.4 调用 API 获取数据](./04-calling-apis.md)
- [resources/common-errors.md](../resources/common-errors.md)

---

**完成 LAB-08 后**，你已经完成了 module-04！🎉

下一步：[模块 5：系统与 AI 准备](../module-05-systems-ai-prep/README.md)
