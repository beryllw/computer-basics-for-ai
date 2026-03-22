# Linux 命令速查表 (Command Cheatsheet)

> 20+ 个核心命令，掌握 Linux 命令行基础

---

## 📖 如何使用本速查表

- **初学者**: 按顺序学习，每个命令都动手试试
- **复习**: 用目录快速查找需要的命令
- **进阶**: 查看每个命令的"进阶用法"部分

---

## 🔰 基础命令

### 文件和目录操作

#### `pwd` - 显示当前目录
```bash
pwd
# 输出示例：/home/username
```
**作用**: 显示你当前在文件系统的哪个位置

---

#### `ls` - 列出目录内容
```bash
ls               # 列出当前目录文件
ls -l            # 详细列表（权限、大小、时间）
ls -a            # 显示隐藏文件（以 . 开头）
ls -la           # 组合选项：详细 + 隐藏文件
ls /path         # 列出指定目录
ls -lh           # 人类可读的文件大小（K, M, G）
```
**常用选项**:
| 选项 | 作用 |
|------|------|
| `-l` | 详细列表 |
| `-a` | 显示隐藏文件 |
| `-h` | 人类可读大小 |
| `-t` | 按时间排序 |
| `-r` | 反向排序 |

---

#### `cd` - 切换目录
```bash
cd /path/to/dir      # 切换到指定目录
cd ..                # 返回上一级
cd ~                 # 回到家目录
cd -                 # 返回上一个目录
cd                   # 等同于 cd ~
```
**路径说明**:
- `.` 当前目录
- `..` 上级目录
- `~` 家目录
- `/` 根目录

---

#### `mkdir` - 创建目录
```bash
mkdir newdir                  # 创建单个目录
mkdir dir1 dir2 dir3          # 创建多个目录
mkdir -p parent/child/grand   # 递归创建目录（包括不存在的父目录）
```

---

#### `cp` - 复制文件或目录
```bash
cp file.txt backup.txt           # 复制文件
cp file.txt /path/to/dest        # 复制到指定目录
cp -r dir1/ dir2/                # 递归复制目录
cp *.txt backup/                 # 复制所有 .txt 文件
```
**常用选项**:
| 选项 | 作用 |
|------|------|
| `-r` | 递归复制（用于目录） |
| `-i` | 覆盖前询问 |
| `-v` | 显示复制过程 |

---

#### `mv` - 移动或重命名文件
```bash
mv old.txt new.txt              # 重命名文件
mv file.txt /path/to/dir/       # 移动文件
mv dir1/ dir2/                  # 移动目录
```
**注意**: `mv` 既可以移动也可以重命名，本质是改变文件路径

---

#### `rm` - 删除文件
```bash
rm file.txt                # 删除文件
rm -r directory/           # 递归删除目录
rm -rf directory/          # 强制删除（不询问）⚠️ 危险！
rm -i file.txt             # 删除前询问
```
**⚠️ 警告**:
- `rm -rf` 非常危险，删除后无法恢复
- 使用前务必确认路径正确

---

#### `touch` - 创建空文件或更新时间
```bash
touch newfile.txt          # 创建空文件
touch file1 file2 file3    # 创建多个文件
touch existing.txt         # 更新现有文件的时间戳
```

---

### 查看文件内容

#### `cat` - 显示文件内容
```bash
cat file.txt               # 显示整个文件
cat file1 file2            # 合并显示多个文件
cat > newfile.txt          # 创建文件并输入内容（Ctrl+D 结束）
```

---

#### `less` - 分页查看文件
```bash
less largefile.txt         # 分页查看大文件
```
**交互命令**:
- `Space` - 下一页
- `b` - 上一页
- `q` - 退出
- `/pattern` - 搜索
- `n` - 下一个匹配
- `g` - 跳到开头
- `G` - 跳到结尾

---

#### `head` - 显示文件开头
```bash
head file.txt              # 显示前 10 行
head -n 20 file.txt        # 显示前 20 行
```

---

#### `tail` - 显示文件结尾
```bash
tail file.txt              # 显示最后 10 行
tail -n 20 file.txt        # 显示最后 20 行
tail -f logfile.log        # 实时跟踪文件更新（看日志神器）
```

---

### 文本处理

