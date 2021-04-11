---
title: WSL
icon: windows
time: '2019-11-23T00:00:00.000Z'
category: Linux
---

# readme

WSL 可以直接在 Windows 系统上安装并运行 Linux。目前最新的版本是 WSL2。

## Ubuntu

Windows 上的功能有很大缺失。已知不能用 Snap。

## WSL 文件位置

```text
C:\Users\%USERNAME%\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs
```

## 重启 WSL

使用

```bash
net stop LxssManager
```

和

```bash
net start LxssManager
```

