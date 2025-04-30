# 商店模块产品需求文档 - TypeScript + React 版本

## 1. 概述

商店模块是游戏内购买框架、VIP会员、高级组合包的统一入口，使用TypeScript + React + Firebase技术栈实现所有功能，采用组件化、类型安全和响应式设计架构。实现严格遵循MDC规则，包括认证、状态管理、数据管理、UI组件、安全机制等。

## 2. 核心功能模块

### 2.1 商店主页

- 提供框架展示区、VIP会员区、高级组合包区、订单历史四大核心区域
- **默认展示"世界框架"(world类别)** 作为首个展示的框架类型
- 支持根据用户状态（游客/登录/VIP）显示不同内容
- 实现顶部导航栏，包含分类切换功能
- 右侧/顶部显示用户资产（金币、钻石）信息
- 使用React Context提供全局状态管理

### 2.2 框架展示与购买

- 展示所有可购买框架，包含名称、价格
- 框架分类支持七种固定类型：**world、era、technology、rules、race、politics、conflict**
- 点击框架显示详情弹窗，包含更多信息和购买按钮
- 购买流程：确认、支付、结果展示
- 已拥有框架显示"已拥有"状态，VIP专属框架为非VIP用户显示VIP专属标记
- 使用TypeScript接口定义框架数据结构

### 2.3 VIP会员

- 展示VIP会员特权和价格
- 支持购买/续费VIP会员，**固定周期为30天**
- 显示VIP到期时间和状态
- VIP特权：普通世界框架在世界选择界面可通过unlockmanager解锁，有效期内随便使用，商店仍正常提供购买
- VIP购买确认和支付流程
- 使用Firebase Authentication和Firestore管理VIP状态

### 2.4 高级组合包

- 展示**固定组合好的高级框架组合包**（非VIP专属）
- 组合包内容包含多个高级框架，不是单个高级框架
- 组合包详情展示，包含所有包含框架
- 组合包购买流程和确认
- 已拥有组合包的展示逻辑
- 使用TypeScript接口定义组合包数据结构

### 2.5 订单历史

- 展示用户历史订单记录
- 包含订单ID、购买内容、时间、价格、状态等信息
- 支持按时间、状态、商品类型筛选
- 订单详情查看功能
- 使用虚拟滚动优化长列表性能

### 2.6 购买与交易系统

- 统一的购买确认弹窗组件
- 支持金币/钻石支付方式
- 交易记录和历史订单
- 购买成功/失败的反馈机制
- 防重复提交和订单验证
- 使用Firebase事务确保交易原子性

### 2.7 资产管理

- 顶部显示用户当前金币和钻石数量
- 资产不足时的提示和充值引导
- 资产变更时的动画效果
- 实时同步和更新资产数据
- 使用React Context管理资产状态

## 3. 用户界面

### 3.1 整体布局

- 响应式设计，使用SCSS预处理器结合Grid和Flexbox，遵循BEM命名规范，适配各种屏幕尺寸
- 主体内容区域居中，最大宽度限制
- 顶部导航，中间内容区，右侧/顶部资产栏
- 所有UI元素必须位于页面可视区域内，避免超出屏幕
- 采用SCSS模块化组织，确保组件样式隔离，避免全局污染

### 3.2 卡片组件

- 使用React函数组件实现卡片设计(`<ShopCard>`)
- 普通框架卡片包含：名称、价格、已拥有/未拥有状态
- 组合包卡片包含：名称、描述、价格、包含框架列表、已拥有/未拥有状态
- 卡片悬停效果和点击动画
- 不同状态（可购买、已拥有、VIP专属）的视觉区分
- 支持批量渲染和虚拟列表技术(react-virtualized)
- 使用TypeScript接口定义卡片Props

### 3.3 弹窗组件

- 使用React Portal实现弹窗组件(`<ShopDialog>`)
- 详情弹窗，展示更多信息
- 购买确认弹窗，显示价格和支付方式
- 结果反馈弹窗，显示成功或失败
- 统一的关闭按钮和动画效果
- 使用useDialog钩子管理弹窗状态

