# v2.0.2

新增
- 新管理器根据设备状态（如省电模式、性能等级）动态决定是否启用模糊效果
- 新管理器支持折叠过长的模块描述
- 新增点按劫持（tapjacking）缓解开关及提示
- 当模块已安装时，新管理器隐藏“安装到其他用户”的选项

改进
- 减少每个方法的最大回调数量，降低异常模块导致的系统崩溃扩散风险
- 确保模块更新后重新分发 Xposed 服务
- 系统启动阶段更早向 daemon 发送 binder，减少初始化竞态窗口
- 切换管理器无需再强行停止进程
- 更新 LSPlant，修复多类注入与 hook 相关问题
- 更新 MIUIX，修复已知兼容性问题
- 优化管理器启动及模块仓库加载时的内存占用

修复
- 修复新管理器“安装到用户”选项异常
- 修复卸载模块时未清理配置的问题
- 修复模块更新后在极少数情况下 hook 未生效的问题（如更新后立即强制停止目标应用）
- 修复新 API 的 native API 加载时机问题
- 修复管理器启动及加载模块仓库时的内存占用异常
- 修复搜索结果被底栏遮挡的问题（窗口 inset 处理）
- 修复新管理器边到边布局问题

Added
- Enabled dynamic blur based on device state (e.g. power saving mode, performance class)
- Added collapsing for long module descriptions
- Added tapjacking mitigation toggle and hint
- Hid the "install to other user" option when the module is already installed

Improved
- Reduced per-method callback count to limit crash propagation caused by faulty modules
- Ensured Xposed service is re-delivered after module updates
- Sent binder to daemon earlier during system boot to reduce initialization race conditions
- Removed the need to force stop when switching manager
- Updated LSPlant to fix various injection issues
- Updated MIUIX to address known issues
- Optimized memory usage during manager startup and repository loading for low-RAM devices

Fixed
- Fixed incorrect "install to user" behavior in the new manager
- Fixed module configuration not being removed on uninstall
- Fixed rare cases where hooks were not updated after module upgrade
- Fixed native API loading timing for the new API
- Fixed excessive memory usage during manager startup and repository loading
- Fixed search results being obscured by the bottom bar
- Fixed edge-to-edge layout issues in the new manager

# v2.0.1

新增
- 支持 Android 8.1 至 Android 17 Beta 3
- 新增完整的 libxposed API 101 支持
- 新增 miuix 版本管理器并默认启用
- 新增可按应用配置的还原内联钩子功能
- 新增对 libxposed 相关类启用 API 调用保护
- 新增安全模式
- 新增 action.sh 支持，可从 action.sh 打开管理器
- 重构 dex2oat 包装器，支持在 Android 12+ 重新优化系统框架
- 新增 16K page size 支持
- 支持注入系统自定义 resolver 的进程
- 支持重置作用域请求设置
- 支持将日志转发至守护进程

改进
- 大幅度增强对被注入的应用的隐藏能力
- 适配新版 Android 上的反射限制与部分系统行为变化
- 改进软件包与模块解析逻辑
- 优化管理器与服务之间的通信方式，加快启动速度
- 改进 LoadedApk、类初始化 Hook、native hook 的兼容性
- 改进 system_server 相关初始化、binder 发送、异步重试与重启恢复逻辑
- 改进日志系统，提供更丰富的上下文信息，例如 UID / PID
- 改进多用户支持

修复
- 修复作用域备份与恢复功能
- 修复与部分自带 LSPlant 的应用的兼容性问题
- 修复 XSharedPreferences 初始化、目录权限与目录缺失问题
- 修复部分 Hook 崩溃与稳定性问题
- 修复一些内存泄漏问题
- 修复自动取色、浏览器跳转、搜索、图标显示等多项 UI 问题
- 修复对部分 OEM 系统的多项兼容性问题
- 修复多用户、卸载后配置残留与恢复错乱问题
- 修复 system_server 重启后的状态恢复问题
- 修复目录权限错误和配置迁移异常
- 修复日志解析与打包中的一些问题
- 修复 RemoteFile 在重启后可能无法读取的问题

移除
- 移除桌面快捷方式，可通过通知、拨号盘或 action.sh 启动管理器
- 移除 Riru 支持
- 移除对 libxposed API 版本 100 的支持

Added
- Support for Android 8.1 through Android 17 Beta 3
- Full support for libxposed API 101
- Added a new MIUIX-based Manager and enabled it by default
- Added per-app restore inline hooks support
- Added API call protection for libxposed-related classes
- Added safe mode
- Added action.sh support, including opening the Manager from action.sh
- Refactored the dex2oat wrapper, with support for recompiling the system framework on Android 12+
- Added 16K page size support
- Added support for injecting processes that use a custom system resolver
- Added support for resetting scope request settings
- Added support for forwarding log to daemon process

Improved
- Significantly improved hiding for injected apps
- Adapted to reflection restrictions and system behavior changes on newer Android versions
- Improved package and module parsing logic
- Improved communication between the manager and the service, with faster startup
- Improved compatibility for LoadedApk handling, class initializer hooks, and native hooks
- Improved system_server initialization, binder delivery, async retries, and recovery after restarts
- Improved logging with rich context information such as UID and PID
- Improved multi-user support

Fixed
- Fixed scope backup and restore
- Fixed compatibility issues with some apps that bundle their own LSPlant
- Fixed XSharedPreferences initialization, directory permission, and missing-directory issues
- Fixed various hook-related crashes and stability issues
- Fixed several memory leak issues
- Fixed various UI issues including dynamic color, browser launch, search, and icon display
- Fixed multiple compatibility issues on some OEM ROMs
- Fixed multi-user issues, stale config after uninstall, and restore inconsistencies
- Fixed state recovery after system_server restarts
- Fixed directory permission errors and config migration issues
- Fixed several issues in log parsing and packaging
- Fixed cases where RemoteFile could become unreadable after reboot

Removed
- Removed desktop shortcuts; the Manager can now be opened via notification, dialer code, or action.sh
- Removed Riru support
- Removed support for libxposed API version 100
