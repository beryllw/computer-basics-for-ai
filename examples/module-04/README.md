# Module 04 Examples

> 模块 4 的示例代码：数据格式和 API 调用

---

## 示例 1：JSON 处理

```python
# json_demo.py
# JSON 数据处理演示

import json

# Python 对象
person = {
    "name": "Alice",
    "age": 25,
    "city": "Beijing",
    "skills": ["Python", "JavaScript", "SQL"],
    "active": True
}

# 转为 JSON 字符串
json_str = json.dumps(person, indent=2, ensure_ascii=False)
print("=== Python 转 JSON ===")
print(json_str)

# JSON 字符串转 Python
parsed = json.loads(json_str)
print(f"\n姓名：{parsed['name']}")
print(f"技能：{parsed['skills']}")

# 读写 JSON 文件
with open("person.json", "w") as f:
    json.dump(person, f, indent=2, ensure_ascii=False)

with open("person.json") as f:
    data = json.load(f)
    print(f"\n从文件读取：{data['name']}")

# 清理
import os
os.remove("person.json")
```

---

## 示例 2：CSV 处理

```python
# csv_demo.py
# CSV 数据处理演示

import csv

# 写入 CSV
data = [
    ["name", "age", "city"],
    ["Alice", 25, "Beijing"],
    ["Bob", 30, "Shanghai"],
    ["Charlie", 28, "Guangzhou"]
]

with open("people.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerows(data)

# 读取 CSV
print("=== 读取 CSV ===")
with open("people.csv") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)

# 使用 DictReader
print("\n=== DictReader ===")
with open("people.csv") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(f"{row['name']} - {row['age']}岁 - {row['city']}")

# 清理
import os
os.remove("people.csv")
```

---

## 示例 3：API 调用基础

```python
# api_basics.py
# API 调用基础演示

import requests

def test_api():
    """测试 API 调用"""

    # 简单的 GET 请求
    url = "https://httpbin.org/get"
    response = requests.get(url)

    print("=== API 响应 ===")
    print(f"状态码：{response.status_code}")
    print(f"内容类型：{response.headers.get('Content-Type')}")

    # 解析 JSON
    data = response.json()
    print(f"\nOrigin: {data['origin']}")

# 运行测试
if __name__ == "__main__":
    test_api()
```

---

## 示例 4：获取公开 API 数据

```python
# fetch_public_api.py
# 获取公开 API 数据

import requests

def get_cat_fact():
    """获取猫咪事实"""
    url = "https://catfact.ninja/fact"
    response = requests.get(url)

    if response.status_code == 200:
        data = response.json()
        print(f"🐱 猫咪事实：{data['fact']}")
    else:
        print(f"错误：{response.status_code}")

def get_users():
    """获取用户列表"""
    url = "https://jsonplaceholder.typicode.com/users"
    response = requests.get(url)

    if response.status_code == 200:
        users = response.json()
        print("\n=== 用户列表 ===")
        for user in users[:5]:
            print(f"- {user['name']} ({user['email']})")
    else:
        print(f"错误：{response.status_code}")

def get_posts():
    """获取帖子"""
    url = "https://jsonplaceholder.typicode.com/posts"
    params = {"_limit": 5}
    response = requests.get(url, params=params)

    if response.status_code == 200:
        posts = response.json()
        print("\n=== 最新帖子 ===")
        for post in posts:
            title = post["title"][:40]
            print(f"- {title}...")
    else:
        print(f"错误：{response.status_code}")

if __name__ == "__main__":
    get_cat_fact()
    get_users()
    get_posts()
```

---

## 示例 5：带错误处理的 API 调用

