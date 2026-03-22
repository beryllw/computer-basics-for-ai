# 实验 LAB-10：构建简单工作流

> 综合运用所学构建自动化工作流

---

## 🎯 实验目标

- [ ] 能够设计简单的工作流
- [ ] 能够组合多个工具
- [ ] 能够用脚本自动化任务
- [ ] 能够验证工作流正确性

---

## 📋 准备工作

```bash
# 创建实验目录
mkdir -p ~/computer-basics/module-05/lab10
cd ~/computer-basics/module-05/lab10
```

---

## 第一部分：日志分析工作流 (30 分钟)

### 任务 1.1：创建示例日志

创建 `app.log`：

```
2026-03-22 10:15:23 INFO Application started
2026-03-22 10:15:24 INFO Connecting to database
2026-03-22 10:15:25 ERROR Database connection failed
2026-03-22 10:15:26 INFO Retrying database connection
2026-03-22 10:15:27 INFO Database connected
2026-03-22 10:15:28 INFO Loading configuration
2026-03-22 10:15:29 WARNING Config file not found, using defaults
2026-03-22 10:15:30 INFO Server starting on port 8080
2026-03-22 10:15:31 INFO Server ready
2026-03-22 10:20:45 ERROR Request timeout for /api/users
2026-03-22 10:21:00 INFO Request completed
2026-03-22 10:25:33 ERROR Invalid input received
```

### 任务 1.2：命令行分析

```bash
# 统计错误数量
grep "ERROR" app.log | wc -l

# 统计警告数量
grep "WARNING" app.log | wc -l

# 提取所有错误消息
grep "ERROR" app.log

# 按时间排序的错误
grep "ERROR\|WARNING" app.log
```

### 任务 1.3：Python 分析脚本

创建 `analyze_log.py`：

```python
"""日志分析脚本"""

from collections import Counter

def analyze_log(filename):
    """分析日志文件"""
    errors = []
    warnings = []
    info_count = 0

    with open(filename) as f:
        for line in f:
            if "ERROR" in line:
                errors.append(line.strip())
            elif "WARNING" in line:
                warnings.append(line.strip())
            elif "INFO" in line:
                info_count += 1

    print(f"=== Log Analysis Report ===\n")
    print(f"Total INFO messages: {info_count}")
    print(f"Total WARNING messages: {len(warnings)}")
    print(f"Total ERROR messages: {len(errors)}\n")

    if errors:
        print("=== Errors ===")
        for error in errors:
            print(f"  {error}")

    if warnings:
        print("\n=== Warnings ===")
        for warning in warnings:
            print(f"  {warning}")

    return {
        "errors": len(errors),
        "warnings": len(warnings),
        "info": info_count
    }

if __name__ == "__main__":
    analyze_log("app.log")
```

**运行**：
```bash
python3 analyze_log.py
```

---

## 第二部分：数据备份工作流 (30 分钟)

### 任务 2.1：创建备份脚本

创建 `backup.sh`：

```bash
#!/bin/bash

# 简单备份脚本

# 设置变量
SOURCE_DIR="."
BACKUP_DIR="./backups"
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_NAME="backup_${DATE}.tar.gz"

# 创建备份目录
mkdir -p "$BACKUP_DIR"

# 创建备份
echo "Creating backup: $BACKUP_NAME"
tar -czf "$BACKUP_DIR/$BACKUP_NAME" \
    --exclude="backups" \
    --exclude="*.log" \
    "$SOURCE_DIR"

# 验证备份
if [ -f "$BACKUP_DIR/$BACKUP_NAME" ]; then
    SIZE=$(du -h "$BACKUP_DIR/$BACKUP_NAME" | cut -f1)
    echo "✓ Backup created successfully: $BACKUP_NAME ($SIZE)"
else
    echo "✗ Backup failed!"
    exit 1
fi

# 列出备份
echo ""
echo "=== Existing Backups ==="
ls -lh "$BACKUP_DIR"
```

**运行**：
```bash
chmod +x backup.sh
./backup.sh
```

### 任务 2.2：Python 版本

创建 `backup.py`：

```python
"""Python 备份脚本"""

import os
import tarfile
from datetime import datetime

def create_backup(source_dir=".", backup_dir="./backups"):
    """创建备份"""
    # 创建备份目录
    os.makedirs(backup_dir, exist_ok=True)

    # 生成备份文件名
    date_str = datetime.now().strftime("%Y%m%d_%H%M%S")
    backup_name = f"backup_{date_str}.tar.gz"
    backup_path = os.path.join(backup_dir, backup_name)

    # 创建 tar.gz 备份
    print(f"Creating backup: {backup_name}")

    with tarfile.open(backup_path, "w:gz") as tar:
        for item in os.listdir(source_dir):
            # 排除备份目录和日志文件
            if item == "backups" or item.endswith(".log"):
                continue
            tar.add(item)

    # 验证
    if os.path.exists(backup_path):
        size = os.path.getsize(backup_path)
        size_kb = size / 1024
        print(f"✓ Backup created: {backup_name} ({size_kb:.1f} KB)")
        return True
    else:
        print("✗ Backup failed!")
        return False

if __name__ == "__main__":
    create_backup()
```

---

## 第三部分：API 数据收集工作流 (40 分钟)

