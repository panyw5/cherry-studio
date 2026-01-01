# Cherry Studio 前端 CSS 设计分析

## 1. 项目 CSS 架构概览

### 1.1 使用的技术栈

Cherry Studio 项目使用了多种 CSS 技术和框架的组合：

1. **Tailwind CSS v4** - 原子化 CSS 框架
2. **styled-components** - CSS-in-JS 解决方案
3. **Ant Design (antd)** - UI 组件库
4. **Hero UI** - 自定义 UI 组件库
5. **原生 CSS 变量** - 用于主题系统
6. **CSS Modules** - 模块化样式

### 1.2 CSS 文件结构

```
src/renderer/src/assets/styles/
├── index.css           # 主入口文件，导入所有样式
├── tailwind.css        # Tailwind CSS 配置和自定义
├── color.css           # 颜色系统和主题变量
├── font.css            # 字体配置
├── markdown.css        # Markdown 渲染样式
├── ant.css             # Ant Design 自定义覆盖
├── scrollbar.css       # 滚动条样式
├── container.css       # 容器布局样式
├── animation.css       # 动画效果
├── richtext.css        # 富文本编辑器样式
└── responsive.css      # 响应式设计
```

## 2. 主题系统设计

### 2.1 CSS 变量系统

Cherry Studio 使用 CSS 变量实现强大的主题系统，支持亮色/暗色模式切换。

#### 核心变量（color.css）

**暗色主题 (默认)**
```css
:root {
  /* 基础颜色 */
  --color-background: #181818;
  --color-background-soft: #222222;
  --color-background-mute: #333333;
  --color-text: rgba(255, 255, 245, 0.9);
  --color-text-secondary: rgba(235, 235, 245, 0.7);
  
  /* 主色调 */
  --color-primary: #00b96b;
  --color-primary-soft: #00b96b99;
  --color-primary-mute: #00b96b33;
  
  /* 交互元素 */
  --color-border: #ffffff19;
  --color-hover: rgba(40, 40, 40, 1);
  --color-active: rgba(55, 55, 55, 1);
  --color-icon: #ffffff99;
  
  /* 聊天气泡 */
  --chat-background-user: rgba(255, 255, 255, 0.08);
  --chat-background-assistant: transparent;
  
  /* 导航栏 */
  --navbar-background-mac: rgba(20, 20, 20, 0.55);
  --navbar-background: #1f1f1f;
}
```

**亮色主题**
```css
[theme-mode='light'] {
  --color-background: #ffffff;
  --color-background-soft: rgba(0, 0, 0, 0.04);
  --color-text: rgba(0, 0, 0, 1);
  --color-icon: #00000099;
  --color-border: #00000019;
  --chat-background-user: rgba(0, 0, 0, 0.045);
  /* ... */
}
```

### 2.2 Tailwind CSS 变量

项目还使用 Tailwind v4 的新变量系统（tailwind.css）：

```css
:root {
  --radius: 0.625rem;
  --background: oklch(1 0 0);
  --foreground: oklch(0.141 0.005 285.823);
  --primary: oklch(0.21 0.006 285.885);
  --border: oklch(0.92 0.004 286.32);
  /* ... 更多 oklch 颜色空间变量 */
}
```

### 2.3 字体系统

```css
:root {
  --font-family: var(--user-font-family), Ubuntu, -apple-system, 
                 BlinkMacSystemFont, 'Segoe UI', system-ui, ...;
  
  --code-font-family: var(--user-code-font-family), 'Cascadia Code', 
                      'Fira Code', 'Consolas', Menlo, ...;
}
```

支持用户自定义字体：
- `--user-font-family` - 全局字体
- `--user-code-font-family` - 代码字体

## 3. Custom CSS 功能实现

### 3.1 功能入口

**设置页面位置：**
- 文件：`src/renderer/src/pages/settings/DisplaySettings/DisplaySettings.tsx`
- 路径：设置 → 显示 → 自定义 CSS

### 3.2 实现机制

#### 3.2.1 状态管理

使用 Redux 存储用户的自定义 CSS：

```typescript
// src/renderer/src/store/settings.ts
export interface SettingsState {
  customCss: string;
  // ...其他设置
}

// reducer
setCustomCss: (state, action: PayloadAction<string>) => {
  state.customCss = action.payload
}
```

#### 3.2.2 动态应用 CSS

