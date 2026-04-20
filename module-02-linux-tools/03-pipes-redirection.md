# 2.3 管道和重定向

> 学会组合命令，像搭积木一样构建强大功能

---

## 🎯 学习目标

学完本课后，你将能够：

- [ ] 理解管道的概念和用法
- [ ] 使用重定向保存命令输出
- [ ] 组合多个命令完成复杂任务
- [ ] 理解标准输入、输出、错误

---

## 💡 核心概念

### 什么是管道（Pipe）？

> **管道 = 把一个命令的输出作为另一个命令的输入**

符号：`|`

```
命令 1  |  命令 2  |  命令 3
  ↓         ↓         ↓
输出 →   输入 →   输入 → 最终输出
```

### 类比：工厂流水线

```
原材料 → 加工站 1 → 加工站 2 → 加工站 3 → 成品

每个命令是一个"加工站"
管道是"传送带"
```

---

## 🔧 管道用法

### 基础示例

```bash
# 列出文件，然后分页查看
ls -la | less

# 列出所有 Python 文件，然后计数
ls *.py | wc -l

# 查看日志，搜索错误，显示行号
cat app.log | grep -n "ERROR"

# 查看进程，搜索 python
ps aux | grep python
```

### 实用组合

```bash
# 查找出现最多的命令历史
cat ~/.bash_history | cut -d ' ' -f 1 | sort | uniq -c | sort -rn | head -10

# 统计代码行数
find . -name "*.py" | xargs cat | wc -l

# 查找大文件
find . -type f -size +100M | xargs ls -lh | sort -k5 -h

# 查看系统资源占用
ps aux | sort -k3 -rn | head -10  # CPU 占用前 10
ps aux | sort -k4 -rn | head -10  # 内存占用前 10
```

### 管道技巧

```bash
# tee：同时输出到屏幕和文件
ls -la | tee file_list.txt

# 查看处理进度
cat largefile.txt | grep "pattern" | tee matches.txt | wc -l

# 多条管道调试：在中间插入 tee 查看
command1 | tee /dev/stderr | command2
```

---

## 📤 重定向

### 输出重定向

| 符号 | 作用 | 例子 |
|------|------|------|
| `>` | 覆盖输出到文件 | `echo "hi" > file.txt` |
| `>>` | 追加输出到文件 | `echo "hi" >> file.txt` |
| `2>` | 重定向错误输出 | `cmd 2> error.log` |
| `&>` | 重定向所有输出 | `cmd &> all.log` |

### 示例

```bash
# 覆盖写入
echo "Hello" > greeting.txt
cat greeting.txt  # 输出：Hello

# 追加写入
echo "World" >> greeting.txt
cat greeting.txt  # 输出：Hello\nWorld

# 保存命令输出
ls -la > file_list.txt

# 保存错误（正确输出到屏幕）
invalid_command 2> error.log

# 保存所有输出
cmd &> output.log

# 丢弃输出（发送到黑洞）
cmd > /dev/null 2>&1
```

### 输入重定向

```bash
# 从文件读取输入
sort < unsorted.txt

# 等价于
cat unsorted.txt | sort

# 多个输入
cat < file1.txt < file2.txt
```

---

## 🎯 标准流

### 三个标准流

| 流 | 文件描述符 | 默认目标 |
|----|-----------|----------|
| **stdin** | 0 | 键盘输入 |
| **stdout** | 1 | 屏幕输出 |
| **stderr** | 2 | 屏幕输出（错误） |

### 重定向示例

```bash
# 只保存正确输出
cmd > output.txt

# 只保存错误
cmd 2> error.txt

# 保存所有输出
cmd > all.txt 2>&1
# 或简写（bash 4+）
cmd &> all.txt

# 丢弃所有输出
cmd > /dev/null 2>&1

# 错误合并到正确输出
cmd 2>&1 | grep "pattern"
```

### /dev/null 是什么？

```
/dev/null = "黑洞"，写入的内容会被丢弃

用途：
- 丢弃不需要的输出
- 测试程序
- 静音运行

例子：
cmd > /dev/null 2>&1  # 完全静音
```

---

## 🧪 实战练习

### 练习 1：日志分析

```bash
# 1. 创建测试日志
cat > app.log << 'EOF'
2024-01-01 10:00:00 INFO Starting application
2024-01-01 10:01:00 DEBUG Loading configuration
2024-01-01 10:02:00 INFO Connected to database
2024-01-01 10:03:00 ERROR Failed to load module
2024-01-01 10:04:00 WARN Retry attempt 1
2024-01-01 10:05:00 ERROR Connection timeout
2024-01-01 10:06:00 INFO Retry successful
2024-01-01 10:07:00 DEBUG Processing request
2024-01-01 10:08:00 ERROR Invalid input
2024-01-01 10:09:00 INFO Request completed
EOF

# 2. 统计各级别日志数量
grep -oE "(INFO|DEBUG|ERROR|WARN)" app.log | sort | uniq -c

# 3. 提取所有错误到单独文件
grep "ERROR" app.log > errors.log
cat errors.log

# 4. 查看错误数量
wc -l errors.log

# 5. 创建摘要报告
{
    echo "=== 日志分析报告 ==="
    echo "生成时间：$(date)"
    echo ""
    echo "总行数：$(wc -l < app.log)"
    echo "错误数：$(grep -c ERROR app.log)"
    echo "警告数：$(grep -c WARN app.log)"
    echo ""
    echo "错误详情："
    grep ERROR app.log
} > report.txt

cat report.txt
```

