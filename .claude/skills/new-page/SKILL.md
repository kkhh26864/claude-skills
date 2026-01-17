---
name: new-page
description: "Vue 2 page creation specialist. Auto-triggers when user wants to: create new page, add page, build page, new vue page, create vue component page. Handles: page structure, routing, Vant components, Tailwind styling, mobile optimization. Works with Vue 2.6.11, Vant 2.13.2, Tailwind CSS, Vue Router."
---

# 新建页面 (Vue 2 + Vant + Tailwind)

本项目是一个基于 Vue 2.6.11 的移动端应用，使用 Vant 2.13.2 UI 库和 Tailwind CSS。

## 自动触发条件

当用户请求以下任务时，此 skill 会自动激活：
- 创建/新建/添加一个新页面
- 创建 Vue 页面/组件页面
- 添加路由页面
- 实现某个页面（如"创建一个用户设置页面"）

## 开始前必读

在创建页面之前，**务必先询问用户**以下问题：

### 1. 页面类型
- 🔹 **带底部导航栏的页面**（如：首页、个人中心、团队等主功能页）
  - 需要添加到 Main 组件的 children 路由
  - 用户可以通过底部导航栏切换

- 🔹 **独立页面**（如：登录、详情页、表单页等）
  - 添加为顶级路由
  - 通常需要返回按钮

### 2. 页面文件位置
- 页面是否属于某个功能模块（如 profile、team、award、stock、insurance 等）？
- **如果是**：应放在对应的子目录下
  - 示例：`src/pages/profile/mySettings.vue`
- **如果不是**：直接放在 `src/pages/` 下
  - 示例：`src/pages/MyNewPage.vue`

### 3. 是否需要登录验证
- **需要登录**（默认）：大部分页面需要登录后才能访问
- **公开页面**：登录、注册、密码重置等页面可跳过验证

### 4. 页面功能说明
- 页面的主要功能是什么？
- 是否有设计图或参考页面？

## 实现要求

### 1. 设计还原
- ✅ 如有设计图，按照 1:1 严格还原（尺寸、间距、颜色、字体、样式）
- ✅ **不要去读取图片文件**，先命名图片路径（如 `@/assets/img/模块名/图片名.png`）
- ✅ 告知用户需要准备的图片资源列表
- ✅ 参考项目配色方案（定义在 `tailwind.config.js` 中，主色 #FF8FA9）

### 2. 技术栈使用
- ✅ **优先使用 Vant 2 组件**：
  - 导航：`van-nav-bar`, `van-tabbar`, `van-tab`, `van-sidebar`
  - 表单：`van-field`, `van-button`, `van-checkbox`, `van-radio`, `van-switch`
  - 展示：`van-cell`, `van-card`, `van-list`, `van-grid`, `van-image`
  - 反馈：`van-popup`, `van-dialog`, `van-toast`, `van-loading`

- ✅ **使用 Tailwind CSS** 进行样式调整和布局：
  - 间距：`p-4`, `m-2`, `space-y-4`
  - 布局：`flex`, `grid`, `relative`, `absolute`
  - 颜色：使用项目自定义颜色类

- ✅ 保持与项目现有页面风格一致

### 3. 文件创建
- ✅ 创建 Vue 2 单文件组件（.vue）
- ✅ 文件命名规范：
  - 使用 PascalCase（推荐）：`MyProfile.vue`, `UserSettings.vue`
  - 或使用 camelCase：`myProfile.vue`, `userSettings.vue`

- ✅ 放置位置：
  - 功能模块页面：`src/pages/[模块名]/[页面名].vue`
  - 独立页面：`src/pages/[页面名].vue`

### 4. 路由配置

#### 必须在文件顶部添加 import
```javascript
import YourPageName from '../pages/[模块名]/yourPage.vue';
// 或
import YourPageName from '../pages/yourPage.vue';
```

#### 选项 A - 带底部导航栏的页面（Main children）
在 `src/router/index.js` 的 Main 组件 children 数组中添加：

```javascript
{
    path: '/yourpage',
    name: 'yourPage',
    component: YourPage,
    meta: {title: "页面标题"},
}
```

#### 选项 B - 独立页面（顶级路由）
在 `src/router/index.js` 的 routes 数组中添加：

```javascript
{
    path: '/yourpage',
    component: YourPage,
    name: 'yourPage',
    meta: {title: "页面标题"},
}
```

### 5. 页面结构规范

#### 标准模板（独立页面）
```vue
<template>
  <div class="page-container">
    <!-- 顶部导航栏（独立页面需要） -->
    <van-nav-bar
      title="页面标题"
      left-arrow
      @click-left="$router.back()"
    />

    <!-- 页面内容区域 -->
    <div class="content-wrapper p-4">
      <!-- 你的页面内容 -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'YourPageName',
  data() {
    return {
      // 数据定义
    }
  },
  methods: {
    // 方法定义
  },
  mounted() {
    // 页面加载后执行
    this.initPage();
  }
}
</script>

<style scoped>
/* 使用 Tailwind CSS 类，必要时添加自定义样式 */
.page-container {
  min-height: 100vh;
  background-color: #f5f5f5;
}
</style>
```

