# 新大厅模块产品需求文档

## 1. 概述

新大厅是游戏的主要交互界面，负责世界框架展示、存档管理、用户资产显示和全局导航等核心功能。全新实现原有大厅的所有功能，但使用更现代化的架构和更清晰的代码组织。实现严格遵循MDC规则，包括认证、事件系统、数据管理、UI组件、安全机制等。

## 2. 核心功能模块

### 2.1 大厅主页

- 提供世界框架展示区、存档管理区、资产栏、快捷入口、操作按钮区四大核心区域
- **默认展示"世界框架"(world类别)** 作为首个展示的框架类型
- 支持根据用户状态（游客/登录/VIP）显示不同内容
- 实现顶部导航栏，包含分类切换功能
- 右侧/顶部显示用户资产（金币、钻石）信息

### 2.2 世界选择（开始游戏）

- 点击"开始游戏"或"世界选择"按钮，打开世界框架选择界面
- 世界框架以卡片形式展示，支持分类
- 框架卡片包含名称、描述和解锁状态
- 已解锁框架点击后展示操作选项：
  - 创建新存档
  - 载入现有存档（如有）
- 未解锁框架显示锁定状态，点击显示解锁条件或跳转商店
- 世界选择流程完全遵循world-selection.mdc规则
- 选择完成后，根据用户选择进入游戏或创建新存档

### 2.3 存档管理

- 展示当前用户所有存档，包含标题、创建时间、最后游玩时间
- 支持创建新存档、加载存档、删除存档、导入/导出存档
- 存档操作必须通过统一的SaveManager接口
- 支持自动保存、云同步、多端合并
- 存档列表根据更新时间排序
- **存档配置文件**：
  - 位于`newlobby/config/save-config.js`
  - 可配置免费用户存档位数（默认3个）
  - 可配置VIP用户存档位数（默认10个）
  - 可配置存档最大容量（默认5MB）
  - 可配置自动保存间隔（默认5分钟）
- 存档功能完全遵循save-manager.mdc规则

### 2.4 冒险记录

- **注：本功能将在后续版本实现，当前PRD仅作占位说明**
- 冒险记录为玩家之前完成的故事完整剧情回顾
- 按时间顺序展示所有已完成的故事
- 每个故事条目包含：
  - 故事标题
  - 完成时间
  - 所用框架
  - 角色信息
- 点击后可查看完整故事流程和选择
- 支持收藏、分享功能

### 2.5 资产栏与VIP状态

- 顶部显示用户当前金币、钻石数量和VIP状态
- 点击金币/钻石图标可跳转商店充值
- VIP状态显示到期时间和特权图标
- 资产变更时的动画效果
- 实时同步和更新资产数据

### 2.6 个人档案

- 显示用户基本信息：
  - 用户名/昵称
  - 账号类型（匿名、Google账号、邮箱账号）
  - 邮箱地址（如有）
  - 创建时间
  - VIP状态和到期时间
- 匿名用户显示"升级到正式账号"按钮
  - 点击后显示注册窗口
  - 支持邮箱注册和Google账号绑定
  - 升级过程确保所有数据和资产完整迁移
- 正式账户显示"修改资料"按钮
  - 可修改用户昵称
- 显示游戏统计数据：
  - 总游戏时长
  - 完成故事数
  - 解锁框架数
  - 创建角色数
- 个人档案功能完全遵循auth-ui.mdc规则

### 2.7 商店入口

- 提供明显的"商店"入口按钮
- 点击后跳转到shop.html页面
- 支持传递当前用户状态和VIP信息
- 与商店模块完全集成，遵循shop相关的mdc规则
- 商店返回时自动刷新大厅数据

### 2.8 设置功能

- 提供全局游戏设置功能，包括：
  - 音效设置（开/关、音量）
  - 音乐设置（开/关、音量）
  - 文字大小调整
  - 动画效果（开/关、简化）
  - 语言选择
  - 通知设置
  - 自动保存频率
  - 数据同步设置
- 设置实时生效，自动保存到本地
- 支持重置为默认设置
- 设置弹窗使用统一的UI组件，遵循lobby-ui.mdc规则

### 2.9 快捷入口

- 商店入口：跳转至商店页面
- 设置入口：显示游戏设置面板
- 帮助入口：显示游戏帮助文档
- 所有入口通过事件系统触发，禁止直接页面跳转

### 2.10 操作按钮区

- 刷新按钮：重新加载框架和存档数据
- 同步按钮：强制云同步所有数据
- 登出按钮：清理数据并登出账号
- 所有操作必须通过事件系统触发，有加载状态和结果反馈

### 2.11 通知区

- 统一的通知展示区域
- 支持成功、错误、警告、信息四种类型通知
- 通知自动消失，支持手动关闭
- 所有系统消息必须通过通知区展示，禁止自定义弹窗

## 3. 用户界面

### 3.1 整体布局

