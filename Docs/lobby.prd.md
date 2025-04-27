# 新大厅模块产品需求文档 - TypeScript + React 版本

## 1. 概述

新大厅是游戏的主要交互界面，负责世界框架展示、存档管理、用户资产显示和全局导航等核心功能。使用TypeScript + React + Firebase技术栈实现所有功能，采用组件化、类型安全和响应式设计架构。实现严格遵循MDC规则，包括认证、状态管理、数据管理、UI组件、安全机制等。

## 2. 核心功能模块

### 2.1 大厅主页

- 提供世界框架展示区、存档管理区、资产栏、快捷入口、操作按钮区四大核心区域
- **默认展示"世界框架"(world类别)** 作为首个展示的框架类型
- 支持根据用户状态（游客/登录/VIP）显示不同内容
- 实现顶部导航栏，包含分类切换功能
- 右侧/顶部显示用户资产（金币、钻石）信息
- 使用React Context提供全局状态管理

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
- 使用TypeScript接口定义所有数据结构，保证类型安全

### 2.3 存档管理

- 展示当前用户所有存档，包含标题、创建时间、最后游玩时间
- 支持创建新存档、加载存档、删除存档、导入/导出存档
- 存档操作必须通过统一的SaveManager服务和useSave钩子
- 支持自动保存、云同步、多端合并
- 存档列表根据更新时间排序
- **存档配置文件**：
  - 位于`src/features/save/saveConfig.ts`
  - 可配置免费用户存档位数（默认3个）
  - 可配置VIP用户存档位数（默认10个）
  - 可配置存档最大容量（默认5MB）
  - 可配置自动保存间隔（默认5分钟）
- 存档功能完全遵循save-manager.mdc规则
- 使用Firebase Firestore存储存档数据

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
- 实现为React组件，使用虚拟列表优化长列表性能

### 2.5 资产栏与VIP状态

- 顶部显示用户当前金币、钻石数量和VIP状态
- 点击金币/钻石图标可跳转商店充值
- VIP状态显示到期时间和特权图标
- 资产变更时的动画效果
- 实时同步和更新资产数据
- 使用Context Provider共享资产状态
- 使用React hooks封装资产相关操作

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
- 使用TypeScript接口严格定义用户档案数据结构

### 2.7 商店入口

- 提供明显的"商店"入口按钮
- 点击后使用React Router导航到Shop页面
- 通过React Context传递用户状态和VIP信息
- 与商店模块完全集成，遵循shop相关的mdc规则
- 商店返回时自动刷新大厅数据
- 使用TypeScript类型保证导航参数类型安全

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
- 设置使用统一的React组件，遵循lobby-ui.mdc规则
- 使用自定义钩子(useSettings)管理设置状态

### 2.9 快捷入口

- 商店入口：使用React Router导航至商店页面
- 设置入口：显示设置组件
- 所有入口通过事件处理函数和React Router实现导航

### 2.10 操作按钮区

- 刷新按钮：调用刷新函数重新加载框架和存档数据
- 同步按钮：调用同步函数强制云同步所有数据
- 登出按钮：调用logout函数清理数据并登出账号
- 所有操作使用React事件处理函数，有加载状态和结果反馈
- 使用加载指示器显示异步操作状态

### 2.11 通知区

- 统一的通知组件`<NotificationSystem>`
- 支持成功、错误、警告、信息四种类型通知
- 通知自动消失，支持手动关闭
- 使用自定义钩子(useNotification)管理通知状态
- 所有系统消息必须通过通知组件展示，禁止自定义弹窗

## 3. 用户界面

### 3.1 整体布局

- 响应式设计，使用SCSS预处理器结合Grid和Flexbox，遵循BEM命名规范，适配各种屏幕尺寸
- 主体内容区域居中，最大宽度限制
- 分层结构：背景层、装饰层、主内容区、通知区
- 所有UI元素必须位于页面可视区域内，避免超出屏幕
- 采用SCSS模块化组织，确保组件样式隔离，避免全局污染

### 3.2 框架卡片组件

- 使用React函数组件实现卡片设计(`<FrameworkCard>`)
- 卡片包含标题、描述、状态标记
- 卡片悬停效果和点击动画
- 不同状态（已解锁、未解锁、VIP专属）的视觉区分
- 支持批量渲染和虚拟列表技术(react-virtualized)
- 使用TypeScript接口定义卡片Props和数据结构