#### 带底部导航栏的页面（无需 van-nav-bar）
```vue
<template>
  <div class="page-container">
    <!-- 页面内容区域 -->
    <div class="content-wrapper p-4">
      <!-- 你的页面内容 -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'YourPageName',
  data() {
    return {
      // 数据定义
    }
  },
  methods: {
    // 方法定义
  }
}
</script>

<style scoped>
/* 样式定义 */
</style>
```

### 6. 代码质量
- ✅ 添加适当的注释，说明关键部分的功能
- ✅ 确保代码可直接运行，无语法错误
- ✅ **不引入新的 npm 依赖**
- ✅ 保持代码简洁，避免过度设计
- ✅ 遵循 Vue 2 组件化开发规范

### 7. 移动端适配
- ✅ 本项目为移动优先设计（viewport meta 已禁用缩放）
- ✅ 确保在移动设备上显示正常（宽度 375px 基准）
- ✅ 使用 Vant 的移动端适配方案
- ✅ 避免使用固定像素，优先使用相对单位或 Tailwind 类

### 8. 状态管理与工具
- ✅ 如需用户信息，使用 `UserStorage` 工具：
  ```javascript
  import UserStorage from '@/utils/user_storage';

  // 获取用户信息
  const userInfo = UserStorage.getUserInfo();
  const token = UserStorage.getToken();
  ```

- ✅ 如需 Vuex，参考现有 store 模块（`src/store/`）

- ✅ API 请求示例：
  ```javascript
  import request from '@/utils/request';

  export default {
    methods: {
      async fetchData() {
        try {
          const res = await request.get('/api/your-endpoint');
          console.log(res.data);
        } catch (error) {
          this.$toast.fail('请求失败');
        }
      }
    }
  }
  ```

## 创建流程（必须按顺序执行）

### Step 1: 询问用户
使用 `AskUserQuestion` 工具询问：
1. 页面类型（带底部导航栏 / 独立页面）
2. 页面文件位置（功能模块 / 独立）
3. 是否需要登录验证
4. 页面功能说明

### Step 2: 查看参考页面（可选）
如果用户提到类似的现有页面，先读取参考：
```bash
Read /Users/mac/work/takphone/zyfp/src/pages/[参考页面].vue
```

### Step 3: 创建 Vue 组件文件
使用 `Write` 工具创建页面文件

### Step 4: 配置路由
使用 `Edit` 工具修改 `src/router/index.js`：
1. 在顶部添加 import 语句
2. 在正确位置（Main children 或顶级 routes）添加路由配置

### Step 5: 告知用户所需图片
列出所有需要准备的图片资源：
```
📦 需要准备的图片资源：
1. @/assets/img/模块名/icon_xxx.png (尺寸: 48x48)
2. @/assets/img/模块名/banner_xxx.png (尺寸: 750x300)
...
```

### Step 6: 测试说明
告知用户如何访问新页面：
```
✅ 页面创建完成！

访问路径：/yourpage
页面标题：页面标题

测试方法：
1. 运行 yarn dev
2. 在浏览器访问 http://localhost:50828/yourpage
3. 或在代码中使用 this.$router.push('/yourpage') 跳转
```

## 常见页面类型示例

### 列表页面（带上拉加载）
```vue
<van-list
  v-model="loading"
  :finished="finished"
  finished-text="没有更多了"
  @load="onLoad"
>
  <van-cell v-for="item in list" :key="item.id" :title="item.title" />
</van-list>
```

### 表单页面
```vue
<van-form @submit="onSubmit">
  <van-field v-model="form.name" label="姓名" placeholder="请输入姓名" />
  <van-field v-model="form.phone" label="手机号" placeholder="请输入手机号" />
  <div class="p-4">
    <van-button block type="info" native-type="submit">提交</van-button>
  </div>
</van-form>
```

### 详情页面
```vue
<div class="detail-page">
  <van-image :src="detail.image" width="100%" height="200px" />
  <div class="p-4">
    <h2 class="text-xl font-bold mb-2">{{ detail.title }}</h2>
    <p class="text-gray-600">{{ detail.content }}</p>
  </div>
</div>
```

## 注意事项

1. **路由路径命名**：使用小写字母和连字符（如 `/user-settings`）
2. **组件命名**：使用 PascalCase（如 `UserSettings`）
3. **避免路由冲突**：检查 `router/index.js` 确保路径唯一
4. **图片路径**：使用 `@/assets/img/` 别名，不要使用相对路径
5. **Vant 组件导入**：全局已注册，无需手动导入
6. **Toast 提示**：使用 `this.$toast.success()` 或 `this.$toast.fail()`

## 项目路径参考

```
src/
├── pages/
│   ├── home/              # 首页模块
│   ├── profile/           # 个人中心模块
│   ├── team/              # 团队模块
│   ├── stock/             # 股权模块
│   ├── insurance/         # 保险模块
│   ├── award/             # 抽奖模块
│   ├── exchange/          # 兑换模块
│   ├── realestate/        # 地产模块
│   ├── supportCard/       # 扶贫卡模块
│   └── ...
├── router/
│   └── index.js           # 路由配置文件
├── assets/
│   └── img/               # 图片资源
└── utils/
    └── user_storage.js    # 用户工具
```

## 其他要求
$ARGUMENTS
