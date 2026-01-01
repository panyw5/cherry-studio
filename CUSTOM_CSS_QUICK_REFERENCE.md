# Cherry Studio Custom CSS 快速参考指南

## 📚 文件说明

本项目包含以下文档：

1. **CUSTOM_CSS_ANALYSIS.md** - 完整的 CSS 设计分析文档
2. **CUSTOM_CSS_TEMPLATES.css** - 10 个预设主题模板集合
3. **MY_CUSTOM_CSS.css** - 个人自定义样式示例（推荐使用）

## 🚀 快速开始

### 步骤 1: 打开自定义 CSS 设置

1. 启动 Cherry Studio
2. 点击左下角设置图标（⚙️）
3. 选择 "显示" 标签
4. 滚动到 "自定义 CSS" 部分

### 步骤 2: 选择并应用模板

#### 方案 A - 使用个人推荐模板（推荐）

```bash
# 打开 MY_CUSTOM_CSS.css 文件
# 复制全部内容
# 粘贴到 Cherry Studio 的自定义 CSS 编辑器
# 保存并查看效果
```

#### 方案 B - 使用预设主题模板

```bash
# 打开 CUSTOM_CSS_TEMPLATES.css 文件
# 选择你喜欢的模板（共 10 个）
# 复制该模板的代码
# 粘贴到编辑器
# 保存
```

#### 方案 C - 混合使用

```bash
# 可以从不同模板中选择部分代码组合使用
# 例如：模板 1 的消息气泡 + 模板 7 的字体设置
```

## 🎨 10 个预设主题模板

1. **极简优雅主题** - 简洁大方，专注内容
2. **赛博朋克风格** - 霓虹灯效果，科技感强
3. **温暖舒适主题** - 暖色调，护眼
4. **玻璃拟态** - 半透明毛玻璃效果
5. **高对比度主题** - 增强可读性
6. **紧凑布局** - 节省空间
7. **舒适阅读** - 大字体，宽行距
8. **彩虹渐变主题** - 多彩活力
9. **深色 OLED 纯黑** - 省电，适合 OLED 屏
10. **毛玻璃模糊增强** - 柔和梦幻

## 🔧 常用选择器速查

### 消息相关
```css
.message-user                       /* 用户消息 */
.message-assistant                  /* AI 助手消息 */
.message-content-container          /* 消息内容容器 */
.message-header                     /* 消息头部 */
.MessageFooter                      /* 消息底部 */
```

### Markdown 内容
```css
.markdown                           /* Markdown 容器 */
.markdown h1, .markdown h2          /* 标题 */
.markdown p                         /* 段落 */
.markdown code                      /* 行内代码 */
.markdown pre                       /* 代码块 */
.markdown table                     /* 表格 */
.markdown blockquote                /* 引用 */
.markdown a                         /* 链接 */
```

### 主题相关
```css
[theme-mode='dark']                 /* 暗色主题 */
[theme-mode='light']                /* 亮色主题 */
body[os='mac']                      /* macOS 系统 */
body[os='windows']                  /* Windows 系统 */
[navbar-position='left']            /* 左侧导航栏 */
[navbar-position='top']             /* 顶部导航栏 */
```

## 🎯 常用 CSS 变量

### 颜色变量
```css
var(--color-primary)                /* 主题色 */
var(--color-primary-soft)           /* 主题色半透明 */
var(--color-primary-mute)           /* 主题色浅色 */
var(--color-background)             /* 背景色 */
var(--color-background-soft)        /* 浅背景色 */
var(--color-text)                   /* 文字色 */
var(--color-text-secondary)         /* 次要文字色 */
var(--color-border)                 /* 边框色 */
var(--color-hover)                  /* 悬停色 */
var(--color-icon)                   /* 图标色 */
```

### 布局变量
```css
var(--radius)                       /* 圆角大小 */
var(--list-item-border-radius)      /* 列表项圆角 */
var(--scrollbar-width)              /* 滚动条宽度 */
var(--font-family)                  /* 全局字体 */
var(--code-font-family)             /* 代码字体 */
```

### 聊天变量
```css
var(--chat-background-user)         /* 用户消息背景 */
var(--chat-background-assistant)    /* AI 消息背景 */
```

## 💡 常见自定义需求

