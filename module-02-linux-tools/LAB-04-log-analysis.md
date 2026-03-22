# 实验 04：日志分析

> 使用文本处理工具分析日志文件

---

## 🎯 实验目标

- 使用 grep 搜索日志
- 使用管道组合命令
- 完成实际的日志分析任务
- 生成分析报告

---

## 📋 实验准备

**时间：** 45-60 分钟

**需要：**
- 终端
- 本实验指南

---

## 🔬 实验任务

### 步骤 1：创建测试日志

```bash
# 创建工作目录
mkdir -p ~/log_lab
cd ~/log_lab

# 创建测试日志文件
cat > app.log << 'EOF'
2024-01-15 08:00:00 INFO Application starting...
2024-01-15 08:00:01 DEBUG Loading configuration from config.yaml
2024-01-15 08:00:02 INFO Configuration loaded successfully
2024-01-15 08:00:03 DEBUG Connecting to database
2024-01-15 08:00:04 INFO Database connection established
2024-01-15 08:00:05 DEBUG Starting web server on port 8080
2024-01-15 08:00:06 INFO Web server started
2024-01-15 08:01:00 INFO Received request: GET /api/users
2024-01-15 08:01:01 DEBUG Querying database for users
2024-01-15 08:01:02 INFO Response sent: 200 OK
2024-01-15 08:02:00 INFO Received request: POST /api/login
2024-01-15 08:02:01 DEBUG Validating credentials
2024-01-15 08:02:02 ERROR Invalid credentials for user: admin
2024-01-15 08:02:03 INFO Response sent: 401 Unauthorized
2024-01-15 08:03:00 INFO Received request: GET /api/products
2024-01-15 08:03:01 DEBUG Querying database for products
2024-01-15 08:03:02 WARN Database query slow: 1.5s
2024-01-15 08:03:03 INFO Response sent: 200 OK
2024-01-15 08:04:00 ERROR Database connection lost
2024-01-15 08:04:01 WARN Attempting to reconnect...
2024-01-15 08:04:02 INFO Reconnection successful
2024-01-15 08:05:00 INFO Received request: DELETE /api/users/5
2024-01-15 08:05:01 DEBUG Checking user permissions
2024-01-15 08:05:02 ERROR Permission denied for user: guest
2024-01-15 08:05:03 INFO Response sent: 403 Forbidden
2024-01-15 08:06:00 INFO Received request: GET /api/stats
2024-01-15 08:06:01 DEBUG Calculating statistics
2024-01-15 08:06:02 INFO Response sent: 200 OK
2024-01-15 08:07:00 WARN High memory usage: 85%
2024-01-15 08:07:01 INFO Garbage collection triggered
2024-01-15 08:07:02 DEBUG Memory freed: 500MB
2024-01-15 08:08:00 INFO Received request: PUT /api/users/3
2024-01-15 08:08:01 DEBUG Updating user record
2024-01-15 08:08:02 INFO Response sent: 200 OK
2024-01-15 08:09:00 ERROR Timeout waiting for response from external API
2024-01-15 08:09:01 WARN Retrying request...
2024-01-15 08:09:02 INFO External API response received
2024-01-15 08:10:00 INFO Application shutdown requested
2024-01-15 08:10:01 DEBUG Closing database connections
2024-01-15 08:10:02 INFO Database connections closed
2024-01-15 08:10:03 INFO Application stopped
EOF

# 查看日志
cat app.log
```

### 步骤 2：基础分析

```bash
# 1. 统计总行数
echo "=== 日志总数 ==="
wc -l app.log

# 2. 统计各级别日志数量
echo ""
echo "=== 日志级别统计 ==="
grep -oE "(INFO|DEBUG|ERROR|WARN)" app.log | sort | uniq -c | sort -rn

# 3. 查看所有错误
echo ""
echo "=== 错误列表 ==="
grep "ERROR" app.log

# 4. 查看错误数量
echo ""
echo "=== 错误数量 ==="
grep -c "ERROR" app.log

# 5. 查看警告
echo ""
echo "=== 警告列表 ==="
grep "WARN" app.log
```

### 步骤 3：深入分析

```bash
# 1. 查看错误前后上下文（各 2 行）
echo "=== 错误上下文 ==="
grep -C 2 "ERROR" app.log

# 2. 查看特定时间的日志
echo ""
echo "=== 08:02 的日志 ==="
grep "08:02" app.log

# 3. 查看第一个和最后一个日志
echo ""
echo "=== 第一个日志 ==="
head -n 1 app.log

echo ""
echo "=== 最后一个日志 ==="
tail -n 1 app.log

# 4. 统计请求类型
echo ""
echo "=== 请求类型统计 ==="
grep "Received request" app.log | \
    grep -oE "(GET|POST|PUT|DELETE)" | \
    sort | uniq -c
```

### 步骤 4：生成报告

