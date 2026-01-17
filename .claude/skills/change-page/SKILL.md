---
name: change-page
description: "Vue 2 page layout modification specialist. Auto-triggers when user wants to: change layout, update design, redesign page, modify page UI, adjust page structure, refactor page appearance. Preserves functionality while updating visual design. Works with Vue 2.6.11, Vant 2.13.2, Tailwind CSS."
---

# 更改页面布局 (Vue 2 + Vant + Tailwind)

本 skill 专门用于根据设计图修改现有页面的布局和样式，同时保留原有的功能逻辑。

## 自动触发条件

当用户请求以下任务时，此 skill 会自动激活：
- 更改/修改/调整页面布局
- 重新设计/优化页面UI
- 根据设计图更新页面
- 修改页面样式/外观
- 重构页面布局结构

## 核心原则 ⚠️

**只改布局，不改功能**
- ✅ 修改：HTML 结构、CSS 样式、Tailwind 类、Vant 组件选择
- ❌ 保留：JavaScript 逻辑、事件处理、数据交互、methods、computed、watch

## 开始前必读

在修改页面之前，**务必先询问用户**以下问题：

### 1. 确认目标页面
- 📄 **页面路径**：需要修改哪个页面？
  - 示例：`src/pages/profile/index.vue`
  - 示例：`src/pages/home/index.vue`

### 2. 设计图信息
- 🎨 **是否有设计图**？
  - 有设计图：提供设计图路径或描述
  - 无设计图：描述期望的布局变化

### 3. 修改范围
- 🔧 **修改内容**：
  - 整个页面重新布局
  - 局部区域调整（如头部、列表区域）
  - 样式优化（颜色、间距、字体）

### 4. 特殊要求
- 📋 **其他要求**：
  - 是否需要保留某些特定样式？
  - 是否有动画效果要求？
  - 是否需要响应式调整？

## 实现要求

### 1. 设计还原
- ✅ 如有设计图，按照 1:1 严格还原（尺寸、间距、颜色、字体、样式）
- ✅ **不要去读取图片文件**，先命名图片路径
- ✅ 告知用户需要准备的新图片资源列表
- ✅ 参考项目配色方案（主色 #FF8FA9）

### 2. 功能保留（重要！）
- ✅ **完整保留** `<script>` 部分的所有代码
  - data() 中的数据定义
  - methods 中的方法
  - computed 计算属性
  - watch 监听器
  - 生命周期钩子

- ✅ **保留所有事件绑定**
  - `@click`、`@change`、`@input` 等事件
  - 确保按钮、表单元素的事件处理不变

- ✅ **保留数据绑定**
  - `v-model`、`:value`、`:src` 等绑定
  - 确保数据流向不变

- ✅ **保留条件渲染和循环**
  - `v-if`、`v-show`、`v-for` 等指令
  - 根据设计图调整位置，但保留逻辑

### 3. 布局修改
- ✅ **可以修改的内容**：
  - HTML 元素的顺序和嵌套结构
  - CSS 类名（Tailwind 类）
  - Vant 组件的选择和配置
  - 样式布局（flex、grid、间距、颜色）
  - 图片资源路径

- ✅ **修改时注意**：
  - 保持原有的 ref 属性（如 `ref="myRef"`）
  - 保持原有的 key 属性（如 `v-for` 中的 `:key`）
  - 保持原有的 class 绑定（如 `:class="{ active: isActive }"`）

### 4. 技术栈使用
- ✅ **优先使用 Vant 2 组件**：
  - 如设计图中的元素有对应的 Vant 组件，优先使用
  - 示例：列表用 `van-list`，表单用 `van-field`

- ✅ **使用 Tailwind CSS**：
  - 间距、颜色、字体、布局等使用 Tailwind 类
  - 避免内联样式，除非 Tailwind 无法实现

- ✅ **保持项目风格一致**

### 5. 代码质量
- ✅ 添加注释说明主要修改点
- ✅ 确保代码可直接运行，无语法错误
- ✅ **不引入新的 npm 依赖**
- ✅ 保持代码简洁清晰

