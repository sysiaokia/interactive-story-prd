# YAML Front Matter 模板集合

以下是所有 `.mdc` 文件应使用的 YAML Front Matter 格式模板：

## 1. vip-and-package.mdc

```yaml
---
description: VIP会员与高级框架包（package）规则，约束VIP会员权限、package定义、数据结构、数据库读取、WorldDataManager统一解析、权限边界、事件、UI等，适用于所有商店相关模块。
globs: src/services/shop/VIPService.ts, src/services/shop/PackageService.ts, src/hooks/useVIP.ts, src/hooks/usePackage.ts
---
```

## 2. background-effects.mdc

```yaml
---
description: 背景特效模块管理全局背景动画，通过BackgroundEffectsModule单例进行统一管理。采用组件化设计，将主模块与具体特效分离，职责清晰。所有动画基于requestAnimationFrame实现，自动适配设备性能，低端设备自动降级。支持响应式布局和多端适配，特效实例可自动销毁和清理以防止内存泄漏。
globs: src/features/background-effects/BackgroundEffectsModule.ts, src/components/background-effects/BackgroundEffect.tsx, src/hooks/useBackgroundEffects.ts
---
```

## 3. world-selection.mdc

```yaml
---
description: 世界选择模块管理规则，约束初始化流程、全局状态、数据加载、缓存策略、事件通信、UI交互、锁定/解锁规则和错误处理，确保世界选择模块功能完整、一致和解耦。
globs: src/features/world-selection/WorldSelectionManager.ts, src/features/world-selection/WorldFrameworkSelector.ts, src/hooks/useWorldSelection.ts
---
```

## 4. world-data-manager.mdc

```yaml
---
description: 世界数据管理规则，约束框架数据加载、处理、分类、缓存等功能，确保数据一致性和高效访问，适用于所有世界数据管理相关模块。
globs: src/services/firebase/WorldDataManager.ts, src/hooks/useWorldData.ts, src/services/firebase/worldDataServices.ts
---
```

## 5. WorldFrameworks.mdc

```yaml
---
description: WorldFrameworks模块负责全局框架数据的加载、分类、存储和基础查询，作为系统的唯一数据来源，所有模块通过该服务获取框架数据。
globs: src/services/firebase/WorldFrameworksService.ts, src/hooks/useWorldFrameworks.ts, src/contexts/WorldFrameworksContext.tsx
---
```

## 6. world-selection-ui.mdc

```yaml
---
description: 世界选择界面UI规则，约束界面结构、组件命名、交互事件、全局状态、与业务解耦、事件驱动、错误与通知、适配与降级等，适用于世界选择UI相关模块。
globs: src/features/world-selection/components/*, src/features/world-selection/hooks/*.ts
---
```

## 7. unlock-manager.mdc

```yaml
---
description: 解锁管理器规则，约束框架解锁流程、购买事务、数据同步、验证、回滚、事件分发等，适用于所有框架解锁相关模块。
globs: src/features/framework-unlock/UnlockManager.ts, src/services/assets/UnlockService.ts, src/hooks/useUnlock.ts
---
```

## 8. unlock-animation.mdc

```yaml
---
description: 解锁动画规则，约束框架解锁动画的预加载、播放、显示、隐藏、音效、性能优化等，适用于所有解锁动画相关模块。
globs: src/features/framework-unlock/components/UnlockAnimation.tsx, src/hooks/useUnlockAnimation.ts
---
```

## 9. TransactionCore.mdc

```yaml
---
description: 全局交易核心规则，约束所有资产变更、订单创建、购买状态管理、事务原子性保证和回滚机制，作为全局唯一的交易入口，统一管理各类购买流程的状态和生命周期。
globs: src/services/shop/TransactionCore.ts, src/services/shop/TransactionService.ts, src/hooks/useTransaction.ts, src/services/core/transactions/*.ts
---
```

## 10. third-party-integration.mdc

```yaml
---
description: 第三方集成规则，约束外部服务接入流程、API调用、数据转换、错误处理、状态同步等，确保系统与外部服务的安全稳定交互。
globs: src/services/integrations/*.ts, src/hooks/useThirdParty*.ts, src/utils/integrations/*.ts
---
```

