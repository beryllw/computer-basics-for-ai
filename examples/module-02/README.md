# Module 02 Examples

> 模块 2 的示例脚本和命令

---

## 示例 1：文件组织脚本

```bash
#!/bin/bash
# organize_files.sh
# 自动整理下载目录的文件

# 创建目标目录
mkdir -p ~/Downloads/Organized/{Documents,Images,Videos,Archives,Others}

# 进入下载目录
cd ~/Downloads

# 移动文件到对应目录
mv *.pdf *.doc *.docx *.txt Documents/ 2>/dev/null
mv *.jpg *.png *.gif *.bmp Images/ 2>/dev/null
mv *.mp4 *.avi *.mkv Videos/ 2>/dev/null
mv *.zip *.tar *.gz *.rar Archives/ 2>/dev/null

# 移动其他文件
mv * Others/ 2>/dev/null

echo "文件整理完成！"
```

---

## 示例 2：日志分析脚本

```bash
#!/bin/bash
# analyze_log.sh
# 分析日志文件并生成报告

LOG_FILE="${1:-app.log}"

if [ ! -f "$LOG_FILE" ]; then
    echo "错误：文件 $LOG_FILE 不存在"
    exit 1
fi

echo "=== 日志分析报告 ==="
echo "文件：$LOG_FILE"
echo "日期：$(date)"
echo ""

# 统计
echo "=== 统计信息 ==="
echo "总行数：$(wc -l < "$LOG_FILE")"
echo "错误数：$(grep -c "ERROR" "$LOG_FILE")"
echo "警告数：$(grep -c "WARNING" "$LOG_FILE")"
echo "信息数：$(grep -c "INFO" "$LOG_FILE")"
echo ""

# 最新错误
echo "=== 最新错误 ==="
grep "ERROR" "$LOG_FILE" | tail -5

echo ""
echo "=== 报告完成 ==="
```

---

## 示例 3：批量重命名脚本

```bash
#!/bin/bash
# batch_rename.sh
# 批量重命名文件

# 检查参数
if [ $# -ne 3 ]; then
    echo "用法：$0 <目录> <原前缀> <新前缀>"
    echo "例如：$0 ./photos IMG Vacation"
    exit 1
fi

DIR=$1
OLD_PREFIX=$2
NEW_PREFIX=$3

# 遍历文件
for file in "$DIR"/${OLD_PREFIX}*; do
    if [ -f "$file" ]; then
        # 获取文件名和扩展名
        filename=$(basename "$file")
        extension="${filename##*.}"
        name="${filename%.*}"

        # 生成新名字
        new_name="${name/$OLD_PREFIX/$NEW_PREFIX}.$extension"

        # 重命名
        mv "$file" "$DIR/$new_name"
        echo "重命名：$filename -> $new_name"
    fi
done

echo "批量重命名完成！"
```

---

## 示例 4：系统信息脚本

```bash
#!/bin/bash
# system_info.sh
# 显示系统信息

echo "========== 系统信息 =========="
echo ""

# 操作系统
echo "=== 操作系统 ==="
uname -a
echo ""

# CPU 信息
echo "=== CPU 信息 ==="
lscpu | grep -E "Model name|CPU\(s\)|Architecture"
echo ""

# 内存信息
echo "=== 内存信息 ==="
free -h
echo ""

# 磁盘信息
echo "=== 磁盘使用 ==="
df -h | grep -E "Filesystem|/dev/sd"
echo ""

# 登录用户
echo "=== 登录用户 ==="
who
echo ""

echo "========== 信息收集完成 =========="
```

---

## 示例 5：文本处理命令组合

```bash
# 文本处理示例命令

# 1. 统计日志中每个错误类型的数量
grep "ERROR" app.log | cut -d':' -f3 | sort | uniq -c | sort -rn

# 2. 提取邮箱地址
grep -oE "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" file.txt

# 3. 找出最大的 10 个文件
find . -type f -exec du -h {} + | sort -rh | head -n 10

# 4. 监控日志中的特定模式
tail -f app.log | grep --line-buffered "ERROR\|WARNING"

# 5. 批量转换文件名（大写转小写）
for f in *.TXT; do mv "$f" "$(echo $f | tr '[:upper:]' '[:lower:]')"; done

# 6. 合并多个 CSV 文件
head -n 1 file1.csv > combined.csv  # 复制标题
for f in *.csv; do tail -n +2 "$f" >> combined.csv; done  # 追加数据
```

---

## Python 示例：日志分析器

```python
#!/usr/bin/env python3
# log_analyzer.py
# Python 版本的日志分析器

import sys
from collections import Counter
from datetime import datetime

def analyze_log(filename):
    """分析日志文件"""
    stats = Counter()
    errors = []

    with open(filename) as f:
        for line in f:
            if "ERROR" in line:
                stats["error"] += 1
                errors.append(line.strip())
            elif "WARNING" in line:
                stats["warning"] += 1
            elif "INFO" in line:
                stats["info"] += 1
            stats["total"] += 1

    # 打印报告
    print(f"=== 日志分析报告 ===")
    print(f"文件：{filename}")
    print(f"时间：{datetime.now().strftime('%Y-%m-%d %H:%M:%S')}")
    print()
    print(f"总行数：{stats['total']}")
    print(f"错误：{stats['error']}")
    print(f"警告：{stats['warning']}")
    print(f"信息：{stats['info']}")

    if errors:
        print("\n=== 错误详情 ===")
        for error in errors[:10]:  # 只显示前 10 个
            print(f"  {error}")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("用法：python3 log_analyzer.py <日志文件>")
        sys.exit(1)

    analyze_log(sys.argv[1])
```

---

## 运行示例

```bash
# 进入示例目录
cd examples/module-02

# 添加执行权限
chmod +x *.sh

# 运行脚本
./system_info.sh
./analyze_log.sh ../app.log

# Python 示例
python3 log_analyzer.py ../app.log
```
