# Cherry Studio CSS 自定义指南

欢迎使用 Cherry Studio 的 CSS 自定义功能！本指南将帮助你完全掌握界面定制。

## 📋 目录

- [快速开始](#快速开始)
- [文档概览](#文档概览)
- [使用建议](#使用建议)
- [示例展示](#示例展示)

## 🚀 快速开始

### 3 步完成自定义

1. **选择模板**
   - 打开 `MY_CUSTOM_CSS.css`（推荐新手）
   - 或浏览 `CUSTOM_CSS_TEMPLATES.css` 中的 10 个主题

2. **复制代码**
   - 复制整个文件或选择部分代码

3. **应用样式**
   - 打开 Cherry Studio
   - 进入：设置 → 显示 → 自定义 CSS
   - 粘贴代码 → 保存

就这么简单！🎉

## 📚 文档概览

### 1. CUSTOM_CSS_ANALYSIS.md
**完整的技术分析文档**
- ✅ CSS 架构详解
- ✅ 主题系统原理
- ✅ Custom CSS 实现机制
- ✅ 所有可用的 CSS 变量
- ✅ 最佳实践和调试技巧

**适合人群**: 想深入了解系统的开发者

### 2. CUSTOM_CSS_TEMPLATES.css
**10 个预设主题模板**
1. 极简优雅主题
2. 赛博朋克风格
3. 温暖舒适主题
4. 玻璃拟态
5. 高对比度主题
6. 紧凑布局
7. 舒适阅读
8. 彩虹渐变主题
9. 深色 OLED 纯黑
10. 毛玻璃模糊增强

**适合人群**: 想要快速应用不同风格的用户

### 3. MY_CUSTOM_CSS.css
**个人推荐的完整样式模板**
- ✅ 消息气泡美化
- ✅ Markdown 内容优化
- ✅ 代码块美化
- ✅ 表格、列表、图片优化
- ✅ 滚动条美化
- ✅ 输入框优化
- ✅ 亮/暗模式适配
- ✅ 详细注释说明

**适合人群**: 想要一套完整优化方案的用户（推荐）

### 4. CUSTOM_CSS_QUICK_REFERENCE.md
**快速参考手册**
- ✅ 常用选择器速查
- ✅ CSS 变量列表
- ✅ 常见需求代码片段
- ✅ 调试技巧
- ✅ 常见问题解答

**适合人群**: 需要快速查找某个功能的用户

## 💡 使用建议

### 新手推荐路径

```
第一步：阅读 CUSTOM_CSS_QUICK_REFERENCE.md（5分钟）
       ↓
第二步：使用 MY_CUSTOM_CSS.css（直接复制粘贴）
       ↓
第三步：查看效果，按需微调
       ↓
第四步：浏览 CUSTOM_CSS_TEMPLATES.css 尝试其他风格
```

### 进阶用户路径

```
第一步：阅读 CUSTOM_CSS_ANALYSIS.md（了解系统）
       ↓
第二步：混合使用多个模板的代码
       ↓
第三步：创建自己的独特样式
       ↓
第四步：分享到社区或 cherrycss.com
```

## 🎨 示例展示

### 示例 1: 修改主题色为紫色

```css
:root {
  --color-primary: #8b5cf6;
  --color-primary-soft: #8b5cf699;
  --color-primary-mute: #8b5cf633;
}
```

### 示例 2: 增大字体

```css
body {
  font-size: 16px !important;
}

.markdown {
  font-size: 16px !important;
  line-height: 1.8 !important;
}
```

### 示例 3: 圆润气泡

```css
.message-user .message-content-container {
  border-radius: 20px 20px 4px 20px !important;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.message-assistant .message-content-container {
  border-radius: 20px 20px 20px 4px !important;
}
```

### 示例 4: 霓虹边框（赛博朋克）

```css
[theme-mode='dark'] .message-user .message-content-container {
  border: 1px solid #00ffff;
  box-shadow: 0 0 10px #00ffff, 0 0 20px #00ffff;
  background: rgba(0, 255, 255, 0.05) !important;
}
```

### 示例 5: 玻璃拟态

```css
.message-content-container {
  background: rgba(255, 255, 255, 0.05) !important;
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}
```

## 🔧 常用技巧

### 1. 快速测试样式

在开发者工具 Console 中：
```javascript
const style = document.createElement('style');
style.textContent = '.markdown { font-size: 20px !important; }';
document.head.appendChild(style);
```

### 2. 查看当前使用的样式

```javascript
// 查看自定义 CSS 内容
document.getElementById('user-defined-custom-css').textContent

// 查看当前主题
document.body.getAttribute('theme-mode')
```

### 3. 混合多个模板

```css
/* 从模板 1 复制消息气泡样式 */
.message-user .message-content-container {
  /* ... */
}

/* 从模板 7 复制字体设置 */
body {
  font-size: 16px !important;
}

/* 从模板 4 复制玻璃效果 */
.message-content-container {
  backdrop-filter: blur(10px);
}
```

## 📖 学习资源

### 官方文档
- **Cherry Studio GitHub**: https://github.com/CherryHQ/cherry-studio
- **CSS 模板库**: https://cherrycss.com
- **官方网站**: https://cherry-ai.com

### CSS 学习
- [MDN CSS 文档](https://developer.mozilla.org/zh-CN/docs/Web/CSS)
- [CSS-Tricks](https://css-tricks.com/)
- [Can I Use](https://caniuse.com/) - 检查 CSS 兼容性

### 设计灵感
- [Dribbble](https://dribbble.com/)
- [Behance](https://www.behance.net/)
- [Pinterest](https://www.pinterest.com/)

## ❓ 常见问题

### Q: 为什么我的样式没有生效？

**A**: 按以下步骤排查：
1. ✅ 确认已保存设置
2. ✅ 尝试添加 `!important`
3. ✅ 检查选择器是否正确
4. ✅ 打开开发者工具检查是否有语法错误
5. ✅ 尝试重启 Cherry Studio

### Q: 如何恢复默认样式？

**A**: 在自定义 CSS 编辑器中删除所有内容，然后保存。

### Q: 可以同时使用多个模板吗？

**A**: 可以！复制你想要的多个模板的代码，粘贴到编辑器中即可。

### Q: 我的样式会影响其他用户吗？

**A**: 不会。自定义 CSS 只在你的本地生效，不会影响其他用户。

### Q: 更新 Cherry Studio 后样式会丢失吗？

**A**: 不会。自定义 CSS 保存在用户配置中，更新不会影响。

### Q: 如何分享我的样式？

**A**: 
1. 复制你的 CSS 代码
2. 上传到 https://cherrycss.com
3. 或在 GitHub 提交 Pull Request
4. 或在社区分享

## 🎯 下一步

1. **立即开始**: 复制 `MY_CUSTOM_CSS.css` 到 Cherry Studio
2. **探索更多**: 浏览 `CUSTOM_CSS_TEMPLATES.css` 中的其他主题
3. **深入学习**: 阅读 `CUSTOM_CSS_ANALYSIS.md` 了解原理
4. **快速查找**: 使用 `CUSTOM_CSS_QUICK_REFERENCE.md` 作为速查手册

## 💬 反馈与贡献

如果你：
- 🐛 发现了问题
- 💡 有新的想法
- 🎨 创建了酷炫的样式
- 📝 想改进文档

欢迎：
- 在 GitHub 提交 Issue
- 提交 Pull Request
- 加入社区讨论
- 分享你的作品

## 📜 版权说明

本指南和模板遵循 Cherry Studio 项目的开源协议。
欢迎自由使用、修改和分享。

---

## 🌟 致谢

感谢 Cherry Studio 团队提供如此优秀的 AI 助手应用！

**开始你的定制之旅吧！** 🚀✨

---

*最后更新: 2025-10-07*
