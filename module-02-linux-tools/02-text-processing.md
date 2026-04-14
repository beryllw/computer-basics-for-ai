# 2.2 文本处理

> 学会查看、搜索和处理文本文件

---

## 🎯 学习目标

学完本课后，你将能够：

- [ ] 使用 cat, less, head, tail 查看文件
- [ ] 使用 grep 搜索文本内容
- [ ] 使用 wc 统计文件信息
- [ ] 使用文本编辑器进行基本编辑

---

## 📄 查看文件内容

### cat — 显示整个文件

```bash
# 显示文件内容
cat file.txt

# 显示多个文件
cat file1.txt file2.txt

# 显示行号
cat -n file.txt

# 显示不可见字符（调试用）
cat -A file.txt
```

⚠️ **注意：** `cat` 会一次性输出全部内容，大文件会刷屏。

### less — 分页查看（推荐）

```bash
# 分页查看
less largefile.txt

# 在 less 中的操作：
# 空格/ PgDn    - 向下翻页
# b / PgUp      - 向上翻页
# /关键词        - 搜索
# n             - 下一个匹配
# N             - 上一个匹配
# G             - 跳到最后
# 1G 或 g       - 跳到开头
# q             - 退出
```

### head / tail — 查看头部/尾部

```bash
# 查看前 10 行
head file.txt

# 查看前 20 行
head -n 20 file.txt

# 查看最后 10 行（常用于日志）
tail file.txt

# 查看最后 50 行
tail -n 50 file.txt

# 实时跟踪日志（非常实用！）
tail -f /var/log/syslog
# 按 Ctrl+C 退出
```

**实用场景：**

```bash
# 查看日志最新错误
tail -n 100 error.log | grep ERROR

# 查看 CSV 文件结构（看表头 + 几行数据）
head -n 5 data.csv

# 查看文件开头和结尾
head -n 10 file.txt && echo "..." && tail -n 10 file.txt
```

---

## 🔍 grep — 文本搜索

### 基础用法

```bash
# 搜索包含关键词的行
grep "error" log.txt

# 忽略大小写
grep -i "error" log.txt

# 显示行号
grep -n "error" log.txt

# 显示匹配行前后 3 行
grep -C 3 "error" log.txt

# 只显示匹配的文件名（搜索多个文件）
grep -l "TODO" *.py
```

### 常用选项

| 选项 | 作用 | 例子 |
|------|------|------|
| `-i` | 忽略大小写 | `grep -i "hello"` |
| `-n` | 显示行号 | `grep -n "error"` |
| `-v` | 反向匹配（不包含） | `grep -v "DEBUG"` |
| `-c` | 只计数 | `grep -c "error"` |
| `-r` | 递归搜索目录 | `grep -r "TODO" .` |
| `-l` | 只显示文件名 | `grep -l "TODO" *.py` |

### 正则表达式基础

```bash
# 匹配行首
grep "^Error" log.txt

# 匹配行尾
grep "failed$" log.txt

# 匹配任意字符
grep "f..t" file.txt  # 匹配 fast, feet, foot 等

# 匹配数字
grep "[0-9]" file.txt

# 匹配多个模式
grep -E "error|warning|critical" log.txt

# 匹配精确单词
grep -w "the" file.txt  # 匹配 "the" 但不匹配 "there"
```

### 实用例子

```bash
# 在代码中查找 TODO 注释
grep -rn "TODO" src/

# 查找所有 Python 文件中的 import
grep "^import\|^from" *.py

# 统计错误数量
grep -c "ERROR" log.txt

# 查找包含 email 的行
grep -E "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" file.txt

# 排除注释行
grep -v "^[[:space:]]*#" config.txt
```

---

## 📊 wc — 统计信息

```bash
# 统计行数、词数、字节数
wc file.txt

# 输出示例：
#   100   500  2048 file.txt
#   行数  词数  字节数

# 只统计行数
wc -l file.txt

# 只统计词数
wc -w file.txt

# 只统计字节数
wc -c file.txt

# 统计多个文件
wc -l *.txt

# 统计目录中所有文件的行数
find . -name "*.py" -exec wc -l {} + | tail -1
```

**实用场景：**

```bash
# 统计代码行数
find . -name "*.py" -exec cat {} + | wc -l

# 统计日志中的错误数
grep -c "ERROR" app.log

# 比较文件大小
wc -c *.log | sort -n
```

---

## ✏️ 文本编辑器

### nano — 简单易用（推荐新手）

