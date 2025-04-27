# TypeScript + React 目录各模块职责

## 核心文件

- **src/index.tsx**: 应用入口，负责初始化React应用，配置Firebase，渲染根组件，处理全局错误处理和性能监控。

- **src/App.tsx**: 根组件，管理路由配置，全局Context提供，主题配置，认证状态检查和页面跳转逻辑。

- **src/pages/Game.tsx**: 游戏页面组件，管理游戏主流程、状态更新、玩家交互、战斗系统和自动保存机制。

- **src/contexts/GameContext.tsx**: 游戏状态上下文，提供游戏状态管理，包括玩家属性、历史选择和战斗状态数据。

- **src/services/ai/AIService.ts**: AI服务，负责与后端AI接口通信，处理故事生成请求、响应缓存和失败重试机制。

- **src/services/ai/ResponseHandler.ts**: AI响应处理，解析AI生成的内容并提取选项、战斗触发条件和行为评分。

## 事件系统

- **src/services/core/EventBus.ts**: 事件总线，提供全局统一的事件发布/订阅系统，实现模块间松耦合通信，支持基于优先级的事件监听和处理。

- **src/hooks/useEvent.ts**: 事件钩子，封装事件监听、触发和清理逻辑，简化组件内事件处理。

## 全局状态管理

- **src/contexts/GlobalState.tsx**: 全局状态上下文，提供应用级状态管理，实现各模块间共享数据的存储和访问。

- **src/hooks/useGlobalState.ts**: 全局状态钩子，提供组件级别全局状态访问和更新功能。

- **src/services/state/StateManager.ts**: 状态管理服务，处理复杂状态逻辑，包括状态持久化、变更追踪和调试支持。

## UI组件与Hooks

- **src/components/common/NotificationSystem.tsx**: 通知系统组件，负责显示系统通知、错误提示和操作反馈。

- **src/components/common/LoadingOverlay.tsx**: 加载组件，负责显示加载状态、进度条和加载动画。

- **src/components/common/Dialog.tsx**: 对话框组件，提供各类模态对话框，包括确认、表单和信息展示。

- **src/hooks/useUI.ts**: UI钩子，管理UI状态、主题切换、界面交互逻辑和错误处理。

- **src/components/common/BackgroundEffects.tsx**: 背景特效组件，负责渲染游戏背景动画和视觉效果。

## 用户数据与存储

- **src/services/firebase/config.ts**: Firebase配置，初始化Firebase服务，提供认证、数据库和存储功能。

- **src/services/firebase/useFirestore.ts**: Firestore钩子，提供数据库操作封装，包括读取、写入、查询和监听。

- **src/features/save/SaveManager.ts**: 存档管理器，封装存档操作逻辑，处理游戏存档的创建、读取、删除、云同步功能。

- **src/hooks/useSave.ts**: 存档钩子，提供组件级存档操作，自动保存功能和存档状态管理。

## 页面和路由

- **src/pages/Home.tsx**: 首页组件，处理游戏首页渲染、用户登录状态检测和导航交互，集成神秘声音和玩家选择组件。

- **src/pages/Lobby.tsx**: 大厅页面，负责大厅界面渲染、事件处理和世界选择流程，集成各类大厅功能组件。

- **src/contexts/LobbyContext.tsx**: 大厅上下文，提供大厅状态管理，用户资产数据和框架选择状态。

## 工具函数库