- 响应式设计，适配各种屏幕尺寸
- 主体内容区域居中，最大宽度限制
- 分层结构：背景层、装饰层、主内容区、通知区
- 所有UI元素必须位于页面可视区域内，避免超出屏幕

### 3.2 框架卡片组件

- 统一的卡片设计，类名统一用 ui-lobby-card-* 前缀
- 卡片包含标题、描述、状态标记
- 卡片悬停效果和点击动画
- 不同状态（已解锁、未解锁、VIP专属）的视觉区分
- 支持批量渲染和虚拟列表技术

### 3.3 存档列表组件

- 统一的存档项设计，类名统一用 ui-lobby-save-* 前缀
- 存档项包含标题、时间、操作按钮
- 新建存档按钮位于列表顶部
- 存档项操作菜单（加载、删除、导出）
- 支持空状态和加载状态显示

### 3.4 弹窗组件

- 统一的弹窗设计，类名统一用 ui-lobby-dialog-* 前缀
- 支持确认弹窗、表单弹窗、结果弹窗
- 所有弹窗有统一的关闭按钮和动画效果
- 弹窗显示时禁用背景交互

### 3.5 导航

- 顶部分类导航，支持在七个固定类型间切换
- 分类切换时保留当前选择状态
- 过滤器仅存储当前选中分类，默认为"world"

## 4. 数据结构与管理

### 4.1 框架数据结构

```
{
  id: string,         // 如 "world_1" 
  name: string,       // 显示名称
  description: string, // 描述
  category: string,   // "world"、"era"、"technology"等七种固定类型
  type: "normal" | "premium", // 普通/高级
  isVIP: boolean,     // 是否VIP专属
  isUnlocked: boolean, // 是否已解锁
}
```

### 4.2 存档数据结构

```
{
  id: string,         // 存档ID
  userId: string,     // 用户ID
  title: string,      // 存档标题
  description: string, // 存档描述
  frameworkId: string, // 关联的框架ID
  createdAt: string,  // 创建时间，ISO格式
  updatedAt: string,  // 更新时间，ISO格式
  playTime: number,   // 游戏时长（秒）
  gameVersion: string, // 游戏版本
  lastScene: string,  // 最后场景
  data: object        // 实际游戏数据（序列化）
}
```

### 4.3 用户资产数据结构

```
{
  userId: string,
  coins: number,
  diamonds: number,
  ownedFrameworks: string[], // 拥有的框架ID
  vipStatus: {
    isActive: boolean,
    expiryDate: string      // ISO日期
  },
  lastUpdated: string       // ISO日期
}
```

### 4.4 用户个人档案数据结构

```
{
  userId: string,
  displayName: string,      // 显示名称
  accountType: "anonymous" | "google" | "email", // 账号类型
  email: string,            // 邮箱（如有）
  createdAt: string,        // 创建时间，ISO格式
  stats: {
    totalPlayTime: number,  // 总游戏时长（秒）
    completedStories: number, // 完成故事数
    unlockedFrameworks: number, // 解锁框架数
    createdCharacters: number   // 创建角色数
  }
}
```

### 4.5 设置数据结构

```
{
  userId: string,
  audioEffects: {
    enabled: boolean,
    volume: number         // 0-100
  },
  music: {
    enabled: boolean,
    volume: number         // 0-100
  },
  textSize: "small" | "medium" | "large",
  animations: {
    enabled: boolean,
    simplified: boolean
  },
  language: string,        // "zh-CN", "en-US"等
  notifications: {
    enabled: boolean,
    types: string[]        // ["success", "error", "info"]
  },
  autoSave: {
    interval: number,      // 分钟
    enabled: boolean
  },
  dataSync: {
    autoSync: boolean,
    syncInterval: number   // 分钟
  }
}
```

### 4.6 数据获取策略

- 框架数据**优先从本地缓存获取**
  - 框架数据通过 `window.WorldFrameworks` 获取
  - 存档数据通过 `window.saveManager` 获取
  - 用户资产通过 `window.userAssetsManager` 获取
- 缓存失效或不存在时，才从服务器拉取
- 本地缓存加签名和过期时间（12小时），读取时验证
- 数据刷新使用指数退避策略，有频率限制

## 5. 事件系统

### 5.1 大厅核心事件

- `lobby.initialized` - 大厅初始化完成
- `lobby.category.changed` - 分类切换（如从world切换到era）
- `world-frameworks-ready` - 框架数据加载完成
- `lobby.filter-changed` - 过滤条件变更

### 5.2 框架与存档事件

- `lobby.framework.selected` - 框架选中
- `lobby.framework.enter` - 进入已解锁框架
- `lobby.save.created` - 创建新存档
- `lobby.save.loaded` - 加载存档
- `lobby.save.deleted` - 删除存档
- `lobby.save.exported` - 导出存档
- `lobby.save.imported` - 导入存档

### 5.3 操作与状态事件

