# AI互动叙事小说游戏项目结构

## 一、目录总体结构

```
public/
├── index.html            # 主入口页面
├── lobby.html            # 大厅页面
├── shop.html             # 商店页面
├── game.html             # 游戏主页面
├── styles/               # 全局样式
│   ├── variables.css     # 全局变量
│   ├── common-reset.css  # 重置样式
│   ├── common-utils.css  # 工具类
│   ├── common-btn.css    # 通用按钮
│   └── common-layout.css # 通用布局
├── assets/               # 静态资源
│   ├── images/           # 图片资源
│   ├── sounds/           # 音效资源
│   └── fonts/            # 字体资源
└── js/                   # JavaScript代码
    ├── core/             # 核心模块
    ├── firebase/         # Firebase相关
    ├── modules/          # 功能模块
    ├── home/             # 主页模块
    ├── lobby/            # 大厅模块
    ├── shop/             # 商店模块
    ├── game/             # 游戏模块
    └── world-selection/  # 世界选择模块
```

## 二、核心模块结构详解

### 1. 核心模块 (js/core/)

```
core/
├── auth/                         # 认证相关
│   ├── AuthService.js            # 认证服务
│   ├── AuthModal.js              # 认证弹窗
│   └── AnonymousUpgrader.js      # 匿名升级
├── cache/                        # 缓存相关
│   ├── CacheManager.js           # 缓存管理器
│   ├── CacheConfig.js            # 缓存配置
│   ├── CommonDataCache.js        # 通用数据缓存
│   ├── UserDataCache.js          # 用户数据缓存
│   └── CacheHelper.js            # 缓存辅助工具
├── events/                       # 事件相关
│   ├── EventBus.js               # 事件总线
│   └── EventListeners.js         # 事件监听器
├── ui/                           # UI工具
│   ├── NotificationManager.js    # 通知管理
│   ├── LoadingManager.js         # 加载管理
│   ├── DialogManager.js          # 对话框管理
│   └── Templates.js              # 模板系统
├── assets/                       # 资产相关
│   ├── UserAssetsManager.js      # 用户资产管理
│   └── TransactionCore.js        # 交易核心
├── utils/                        # 工具模块
│   ├── LoggerService.js          # 日志服务
│   ├── SessionGuard.js           # 会话守卫
│   ├── ErrorHandler.js           # 错误处理
│   └── DeviceDetector.js         # 设备检测
└── services/                     # 服务模块
    ├── ModuleDependency.js       # 模块依赖
    ├── LogoutManager.js          # 登出管理
    └── BackgroundEffects.js      # 背景特效
```

### 2. Firebase模块 (js/firebase/)

```
firebase/
├── FirebaseConfig.js             # Firebase配置
├── FirebaseDataReader.js         # 数据读取
├── WorldDataManager.js           # 世界数据管理
└── WorldFrameworks.js            # 世界框架管理
```

### 3. 模块目录 (js/modules/)

```
modules/
├── ai-service/                   # AI服务
│   ├── AIService.js              # AI服务主类
│   └── ResponseHandler.js        # 响应处理
├── save/                         # 存档系统
│   ├── SaveManager.js            # 存档管理器
│   └── CloudSync.js              # 云同步
├── unlock/                       # 解锁系统
│   ├── UnlockManager.js          # 解锁管理器
│   └── UnlockAnimation.js        # 解锁动画
├── world-selection/              # 世界选择
│   ├── WorldSelectionManager.js  # 选择管理器
│   └── ui/                       # 选择UI
│       └── WorldSelectionUI.js   # 选择界面
└── vip-and-package/              # VIP和组合包
    ├── VIPManager.js             # VIP管理
    └── PackageManager.js         # 包管理
```

## 三、业务模块详解

### 1. 主页模块 (js/home/)

```
home/
├── css/                          # 主页样式
│   ├── home-main.css             # 主样式
│   ├── home-header.css           # 头部样式
│   └── home-content.css          # 内容样式
├── main.js                       # 主入口
├── HomeManager.js                # 主页管理器
├── components/                   # 组件
│   ├── MysteriousVoice.js        # 神秘声音
│   └── PlayerChoices.js          # 玩家选择
└── Auth.js                       # 主页认证
```

### 2. 大厅模块 (js/lobby/)

```
lobby/
├── css/                          # 大厅样式
│   ├── lobby-main.css            # 主样式
│   ├── lobby-nav.css             # 导航样式
│   └── lobby-cards.css           # 卡片样式
├── main.js                       # 主入口
├── LobbyManager.js               # 大厅管理器
├── components/                   # 组件
│   ├── WorldFrameworksPanel.js   # 框架面板
│   ├── SavesPanel.js             # 存档面板
│   ├── UserProfilePanel.js       # 个人资料
│   └── SettingsPanel.js          # 设置面板
├── Auth.js                       # 大厅认证
└── config/                       # 配置
    └── save-config.js            # 存档配置
```

