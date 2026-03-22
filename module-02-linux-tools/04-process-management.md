# 2.4 进程管理

> 理解和管理正在运行的程序

---

## 🎯 学习目标

学完本课后，你将能够：

- [ ] 理解什么是进程
- [ ] 使用 ps、top 查看进程
- [ ] 终止失控的进程
- [ ] 理解前台和后台任务

---

## 💡 核心概念

### 什么是进程？

> **进程 = 正在运行的程序实例**

```
程序（静态文件） vs 进程（动态运行）

程序：/usr/bin/python3  ← 文件
进程：python3 script.py ← 正在运行

一个程序可以有多个进程：
python3 app1.py  ← 进程 1
python3 app2.py  ← 进程 2
```

### 进程的状态

| 状态 | 含义 |
|------|------|
| **R (Running)** | 正在运行或可运行 |
| **S (Sleeping)** | 等待某事件（如 I/O） |
| **Z (Zombie)** | 已结束但未被回收 |
| **T (Stopped)** | 被停止 |

---

## 🔍 查看进程

### ps 命令

```bash
# 查看当前用户的进程
ps

# 查看所有进程
ps aux

# 输出列说明：
# USER     PID  %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
# admin   12345  0.5  1.2  12345  6789 pts/0    S+   10:00   0:01 python3 app.py

# PID     - 进程 ID
# %CPU    - CPU 使用率
# %MEM    - 内存使用率
# STAT    - 状态
# COMMAND - 启动命令
```

### 实用 ps 组合

```bash
# 查找特定进程
ps aux | grep python

# 查找并排除 grep 本身
ps aux | grep python | grep -v grep

# 按 CPU 排序
ps aux --sort=-%cpu | head -10

# 按内存排序
ps aux --sort=-%mem | head -10

# 查看特定用户的进程
ps -u admin
```

### top / htop — 实时监控

```bash
# 启动 top
top

# top 中的操作：
# q       - 退出
# P       - 按 CPU 排序
# M       - 按内存排序
# k       - 终止进程
# c       - 显示完整命令

# htop（更友好，需要安装）
htop

# top 输出示例：
# top - 10:30:00 up 1 day,  2:30,  1 user,  load average: 0.50, 0.40, 0.35
# Tasks: 200 total,   1 running, 199 sleeping,   0 stopped,   0 zombie
# %Cpu(s):  5.0 us,  2.0 sy,  0.0 ni, 93.0 id,  0.0 wa,  0.0 hi,  0.0 si
# MiB Mem :   7982.5 total,   2048.0 free,   3000.0 used,   2934.5 buff/cache
```

---

## 🛑 终止进程

### kill 命令

```bash
# 终止进程（发送 SIGTERM）
kill 12345

# 强制终止（发送 SIGKILL）
kill -9 12345

# 按名称终止
pkill python
killall python3

# 先查找再终止
ps aux | grep python
kill <PID>
```

### 信号（Signals）

| 信号 | 编号 | 含义 |
|------|------|------|
| **SIGTERM** | 15 | 请求终止（默认） |
| **SIGKILL** | 9 | 强制终止（无法捕获） |
| **SIGHUP** | 1 | 挂起（常用于重载配置） |
| **SIGINT** | 2 | 中断（Ctrl+C） |
| **SIGSTOP** | 19 | 停止 |
| **SIGCONT** | 18 | 继续 |

### 实用例子

```bash
# 优雅地终止进程
kill 12345

# 如果没反应，强制终止
kill -9 12345

# 重启服务（发送 SIGHUP）
kill -HUP <service_pid>

# 终止所有 chrome 进程
pkill chrome

# 终止超过 1 小时的进程
ps -eo pid,etimes,cmd | awk '$2 > 3600 {print $1}' | xargs kill
```

---

## 🎭 前台和后台

### 任务控制

```bash
# 前台运行（默认）
python3 long_task.py

# 后台运行（加 &）
python3 long_task.py &

# 查看后台任务
jobs

# 输出示例：
# [1]  + running    python3 long_task.py

# 把后台任务带到前台
fg %1

# 把前台任务放到后台（先 Ctrl+Z，然后）
bg

# 终止后台任务
kill %1
```

### nohup — 退出终端后继续运行