### 练习 2：文件处理流水线

```bash
# 1. 创建测试数据
cat > users.txt << 'EOF'
alice,25,alice@example.com,Beijing
bob,30,bob@example.com,Shanghai
charlie,28,charlie@example.com,Guangzhou
david,35,david@example.com,Shenzhen
eve,22,eve@example.com,Beijing
EOF

# 2. 按年龄排序
sort -t',' -k2 -n users.txt

# 3. 提取邮箱
cut -d',' -f3 users.txt

# 4. 找出北京的用户
grep "Beijing" users.txt

# 5. 创建格式化输出
cat users.txt | while IFS=',' read name age email city; do
    echo "$name ($age) from $city - $email"
done

# 6. 保存处理结果
cat users.txt | \
    sort -t',' -k2 -n | \
    cut -d',' -f1,3 | \
    tr ',' '\t' > processed_users.txt

cat processed_users.txt
```

### 练习 3：系统信息收集

```bash
# 创建系统信息报告
{
    echo "=== 系统信息报告 ==="
    echo "生成时间：$(date)"
    echo ""
    
    echo "=== 主机信息 ==="
    hostname
    echo ""
    
    echo "=== 磁盘使用 ==="
    df -h | head -5
    echo ""
    
    echo "=== 内存使用 ==="
    free -h
    echo ""
    
    echo "=== 当前用户 ==="
    whoami
    echo ""
    
    echo "=== 登录用户 ==="
    who
    echo ""
    
    echo "=== 前 5 个 CPU 占用进程 ==="
    ps aux | sort -k3 -rn | head -5
    
} > system_report.txt

cat system_report.txt
```

---

## 📊 常用管道组合

### 文本处理

```bash
# 词频统计
cat file.txt | tr ' ' '\n' | sort | uniq -c | sort -rn | head -20

# 提取特定列
cat data.csv | cut -d',' -f2,4

# 去重
cat list.txt | sort | uniq

# 合并文件
cat file1.txt file2.txt | sort | uniq > merged.txt
```

### 文件查找

```bash
# 查找并处理
find . -name "*.log" | xargs grep "ERROR"

# 查找大文件并排序
find . -type f -size +10M | xargs ls -lh | sort -k5 -h

# 查找并删除
find . -name "*.tmp" | xargs rm
```

### 系统监控

```bash
# 实时日志
tail -f app.log | grep --line-buffered "ERROR"

# 监控进程
ps aux | grep python | grep -v grep

# 网络监控
netstat -tuln | sort -k4 -t':'
```

---

## ⚠️ 注意事项

### 常见错误

```bash
# ❌ 错误：覆盖了自己要读取的文件
cat file.txt | grep "pattern" > file.txt

# ✅ 正确：先保存到临时文件
cat file.txt | grep "pattern" > temp.txt && mv temp.txt file.txt

# ❌ 错误：管道中命令失败不会停止
command1 | command2 | command3

# ✅ 更好：设置错误处理
set -o pipefail
command1 | command2 | command3
```

### 性能考虑

```bash
# 对于大文件，避免不必要的 cat
cat largefile.txt | grep "pattern"  # 多一个进程

grep "pattern" largefile.txt  # 更直接
```

---

## ✅ 本课小结

```
核心要点：

1. 管道 | 把前一个命令的输出作为后一个命令的输入

2. 重定向 > 和 >> 用于保存输出到文件

3. 2> 重定向错误输出，&> 重定向所有输出

4. /dev/null 是"黑洞"，用于丢弃输出

5. 命令组合可以完成复杂任务

6. 管道是 Unix 哲学的核心体现：小工具，大组合
```

---

## 📚 延伸阅读

- 文件操作 → 01-file-system-ops.md
- 文本处理 → 02-text-processing.md
- Shell 脚本入门 → 05-shell-scripting-intro.md

---

## 🤔 思考题

1. `>` 和 `>>` 有什么区别？什么情况下会误用？
2. 如何同时看到命令输出并保存到文件？
3. 为什么 `cat file | grep pattern` 不如 `grep pattern file` 好？

> 💡 可以把你的思考告诉 AI，让它帮你深化理解

---

**下一步**: [2.4 进程管理](./04-process-management.md)
