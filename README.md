# Sultan Character Overview

English | [中文](#中文)

Sultan Character Overview is a read-only BepInEx IL2CPP mod for *Sultan's Game*. It adds an in-game IMGUI window that displays the player's currently owned character cards and their live attributes from the save file.

This project is an unofficial fan-made mod and is not affiliated with or endorsed by DoubleCross or the developers/publishers of *Sultan's Game*.

## Features

- Toggle the overview window with `F8`.
- Read-only: the mod does not modify save files or game state.
- Shows currently owned character cards, including protagonist cards.
- Reads live attribute values from the current save file.
- Supports search, sorting, vertical scrolling, horizontal scrolling, and auto-refresh.
- Keeps the name column fixed while scrolling attributes horizontally.
- Default attribute order:
  - Physique
  - Charm
  - Wisdom
  - Conceal
  - Battle
  - Social
  - Survival
  - Support
  - Passion
- Additional visible numeric attributes are appended automatically.
- Left-click and drag the title bar to move the window.
- Left-click and drag the bottom-right handle to resize the window.

## Requirements

- Windows
- *Sultan's Game*
- BepInEx 6 IL2CPP installed for the game

The current build targets the BepInEx 6 IL2CPP runtime used by the game. It is not a BepInEx 5 Mono plugin.

## What Is BepInEx 6 IL2CPP?

BepInEx is the mod loader. It starts before the game finishes loading and then loads plugin DLLs from the `BepInEx\plugins` folder.

Unity games usually use one of two scripting backends:

- **Mono**
- **IL2CPP**

*Sultan's Game* is an IL2CPP Unity game, so it needs the **BepInEx 6 Unity IL2CPP Windows x64** build. Using BepInEx 5, a Mono build, or the wrong CPU architecture can make the plugin fail to load.

Choose a file with a name like:

```text
BepInEx-Unity.IL2CPP-win-x64-6.0.0-be.xxx+xxxxxxx.zip
```

Do not choose files containing:

```text
Unity.Mono
win-x86
NET.Framework
NET.CoreCLR
BepInEx 5.x
```

## Installing BepInEx 6 IL2CPP

BepInEx is the mod loader that allows the game to load plugin DLLs. *Sultan's Game* uses Unity IL2CPP, so this mod requires a BepInEx 6 IL2CPP x64 build. Do not use the Mono build.

1. Download a BepInEx 6 Unity IL2CPP Windows x64 build from the official BepInEx bleeding edge builds page:

```text
https://builds.bepinex.dev/projects/bepinex_be
```

The correct archive name should look similar to:

```text
BepInEx-Unity.IL2CPP-win-x64-6.0.0-be.xxx+xxxxxxx.zip
```

2. Extract the archive into the game folder, next to:

```text
Sultan's Game.exe
```

3. Start the game once.

4. The first launch after installing BepInEx may take longer than usual because BepInEx generates IL2CPP interop files.

5. If BepInEx was installed correctly, the game folder should contain a `BepInEx` folder and log files such as:

```text
BepInEx\LogOutput.log
```

The log should contain lines similar to:

```text
BepInEx 6.0.0-be.xxx
Running under Unity 2022
Loading [Sultan Character Overview ...]
Chainloader startup complete
```

6. After BepInEx works, install this mod by placing `SultanCharacterOverview.dll` into:

```text
BepInEx\plugins\SultanCharacterOverview\
```

If the mod does not load, check these common mistakes first:

- The DLL is not inside `BepInEx\plugins\SultanCharacterOverview\`.
- You installed a Mono build instead of `Unity.IL2CPP`.
- You installed a 32-bit `win-x86` build instead of `win-x64`.
- You installed BepInEx 5 instead of BepInEx 6.
- The game was not started once after installing BepInEx.

## Installation

1. Install BepInEx 6 IL2CPP for *Sultan's Game*.
2. Download the release zip or `SultanCharacterOverview.dll`.
3. Place the DLL here:

```text
<Sultan's Game folder>\BepInEx\plugins\SultanCharacterOverview\SultanCharacterOverview.dll
```

Example:

```text
Sultan's Game
└─ BepInEx
   └─ plugins
      └─ SultanCharacterOverview
         └─ SultanCharacterOverview.dll
```

4. Start the game.
5. Press `F8` in game.

## Save Detection

The mod automatically searches the current Windows user's save directory:

```text
%USERPROFILE%\AppData\LocalLow\DoubleCross\SultansGame\SAVEDATA
```

It selects the newest Steam ID save folder that contains one of these files:

- `auto_save.json`
- `round_X.json`
- `round_X_end.json`

Save priority:

1. `auto_save.json`
2. Newest `round_X.json` or `round_X_end.json`

If auto-detection chooses the wrong folder, set `SaveDirectoryOverride` in the config file.

## Configuration

After the game runs once with the mod installed, BepInEx creates:

```text
<Sultan's Game folder>\BepInEx\config\natsu.sultansgame.characteroverview.cfg
```

Available options:

```ini
[Paths]
SaveDirectoryOverride =

[UI]
ToggleKey = F8
AutoRefreshSeconds = 3
ShowNameHoverTooltip = true
```

`SaveDirectoryOverride` can be set to a specific save folder, for example:

```text
C:\Users\YourName\AppData\LocalLow\DoubleCross\SultansGame\SAVEDATA\7656119xxxxxxxxxx
```

`AutoRefreshSeconds` controls automatic refresh while the window is open. Recommended value: `3`.

Set `AutoRefreshSeconds = 0` to disable auto-refresh.

## Build From Source

Requirements:

- .NET SDK
- A local *Sultan's Game* install with BepInEx 6 IL2CPP

Build:

```powershell
dotnet build .\src\SultanCharacterOverview\SultanCharacterOverview.csproj -c Release
```

Output:

```text
src\SultanCharacterOverview\bin\Release\SultanCharacterOverview.dll
```

The project file currently references BepInEx and Unity interop assemblies from the local game install. If your game is installed in a different path, update the `<HintPath>` values in:

```text
src\SultanCharacterOverview\SultanCharacterOverview.csproj
```

## Known Notes

- The window is implemented with Unity IMGUI.
- The mod reads save/config JSON files and merges base card attributes, save-time attribute changes, and equipment attributes.
- Attribute names and visibility come from the game's configuration files.
- The mod is intended for viewing data only.

---

# 中文

《苏丹的游戏》角色属性总览 MOD。基于 BepInEx 6 IL2CPP，在游戏内提供一个只读 IMGUI 窗口，用于查看当前玩家拥有的角色卡及其实时属性。

本项目为玩家自制非官方 MOD，与《苏丹的游戏》开发商/发行商无关，也未获得官方背书。

## 功能

- 按 `F8` 打开/关闭窗口。
- 只读查看，不修改存档或游戏状态。
- 显示当前拥有的角色卡，包括主角卡。
- 从当前存档读取实时属性。
- 支持搜索、排序、纵向滚动、横向滚动、自动刷新。
- 横向滚动时固定名称列。
- 默认属性顺序：
  - 体魄
  - 魅力
  - 智慧
  - 隐匿
  - 战斗
  - 社交
  - 生存
  - 支持
  - 激情
- 其他可见的数值属性会自动追加在后面。
- 左键拖动标题栏移动窗口。
- 左键拖动右下角手柄缩放窗口。

## 需求

- Windows
- 《苏丹的游戏》
- 已安装 BepInEx 6 IL2CPP

当前版本面向游戏使用的 BepInEx 6 IL2CPP 环境，不是 BepInEx 5 Mono 插件。

## BepInEx 6 IL2CPP 是什么？

BepInEx 是 MOD 加载器。它会在游戏启动时先运行，然后从 `BepInEx\plugins` 文件夹加载 MOD DLL。

Unity 游戏通常有两种脚本后端：

- **Mono**
- **IL2CPP**

《苏丹的游戏》是 Unity IL2CPP 游戏，所以需要安装 **BepInEx 6 Unity IL2CPP Windows x64** 版本。如果装成 BepInEx 5、Mono 版本，或者 32 位版本，MOD 很可能不会被加载。

你要下载的文件名应该类似：

```text
BepInEx-Unity.IL2CPP-win-x64-6.0.0-be.xxx+xxxxxxx.zip
```

不要下载文件名里包含这些内容的版本：

```text
Unity.Mono
win-x86
NET.Framework
NET.CoreCLR
BepInEx 5.x
```

## 安装 BepInEx 6 IL2CPP

BepInEx 是用于让游戏加载 MOD DLL 的加载器。《苏丹的游戏》使用 Unity IL2CPP，因此本 MOD 需要 BepInEx 6 IL2CPP x64 版本。不要使用 Mono 版本。

1. 从 BepInEx 官方 bleeding edge builds 页面下载 BepInEx 6 Unity IL2CPP Windows x64 构建：

```text
https://builds.bepinex.dev/projects/bepinex_be
```

正确压缩包的文件名应该类似：

```text
BepInEx-Unity.IL2CPP-win-x64-6.0.0-be.xxx+xxxxxxx.zip
```

2. 将压缩包内容解压到游戏目录，也就是这个文件所在的目录：

```text
Sultan's Game.exe
```

3. 启动游戏一次。

4. 第一次安装 BepInEx 后启动游戏可能会慢一些，因为 BepInEx 需要生成 IL2CPP interop 文件。

5. 如果 BepInEx 安装成功，游戏目录下应该会出现 `BepInEx` 文件夹和日志文件，例如：

```text
BepInEx\LogOutput.log
```

日志里通常能看到类似内容：

```text
BepInEx 6.0.0-be.xxx
Running under Unity 2022
Loading [Sultan Character Overview ...]
Chainloader startup complete
```

6. 确认 BepInEx 可用后，再将本 MOD 的 `SultanCharacterOverview.dll` 放入：

```text
BepInEx\plugins\SultanCharacterOverview\
```

如果 MOD 没有加载，优先检查这些常见问题：

- DLL 没有放在 `BepInEx\plugins\SultanCharacterOverview\` 里面。
- 装成了 Mono 版本，而不是 `Unity.IL2CPP`。
- 装成了 32 位 `win-x86`，而不是 `win-x64`。
- 装成了 BepInEx 5，而不是 BepInEx 6。
- 安装 BepInEx 后没有先启动过一次游戏。

## 安装

1. 为《苏丹的游戏》安装 BepInEx 6 IL2CPP。
2. 下载 Release 压缩包或 `SultanCharacterOverview.dll`。
3. 将 DLL 放到：

```text
<游戏目录>\BepInEx\plugins\SultanCharacterOverview\SultanCharacterOverview.dll
```

目录结构示例：

```text
Sultan's Game
└─ BepInEx
   └─ plugins
      └─ SultanCharacterOverview
         └─ SultanCharacterOverview.dll
```

4. 启动游戏。
5. 在游戏内按 `F8`。

## 存档识别

MOD 会自动搜索当前 Windows 用户的存档目录：

```text
%USERPROFILE%\AppData\LocalLow\DoubleCross\SultansGame\SAVEDATA
```

如果有多个 Steam ID 存档目录，会选择最近修改过、且包含下列文件之一的目录：

- `auto_save.json`
- `round_X.json`
- `round_X_end.json`

读取优先级：

1. `auto_save.json`
2. 最新的 `round_X.json` 或 `round_X_end.json`

如果自动识别错了，可以在配置文件里手动指定。

## 配置

游戏运行一次后，BepInEx 会生成配置文件：

```text
<游戏目录>\BepInEx\config\natsu.sultansgame.characteroverview.cfg
```

可配置项：

```ini
[Paths]
SaveDirectoryOverride =

[UI]
ToggleKey = F8
AutoRefreshSeconds = 3
ShowNameHoverTooltip = true
```

`SaveDirectoryOverride` 可以手动指定某个存档目录，例如：

```text
C:\Users\YourName\AppData\LocalLow\DoubleCross\SultansGame\SAVEDATA\7656119xxxxxxxxxx
```

`AutoRefreshSeconds` 控制窗口打开时的自动刷新间隔，推荐值为 `3`。

设置为 `0` 可关闭自动刷新。

## 从源码构建

需求：

- .NET SDK
- 本地《苏丹的游戏》目录
- 已安装 BepInEx 6 IL2CPP

构建：

```powershell
dotnet build .\src\SultanCharacterOverview\SultanCharacterOverview.csproj -c Release
```

输出：

```text
src\SultanCharacterOverview\bin\Release\SultanCharacterOverview.dll
```

项目文件当前引用本地游戏目录中的 BepInEx 和 Unity interop DLL。如果你的游戏路径不同，需要修改：

```text
src\SultanCharacterOverview\SultanCharacterOverview.csproj
```

中的 `<HintPath>`。

## 说明

- 窗口使用 Unity IMGUI 实现。
- MOD 会读取存档和游戏配置 JSON。
- 属性由基础卡牌属性、存档中的属性变化、装备属性合并得出。
- 属性名称和是否可见来自游戏配置。
- 本 MOD 仅用于查看数据。