在应用初始化时动态注入自定义样式：

```typescript
// src/renderer/src/hooks/useAppInit.ts
useEffect(() => {
  let customCssElement = document.getElementById('user-defined-custom-css') as HTMLStyleElement
  
  // 移除旧的自定义样式
  if (customCssElement) {
    customCssElement.remove()
  }

  // 添加新的自定义样式
  if (customCss) {
    customCssElement = document.createElement('style')
    customCssElement.id = 'user-defined-custom-css'
    customCssElement.textContent = customCss
    document.head.appendChild(customCssElement)
  }
}, [customCss])
```

#### 3.2.3 多窗口支持

自定义 CSS 在所有窗口类型中都会被应用：
- 主窗口（Main Window）
- 迷你窗口（Mini Window）
- 选择工具栏（Selection Toolbar）
- 选择操作窗口（Selection Action）

### 3.3 编辑器集成

使用 CodeMirror 编辑器提供语法高亮和代码补全：

```tsx
<CodeEditor
  value={customCss}
  language="css"
  placeholder={t('settings.display.custom.css.placeholder')}
  onChange={(value) => dispatch(setCustomCss(value))}
  height="60vh"
  options={{
    autocompletion: true,
    lineNumbers: true,
    foldGutter: true,
    keymap: true
  }}
/>
```

### 3.4 相关资源

