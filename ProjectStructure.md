# AI互动叙事小说游戏项目结构 (TypeScript + React + Firebase)

## 一、目录总体结构

```
src/
├── index.tsx             # 应用入口点
├── App.tsx               # 应用根组件
├── pages/                # 页面组件
│   ├── Home.tsx          # 主页组件
│   ├── Lobby.tsx         # 大厅页面组件
│   ├── Shop.tsx          # 商店页面组件
│   └── Game.tsx          # 游戏主页面组件
├── components/           # 共享UI组件
│   ├── common/           # 通用组件
│   ├── home/             # 主页相关组件
│   ├── lobby/            # 大厅相关组件
│   ├── shop/             # 商店相关组件
│   └── game/             # 游戏相关组件
├── styles/               # 样式文件
│   ├── variables.scss    # 全局变量
│   ├── global.scss       # 全局样式
│   ├── components/       # 组件样式
│   └── pages/            # 页面样式
├── assets/               # 静态资源
│   ├── images/           # 图片资源
│   ├── sounds/           # 音效资源
│   └── fonts/            # 字体资源
├── services/             # 服务层
│   ├── firebase/         # Firebase相关服务
│   ├── ai/               # AI服务
│   ├── auth/             # 认证服务
│   └── game/             # 游戏服务
├── hooks/                # 自定义React Hooks
├── contexts/             # React Context
├── utils/                # 工具函数
├── types/                # TypeScript类型定义
└── config/               # 配置文件
```

## 二、核心模块结构详解

### 1. 服务层 (src/services/)

```
services/
├── auth/                           # 认证相关
│   ├── AuthService.ts              # 认证服务
│   ├── useAuth.ts                  # 认证Hook
│   └── AnonymousUpgrader.ts        # 匿名升级
├── cache/                          # 缓存相关
│   ├── CacheManager.ts             # 缓存管理器
│   ├── CacheConfig.ts              # 缓存配置
│   ├── CommonDataCache.ts          # 通用数据缓存
│   ├── UserDataCache.ts            # 用户数据缓存
│   └── CacheHelper.ts              # 缓存辅助工具
├── events/                         # 事件相关
│   ├── EventBus.ts                 # 事件总线
│   └── useEventListener.ts         # 事件监听Hook
├── ui/                             # UI服务
│   ├── NotificationService.ts      # 通知服务
│   ├── LoadingService.ts           # 加载服务
│   └── DialogService.ts            # 对话框服务
├── assets/                         # 资产相关
│   ├── UserAssetsService.ts        # 用户资产服务
│   └── TransactionService.ts       # 交易核心
├── utils/                          # 工具服务
│   ├── LoggerService.ts            # 日志服务
│   ├── SessionGuard.ts             # 会话守卫
│   ├── ErrorHandler.ts             # 错误处理
│   └── DeviceDetector.ts           # 设备检测
└── core/                           # 核心服务
    ├── ModuleDependency.ts         # 模块依赖
    ├── LogoutService.ts            # 登出管理
    └── BackgroundEffects.ts        # 背景特效
```

### 2. Firebase服务 (src/services/firebase/)

```
firebase/
├── config.ts                       # Firebase配置
├── FirebaseDataReader.ts           # 数据读取
├── WorldDataService.ts             # 世界数据服务
└── WorldFrameworksService.ts       # 世界框架服务
```

### 3. 特性模块 (src/features/)

```
features/
├── ai-service/                     # AI服务
│   ├── AIService.ts                # AI服务主类
│   └── ResponseHandler.ts          # 响应处理
├── save/                           # 存档系统
│   ├── SaveManager.ts              # 存档管理器
│   ├── CloudSync.ts                # 云同步
│   └── useSaves.ts                 # 存档Hook
├── unlock/                         # 解锁系统
│   ├── UnlockManager.ts            # 解锁管理器
│   ├── UnlockAnimation.tsx         # 解锁动画组件
│   └── useUnlock.ts                # 解锁Hook
├── world-selection/                # 世界选择
│   ├── WorldSelectionService.ts    # 选择服务
│   ├── components/                 # 选择组件
│   │   └── WorldSelectionUI.tsx    # 选择界面
│   └── useWorldSelection.ts        # 世界选择Hook
└── vip-and-package/                # VIP和组合包
    ├── VIPService.ts               # VIP服务
    ├── PackageService.ts           # 包服务
    └── useVIP.ts                   # VIP Hook
```

## 三、业务组件详解

### 1. 主页组件 (src/components/home/)

```
home/
├── MysteriousVoice.tsx             # 神秘声音组件
├── PlayerChoices.tsx               # 玩家选择组件
├── HomeAuthSection.tsx             # 主页认证部分
└── hooks/                          # 主页相关Hooks
    └── useHomeState.ts             # 主页状态Hook
```

