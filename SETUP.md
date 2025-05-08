# 学术周报生成器设置指南

你的仓库已成功初始化并配置了必要的文件。为了让系统正常工作，还需要完成以下几个步骤：

## 1. 启用GitHub Pages

1. 前往GitHub仓库 [https://github.com/Jannhsu/paper_summary](https://github.com/Jannhsu/paper_summary)
2. 点击"Settings"选项卡
3. 在左侧边栏中找到"Pages"
4. 在"Source"部分，选择"main"分支
5. 点击"Save"
6. 稍等片刻，GitHub Pages将会部署你的网站

## 2. 配置GitHub Actions密钥

为了使自动更新脚本能够正常工作，你需要添加Perplexity API密钥到GitHub Actions密钥中：

1. 前往GitHub仓库 [https://github.com/Jannhsu/paper_summary](https://github.com/Jannhsu/paper_summary)
2. 点击"Settings"选项卡
3. 在左侧边栏中找到"Secrets and variables" -> "Actions"
4. 点击"New repository secret"
5. 添加一个名为`PERPLEXITY_API_KEY`的密钥，值为`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`
6. 点击"Add secret"保存

## 3. 手动触发GitHub Actions工作流（可选）

如果想立即生成内容而不等待定时触发：

1. 前往GitHub仓库 [https://github.com/Jannhsu/paper_summary](https://github.com/Jannhsu/paper_summary)
2. 点击"Actions"选项卡
3. 在左侧找到"Update Academic Data"工作流
4. 点击"Run workflow"按钮
5. 在弹出的下拉菜单中点击"Run workflow"确认

## 4. 访问你的GitHub Pages网站

完成以上步骤后，你可以通过以下URL访问你的学术周报生成器：

```
https://jannhsu.github.io/paper_summary/
```

注意：GitHub Pages部署可能需要几分钟时间。如果网站不能立即访问，请稍等片刻再试。

## 常见问题排查

- 如果GitHub Actions工作流执行失败，检查工作流日志了解具体错误信息
- 如果网站显示但无法加载数据，可能是因为academic_data.json文件尚未生成，请手动触发GitHub Actions工作流
- 如果仍然遇到问题，可以检查浏览器控制台日志获取更详细的错误信息 