# 常见错误与解决方案 (Common Errors)

> 遇到问题不要慌，这里整理了学习者常犯的错误和解决方法

---

## 📖 如何使用本文档

1. **先看错误信息** - 复制你看到的错误信息
2. **用 Ctrl+F 搜索** - 查找错误关键词
3. **按类别浏览** - 根据你遇到的问题类型查找
4. **理解原因** - 不只是复制解决方案，理解为什么出错

---

## 🔰 命令行错误

### 1. `command not found` / 命令未找到

```bash
$ pyhton --version
bash: pyhton: command not found
```

**原因**:
- 命令拼写错误（如上面 `pyhton` 应为 `python`）
- 命令未安装
- 命令不在 PATH 中

**解决方法**:
```bash
# 1. 检查拼写
python --version  # 正确的拼写

# 2. 检查是否安装
which python      # 查看命令路径

# 3. 尝试安装（如果需要）
sudo apt install python3
```

---

### 2. `Permission denied` / 权限拒绝

```bash
$ ./script.sh
bash: ./script.sh: Permission denied
```

**原因**: 文件没有执行权限

**解决方法**:
```bash
# 添加执行权限
chmod +x script.sh
./script.sh

# 或者用解释器运行
python script.sh
bash script.sh
```

---

### 3. `No such file or directory`

```bash
$ cd /home/user/projec
bash: cd: /home/user/projec: No such file or directory
```

**原因**:
- 路径拼写错误
- 目录不存在
- 大小写错误（Linux 区分大小写）

**解决方法**:
```bash
# 1. 检查当前目录内容
ls

# 2. 使用 Tab 补全避免拼写错误
cd /home/user/proj<TAB>

# 3. 确认路径存在
ls -la /home/user/
```

---

### 4. `rm: cannot remove` / 无法删除

```bash
$ rm /root/file.txt
rm: cannot remove '/root/file.txt': Permission denied
```

**原因**:
- 没有文件所有权
- 目录权限不足
- 文件被占用

**解决方法**:
```bash
# 1. 检查文件权限
ls -la /root/file.txt

# 2. 如果是你的文件但权限不对
chmod u+w file.txt

# 3. 谨慎使用 sudo（确保你知道在做什么）
sudo rm file.txt

# 4. 如果是目录，需要递归删除
rm -r directory/
```

---

### 5. `sudo: command not found`

```bash
$ sudo apt update
sudo: command not found
```

**原因**: 系统没有安装 sudo（某些最小化安装）

**解决方法**:
```bash
# 切换到 root 用户
su -

# 然后安装 sudo
apt update && apt install sudo

# 或者直接用 root 执行
apt update
```

---

### 6. 管道和重定向错误

```bash
# 错误：覆盖了重要文件
cat important.txt > important.txt

# 错误：管道方向错了
grep "pattern" < file.txt  # 应该是 grep "pattern" file.txt
```

**原因**: 混淆了 `>` 和 `<` 的用法

**解决方法**:
```bash
# 正确的重定向
cat file.txt > output.txt     # 输出到文件
command < input.txt           # 从文件读取
command >> log.txt            # 追加到文件

# 重要：不要用输出重定向到同一个文件！
# 错误：cat file.txt > file.txt
# 正确：cat file.txt > newfile.txt
```

---

## 🐍 Python 错误

### 1. `SyntaxError: invalid syntax`

```python
>>> if x > 5
  File "<stdin>", line 1
    if x > 5
            ^
SyntaxError: invalid syntax
```

**原因**: 缺少冒号、括号不匹配等语法错误

**解决方法**:
```python
# 正确写法
if x > 5:
    print("x is greater than 5")

# 检查：
# - if/for/while/def/class 后面都要有冒号
# - 括号要成对出现
```

---

### 2. `IndentationError`

```python
>>> def hello():
... print("Hello")
  File "<stdin>", line 2
    print("Hello")
    ^
IndentationError: expected an indented block
```

**原因**: Python 用缩进表示代码块，缺少或混用缩进

**解决方法**:
```python
# 正确写法
def hello():
    print("Hello")  # 4 个空格或 1 个 Tab

# 重要规则：
# - 同一个代码块缩进必须一致
# - 不要混用 Tab 和空格
# - 推荐使用 4 个空格
```