### 2. 大厅组件 (src/components/lobby/)

```
lobby/
├── WorldFrameworksPanel.tsx        # 框架面板组件
├── SavesPanel.tsx                  # 存档面板组件
├── UserProfilePanel.tsx            # 个人资料组件
├── SettingsPanel.tsx               # 设置面板组件
├── LobbyAuth.tsx                   # 大厅认证组件
├── hooks/                          # 大厅相关Hooks
│   └── useLobbyState.ts            # 大厅状态Hook
└── config/                         # 配置
    └── saveConfig.ts               # 存档配置
```

### 3. 商店组件 (src/components/shop/)

```
shop/
├── FrameworksPanel.tsx             # 框架面板组件
├── VIPPanel.tsx                    # VIP面板组件
├── PackagesPanel.tsx               # 组合包面板组件
├── OrdersPanel.tsx                 # 订单面板组件
├── PurchaseDialog.tsx              # 购买弹窗组件
├── ShopAuth.tsx                    # 商店认证组件
├── services/                       # 商店服务
│   ├── FrameworksService.ts        # 框架服务
│   ├── PriceService.ts             # 价格服务
│   ├── OrdersService.ts            # 订单服务
│   ├── PurchaseService.ts          # 购买服务
│   └── RefreshService.ts           # 刷新服务
├── hooks/                          # 商店相关Hooks
│   ├── useShopState.ts             # 商店状态Hook
│   └── usePurchase.ts              # 购买Hook
└── context/                        # 商店上下文
    └── ShopContext.tsx             # 商店上下文
```

### 4. 游戏组件 (src/components/game/)

```
game/
├── StoryDisplay.tsx                # 故事显示组件
├── ChoicesPanel.tsx                # 选择面板组件
├── CharacterPanel.tsx              # 角色面板组件
├── BattleSystem.tsx                # 战斗系统组件
├── hooks/                          # 游戏相关Hooks
│   ├── useGameState.ts             # 游戏状态Hook
│   └── useStory.ts                 # 故事Hook
└── utils/                          # 工具
    ├── storyParser.ts              # 故事解析
    └── gameSaver.ts                # 游戏保存
```

## 四、共享类型定义 (src/types/)

```
types/
├── auth.ts                         # 认证相关类型
├── game.ts                         # 游戏相关类型
├── frameworks.ts                   # 框架相关类型
├── shop.ts                         # 商店相关类型
└── save.ts                         # 存档相关类型
```

## 五、数据流与状态管理

### 1. React Context
- `AuthContext` - 认证上下文
- `WorldFrameworksContext` - 世界框架数据上下文
- `UserAssetsContext` - 用户资产上下文
- `SaveContext` - 存档上下文
- `ShopContext` - 商店上下文

### 2. 主要数据流
- 严格通过Context和Props传递数据
- 使用自定义Hooks管理复杂状态和副作用
- Firebase操作通过专用服务类处理
- 共享状态通过Context Provider共享

### 3. 认证流程
- AuthService → UserAssetsService → Firebase → UI更新

### 4. 框架数据流
- FirebaseDataReader → WorldDataService → WorldFrameworksContext → 业务组件

### 5. 购买流程
- PurchaseDialog → PurchaseService → TransactionService → UserAssetsService → UnlockManager → UI更新

### 6. 存档流程
- SaveManager → FirebaseDataReader → CloudSync → UI更新

### 7. AI生成流程
- Game组件 → AIService → ResponseHandler → StoryDisplay组件

## 六、构建与部署

```
/
├── src/                            # 源代码目录
├── public/                         # 静态资源
│   ├── index.html                  # HTML入口
│   └── assets/                     # 静态资源
├── Docs/                           # 文档目录
│   ├── PRD.md                      # 产品需求文档
│   ├── home.prd.md                 # 主页需求
│   ├── lobby.prd.md                # 大厅需求
│   └── shop.prd.md                 # 商店需求
├── .env                            # 环境变量(敏感信息)
├── firebase.json                   # Firebase配置
├── package.json                    # 项目配置
├── tsconfig.json                   # TypeScript配置
└── README.md                       # 项目说明
```

## 七、代码规范与命名约定

### 1. 组件命名
- 组件文件: 大驼峰 `ComponentName.tsx`
- 组件目录: 小驼峰 `featureName/`

### 2. 类型命名
- 接口: `IComponentName`
- 类型: `TComponentName`

### 3. 样式规范
- 使用SCSS模块: `ComponentName.module.scss`
- 使用CSS-in-JS: styled-components

### 4. Hook命名
- 自定义Hook: `use名词动词` (如 `useWorldSelection`)

### 5. 服务命名
- 服务类: `名词Service` (如 `AuthService`)