### 3.3 存档列表组件

- 使用React函数组件实现存档项设计(`<SaveItem>`)
- 存档项包含标题、时间、操作按钮
- 新建存档按钮位于列表顶部
- 存档项操作菜单（加载、删除、导出）
- 支持空状态和加载状态显示
- 使用React钩子处理异步操作

### 3.4 弹窗组件

- 使用React Portal实现弹窗组件(`<Dialog>`)
- 支持确认弹窗、表单弹窗、结果弹窗
- 所有弹窗有统一的关闭按钮和动画效果
- 弹窗显示时禁用背景交互
- 使用useDialog钩子管理弹窗状态

### 3.5 导航

- 顶部分类导航，使用React Tab组件实现类型切换
- 分类切换时保留当前选择状态
- 使用React state管理当前选中分类，默认为"world"
- 使用TypeScript联合类型定义固定分类选项

## 4. 数据结构与管理

### 4.1 框架数据结构

```typescript
interface IFramework {
  id: string;         // 如 "world_1" 
  name: string;       // 显示名称
  description: string; // 描述
  category: FrameworkCategory;   // "world"、"era"、"technology"等七种固定类型
  type: "normal" | "premium"; // 普通/高级
  isVIP: boolean;     // 是否VIP专属
  isUnlocked: boolean; // 是否已解锁
}

// 框架类别类型
type FrameworkCategory = "world" | "era" | "technology" | "rules" | "race" | "politics" | "conflict";
```

### 4.2 存档数据结构

```typescript
interface ISaveGame {
  id: string;         // 存档ID
  userId: string;     // 用户ID
  title: string;      // 存档标题
  description: string; // 存档描述
  frameworkId: string; // 关联的框架ID
  createdAt: string;  // 创建时间，ISO格式
  updatedAt: string;  // 更新时间，ISO格式
  playTime: number;   // 游戏时长（秒）
  gameVersion: string; // 游戏版本
  lastScene: string;  // 最后场景
  data: GameData;     // 实际游戏数据（序列化）
}

// 游戏数据接口
interface GameData {
  // 游戏相关数据...
  [key: string]: any;
}
```

### 4.3 用户资产数据结构

```typescript
interface IUserAssets {
  userId: string;
  coins: number;
  diamonds: number;
  ownedFrameworks: string[]; // 拥有的框架ID
  vipStatus: {
    isActive: boolean;
    expiryDate: string;      // ISO日期
  };
  lastUpdated: string;       // ISO日期
}
```

### 4.4 用户个人档案数据结构

```typescript
interface IUserProfile {
  userId: string;
  displayName: string;      // 显示名称
  accountType: "anonymous" | "google" | "email"; // 账号类型
  email: string;            // 邮箱（如有）
  createdAt: string;        // 创建时间，ISO格式
  stats: {
    totalPlayTime: number;  // 总游戏时长（秒）
    completedStories: number; // 完成故事数
    unlockedFrameworks: number; // 解锁框架数
    createdCharacters: number;   // 创建角色数
  }
}
```

### 4.5 设置数据结构

```typescript
interface IGameSettings {
  userId: string;
  audioEffects: {
    enabled: boolean;
    volume: number;         // 0-100
  };
  music: {
    enabled: boolean;
    volume: number;         // 0-100
  };
  textSize: "small" | "medium" | "large";
  animations: {
    enabled: boolean;
    simplified: boolean;    // 简化动画
  };
  language: string;         // 语言代码，如"zh-CN"
  notifications: {
    enabled: boolean;
    gameEvents: boolean;    // 游戏内事件通知
    systemEvents: boolean;  // 系统事件通知
  };
  autoSave: {
    enabled: boolean;
    interval: number;       // 保存间隔（分钟）
  };
  sync: {
    enabled: boolean;
    autoSync: boolean;      // 自动同步
    syncInterval: number;   // 同步间隔（分钟）
  };
}
```

## 5. 主要流程示例

### 5.1 大厅初始化流程