## 11. shop-utils.mdc

```yaml
---
description: 商店通用工具规则，约束通用工具、辅助函数、兼容处理、事件等，适用于所有商店工具相关模块。
globs: src/utils/shop/*.ts, src/services/shop/utils/*.ts
---
```

## 12. shop-auth.mdc

```yaml
---
description: 商店业务认证规则，约束商店内用户认证、会话检测、资产初始化、VIP同步、事件监听、缓存恢复等，适用于所有商店认证相关模块。
globs: src/services/shop/ShopAuthService.ts, src/hooks/useShopAuth.ts
---
```

## 13. shop-core.mdc

```yaml
---
description: 商店主流程与入口规则，约束主流程初始化、全局状态、事件注册、模块加载、清理等，适用于所有商店主流程相关模块。
globs: src/services/shop/ShopCoreService.ts, src/services/shop/ShopMainService.ts, src/contexts/ShopContext.tsx
---
```

## 14. shop-events.mdc

```yaml
---
description: 商店事件系统的详细规则，约束事件注册、触发、命名、优先级、解耦、通信、监听、错误处理等。
globs: src/services/shop/ShopEventBus.ts, src/hooks/useShopEvents.ts
---
```

## 15. shop-refresh.mdc

```yaml
---
description: 商店数据刷新规则，约束数据刷新、重试、异常恢复、指数退避、统一错误提示等，适用于所有商店数据刷新相关模块。
globs: src/services/shop/RefreshService.ts, src/hooks/useDataRefresh.ts
---
```

## 16. shop-frameworks.mdc

```yaml
---
description: 商店框架模块负责商店内框架数据的展示、过滤、状态管理和购买交互，从window.WorldFrameworks获取数据并处理商店特有的业务逻辑。
globs: src/features/shop/ShopFrameworksService.ts, src/components/shop/FrameworksList.tsx, src/hooks/useShopFrameworks.ts
---
```

## 17. shop-orders.mdc

```yaml
---
description: 商店订单管理规则，约束订单结构、分片存储、同步、回滚、事件、日志等，适用于所有订单相关模块。
globs: src/services/shop/OrdersService.ts, src/hooks/useOrders.ts
---
```

## 18. shop-price.mdc

```yaml
---
description: 商店价格数据的加载、缓存、校验、解析、锁定与使用规则，约束价格数据的来源、结构、接口、事件等。
globs: src/services/shop/PriceService.ts, src/hooks/usePrices.ts
---
```

## 19. shop-purchase.mdc

```yaml
---
description: 商店购买流程、校验、事务、订单、事件、回滚、日志等详细规则，约束购买相关的所有实现细节。
globs: src/services/shop/PurchaseService.ts, src/hooks/usePurchase.ts
---
```

## 20. shop-ui.mdc

```yaml
---
description: 商店UI与组件规则，约束UI风格、布局、组件、交互、动画、事件、降级、适配、可视区域等，适用于所有商店UI相关模块。
globs: src/components/shop/*.tsx, src/features/shop/components/*.tsx
---
```

## 21. UserAssetsManager.mdc

```yaml
---
description: 用户资产（金币、钻石等）管理的详细规则，约束资产数据结构、变更、缓存、同步、事件、校验等，确保游戏内所有虚拟资产的一致性、安全性和可追溯性。
globs: src/services/assets/UserAssetsManager.ts, src/hooks/useAssets.ts
---
```

## 22. loading-manager.mdc

```yaml
---
description: 全局加载管理与页面跳转加载规则，约束加载界面、页面跳转、加载动画、状态管理、配置、事件分发等，适用于所有加载相关模块。
globs: src/services/ui/LoadingManager.ts, src/components/common/LoadingOverlay.tsx
---
```

## 23. auth.mdc

```yaml
---
description: 认证与会话管理规则，约束认证流程、会话检测、初始资产、匿名登录、登出、事件分发、缓存清理等，适用于所有认证相关模块。
globs: src/services/auth/AuthService.ts, src/hooks/useAuth.ts
---
```

## 24. auth-ui.mdc