- `lobby.refresh.started` - 刷新数据开始
- `lobby.refresh.completed` - 刷新数据完成
- `lobby.sync.started` - 同步数据开始
- `lobby.sync.completed` - 同步数据完成
- `lobby.logout.requested` - 请求登出
- `lobby.logout.completed` - 登出完成

### 5.4 资产与通知事件

- `lobby.assets.updated` - 资产更新
- `lobby.notification.show` - 显示通知
- `lobby.notification.hide` - 隐藏通知
- `lobby.error.occurred` - 发生错误

### 5.5 个人档案与设置事件

- `lobby.profile.opened` - 打开个人档案
- `lobby.profile.updated` - 更新个人档案
- `lobby.settings.changed` - 设置变更
- `lobby.settings.reset` - 重置设置
- `lobby.anonymous.upgrade.started` - 匿名升级开始
- `lobby.anonymous.upgrade.completed` - 匿名升级完成

## 6. 交互流程

### 6.1 大厅初始化流程

1. 初始化Lobby.Core单例，创建全局状态
2. 检查用户认证状态（Lobby.Auth）
3. 加载世界框架数据（优先缓存）
4. 加载用户存档列表（优先缓存）
5. 分类框架数据（七个固定类别）
6. 默认选中"world"类别
7. 渲染UI，显示框架卡片和存档列表
8. 绑定事件监听
9. 派发`lobby.initialized`事件

### 6.2 进入游戏流程

1. 用户点击"开始游戏"或选择已解锁框架，派发`lobby.framework.selected`事件
2. 系统显示两个选项：创建新存档或选择已有存档
3. 如选择创建新存档：
   - 显示创建存档弹窗
   - 用户输入存档名称并确认
   - 系统创建新存档，派发`lobby.save.created`事件
   - 进入游戏界面
4. 如选择已有存档：
   - 显示相关框架的存档列表
   - 用户选择一个存档
   - 系统加载存档，派发`lobby.save.loaded`事件
   - 进入游戏界面

### 6.3 框架解锁流程

1. 用户点击未解锁框架卡片
2. 系统检查是否满足解锁条件
3. 如果可以直接解锁（满足条件）：
   - 显示解锁确认弹窗
   - 用户确认解锁
   - 系统更新框架状态，派发`framework.unlocked`事件
   - 更新UI，显示解锁动画
4. 如需要购买：
   - 显示跳转商店确认弹窗
   - 用户确认后跳转商店对应框架购买页

### 6.4 匿名账号升级流程

1. 用户点击个人档案中的"升级到正式账号"按钮
2. 系统显示账号升级选项：邮箱注册或Google账号
3. 用户选择升级方式并完成注册/绑定
4. 系统迁移所有用户数据和资产
5. 更新用户状态和UI显示
6. 派发`lobby.anonymous.upgrade.completed`事件
7. 显示升级成功通知

### 6.5 设置管理流程

1. 用户点击设置按钮
2. 系统显示设置面板
3. 用户调整设置选项
4. 设置实时保存和应用
5. 用户关闭设置面板
6. 系统派发`lobby.settings.changed`事件

### 6.6 数据同步与冲突处理

1. 用户资产或存档变更后，触发同步
2. 优先使用BroadcastChannel同步，不可用时降级为localStorage事件
3. 检测到冲突时，按时间戳取最新，支持三向合并
4. 合并后广播同步完成事件
5. 所有模块响应刷新UI

### 6.7 错误处理流程

1. 网络错误时，显示重试选项，采用指数退避策略
2. 会话过期时，强制登出并提示重新登录
3. 数据加载失败时，显示错误提示，支持手动刷新
4. 所有错误通过统一通知区显示，包含错误代码和说明
5. 关键操作失败时，有详细日志记录

## 7. 安全与性能

### 7.1 安全措施

- 所有关键操作必须在服务端验证
- 会话状态定期校验，关键操作前实时验证
- 敏感数据加密存储，添加签名和时间戳
- 用户切换、登出时彻底清理所有相关缓存和状态
- 资产变更必须有详细日志记录

### 7.2 性能优化

- 使用DocumentFragment减少DOM操作，降低重排重绘
- 应用虚拟列表技术，只渲染可视区域的卡片
- 本地缓存频繁访问的数据，减少网络请求
- 检测设备性能，低端设备自动降级动画效果

## 8. 样式与组件规范

- 所有UI组件命名和类名使用功能性前缀（ui-lobby-*）
- 所有样式文件集中在public/css/lobby/目录，按页面和组件分类
- 所有风格、颜色、字体等变量集中在variables.css
- 组件化开发，每个UI/功能块单独文件
- 响应式设计，适配从320px到2560px的屏幕宽度

## 9. 约束与禁止事项
- 禁止内联样式和硬编码颜色、字体。
- 禁止直接操作DOM或全局变量，所有交互通过事件系统。
- 禁止各处自定义弹窗，必须通过统一的通知和弹窗组件。
- 所有实现必须严格遵守 mdc 规则。
