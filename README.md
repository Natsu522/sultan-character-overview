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
