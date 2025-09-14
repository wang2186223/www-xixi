
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