```bash
# 打开文件
nano file.txt

# 常用快捷键：
# Ctrl+O  - 保存
# Ctrl+X  - 退出
# Ctrl+K  - 剪切行
# Ctrl+U  - 粘贴
# Ctrl+W  - 搜索
# Ctrl+\  - 替换
```

### vim — 功能强大（可选学习）

```bash
# 打开文件
vim file.txt

# 基本模式：
# 正常模式（启动时）- 移动、删除、复制
# 插入模式（按 i）  - 编辑文本
# 命令模式（按 :）  - 保存、退出等

# 常用命令：
# i         - 进入插入模式
# :w        - 保存
# :q        - 退出
# :wq       - 保存并退出
# :q!       - 强制退出不保存
# dd        - 删除当前行
# yy        - 复制当前行
# p         - 粘贴
# /关键词    - 搜索
# :s/old/new/g  - 替换
```

### VS Code（图形界面）

如果偏好图形界面，VS Code 是很好的选择：
- 安装：https://code.visualstudio.com/
- 支持语法高亮、自动补全、Git 集成等

---

## 🧪 实战练习

### 练习 1：日志分析

```bash
# 1. 创建测试日志
cat > test.log << 'EOF'
2024-01-01 10:00:00 INFO Application started
2024-01-01 10:01:00 DEBUG Loading config
2024-01-01 10:02:00 ERROR Database connection failed
2024-01-01 10:03:00 INFO Retrying connection
2024-01-01 10:04:00 ERROR Timeout occurred
2024-01-01 10:05:00 WARN Low memory warning
2024-01-01 10:06:00 INFO Connection established
2024-01-01 10:07:00 ERROR File not found
EOF

# 2. 查看所有错误
grep "ERROR" test.log

# 3. 统计错误数量
grep -c "ERROR" test.log

# 4. 查看错误前后上下文
grep -C 1 "ERROR" test.log

# 5. 只看最后发生的错误
tail -n 20 test.log | grep "ERROR"
```

### 练习 2：代码搜索

```bash
# 在项目目录中

# 1. 查找所有 TODO 注释
grep -rn "TODO" .

# 2. 查找行首的函数定义（顶层函数）
grep -n "^def " *.py

# 3. 统计代码行数
find . -name "*.py" -exec wc -l {} + | tail -1

# 4. 查找包含特定关键词的文件
grep -l "import requests" *.py
```

### 练习 3：配置文件管理

```bash
# 1. 创建配置文件
nano config.txt

# 内容示例：
# Database settings
DB_HOST=localhost
DB_PORT=5432
DB_NAME=myapp

# Application settings
DEBUG=true
LOG_LEVEL=INFO

# 2. 查看配置
cat config.txt

# 3. 搜索特定配置
grep "DB_" config.txt

# 4. 修改配置（用 sed）
sed -i 's/DEBUG=true/DEBUG=false/' config.txt

# 5. 验证修改
grep "DEBUG" config.txt
```

---

## 📝 管道组合示例

```bash
# 查找出现次数最多的命令（分析 bash 历史）
cat ~/.bash_history | cut -d ' ' -f 1 | sort | uniq -c | sort -rn | head -10

# 查找最大的 Python 文件
find . -name "*.py" -exec wc -l {} + | sort -rn | head -10

# 统计日志中各级别的数量
grep -oE "(INFO|DEBUG|ERROR|WARN)" app.log | sort | uniq -c

# 查找包含 email 的行并提取 email
grep -oE "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" file.txt
```

---

## ✅ 本课小结

```
核心要点：

1. 查看文件：小文件用 cat，大文件用 less，看尾部用 tail

2. grep 是强大的搜索工具，配合正则更强大

3. wc 用于统计行数、词数、字节数

4. nano 适合新手，vim 功能更强但需要学习

5. 命令组合（管道）可以完成复杂任务

6. 日志分析是常用场景，tail + grep 是黄金组合
```

---

## 📚 延伸阅读

- 文件操作 → 01-file-system-ops.md
- 管道和重定向 → 03-pipes-redirection.md
- 命令速查表 → resources/command-cheatsheet.md

---

## 🤔 思考题

1. 查看一个 10GB 的日志文件，应该用什么命令？为什么？
2. 如何在多个文件中搜索并只显示包含关键词的文件名？
3. `grep -v` 的作用是什么？有什么实用场景？

> 💡 可以把你的思考告诉 AI，让它帮你深化理解

---

**下一步**: [2.3 管道和重定向](./03-pipes-redirection.md)
