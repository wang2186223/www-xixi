
# 📚 Git推送教程 - 小说网站管理指南


### 典型使用场景

#### 场景1: 添加新小说
```bash
# 1. 将新小说文件夹放入 source/
# 2. 运行增量构建
python3 tools/build-website.py

# 输出: 检测到新增小说，自动生成所有页面
```

#### 场景2: 更新现有小说章节
```bash
# 1. 修改 source/小说名/书籍正文.txt
# 2. 运行增量构建  
python3 tools/build-website.py

# 输出: 检测到内容变化，重新生成该小说的所有页面
```

#### 场景3: 日常维护
```bash
# 定期检查和更新
python3 tools/build-website.py

# 如果没有变化，几秒钟完成
# 如果有变化，只重新生成需要的部分
```


## 🎯 快速开始

当你新增小说后，只需要这一条命令：
```bash
git add . && git commit -m "增加新小说：[小说名]" && git push origin main
```

## 📋 详细步骤解析

### 第一步：检查当前状态
```bash
git status
```

**这个命令会告诉你：**
- 🔴 红色文件 = 已修改但未添加到暂存区
- 🟢 绿色文件 = 已添加到暂存区，准备提交
- ❓ Untracked = 新文件，Git还不知道

**示例输出：**
```
Changes not staged for commit:
        modified:   docs/index.html
        modified:   docs/sitemap.xml

Untracked files:
        docs/novels/new-novel/
        source/NEW-NOVEL/
```

### 第二步：添加文件到暂存区
```bash
git add .
```

**选项说明：**
- `git add .` = 添加当前目录下所有变化
- `git add 文件名` = 只添加特定文件
- `git add docs/` = 只添加docs目录的变化

### 第三步：提交更改
```bash
git commit -m "提交说明"
```

**好的提交说明示例：**
- ✅ `"📚 增加新小说：霸道总裁的替身新娘 (45章)"`
- ✅ `"🔧 修复章节导航问题"`
- ✅ `"🎨 优化首页布局和样式"`
- ❌ `"更新"` (太简单)
- ❌ `"fix bug"` (不够具体)

### 第四步：推送到GitHub
```bash
git push origin main
```

**推送成功标志：**
```
Writing objects: 100% (58/58), 712.65 KiB | 10.18 MiB/s, done.
Total 58 (delta 48), reused 0 (delta 0)
To https://github.com/wang2186223/html-01.git
   3922be7..0b8c1b9  main -> main
```

## 🔄 完整工作流程

### 新增小说的标准流程

1. **准备小说文件**
   ```bash
   # 创建小说目录（如果还没有）
   mkdir -p source/新小说名
   
   # 放入必要文件：
   # - 书籍正文.txt
   # - 书籍描述.txt
   # - 封面图片.png/jpg
   ```

2. **生成网站文件**
   ```bash
   python3 tools/build-website.py
   ```
   
   **输出解读：**
   ```
   📖 检查小说: 新小说名
     ✅ 新增: 新小说名 (45章)
   🔄 构建小说: 新小说名
   ✅ 网站构建完成!
   ```

3. **检查生成结果**
   ```bash
   git status
   
   # 应该看到：
   # - docs/novels/新小说名/ (新目录)
   # - docs/covers/新小说名-*.png (封面)
   # - docs/index.html (已更新)
   # - docs/sitemap.xml (已更新)
   ```

4. **推送到GitHub**
   ```bash
   git add . && git commit -m "📚 增加新小说：新小说名 (45章)" && git push origin main
   ```

## 🛠️ 常用Git命令

### 查看类命令
```bash
git status              # 查看当前状态
git log --oneline -5    # 查看最近5次提交
git remote -v           # 查看远程仓库地址
git branch -v           # 查看当前分支信息
```

### 操作类命令
```bash
git add .               # 添加所有变化
git commit -m "说明"    # 提交变化
git push origin main    # 推送到远程
git pull origin main    # 拉取远程更新
```

### 撤销类命令
```bash
git restore 文件名      # 撤销文件修改
git reset HEAD~1        # 撤销最后一次提交
git checkout -- .      # 撤销所有未提交的修改
```

## 📊 推送历史记录

### 最近的成功推送
```
0b8c1b9 📚 增加新小说：VEILBORN (44章)          # 刚刚推送
3922be7 🎉 优化首页内容更新检测                 # 之前推送
e04d25f Initial commit: Novel website generator  # 初始提交
```

## ⚠️ 常见问题解决

### 问题1：推送失败
```bash
# 错误信息：Updates were rejected
# 解决方案：先拉取远程更新
git pull origin main
git push origin main
```

### 问题2：合并冲突
```bash
# 错误信息：CONFLICT (merge)
# 解决方案：手动解决冲突后
git add .
git commit -m "解决合并冲突"
git push origin main
```

### 问题3：忘记提交说明
```bash
# 如果执行了 git commit 但忘记 -m
# Git会打开编辑器，输入提交说明后保存退出即可
```

### 问题4：文件太大
```bash
# 如果有大文件无法推送
# 检查并删除不必要的大文件
du -sh source/*/
```

## 🎯 最佳实践

### 1. 提交说明规范
- 📚 新增小说
- 🔧 修复问题
- 🎨 样式优化
- ⚡ 性能优化
- 📝 文档更新

### 2. 推送频率
- ✅ 新增小说后立即推送
- ✅ 修复重要问题后推送
- ✅ 一天结束时推送当天所有改动
- ❌ 避免过于频繁的小改动推送

### 3. 备份策略
- 定期推送到GitHub（自动备份）
- 重要版本打标签：`git tag v1.0`
- 保持本地代码整洁

## 📞 应急联系

如果遇到复杂的Git问题：
1. 先备份当前工作
2. 记录错误信息
3. 尝试基本的撤销命令
4. 如需帮助，提供具体的错误信息

---

*最后更新：2025年9月14日*
*当前仓库：https://github.com/wang2186223/html-01*