### 任务：收集并保存 API 数据

创建 `collect_data.py`：

```python
"""
数据收集工作流
1. 从 API 获取数据
2. 保存到 JSON 文件
3. 生成简单报告
"""

import requests
import json
from datetime import datetime

def fetch_users():
    """从 API 获取用户数据"""
    url = "https://jsonplaceholder.typicode.com/users"

    try:
        response = requests.get(url, timeout=10)
        response.raise_for_status()
        return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Error fetching data: {e}")
        return None

def save_to_file(data, filename):
    """保存到 JSON 文件"""
    with open(filename, "w") as f:
        json.dump(data, f, indent=2)
    print(f"✓ Data saved to {filename}")

def generate_report(data):
    """生成简单报告"""
    print("\n=== Data Collection Report ===")
    print(f"Timestamp: {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}")
    print(f"Total records: {len(data)}")

    # 统计
    cities = Counter(user["address"]["city"] for user in data)
    print(f"\nCities: {dict(cities)}")

    # 公司信息
    companies = set(user["company"]["name"] for user in data)
    print(f"Unique companies: {len(companies)}")

from collections import Counter

if __name__ == "__main__":
    # 步骤 1：获取数据
    print("Fetching data from API...")
    users = fetch_users()

    if users:
        # 步骤 2：保存数据
        save_to_file(users, "users_data.json")

        # 步骤 3：生成报告
        generate_report(users)
    else:
        print("Failed to fetch data")
```

**运行**：
```bash
python3 collect_data.py
```

**验证输出**：
```bash
cat users_data.json | head -30
```

---

## 第四部分：综合项目 (40 分钟)

### 任务：完整的日志分析系统

创建 `log_system.py`：

```python
"""
完整日志分析系统
1. 读取日志文件
2. 分析并统计
3. 生成 JSON 报告
4. 输出人类可读报告
"""

import json
from datetime import datetime
from collections import Counter

def parse_log_line(line):
    """解析单行日志"""
    parts = line.strip().split(" ", 3)
    if len(parts) >= 4:
        return {
            "date": parts[0],
            "time": parts[1],
            "level": parts[2],
            "message": parts[3]
        }
    return None

def analyze_log(filename):
    """分析日志文件"""
    logs = {
        "INFO": [],
        "WARNING": [],
        "ERROR": []
    }

    with open(filename) as f:
        for line in f:
            parsed = parse_log_line(line)
            if parsed:
                level = parsed["level"]
                if level in logs:
                    logs[level].append(parsed)

    return logs

def generate_json_report(logs, output_file):
    """生成 JSON 报告"""
    report = {
        "timestamp": datetime.now().isoformat(),
        "summary": {
            "info_count": len(logs["INFO"]),
            "warning_count": len(logs["WARNING"]),
            "error_count": len(logs["ERROR"])
        },
        "errors": logs["ERROR"],
        "warnings": logs["WARNING"]
    }

    with open(output_file, "w") as f:
        json.dump(report, f, indent=2)

    return report

def print_report(report):
    """打印人类可读报告"""
    print("\n" + "=" * 50)
    print("       LOG ANALYSIS REPORT")
    print("=" * 50)
    print(f"Generated: {report['timestamp']}")
    print()
    print("Summary:")
    summary = report["summary"]
    print(f"  INFO messages:  {summary['info_count']}")
    print(f"  WARNING messages: {summary['warning_count']}")
    print(f"  ERROR messages:   {summary['error_count']}")

    if report["errors"]:
        print("\nErrors:")
        for error in report["errors"]:
            print(f"  [{error['time']}] {error['message']}")

    if report["warnings"]:
        print("\nWarnings:")
        for warning in report["warnings"]:
            print(f"  [{warning['time']}] {warning['message']}")

    print("\n" + "=" * 50)

if __name__ == "__main__":
    # 分析日志
    logs = analyze_log("app.log")

    # 生成 JSON 报告
    report = generate_json_report(logs, "log_report.json")

    # 打印报告
    print_report(report)
```

**运行**：
```bash
python3 log_system.py
```

---

## 📝 实验报告

```markdown
# LAB-10 实验报告

姓名：__________  日期：__________

## 第一部分：日志分析
- [ ] 创建了日志文件
- [ ] 用命令行分析
- [ ] 用 Python 分析

## 第二部分：备份工作流
- [ ] 创建了 Shell 备份脚本
- [ ] 创建了 Python 备份脚本
- [ ] 验证了备份文件

## 第三部分：数据收集
- [ ] 从 API 获取了数据
- [ ] 保存到了 JSON 文件
- [ ] 生成了报告

## 第四部分：综合项目
- [ ] 完成了日志分析系统
- [ ] 生成了 JSON 报告
- [ ] 输出了人类可读报告

## 遇到的挑战

## 最大的收获

## 想进一步探索的方向
```

---

## 🔗 相关资源

- [module-02: Linux 工具](../module-02-linux-tools/README.md)
- [module-03: 编程概念](../module-03-programming-concepts/README.md)
- [module-04: 数据与网络](../module-04-data-network/README.md)

---

**完成 LAB-10 后**，你已经完成了整个课程的所有实验！🎉

继续到 [assessments/](../assessments/) 完成课程评估测试
