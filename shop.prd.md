# 商店模块产品需求文档

## 1. 概述

商店模块是游戏内购买框架、VIP会员、高级组合包的统一入口，全新实现原有商店的所有功能，但使用更现代化的架构和更清晰的代码组织。实现严格遵循MDC规则，包括认证、事件系统、数据管理、UI组件、安全机制等。

## 2. 核心功能模块

### 2.1 商店主页

- 提供框架展示区、VIP会员区、高级组合包区、订单历史四大核心区域
- **默认展示"世界框架"(world类别)** 作为首个展示的框架类型
- 支持根据用户状态（游客/登录/VIP）显示不同内容
- 实现顶部导航栏，包含分类切换功能
- 右侧/顶部显示用户资产（金币、钻石）信息

### 2.2 框架展示与购买

- 展示所有可购买框架，包含名称、价格
- 框架分类支持七种固定类型：**world、era、technology、rules、race、politics、conflict**
- 点击框架显示详情弹窗，包含更多信息和购买按钮
- 购买流程：确认、支付、结果展示
- 已拥有框架显示"已拥有"状态，VIP专属框架为非VIP用户显示VIP专属标记

### 2.3 VIP会员

- 展示VIP会员特权和价格
- 支持购买/续费VIP会员，**固定周期为30天**
- 显示VIP到期时间和状态
- VIP特权：普通世界框架在世界选择界面可通过unlockmanager解锁，有效期内随便使用，商店仍正常提供购买
- VIP购买确认和支付流程

### 2.4 高级组合包

- 展示**固定组合好的高级框架组合包**（非VIP专属）
- 组合包内容包含多个高级框架，不是单个高级框架
- 组合包详情展示，包含所有包含框架
- 组合包购买流程和确认
- 已拥有组合包的展示逻辑

### 2.5 订单历史

- 展示用户历史订单记录
- 包含订单ID、购买内容、时间、价格、状态等信息
- 支持按时间、状态、商品类型筛选
- 订单详情查看功能

### 2.6 购买与交易系统

- 统一的购买确认弹窗
- 支持金币/钻石支付方式
- 交易记录和历史订单
- 购买成功/失败的反馈机制
- 防重复提交和订单验证

### 2.7 资产管理

- 顶部显示用户当前金币和钻石数量
- 资产不足时的提示和充值引导
- 资产变更时的动画效果
- 实时同步和更新资产数据

## 3. 用户界面

### 3.1 整体布局

- 响应式设计，适配各种屏幕尺寸
- 主体内容区域居中，最大宽度限制
- 顶部导航，中间内容区，右侧/顶部资产栏
- 所有UI元素必须位于页面可视区域内，避免超出屏幕

### 3.2 卡片组件

- 统一的卡片设计，类名统一用 shop-card-* 前缀
- 普通框架卡片包含：名称、价格、已拥有/未拥有状态
- 组合包卡片包含：名称、描述、价格、包含框架列表、已拥有/未拥有状态
- 卡片悬停效果和点击动画
- 不同状态（可购买、已拥有、VIP专属）的视觉区分
- 支持批量渲染和虚拟列表技术

### 3.3 弹窗组件

- 详情弹窗，展示更多信息
- 购买确认弹窗，显示价格和支付方式
- 结果反馈弹窗，显示成功或失败
- 统一的关闭按钮和动画效果

### 3.4 导航

- 顶部分类导航，支持在七个固定类型间切换
- 过滤器仅存储当前选中分类，默认为"world"

## 4. 数据结构与管理

### 4.1 数据来源

所有数据必须从Firebase数据库中实时获取，严禁硬编码任何框架、价格或其他数据：

- **数据库位置**：TheStoryBegins集合 > Selection文档
- **数据存储方式**：各类数据以字段数组形式存储，需动态读取，禁止硬编码

#### 4.1.1 普通框架数据来源
- 位置：数据库TheStoryBegins集合 > Selection文档 > 7大框架字段
  - Worlds（世界框架）
  - Era（时代框架）
  - TechnologyLevel（技术框架）
  - CoreRules（规则框架）
  - MainRace（种族框架）
  - PoliticalSystem（政治框架）
  - Conflict（冲突框架）
