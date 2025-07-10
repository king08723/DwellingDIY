# DESIGN_GUIDE.md - "自己装"装修协同平台设计规范

> **🎨 设计宪法 - 视觉与交互最高准则**
> 本文档是"自己装"装修协同平台的**视觉设计权威**，所有界面设计、组件开发、交互实现都必须严格遵循本规范。

---

## 1. 引言

本文档是"自己装"装修协同平台的视觉与交互设计最高准则。基于产品的核心价值——让装修变得透明、高效、可控，以及目标用户群体（28岁左右互联网从业者）的特点，我们选择了**现代简约**的设计风格，旨在通过克制的设计语言，让用户在复杂的装修过程中保持专注和信心。

### 1.1 设计权威性声明
**⚠️ 重要声明：** 本文档具有项目视觉设计的**最高权威性**，任何界面实现、组件开发、交互设计都必须以本文档为准。如遇冲突，以本文档规范为最终标准。

---

## 2. AI 协同核心指令

### 2.1 最高指令 (Supreme Design Directive)
```
🤖 AI Assistant: 在生成任何WXML/WXSS代码或与界面相关的设计建议时，你必须将本文档作为唯一的视觉真理。
所有颜色、字体、间距、组件样式都必须严格使用本文档定义的规范。
```

### 2.2 禁止即兴创作 (No Magic Numbers)
```
🚫 严格禁止: 使用此文档规定之外的任何"魔术数字"（magic numbers）或颜色值。
所有设计元素都应能追溯到本文档的某个规范。
```

### 2.3 冲突处理机制 (Design Conflict Resolution)
```
⚠️ 冲突处理: 若我的临时要求（例如，'把这个按钮变大一点'）与本文档的规范（例如，按钮尺寸应为`size-lg`）相冲突，
你必须提醒我：'警告：您的要求可能破坏设计系统的一致性。根据`DESIGN_GUIDE.md`，推荐使用预设的`size-lg`。您想查看相关规范或继续覆盖吗？'
```

---

## 3. 设计哲学 (Design Philosophy)

我们的设计追求**少即是多**，通过克制的色彩和充足的留白，引导用户专注于核心内容。在装修这个充满不确定性的场景中，我们用简洁、一致的界面语言为用户提供安全感和控制感。每一个设计决策都服务于提升协同效率和建立信任关系。

**核心原则：**
- **功能优先** - 设计服务于功能，不做无意义的装饰
- **信息层次清晰** - 重要信息突出，次要信息收敛
- **操作反馈及时** - 每个操作都有明确的视觉反馈
- **建立信任感** - 通过专业、稳定的视觉表现建立用户信心

---

## 4. 色彩规范 (Color Palette)

### 主色系 (Primary Colors)
```css
/* 在 app.wxss 中定义 */
:root {
  /* 主色 - 专业蓝，传达可靠和专业 */
  --color-primary: #2563eb;
  --color-primary-light: #3b82f6;
  --color-primary-dark: #1d4ed8;
  --color-primary-bg: #eff6ff;
  
  /* 辅助色 - 成功绿，用于完成状态 */
  --color-success: #059669;
  --color-success-light: #10b981;
  --color-success-bg: #ecfdf5;
  
  /* 警告色 - 温和橙，用于待处理状态 */
  --color-warning: #d97706;
  --color-warning-light: #f59e0b;
  --color-warning-bg: #fffbeb;
  
  /* 错误色 - 克制红，用于错误和驳回 */
  --color-error: #dc2626;
  --color-error-light: #ef4444;
  --color-error-bg: #fef2f2;
}
```

### 中性色系 (Neutral Colors)
```css
:root {
  /* 文字色 */
  --color-text-primary: #111827;    /* 主要文字 */
  --color-text-secondary: #6b7280;  /* 次要文字 */
  --color-text-tertiary: #9ca3af;   /* 辅助文字 */
  --color-text-disabled: #d1d5db;   /* 禁用文字 */
  
  /* 背景色 */
  --color-bg-primary: #ffffff;      /* 主背景 */
  --color-bg-secondary: #f9fafb;    /* 次背景 */
  --color-bg-tertiary: #f3f4f6;     /* 三级背景 */
  
  /* 边框色 */
  --color-border-light: #f3f4f6;    /* 浅边框 */
  --color-border-default: #e5e7eb;  /* 默认边框 */
  --color-border-strong: #d1d5db;   /* 强边框 */
}
```