```yaml
---
description: 认证与升级UI及流程规则，约束匿名账号升级、认证模态框、登录/注册表单等认证相关UI组件的行为、交互、数据一致性、事件分发等，适用于所有认证UI相关模块。
globs: src/components/auth/*.tsx
---
```

## 25. ai-service.mdc

```yaml
---
description: AI服务与响应处理规则，约束AI请求、重试、缓存、超时、提示词构建、响应解析、事件分发、降级处理等，适用于所有AI服务与响应处理相关模块。
globs: src/services/ai/*.ts, src/hooks/useAI.ts
---
```

## 26. CacheManager.mdc

```yaml
---
description: 全局缓存与数据缓存规则，适用于src/services/cache/相关模块。主要覆盖CacheManager（缓存管理器）、CacheConfig（缓存配置）、CacheHelper（缓存辅助工具）、CommonDataCache（通用数据缓存）、UserDataCache（用户数据缓存）等，约束缓存分层、加密、签名、过期、清理、降级、分片、配置、初始化、异步调用等所有缓存相关功能。
globs: src/services/cache/*.ts, src/hooks/useCache.ts
---
```

## 27. event-bus.mdc

```yaml
---
description: 事件总线模块提供全局统一的事件发布/订阅系统，实现模块间松耦合通信。支持基于优先级的事件监听和处理，确保关键监听器优先执行。具有事件分组管理、防抖节流功能，内置错误隔离机制确保单个监听器异常不影响整个事件流。事件命名必须使用命名空间格式：{模块}.{子模块}.{动作}，如auth.session.created。包含完整的事件生命周期钩子和异步事件处理能力。
globs: src/services/core/EventBus.ts, src/hooks/useEvent.ts
---
```

## 28. firebase-config.mdc

```yaml
---
description: Firebase配置与会话/数据管理规则，约束Firebase初始化、认证、会话检测、用户数据、存档、网络异常、清理、事件分发等，适用于所有Firebase相关模块。
globs: src/services/firebase/config.ts, src/services/firebase/FirebaseManager.ts
---
```

## 29. firebase-data-reader.mdc

```yaml
---
description: Firebase数据读取规则，约束数据读取统一入口、缓存优先、会话校验、错误处理、数据结构、事件广播等，适用于所有Firebase数据读取相关模块。
globs: src/services/firebase/FirebaseDataReader.ts, src/hooks/useFirebaseData.ts
---
```

## 30. game.mdc

```yaml
---
description: 游戏主流程与状态管理规则，约束游戏初始化、主流程、状态管理、AI服务、存档、UI集成、事件驱动、自动保存、异常处理等，适用于所有游戏相关模块。
globs: src/pages/Game.tsx, src/contexts/GameContext.tsx, src/hooks/useGame.ts
---
```

## 31. global-state-management.mdc

```yaml
---
description: 全局状态管理架构规范，约束状态管理分层结构、状态不可变性、选择性订阅、状态持久化、变更追踪、调试工具等，提供React集成方案。
globs: src/contexts/*.tsx, src/hooks/useGlobalState.ts, src/services/state/*.ts
---
```

## 32. home.mdc

```yaml
---
description: 首页与入口初始化规则，约束首页（home）和应用入口（index）初始化流程、UI结构、认证与会话检测、全局状态、事件驱动、缓存清理、错误处理等，适用于所有首页相关模块。
globs: src/pages/Home.tsx, src/index.tsx
---
```

## 33. home-ui.mdc

```yaml
---
description: 主页UI与组件规范，约束主页布局、分区、交互、样式、动画、错误处理等，确保主页风格统一、交互一致、功能完整，适用于所有主页UI相关模块。
globs: src/components/home/*.tsx
---
```

## 34. lobby.mdc

```yaml
---
description: 大厅主流程与UI规则，约束大厅初始化、UI、事件、世界框架加载、同步、资产、登出、错误处理、命名、数据流、缓存、会话检测等，适用于所有大厅相关模块。
globs: src/pages/Lobby.tsx, src/contexts/LobbyContext.tsx
---
```

## 35. lobby-ui.mdc

