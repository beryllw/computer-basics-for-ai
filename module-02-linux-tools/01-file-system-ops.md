# 2.1 文件系统操作

> 熟练掌握文件和目录管理命令

---

## 🎯 学习目标

学完本课后，你将能够：

- [ ] 熟练使用文件操作命令（ls, cd, cp, mv, rm）
- [ ] 理解文件权限概念
- [ ] 使用通配符批量操作文件
- [ ] 高效管理项目文件结构

---

## 📁 核心命令复习

### 你已经学过的命令

| 命令 | 作用 | 常用选项 |
|------|------|----------|
| `ls` | 列出文件 | `-l`, `-a`, `-la`, `-h` |
| `cd` | 切换目录 | `cd ..`, `cd ~`, `cd -` |
| `pwd` | 显示当前路径 | 无 |
| `mkdir` | 创建目录 | `-p` (递归创建) |
| `touch` | 创建/更新时间戳 | 无 |
| `cp` | 复制 | `-r` (递归), `-i` (确认) |
| `mv` | 移动/重命名 | `-i` (确认) |
| `rm` | 删除 | `-r` (递归), `-f` (强制) |

---

## 🔍 深入理解

### ls 命令的高级用法

```bash
# 详细信息（权限、大小、时间）
ls -l

# 输出示例：
# drwxr-xr-x  5 admin admin  4096 Mar 17 10:00 Documents
# -rw-r--r--  1 admin admin   256 Mar 17 09:30 notes.txt

# 人类可读的大小
ls -lh

# 输出示例：
# -rw-r--r--  1 admin admin   1.2K Mar 17 09:30 notes.txt
# -rw-r--r--  1 admin admin   3.4M Mar 17 08:00 video.mp4

# 按时间排序（最新在前）
ls -lt

# 按大小排序（最大在前）
ls -lS

# 按时间排序（最新在前）+ 人类可读大小
ls -lth

# 按大小排序（最大在前）+ 人类可读大小
ls -lhS
```

### 理解文件权限

```bash
# 权限字符串：drwxr-xr-x
# 第 1 位：文件类型（d=目录，-=文件，l=链接）
# 第 2-4 位：所有者权限（rwx）
# 第 5-7 位：组权限（r-x）
# 第 8-10 位：其他人权限（r-x）

权限含义：
r (read)    = 读，数值 4
w (write)   = 写，数值 2
x (execute) = 执行，数值 1

示例：
rwx = 4+2+1 = 7
r-x = 4+0+1 = 5
r-- = 4+0+0 = 4

chmod 755 file  # rwxr-xr-x
chmod 644 file  # rw-r--r--
chmod 600 file  # rw-------
```

---

## 🎯 实用技巧

### 通配符（Glob Patterns）

| 通配符 | 含义 | 例子 |
|--------|------|------|
| `*` | 匹配任意字符 | `*.txt` 匹配所有 txt 文件 |
| `?` | 匹配单个字符 | `file?.txt` 匹配 file1.txt, fileA.txt |
| `[abc]` | 匹配括号内任一字符 | `file[123].txt` |
| `[0-9]` | 匹配范围 | `file[0-9].txt` |
| `!` | 取反 | `*.[!txt]` 匹配非 txt 文件 |

**实用例子：**

```bash
# 列出所有 Python 文件
ls *.py

# 列出所有以 test 开头的文件
ls test*

# 复制常见图片格式到 backup 目录
# 可根据需要添加更多格式（如 .bmp, .webp 等）
cp *.jpg *.jpeg *.png *.gif backup/

# 删除所有临时文件
rm *.tmp *~

# 重命名多个文件（需要 rename 命令）
rename 's/\.txt$/.md/' *.txt
```

### 高效文件操作

```bash
# 创建多个目录
mkdir -p project/{src,docs,tests,data}

# 一次性创建多个文件
touch file{1..5}.txt
# 创建：file1.txt file2.txt file3.txt file4.txt file5.txt

# 批量重命名（使用循环）
for f in *.txt; do mv "$f" "${f%.txt}.md"; done

# 查找并删除空文件
find . -type f -empty -delete

# 查找最大的 10 个文件
du -ah | sort -rh | head -10
```