---

### 3. `NameError: name 'xxx' is not defined`

```python
>>> print(message)
NameError: name 'message' is not defined
```

**原因**:
- 变量未定义就使用
- 变量名拼写错误
- 变量作用域问题

**解决方法**:
```python
# 先定义再使用
message = "Hello"
print(message)

# 检查拼写
# 检查变量是否在当前作用域可用
```

---

### 4. `TypeError`

```python
>>> "Age: " + 25
TypeError: can only concatenate str (not "int") to str

>>> len(123)
TypeError: object of type 'int' has no len()
```

**原因**: 对错误的数据类型执行操作

**解决方法**:
```python
# 类型转换
"Age: " + str(25)  # "Age: 25"

# 检查类型
type(123)  # <class 'int'>
type("123")  # <class 'str'>

# 使用正确的操作
len("123")  # 3
```

---

### 5. `IndexError: list index out of range`

```python
>>> my_list = [1, 2, 3]
>>> my_list[5]
IndexError: list index out of range
```

**原因**: 访问了不存在的索引

**解决方法**:
```python
# 检查列表长度
len(my_list)  # 3

# 有效索引：0 到 len(list)-1
my_list[0]  # 1
my_list[2]  # 3
my_list[-1] # 3 (最后一个元素)

# 安全访问
if len(my_list) > 5:
    print(my_list[5])
```

---

### 6. `KeyError: 'xxx'`

```python
>>> data = {"name": "Alice"}
>>> data["age"]
KeyError: 'age'
```

**原因**: 访问字典中不存在的键

**解决方法**:
```python
# 方法 1：先检查
if "age" in data:
    print(data["age"])

# 方法 2：使用 get（推荐）
data.get("age")  # 返回 None
data.get("age", 0)  # 返回默认值 0

# 方法 3：使用 try-except
try:
    print(data["age"])
except KeyError:
    print("Key not found")
```

---

### 7. `FileNotFoundError`

```python
>>> open("nonexistent.txt")
FileNotFoundError: [Errno 2] No such file or directory: 'nonexistent.txt'
```

**原因**: 文件路径不存在

**解决方法**:
```python
# 检查文件是否存在
import os
os.path.exists("file.txt")

# 使用绝对路径
with open("/full/path/to/file.txt") as f:
    content = f.read()

# 先创建文件
with open("file.txt", "w") as f:
    f.write("content")
```

---

### 8. `ModuleNotFoundError`

```python
>>> import requests
ModuleNotFoundError: No module named 'requests'
```

**原因**: 模块未安装

**解决方法**:
```bash
# 安装模块
pip install requests

# 或者用 pip3
pip3 install requests

# 检查已安装的包
pip list
```

---

## 🔗 网络和 API 错误

### 1. `Connection refused`

```bash
$ curl http://localhost:8080
curl: (7) Failed to connect to localhost port 8080: Connection refused
```

**原因**:
- 服务没有运行
- 端口错误
- 防火墙阻止

**解决方法**:
```bash
# 1. 检查服务是否运行
ps aux | grep <service_name>

# 2. 检查端口是否监听
netstat -tlnp | grep 8080
# 或
lsof -i :8080

# 3. 检查防火墙
sudo ufw status
```

---

### 2. `SSL certificate problem`

```bash
$ curl https://example.com
curl: (60) SSL certificate problem: unable to get local issuer certificate
```

**原因**: SSL 证书验证失败

**解决方法**:
```bash
# 开发环境（不推荐生产环境）
curl -k https://example.com

# 或者更新证书
sudo apt install ca-certificates

# 或者指定证书
curl --cacert /path/to/cert.pem https://example.com
```

---

### 3. `404 Not Found`

```bash
$ curl https://api.example.com/invalid-endpoint
{"error": "404 Not Found"}
```

**原因**: 请求的资源不存在

**解决方法**:
```bash
# 1. 检查 URL 拼写
# 2. 查看 API 文档确认端点
# 3. 检查 API 版本
curl https://api.example.com/v1/endpoint
```

---

### 4. `401 Unauthorized` / `403 Forbidden`

```bash
$ curl https://api.example.com/protected
{"error": "401 Unauthorized"}
```

**原因**: 认证失败或权限不足