### 6. 移动端适配
- ✅ 确保在移动设备上显示正常（375px 基准）
- ✅ 使用 Vant 的移动端适配方案
- ✅ 必要时使用 Tailwind 响应式类

## 修改流程（必须按顺序执行）

### Step 1: 询问用户
使用 `AskUserQuestion` 工具询问：
1. 目标页面路径
2. 是否有设计图
3. 修改范围（整页/局部）
4. 特殊要求

### Step 2: 读取现有页面
使用 `Read` 工具读取目标页面文件：
```bash
Read /Users/mac/work/takphone/zyfp/src/pages/[目标页面].vue
```

**重点分析**：
- 📋 理解当前页面结构
- 🔍 找出所有事件处理方法
- 📊 识别数据绑定关系
- 🎯 确认需要保留的逻辑

### Step 3: 规划修改方案
在修改前，明确：
1. 哪些部分需要重新布局
2. 哪些 Vant 组件需要替换或新增
3. 哪些功能代码必须保留
4. 新增的图片资源有哪些

### Step 4: 修改页面
使用 `Edit` 工具修改页面文件：

**修改 `<template>` 部分**：
- 调整 HTML 结构以匹配设计图
- 更新 Tailwind CSS 类
- 替换或新增 Vant 组件
- **保留所有事件绑定和数据绑定**

**修改 `<style>` 部分**（如需要）：
- 添加自定义样式（Tailwind 无法实现的效果）
- 保持 scoped 属性

**保留 `<script>` 部分**：
- **完全不修改**，除非用户明确要求修改功能

### Step 5: 告知用户所需图片
列出所有新增或修改的图片资源：
```
📦 需要准备的图片资源：
✅ 保留的图片：
   - @/assets/img/xxx/old_icon.png

🆕 新增的图片：
   1. @/assets/img/xxx/new_banner.png (尺寸: 750x300)
   2. @/assets/img/xxx/new_icon.png (尺寸: 48x48)
```

### Step 6: 修改说明
告知用户修改的内容：
```
✅ 页面布局修改完成！

📝 主要修改：
1. 重新设计了顶部区域，使用 van-nav-bar 组件
2. 调整了列表项布局，使用 flex 布局替代 grid
3. 更新了颜色方案，使用项目主色

🔒 保留的功能：
1. 所有数据交互逻辑
2. 表单验证和提交
3. 列表加载和分页
4. 所有事件处理

🧪 测试建议：
1. 测试所有按钮点击事件
2. 测试表单提交功能
3. 测试数据加载和显示
4. 检查移动端适配效果
```

## 常见修改场景

### 场景 1: 更改导航栏样式
**设计图要求**：导航栏背景色改为渐变色

**修改前**：
```vue
<van-nav-bar title="个人中心" />
```

**修改后**：
```vue
<van-nav-bar
  title="个人中心"
  class="custom-navbar"
/>

<style scoped>
.custom-navbar {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}
</style>
```

### 场景 2: 调整列表布局
**设计图要求**：列表项从垂直布局改为卡片式布局

**修改前**：
```vue
<van-cell-group>
  <van-cell v-for="item in list" :key="item.id" :title="item.name" />
</van-cell-group>
```

**修改后**：
```vue
<div class="grid grid-cols-2 gap-4 p-4">
  <van-card
    v-for="item in list"
    :key="item.id"
    :title="item.name"
    :thumb="item.image"
  />
</div>
```

**保留功能**：`list` 数据、`:key` 绑定、`v-for` 循环

### 场景 3: 重构表单布局
**设计图要求**：表单项间距增大，添加图标

**修改前**：
```vue
<van-form @submit="onSubmit">
  <van-field v-model="form.name" label="姓名" />
  <van-field v-model="form.phone" label="手机号" />
  <van-button native-type="submit">提交</van-button>
</van-form>
```