### 3. 商店模块 (js/shop/)

```
shop/
├── css/                          # 商店样式
│   ├── shop-main.css             # 主样式
│   ├── shop-cards.css            # 卡片样式
│   └── shop-modals.css           # 弹窗样式
├── main.js                       # 主入口
├── ShopManager.js                # 商店管理器
├── Core.js                       # 商店核心
├── Auth.js                       # 商店认证
├── components/                   # 组件
│   ├── FrameworksPanel.js        # 框架面板
│   ├── VIPPanel.js               # VIP面板
│   ├── PackagesPanel.js          # 组合包面板
│   ├── OrdersPanel.js            # 订单面板
│   └── PurchaseDialog.js         # 购买弹窗
├── services/                     # 服务
│   ├── Frameworks.js             # 框架服务
│   ├── Price.js                  # 价格服务
│   ├── Orders.js                 # 订单服务
│   ├── Purchase.js               # 购买服务
│   └── Refresh.js                # 刷新服务
└── events/                       # 事件
    └── Events.js                 # 商店事件
```

### 4. 游戏模块 (js/game/)

```
game/
├── css/                          # 游戏样式
│   ├── game-main.css             # 主样式
│   └── game-ui.css               # UI样式
├── main.js                       # 主入口
├── Game.js                       # 游戏主类
├── GameState.js                  # 游戏状态
├── components/                   # 组件
│   ├── StoryDisplay.js           # 故事显示
│   ├── ChoicesPanel.js           # 选择面板
│   ├── CharacterPanel.js         # 角色面板
│   └── BattleSystem.js           # 战斗系统
└── utils/                        # 工具
    ├── StoryParser.js            # 故事解析
    └── GameSaver.js              # 游戏保存
```

## 四、部署与构建结构

```
/
├── public/                       # 静态资源和代码
├── Docs/                         # 文档目录
│   ├── PRD.md                    # 产品需求文档
│   ├── home.prd.md               # 主页需求
│   ├── lobby.prd.md              # 大厅需求
│   └── shop.prd.md               # 商店需求
├── .env                          # 环境变量(敏感信息)
├── firebase.json                 # Firebase配置
├── package.json                  # 项目配置
└── README.md                     # 项目说明
```

## 五、数据流与模块关系

### 1. 认证流程
- AuthService → UserAssetsManager → Firebase → UI更新

### 2. 框架数据流
- FirebaseDataReader → WorldDataManager → WorldFrameworks → 业务模块

### 3. 购买流程
- PurchaseDialog → Shop.Purchase → TransactionCore → UserAssetsManager → UnlockManager → UI更新

### 4. 存档流程
- SaveManager → FirebaseDataReader → CloudSync → UI更新

### 5. AI生成流程
- Game → AIService → ResponseHandler → StoryDisplay

## 六、关键接口与依赖

### 1. 全局单例模块
- `window.firebaseApp` - Firebase应用
- `window.CacheManager` - 缓存管理
- `window.EventBus` - 事件总线
- `window.WorldFrameworks` - 世界框架数据
- `window.userAssetsManager` - 用户资产
- `window.saveManager` - 存档管理
- `window.authService` - 认证服务
- `window.logoutManager` - 登出管理

### 2. 主要模块间通信
- 严格通过事件系统通信，遵循事件命名规范
- 各模块通过公开接口提供服务，不直接修改他人数据
- 用户资产、存档、框架等核心数据由专属模块管理

### 3. 外部依赖
- Firebase (认证、数据库、存储)
- 外部AI服务 (通过AIService统一调用)

## 七、代码规范与命名约定

### 1. CSS规范
- 全局样式: `common-*.css`
- 模块样式: `[模块]-*.css`
- 类名前缀: 全局`.common-*`，模块`.模块-*`

### 2. JavaScript规范
- 类文件: 大驼峰 `ClassName.js`
- 工具文件: 小驼峰 `utilName.js`
- 配置文件: 小驼峰 `configName.js`
- 常量: 全大写下划线 `CONSTANT_NAME`

### 3. 模块导出规范
- 全局挂载到`window.Modules`对象
- 业务模块挂载到对应命名空间(`window.Shop`等)

## 八、开发规则

### 1. 模块边界与职责
- 严格遵循MDC规则定义的模块边界
- 每个模块只负责自身职责范围内的功能
- 禁止跨模块直接操作数据或DOM

### 2. 事件通信规则
- 所有模块间通信必须通过事件系统
- 事件命名必须遵循`命名空间.操作`格式
- 事件detail必须包含关键信息和时间戳

### 3. 缓存管理规则
- 所有缓存必须通过CacheManager统一管理
- 缓存数据必须带有签名和过期时间
- 敏感数据必须加密存储

### 4. 错误处理规则
- 所有异步操作必须有错误捕获
- 关键操作必须有重试机制
- 用户界面必须提供明确的错误反馈
