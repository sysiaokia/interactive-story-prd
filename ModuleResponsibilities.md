# public/js 目录各模块职责

## 核心文件

- **index.js**: 应用入口，负责初始化核心组件，加载游戏，处理页面生命周期和全局错误处理。

- **game.js**: 游戏核心逻辑，管理游戏主流程、状态更新、玩家交互、战斗系统和自动保存机制。

- **GameState.js**: 游戏状态管理，负责存储和更新游戏进度、玩家属性、历史选择和战斗状态数据。

- **AIService.js**: AI服务，负责与后端AI接口通信，处理故事生成请求、响应缓存和失败重试机制。

- **ResponseHandler.js**: AI响应处理，解析AI生成的内容并提取选项、战斗触发条件和行为评分。

## 用户界面

- **UIManager.js**: UI核心管理，负责创建、显示和隐藏UI组件，处理UI事件绑定和通知系统。

- **templates.js**: UI模板系统，管理游戏中各类对话框、设置、帮助和游戏界面模板。

- **background.js**: 全局背景特效，管理游戏背景动画、过渡效果和性能优化。

## 用户数据与存储

- **firebase-config.js**: Firebase服务配置与用户认证，管理用户会话、数据同步和错误处理。

- **SaveManager.js**: 存档系统，处理游戏存档的创建、读取、删除、云同步和自动保存功能。

## 大厅与世界系统

- **home.js**: 首页管理，处理游戏首页初始化、用户登录状态检测和主界面交互。

- **lobby.js**: 大厅入口，负责大厅界面初始化、事件绑定和状态管理。

- **LobbyManager.js**: 大厅核心系统，管理世界选择、用户资产、跨页同步和多设备同步机制。

## 工具与辅助系统

- **loading-manager.js**: 加载管理器，控制游戏加载流程、过渡动画和资源预加载。

## 目录结构

