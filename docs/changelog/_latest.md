**当前版本：v2.5.2**

**⬇️ 下载 (Downloads)**
- Android: [arm64-Apk](https://github.com/The-Brotherhood-of-SCU/Bugaoshan/releases/download/v2.5.2/bugaoshan_2.5.2_arm64-v8a.apk)
- Windows: [x64 Zip](https://github.com/The-Brotherhood-of-SCU/Bugaoshan/releases/download/v2.5.2/bugaoshan_2.5.2_windows_x64.zip)
- macOS (Apple Silicon): [dmg](https://github.com/Visio-Vanitas/Bugaoshan/releases/download/v2.5.2/bugaoshan_2.5.2_macos_arm64.dmg)
- iOS: 未发布正式版，可安装testflight后点击链接进行邀测: https://testflight.apple.com/join/Vyenb6gC ；另提供 [ipa](https://github.com/Visio-Vanitas/Bugaoshan/releases/download/v2.5.2/bugaoshan_2.5.2_ios_unsigned.ipa)（ipa仅供理解有关技术的同学测试使用，非技术背景同学请勿下载）

> 💡 **Note**: 当前项目优先保障 Android 端的稳定与体验。 Windows 版本可能存在部分兼容性或体验问题。

**Added**
- 课表显示设置新增「显示课程周数」开关，支持自由控制课程卡片上是否显示周数范围
- 新增用户手册与官网入口：个人信息页可一键打开官方用户手册与官网
- 登录页新增「重置密码」：应用内完成官方三步密码重置流程
- 设置页新增页面转场时长与动画开关，可动态调整转场动画效果

**Fixed**
- 修复课表「复制课程」覆盖原课程、无法生成副本的问题：现在点「复制」会打开「新建副本」界面，调整好时段并保存后生成副本，取消则不产生副本（#312）
- 修复编辑课程后校区信息被清空的问题
- 修复页面切换动画开关仅对 Dock 栏切换生效的问题
- 修复课表背景图淡入因图片缓存同步命中而被跳过的问题
- 修复方案成绩接口结构变化导致的成绩解析失败问题

**Full diff:** https://github.com/The-Brotherhood-of-SCU/Bugaoshan/compare/v2.5.1...v2.5.2
