# 学术周报生成器 - GitHub Pages 版

这是一个使用Perplexity API自动生成学术文献摘要的工具，可以部署在GitHub Pages上，通过GitHub API实现内容持久化，使所有用户都能看到相同的内容。

## 特性

- 基于关键词自动获取最新学术论文
- 自动生成论文摘要和深入解读
- 每日自动更新内容
- 使用GitHub存储数据，实现内容共享
- 移动端友好的响应式设计
- 通过GitHub Actions实现定时自动更新

## 如何部署

### 1. Fork本仓库

点击GitHub仓库右上角的Fork按钮，创建你自己的副本。

### 2. 启用GitHub Pages

1. 转到你Fork的仓库
2. 点击"Settings"选项卡
3. 在左侧边栏中找到"Pages"
4. 在"Source"部分，选择"main"分支
5. 点击"Save"
6. 稍等片刻，GitHub Pages将会部署你的网站

### 3. 配置GitHub API访问令牌（可选，但推荐）

为了启用内容持久化，你需要一个GitHub个人访问令牌：

1. 在GitHub上，点击你的头像 -> Settings -> Developer settings -> Personal access tokens -> Tokens (classic)
2. 点击"Generate new token"
3. 给令牌起个名字，如"学术周报生成器"
4. 勾选"repo"权限（这允许访问仓库内容）
5. 点击"Generate token"
6. 复制生成的令牌（重要：令牌只会显示一次！）

### 4. 配置GitHub Actions密钥

为了使自动更新脚本能够正常工作，你需要添加Perplexity API密钥到GitHub Actions密钥中：

1. 转到你Fork的仓库
2. 点击"Settings"选项卡
3. 在左侧边栏中找到"Secrets and variables" -> "Actions"
4. 点击"New repository secret"
5. 添加一个名为`PERPLEXITY_API_KEY`的密钥，值为你的Perplexity API密钥
6. 点击"Add secret"保存

### 5. 修改配置

在`index.html`文件中，找到并编辑以下配置：

```javascript
// GitHub API configuration
const GITHUB_USERNAME = "your-github-username"; // 修改为你的GitHub用户名
const GITHUB_REPO = "paper_summary"; // 修改为你的仓库名
const GITHUB_TOKEN = ""; // 粘贴你的GitHub访问令牌
const GITHUB_API_BASE = `https://api.github.com/repos/${GITHUB_USERNAME}/${GITHUB_REPO}/contents`;
const GITHUB_DATA_FILE = "academic_data.json"; // 存储数据的文件名
const USE_GITHUB_STORAGE = true; // 修改为true启用GitHub存储
```

### 6. 配置Perplexity API

为了获取最新学术论文，你需要一个Perplexity API密钥：

1. 注册并获取一个[Perplexity API密钥](https://perplexity.ai)
2. 在`index.html`文件中，修改API密钥：

```javascript
const PERPLEXITY_API_KEY = "your-perplexity-api-key-here"; 
```

## 自动化更新

系统提供两种自动更新内容的方式：

1. **浏览器自动更新**：当有用户在北京时间早上8:00访问网站时，系统会自动更新内容。

2. **GitHub Actions自动更新**：无需用户访问，系统每天都会通过GitHub Actions自动更新内容。
   - 这个功能由`.github/workflows/update-academic-data.yml`文件控制
   - 每天UTC时间0:00（北京时间8:00）自动运行
   - 从Perplexity API获取最新论文，并更新GitHub中的数据文件

你可以在GitHub仓库的"Actions"选项卡中查看更新日志和状态。

## 如何工作

1. 当用户访问网站时，系统首先尝试从GitHub上的`academic_data.json`文件加载数据
2. 如果找到数据，则显示共享内容（所有用户看到相同的内容）
3. 如果找不到数据或启用了手动刷新，系统将调用Perplexity API获取最新论文
4. 获取的内容将保存到GitHub仓库中，供所有用户查看
5. 系统每天北京时间早上8:00自动更新内容（通过GitHub Actions或浏览器访问触发）

## 问题排查

- 如果页面无法加载数据，请检查浏览器控制台是否有错误信息
- 确保已正确配置GitHub用户名、仓库名和API令牌
- 检查Perplexity API密钥是否有效
- 如果GitHub API调用失败，系统会回退到本地存储模式
- 检查GitHub Actions日志以确定自动更新是否正常运行

## 自定义

- 修改`userKeywords`数组可以更改默认关键词
- 调整UI样式可以编辑CSS部分
- 可以修改API调用频率和自动更新时间
- 在`.github/workflows/update-academic-data.yml`文件中调整自动更新时间表

## 许可证

MIT 