**解决方法**:
```bash
# 添加认证头
curl -H "Authorization: Bearer YOUR_TOKEN" \
     https://api.example.com/protected

# 或者用 API key
curl -H "X-API-Key: YOUR_KEY" \
     https://api.example.com/endpoint
```

---

### 5. `Timeout` / 请求超时

```bash
$ curl https://slow-server.com
curl: (28) Operation timed out after 30000 milliseconds
```

**原因**:
- 服务器响应慢
- 网络问题
- 服务器过载

**解决方法**:
```bash
# 增加超时时间
curl --connect-timeout 60 --max-time 300 \
     https://slow-server.com

# 检查网络
ping slow-server.com

# 重试请求
```

---

## 📁 文件系统错误

### 1. `No space left on device`

```bash
$ echo "test" > file.txt
bash: file.txt: write error: No space left on device
```

**原因**: 磁盘已满

**解决方法**:
```bash
# 检查磁盘空间
df -h

# 查找大文件
du -ah | sort -rh | head -n 10

# 清理空间
rm -rf /path/to/large/file
# 或清理缓存
sudo apt clean
```

---

### 2. `Too many open files`

```bash
$ python script.py
OSError: [Errno 24] Too many open files
```

**原因**: 打开的文件句柄超过系统限制

**解决方法**:
```python
# 确保关闭文件
with open("file.txt") as f:
    content = f.read()
# 自动关闭

# 检查限制
ulimit -n

# 提高限制（临时）
ulimit -n 4096
```

---

## 🧩 Git 错误（如果使用）

### 1. `fatal: not a git repository`

```bash
$ git status
fatal: not a git repository (or any of the parent directories): .git
```

**原因**: 不在 Git 仓库目录中

**解决方法**:
```bash
# 初始化新仓库
git init

# 或克隆现有仓库
git clone <url>

# 或切换到正确的目录
cd /path/to/repo
```

---

### 2. `fatal: remote origin already exists`

```bash
$ git remote add origin <url>
fatal: remote origin already exists.
```

**原因**: 远程仓库已配置

**解决方法**:
```bash
# 查看现有远程
git remote -v

# 更新远程 URL
git remote set-url origin <new_url>

# 或删除后重新添加
git remote remove origin
git remote add origin <url>
```

---

### 3. `error: failed to push`

```bash
$ git push
error: failed to push some refs to '...'
hint: Updates were rejected because the remote contains work that you do
```

**原因**: 远程仓库有本地没有的提交

**解决方法**:
```bash
# 安全的方法：先拉取再推送
git pull --rebase
git push

# 或者查看差异
git log HEAD..origin/main

# 强制推送（危险！仅在你知道后果时使用）
git push -f
```

---

## 🆘 调试技巧

### 通用调试步骤

1. **仔细阅读错误信息**
   - 错误类型是什么？
   - 哪个文件、哪一行？
   - 具体的错误描述？

2. **复现问题**
   - 每次只改变一个变量
   - 最小化复现步骤

3. **搜索错误信息**
   - 用 Google/AI 搜索完整错误
   - 加上你的编程语言和版本

4. **打印调试**
   ```python
   print(f"DEBUG: x = {x}")
   print(f"DEBUG: type = {type(x)}")
   ```

5. **问 AI 时的最佳实践**
   ```
   - 提供完整的错误信息
   - 说明你做了什么
   - 说明期望的结果
   - 提供相关代码片段
   ```

---

## 📞 何时寻求帮助

当遇到以下情况时，应该寻求 AI 或他人的帮助：

- ✅ 已经尝试了上述方法但问题依旧
- ✅ 错误信息看不懂
- ✅ 不确定解决方案是否安全
- ✅ 问题影响了其他功能

**提问模板**:
```
1. 我想做什么：...
2. 我做了什么：...
3. 期望结果：...
4. 实际结果（错误信息）：...
5. 我已经尝试的方法：...
```

---

## 🔗 相关资源

- [glossary.md](./glossary.md) - 术语表
- [command-cheatsheet.md](./command-cheatsheet.md) - 命令速查
- [ai-collab-tips.md](./ai-collab-tips.md) - AI 协作技巧

---

**记住**: 遇到错误是正常的，每个错误都是学习的机会！🎯
