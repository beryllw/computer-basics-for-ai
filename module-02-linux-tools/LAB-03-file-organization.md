# 实验 03：文件整理

> 运用所学命令完成文件整理任务

---

## 🎯 实验目标

- 综合运用文件操作命令
- 使用通配符和管道
- 完成实际的文件整理任务

---

## 📋 实验准备

**时间：** 30-45 分钟

**需要：**
- 终端
- 一些测试文件（实验中会创建）

---

## 🔬 实验任务

### 场景：整理杂乱的下载目录

假设你的下载目录有很多杂乱的文件，需要分类整理。

### 步骤 1：创建测试环境

```bash
# 1. 创建"下载目录"
mkdir -p ~/fake_downloads
cd ~/fake_downloads

# 2. 创建各种类型的文件
touch report.pdf presentation.pdf notes.txt readme.txt
touch photo1.jpg photo2.png screenshot.gif
touch archive.zip backup.tar.gz data.rar
touch installer.exe package.dmg app.deb
touch script.py code.js style.css index.html
touch data.csv config.json log.txt

# 3. 查看创建的文件
ls -la
```

### 步骤 2：创建分类目录

```bash
# 创建分类目录
mkdir -p {documents,images,archives,installers,code,misc}

# 查看结构
ls -la
```

### 步骤 3：分类移动文件

```bash
# 文档
mv *.pdf documents/
mv *.txt documents/

# 图片
mv *.jpg *.png *.gif images/

# 压缩包
mv *.zip *.tar.gz *.rar archives/

# 安装程序
mv *.exe *.dmg *.deb installers/

# 代码
mv *.py *.js *.css *.html code/

# 其他（如果有）
mv *.json misc/
```

### 步骤 4：验证结果

```bash
# 查看每个目录的内容
echo "=== Documents ==="
ls -la documents/

echo "=== Images ==="
ls -la images/

echo "=== Archives ==="
ls -la archives/

echo "=== Installers ==="
ls -la installers/

echo "=== Code ==="
ls -la code/

echo "=== Misc ==="
ls -la misc/

# 统计每个目录的文件数
echo ""
echo "=== 文件统计 ==="
echo "Documents: $(ls documents/ | wc -l) 个文件"
echo "Images: $(ls images/ | wc -l) 个文件"
echo "Archives: $(ls archives/ | wc -l) 个文件"
echo "Installers: $(ls installers/ | wc -l) 个文件"
echo "Code: $(ls code/ | wc -l) 个文件"
echo "Misc: $(ls misc/ | wc -l) 个文件"
```

### 步骤 5：创建索引文件

```bash
# 为每个目录创建索引
for dir in documents images archives installers code misc; do
    echo "=== $dir ===" > $dir/INDEX.txt
    echo "生成时间：$(date)" >> $dir/INDEX.txt
    echo "" >> $dir/INDEX.txt
    echo "文件列表：" >> $dir/INDEX.txt
    ls -lh $dir/ | grep -v '^total' | grep -v '^\.' >> $dir/INDEX.txt
done

# 查看索引
cat documents/INDEX.txt
```

### 步骤 6：清理实验环境

```bash
# 回到 home 目录
cd ~

# 删除实验目录
rm -rf ~/fake_downloads

# 确认删除
ls ~/fake_downloads 2>&1
```

---

## 🎯 进阶挑战

### 挑战 1：编写整理脚本

```bash
# 创建一个可复用的整理脚本
cat > organize.sh << 'EOF'
#!/bin/bash
# 文件整理脚本

# 检查参数
if [ $# -eq 0 ]; then
    echo "用法：$0 <目录>"
    exit 1
fi

TARGET_DIR=$1

# 进入目录
cd $TARGET_DIR || exit 1

# 创建分类目录
mkdir -p {documents,images,archives,code,misc}

# 移动文件
mv *.pdf *.txt *.doc *.docx documents/ 2>/dev/null
mv *.jpg *.png *.gif *.bmp images/ 2>/dev/null
mv *.zip *.tar.gz *.rar *.7z archives/ 2>/dev/null
mv *.py *.js *.css *.html *.sh code/ 2>/dev/null

echo "整理完成！"
EOF

chmod +x organize.sh
```

### 挑战 2：按大小分类

```bash
# 创建按大小分类的脚本
cat > sort_by_size.sh << 'EOF'
#!/bin/bash

mkdir -p {small,medium,large}

# 小于 1KB
find . -maxdepth 1 -type f -size -1k -exec mv {} small/ \;

# 1KB - 1MB
find . -maxdepth 1 -type f -size +1k -size -1M -exec mv {} medium/ \;

# 大于 1MB
find . -maxdepth 1 -type f -size +1M -exec mv {} large/ \;

echo "按大小分类完成！"
EOF

chmod +x sort_by_size.sh
```

---

## 📊 实验记录

记录你的操作和发现：

```
1. 我创建了多少个测试文件：____

2. 每个分类目录的文件数：
   - Documents: ____
   - Images: ____
   - Archives: ____
   - Installers: ____
   - Code: ____
   - Misc: ____

3. 遇到的问题：
   _________________________________
   _________________________________

4. 我的解决方案：
   _________________________________
   _________________________________
```

---

## ✅ 实验检查清单

完成实验后，确认你能：

- [ ] 使用 mkdir 创建目录结构
- [ ] 使用通配符批量选择文件
- [ ] 使用 mv 移动文件
- [ ] 使用 ls 和 wc 统计文件
- [ ] 使用循环处理多个目录
- [ ] 清理实验环境

---

## 🤔 思考题

1. 如果有同名文件怎么办？如何避免覆盖？
2. 如何修改脚本让它能处理子目录中的文件？
3. 如果要按日期分类，应该如何设计？

---

**实验完成！** 🎉

下一个实验：[LAB-04: 日志分析](./LAB-04-log-analysis.md)
