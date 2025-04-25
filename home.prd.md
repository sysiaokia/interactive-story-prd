# 主页产品需求文档（PRD）- TypeScript + React版本

## 一、产品定位
主页是AI叙事互动小说游戏的统一入口，负责用户认证、神秘声音与玩家选项交互演示、主操作按钮、底部登录注册入口等核心功能，要求风格统一、响应式、基于React组件化开发，使用TypeScript确保类型安全。

## 二、核心功能
1. **用户认证与入口**
   - 支持邮箱注册、邮箱登录、Google登录、匿名登录。
   - 认证状态检测，未登录自动跳转登录页。
   - 认证异常、会话失效自动清理缓存并提示。
   - 认证切换、登出、匿名升级等流程完整。
   - 使用Firebase Authentication集成认证服务。
2. **神秘声音与玩家选项交互演示**
   - 通过`<MysteriousVoice>`组件展示主提示语、打字动画、声波特效。
   - 通过`<PlayerChoices>`组件展示玩家可选项，按钮交互，选项与神秘声音联动。
   - 该部分为游戏世界观和交互Demo，不是FAQ或帮助说明。
   - 所有状态管理使用React钩子，所有交互基于事件处理函数。
3. **主操作按钮区**
   - 包含"继续探索这个世界""我需要更多的信息"等主操作按钮。
   - 按钮组件化，支持键盘、触屏、鼠标等多种交互。
   - 使用TypeScript类型确保按钮属性和事件处理的类型安全。
4. **底部入口**
   - 提供登录、注册、匿名访问等入口。
   - 所有入口按钮组件化，使用事件处理函数。
5. **响应式布局与降级**
   - 使用响应式CSS（如styled-components或CSS Modules）适配手机、平板、桌面。
   - 低端设备自动降级动画，使用React.lazy实现组件懒加载。
6. **错误处理与降级**
   - 使用错误边界（Error Boundaries）捕获渲染错误。
   - 网络异常、认证失效、数据加载失败等统一错误提示。
   - 支持自动重试、手动重试。
7. **多端同步与缓存**
   - 认证等数据多端同步，使用Firebase实时数据库。
   - 使用自定义钩子封装缓存逻辑，支持分片、签名、过期、清理。

## 三、主要流程
1. **初始化流程**
   - 加载React应用 → 检查认证状态(useAuth钩子) → 初始化全局状态(Context) → 渲染主页组件 → 设置事件处理函数。
2. **认证切换流程**
   - 用户点击登出 → 调用logout函数 → 清理缓存 → 重定向到登录页。
   - 匿名用户升级 → 调用upgradeAccount函数 → 迁移资产与进度 → 刷新UI。

## 四、UI与交互
- 所有UI组件使用React函数组件，放在`src/components/home/`目录下。
- 样式使用CSS Modules或styled-components，放在`src/styles/components/home/`。
- 主页组件结构包括：
  - `<Home>` - 主页容器组件
  - `<HomeHeader>` - 顶部标题区
  - `<MysteriousVoice>` - 神秘声音组件
  - `<PlayerChoices>` - 玩家选项组件
  - `<ActionButtons>` - 主操作按钮区
  - `<AuthFooter>` - 底部认证入口
- 组件间通过props和context传递数据，避免直接操作DOM。
- 支持键盘、触屏、鼠标等多种交互方式。
- 认证等变更通过React Context和状态钩子驱动UI刷新。

## 五、数据与接口
- 使用Firebase SDK和自定义钩子封装数据操作:
  ```tsx
  // 用户认证钩子
  const { user, loading, error, login, logout, register, upgradeAnonymous } = useAuth();
  
  // 数据缓存钩子
  const { data, isLoading, error, refresh } = useCache('keyName', fetchFunction, options);
  ```
- 所有接口返回Promise，支持async/await语法。
- 数据结构包含时间戳、签名、版本号，支持TypeScript接口定义。

## 六、异常与降级
- 使用React Error Boundary捕获渲染错误:
  ```tsx
  <ErrorBoundary fallback={<ErrorScreen />}>
    <HomeContent />
  </ErrorBoundary>
  ```
- 网络异常、认证失效等使用统一通知组件`<Notification />`。
- 低端设备通过特性检测自动降级。
- 所有异步操作使用try/catch包装，详细日志便于排查。

## 七、兼容与安全
- 使用React和TypeScript确保跨浏览器兼容性。
- 敏感数据使用Firebase安全规则保护。
- 用户切换、登出时使用useEffect清理所有监听器。

## 八、伪代码与典型场景
```tsx
// 主页组件
const Home: React.FC = () => {
  // 认证状态
  const { user, loading, logout } = useAuth();
  
  // 初始化
  useEffect(() => {
    // 初始化逻辑
  }, []);
  
  // 处理登出
  const handleLogout = async () => {
    await logout();
    // 清理逻辑
  };
  
  // 错误处理
  const handleError = (error: Error) => {
    // 显示错误
  };
  
  // 加载状态
  if (loading) return <LoadingScreen />;
  
  return (
    <div className={styles.homeContainer}>
      <HomeHeader />
      <MysteriousVoice />
      <PlayerChoices />
      <ActionButtons />
      <AuthFooter onLogout={handleLogout} />
    </div>
  );
};
```

## 九、非功能性需求
- 性能：主页加载时间<2s，使用React.memo和useMemo优化渲染性能。
- 可维护性：TypeScript类型定义，组件化设计，单元测试覆盖率>80%。
- 可扩展性：支持后续增加新入口等，使用插件式架构。

## 十、约束与禁止事项
- 禁止内联样式和硬编码颜色、字体，使用主题变量。
- 禁止不必要的组件重渲染，合理使用React.memo和useMemo。
- 禁止任何组件直接操作全局状态，必须通过统一的Context和钩子。
- 禁止各处自定义弹窗，必须通过统一的通知和弹窗组件。
- 所有实现必须严格遵守 mdc 规则，同时使用TypeScript确保类型安全。
