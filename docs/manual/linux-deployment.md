---
order: 8
title: Linux 部署指南
icon: mdi:linux
---

# Linux 部署指南

Linux 提供随正式版发布的 `linux_x64.tar.gz` 预编译包，也可按本指南从源码构建。

本页介绍在 Linux 电脑上从源码构建并运行不高山上，适用于 Ubuntu、Debian、Arch Linux 等能够安装 Flutter Linux 桌面依赖的发行版。

> 本指南基于主仓库的 Linux 配置整理。不同发行版的软件包名称可能略有差异，安装前请以本机软件源中的名称为准。

## 一、安装系统依赖

### Ubuntu / Debian

打开终端，安装 Flutter 编译工具与 GTK 桌面依赖：

```bash
sudo apt update
sudo apt install -y \
  git curl unzip xz-utils zip \
  clang cmake ninja-build pkg-config libgtk-3-dev liblzma-dev \
  libsecret-1-dev libepoxy-dev \
  libwayland-dev
```

Linux 端不提供原生 WebView，因此无需安装 WPE WebKit、WPEBackend-fdo 或 libwpe。

### Arch Linux

```bash
sudo pacman -Syu --needed \
  git curl unzip xz zip \
  clang cmake ninja pkgconf gtk3 libsecret libepoxy wayland
```

Fedora、openSUSE 等发行版请安装对应的 GTK 3、Clang、CMake、Ninja、pkg-config、libsecret、libepoxy 和 Wayland 开发包。

## 二、安装 Flutter

按照 [Flutter 官方 Linux 安装说明](https://docs.flutter.dev/get-started/install/linux) 安装 stable 通道的 Flutter SDK，并将 `flutter` 加入 `PATH`。安装完成后检查环境：

```bash
flutter --version
flutter doctor -v
flutter config --enable-linux-desktop
```

如果 `flutter doctor -v` 报告 Linux toolchain 或 GTK 缺失，请先补齐系统依赖，再继续后面的步骤。Flutter 版本应满足主仓库 [`pubspec.yaml`](https://github.com/The-Brotherhood-of-SCU/Bugaoshan/blob/main/pubspec.yaml) 中的 SDK 约束。

## 三、获取源码并构建

```bash
git clone https://github.com/The-Brotherhood-of-SCU/Bugaoshan.git
cd Bugaoshan

flutter pub get
flutter build linux --release
```

构建成功后，可执行文件位于：

```text
build/linux/x64/release/bundle/Bugaoshan
```

## 四、运行应用

直接从构建目录运行：

```bash
./build/linux/x64/release/bundle/Bugaoshan
```

开发或排查问题时，也可以使用 Flutter 直接启动：

```bash
flutter run -d linux
```

## 五、安装到当前用户

如果希望像普通桌面程序一样保留一份固定副本，可以安装到当前用户目录，不需要写入系统目录：

```bash
install -d "$HOME/.local/opt/bugaoshan" "$HOME/.local/bin"
cp -a build/linux/x64/release/bundle/. "$HOME/.local/opt/bugaoshan/"
ln -sfn "$HOME/.local/opt/bugaoshan/Bugaoshan" "$HOME/.local/bin/bugaoshan"
```

然后运行：

```bash
"$HOME/.local/bin/bugaoshan"
```

如果系统找不到 `bugaoshan` 命令，把下面一行加入 shell 配置文件（例如 `~/.bashrc` 或 `~/.zshrc`），重新打开终端：

```bash
export PATH="$HOME/.local/bin:$PATH"
```

## 六、更新应用

源码目录中执行以下命令即可更新并重新安装：

```bash
cd Bugaoshan
git pull --ff-only
flutter pub get
flutter build linux --release

rm -rf "$HOME/.local/opt/bugaoshan"
install -d "$HOME/.local/opt/bugaoshan"
cp -a build/linux/x64/release/bundle/. "$HOME/.local/opt/bugaoshan/"
```

应用数据不在构建目录中；更新前请退出正在运行的应用，不要删除自己的配置目录。

## 常见问题

### 提示缺少 GTK 或 Wayland 运行库

从终端启动应用，根据报错安装当前发行版对应的 GTK 3、libsecret、libepoxy 和 Wayland 运行库。可用 `ldd build/linux/x64/release/bundle/Bugaoshan | grep 'not found'` 检查动态库依赖。

### 通知或志愿四川显示“用浏览器打开此页面”

Linux 端不提供应用内网页视图。通知公告、志愿四川等依赖网页的功能会显示交接页，点击按钮即可用系统默认浏览器打开目标地址，也可以复制链接后在浏览器中手动打开。登录与附件下载都在浏览器中完成；研究生课表导入仅保留直连路径。

### `flutter build linux` 提示找不到 Linux 设备

先执行：

```bash
flutter config --enable-linux-desktop
flutter devices
flutter doctor -v
```

确认 Linux toolchain 没有错误后，再运行 `flutter run -d linux` 或 `flutter build linux --release`。

### 想卸载用户目录安装

退出应用后删除本指南创建的程序副本和启动链接即可：

```bash
rm -rf "$HOME/.local/opt/bugaoshan"
rm -f "$HOME/.local/bin/bugaoshan"
```

这不会自动删除应用配置和缓存；如果还需要清理个人数据，请先确认对应目录，避免误删其他应用文件。