### 3.4 导航

- 顶部分类导航，使用React Tab组件实现类型切换
- 使用React state管理当前选中分类，默认为"world"
- 使用TypeScript联合类型定义固定分类选项

## 4. 数据结构与管理

### 4.1 数据来源

所有数据必须从Firebase数据库中实时获取，严禁硬编码任何框架、价格或其他数据：

- **数据库位置**：TheStoryBegins集合 > Selection文档
- **数据存储方式**：各类数据以字段数组形式存储，需动态读取，禁止硬编码
- **数据访问方式**：使用自定义React钩子封装所有数据操作

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
- 访问方法：使用useFrameworks钩子获取数据

#### 4.1.2 框架价格数据来源
- 位置：数据库TheStoryBegins集合 > Selection文档 > WorldFrameworkPrice字段
- 形式：数组格式，"框架前缀-价格"形式存储（如"Worlds-价格"）
- 解析：使用usePrices钩子解析价格数据，严格按world-data-manager.mdc规则执行

#### 4.1.3 VIP会员数据来源
- 位置：数据库TheStoryBegins集合 > Selection文档 > VIPMemberPrice字段
- 形式：数组格式，下标0为月会员价格（固定30天）
- 备注：后续可能启用数组1作为年会员价格（暂不支持）
- 访问方法：使用useVIPInfo钩子获取VIP数据

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
- 访问方法：使用usePackages钩子获取组合包数据

#### 4.1.5 组合包价格数据来源
- 位置：数据库TheStoryBegins集合 > Selection文档 > PackagePrice字段
- 形式：数组格式，下标对应组合包编号（数组0对应组合包0，1对应1）
- 访问方法：与usePackages钩子集成

### 4.2 框架数据结构

```typescript
interface IFramework {
  id: string;         // 如 "world_1"
  name: string;       // 显示名称
  category: FrameworkCategory;   // "world"、"era"、"technology"等七种固定类型
  type: "normal" | "premium"; // 普通/高级
  isVIP: boolean;     // 是否VIP专属
  price: number;      // 价格（通过框架前缀-价格形式从WorldFrameworkPrice解析）
  owned: boolean;     // 是否已拥有
}

// 框架类别类型
type FrameworkCategory = "world" | "era" | "technology" | "rules" | "race" | "politics" | "conflict";
```

### 4.3 VIP会员数据结构

```typescript
interface IVIP {
  price: number;      // VIP价格（从VIPMemberPrice字段数组0获取）
  duration: 30;       // 固定30天
  benefits: string[]; // 特权描述
  isActive: boolean;  // 是否激活
  expiryDate: string; // ISO日期格式的到期时间
}
```

### 4.4 组合包数据结构

```typescript
interface IPackage {
  id: string;         // 组合包ID
  name: string;       // 组合包名称
  description: string; // 组合包描述（仅组合包需要描述，普通框架不需要）
  price: number;      // 组合包价格（从PackagePrice字段相应数组索引获取）
  frameworks: string[]; // 包含的框架ID列表（从Package相关字段获取）
  isOwned: boolean;   // 是否已拥有
}
```

### 4.5 用户资产数据结构

```typescript
interface IUserAssets {
  userId: string;
  coins: number;
  diamonds: number;
  ownedFrameworks: string[]; // 拥有的框架ID
  ownedPackages: string[];   // 拥有的组合包ID
  vipStatus: {
    isActive: boolean;
    expiryDate: string;      // ISO日期
  };
  lastUpdated: string;       // ISO日期
}
```

### 4.6 订单数据结构

```typescript
interface IOrder {
  orderId: string;
  userId: string;
  productId: string;
  productType: "framework" | "vip" | "package";
  price: number;
  currency: "coins" | "diamonds";
  status: "pending" | "completed" | "failed" | "cancelled";
  createdAt: string;       // ISO日期
  updatedAt: string;       // ISO日期
}
```

### 4.7 数据获取策略

