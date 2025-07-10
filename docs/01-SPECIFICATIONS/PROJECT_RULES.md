# PROJECT_RULES.md - "自己装"装修协同平台开发规范

> **🏗️ 项目宪法 - 最高开发准则**  
> 本文档是"自己装"装修协同平台的**最高技术权威**，所有代码开发、架构设计、功能实现都必须严格遵循本规范。

---

## 📋 目录

1. [项目概述](#1-项目概述)
2. [AI协作核心指令](#2-ai协作核心指令)
3. [文档驱动开发标准](#3-文档驱动开发标准)
4. [核心架构原则：关注点分离](#4-核心架构原则关注点分离)
5. [全局状态管理](#5-全局状态管理)
6. [目录结构规范](#6-目录结构规范)
7. [命名约定](#7-命名约定)
8. [API接口规范](#8-api接口规范)
9. [代码风格规范](#9-代码风格规范)
10. [微信小程序最佳实践](#10-微信小程序最佳实践)

---

## 1. 项目概述

### 1.1 项目定位
**产品名称：** "自己装"装修协同平台  
**技术栈：** 微信小程序原生开发 + 微信云开发 + MobX状态管理  
**核心目标：** 构建以业主为中心的装修数字化协同与服务平台

### 1.2 项目特点
- **用户角色：** 项目经理、业主、工人三方协同
- **核心功能：** 项目管理、任务协同、进度跟踪、验收流程
- **技术特色：** 云原生架构、实时协同、移动优先

### 1.3 文档权威性声明
**⚠️ 重要声明：** 本文档具有项目开发的**最高权威性**，任何代码实现、架构决策、功能开发都必须以本文档为准。如遇冲突，以本文档规范为最终标准。

---

## 2. AI协作核心指令

### 2.1 最高指令 (Supreme Directive)
```
🤖 AI Assistant: 在处理本项目的任何任务时，你必须将本文档视为最高上下文和终极行为准则。
在生成任何代码或文件之前，必须内部验证你的解决方案完全符合本文档的规范要求。
```

### 2.2 架构优先级 (Architecture Priority)
```
🏗️ 架构核心: 特别注意严格理解和执行 [第4节：核心架构原则] 和 [第5节：全局状态管理] 中的规则。
这些是本项目的核心差异化逻辑，是你在生成代码时必须遵循的关键原则。
```

### 2.3 冲突解决机制 (Conflict Resolution)
```
⚠️ 冲突处理: 如果我的临时请求与本文档冲突，你必须优先考虑本文档并警告我冲突。
示例："警告：您要求在Page文件中直接编写业务逻辑，这违反了PROJECT_RULES.md第4.1节关于页面文件职责的规定。
建议将逻辑移至 `miniprogram/utils/pages/` 模块。是否继续？"
```

### 2.4 代码生成标准
- **架构检查：** 每次生成代码前，检查是否符合SoC原则
- **文件职责：** 确保每个文件只承担其规定的单一职责
- **依赖关系：** 严格按照规定的模块依赖关系组织代码
- **命名规范：** 严格遵循第7节的命名约定

---

## 3. 文档驱动开发标准

### 3.1 核心理念
**文档驱动开发 (Document-Driven Development, DDD)**
> 文档先行，代码后行。文档是结晶化的思考、沟通的契约、实现的标准。

### 3.2 文档目录结构
```
docs/
├── 00-CONCEPT/                    # 0. 概念与战略 (顶层，最稳定)
│   ├── product_brief.md           # 产品战略分析
│   └── architecture_overview.md   # 整体技术架构图
│
├── 01-SPECIFICATIONS/             # 1. 核心规范 (双重宪法)
│   ├── PROJECT_RULES.md           # 项目编码与架构标准 (本文档)
│   └── DESIGN_GUIDE.md            # UI/UX设计标准
│
├── 02-BLUEPRINTS/                 # 2. 功能蓝图 (持续增长)
│   ├── mvp_scope.md               # MVP范围定义 (含Mermaid流程图)
│   ├── TODO.md                    # 高层功能待办 (Epic/User Story格式)
│   └── features/                  # 详细设计文档按功能模块
│       ├── 01-user-auth.md        # 用户认证功能蓝图
│       ├── 02-project-mgmt.md     # 项目管理功能蓝图
│       ├── 03-task-collab.md      # 任务协同功能蓝图
│       └── 04-acceptance-flow.md  # 验收流程功能蓝图
│
├── 03-MEETINGS/                   # 3. 会议与决策 (可选，团队用)
│   └── meeting-notes/
│
├── 04-TESTING/                    # 4. 测试用例 (可选，团队用)
│   └── test-cases/
│
└── README.md                      # 文档索引，解释各目录用途
```

### 3.3 文档生命周期管理
- **版本控制：** 所有 `.md` 文件必须纳入Git管理
- **变更审查：** `docs/01-SPECIFICATIONS/` 中的"宪法级"文档修改需要Pull Request审查
- **文档同步：** 功能开发/修改后，对应的 `features/*.md` 文档必须同步更新

---

## 4. 核心架构原则：关注点分离 (SoC)

### 4.1 Page文件 (`miniprogram/pages/**/*.js`)：单一职责
**职责定义：** 仅包含 `data` 对象和官方生命周期函数

**严格规则：**
- ✅ **允许：** `data` 对象定义、`onLoad`、`onShow`、`onHide` 等生命周期
- ❌ **禁止：** 事件处理函数、业务逻辑函数、API调用
- ✅ **必须：** 所有事件处理器和业务逻辑必须从对应的 `miniprogram/utils/pages/` 模块导入

**标准模板：**
```javascript
// miniprogram/pages/project-detail/project-detail.js
const projectDetailLogic = require('../../utils/pages/project-detail/project-detail');

Page({
  data: {
    project: null,
    tasks: [],
    loading: false,
    userRole: ''
  },

  onLoad(options) {
    projectDetailLogic.onLoad.call(this, options);
  },

  onShow() {
    projectDetailLogic.onShow.call(this);
  },

  // 事件处理器 - 必须从logic模块导入
  onTaskClick: projectDetailLogic.onTaskClick,
  onCreateTask: projectDetailLogic.onCreateTask,
  onAcceptanceRequest: projectDetailLogic.onAcceptanceRequest
});
```

### 4.2 Page逻辑模块 (`miniprogram/utils/pages/**/*.js`)：业务内聚
**职责定义：** 存储特定页面的所有业务逻辑和事件处理器

**组织原则：**
- 按页面路径组织：`miniprogram/utils/pages/project-detail/project-detail.js`
- 导出对象包含所有页面相关的逻辑函数
- 可以调用API模块、工具函数、Store等

**标准模板：**
```javascript
// miniprogram/utils/pages/project-detail/project-detail.js
const projectApi = require('../../../api/project');
const taskApi = require('../../../api/task');
const { projectStore } = require('../../../stores/project-store');

module.exports = {
  async onLoad(options) {
    const projectId = options.id;
    this.setData({ loading: true });
    
    try {
      const project = await projectApi.getProjectDetail(projectId);
      const tasks = await taskApi.getProjectTasks(projectId);
      
      this.setData({
        project,
        tasks,
        userRole: projectStore.currentUserRole
      });
    } catch (error) {
      wx.showToast({
        title: '加载失败',
        icon: 'error'
      });
    } finally {
      this.setData({ loading: false });
    }
  },

  async onTaskClick(event) {
    const taskId = event.currentTarget.dataset.taskId;
    wx.navigateTo({
      url: `/pages/task-detail/task-detail?id=${taskId}`
    });
  },

  async onCreateTask() {
    // 创建任务逻辑
  },

  async onAcceptanceRequest(event) {
    // 验收申请逻辑
  }
};
```

### 4.3 API模块 (`miniprogram/api/**/*.js`)：数据获取
**职责定义：** 封装后端接口请求，仅负责与服务器通信

**组织原则：**
- 按业务领域组织：`miniprogram/api/project.js`、`miniprogram/api/task.js`、`miniprogram/api/user.js`
- 所有请求通过统一的 `miniprogram/utils/request.js` 发送
- 返回标准化的数据格式

**标准模板：**
```javascript
// miniprogram/api/project.js
const request = require('../utils/request');

module.exports = {
  // 获取项目列表
  async getProjectList(params = {}) {
    return await request.get('/api/projects', params);
  },

  // 获取项目详情
  async getProjectDetail(projectId) {
    return await request.get(`/api/projects/${projectId}`);
  },

  // 创建项目
  async createProject(projectData) {
    return await request.post('/api/projects', projectData);
  },

  // 更新项目
  async updateProject(projectId, updateData) {
    return await request.put(`/api/projects/${projectId}`, updateData);
  },

  // 邀请成员
  async inviteMembers(projectId, memberData) {
    return await request.post(`/api/projects/${projectId}/members`, memberData);
  }
};
```

### 4.4 请求模块 (`miniprogram/utils/request.js`)：统一网关
**职责定义：** 作为项目中所有HTTP请求的唯一出口

**核心功能：**
- 统一请求配置（baseURL、timeout、headers）
- 统一错误处理
- 请求/响应拦截器
- 加载状态管理

**标准实现：**
```javascript
// miniprogram/utils/request.js
// 微信小程序云开发统一请求模块

// 统一错误处理
const handleError = (error, showToast = true) => {
  console.error('Request Error:', error);

  if (showToast) {
    wx.showToast({
      title: error.message || '请求失败',
      icon: 'error'
    });
  }

  return Promise.reject(error);
};

// 统一响应处理
const handleResponse = (response) => {
  const { result } = response;

  if (result.code === 0) {
    return result.data;
  } else {
    throw new Error(result.message || '请求失败');
  }
};

// 从URL中提取资源类型，如 '/api/projects' -> 'project'
const extractResource = (url) => {
  const match = url.match(/\/api\/(\w+)/);
  return match ? match[1].replace(/s$/, '') : 'unknown'; // 去掉复数s
};

const request = {
  // GET请求
  async get(url, params = {}) {
    try {
      const response = await wx.cloud.callFunction({
        name: 'api',  // 对应 cloudfunctions/api/ 云函数
        data: {
          method: 'GET',
          resource: extractResource(url),
          params
        }
      });
      return handleResponse(response);
    } catch (error) {
      return handleError(error);
    }
  },

  // POST请求
  async post(url, data = {}) {
    try {
      const response = await wx.cloud.callFunction({
        name: 'api',
        data: {
          method: 'POST',
          resource: extractResource(url),
          data
        }
      });
      return handleResponse(response);
    } catch (error) {
      return handleError(error);
    }
  },

  // PUT请求
  async put(url, data = {}) {
    try {
      const response = await wx.cloud.callFunction({
        name: 'api',
        data: {
          method: 'PUT',
          resource: extractResource(url),
          data
        }
      });
      return handleResponse(response);
    } catch (error) {
      return handleError(error);
    }
  },

  // DELETE请求
  async delete(url, params = {}) {
    try {
      const response = await wx.cloud.callFunction({
        name: 'api',
        data: {
          method: 'DELETE',
          resource: extractResource(url),
          params
        }
      });
      return handleResponse(response);
    } catch (error) {
      return handleError(error);
    }
  }
};

module.exports = request;
```

### 4.5 完整代码示例：三层协作
以下是一个完整的页面、逻辑、API三层协作示例：

**页面层 (`miniprogram/pages/project-list/project-list.js`)：**
```javascript
const projectListLogic = require('../../utils/pages/project-list/project-list');

Page({
  data: {
    projects: [],
    loading: false,
    userRole: 'owner' // owner, pm, worker
  },

  onLoad() {
    projectListLogic.onLoad.call(this);
  },

  onPullDownRefresh() {
    projectListLogic.onRefresh.call(this);
  },

  // 事件处理器
  onProjectClick: projectListLogic.onProjectClick,
  onCreateProject: projectListLogic.onCreateProject
});
```

**逻辑层 (`miniprogram/utils/pages/project-list/project-list.js`)：**
```javascript
const projectApi = require('../../../api/project');
const { userStore } = require('../../../stores/user-store');

module.exports = {
  async onLoad() {
    await this.loadProjects();
  },

  async onRefresh() {
    await this.loadProjects();
    wx.stopPullDownRefresh();
  },

  async loadProjects() {
    this.setData({ loading: true });

    try {
      const projects = await projectApi.getProjectList({
        role: userStore.currentUser.role
      });

      this.setData({ projects });
    } catch (error) {
      console.error('加载项目列表失败:', error);
    } finally {
      this.setData({ loading: false });
    }
  },

  onProjectClick(event) {
    const projectId = event.currentTarget.dataset.projectId;
    wx.navigateTo({
      url: `/pages/project-detail/project-detail?id=${projectId}`
    });
  },

  onCreateProject() {
    wx.navigateTo({
      url: '/pages/create-project/create-project'
    });
  }
};
```

**API层 (`miniprogram/api/project.js`)：**
```javascript
const request = require('../utils/request');

module.exports = {
  async getProjectList(params) {
    return await request.get('/api/projects', params);
  }
};
```

---

## 5. 全局状态管理

### 5.1 技术选型
**官方状态管理方案：** `mobx-miniprogram` + `mobx-miniprogram-bindings`

**安装依赖：**
```bash
npm install mobx-miniprogram mobx-miniprogram-bindings
```

### 5.2 使用场景
**何时使用全局状态：**
- ✅ 用户信息（登录状态、角色、权限）
- ✅ 项目信息（当前项目、项目列表）
- ✅ 全局设置（主题、语言、通知设置）
- ✅ 跨页面共享的数据（购物车、消息计数）
- ❌ 页面级临时数据（表单输入、加载状态）

### 5.3 Store规范

**目录结构：**
```
miniprogram/stores/
├── index.js           # Store统一导出
├── user-store.js      # 用户状态管理
├── project-store.js   # 项目状态管理
├── task-store.js      # 任务状态管理
└── app-store.js       # 应用全局状态
```

**Store标准模板：**
```javascript
// miniprogram/stores/user-store.js
const { observable, action, computed } = require('mobx-miniprogram');

const userStore = observable({
  // 状态数据
  currentUser: null,
  isLoggedIn: false,
  userRole: '', // 'owner', 'pm', 'worker'
  permissions: [],

  // 计算属性
  get isProjectManager() {
    return this.userRole === 'pm';
  },

  get isOwner() {
    return this.userRole === 'owner';
  },

  get isWorker() {
    return this.userRole === 'worker';
  },

  // Actions - 所有状态修改必须通过action
  setUser: action(function(user) {
    this.currentUser = user;
    this.isLoggedIn = true;
    this.userRole = user.role;
    this.permissions = user.permissions || [];
  }),

  logout: action(function() {
    this.currentUser = null;
    this.isLoggedIn = false;
    this.userRole = '';
    this.permissions = [];
  }),

  updateUserInfo: action(function(userInfo) {
    if (this.currentUser) {
      Object.assign(this.currentUser, userInfo);
    }
  })
});

module.exports = {
  userStore
};
```

**项目Store示例：**
```javascript
// miniprogram/stores/project-store.js
const { observable, action, computed } = require('mobx-miniprogram');

const projectStore = observable({
  // 状态数据
  currentProject: null,
  projectList: [],
  currentProjectTasks: [],

  // 计算属性
  get currentProjectId() {
    return this.currentProject?.id || null;
  },

  get completedTasksCount() {
    return this.currentProjectTasks.filter(task => task.status === 'completed').length;
  },

  get totalTasksCount() {
    return this.currentProjectTasks.length;
  },

  get projectProgress() {
    if (this.totalTasksCount === 0) return 0;
    return Math.round((this.completedTasksCount / this.totalTasksCount) * 100);
  },

  // Actions
  setCurrentProject: action(function(project) {
    this.currentProject = project;
  }),

  setProjectList: action(function(projects) {
    this.projectList = projects;
  }),

  setCurrentProjectTasks: action(function(tasks) {
    this.currentProjectTasks = tasks;
  }),

  updateTask: action(function(taskId, updates) {
    const taskIndex = this.currentProjectTasks.findIndex(task => task.id === taskId);
    if (taskIndex !== -1) {
      Object.assign(this.currentProjectTasks[taskIndex], updates);
    }
  }),

  addTask: action(function(task) {
    this.currentProjectTasks.push(task);
  }),

  removeTask: action(function(taskId) {
    const taskIndex = this.currentProjectTasks.findIndex(task => task.id === taskId);
    if (taskIndex !== -1) {
      this.currentProjectTasks.splice(taskIndex, 1);
    }
  })
});

module.exports = {
  projectStore
};
```

### 5.4 页面中使用Store

**在页面中注入Store：**
```javascript
// miniprogram/pages/project-detail/project-detail.js
const { storeBindingsBehavior } = require('mobx-miniprogram-bindings');
const { projectStore, userStore } = require('../../stores/index');

const projectDetailLogic = require('../../utils/pages/project-detail/project-detail');

Page({
  behaviors: [storeBindingsBehavior],

  storeBindings: {
    store: projectStore,
    fields: {
      currentProject: 'currentProject',
      projectProgress: 'projectProgress',
      tasks: 'currentProjectTasks'
    },
    actions: {
      setCurrentProject: 'setCurrentProject',
      updateTask: 'updateTask'
    }
  },

  data: {
    loading: false
  },

  onLoad(options) {
    projectDetailLogic.onLoad.call(this, options);
  },

  // 事件处理器
  onTaskClick: projectDetailLogic.onTaskClick,
  onTaskStatusChange: projectDetailLogic.onTaskStatusChange
});
```

**在逻辑模块中使用Store：**
```javascript
// miniprogram/utils/pages/project-detail/project-detail.js
const projectApi = require('../../../api/project');
const { projectStore, userStore } = require('../../../stores/index');

module.exports = {
  async onLoad(options) {
    const projectId = options.id;
    this.setData({ loading: true });

    try {
      const project = await projectApi.getProjectDetail(projectId);
      const tasks = await taskApi.getProjectTasks(projectId);

      // 更新Store状态
      projectStore.setCurrentProject(project);
      projectStore.setCurrentProjectTasks(tasks);

    } catch (error) {
      wx.showToast({
        title: '加载失败',
        icon: 'error'
      });
    } finally {
      this.setData({ loading: false });
    }
  },

  async onTaskStatusChange(event) {
    const { taskId, newStatus } = event.detail;

    try {
      await taskApi.updateTaskStatus(taskId, newStatus);

      // 更新Store中的任务状态
      projectStore.updateTask(taskId, { status: newStatus });

      wx.showToast({
        title: '状态更新成功',
        icon: 'success'
      });
    } catch (error) {
      wx.showToast({
        title: '更新失败',
        icon: 'error'
      });
    }
  }
};
```

### 5.5 Store统一导出
```javascript
// miniprogram/stores/index.js
const { userStore } = require('./user-store');
const { projectStore } = require('./project-store');
const { taskStore } = require('./task-store');
const { appStore } = require('./app-store');

module.exports = {
  userStore,
  projectStore,
  taskStore,
  appStore
};
```

---

## 6. 目录结构规范

### 6.1 完整目录结构
```
DwellingDIY/                       # 项目根目录
├── docs/                          # 项目文档中心
│   ├── 00-CONCEPT/
│   ├── 01-SPECIFICATIONS/
│   ├── 02-BLUEPRINTS/
│   ├── 03-MEETINGS/
│   ├── 04-TESTING/
│   └── README.md
│
├── miniprogram/                   # 小程序主体
│   ├── api/                       # API数据接口模块 (核心)
│   │   ├── user.js                # 用户相关API
│   │   ├── project.js             # 项目相关API
│   │   ├── task.js                # 任务相关API
│   │   ├── message.js             # 消息相关API
│   │   └── upload.js              # 文件上传API
│   │
│   ├── components/                # 全局可复用组件
│   │   ├── task-card/             # 任务卡片组件
│   │   ├── project-progress/      # 项目进度组件
│   │   ├── user-avatar/           # 用户头像组件
│   │   ├── photo-uploader/        # 照片上传组件
│   │   └── chat-bubble/           # 聊天气泡组件
│   │
│   ├── pages/                     # 主包页面
│   │   ├── index/                 # 首页
│   │   ├── login/                 # 登录页
│   │   ├── project-list/          # 项目列表
│   │   ├── project-detail/        # 项目详情
│   │   ├── task-detail/           # 任务详情
│   │   ├── create-project/        # 创建项目
│   │   ├── user-profile/          # 用户资料
│   │   └── settings/              # 设置页面
│   │
│   ├── stores/                    # 全局状态管理 (核心)
│   │   ├── index.js               # Store统一导出
│   │   ├── user-store.js          # 用户状态
│   │   ├── project-store.js       # 项目状态
│   │   ├── task-store.js          # 任务状态
│   │   └── app-store.js           # 应用全局状态
│   │
│   ├── static/                    # 静态资源
│   │   ├── images/                # 图片资源
│   │   ├── icons/                 # 图标资源
│   │   └── fonts/                 # 字体资源
│   │
│   ├── subpackages/               # 分包页面
│   │   ├── chat/                  # 聊天功能分包
│   │   ├── finance/               # 财务功能分包
│   │   └── admin/                 # 管理功能分包
│   │
│   ├── utils/                     # 工具库
│   │   ├── pages/                 # 页面逻辑模块 (核心)
│   │   │   ├── project-list/
│   │   │   │   └── project-list.js
│   │   │   ├── project-detail/
│   │   │   │   └── project-detail.js
│   │   │   └── task-detail/
│   │   │       └── task-detail.js
│   │   ├── request.js             # 统一请求模块 (核心)
│   │   ├── tool.js                # 通用工具函数
│   │   ├── constants.js           # 常量定义
│   │   ├── validator.js           # 数据验证工具
│   │   └── date.js                # 日期处理工具
│   │
│   ├── app.js                     # 应用入口
│   ├── app.json                   # 应用配置
│   ├── app.wxss                   # 全局样式
│   └── sitemap.json               # 站点地图
│
├── cloudfunctions/                # 云函数
│   ├── api/                       # 后端API云函数
│   ├── auth/                      # 认证相关云函数
│   └── upload/                    # 文件上传云函数
│
├── project.config.json            # 项目配置
├── project.private.config.json    # 私有配置
├── README.md                      # 项目说明
├── TODO.md                        # 待办事项
└── PROJECT_RULES.md               # 本文档
```

### 6.2 目录职责说明

**核心目录 (CORE)：**
- `miniprogram/api/` - 数据接口层，负责与后端通信
- `miniprogram/utils/pages/` - 页面逻辑层，承载业务逻辑
- `miniprogram/utils/request.js` - 请求统一网关
- `miniprogram/stores/` - 全局状态管理

**支撑目录：**
- `miniprogram/components/` - 可复用UI组件
- `miniprogram/pages/` - 页面视图层
- `miniprogram/utils/` - 工具函数库
- `miniprogram/static/` - 静态资源

---

## 7. 命名约定

### 7.1 文件和目录命名
- **文件名：** `kebab-case` (短横线分隔)
  - ✅ `project-detail.js`
  - ✅ `user-profile.wxml`
  - ❌ `projectDetail.js`
  - ❌ `UserProfile.wxml`

- **目录名：** `kebab-case`
  - ✅ `project-detail/`
  - ✅ `user-profile/`
  - ❌ `projectDetail/`

### 7.2 JavaScript命名
- **变量和函数：** `camelCase`
  ```javascript
  const projectList = [];
  const currentUser = {};

  function getProjectDetail() {}
  async function createNewTask() {}
  ```

- **常量：** `UPPER_SNAKE_CASE`
  ```javascript
  const API_BASE_URL = 'https://api.example.com';
  const USER_ROLES = {
    OWNER: 'owner',
    PROJECT_MANAGER: 'pm',
    WORKER: 'worker'
  };
  const MAX_UPLOAD_SIZE = 10 * 1024 * 1024; // 10MB
  ```

- **类名：** `PascalCase` (如果使用ES6类)
  ```javascript
  class ProjectManager {
    constructor() {}
  }
  ```

### 7.3 CSS类命名 (BEM方法论)
**BEM格式：** `block__element--modifier`

```css
/* 块 (Block) */
.task-card {}

/* 元素 (Element) */
.task-card__title {}
.task-card__content {}
.task-card__footer {}

/* 修饰符 (Modifier) */
.task-card--completed {}
.task-card--urgent {}
.task-card__title--large {}
```

**实际应用示例：**
```css
/* 项目卡片组件 */
.project-card {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 16px;
}

.project-card__header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 12px;
}

.project-card__title {
  font-size: 18px;
  font-weight: 600;
  color: #333;
}

.project-card__status {
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 12px;
}

.project-card__status--active {
  background-color: #e8f5e8;
  color: #2e7d2e;
}

.project-card__status--completed {
  background-color: #e3f2fd;
  color: #1976d2;
}

.project-card__progress {
  margin-top: 12px;
}

.project-card--featured {
  border-color: #1976d2;
  box-shadow: 0 2px 8px rgba(25, 118, 210, 0.1);
}
```

### 7.4 数据字段命名
- **数据库字段：** `snake_case`
  ```javascript
  {
    user_id: 123,
    project_name: "小明家装修",
    created_at: "2024-01-01T00:00:00Z",
    updated_at: "2024-01-02T00:00:00Z"
  }
  ```

- **API响应字段：** `camelCase`
  ```javascript
  {
    userId: 123,
    projectName: "小明家装修",
    createdAt: "2024-01-01T00:00:00Z",
    updatedAt: "2024-01-02T00:00:00Z"
  }
  ```

### 7.5 页面和组件命名规范
- **页面目录：** 功能描述 + 类型
  - `project-list/` (项目列表)
  - `task-detail/` (任务详情)
  - `user-profile/` (用户资料)

- **组件目录：** 功能描述
  - `task-card/` (任务卡片)
  - `photo-uploader/` (照片上传器)
  - `progress-bar/` (进度条)

---

## 8. API接口规范

### 8.1 请求封装标准
**所有API请求必须通过 `miniprogram/utils/request.js` 统一处理**

### 8.2 标准响应格式
```javascript
// 成功响应
{
  "code": 0,
  "message": "success",
  "data": {
    // 实际数据
  },
  "timestamp": 1640995200000
}

// 错误响应
{
  "code": 1001,
  "message": "参数错误",
  "data": null,
  "timestamp": 1640995200000
}
```

### 8.3 错误码规范
```javascript
const ERROR_CODES = {
  SUCCESS: 0,

  // 客户端错误 (1000-1999)
  INVALID_PARAMS: 1001,
  UNAUTHORIZED: 1002,
  FORBIDDEN: 1003,
  NOT_FOUND: 1004,

  // 业务错误 (2000-2999)
  USER_NOT_EXISTS: 2001,
  PROJECT_NOT_EXISTS: 2002,
  TASK_NOT_EXISTS: 2003,
  PERMISSION_DENIED: 2004,

  // 服务器错误 (5000-5999)
  INTERNAL_ERROR: 5000,
  DATABASE_ERROR: 5001,
  THIRD_PARTY_ERROR: 5002
};
```

### 8.4 API模块组织示例
```javascript
// miniprogram/api/task.js
const request = require('../utils/request');

module.exports = {
  // 获取任务列表
  async getTaskList(projectId, params = {}) {
    return await request.get(`/api/projects/${projectId}/tasks`, params);
  },

  // 获取任务详情
  async getTaskDetail(taskId) {
    return await request.get(`/api/tasks/${taskId}`);
  },

  // 创建任务
  async createTask(projectId, taskData) {
    return await request.post(`/api/projects/${projectId}/tasks`, taskData);
  },

  // 更新任务
  async updateTask(taskId, updateData) {
    return await request.put(`/api/tasks/${taskId}`, updateData);
  },

  // 删除任务
  async deleteTask(taskId) {
    return await request.delete(`/api/tasks/${taskId}`);
  },

  // 任务验收申请
  async requestAcceptance(taskId, acceptanceData) {
    return await request.post(`/api/tasks/${taskId}/acceptance`, acceptanceData);
  },

  // 任务验收审核
  async reviewAcceptance(taskId, reviewData) {
    return await request.put(`/api/tasks/${taskId}/acceptance`, reviewData);
  },

  // 上传任务照片
  async uploadTaskPhoto(taskId, photoData) {
    return await request.post(`/api/tasks/${taskId}/photos`, photoData);
  }
};
```

### 8.5 云函数适配
由于使用微信云开发，实际的HTTP请求会通过云函数代理：

```javascript
// miniprogram/utils/request.js (云函数版本)
const request = {
  async get(url, params = {}) {
    try {
      const response = await wx.cloud.callFunction({
        name: 'api',  // 对应 cloudfunctions/api/ 云函数
        data: {
          method: 'GET',
          resource: this.extractResource(url),
          params
        }
      });
      return this.handleResponse(response);
    } catch (error) {
      return this.handleError(error);
    }
  },

  async post(url, data = {}) {
    try {
      const response = await wx.cloud.callFunction({
        name: 'api',
        data: {
          method: 'POST',
          resource: this.extractResource(url),
          data
        }
      });
      return this.handleResponse(response);
    } catch (error) {
      return this.handleError(error);
    }
  },

  async put(url, data = {}) {
    try {
      const response = await wx.cloud.callFunction({
        name: 'api',
        data: {
          method: 'PUT',
          resource: this.extractResource(url),
          data
        }
      });
      return this.handleResponse(response);
    } catch (error) {
      return this.handleError(error);
    }
  },

  async delete(url, params = {}) {
    try {
      const response = await wx.cloud.callFunction({
        name: 'api',
        data: {
          method: 'DELETE',
          resource: this.extractResource(url),
          params
        }
      });
      return this.handleResponse(response);
    } catch (error) {
      return this.handleError(error);
    }
  },

  // 从URL中提取资源类型，如 '/api/projects' -> 'project'
  extractResource(url) {
    const match = url.match(/\/api\/(\w+)/);
    return match ? match[1].replace(/s$/, '') : 'unknown'; // 去掉复数s
  },

  handleResponse(response) {
    const { result } = response;
    if (result.code === 0) {
      return result.data;
    } else {
      throw new Error(result.message || '请求失败');
    }
  },

  handleError(error) {
    console.error('Request Error:', error);
    wx.showToast({
      title: error.message || '网络错误',
      icon: 'error'
    });
    return Promise.reject(error);
  }
};

module.exports = request;
```

---

## 9. 代码风格规范

### 9.1 ESLint配置
**推荐使用ESLint + Prettier进行代码格式化**

`.eslintrc.js` 配置：
```javascript
module.exports = {
  env: {
    browser: true,
    es6: true,
    node: true
  },
  extends: [
    'eslint:recommended'
  ],
  globals: {
    wx: 'readonly',
    App: 'readonly',
    Page: 'readonly',
    Component: 'readonly',
    getApp: 'readonly',
    getCurrentPages: 'readonly'
  },
  parserOptions: {
    ecmaVersion: 2020,
    sourceType: 'module'
  },
  rules: {
    // 强制使用分号
    'semi': ['error', 'always'],

    // 强制使用单引号
    'quotes': ['error', 'single'],

    // 禁止未使用的变量
    'no-unused-vars': 'error',

    // 禁止console.log (生产环境)
    'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'warn',

    // 强制使用const/let而不是var
    'no-var': 'error',
    'prefer-const': 'error',

    // 对象和数组的尾随逗号
    'comma-dangle': ['error', 'never'],

    // 缩进规则
    'indent': ['error', 2],

    // 行尾空格
    'no-trailing-spaces': 'error'
  }
};
```

### 9.2 异步操作规范
**优先使用 `async/await` 而不是 Promise.then()**

```javascript
// ✅ 推荐写法
async function loadProjectData(projectId) {
  try {
    const project = await projectApi.getProjectDetail(projectId);
    const tasks = await taskApi.getProjectTasks(projectId);
    const members = await projectApi.getProjectMembers(projectId);

    return {
      project,
      tasks,
      members
    };
  } catch (error) {
    console.error('加载项目数据失败:', error);
    throw error;
  }
}

// ❌ 不推荐写法
function loadProjectData(projectId) {
  return projectApi.getProjectDetail(projectId)
    .then(project => {
      return taskApi.getProjectTasks(projectId)
        .then(tasks => {
          return projectApi.getProjectMembers(projectId)
            .then(members => {
              return { project, tasks, members };
            });
        });
    })
    .catch(error => {
      console.error('加载项目数据失败:', error);
      throw error;
    });
}
```

### 9.3 错误处理规范
```javascript
// 统一错误处理模式
async function handleAsyncOperation() {
  try {
    const result = await someAsyncOperation();
    return result;
  } catch (error) {
    // 记录错误
    console.error('操作失败:', error);

    // 用户友好的错误提示
    wx.showToast({
      title: '操作失败，请重试',
      icon: 'error'
    });

    // 重新抛出错误供上层处理
    throw error;
  }
}
```

### 9.4 代码注释规范
```javascript
/**
 * 获取项目详情和相关数据
 * @param {string} projectId - 项目ID
 * @param {Object} options - 可选参数
 * @param {boolean} options.includeTasks - 是否包含任务列表
 * @param {boolean} options.includeMembers - 是否包含成员列表
 * @returns {Promise<Object>} 项目详情数据
 */
async function getProjectDetail(projectId, options = {}) {
  const { includeTasks = true, includeMembers = true } = options;

  // 获取基础项目信息
  const project = await projectApi.getProjectDetail(projectId);

  // 根据选项获取额外数据
  const additionalData = {};

  if (includeTasks) {
    additionalData.tasks = await taskApi.getProjectTasks(projectId);
  }

  if (includeMembers) {
    additionalData.members = await projectApi.getProjectMembers(projectId);
  }

  return {
    ...project,
    ...additionalData
  };
}
```

---

## 10. 微信小程序最佳实践

### 10.1 分包策略
**主包 (Main Package)：** 核心功能，控制在2MB以内
- 登录注册
- 项目列表
- 项目详情
- 任务管理核心功能

**分包 (Sub Packages)：** 按功能模块拆分
```json
{
  "pages": [
    "pages/index/index",
    "pages/login/login",
    "pages/project-list/project-list",
    "pages/project-detail/project-detail"
  ],
  "subpackages": [
    {
      "root": "subpackages/chat",
      "name": "chat",
      "pages": [
        "pages/chat-room/chat-room",
        "pages/chat-list/chat-list"
      ]
    },
    {
      "root": "subpackages/finance",
      "name": "finance",
      "pages": [
        "pages/expense-record/expense-record",
        "pages/budget-manage/budget-manage"
      ]
    },
    {
      "root": "subpackages/admin",
      "name": "admin",
      "pages": [
        "pages/user-manage/user-manage",
        "pages/project-settings/project-settings"
      ]
    }
  ],
  "preloadRule": {
    "pages/project-detail/project-detail": {
      "network": "all",
      "packages": ["chat"]
    }
  }
}
```

### 10.2 组件化开发
**组件设计原则：**
- 单一职责：每个组件只负责一个功能
- 可复用性：组件应该在多个场景下可用
- 数据驱动：通过props传递数据，通过events通信

**任务卡片组件示例：**
```javascript
// miniprogram/components/task-card/task-card.js
Component({
  properties: {
    task: {
      type: Object,
      value: {}
    },
    showActions: {
      type: Boolean,
      value: true
    },
    userRole: {
      type: String,
      value: 'owner'
    }
  },

  data: {
    statusMap: {
      'pending': '待开始',
      'in_progress': '进行中',
      'completed': '已完成',
      'accepted': '已验收'
    }
  },

  methods: {
    onTaskClick() {
      this.triggerEvent('taskclick', {
        taskId: this.data.task.id
      });
    },

    onAcceptanceRequest() {
      this.triggerEvent('acceptancerequest', {
        taskId: this.data.task.id
      });
    },

    onStatusChange(event) {
      const newStatus = event.detail.value;
      this.triggerEvent('statuschange', {
        taskId: this.data.task.id,
        newStatus
      });
    }
  }
});
```

### 10.3 setData优化技巧
**批量更新：**
```javascript
// ✅ 推荐：批量更新
this.setData({
  'project.name': newName,
  'project.status': newStatus,
  'project.updatedAt': new Date().toISOString(),
  loading: false
});

// ❌ 不推荐：多次调用setData
this.setData({ 'project.name': newName });
this.setData({ 'project.status': newStatus });
this.setData({ 'project.updatedAt': new Date().toISOString() });
this.setData({ loading: false });
```

**数据差异更新：**
```javascript
// 只更新变化的数据
updateTaskList(newTasks) {
  const currentTasks = this.data.tasks;
  const updates = {};

  newTasks.forEach((task, index) => {
    if (!currentTasks[index] || currentTasks[index].id !== task.id) {
      updates[`tasks[${index}]`] = task;
    } else {
      // 检查任务属性是否有变化
      Object.keys(task).forEach(key => {
        if (currentTasks[index][key] !== task[key]) {
          updates[`tasks[${index}].${key}`] = task[key];
        }
      });
    }
  });

  if (Object.keys(updates).length > 0) {
    this.setData(updates);
  }
}
```

### 10.4 内存管理和生命周期优化
```javascript
// 页面生命周期管理
Page({
  data: {
    timer: null,
    observer: null
  },

  onLoad() {
    // 初始化
    this.initPage();
  },

  onShow() {
    // 页面显示时启动定时器
    this.startTimer();
    // 监听网络状态
    this.watchNetworkStatus();
  },

  onHide() {
    // 页面隐藏时清理定时器
    this.clearTimer();
  },

  onUnload() {
    // 页面卸载时清理所有资源
    this.cleanup();
  },

  startTimer() {
    this.data.timer = setInterval(() => {
      this.refreshData();
    }, 30000); // 30秒刷新一次
  },

  clearTimer() {
    if (this.data.timer) {
      clearInterval(this.data.timer);
      this.setData({ timer: null });
    }
  },

  watchNetworkStatus() {
    this.data.observer = wx.onNetworkStatusChange((res) => {
      if (res.isConnected) {
        this.refreshData();
      }
    });
  },

  cleanup() {
    this.clearTimer();
    if (this.data.observer) {
      wx.offNetworkStatusChange(this.data.observer);
    }
  }
});
```

### 10.5 性能优化策略
**图片优化：**
```javascript
// 图片懒加载组件
Component({
  properties: {
    src: String,
    defaultSrc: String
  },

  data: {
    loaded: false,
    currentSrc: ''
  },

  lifetimes: {
    attached() {
      this.setData({
        currentSrc: this.data.defaultSrc || '/static/images/placeholder.png'
      });
      this.observeImage();
    }
  },

  methods: {
    observeImage() {
      const observer = this.createIntersectionObserver();
      observer.relativeToViewport().observe('.lazy-image', (res) => {
        if (res.intersectionRatio > 0) {
          this.loadImage();
          observer.disconnect();
        }
      });
    },

    loadImage() {
      if (this.data.src) {
        this.setData({
          currentSrc: this.data.src,
          loaded: true
        });
      }
    }
  }
});
```

**列表优化：**
```javascript
// 虚拟列表实现
Page({
  data: {
    allTasks: [],
    visibleTasks: [],
    scrollTop: 0,
    itemHeight: 120,
    containerHeight: 600,
    startIndex: 0,
    endIndex: 0
  },

  onLoad() {
    this.calculateVisibleItems();
  },

  onScroll(event) {
    const scrollTop = event.detail.scrollTop;
    this.setData({ scrollTop });
    this.updateVisibleItems(scrollTop);
  },

  calculateVisibleItems() {
    const { containerHeight, itemHeight } = this.data;
    const visibleCount = Math.ceil(containerHeight / itemHeight) + 2; // 缓冲2个
    this.setData({ visibleCount });
  },

  updateVisibleItems(scrollTop) {
    const { itemHeight, visibleCount, allTasks } = this.data;
    const startIndex = Math.floor(scrollTop / itemHeight);
    const endIndex = Math.min(startIndex + visibleCount, allTasks.length);

    const visibleTasks = allTasks.slice(startIndex, endIndex).map((task, index) => ({
      ...task,
      _index: startIndex + index
    }));

    this.setData({
      startIndex,
      endIndex,
      visibleTasks
    });
  }
});
```

### 10.6 云开发最佳实践
**云函数组织：**
```javascript
// 云函数统一入口
// cloudfunctions/api/index.js
const cloud = require('wx-server-sdk');
cloud.init({ env: cloud.DYNAMIC_CURRENT_ENV });

const userHandler = require('./handlers/user');
const projectHandler = require('./handlers/project');
const taskHandler = require('./handlers/task');

exports.main = async (event, context) => {
  const { method, resource, data } = event;

  try {
    switch (resource) {
      case 'user':
        return await userHandler[method](data, context);
      case 'project':
        return await projectHandler[method](data, context);
      case 'task':
        return await taskHandler[method](data, context);
      default:
        throw new Error('Unknown resource');
    }
  } catch (error) {
    console.error('API Error:', error);
    return {
      code: 5000,
      message: error.message,
      data: null
    };
  }
};
```

**数据库操作优化：**
```javascript
// 批量操作
async function batchUpdateTasks(taskUpdates) {
  const db = cloud.database();
  const batch = db.batch();

  taskUpdates.forEach(update => {
    batch.collection('tasks').doc(update.id).update({
      data: update.data
    });
  });

  return await batch.commit();
}

// 聚合查询
async function getProjectStatistics(projectId) {
  const db = cloud.database();
  const $ = db.command.aggregate;

  return await db.collection('tasks')
    .aggregate()
    .match({ projectId })
    .group({
      _id: '$status',
      count: $.sum(1)
    })
    .end();
}
```

---

## 📚 总结

本文档定义了"自己装"装修协同平台的完整开发规范，涵盖：

1. **架构原则** - 严格的关注点分离，确保代码可维护性
2. **状态管理** - 基于MobX的全局状态管理方案
3. **开发规范** - 从命名到代码风格的全面标准
4. **性能优化** - 微信小程序特有的优化策略

**🎯 核心要求：**
- 所有开发必须遵循本文档规范
- AI助手必须以本文档为最高准则
- 任何架构变更需要更新本文档

**📈 持续改进：**
- 定期review和更新规范
- 根据项目发展调整架构
- 保持文档与代码同步

---

*最后更新：2024-01-01*
*版本：v1.0*
*维护者：项目架构团队*