---

## 5. 字体规范 (Typography)

### 字体选择 (Font Family)
```css
:root {
  --font-family-primary: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
}
```

### 字阶系统 (Type Scale)
```css
:root {
  /* 标题字体 */
  --font-size-h1: 48rpx;    /* 页面主标题 */
  --font-size-h2: 36rpx;    /* 区块标题 */
  --font-size-h3: 32rpx;    /* 卡片标题 */
  --font-size-h4: 28rpx;    /* 小标题 */
  
  /* 正文字体 */
  --font-size-body-lg: 32rpx;   /* 大正文 */
  --font-size-body: 28rpx;      /* 标准正文 */
  --font-size-body-sm: 24rpx;   /* 小正文 */
  
  /* 辅助字体 */
  --font-size-caption: 22rpx;   /* 说明文字 */
  --font-size-label: 20rpx;     /* 标签文字 */
  
  /* 字重 */
  --font-weight-regular: 400;
  --font-weight-medium: 500;
  --font-weight-semibold: 600;
  --font-weight-bold: 700;
  
  /* 行高 */
  --line-height-tight: 1.2;
  --line-height-normal: 1.5;
  --line-height-relaxed: 1.75;
}
```

---

## 6. 间距与布局 (Spacing & Layout)

### 网格系统
采用 **8rpx 网格系统**，所有间距都是8的倍数，确保视觉节奏的一致性。

```css
:root {
  /* 基础间距单位 */
  --space-unit: 8rpx;
  
  /* 间距变量 */
  --space-xs: 8rpx;     /* 1 unit - 极小间距 */
  --space-sm: 16rpx;    /* 2 units - 小间距 */
  --space-md: 24rpx;    /* 3 units - 中等间距 */
  --space-lg: 32rpx;    /* 4 units - 大间距 */
  --space-xl: 48rpx;    /* 6 units - 超大间距 */
  --space-2xl: 64rpx;   /* 8 units - 页面级间距 */
  
  /* 页面布局 */
  --page-padding: var(--space-lg);     /* 页面左右边距 */
  --section-gap: var(--space-xl);      /* 区块间距 */
  --card-padding: var(--space-lg);     /* 卡片内边距 */
}
```

### 布局原则
- **页面内容区距离屏幕边缘的安全边距应为 `--space-lg` (32rpx)**
- **卡片之间的间距使用 `--space-md` (24rpx)**
- **同一组元素内部间距使用 `--space-sm` (16rpx)**

---

## 7. 核心组件样式 (Component Styles)

### 按钮 (Button)
```css
/* 主要按钮 */
.btn-primary {
  background-color: var(--color-primary);
  color: #ffffff;
  border: none;
  border-radius: 12rpx;
  padding: var(--space-sm) var(--space-lg);
  font-size: var(--font-size-body);
  font-weight: var(--font-weight-medium);
  min-height: 88rpx;
}

/* 次要按钮 */
.btn-secondary {
  background-color: transparent;
  color: var(--color-primary);
  border: 2rpx solid var(--color-border-default);
  border-radius: 12rpx;
  padding: var(--space-sm) var(--space-lg);
  font-size: var(--font-size-body);
  font-weight: var(--font-weight-medium);
  min-height: 88rpx;
}

/* 按钮尺寸 */
.btn-sm { min-height: 64rpx; padding: var(--space-xs) var(--space-md); }
.btn-lg { min-height: 96rpx; padding: var(--space-md) var(--space-xl); }
```

### 卡片 (Card)
```css
.card {
  background-color: var(--color-bg-primary);
  border-radius: 16rpx;
  padding: var(--card-padding);
  box-shadow: 0 2rpx 8rpx rgba(0, 0, 0, 0.04);
  border: 1rpx solid var(--color-border-light);
}

.card-header {
  margin-bottom: var(--space-md);
  padding-bottom: var(--space-md);
  border-bottom: 1rpx solid var(--color-border-light);
}

.card-title {
  font-size: var(--font-size-h3);
  font-weight: var(--font-weight-semibold);
  color: var(--color-text-primary);
}
```