#### `grep` - 搜索文本
```bash
grep "pattern" file.txt           # 在文件中搜索
grep -r "pattern" dir/            # 递归搜索目录下所有文件
grep -i "pattern" file.txt        # 忽略大小写
grep -n "pattern" file.txt        # 显示行号
grep -v "pattern" file.txt        # 显示不匹配的行
grep -c "pattern" file.txt        # 统计匹配行数
ps aux | grep python              # 查找 Python 进程
```
**常用选项**:
| 选项 | 作用 |
|------|------|
| `-i` | 忽略大小写 |
| `-r` | 递归搜索 |
| `-n` | 显示行号 |
| `-v` | 反向匹配 |
| `-c` | 计数 |

---

#### `wc` - 统计行数、字数
```bash
wc file.txt                # 行数、词数、字节数
wc -l file.txt             # 只统计行数
wc -w file.txt             # 只统计词数
wc -c file.txt             # 只统计字节数
```

---

### 权限和所有权

#### `chmod` - 修改文件权限
```bash
chmod +x script.sh         # 添加执行权限
chmod -x script.sh         # 移除执行权限
chmod 755 file.txt         # 设置权限为 rwxr-xr-x
chmod 644 file.txt         # 设置权限为 rw-r--r--
chmod -R 755 dir/          # 递归修改目录权限
```
**权限说明**:
| 数字 | 权限 | 含义 |
|------|------|------|
| 7 | rwx | 读 + 写 + 执行 |
| 6 | rw- | 读 + 写 |
| 5 | r-x | 读 + 执行 |
| 4 | r-- | 只读 |
| 0 | --- | 无权限 |

**权限位**: `chmod XYZ file`
- X = 所有者权限
- Y = 组权限
- Z = 其他人权限

---

#### `chown` - 修改文件所有者
```bash
chown user file.txt        # 修改所有者
chown user:group file.txt  # 修改所有者和组
chown -R user dir/         # 递归修改
```

---

### 压缩和解压

#### `tar` - 打包和解包
```bash
tar -cvf archive.tar file1 file2        # 创建 tar 包
tar -xvf archive.tar                    # 解压 tar 包
tar -czvf archive.tar.gz dir/           # 创建 gzip 压缩
tar -xzvf archive.tar.gz                # 解压 gzip 压缩
tar -tjf archive.tar.bz2                # 查看 bz2 压缩内容
```
**常用选项**:
| 选项 | 作用 |
|------|------|
| `-c` | 创建 |
| `-x` | 解压 |
| `-v` | 显示过程 |
| `-f` | 指定文件名 |
| `-z` | gzip 压缩 |
| `-j` | bzip2 压缩 |
| `-t` | 查看内容 |

---

#### `zip` / `unzip` - ZIP 压缩
```bash
zip archive.zip file1 file2      # 创建 ZIP
zip -r archive.zip dir/          # 压缩目录
unzip archive.zip                # 解压 ZIP
```

---

### 网络相关

#### `curl` - 发送 HTTP 请求
```bash
curl https://example.com              # 获取网页
curl -O https://example.com/file.zip  # 下载文件（保留原名）
curl -o newfile.zip URL               # 下载文件（重命名）
curl -X POST https://api.example.com  # POST 请求
curl -H "Authorization: Bearer XXX"   # 添加请求头
```

---

#### `ssh` - 远程登录
```bash
ssh user@hostname          # 登录远程服务器
ssh -p 2222 user@host      # 指定端口
ssh -i key.pem user@host   # 使用密钥登录
```

---

#### `scp` - 安全复制
```bash
scp file.txt user@host:/path/       # 上传文件
scp user@host:/path/file.txt ./     # 下载文件
scp -r dir/ user@host:/path/        # 复制目录
```

---

### 进程管理

#### `ps` - 显示进程状态
```bash
ps                     # 显示当前终端的进程
ps aux                 # 显示所有进程（详细）
ps aux | grep python   # 查找 Python 进程
```

---

#### `top` / `htop` - 实时进程监控
```bash
top                    # 实时显示进程（内置）
htop                   # 更友好的界面（需安装）
```
**top 交互命令**:
- `q` - 退出
- `k` - 杀死进程
- `M` - 按内存排序
- `P` - 按 CPU 排序

---

#### `kill` - 终止进程
```bash
kill PID               # 发送终止信号
kill -9 PID            # 强制终止
killall process_name   # 按名称终止
```

---

#### `bg` / `fg` - 后台/前台任务
```bash
Ctrl+Z                 # 暂停当前任务
bg                     # 将暂停的任务放到后台
fg                     # 将后台任务拉到前台
jobs                   # 列出后台任务
```

