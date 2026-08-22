---
order: 2
icon: mdi:rocket-launch-outline
---

# 环境与构建

本页写给第一次接触 Flutter 项目的贡献者。即使你只会使用命令行，也可以按顺序完成准备、运行和检查。

这里的“构建”可以理解为：把源代码和依赖打包成可以运行的 App。第一次配置环境时不必一次理解整个项目，先让示例 App 成功启动，再逐步阅读代码。

## 先理解几个词

- **仓库（repository）**：项目的完整代码目录，Git 用它记录每次修改。
- **依赖（dependency）**：项目使用的第三方库，例如 Flutter 的网络请求、数据库和界面组件。
- **分支（branch）**：在不影响 `main` 主线的情况下进行一组修改的独立工作区。
- **代码生成**：根据注解或配置自动生成 Dart 文件，例如依赖注入和国际化文件。
- **构建产物**：编译后生成的 APK、Windows 程序或 Linux 压缩包，不应当当作源代码修改提交。

## 一、准备工具

### 必需工具

1. [Git](https://git-scm.com/downloads)：下载仓库、创建分支和提交修改。
2. [Flutter SDK](https://docs.flutter.dev/get-started/install) 3.44 或更高版本：包含 Dart SDK，要求 Dart SDK 3.10.4 或更高版本。
3. 代码编辑器：推荐 [VS Code](https://code.visualstudio.com/download) ，并安装 Flutter、Dart 插件。

安装 Flutter 后，在终端执行：

```bash
flutter --version
dart --version
flutter doctor -v
```

`flutter doctor -v` 会列出每项工具是否可用。首次配置不要求所有平台都通过：如果只开发 Dart 逻辑，可以先确保 Flutter、Dart 和 Git 正常；如果要运行 Android 或桌面端，再按提示安装对应工具。

### 平台附加要求

- **Android**：安装 [Android Studio](https://developer.android.com/studio)、Android SDK 和一个模拟器，或连接已开启开发者选项的实体设备。(当然，直接向你的手机传输apk也不失为一种办法)
- **Windows**：Windows 桌面目标需要 [Visual Studio](https://visualstudio.microsoft.com/downloads/) 的桌面 C++ 工具，以及 [NuGet CLI](https://learn.microsoft.com/en-us/nuget/install-nuget-client-tools?tabs=windows#nugetexe-cli)；后者是 `flutter_inappwebview` 的 Windows 目标所需依赖。
- **Linux**：按照 [Flutter Linux 桌面环境要求](https://docs.flutter.dev/platform-integration/linux/setup) 安装 GTK 3、WPE WebKit 2.0、WPEBackend-fdo、libwpe、libsecret、libepoxy 和 Wayland 开发包。正式 Linux 发布包会动态链接这些系统库，不会把 WPE WebKit 一起打包。
- **iOS/macOS**：需要 macOS 和 [Xcode](https://developer.apple.com/xcode/) 以及对应的签名/开发环境；普通 Windows 或 Linux 电脑不能直接构建 Apple 平台应用。

## 二、下载项目

在 GitHub 上点击 Fork，可以在自己的账号下创建一份仓库副本。只想阅读或本地运行时，也可以直接克隆主仓库。

推荐初学者使用 HTTPS：

```bash
git clone https://github.com/The-Brotherhood-of-SCU/Bugaoshan.git
cd Bugaoshan
```

如果你已经配置了 GitHub SSH 密钥，也可以使用：

```bash
git clone git@github.com:The-Brotherhood-of-SCU/Bugaoshan.git
cd Bugaoshan
```

确认当前目录正确：

```bash
git status
```

看到类似 `On branch main` 的提示，说明 Git 已经识别到项目仓库。

## 三、配置 Pub 镜像（可选）

Flutter 依赖从 Pub 下载。网络较慢时可以使用国内镜像；如果网络正常，也可以跳过本节。

### Windows PowerShell

以管理员身份打开 PowerShell，执行：

```powershell
setx PUB_HOSTED_URL "https://pub.flutter-io.cn" /M
setx FLUTTER_STORAGE_BASE_URL "https://storage.flutter-io.cn" /M
```

执行后重新打开终端，新的环境变量才会生效。

### Linux / macOS

将下面两行加入正在使用的 Shell 配置文件（例如 `~/.bashrc` 或 `~/.zshrc`），然后重新打开终端：

```bash
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
```

::: warning 不要随意改动锁文件
项目提交了 `pubspec.lock`。安装依赖时如果切换了源，锁文件可能出现与源地址有关的变化。提交前请检查 `git diff pubspec.lock`，确认没有把无关的依赖源变化带进 PR。
:::

## 四、安装依赖

在项目根目录运行：

```bash
flutter pub get
```

这一步会读取 `pubspec.yaml`，下载项目需要的库，并在本机建立依赖缓存。它不会把依赖源码复制到你的 Git 提交中。

如果出现 `flutter: command not found` 或“不是内部或外部命令”，说明 Flutter 没有加入系统 PATH；先修复 `flutter doctor -v`，再重新执行本节命令。

## 五、生成项目文件

项目有两类常用生成文件：依赖注入/序列化代码，以及本地化代码。第一次运行或修改相关源文件后，按以下顺序执行：

```bash
# 根据注解生成依赖注入和序列化代码
dart run build_runner build --delete-conflicting-outputs

# 根据 lib/l10n/*.arb 生成本地化 Dart 文件
flutter gen-l10n
```

`--delete-conflicting-outputs` 表示生成器发现旧文件冲突时，先删除可以安全重建的旧产物。不要手动编辑生成的 Dart 文件；应该修改它们对应的注解、模型或 ARB 源文件，然后重新生成。

## 六、第一次运行 App

先查看 Flutter 找到的设备：

```bash
flutter devices
```

然后直接运行：

```bash
flutter run
```

如果有多个设备，指定设备 ID：

```bash
flutter run -d <device-id>
```

其中 `<device-id>` 要替换为 `flutter devices` 输出中的实际值，例如 Android 模拟器或 `windows`。第一次运行会编译较多依赖，等待时间较长是正常现象。

修改 Dart 文件后，运行中的终端通常支持：

- `r`：热重载，保留当前页面状态，适合调整界面。
- `R`：热重启，重新启动 Dart 程序，适合修改初始化逻辑。
- `q`：退出运行。

## 七、修改后如何自检

提交前至少运行以下检查：

```bash
# 自动格式化 Dart 文件
dart format .

# 静态分析，检查类型和常见错误
flutter analyze

# 运行单元测试和组件测试
flutter test
```

如果本次只修改了少数文件，也可以先对相关目录执行格式化，减少无关差异。检查结果中出现原本就存在的告警时，不要假装它们已经修复；在 PR 描述中说明新增或未新增告警即可。

## 八、安装提交钩子

项目提供了 pre-commit hook。它会在提交时对暂存的 `.dart` 文件运行 `dart format`，帮助避免格式不一致。

### Linux / macOS

```bash
ln -sf .githooks/pre-commit .git/hooks/pre-commit
```

### Windows（Git Bash）

```bash
cp .githooks/pre-commit .git/hooks/pre-commit
```

安装后，提交代码时如果格式不符合要求，Git 可能会拒绝提交或修改暂存内容。请重新查看 `git diff --cached`，确认格式化没有带来无关变化。

## 九、按平台构建发布包

确认代码、分析和测试通过后，可以按目标平台构建：

```bash
flutter build apk --release       # Android
flutter build windows --release  # Windows
flutter build linux --release    # Linux
flutter build macos --release    # macOS
flutter build ios --release --no-codesign  # iOS，未签名
```

发布构建会生成 `build/` 目录。`build/` 是临时产物，不要把其中的 APK、缓存或编译目录直接提交到仓库。

需要在已连接的 iPhone 上以 Profile 模式验证时，可使用：

```bash
tool/install_ios_profile.sh <device>
```

`<device>` 可以是 `xcrun devicectl list devices` 输出的设备 ID、UDID 或设备名。不要对正在运行的 App 反复直接执行 `devicectl device install app`；遇到白屏时按脚本提示解锁设备或重启设备。

## 常见问题

| 现象 | 可能原因 | 处理方式 |
| --- | --- | --- |
| `flutter` 或 `dart` 找不到 | SDK 未安装或未加入 PATH | 重新打开终端，运行 `flutter doctor -v`，检查 PATH |
| `flutter pub get` 超时 | 网络或 Pub 源不可用 | 检查网络，按本页设置镜像后重试 |
| `No devices found` | 没有启动模拟器或连接设备 | 运行 `flutter devices`，启动模拟器或连接实体设备 |
| 生成文件冲突 | 旧产物与当前源文件不一致 | 重新运行 `dart run build_runner build --delete-conflicting-outputs` |
| Windows 构建缺 NuGet | 未安装或 NuGet 不在 PATH | 安装 NuGet CLI 后重新打开终端 |
| Linux 构建缺系统库 | 缺少 GTK/WPE 等开发包 | 按平台文档安装依赖；这不是 Dart 代码错误 |
| `flutter analyze` 出现告警 | 代码风格或类型问题 | 先看文件和行号，再修复或在 PR 中说明已有告警 |
| 命令行输出 `Error: Building with plugins requires symlink support. Please enable Developer Mode in your system settings.` | Windows 未启用符号链接支持 | 在 PowerShell 中运行 `start ms-settings:developers`，打开“开发者模式”后重试 |

遇到无法判断的问题时,不妨把错误发给deepseek询问。如果你觉得这是每一个新手都可能遇见的问题，可以向**文档站**仓库[提出Issue](https://github.com/The-Brotherhood-of-SCU/Bugaoshan_docs_page/issues)。