```yaml
---
description: 大厅UI结构与组件规则，约束大厅分区、布局、命名、样式、子模块、错误与空状态、伪代码等，适用于所有大厅UI相关模块。
globs: src/components/lobby/*.tsx
---
```

## 36. logout-manager.mdc

```yaml
---
description: 登出与数据清理规则，约束登出流程、数据清理、事件分发、匿名用户特殊处理等，适用于所有登出相关模块。
globs: src/services/auth/LogoutService.ts, src/hooks/useLogout.ts
---
```

## 37. module-dependency.mdc

```yaml
---
description: 模块依赖与加载顺序规则，约束模块注册、依赖声明、异步加载、全局唯一性、版本管理与错误恢复机制，适用于所有模块依赖管理相关代码。
globs: src/services/core/ModuleDependency.ts, src/services/core/ModuleLoader.ts
---
```

## 38. multi-platform-adaption.mdc

```yaml
---
description: 多平台适配规范，约束响应式设计、布局结构、断点设计、UI组件适配、性能优化、触摸与输入适配、测试验证等，确保应用在各类设备与平台上的一致体验和功能完整性。
globs: src/styles/responsive/*.scss, src/hooks/useResponsive.ts, src/utils/platform/*.ts
---
```

## 39. purchase-dialog.mdc

```yaml
---
description: 购买对话框规则，约束购买弹窗的显示、隐藏、结果展示、确认流程、错误处理、动画效果等，适用于所有购买弹窗相关模块。
globs: src/components/shop/PurchaseDialog.tsx, src/hooks/usePurchaseDialog.ts
---
```

## 40. save-manager.mdc

```yaml
---
description: 存档管理规则，约束存档的保存、加载、删除、云同步、事件分发、索引、自动保存、导入导出等，适用于所有存档相关模块。
globs: src/features/save/SaveManager.ts, src/hooks/useSave.ts
---
```

## 41. session-guard.mdc

```yaml
---
description: 会话唯一性与设备标识规则，约束全局唯一会话检测、deviceId生成、页面锁定等，适用于所有会话安全相关模块。
globs: src/services/auth/SessionGuard.ts, src/hooks/useSession.ts
---
```

## 42. styles.mdc

```yaml
---
description: 全局样式与风格规范，约束CSS变量管理、文件组织、命名规范、样式引用策略、响应式设计、性能优化与适配降级。提供完整的UI风格指南，确保所有模块在视觉和交互上保持一致性，同时支持多设备和分辨率适配。
globs: src/styles/**/*.scss, src/styles/**/*.css
---
```

## 43. templates.mdc

```yaml
---
description: 游戏模板管理规则，约束所有对话框、设置、帮助、大厅、世界选择等UI模板的结构、命名、复用、动态渲染，适用于所有模板相关模块。
globs: src/components/templates/*.tsx, src/utils/templates/*.ts
---
```

## 44. cursorrules.mdc

```yaml
---
description: 项目核心定律（不可变规则），适用于整个项目所有模块。主要覆盖认证、用户、资产、解锁、存档、AI、事件、样式、缓存等所有基础模块，约束数据一致性、模块边界、命名规范、目录结构、安全验证、缓存同步、事件通信、UI交互、错误处理等全局开发与审核规则。
globs: src/**/*.ts, src/**/*.tsx
---
```

## 45. offline-sync.mdc

```yaml
---
description: 离线模式与数据同步策略规则，约束网络状态检测、离线数据管理、操作队列、数据冲突解决、多设备同步等，确保应用在各种网络环境下的可用性和数据一致性。
globs: src/services/sync/NetworkManager.ts, src/services/sync/SyncManager.ts, src/services/sync/OfflineQueue.ts, src/hooks/useNetworkStatus.ts, src/hooks/useOfflineSync.ts
---
```

## 46. error-handling.mdc

```yaml
---
description: 错误处理与日志系统规则，约束全局错误捕获、错误分类、错误降级策略、错误重试机制、错误上报、日志记录与分级、组件级错误边界等，确保应用在异常情况下的稳定性和用户体验连贯性。
globs: src/services/utils/ErrorHandler.ts, src/services/utils/LoggerService.ts, src/hooks/useErrorBoundary.ts, src/components/common/ErrorBoundary.tsx
---
``` 