---

### 管道和重定向

#### 管道 `|`
```bash
ls -la | grep ".txt"           # ls 输出作为 grep 输入
cat file.txt | head -n 10      # 显示前 10 行
ps aux | grep python | wc -l   # 统计 Python 进程数
```

#### 重定向
```bash
command > file.txt             # 覆盖输出到文件
command >> file.txt            # 追加输出到文件
command < file.txt             # 从文件读取输入
2> error.log                   # 重定向错误输出
&> all.log                     # 重定向所有输出
```

---

### 其他实用命令

#### `echo` - 输出文本
```bash
echo "Hello"                   # 输出文本
echo $HOME                     # 输出环境变量
echo "text" > file.txt         # 写入文件
```

#### `which` - 查找命令位置
```bash
which python                   # 查找 python 命令路径
which ls
```

#### `man` - 查看帮助文档
```bash
man ls                         # 查看 ls 的手册
man grep                       # 查看 grep 的手册
```
**man 页面导航**:
- `Space` - 下一页
- `b` - 上一页
- `q` - 退出
- `/pattern` - 搜索

#### `history` - 查看命令历史
```bash
history                        # 查看所有历史命令
history | grep git             # 搜索 git 相关命令
!!                             # 执行上一条命令
!123                           # 执行第 123 条历史命令
Ctrl+R                         # 搜索历史命令（交互）
```

#### `find` - 查找文件
```bash
find . -name "*.txt"           # 查找当前目录的 txt 文件
find /home -name "*.log"       # 在/home 下查找 log 文件
find . -type d -name "test"    # 查找目录
find . -mtime -7               # 查找 7 天内修改的文件
```

#### `du` - 查看磁盘使用
```bash
du -sh directory/              # 查看目录总大小
du -h --max-depth=1            # 查看一级子目录大小
```

#### `df` - 查看磁盘空间
```bash
df -h                          # 以人类可读格式显示磁盘空间
df -i                          # 显示 inode 使用情况
```

---

## 🔗 组合使用示例

```bash
# 1. 查找并统计日志中的错误
grep "ERROR" app.log | wc -l

# 2. 找出最大的 10 个文件
find . -type f -exec du -h {} + | sort -rh | head -n 10

# 3. 批量重命名（所有 jpg 改名为 jpeg）
for f in *.jpg; do mv "$f" "${f%.jpg}.jpeg"; done

# 4. 监控日志文件并过滤特定内容
tail -f app.log | grep --line-buffered "WARNING"

# 5. 下载并解压
curl -O https://example.com/file.tar.gz && tar -xzf file.tar.gz

# 6. 查看系统信息
uname -a && cat /etc/os-release && df -h

# 7. 查找并删除所有临时文件
find . -name "*.tmp" -type f -delete

# 8. 统计代码行数
find . -name "*.py" -exec cat {} \; | wc -l
```

---

## 📝 命令分类速查

| 类别 | 命令 |
|------|------|
| **导航** | `pwd`, `cd`, `ls` |
| **文件操作** | `mkdir`, `cp`, `mv`, `rm`, `touch` |
| **查看内容** | `cat`, `less`, `head`, `tail` |
| **文本处理** | `grep`, `wc` |
| **权限** | `chmod`, `chown` |
| **压缩** | `tar`, `zip`, `unzip` |
| **网络** | `curl`, `ssh`, `scp` |
| **进程** | `ps`, `top`, `kill`, `bg`, `fg` |
| **管道/重定向** | `|`, `>`, `>>`, `<` |
| **帮助** | `man`, `history`, `which` |
| **查找** | `find`, `du`, `df` |

---

## 🎯 学习建议

1. **每天学习 3-5 个命令**，动手实践
2. **用 `man` 命令**查看每个命令的完整文档
3. **组合使用**命令提高效率
4. **记住常用选项**，不需要记住所有参数
5. **善用 Tab 补全**和命令历史（上下箭头、Ctrl+R）

---

## 🆘 遇到问题？

- 命令不熟悉 → `man <command>` 或 `<command> --help`
- 权限不够 → 检查是否需要 `sudo`（谨慎使用）
- 路径找不到 → 用 `pwd` 确认当前位置，用 `ls` 查看文件

---

**提示**: 将此速查表保存为书签，随时查阅！
