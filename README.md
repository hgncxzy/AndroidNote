# Work Note

1. [App 更新](https://github.com/hgncxzy/AndroidNote/blob/master/note/App更新.md)
2. [Android 教程](https://www.runoob.com/w3cnote/android-tutorial-intro.html)
3. [Android 新特性](https://github.com/hgncxzy/AndroidNote/tree/master/note/Android版本与新特性)
4. [测试](https://github.com/hgncxzy/AndroidNote/blob/master/note/测试.md)
5. [打包](https://github.com/hgncxzy/AndroidNote/blob/master/note/打包.md)
6. [Git ](https://github.com/hgncxzy/AndroidNote/blob/master/note/Git.md)
7. [绘图](https://github.com/hgncxzy/AndroidNote/blob/master/note/绘图.md)
8. [架构](https://github.com/hgncxzy/AndroidNote/blob/master/note/架构.md)
9. [Kotlin](https://github.com/hgncxzy/AndroidNote/blob/master/note/Kotlin.md)
10. [LeetCode](https://leetcode-cn.com/problemset/algorithms/?difficulty=简单)
11. [权限](https://github.com/hgncxzy/AndroidNote/blob/master/note/权限.md)
12. [RxJava](https://github.com/hgncxzy/AndroidNote/blob/master/note/RxJava.md)
13. [适配](https://github.com/hgncxzy/AndroidNote/blob/master/note/适配.md)
14. [数据库](https://github.com/hgncxzy/AndroidNote/blob/master/note/数据库.md)
15. [UI](https://github.com/hgncxzy/AndroidNote/blob/master/note/UI.md)
16. [性能优化](https://github.com/hgncxzy/AndroidNote/blob/master/note/性能.md)
17. [XML](https://github.com/hgncxzy/AndroidNote/blob/master/note/Android中自定义属性attr.xml的格式详解.md)
18. [字符串处理](https://github.com/hgncxzy/AndroidNote/blob/master/note/字符串处理/字符串处理.md)
19. [环境配置](https://github.com/hgncxzy/AndroidNote/blob/master/note/环境配置/开发环境配置.md)
20. [数组处理](https://github.com/hgncxzy/AndroidNote/blob/master/note/数组处理/数组处理.md)
21. [Java 回调机制](https://github.com/hgncxzy/AndroidNote/blob/master/note/回调机制/Java回调.md)
22. [时间日期处理](https://github.com/hgncxzy/AndroidNote/blob/master/note/时间日期处理/时间和日期处理.md)
23. [文件操作](https://github.com/hgncxzy/AndroidNote/blob/master/note/文件操作/文件操作.md)
24. [图片相关](https://github.com/hgncxzy/AndroidNote/blob/master/note/图片相关/图片相关.md)
25. [TextView](https://github.com/hgncxzy/AndroidNote/blob/master/note/TextView/TextView.md)
26. [虚拟键盘](https://github.com/hgncxzy/AndroidNote/blob/master/note/虚拟键盘/虚拟键盘.md)
27. [系统按键相关](https://github.com/hgncxzy/AndroidNote/blob/master/note/系统按键相关/按键.md)
28. [EditText](https://github.com/hgncxzy/AndroidNote/blob/master/note/EditText/EditText.md)
29. GridView
30. Fragment
31. NDK
32. 系统返回、退出操作等
33. ListView
34. ADB
35. 通用工具类和方法
36. Activity
37. SQLite
38. 



# Android App Dev Skills

（[参考资料]( https://github.com/TeamStuQ/skill-map/blob/master/data/map-MobileDev-AndroidDev.md)）

## 操作系统

- Windows/MacOSX/Linux

## 编程语言

- Java
- HTML/JS (Hybrid/Web App)
- C/C++ (NDK)
- SQL (DB)
- Kotlin

## 开发工具

- [IDE](https://github.com/hgncxzy/AndroidNote/blob/master/note/IDE.md)

- [Android Studio](https://github.com/hgncxzy/AndroidNote/blob/master/note/Android%20Studio.md)
- Eclipse

- 调试工具
  - 网络调试
    - Charles
    - Wireshark
    - Fiddler
    - tcpdump
    - Paw/Postman
  - 内存分析
    - monitor
    - MAT
  - Android tools
    - adb
    - draw9patch
    - hierarchyviewer
    - uiautomatorviewer
- 版本管理
  - Git
    - Git命令
    - Github/GitLab
  - SVN
- CodeReview
  - Gerrit
  - Github pull request
- Bug/任务管理
  - Redmine
  - JIRA
  - Bugzilla
  - Teambition
  - Tower
- 编译工具
  - Gradle
- 持续集成
  - Jenkins
  - Travis CI
- 应用分发
  - 蒲公英
  - fir.im

------

## App基础

- 基本组件
  - Activity
  - Service
  - Content Provider
  - Broadcast Receiver
  - Intent/Intent Filter
  - App Manifest File
- UI
  - Layouts
  - Widgets
  - Resources
  - Animations
  - 设备适配
- Connectivity
  - WiFi
  - Mobile网络
  - 网络状态监听
- MultiMedia
  - Audio/Video
  - Camera/Gallery
- GPS&Location&Map
  - 系统定位
    - GPS定位
    - Network定位
  - 3rd Map定位
    - 百度Map
    - 高德Map

## App进阶

- Process&Thread
  - Process
    - Linux进程
    - App进程原理
  - AIDL
    - 实现方式
    - 原理
  - Handler/Looper/MQ/Thread
  - Loader
  - AsyncTask
- 性能优化
  - ANR
  - 布局层级性能优化
- 内存优化
  - 内存检测工具
  - 内存分析工具
  - Bitmap优化
  - 内存泄露查找及分析
- 网络优化
  - API优化
  - 低网速下优化
  - 流量使用优化
    - 判断当前网络类型
    - 使用缓存
- 单元测试

## App高级

- 相关原理熟悉
  - Activity
    - 启动流程
    - 生命周期回调原理
    - 与View/Window的关系
    - 与Fragment的关系
  - View/Window
    - View/Window关系
    - View渲染
    - View事件分发处理流程
  - 编译打包
    - 编译打包原理
    - 逆向工程分析
    - 热修复
- Hybrid App
  - 与Native App的异同
  - 主流框架
    - PhoneGap
    - ionic
    - React Native
- 架构能力
  - 架构
    - MVC
    - MVP
    - MVVM
    - Flux
    - Clean Architecture
  - App框架
    - 分包
    - 分层
  - 设计模式
    - OOD原则
    - 常用设计模式运用
- ART&Dalvik
  - AOT compilation
  - GC
  - Bytecode&.Dex
- 自动化测试
  - monkey/monkey runner
  - UIAutomator
  - Espresso
  - Robotium

## 扩展学习

- 响应式编程
  - Rx
    - RxJava
    - RxAndroid
    - RxBinding
  - Agera
- 主流开源库
  - 快速开发
    - Android Annotation
    - ButterKnife
  - Views
    - 太多
  - HTTP模型
    - Retrofit
    - OkHttp
    - Volley
  - 图片处理
    - Glide
    - Fresco
    - Picasso
    - UIL
  - 依赖注入
    - Dagger2
  - 数据库
    - ORMLite
    - GreenDAO
    - Realm
    - Sugar
  - 辅助
    - Logger
    - LeakCanary
    - DbInspector

# App 架构师技能图谱

([参考书籍 -- App 架构师](https://github.com/SkySeraph-XKnife/XKnife-Android))

## Start

## Learn the Basics

1. 语言语法
   1. Kotlin/Java/C/C++
   2. OC/Swift
2. 工具使用
   1. IDE
   2. 编译测试
   3. 版本管理
   4. 产品设计
   5. ......
3. SDK 使用
4. 开源选择

## Getting Deeper

1. 安全逆向
   1. 逆向分析
   2. 安全测试
   3. 安全建议
      1. 混淆签名
      2. 加固加壳
      3. 安全编码
2. 热门技术
3. 性能优化
   1. 硬件性能
   2. UI 和 CPU
   3. 内存性能
   4. 网络性能
   5. 包 Size
   6. 启动速度
   7. 代码优化
4. 常用模块
   1. 基础组件
   2. 常用业务模块
   3. 编译打包
   4. 版本适配
   5. 三方 SDK
5. 架构和重构
   1. 组件化和模块化
   2. UML 基本功
   3. 设计模式
   4. 接口设计
   5. 架构模式选型
   6. 重构
6. 质量和稳定
   1. 质量稳定性指标
   2. CI 和代码监控
   3. Crash
   4. 测试专场
      1. 兼容性测试
      2. 自动化测试
      3. 性能/安全测试
      4. A/B Testing
      5. 代码覆盖率

## Expand

1. 项产运设
   1. 项目管理
   2. 产品思维
   3. 设计理念
   4. 运营统计

2. 高效团队

## End