### 任务卡片 (Task Card)
```css
.task-card {
  background-color: var(--color-bg-primary);
  border-radius: 12rpx;
  padding: var(--space-md);
  border-left: 6rpx solid var(--color-border-default);
  margin-bottom: var(--space-md);
}

.task-card.status-todo { border-left-color: var(--color-border-strong); }
.task-card.status-progress { border-left-color: var(--color-warning); }
.task-card.status-review { border-left-color: var(--color-primary); }
.task-card.status-done { border-left-color: var(--color-success); }
```

### 状态标签 (Status Tag)
```css
.tag {
  display: inline-flex;
  align-items: center;
  padding: 4rpx var(--space-sm);
  border-radius: 20rpx;
  font-size: var(--font-size-label);
  font-weight: var(--font-weight-medium);
}

.tag-todo { background-color: var(--color-bg-tertiary); color: var(--color-text-secondary); }
.tag-progress { background-color: var(--color-warning-bg); color: var(--color-warning); }
.tag-review { background-color: var(--color-primary-bg); color: var(--color-primary); }
.tag-done { background-color: var(--color-success-bg); color: var(--color-success); }
```

### 输入框 (Input)
```css
.input {
  width: 100%;
  padding: var(--space-md);
  border: 2rpx solid var(--color-border-default);
  border-radius: 12rpx;
  font-size: var(--font-size-body);
  background-color: var(--color-bg-primary);
  min-height: 88rpx;
}

.input:focus {
  border-color: var(--color-primary);
  outline: none;
}

.input-error {
  border-color: var(--color-error);
}
```

---

## 8. 状态页面 (State Pages)

### 空状态 (Empty State)
- **插图风格：** 简洁的线条插图，使用主色调
- **文案风格：** 友好但专业，提供明确的下一步操作指引
- **示例：** "还没有任务哦，点击右上角'+'创建第一个任务吧"

### 加载状态 (Loading State)
- **加载动画：** 简洁的圆形进度条，使用主色调
- **文案：** "正在加载中..." 或具体的操作提示

### 错误状态 (Error State)
- **插图：** 温和的错误提示图标，避免过于严厉的视觉表现
- **文案风格：** 解释问题并提供解决方案
- **示例：** "网络连接异常，请检查网络后重试"

---

## 9. 特殊场景设计规范

### 照片展示
- **缩略图尺寸：** 120rpx × 120rpx，圆角 8rpx
- **大图查看：** 全屏展示，支持缩放和滑动
- **时间戳：** 右下角显示，半透明黑色背景

### 验收流程
- **步骤指示器：** 使用主色调的圆点连线
- **状态图标：** 待处理（空心圆）、进行中（半填充圆）、完成（实心圆+对勾）

### 群聊界面
- **消息气泡：** 自己的消息使用主色调，他人消息使用浅灰色
- **头像：** 48rpx × 48rpx 圆形
- **时间显示：** 使用辅助文字色，居中显示

---

## 10. 响应式设计

### 屏幕适配
- **设计基准：** iPhone 6/7/8 (375px × 667px)
- **最小支持：** 320px 宽度
- **最大优化：** 414px 宽度

### 关键断点
```css
/* 小屏幕优化 */
@media (max-width: 320px) {
  :root {
    --page-padding: var(--space-md);
    --font-size-h1: 40rpx;
  }
}
```

---

## 11. 动效规范

### 过渡动画
```css
:root {
  --transition-fast: 0.15s ease-out;
  --transition-normal: 0.25s ease-out;
  --transition-slow: 0.35s ease-out;
}

/* 通用过渡 */
.transition {
  transition: all var(--transition-normal);
}
```

### 常用动效
- **按钮点击：** 轻微缩放 (scale: 0.98)
- **页面切换：** 右滑进入，左滑退出
- **状态变更：** 颜色渐变过渡

---

## 12. 可访问性 (Accessibility)

### 颜色对比度
- **正文文字：** 对比度不低于 4.5:1
- **大字体：** 对比度不低于 3:1
- **交互元素：** 对比度不低于 3:1

### 触摸目标
- **最小点击区域：** 88rpx × 88rpx
- **推荐点击区域：** 96rpx × 96rpx

---

*本设计指南将随着产品迭代持续更新，确保设计系统的一致性和可扩展性。*
