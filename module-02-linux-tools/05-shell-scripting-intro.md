# 2.5 Shell 脚本入门

> 把命令组合成自动化脚本

---

## 🎯 学习目标

学完本课后，你将能够：

- [ ] 理解 Shell 脚本的基本结构
- [ ] 编写简单的自动化脚本
- [ ] 使用变量和条件判断
- [ ] 运行和调试脚本

---

## 💡 什么是 Shell 脚本？

> **Shell 脚本 = 一系列命令的集合，保存为文件，可重复执行**

```
手动执行：
$ cd /var/log
$ grep "ERROR" app.log > errors.log
$ wc -l errors.log
$ echo "Done!"

写成脚本 (backup.sh)：
#!/bin/bash
cd /var/log
grep "ERROR" app.log > errors.log
wc -l errors.log
echo "Done!"

执行：
$ ./backup.sh
```

---

## 📝 脚本基础

### 第一个脚本

```bash
#!/bin/bash
# 这是我的第一个脚本

echo "Hello, World!"
echo "今天是：$(date)"
echo "当前用户：$(whoami)"
```

**运行脚本：**

```bash
# 1. 保存为 hello.sh

# 2. 添加执行权限
chmod +x hello.sh

# 3. 运行
./hello.sh

# 输出：
# Hello, World!
# 今天是：Tue Mar 17 10:30:00 CST 2024
# 当前用户：admin
```

### Shebang (`#!`)

```bash
#!/bin/bash    # 使用 bash
#!/bin/sh      # 使用 sh
#!/usr/bin/env python3  # 使用 Python3

# 作用：告诉系统用什么解释器执行脚本
# 必须放在第一行
```

---

## 🔧 变量

### 定义和使用

```bash
#!/bin/bash

# 定义变量（不要有空格）
name="Alice"
age=25
greeting="Hello, $name!"

# 使用变量
echo $name           # 输出：Alice
echo $greeting       # 输出：Hello, Alice!
echo "I am $age years old"

# 读取用户输入
echo "What's your name?"
read user_name
echo "Hello, $user_name!"

# 命令行参数
echo "脚本名：$0"
echo "第一个参数：$1"
echo "第二个参数：$2"
echo "所有参数：$@"
echo "参数个数：$#"
```

**运行带参数的脚本：**

```bash
./script.sh Alice 25

# 输出：
# 脚本名：./script.sh
# 第一个参数：Alice
# 第二个参数：25
```

### 特殊变量

| 变量 | 含义 |
|------|------|
| `$0` | 脚本名 |
| `$1`, `$2`... | 第 1、2 个参数 |
| `$#` | 参数个数 |
| `$@` | 所有参数 |
| `$?` | 上一个命令的退出状态（0=成功） |
| `$$` | 当前进程 ID |

---

## 🔀 条件判断

### if 语句

```bash
#!/bin/bash

age=18

if [ $age -ge 18 ]; then
    echo "你已成年"
else
    echo "你未成年"
fi
```

### 比较运算符

```bash
# 数字比较
-eq    # 等于 (equal)
-ne    # 不等于 (not equal)
-gt    # 大于 (greater than)
-ge    # 大于等于
-lt    # 小于 (less than)
-le    # 小于等于

# 字符串比较
=      # 等于
!=     # 不等于
-z     # 空字符串
-n     # 非空

# 文件测试
-e     # 文件存在
-f     # 是普通文件
-d     # 是目录
-r     # 可读
-w     # 可写
-x     # 可执行
```

### 示例

```bash
#!/bin/bash

# 检查文件是否存在
if [ -f "config.txt" ]; then
    echo "配置文件存在"
else
    echo "配置文件不存在"
fi

# 多条件判断
score=85

if [ $score -ge 90 ]; then
    echo "优秀"
elif [ $score -ge 80 ]; then
    echo "良好"
elif [ $score -ge 60 ]; then
    echo "及格"
else
    echo "不及格"
fi

# 逻辑运算符
if [ -f "file.txt" ] && [ -r "file.txt" ]; then
    echo "文件存在且可读"
fi

if [ ! -f "file.txt" ]; then
    echo "文件不存在"
fi
```

---

## 🔁 循环

### for 循环

```bash
#!/bin/bash

# 遍历列表
for fruit in apple banana orange; do
    echo "I like $fruit"
done

# 遍历数字
for i in 1 2 3 4 5; do
    echo "Number: $i"
done

# 范围
for i in {1..5}; do
    echo "Number: $i"
done

# 遍历文件
for file in *.txt; do
    echo "Processing: $file"
done
```

### while 循环

```bash
#!/bin/bash

# 基础 while
count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    count=$((count + 1))
done

# 读取文件
while read line; do
    echo "Line: $line"
done < file.txt

# 无限循环（需要 break）
while true; do
    echo "按 Ctrl+C 停止"
    sleep 1
done
```