```bash
# 创建分析报告
cat > report.txt << 'HEADER'
====================================
       日志分析报告
====================================

HEADER

echo "生成时间：$(date)" >> report.txt
echo "日志文件：app.log" >> report.txt
echo "" >> report.txt

echo "=== 基本信息 ===" >> report.txt
echo "总行数：$(wc -l < app.log)" >> report.txt
echo "文件大小：$(ls -lh app.log | awk '{print $5}')" >> report.txt
echo "" >> report.txt

echo "=== 日志级别统计 ===" >> report.txt
grep -oE "(INFO|DEBUG|ERROR|WARN)" app.log | \
    sort | uniq -c | sort -rn >> report.txt
echo "" >> report.txt

echo "=== 错误详情 ===" >> report.txt
grep "ERROR" app.log >> report.txt
echo "" >> report.txt

echo "=== 警告详情 ===" >> report.txt
grep "WARN" app.log >> report.txt
echo "" >> report.txt

echo "=== 请求统计 ===" >> report.txt
echo "GET:  $(grep -c 'GET' app.log)" >> report.txt
echo "POST: $(grep -c 'POST' app.log)" >> report.txt
echo "PUT:  $(grep -c 'PUT' app.log)" >> report.txt
echo "DELETE: $(grep -c 'DELETE' app.log)" >> report.txt

# 查看报告
cat report.txt
```

### 步骤 5：创建监控脚本

```bash
# 创建一个可复用的日志分析脚本
cat > analyze_log.sh << 'EOF'
#!/bin/bash
# 日志分析脚本

if [ $# -eq 0 ]; then
    echo "用法：$0 <日志文件>"
    exit 1
fi

LOG_FILE=$1

echo "===================================="
echo "       日志分析报告"
echo "===================================="
echo ""
echo "日志文件：$LOG_FILE"
echo "分析时间：$(date)"
echo ""

echo "=== 基本信息 ==="
echo "总行数：$(wc -l < $LOG_FILE)"
echo ""

echo "=== 日志级别统计 ==="
grep -oE "(INFO|DEBUG|ERROR|WARN)" $LOG_FILE | \
    sort | uniq -c | sort -rn
echo ""

echo "=== 错误详情 ==="
grep "ERROR" $LOG_FILE
echo ""

echo "=== 警告详情 ==="
grep "WARN" $LOG_FILE
EOF

chmod +x analyze_log.sh

# 测试脚本
./analyze_log.sh app.log
```

---

## 🎯 进阶挑战

### 挑战 1：提取错误邮件

```bash
# 假设你要把错误通过邮件发送（模拟）
# 提取错误信息，保存到单独文件
grep "ERROR" app.log > errors_only.log

# 添加邮件头（模拟）
{
    echo "From: monitoring@company.com"
    echo "To: admin@company.com"
    echo "Subject: [ALERT] Error Report"
    echo ""
    echo "以下是今日的错误日志："
    echo ""
    cat errors_only.log
} > error_email.txt

cat error_email.txt
```

### 挑战 2：实时监控脚本

```bash
# 创建一个实时监控错误的脚本
cat > monitor_errors.sh << 'EOF'
#!/bin/bash
# 实时监控日志中的错误

LOG_FILE=${1:-app.log}

echo "开始监控：$LOG_FILE"
echo "按 Ctrl+C 停止"
echo ""

tail -f $LOG_FILE | while read line; do
    if echo "$line" | grep -q "ERROR"; then
        echo "⚠️  [ERROR DETECTED] $(date '+%H:%M:%S')"
        echo "   $line"
    fi
done
EOF

chmod +x monitor_errors.sh

# 测试（新开一个终端）
# ./monitor_errors.sh app.log
```

### 挑战 3：多日志分析

```bash
# 创建额外的日志文件
cat > access.log << 'EOF'
192.168.1.1 - - [15/Jan/2024:08:01:00] "GET /api/users" 200 1234
192.168.1.2 - - [15/Jan/2024:08:02:00] "POST /api/login" 401 89
192.168.1.1 - - [15/Jan/2024:08:03:00] "GET /api/products" 200 5678
192.168.1.3 - - [15/Jan/2024:08:04:00] "DELETE /api/users/5" 403 45
192.168.1.2 - - [15/Jan/2024:08:05:00] "GET /api/stats" 200 890
EOF

# 分析访问日志
echo "=== 访问日志分析 ==="

echo "IP 地址统计："
cut -d' ' -f1 access.log | sort | uniq -c | sort -rn

echo ""
echo "HTTP 状态码统计："
grep -oE '" [0-9]{3} ' access.log | cut -d' ' -f2 | sort | uniq -c | sort -rn

echo ""
echo "请求方法统计："
grep -oE '"(GET|POST|PUT|DELETE)' access.log | cut -d'"' -f2 | sort | uniq -c
```

---

## 📊 实验记录

```
1. 日志总行数：____

2. 各级别日志数量：
   - INFO:  ____
   - DEBUG: ____
   - ERROR: ____
   - WARN:  ____

3. 错误的原因有哪些：
   _________________________________
   _________________________________

4. 我的分析发现：
   _________________________________
   _________________________________
```

---

## ✅ 实验检查清单

完成实验后，确认你能：

- [ ] 使用 grep 搜索特定内容
- [ ] 使用 uniq -c 统计出现次数
- [ ] 使用管道组合多个命令
- [ ] 生成分析报告
- [ ] 创建可复用的分析脚本

---

## 🤔 思考题

1. 如何找出最频繁出现的错误？
2. 如果要分析一周的日志，应该如何修改脚本？
3. 如何区分"新出现的错误"和"重复出现的错误"？

---

## 🧹 清理实验环境

```bash
# 实验完成后清理
cd ~
rm -rf ~/log_lab
```

---

**实验完成！** 🎉

模块 2 完成！准备进入模块 3：编程概念与代码阅读

```bash
cd /home/admin/claw-workspace/computer-basics-for-ai
cat module-03-programming-concepts/01-variables-data.md
```