- 框架数据和价格数据**优先从本地缓存获取**
  - 框架数据通过 `useFrameworks()` 钩子获取
  - 价格数据通过 `usePrices()` 钩子获取
- 缓存失效或不存在时，才重新从Firebase数据库拉取
- 所有数据缓存必须遵循CacheManager.mdc规定的统一缓存管理规则
- 缓存相关的配置、过期时间、签名、加密等全部由CacheManager统一处理
- 数据刷新使用指数退避策略，有频率限制
- 严禁任何形式的硬编码数据，所有数据必须从数据库动态获取

## 5. 主要流程示例

### 5.1 商店初始化流程

```tsx
// 商店页面组件
const Shop: React.FC = () => {
  // 认证状态
  const { user, loading: authLoading } = useAuth();
  
  // 框架数据
  const { frameworks, loading: frameworksLoading, error: frameworksError } = useFrameworks();
  
  // 包数据
  const { packages, loading: packagesLoading, error: packagesError } = usePackages();
  
  // VIP数据
  const { vipInfo, loading: vipLoading, error: vipError } = useVIPInfo();
  
  // 用户资产
  const { assets, loading: assetsLoading } = useUserAssets(user?.uid);
  
  // 加载状态
  const isLoading = authLoading || frameworksLoading || packagesLoading || vipLoading || assetsLoading;
  
  // 选中分类
  const [selectedCategory, setSelectedCategory] = useState<FrameworkCategory>("world");
  
  // 处理分类切换
  const handleCategoryChange = (category: FrameworkCategory) => {
    setSelectedCategory(category);
  };
  
  // 页面加载中
  if (isLoading) {
    return <LoadingScreen />;
  }
  
  // 错误处理
  if (frameworksError || packagesError || vipError) {
    return <ErrorScreen error={frameworksError || packagesError || vipError} />;
  }
  
  return (
    <div className={styles.shopContainer}>
      <ShopHeader assets={assets} />
      <CategoryTabs 
        selectedCategory={selectedCategory} 
        onCategoryChange={handleCategoryChange} 
      />
      <div className={styles.mainContent}>
        <FrameworksPanel 
          frameworks={frameworks.filter(f => f.category === selectedCategory)} 
        />
        <VIPPanel vipInfo={vipInfo} userVIPStatus={assets?.vipStatus} />
        <PackagesPanel packages={packages} />
      </div>
      <NotificationSystem />
    </div>
  );
};
```

### 5.2 购买流程

```tsx
// 在FrameworkPanel组件中
const FrameworkPanel: React.FC<FrameworkPanelProps> = ({ frameworks }) => {
  const { showDialog } = useDialog();
  const { showNotification } = useNotification();
  const { purchaseFramework, isPurchasing } = usePurchase();
  const { assets } = useUserAssets();
  
  const handlePurchase = async (framework: IFramework) => {
    try {
      // 显示购买确认弹窗
      const confirmed = await showDialog({
        title: "购买框架",
        content: (
          <PurchaseConfirmation 
            itemName={framework.name}
            price={framework.price}
            currency={framework.price > 1000 ? "diamonds" : "coins"}
            userBalance={framework.price > 1000 ? assets.diamonds : assets.coins}
          />
        ),
        confirmLabel: "购买"
      });
      
      if (confirmed) {
        // 执行购买
        await purchaseFramework(framework.id);
        
        showNotification({
          type: "success",
          message: `成功购买 ${framework.name}`
        });
      }
    } catch (error) {
      showNotification({
        type: "error",
        message: `购买失败: ${error.message}`
      });
    }
  };
  
  return (
    <div className={styles.frameworksPanel}>
      <h2>框架商店</h2>
      <div className={styles.frameworksGrid}>
        {frameworks.map(framework => (
          <ShopCard
            key={framework.id}
            title={framework.name}
            price={framework.price}
            currency={framework.price > 1000 ? "diamonds" : "coins"}
            isOwned={framework.owned}
            isVipOnly={framework.isVIP}
            onClick={() => !framework.owned && handlePurchase(framework)}
          />
        ))}
      </div>
      {isPurchasing && <LoadingOverlay text="处理购买中..." />}
    </div>
  );
};
```

