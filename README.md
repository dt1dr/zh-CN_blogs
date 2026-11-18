# 稻田里的人的个人博客

## 简介

部署于Github pages， 采用hexo框架 + butterfly主题构建的静态博客页面，用于分享学生时期有趣的技术笔记or生活文章。目前仅支持简中。

A static blog page based on Github pages + hexo(framework) + butterfly(theme). Here is for tech and life.
**Currently, it only supports Simplified Chinese!**

## 站点URL

https://dt1dr.github.io/zh-CN_blogs

## Markdown 格式化

安装项目依赖后，可以用以下命令检查、批量格式化或只格式化一篇文章：

```bash
npm run format:md:check
npm run format:md
npx prettier --write source/_posts/2026-10-14-PL-0.md
```

批量命令覆盖根目录的 README、`source/` 和 `scaffolds/` 中的 Markdown。配置保留正文的换行，也关闭了对围栏内代码的单独格式化。新写的 LaTeX 块公式建议把起止 `$$` 各放一行，并在整个公式块前后留空行。《图神经网络学习：图同构网络》因旧公式写法会被 Prettier 误改，已加入 `.prettierignore`。
