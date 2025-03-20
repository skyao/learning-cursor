---
title: "在linux mint上安装"
linkTitle: "linux mint"
weight: 10
date: 2024-12-07
description: >
  在linux mint22上安装cursor
---

## 下载

下载 linux 的安装文件，会得到类似 `Cursor-0.47.8-82ef0f61c01d079d1b7e5ab04d88499d5af500e3.deb.glibc2.25-x86_64.AppImage` 这样的文件。

## 安装

需要设置可执行权限，然后运行它进行安装：

```bash
chmod +x Cursor-0.47.8-82ef0f61c01d079d1b7e5ab04d88499d5af500e3.deb.glibc2.25-x86_64.AppImage

./Cursor-0.47.8-82ef0f61c01d079d1b7e5ab04d88499d5af500e3.deb.glibc2.25-x86_64.AppImage      
```

安装界面：

![](images/install.jpg)

"Add terminal command" 是用来从终端中启动，因为我同时还使用标准版本的vscode，因此我选择 "+ Install cursor"。但是很遗憾，报错。

配置 vs code 的 extension：

![](images/extensions.jpg)

登录 cursor：

![](images/login.jpg)

完成后打开的 cursor 界面：

![](images/cursor.jpg)

发现其实没所谓安装过程，这个下载的文件就是应用启动文件。

因此转移到特定目录，方便以后使用:

```bash
mkdir -p ~/work/soft/cursor
mv Cursor-0.47.8-82ef0f61c01d079d1b7e5ab04d88499d5af500e3.deb.glibc2.25-x86_64.AppImage ~/work/soft/cursor/cursor.AppImage
cd ~/work/soft/cursor                               
./cursor.AppImage 
```

但这个启动的方式，无法固定在面板，也无法固定在 dock，甚至 Synapse 都找不到它。总不能每次都用终端启动吧？

## 启动

google 之后找到的方法是这样的:

https://forum.cursor.com/t/how-to-open-cursor-from-terminal/3757/10

`ctrl + shift + p` 打开 Command Palette，然后运行 `Shell Command :Install Cursor command`。

但很遗憾，在 linux mint 22 （基于ubuntu24.04）下，找不到 `Shell Command :Install Cursor command`。看回帖有人也遇到和我一样的问题：

![](images/no_shell_command.jpg)

### 命令行启动

可以通过其他方法来解决这个问题：

```bash
vi ~/.zshrc
```

增加以下内容:

```bash
# cursor
cursor() {
  # Run the cursor command and suppress background process output completely
  (nohup ~/work/soft/cursor/cursor.AppImage "$@" >/dev/null 2>&1 &)
} 
```

重新载入：

```bash
source ~/.zshrc
```

之后在终端中输入 `cursor` 就可以启动 cursor 了，而且关闭这个终端也不会造成 cursor 进程退出。

### 应用图标启动

从命令行启动终究有点麻烦，可以自己建立应用程序，然后点击启动 cursor。

从下列地址下载一个 cursor 的图标文件，放到 ` ~/work/soft/cursor/` 目录：

```bash
curl -o ~/work/soft/cursor/cursor-icon.svg https://www.cursor.com/favicon.svg
```

然后新建一个 cursor.desktop：

```bash
cd ~/.local/share/applications/

vi cursor.desktop
```

内容为：

```bash
[Desktop Entry]
Name=Cursor
Comment=start cursor
Exec=gnome-terminal -- bash -c "~/work/soft/cursor/cursor.AppImage;"
Icon=~/work/soft/cursor/cursor-icon.png
Terminal=false
Type=Application
Categories=Development;Application;
```

增加执行权限：  

```bash
chmod +x cursor.desktop
```

进入 `~/.local/share/applications/` 目录，双击 cursor 的图标就可以启动 cursor 了。

启动后，右键选择 "keep in Dock"，以后就可以从 Dock 直接启动了。

如果要增加桌面启动，复制这个 cursor.desktop 文件到桌面即可。

正常情况下，linux mint 默认的 Cinnamon Menu 应用启动器会识别到 `~/.local/share/applications/` 下的这个 cursor 应用，然后将其放置在开始菜单中的 Programming 分类中，从这里也可以打开 cursor。另外 Synapse 之类的应用程序启动器也可以识别到 cursor 了，alt + g 快捷键也可以方便的启动 cursor。