## 6. 状态管理

### 6.1 React Context

商店模块使用React Context管理全局状态：

```tsx
// 创建商店上下文
export interface IShopContext {
  selectedCategory: FrameworkCategory;
  setSelectedCategory: (category: FrameworkCategory) => void;
  frameworks: IFramework[];
  packages: IPackage[];
  vipInfo: IVIP | null;
  isLoading: boolean;
  error: Error | null;
}

export const ShopContext = createContext<IShopContext | undefined>(undefined);

// 商店提供者组件
export const ShopProvider: React.FC = ({ children }) => {
  // 状态和逻辑...
  
  const value = {
    selectedCategory,
    setSelectedCategory,
    frameworks,
    packages,
    vipInfo,
    isLoading,
    error
  };
  
  return (
    <ShopContext.Provider value={value}>
      {children}
    </ShopContext.Provider>
  );
};

// 使用商店上下文的钩子
export const useShop = () => {
  const context = useContext(ShopContext);
  if (!context) {
    throw new Error('useShop must be used within a ShopProvider');
  }
  return context;
};
```

### 6.2 自定义钩子

所有商店功能封装为自定义钩子：

```tsx
// 框架数据钩子
export const useFrameworks = () => {
  const [frameworks, setFrameworks] = useState<IFramework[]>([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);
  
  useEffect(() => {
    const fetchFrameworks = async () => {
      try {
        // 从Firebase获取框架数据
        // 处理逻辑...
        setFrameworks(result);
      } catch (err) {
        setError(err as Error);
      } finally {
        setLoading(false);
      }
    };
    
    fetchFrameworks();
  }, []);
  
  return { frameworks, loading, error };
};

// 购买相关钩子
export const usePurchase = () => {
  const [isPurchasing, setIsPurchasing] = useState(false);
  
  const purchaseFramework = async (frameworkId: string) => {
    setIsPurchasing(true);
    try {
      // 购买逻辑...
      return true;
    } catch (error) {
      throw error;
    } finally {
      setIsPurchasing(false);
    }
  };
  
  const purchaseVIP = async () => {
    // VIP购买逻辑...
  };
  
  const purchasePackage = async (packageId: string) => {
    // 组合包购买逻辑...
  };
  
  return {
    isPurchasing,
    purchaseFramework,
    purchaseVIP,
    purchasePackage
  };
};
```

## 7. 非功能需求

### 7.1 性能要求
- 商店初始加载时间：≤3秒（正常网络条件下）
- 框架/包数据更新响应时间：≤1秒
- 使用React.memo优化组件重渲染
- 大量数据使用虚拟滚动实现

### 7.2 安全性要求
- 所有Firebase操作使用安全规则验证
- 用户数据加密存储
- 敏感操作（如购买）必须二次确认
- 购买事务保持原子性
- 使用TypeScript类型安全防止错误操作

### 7.3 可用性要求
- 离线模式支持基本浏览功能
- 断网期间的浏览功能保持可用，购买功能提示需要联网
- 错误提示明确且可操作
- 支持键盘导航和快捷键
- 适配移动设备触摸操作

## 8. 技术约束

### 8.1 React相关约束
- 使用函数组件和React Hooks
- 状态管理使用Context API和useReducer
- 复杂状态逻辑封装为自定义钩子
- 组件设计遵循单一职责原则
- 避免不必要的组件嵌套和重渲染

### 8.2 TypeScript相关约束
- 为所有组件Props定义接口
- 为所有数据结构定义类型
- 使用联合类型代替枚举
- 避免使用any类型，必须时使用unknown
- 函数返回类型明确声明

### 8.3 Firebase相关约束
- 数据操作封装为自定义钩子
- 使用批量操作减少网络请求
- 敏感数据使用安全规则保护
- 大数据集合使用分页加载
- 使用缓存策略减少网络请求 