**修改后**：
```vue
<van-form @submit="onSubmit" class="space-y-4 p-4">
  <van-field
    v-model="form.name"
    label="姓名"
    left-icon="contact"
    placeholder="请输入姓名"
  />
  <van-field
    v-model="form.phone"
    label="手机号"
    left-icon="phone"
    placeholder="请输入手机号"
  />
  <van-button
    native-type="submit"
    block
    type="primary"
    class="!bg-gradient-to-r !from-pink-400 !to-pink-600"
  >
    提交
  </van-button>
</van-form>
```

**保留功能**：
- `@submit="onSubmit"` 事件
- `v-model` 数据绑定
- `onSubmit` 方法（在 script 中）

## 注意事项 ⚠️

### 1. 绝对不能做的事
- ❌ **删除事件处理方法**（如 `@click="handleClick"` 中的 `handleClick` 方法）
- ❌ **修改数据结构**（除非用户明确要求）
- ❌ **删除 API 请求**（保留所有 data fetching 逻辑）
- ❌ **修改路由跳转逻辑**

### 2. 修改时的检查清单
在完成修改后，确认：
- ✅ 所有按钮的 `@click` 事件都保留了吗？
- ✅ 所有表单的 `v-model` 绑定都保留了吗？
- ✅ 所有 `methods` 中的方法都还在使用吗？
- ✅ 所有 `v-for` 的 `:key` 都保留了吗？
- ✅ 所有 `ref` 引用都保留了吗？

### 3. 常见陷阱
- ⚠️ 更换 Vant 组件时，确保新组件支持相同的事件和属性
- ⚠️ 调整布局时，注意 `v-if` 条件不要被破坏
- ⚠️ 修改样式时，避免影响功能性的 CSS（如 `display: none` 等）

### 4. 图片资源管理
- 📁 图片路径使用 `@/assets/img/` 别名
- 📁 按模块组织图片（如 `@/assets/img/profile/`）
- 📁 图片命名清晰（如 `icon_settings.png`、`banner_promo.png`）

## 验证测试

修改完成后，建议用户进行以下测试：

### 功能测试
- [ ] 所有按钮点击是否正常
- [ ] 表单提交是否正常
- [ ] 数据加载是否正常
- [ ] 路由跳转是否正常

### 视觉测试
- [ ] 布局是否符合设计图
- [ ] 间距、颜色是否准确
- [ ] 移动端适配是否正常
- [ ] 动画效果是否流畅

### 兼容性测试
- [ ] 不同屏幕尺寸下是否正常
- [ ] 是否有样式冲突
- [ ] 图片是否正确显示

## 示例：完整修改流程

### 用户请求
> "根据新设计图修改个人中心页面，顶部改成卡片式布局"

### Step 1: 询问确认
```
我会帮您修改个人中心页面的布局。请确认：
1. 目标页面是 src/pages/profile/index.vue 吗？
2. 您有设计图可以分享吗？
3. 只需要修改顶部区域，还是整个页面？
4. 是否需要保留原有的所有功能（如退出登录、跳转等）？
```

### Step 2: 读取页面
```javascript
// 读取并分析现有代码
Read src/pages/profile/index.vue
// 识别关键功能：handleLogout、goToSettings、fetchUserInfo 等
```

### Step 3: 修改布局
```vue
<!-- 修改前 -->
<div class="profile-header">
  <img :src="userInfo.avatar" />
  <p>{{ userInfo.name }}</p>
</div>

<!-- 修改后 -->
<van-card
  class="profile-header-card m-4 rounded-lg shadow-lg"
  :thumb="userInfo.avatar"
  :title="userInfo.name"
  :desc="userInfo.phone"
>
  <template #footer>
    <van-button size="small" @click="goToSettings">编辑资料</van-button>
  </template>
</van-card>
```

### Step 4: 告知用户
```
✅ 修改完成！

📝 主要改动：
1. 顶部用户信息改为 van-card 卡片式布局
2. 添加了圆角和阴影效果
3. 将"编辑资料"按钮移到卡片底部

🔒 保留功能：
1. goToSettings 方法正常工作
2. userInfo 数据绑定正常
3. 头像显示正常

🧪 请测试：
1. 点击"编辑资料"按钮是否跳转正常
2. 用户信息是否正确显示
```

## 其他要求
$ARGUMENTS