- **src/utils/platform/**: 平台工具，处理不同设备和浏览器环境差异，提供一致性接口。

- **src/utils/templates/**: 模板工具，处理动态模板渲染和内容填充。

- **src/utils/integrations/**: 第三方集成工具，封装外部服务接口调用和数据转换。

- **src/utils/shop/shopUtils.ts**: 商店工具集，提供商店相关辅助函数。

## 类型定义

- **src/types/auth.ts**: 认证相关类型，定义用户、会话和认证流程的接口和类型。

- **src/types/game.ts**: 游戏相关类型，定义游戏状态、玩家属性和游戏流程的接口。

- **src/types/frameworks.ts**: 框架相关类型，定义世界框架、类别和配置的接口。

- **src/types/shop.ts**: 商店相关类型，定义商品、价格和交易的接口和类型。

- **src/types/save.ts**: 存档相关类型，定义存档结构和操作的接口和类型。

## 样式系统

- **src/styles/variables.scss**: 全局样式变量，定义主题颜色、字体和间距等基础样式常量。

- **src/styles/global.scss**: 全局样式，提供应用通用样式规则和重置样式。

- **src/styles/components/**: 组件样式，定义各通用组件的样式模块。

- **src/styles/pages/**: 页面样式，定义各页面特定的样式模块。

- **src/styles/responsive/**: 响应式样式，提供不同设备和分辨率的样式适配规则。

- **src/hooks/useResponsive.ts**: 响应式钩子，提供窗口大小监听和断点检测功能。

## 常量定义

- **src/constants/app.ts**: 应用常量，定义应用级配置项和不变量。

- **src/constants/events.ts**: 事件常量，定义所有事件名称和事件类型。

- **src/constants/api.ts**: API常量，定义API端点和请求配置。

- **src/constants/ui.ts**: UI常量，定义UI相关配置项和默认值。

## 工具与服务

- **src/services/ui/LoadingService.ts**: 加载服务，控制全局加载状态、页面切换动画和资源预加载。

## 服务与功能

- **src/services/cache/CacheManager.ts**: 全局缓存管理系统，提供统一的缓存操作接口，支持分层缓存、签名验证和过期控制。

- **src/services/cache/CacheConfig.ts**: 缓存系统配置定义，包含缓存版本、类型和持续时间等常量配置。

- **src/services/cache/CacheHelper.ts**: 缓存辅助工具，提供缓存签名、版本检查和备份恢复等功能。

- **src/services/cache/CommonDataCache.ts**: 通用数据缓存实现，处理非用户特定的全局数据缓存需求。

- **src/services/cache/UserDataCache.ts**: 用户数据缓存实现，处理与特定用户关联的数据存储和同步。

- **src/services/core/ModuleDependency.ts**: 模块依赖管理器，控制应用模块的加载顺序和依赖注入。

- **src/services/auth/SessionGuard.ts**: 会话安全守卫，确保用户会话唯一性和检测多设备登录。

- **src/services/auth/LogoutService.ts**: 登出服务，处理用户登出流程、数据清理和事件分发。

## Firebase服务

- **src/services/firebase/FirebaseDataReader.ts**: Firebase数据读取统一入口，提供缓存优先的数据访问和错误处理。

- **src/services/firebase/WorldDataService.ts**: 世界数据服务，负责加载、处理和提供世界框架数据。

- **src/services/firebase/UserAssetsService.ts**: 用户资产服务，处理用户金币、钻石等资产的存储、变更和同步。

- **src/services/auth/AuthService.ts**: 认证服务，处理用户登录、注册、会话维护和匿名账户升级。

## 多平台适配

- **src/utils/platform/DeviceDetector.ts**: 设备检测工具，识别用户设备类型和性能参数。

- **src/hooks/useDeviceInfo.ts**: 设备信息钩子，提供组件级设备信息访问和适配功能。

- **src/styles/responsive/breakpoints.scss**: 断点定义，设置响应式布局的尺寸断点。

## 离线同步

- **src/services/sync/NetworkManager.ts**: 网络管理器，监测网络状态变化并触发相应事件。

- **src/services/sync/SyncManager.ts**: 同步管理器，处理在线/离线状态切换和数据同步。

- **src/services/sync/OfflineQueue.ts**: 离线队列，存储离线状态下的操作，在恢复连接时执行。

- **src/hooks/useNetworkStatus.ts**: 网络状态钩子，提供组件级网络状态监测和响应功能。

- **src/hooks/useOfflineSync.ts**: 离线同步钩子，处理组件级离线数据的缓存和同步。

## 错误处理系统

- **src/services/utils/ErrorHandler.ts**: 错误处理器，统一处理和记录应用异常。

- **src/services/utils/LoggerService.ts**: 日志服务，提供分级日志记录和上报功能。

- **src/hooks/useErrorBoundary.ts**: 错误边界钩子，提供组件级错误捕获和恢复功能。

## 商店组件和服务

- **src/features/shop/ShopCore.tsx**: 商店核心组件，提供商店页面的主体结构和状态管理。

- **src/pages/Shop.tsx**: 商店页面，负责商店页面的整体布局和集成各商店子组件。

- **src/components/shop/ShopFrameworks.tsx**: 框架商品组件，负责渲染和管理框架商品展示。

- **src/services/shop/PurchaseService.ts**: 购买服务，处理商品购买流程和状态管理。

- **src/services/shop/TransactionService.ts**: 交易服务，提供原子性交易操作和回滚机制。

- **src/services/shop/OrdersService.ts**: 订单服务，处理订单创建、存储和状态跟踪。

- **src/hooks/useShopAuth.ts**: 商店认证钩子，管理商店内的用户验证和会话检查。

- **src/contexts/ShopContext.tsx**: 商店上下文，提供商店状态和数据共享。

- **src/services/shop/PriceService.ts**: 价格服务，负责加载和提供商品价格信息。

- **src/services/shop/ShopSecurity.ts**: 商店安全服务，处理交易安全验证和异常检测。

- **src/hooks/useShopSync.ts**: 商店同步钩子，处理多标签页和多设备间的数据一致性。

- **src/services/shop/RefreshService.ts**: 数据刷新服务，处理商店数据的定时更新和错误恢复。

- **src/components/shop/ShopButtons.tsx**: 按钮组件，处理商店内各类按钮的渲染和点击事件。

- **src/components/shop/ShopCards.tsx**: 商品卡片组件，展示和管理商品卡片UI。

- **src/components/shop/PremiumUI.tsx**: 高级商品组件，处理VIP会员和高级框架包的展示。

- **src/components/shop/WorldsUI.tsx**: 世界商店组件，处理世界框架的商店展示界面。

- **src/hooks/usePurchaseStatus.ts**: 购买状态钩子，跟踪和通知购买流程状态变化。

## VIP与会员模块

- **src/services/shop/VIPService.ts**: VIP服务，管理VIP会员状态、权益和过期逻辑。

- **src/services/shop/PackageService.ts**: 套餐服务，处理高级框架包的数据和购买逻辑。

- **src/hooks/useVIP.ts**: VIP钩子，提供组件级VIP状态访问和操作功能。

- **src/hooks/usePackage.ts**: 套餐钩子，提供组件级套餐数据访问和操作功能。

## 功能模块

- **src/features/world-selection/**: 世界选择模块，处理游戏世界的选择和配置界面。
  - **WorldSelectionService.ts**: 世界选择服务，负责世界选择流程和用户交互。
  - **components/WorldSelectionUI.tsx**: 世界选择组件，渲染和管理世界选择界面元素。
  - **hooks/useWorldFrameworkSelection.ts**: 框架选择钩子，处理框架数据的选择和过滤。

- **src/features/framework-unlock/**: 框架解锁模块，处理游戏框架的解锁和购买流程。
  - **UnlockManager.ts**: 解锁管理器，协调解锁流程和验证。
  - **components/UnlockAnimation.tsx**: 解锁动画组件，提供框架解锁的视觉效果。
  - **hooks/useUnlock.ts**: 解锁钩子，管理解锁状态和操作。

- **src/features/background-effects/**: 背景特效模块，提供游戏背景的动画和视觉效果。
  - **components/ParticleSystem.tsx**: 粒子系统组件，生成和管理背景粒子效果。
  - **components/BackgroundEffects.tsx**: 背景效果组件，控制多种背景视觉元素。
  - **hooks/useBackgroundEffects.ts**: 背景效果钩子，管理背景效果状态和配置。

- **src/features/tutorial/**: 教程模块，提供游戏新手引导和教程系统。
  - **TutorialManager.ts**: 教程管理器，控制教程流程和进度。
  - **data/TutorialSteps.ts**: 教程步骤定义，包含所有教程内容和触发条件。
  - **components/TutorialUI.tsx**: 教程UI组件，渲染和管理教程提示和高亮元素。
  - **hooks/useTutorial.ts**: 教程钩子，管理教程状态和互动。

- **src/components/home/MysteriousVoice.tsx**: 神秘声音组件，提供游戏内特殊提示和线索系统。

- **src/components/game/PlayerChoices.tsx**: 玩家选择组件，渲染和管理玩家决策的界面和逻辑。

## 配置

- **src/config/app-config.ts**: 应用全局配置，定义环境变量、API端点和功能开关。

## 通用组件

- **src/components/auth/**: 认证组件，包含登录、注册和账户管理界面。
  - **AuthModal.tsx**: 认证模态框，提供登录和注册的用户界面。
  - **LoginForm.tsx**: 登录表单，处理用户登录信息输入和验证。
  - **RegisterForm.tsx**: 注册表单，处理新用户注册信息输入和验证。
  - **AccountUpgradeUI.tsx**: 账户升级界面，处理匿名账户到正式账户的转换。 