# Claude Skills Collection

[English](#english) | [中文](#chinese)

---

<a name="english"></a>
## English

### Overview

A collection of Claude Code skills for improving development productivity. These skills cover UI/UX design, Vue.js development, and mobile app resource management.

### Skills

#### 1. UI/UX Pro Max

**Purpose**: Comprehensive UI/UX design intelligence with searchable databases for styles, colors, fonts, and framework-specific best practices.

**Features**:
- 50 UI styles (glassmorphism, minimalism, brutalism, etc.)
- 21 color palettes by industry
- 50 font pairings with Google Fonts
- 20 chart type recommendations
- 8 technology stacks (React, Next.js, Vue, Svelte, SwiftUI, React Native, Flutter, Tailwind)

**Usage**:
Automatically triggers when you request UI/UX work:
```
"Design a landing page for a healthcare SaaS"
"Create a dashboard with dark mode"
"Build an e-commerce product card"
```

**Triggers**: plan, build, create, design, implement, review, fix, improve, optimize UI/UX code; work with .html, .tsx, .vue, .svelte files; mention styles like glassmorphism, dark mode, responsive design

**Requirements**: Python 3 (for searching design databases)

---

#### 2. New Page (Vue 2)

**Purpose**: Create new Vue 2 pages with Vant UI components and Tailwind CSS styling for mobile applications.

**Features**:
- Automatic page structure generation
- Router configuration
- Vant 2.13.2 component integration
- Mobile-first responsive design
- Image asset planning

**Usage**:
```
"Create a new user settings page"
"Add a profile page with bottom navigation"
"Build a login page"
```

**Triggers**: create/add/build new page, new vue page, create vue component page

**Tech Stack**: Vue 2.6.11, Vant 2.13.2, Tailwind CSS, Vue Router

---

#### 3. Change Page (Vue 2)

**Purpose**: Modify existing Vue 2 page layouts while preserving all functionality and business logic.

**Features**:
- Layout restructuring
- Style updates with Tailwind CSS
- Vant component replacement
- Function preservation (events, data binding, methods)
- Design mockup implementation

**Usage**:
```
"Update the home page layout based on the new design"
"Redesign the profile page header"
"Change the list layout to card style"
```

**Triggers**: change/modify/update layout, redesign page, modify page UI, adjust page structure

**Tech Stack**: Vue 2.6.11, Vant 2.13.2, Tailwind CSS

---

#### 4. Generate Round Icons

**Purpose**: Generate round Android launcher icons (ic_launcher_round.png) from existing launcher icons for all mipmap densities.

**Features**:
- Perfect circular mask generation
- Supports all Android densities (ldpi, mdpi, hdpi, xhdpi, xxhdpi, xxxhdpi)
- Batch processing
- Automatic size detection

**Usage**:
```
"Generate round icons for Android"
"Create circular launcher icons"
```

**Triggers**: generate round icons, create round icons, 生成圆形图标

**Requirements**: ImageMagick

---

#### 5. Copy Launch Screen

**Purpose**: Copy Android launch screen images to iOS with proper density mapping.

**Features**:
- Automatic density mapping (mdpi→1x, xhdpi→2x, xxhdpi→3x)
- Batch copying
- Cross-platform resource synchronization

**Usage**:
```
"Copy launch screen from Android to iOS"
"Sync launch images between platforms"
```

**Triggers**: copy launch screen, sync launch images, update iOS launch screen

**Requirements**: Android and iOS project structure

---

### Installation

1. Clone this repository to your local machine
2. Place it in a location accessible to Claude Code
3. Configure Claude Code to recognize the skills

### Contributing

Contributions are welcome! Feel free to submit issues or pull requests.

---

<a name="chinese"></a>
## 中文

### 项目简介

Claude Code skills集合，用于提高开发效率。这些技能涵盖 UI/UX 设计、Vue.js 开发和移动应用资源管理。

### 技能列表

#### 1. UI/UX Pro Max - UI/UX 设计智能助手

**功能**: 全面的 UI/UX 设计智能助手，包含样式、颜色、字体和框架特定最佳实践的可搜索数据库。

**特性**:
- 50 种 UI 风格（玻璃拟态、极简主义、粗野主义等）
- 21 种行业配色方案
- 50 种字体配对（含 Google Fonts）
- 20 种图表类型推荐
- 8 种技术栈支持（React、Next.js、Vue、Svelte、SwiftUI、React Native、Flutter、Tailwind）

**使用方式**:
当你请求 UI/UX 相关工作时自动触发：
```
"为医疗 SaaS 设计一个落地页"
"创建一个带暗黑模式的仪表板"
"构建一个电商产品卡片"
```

**触发关键词**: plan、build、create、design、implement、review、fix、improve、optimize UI/UX 代码；处理 .html、.tsx、.vue、.svelte 文件；提及 glassmorphism、dark mode、responsive design 等样式

**依赖**: Python 3（用于搜索设计数据库）

---

#### 2. New Page - Vue 2 新建页面

**功能**: 为移动应用创建新的 Vue 2 页面，集成 Vant UI 组件和 Tailwind CSS 样式。

**特性**:
- 自动生成页面结构
- 路由配置
- Vant 2.13.2 组件集成
- 移动优先响应式设计
- 图片资源规划

**使用方式**:
```
"创建一个用户设置页面"
"添加一个带底部导航的个人中心页"
"构建一个登录页面"
```

**触发关键词**: 创建/新建/添加新页面、新 vue 页面、创建 vue 组件页面

**技术栈**: Vue 2.6.11、Vant 2.13.2、Tailwind CSS、Vue Router

---

#### 3. Change Page - Vue 2 修改页面

**功能**: 修改现有 Vue 2 页面的布局，同时保留所有功能和业务逻辑。

**特性**:
- 布局重构
- Tailwind CSS 样式更新
- Vant 组件替换
- 功能保留（事件、数据绑定、方法）
- 设计稿实现

**使用方式**:
```
"根据新设计稿更新首页布局"
"重新设计个人中心页面的头部"
"将列表布局改为卡片样式"
```

**触发关键词**: 更改/修改/调整布局、重新设计页面、修改页面UI、调整页面结构

**技术栈**: Vue 2.6.11、Vant 2.13.2、Tailwind CSS

---

#### 4. Generate Round Icons - 生成圆形图标

**功能**: 为所有 Android mipmap 密度从现有启动图标生成圆形启动图标（ic_launcher_round.png）。

**特性**:
- 完美圆形遮罩生成
- 支持所有 Android 密度（ldpi、mdpi、hdpi、xhdpi、xxhdpi、xxxhdpi）
- 批量处理
- 自动尺寸检测

**使用方式**:
```
"为 Android 生成圆形图标"
"创建圆形启动图标"
```

**触发关键词**: generate round icons、create round icons、生成圆形图标、圆形图标

**依赖**: ImageMagick

---

#### 5. Copy Launch Screen - 复制启动屏幕

**功能**: 将 Android 启动屏幕图片复制到 iOS，并进行正确的密度映射。

**特性**:
- 自动密度映射（mdpi→1x、xhdpi→2x、xxhdpi→3x）
- 批量复制
- 跨平台资源同步

**使用方式**:
```
"将启动屏幕从 Android 复制到 iOS"
"同步两个平台的启动图片"
```

**触发关键词**: copy launch screen、sync launch images、update iOS launch screen、复制启动屏幕、同步启动图片

**依赖**: Android 和 iOS 项目结构

---

### 安装使用

1. 克隆本仓库到本地
2. 将其放置在 Claude Code 可访问的位置
3. 配置 Claude Code 以识别这些技能

### 贡献

欢迎贡献！请随时提交问题或拉取请求。

---

## License

MIT

## Author

Collected and created by the community