```bash
# 问题：退出终端后，运行的程序会被终止

# 解决：使用 nohup
nohup python3 app.py &

# 输出会保存到 nohup.out
cat nohup.out

# 或者重定向输出
nohup python3 app.py > app.log 2>&1 &
```

### screen / tmux — 终端复用器

```bash
# 安装 tmux
sudo apt install tmux

# 创建新会话
tmux new -s mysession

# 在会话中运行命令
python3 long_task.py

# 分离会话（保持运行）
# 按 Ctrl+B，然后按 D

# 查看会话
tmux ls

# 恢复会话
tmux attach -t mysession

# 终止会话
tmux kill-session -t mysession
```

---

## 🧪 实战练习

### 练习 1：进程监控

```bash
# 1. 启动一个后台进程
sleep 1000 &

# 2. 查看进程
ps aux | grep sleep

# 3. 查看后台任务
jobs

# 4. 终止进程
kill %1
# 或
pkill sleep

# 5. 确认已终止
ps aux | grep sleep
```

### 练习 2：资源监控

```bash
# 创建系统监控脚本
cat > monitor.sh << 'EOF'
#!/bin/bash
echo "=== 进程监控 ==="
echo "时间：$(date)"
echo ""

echo "=== CPU 占用前 5 ==="
ps aux --sort=-%cpu | head -6

echo ""
echo "=== 内存占用前 5 ==="
ps aux --sort=-%mem | head -6

echo ""
echo "=== 进程统计 ==="
ps aux | wc -l
echo "个进程"
EOF

chmod +x monitor.sh
./monitor.sh
```

### 练习 3：后台任务管理

```bash
# 1. 启动多个后台任务
sleep 100 &
sleep 200 &
sleep 300 &

# 2. 查看所有后台任务
jobs -l

# 3. 终止特定任务
kill %2

# 4. 确认
jobs -l

# 5. 清理所有
kill %1 %3
```

### 练习 4：查找失控进程

```bash
# 查找 CPU 占用高的进程
ps aux --sort=-%cpu | awk 'NR>1 && NR<6 {print $2, $3, $11}'

# 查找僵尸进程
ps aux | awk '$8 ~ /Z/ {print}'

# 查找运行时间长的进程
ps -eo pid,etime,cmd | sort -k2 -r | head -10
```

---

## 📊 进程树

### 查看进程关系

```bash
# 树形显示进程
pstree

# 显示特定进程的树
pstree -p <PID>

# 包含完整命令
pstree -a
```

### 父子进程

```bash
# 查看进程的父进程
ps -o pid,ppid,cmd -p 12345

# 查找某个进程的所有子进程
pgrep -P <parent_pid>

# 终止进程及其子进程
pkill -P <parent_pid>
```

---

## ⚠️ 注意事项

### 安全终止进程

```bash
# ❌ 危险：不要随意 kill
kill -9 1  # 尝试终止 init 进程，会导致系统崩溃

# ✅ 安全：先确认
ps aux | grep <process>
kill <PID>  # 先尝试 SIGTERM

# 如果必须强制
kill -9 <PID>  # 最后手段
```

### 数据丢失风险

```bash
# 终止数据库、编辑器等进程前，确保数据已保存

# 优雅终止：
kill <PID>      # 给程序清理机会
sleep 5         # 等待
ps -p <PID>     # 检查是否还在

# 如果还在，再强制
kill -9 <PID>
```

---

## ✅ 本课小结

```
核心要点：

1. 进程是正在运行的程序实例

2. ps aux 查看所有进程，top 实时监控

3. kill 终止进程，-9 是强制终止

4. & 后台运行，jobs 查看后台任务

5. nohup 和 tmux 让程序在退出终端后继续运行

6. 终止进程前先确认，避免误杀
```

---

## 📚 延伸阅读

- 管道和重定向 → 03-pipes-redirection.md
- Shell 脚本入门 → 05-shell-scripting-intro.md
- 命令速查表 → resources/command-cheatsheet.md

---

## 🤔 思考题

1. 为什么 `kill -9` 应该是最后手段？
2. 后台运行的程序和前台运行的有什么区别？
3. 如果退出终端后想让程序继续运行，有哪些方法？

> 💡 可以把你的思考告诉 AI，让它帮你深化理解

---

**下一步**: [2.5 Shell 脚本入门](./05-shell-scripting-intro.md)