- 形式：每个字段为数组，包含多个框架数据，与组合包无关

#### 4.1.2 框架价格数据来源
- 位置：数据库TheStoryBegins集合 > Selection文档 > WorldFrameworkPrice字段
- 形式：数组格式，"框架前缀-价格"形式存储（如"Worlds-价格"）
- 解析：使用代码函数解析价格数据，严格按world-data-manager.mdc规则执行

#### 4.1.3 VIP会员数据来源
- 位置：数据库TheStoryBegins集合 > Selection文档 > VIPMemberPrice字段
- 形式：数组格式，下标0为月会员价格（固定30天）
- 备注：后续可能启用数组1作为年会员价格（暂不支持）

#### 4.1.4 组合包数据来源
- 位置：数据库TheStoryBegins集合 > Selection文档 > Package相关字段
  - PackageConflict
  - PackageCoreRules
  - PackageEra
  - PackageMainRace
  - PackagePoliticalSystem
  - PackageTechnologyLevel
  - PackageWorlds
- 形式：每个字段数组0为一个固定组合包的相应框架

#### 4.1.5 组合包价格数据来源
- 位置：数据库TheStoryBegins集合 > Selection文档 > PackagePrice字段
- 形式：数组格式，下标对应组合包编号（数组0对应组合包0，1对应1）

### 4.2 框架数据结构

```
{
  id: string,         // 如 "world_1"
  name: string,       // 显示名称
  category: string,   // "world"、"era"、"technology"等七种固定类型
  type: "normal" | "premium", // 普通/高级
  isVIP: boolean,     // 是否VIP专属
  price: number,      // 价格（通过框架前缀-价格形式从WorldFrameworkPrice解析）
  owned: boolean,     // 是否已拥有
}
```

### 4.3 VIP会员数据结构

```
{
  price: number,      // VIP价格（从VIPMemberPrice字段数组0获取）
  duration: 30,       // 固定30天
  benefits: string[], // 特权描述
  isActive: boolean,  // 是否激活
  expiryDate: string  // ISO日期格式的到期时间
}
```

### 4.4 组合包数据结构

```
{
  id: string,         // 组合包ID
  name: string,       // 组合包名称
  description: string, // 组合包描述（仅组合包需要描述，普通框架不需要）
  price: number,      // 组合包价格（从PackagePrice字段相应数组索引获取）
  frameworks: string[], // 包含的框架ID列表（从Package相关字段获取）
  isOwned: boolean    // 是否已拥有
}
```

### 4.5 用户资产数据结构

```
{
  userId: string,
  coins: number,
  diamonds: number,
  ownedFrameworks: string[], // 拥有的框架ID
  ownedPackages: string[],   // 拥有的组合包ID
  vipStatus: {
    isActive: boolean,
    expiryDate: string      // ISO日期
  },
  lastUpdated: string       // ISO日期
}
```

### 4.6 订单数据结构

```
{
  orderId: string,
  userId: string,
  productId: string,
  productType: string,     // "framework", "vip", "package"
  price: number,
  currency: string,        // "coins", "diamonds"
  status: string,          // "pending", "completed", "failed", "cancelled"
  createdAt: string,       // ISO日期
  updatedAt: string        // ISO日期
}
```

### 4.7 数据获取策略

- 框架数据和价格数据**优先从本地缓存获取**
  - 框架数据通过 `window.WorldFrameworks`（由WorldDataManager从Firebase加载并解析）
  - 价格数据通过 `window.CommonDataCache.getPriceData()`（由价格管理模块从Firebase加载并解析）
- 缓存失效或不存在时，才重新从Firebase数据库拉取
- 所有数据缓存必须遵循CacheManager.mdc规定的统一缓存管理规则
- 缓存相关的配置、过期时间、签名、加密等全部由CacheManager统一处理
- 数据刷新使用指数退避策略，有频率限制
- 严禁任何形式的硬编码数据，所有数据必须从数据库动态获取

## 5. 事件系统

### 5.1 商店核心事件

- `shop.initialized` - 商店初始化完成
- `shop.category.changed` - 分类切换（如从world切换到era）
- `shop.filter-changed` - 过滤条件变更
- `shop-frameworks-data-ready` - 框架数据加载完成
- `shop-price-data-ready` - 价格数据加载完成