项目推荐使用 [CherryCSS.com](https://cherrycss.com/) - 专门为 Cherry Studio 设计的 CSS 模板库。

## 4. 样式优先级和选择器

### 4.1 样式加载顺序

1. Tailwind CSS 基础层
2. 原生 CSS 文件（color.css, font.css 等）
3. Ant Design 组件样式
4. Hero UI 组件样式
5. styled-components 动态样式
6. **用户自定义 CSS（最高优先级）**

### 4.2 重要的 CSS 类名和选择器

#### 主题相关
```css
body[theme-mode='dark']   /* 暗色主题 */
body[theme-mode='light']  /* 亮色主题 */
body[os='mac']            /* macOS 系统 */
body[os='windows']        /* Windows 系统 */
body[navbar-position='left']  /* 侧边导航栏 */
body[navbar-position='top']   /* 顶部导航栏 */
```

#### 聊天消息相关
```css
.bubble                        /* 气泡消息容器 */
.message-user                  /* 用户消息 */
.message-assistant             /* AI 助手消息 */
.message-content-container     /* 消息内容容器 */
.message-header                /* 消息头部 */
.MessageFooter                 /* 消息底部 */
```

#### Markdown 渲染
```css
.markdown                /* Markdown 内容 */
.markdown h1, h2, h3     /* 标题 */
.markdown code           /* 行内代码 */
.markdown pre            /* 代码块 */
.markdown table          /* 表格 */
.markdown blockquote     /* 引用块 */
```

#### 容器和布局
```css
#root                    /* 根容器 */
#content-container       /* 主内容容器 */
.drag                    /* 可拖拽区域 */
.nodrag                  /* 不可拖拽区域 */
```

## 5. 组件样式系统

### 5.1 styled-components 使用

项目广泛使用 styled-components 创建样式化组件：

```tsx
const Container = styled.div`
  display: flex;
  flex-direction: column;
  background: var(--color-background);
  color: var(--color-text);
  
  body[theme-mode='dark'] & {
    /* 暗色主题特殊样式 */
  }
`;
```

### 5.2 Ant Design 自定义

通过 AntdProvider 和主题配置自定义 Ant Design 组件：

```typescript
// 使用 CSS 变量动态配置主题
const theme = {
  token: {
    colorPrimary: userTheme.colorPrimary,
    fontFamily: '--font-family',
    // ...
  }
}
```

## 6. 响应式设计

### 6.1 断点系统

虽然主要是桌面应用，但项目仍包含响应式设计：

```css
@media (max-width: 768px) {
  /* 移动端样式 */
}

@media (max-width: 1024px) {
  /* 平板样式 */
}
```

### 6.2 导航栏位置适配

支持左侧边栏和顶部导航栏两种布局：

```css
[navbar-position='left'] {
  /* 左侧边栏布局 */
}

[navbar-position='top'] {
  /* 顶部导航栏布局 */
}
```

## 7. 特殊功能样式

### 7.1 滚动条自定义

```css
::-webkit-scrollbar {
  width: var(--scrollbar-width);    /* 6px */
  height: var(--scrollbar-height);
}

::-webkit-scrollbar-thumb {
  border-radius: var(--scrollbar-thumb-radius);
  background: var(--color-scrollbar-thumb);
}
```

### 7.2 代码高亮

使用 Shiki 进行代码高亮：

```css
.shiki {
  font-family: var(--code-font-family);
  line-height: initial;
}

.shiki-dark {
  --color-scrollbar-thumb: var(--color-scrollbar-thumb-dark);
}
```

### 7.3 用户选择控制

```css
body {
  -webkit-user-select: none;  /* 默认禁止选择 */
}

/* 特定元素允许选择 */
input,
textarea,
[contenteditable='true'],
.markdown,
.selectable {
  -webkit-user-select: text !important;
}
```

## 8. 性能优化

### 8.1 CSS 变量使用

使用 CSS 变量而不是动态计算，提高性能：

```typescript
// 通过 JavaScript 设置 CSS 变量
document.body.style.setProperty('--color-primary', colorValue);
```

### 8.2 样式隔离

在某些场景使用 Shadow DOM 实现样式隔离，避免样式污染。

## 9. 可自定义的关键变量列表

### 9.1 颜色变量
```css
--color-background
--color-background-soft
--color-background-mute
--color-text
--color-text-secondary
--color-primary
--color-primary-soft
--color-border
--color-hover
--color-active
--color-icon
--color-error
--color-link
```

### 9.2 布局变量
```css
--radius                    /* 圆角大小 */
--list-item-border-radius   /* 列表项圆角 */
--scrollbar-width
--scrollbar-height
```

### 9.3 字体变量
```css
--font-family
--code-font-family
--user-font-family
--user-code-font-family
```

### 9.4 聊天相关
```css
--chat-background
--chat-background-user
--chat-background-assistant
--chat-text-user
```

### 9.5 导航栏
```css
--navbar-background
--navbar-background-mac
--color-list-item
--color-list-item-hover
```

## 10. 最佳实践建议

### 10.1 使用 CSS 变量

优先使用已定义的 CSS 变量，确保与主题系统兼容：

```css
/* ✅ 推荐 */
.my-element {
  background: var(--color-background-soft);
  color: var(--color-text);
}

/* ❌ 不推荐 */
.my-element {
  background: #222222;
  color: white;
}
```

### 10.2 考虑主题模式

为亮色和暗色模式都提供适当的样式：

```css
.my-element {
  background: var(--color-background);
}

[theme-mode='dark'] .my-element {
  border: 1px solid rgba(255, 255, 255, 0.1);
}

[theme-mode='light'] .my-element {
  border: 1px solid rgba(0, 0, 0, 0.1);
}
```

### 10.3 使用特定选择器

使用具体的类名和选择器，避免过度影响其他元素：

```css
/* ✅ 精确定位 */
.message-content-container .markdown code {
  /* 只影响消息中的代码 */
}

/* ❌ 过于宽泛 */
code {
  /* 会影响所有代码元素 */
}
```

### 10.4 保持向后兼容

自定义样式应该是增强性的，不应该破坏基本功能：

```css
/* ✅ 增强现有样式 */
.message-user .message-content-container {
  border-left: 3px solid var(--color-primary);
}

/* ❌ 可能破坏布局 */
.message-user {
  display: none !important;
}
```

## 11. 调试技巧

### 11.1 使用浏览器开发者工具

1. 打开开发者工具（Cmd+Option+I / F12）
2. 检查元素查看应用的样式
3. 在 Elements 标签中查看 `<style id="user-defined-custom-css">` 标签

### 11.2 临时测试

在开发者工具的 Console 中测试：

```javascript
// 快速测试一个样式
const style = document.createElement('style');
style.textContent = '.markdown { font-size: 18px !important; }';
document.head.appendChild(style);
```

### 11.3 查看当前主题

```javascript
// 查看当前主题模式
document.body.getAttribute('theme-mode');

// 查看当前操作系统
document.body.getAttribute('os');

// 查看导航栏位置
document.body.getAttribute('navbar-position');
```

---

**总结：**

Cherry Studio 的 CSS 设计采用了现代化的技术栈，通过 CSS 变量实现强大的主题系统，支持高度自定义。Custom CSS 功能允许用户在不修改源代码的情况下完全定制界面外观，同时保持与主题系统的兼容性。