```python
# api_with_error_handling.py
# 带错误处理的 API 调用

import requests

def safe_api_call(url, timeout=10):
    """安全的 API 调用"""
    try:
        response = requests.get(url, timeout=timeout)

        if response.status_code == 200:
            return {"success": True, "data": response.json()}
        elif response.status_code == 404:
            return {"success": False, "error": "资源未找到 (404)"}
        elif response.status_code == 401:
            return {"success": False, "error": "未授权 (401)"}
        elif response.status_code >= 500:
            return {"success": False, "error": f"服务器错误 ({response.status_code})"}
        else:
            return {"success": False, "error": f"HTTP 错误 ({response.status_code})"}

    except requests.exceptions.Timeout:
        return {"success": False, "error": "请求超时"}
    except requests.exceptions.ConnectionError:
        return {"success": False, "error": "连接失败"}
    except Exception as e:
        return {"success": False, "error": str(e)}

# 测试
if __name__ == "__main__":
    urls = [
        "https://jsonplaceholder.typicode.com/users/1",  # 成功
        "https://jsonplaceholder.typicode.com/invalid",   # 404
        "https://invalid-domain.xyz/api",                 # 连接失败
    ]

    for url in urls:
        print(f"\n请求：{url}")
        result = safe_api_call(url)
        if result["success"]:
            print(f"✓ 成功")
        else:
            print(f"✗ 错误：{result['error']}")
```

---

## 示例 6：天气查询器

```python
# weather_app.py
# 简单天气查询器

import requests

CITIES = {
    "beijing": {"lat": 39.9042, "lon": 116.4074},
    "shanghai": {"lat": 31.2304, "lon": 121.4737},
    "guangzhou": {"lat": 23.1291, "lon": 113.2644},
    "shenzhen": {"lat": 22.5431, "lon": 114.0579},
}

def get_weather(city_name):
    """获取天气数据"""
    city = CITIES.get(city_name.lower())

    if not city:
        print(f"未知城市：{city_name}")
        return

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

        print(f"\n🌤️  {city_name.capitalize()} 天气")
        print(f"温度：{weather['temperature']}°C")
        print(f"风速：{weather['windspeed']} km/h")
        print(f"风向：{weather['winddirection']}°")

    except requests.exceptions.RequestException as e:
        print(f"获取天气失败：{e}")

if __name__ == "__main__":
    import sys

    if len(sys.argv) > 1:
        city = sys.argv[1]
    else:
        city = "beijing"

    get_weather(city)
```

---

## 示例 7：数据收集和报告

```python
# data_collection.py
# 数据收集和报告生成

import requests
import json
from datetime import datetime

def collect_user_data():
    """收集用户数据并生成报告"""

    url = "https://jsonplaceholder.typicode.com/users"

    try:
        response = requests.get(url, timeout=10)
        response.raise_for_status()
        users = response.json()

        # 生成统计
        cities = {}
        for user in users:
            city = user["address"]["city"]
            cities[city] = cities.get(city, 0) + 1

        # 生成报告
        report = {
            "timestamp": datetime.now().isoformat(),
            "total_users": len(users),
            "cities": cities,
            "users": users
        }

        # 保存报告
        with open("user_report.json", "w") as f:
            json.dump(report, f, indent=2)

        # 打印摘要
        print("=== 数据收集报告 ===")
        print(f"时间：{report['timestamp']}")
        print(f"用户总数：{report['total_users']}")
        print(f"\n城市分布:")
        for city, count in cities.items():
            print(f"  {city}: {count}人")

        print("\n报告已保存到 user_report.json")

    except requests.exceptions.RequestException as e:
        print(f"错误：{e}")

if __name__ == "__main__":
    collect_user_data()
```

---

## 运行示例

```bash
# 进入示例目录
cd examples/module-04

# 运行各个示例
python3 json_demo.py
python3 csv_demo.py
python3 api_basics.py
python3 fetch_public_api.py
python3 api_with_error_handling.py
python3 weather_app.py beijing
python3 data_collection.py
```

---

## 扩展练习

1. 修改天气查询器，支持更多城市
2. 添加数据缓存功能
3. 尝试调用其他公开 API（如 GitHub API）
4. 将结果导出为 CSV 格式