### 5.2 产品与交互事件

- `shop.card.clicked` - 卡片点击
- `shop.button.clicked` - 按钮点击
- `shop.product.details.shown` - 产品详情显示
- `shop.world.selected` - 世界框架选中

### 5.3 购买与交易事件

- `shop.purchase.started` - 开始购买流程
- `shop.purchase.confirmed` - 用户确认购买
- `shop.purchase.completed` - 购买完成
- `shop.purchase.failed` - 购买失败
- `shop.order.created` - 订单创建
- `shop.transaction.committed` - 交易提交
- `shop.transaction.rolledback` - 交易回滚

### 5.4 资产与状态事件

- `shop.user.assets.updated` - 用户资产更新
- `shop.assets.insufficient` - 资产不足
- `vip-status-changed` - VIP状态变更
- `frameworks_data_updated` - 框架数据更新

## 6. 交互流程

### 6.1 商店初始化流程

1. 初始化Shop.Core单例，创建全局状态
2. 检查用户认证状态（Shop.Auth）
3. 从Firebase数据库加载框架和价格数据（优先使用缓存）
4. 分类框架数据（七个固定类别）
5. 默认选中"world"类别
6. 渲染UI，显示框架卡片
7. 绑定事件监听
8. 派发`shop.initialized`事件

### 6.2 框架购买流程

1. 用户浏览框架列表（默认展示world类别）
2. 点击框架卡片，派发`shop.card.clicked`事件
3. 系统显示框架详情弹窗
4. 用户点击"购买"按钮
5. 系统验证会话状态和资产余额
6. 显示购买确认弹窗
7. 用户确认购买，派发`shop.purchase.confirmed`事件
8. 创建订单，锁定价格
9. 执行事务（扣减资产、解锁框架、更新订单状态）
10. 事务成功则派发`shop.purchase.completed`，失败则回滚并派发`shop.purchase.failed`
11. 显示购买结果弹窗
12. 更新UI状态和用户资产显示

### 6.3 VIP购买流程

1. 用户点击VIP会员区域
2. 系统显示VIP详情和特权（固定30天周期）
3. 用户点击"购买VIP"按钮
4. 系统验证会话状态和资产余额
5. 显示购买确认弹窗
6. 用户确认购买
7. 创建订单，锁定价格
8. 执行事务（扣减资产、激活VIP、更新订单状态）
9. 事务成功则派发`shop.purchase.completed`，失败则回滚
10. 显示购买结果弹窗
11. 更新UI状态，显示VIP专属内容

### 6.4 数据同步与冲突处理

1. 用户资产或订单变更后，触发同步
2. 优先使用BroadcastChannel同步，不可用时降级为localStorage事件
3. 检测到冲突时，按时间戳取最新，支持三向合并
4. 合并后广播同步完成事件
5. 所有模块响应刷新UI

### 6.5 错误处理流程

1. 资产不足时，显示提示并引导充值
2. 网络错误时，显示重试选项，采用指数退避策略
3. 会话过期时，强制登出并提示重新登录
4. 交易失败时，自动回滚所有变更，确保数据一致性
5. 显示统一错误提示，支持重试

## 7. 安全与性能

### 7.1 安全措施

- 所有交易必须在服务端验证
- 会话状态定期校验，关键操作前实时验证
- 敏感数据加密存储，添加签名和时间戳
- 用户切换、登出时彻底清理所有相关缓存和状态
- 资产变更必须有详细日志和事务保障

### 7.2 性能优化

- 使用DocumentFragment减少DOM操作，降低重排重绘
- 应用虚拟列表技术，只渲染可视区域的卡片
- 本地缓存频繁访问的数据，减少网络请求
- 检测设备性能，低端设备自动降级动画效果

## 8. 样式与组件规范

- 所有UI组件命名和类名使用功能性前缀（shop-card-*、shop-btn-*等）
- 所有样式文件集中在public/styles/目录，按页面和组件分类
- 所有风格、主题、颜色、字体等变量集中在variables.css
- 组件化开发，每个UI/功能块单独文件
- 响应式设计，适配从320px到2560px的屏幕宽度 