### break 和 continue

```bash
#!/bin/bash

# break - 跳出循环
for i in {1..10}; do
    if [ $i -eq 5 ]; then
        break
    fi
    echo $i  # 只输出 1-4
done

# continue - 跳过本次
for i in {1..10}; do
    if [ $((i % 2)) -eq 0 ]; then
        continue
    fi
    echo $i  # 只输出奇数
done
```

---

## 📦 函数

```bash
#!/bin/bash

# 定义函数
greet() {
    echo "Hello, $1!"
}

# 调用函数
greet "Alice"
greet "Bob"

# 带返回值
add() {
    local sum=$(($1 + $2))
    echo $sum
}

result=$(add 5 3)
echo "5 + 3 = $result"

# 返回状态码
check_file() {
    if [ -f "$1" ]; then
        return 0  # 成功
    else
        return 1  # 失败
    fi
}

if check_file "test.txt"; then
    echo "文件存在"
fi
```

---

## 🧪 实战脚本

### 脚本 1：备份脚本

```bash
#!/bin/bash
# backup.sh - 简单备份脚本

# 配置
SOURCE_DIR="/home/admin/documents"
BACKUP_DIR="/home/admin/backups"
DATE=$(date +%Y%m%d_%H%M%S)

# 创建备份目录
mkdir -p $BACKUP_DIR

# 创建备份
echo "开始备份..."
tar -czf $BACKUP_DIR/backup_$DATE.tar.gz $SOURCE_DIR

# 检查是否成功
if [ $? -eq 0 ]; then
    echo "备份成功：backup_$DATE.tar.gz"
else
    echo "备份失败！"
    exit 1
fi

# 清理 7 天前的备份
find $BACKUP_DIR -name "backup_*.tar.gz" -mtime +7 -delete
echo "清理完成"
```

### 脚本 2：系统监控

```bash
#!/bin/bash
# monitor.sh - 系统监控脚本

echo "=== 系统监控报告 ==="
echo "时间：$(date)"
echo "主机：$(hostname)"
echo ""

# CPU 负载
echo "=== CPU 负载 ==="
uptime
echo ""

# 内存使用
echo "=== 内存使用 ==="
free -h
echo ""

# 磁盘使用
echo "=== 磁盘使用 ==="
df -h
echo ""

# 磁盘使用率警告
usage=$(df / | tail -1 | awk '{print $5}' | sed 's/%//')
if [ $usage -gt 80 ]; then
    echo "⚠️  警告：磁盘使用率超过 80%！"
fi

# 进程数
echo "=== 进程统计 ==="
echo "当前进程数：$(ps aux | wc -l)"
```

### 脚本 3：批量处理

```bash
#!/bin/bash
# batch_rename.sh - 批量重命名文件

# 检查参数
if [ $# -ne 2 ]; then
    echo "用法：$0 <旧前缀> <新前缀>"
    echo "例如：$0 img photo"
    exit 1
fi

old_prefix=$1
new_prefix=$2

# 处理文件
count=0
for file in ${old_prefix}*; do
    if [ -f "$file" ]; then
        new_file="${file/$old_prefix/$new_prefix}"
        mv "$file" "$new_file"
        echo "重命名：$file -> $new_file"
        count=$((count + 1))
    fi
done

echo "完成！共处理 $count 个文件"
```

---

## 🐛 调试技巧

### 调试选项

```bash
# 运行脚本时添加 -x 显示执行的命令
bash -x script.sh

# 或在脚本开头添加
#!/bin/bash -x

# 只检查语法，不执行
bash -n script.sh
```

### 调试技巧

```bash
#!/bin/bash

# 打印变量
echo "DEBUG: value=$value" >&2

# 设置 -e 遇到错误立即退出
set -e

# 设置 -u 使用未定义变量时报错
set -u

# 组合使用
set -eu

# 捕获错误
trap 'echo "错误发生在第 $LINENO 行"' ERR
```

---

## ✅ 本课小结

```
核心要点：

1. Shell 脚本是命令的集合，可自动化重复任务

2. #!/bin/bash 必须放在第一行

3. 变量定义不要有空格：name="value"

4. if/for/while 实现条件判断和循环

5. 函数可以复用代码

6. 用 bash -x 调试脚本
```

---

## 📚 延伸阅读

- 管道和重定向 → 03-pipes-redirection.md
- 命令速查表 → resources/command-cheatsheet.md
- 进阶 Shell 编程 → 网上教程

---

## 🤔 思考题

1. 为什么变量定义时 `name = "value"` 是错误的？
2. `$?` 变量的作用是什么？
3. 如何编写一个安全的脚本（处理错误情况）？

> 💡 可以把你的思考告诉 AI，让它帮你深化理解

---

**下一步**: 完成模块 2 的实验

```bash
cat LAB-03-file-organization.md
cat LAB-04-log-analysis.md
```