- **core/**: 核心系统组件，包含基础框架和通用功能模块。

- **firebase/**: Firebase相关模块，包括数据读取、写入和用户认证组件。

- **shopjs/**: 商店系统，管理游戏内物品购买、货币和解锁功能。

- **modules/**: 功能模块集合，包含各类独立功能组件。

- **config/**: 配置文件，存储游戏常量、环境变量和功能开关。

- **components/**: UI组件库，包含可复用的界面元素和交互组件。 

## 子目录文件职责

### core/ 目录

- **cache-manager.js**: 全局缓存管理系统，提供统一的缓存操作接口，支持分层缓存、签名验证和过期控制。

- **cache-init.js**: 缓存系统初始化模块，负责在应用启动时配置和准备缓存系统。

- **cache-config.js**: 缓存系统配置定义，包含缓存版本、类型和持续时间等常量配置。

- **cache-helper.js**: 缓存辅助工具，提供缓存签名、版本检查和备份恢复等功能。

- **common-data-cache.js**: 通用数据缓存实现，处理非用户特定的全局数据缓存需求。

- **user-data-cache.js**: 用户数据缓存实现，处理与特定用户关联的数据存储和同步。

- **module-dependency.js**: 模块依赖管理器，控制应用模块的加载顺序和依赖注入。

- **session-guard.js**: 会话安全守卫，确保用户会话唯一性和检测多设备登录。

- **LogoutManager.js**: 登出管理器，处理用户登出流程、数据清理和事件分发。

### firebase/ 目录

- **FirebaseDataReader.js**: Firebase数据读取统一入口，提供缓存优先的数据访问和错误处理。

- **WorldDataManager.js**: 世界数据管理器，负责加载、处理和提供世界框架数据。

- **UserAssetsManager.js**: 用户资产管理器，处理用户金币、钻石等资产的存储、变更和同步。

- **auth.js**: 认证模块，处理用户登录、注册、会话维护和匿名账户升级。

### shopjs/ 目录

- **shop-core.js**: 商店核心模块，提供商店初始化和状态管理功能。

- **shop-main.js**: 商店入口文件，负责启动商店并集成各个子模块。

- **shop-ui.js**: 商店UI管理器，负责创建和控制商店界面元素。

- **shop-frameworks.js**: 框架商品管理器，处理框架数据的加载和显示。

- **shop-purchase.js**: 购买流程管理器，处理商品购买事务和状态管理。

- **shop-transaction-core.js**: 交易核心系统，提供原子性交易操作和回滚机制。

- **shop-orders.js**: 订单管理系统，处理订单创建、存储和状态跟踪。

- **shop-auth.js**: 商店认证模块，管理商店内的用户验证和会话检查。

- **shop-events.js**: 商店事件系统，定义商店相关的事件类型和触发机制。

- **shop-events-listeners.js**: 商店事件监听器，注册和处理商店事件回调。

- **shop-price.js**: 价格数据管理器，负责加载和提供商品价格信息。

- **shop-security.js**: 商店安全模块，处理交易安全验证和异常检测。

- **shop-sync.js**: 商店数据同步器，处理多标签页和多设备间的数据一致性。

- **shop-utils.js**: 商店工具集，提供通用辅助功能和工具方法。

- **shop-refresh.js**: 数据刷新管理器，处理商店数据的定时更新和错误恢复。

- **shop-buttons.js**: 按钮行为管理器，处理商店内按钮的事件和交互逻辑。

- **shop-cards.js**: 商品卡片组件，显示和管理商品卡片UI。

- **shop-premium-ui.js**: 高级商品UI管理器，处理VIP会员和高级框架包的展示。

- **shop-worlds-ui.js**: 世界商店UI管理器，处理世界框架的商店展示界面。

- **purchase-status-manager.js**: 购买状态管理器，跟踪和通知购买流程状态变化。

### modules/ 目录

- **world-selection/**: 世界选择模块，处理游戏世界的选择和配置界面。
  - **WorldSelectionManager.js**: 世界选择管理器，负责世界选择流程和用户交互。
  - **WorldSelectionUI.js**: 世界选择UI，绘制和管理世界选择界面元素。
  - **WorldFrameworkSelector.js**: 框架选择器，处理框架数据的选择和过滤。

- **framework-unlock/**: 框架解锁模块，处理游戏框架的解锁和购买流程。
  - **UnlockManager.js**: 解锁管理器，协调解锁流程和验证。
  - **UnlockAnimation.js**: 解锁动画，提供框架解锁的视觉效果。

- **background-effects/**: 背景特效模块，提供游戏背景的动画和视觉效果。
  - **ParticleSystem.js**: 粒子系统，生成和管理背景粒子效果。
  - **BackgroundEffects.js**: 背景效果管理器，控制多种背景视觉元素。

- **tutorial/**: 教程模块，提供游戏新手引导和教程系统。
  - **TutorialManager.js**: 教程管理器，控制教程流程和进度。
  - **TutorialSteps.js**: 教程步骤定义，包含所有教程内容和触发条件。
  - **TutorialUI.js**: 教程UI，绘制和管理教程提示和高亮元素。

- **mysterious-voice.js**: 神秘声音模块，提供游戏内特殊提示和线索系统。

- **player-choices.js**: 玩家选择系统，记录和影响玩家决策的历史和结果。

### config/ 目录

- **app-config.js**: 应用全局配置，定义环境变量、API端点和功能开关。

### components/ 目录

- **Auth/**: 认证UI组件，包含登录、注册和账户管理界面。
  - **AuthModal.js**: 认证模态框，提供登录和注册的用户界面。
  - **LoginForm.js**: 登录表单，处理用户登录信息输入和验证。
  - **RegisterForm.js**: 注册表单，处理新用户注册信息输入和验证。
  - **AccountUpgradeUI.js**: 账户升级界面，处理匿名账户到正式账户的转换。 