---

## 📊 文件操作最佳实践

### 安全删除

```bash
# ❌ 危险：直接删除
rm -rf *

# ✅ 安全：先确认
ls -la
rm -ri *  # -i 会逐个确认

# ✅ 更安全：使用 trash（如果安装）
trash *   # 移动到回收站
```

### 备份习惯

```bash
# 修改前先备份
cp important.txt important.txt.bak
cp important.txt important.txt.$(date +%Y%m%d)

# 创建备份目录
mkdir -p backup/$(date +%Y%m%d)
cp *.txt backup/$(date +%Y%m%d)/
```

### 组织项目结构

```bash
# 标准项目结构
mkdir -p myproject/{src,docs,tests,data,scripts}
cd myproject

# 创建基础文件
touch README.md
touch src/__init__.py
touch .gitignore

# 查看结构
tree -L 2
```

---

## 🧪 实战练习

### 练习 1：整理下载目录

```bash
# 假设你的下载目录有很多杂乱文件
cd ~/Downloads

# 1. 查看有什么文件
ls -lh

# 2. 创建分类目录
mkdir -p {images,documents,archives,installers}

# 3. 分类移动
mv *.jpg *.png *.gif images/
mv *.pdf *.doc *.docx *.xls documents/
mv *.zip *.tar.gz *.rar archives/
mv *.dmg *.exe *.deb installers/

# 4. 确认结果
ls -la
```

### 练习 2：项目初始化

```bash
# 创建新项目
mkdir -p myapp/{src,tests,docs,config,data}
cd myapp

# 创建基础文件
touch README.md
touch src/main.py
touch src/__init__.py
touch tests/__init__.py
touch .gitignore
touch requirements.txt

# 写入 README
echo "# My App" > README.md
echo "" >> README.md
echo "A sample project." >> README.md

# 查看结构
find . -type f | head -20
```

### 练习 3：文件权限实践

```bash
# 创建测试文件
touch private.txt
touch public.txt
touch script.sh

# 设置权限
chmod 600 private.txt   # 只有自己能读写
chmod 644 public.txt    # 自己能读写，别人只能读
chmod 755 script.sh     # 自己能执行，别人能读和执行

# 验证
ls -l private.txt public.txt script.sh

# 尝试执行
./script.sh  # 如果可以执行的话
```

---

## 📝 常见问题

### Q: 误删了文件怎么办？

```bash
# 如果刚删除，尝试恢复（不一定成功）
# Linux: 使用 extundelete（需要安装）
# 最好：养成备份习惯，使用 trash 命令
```

### Q: 如何查看文件占用的空间？

```bash
# 单个文件
ls -lh file.txt

# 目录大小
du -sh directory/

# 详细列出
du -ah | sort -rh | head -20
```

### Q: 如何找到最近修改的文件？

```bash
# 最近 7 天修改的文件
find . -type f -mtime -7

# 最近 24 小时修改的文件
find . -type f -mtime -1

# 按时间排序列出
ls -lt | head -20
```

---

## ✅ 本课小结

```
核心要点：

1. ls -l 查看详细信息，-h 人类可读大小

2. 文件权限：rwx 分别对应 4,2,1

3. 通配符 * 和 ? 可以批量操作文件

4. 删除文件前一定要确认（rm -ri）

5. 重要操作前养成备份习惯

6. 用合理的目录结构组织项目
```

---

## 📚 延伸阅读

- 管道和重定向 → 03-pipes-redirection.md
- 文本处理 → 02-text-processing.md
- 命令速查表 → resources/command-cheatsheet.md

---

## 🤔 思考题

1. `chmod 755` 和 `chmod 644` 有什么区别？各适用于什么场景？
2. 如何安全地删除一个包含重要文件的目录？
3. 通配符 `*.txt` 和 `*txt` 有什么区别？

> 💡 可以把你的思考告诉 AI，让它帮你深化理解

---

**下一步**: [2.2 文本处理](./02-text-processing.md)