### 1. 修改消息气泡颜色
```css
.message-user .message-content-container {
  background: #your-color !important;
}
```

### 2. 调整字体大小
```css
body {
  font-size: 16px !important;
}
```

### 3. 修改圆角大小
```css
:root {
  --radius: 16px;
}
```

### 4. 美化代码块
```css
.markdown pre {
  border-radius: 12px !important;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}
```

### 5. 自定义滚动条
```css
::-webkit-scrollbar-thumb {
  background: var(--color-primary);
  border-radius: 10px;
}
```

### 6. 增强链接样式
```css
.markdown a {
  color: var(--color-primary) !important;
  border-bottom: 1px solid var(--color-primary);
}
```

### 7. 表格美化
```css
.markdown th {
  background: var(--color-primary) !important;
  color: white !important;
}
```

### 8. 图片圆角和阴影
```css
.markdown img {
  border-radius: 12px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
}
```

## 🐛 调试技巧

### 1. 打开开发者工具
- **macOS**: `Cmd + Option + I`
- **Windows/Linux**: `F12`

### 2. 查看自定义样式
```javascript
// 在 Console 中运行
document.getElementById('user-defined-custom-css').textContent
```

### 3. 临时测试样式
```javascript
// 在 Console 中快速测试
const style = document.createElement('style');
style.textContent = '.markdown { font-size: 18px; }';
document.head.appendChild(style);
```

### 4. 查看当前主题
```javascript
// 查看当前主题模式
document.body.getAttribute('theme-mode');  // 'dark' 或 'light'
```

### 5. 查看 CSS 变量值
```javascript
// 查看 CSS 变量的实际值
getComputedStyle(document.body).getPropertyValue('--color-primary');
```

## ⚠️ 注意事项

### 1. 使用 !important
某些样式可能需要 `!important` 来覆盖默认样式：
```css
.message-user {
  background: #ff0000 !important;  /* 确保优先级最高 */
}
```

### 2. 考虑主题兼容性
为亮色和暗色模式都提供适当样式：
```css
/* 暗色模式 */
[theme-mode='dark'] .my-element {
  color: white;
}

/* 亮色模式 */
[theme-mode='light'] .my-element {
  color: black;
}
```

### 3. 测试响应式
```css
@media (max-width: 768px) {
  /* 小屏幕样式 */
}
```

### 4. 性能考虑
避免过度使用 `backdrop-filter` 和复杂动画，可能影响性能。

## 🔗 相关资源

- **官方网站**: https://cherry-ai.com
- **GitHub**: https://github.com/CherryHQ/cherry-studio
- **CSS 模板库**: https://cherrycss.com
- **文档**: 查看项目中的 CLAUDE.md

## 📖 学习资源

- [CSS 变量教程](https://developer.mozilla.org/zh-CN/docs/Web/CSS/--*)
- [CSS 选择器参考](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Selectors)
- [Flexbox 布局](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [CSS 动画](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Animations)

## 🎁 额外功能模块（可选添加）

### 平滑滚动
```css
html { scroll-behavior: smooth; }
```

### 淡入动画
```css
.message-content-container {
  animation: fadeIn 0.3s ease-in;
}
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}
```

### 悬停效果
```css
.message-content-container:hover {
  transform: translateY(-2px);
  transition: all 0.2s ease;
}
```

### 选中文本高亮
```css
::selection {
  background: var(--color-primary);
  color: white;
}
```

## 🤔 常见问题

### Q: 样式没有生效？
A: 
1. 检查是否保存了设置
2. 尝试使用 `!important`
3. 重启 Cherry Studio
4. 检查选择器是否正确

### Q: 如何恢复默认样式？
A: 清空自定义 CSS 编辑器中的所有内容并保存

### Q: 可以同时使用多个模板吗？
A: 可以！复制多个模板的代码，合并后粘贴即可

### Q: 如何只修改某个部分？
A: 从模板中复制你想要的部分，而不是整个模板

### Q: 修改后需要重启吗？
A: 通常不需要，保存后即时生效

## 💬 反馈与贡献

如果你创建了很酷的自定义样式，欢迎：
- 在 GitHub 上提交 Pull Request
- 分享到社区
- 访问 https://cherrycss.com 上传你的模板

---

**享受自定义的乐趣！** 🎨✨