```tsx
// 大厅页面组件
const Lobby: React.FC = () => {
  // 认证状态
  const { user, loading: authLoading } = useAuth();
  
  // 框架数据
  const { frameworks, loading: frameworksLoading, error: frameworksError } = useFrameworks();
  
  // 存档数据
  const { saves, loading: savesLoading, error: savesError } = useSaves(user?.uid);
  
  // 用户资产
  const { assets, loading: assetsLoading } = useUserAssets(user?.uid);
  
  // 加载状态
  const isLoading = authLoading || frameworksLoading || savesLoading || assetsLoading;
  
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
  if (frameworksError || savesError) {
    return <ErrorScreen error={frameworksError || savesError} />;
  }
  
  return (
    <div className={styles.lobbyContainer}>
      <LobbyHeader assets={assets} />
      <CategoryTabs 
        selectedCategory={selectedCategory} 
        onCategoryChange={handleCategoryChange} 
      />
      <div className={styles.mainContent}>
        <FrameworksPanel 
          frameworks={frameworks.filter(f => f.category === selectedCategory)} 
        />
        <SavesPanel saves={saves} />
      </div>
      <ActionButtons />
      <NotificationSystem />
    </div>
  );
};
```

### 5.2 存档创建流程

```tsx
// 在SavesPanel组件中
const SavesPanel: React.FC<SavesPanelProps> = ({ saves }) => {
  const { createSave, deleteSave, loadSave } = useSaves();
  const { showDialog } = useDialog();
  const { showNotification } = useNotification();
  
  const handleCreateSave = async (frameworkId: string) => {
    try {
      // 显示创建存档表单
      const saveData = await showDialog({
        title: "创建新存档",
        content: <CreateSaveForm frameworkId={frameworkId} />,
        confirmLabel: "创建"
      });
      
      if (saveData) {
        // 创建存档
        await createSave(saveData);
        showNotification({
          type: "success",
          message: "存档创建成功"
        });
      }
    } catch (error) {
      showNotification({
        type: "error",
        message: `创建存档失败: ${error.message}`
      });
    }
  };
  
  // 其他存档操作...
  
  return (
    <div className={styles.savesPanel}>
      <h2>我的存档</h2>
      {saves.length === 0 ? (
        <EmptyState message="暂无存档" />
      ) : (
        <div className={styles.savesList}>
          {saves.map(save => (
            <SaveItem 
              key={save.id} 
              save={save} 
              onLoad={loadSave} 
              onDelete={deleteSave} 
            />
          ))}
        </div>
      )}
      <Button onClick={() => handleCreateSave()}>创建新存档</Button>
    </div>
  );
};
```

## 6. 非功能需求

### 6.1 性能要求
- 大厅初始加载时间：≤3秒（正常网络条件下）
- 框架/存档数据更新响应时间：≤1秒
- 动画流畅度：60fps，低端设备可降级
- 使用React.memo优化组件重渲染
- 大量数据使用虚拟滚动实现

### 6.2 安全性要求
- 所有Firebase操作使用安全规则验证
- 用户数据加密存储
- 敏感操作（如删除存档）必须二次确认
- XSS防护：使用React自动转义
- 使用TypeScript类型安全防止错误操作

### 6.3 可用性要求
- 离线模式支持基本浏览功能
- 断网期间的数据操作在重连后自动同步
- 错误提示明确且可操作
- 关键操作提供撤销选项
- 支持键盘导航和快捷键

### 6.4 可测试性
- 组件设计为可测试单元
- 业务逻辑与UI分离
- 提供测试钩子和测试ID
- 状态变更可跟踪和预测
- 支持组件故事书(Storybook)展示

## 7. 技术约束

### 7.1 React相关约束
- 使用函数组件和React Hooks
- 状态管理使用Context API和useReducer
- 复杂状态逻辑封装为自定义钩子
- 组件设计遵循单一职责原则
- 避免不必要的组件嵌套和重渲染

### 7.2 TypeScript相关约束
- 为所有组件Props定义接口
- 为所有数据结构定义类型
- 使用联合类型代替枚举
- 避免使用any类型，必须时使用unknown
- 函数返回类型明确声明

### 7.3 Firebase相关约束
- 数据操作封装为自定义钩子
- 使用批量操作减少网络请求
- 敏感数据使用安全规则保护
- 大数据集合使用分页加载
- 使用缓存策略减少网络请求
