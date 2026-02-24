[English](#English)

# 快速入门

自 0.5.0 起，整合包里附带一张地图，以助于快速入门
![CBRC tutorial](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/CBRC%20tutorial.png)

## 沿此路开始游戏

![Start game path](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Start%20game%20path.png)

沿着大厅的彩虹地毯走一圈，途径多个命令方块

### 读取配置
> _/cbr game load_

![Read config](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Read%20config.png)

### 加入游戏
> _/cbr team join_

![Join the game](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Join%20the%20game.png)

- 加入指定队伍：_/cbr team join [队伍 ID]_
- 邀请玩家加入队伍：_/cbr team invite [玩家名]_
- 申请加入队伍：_/cbr team request [玩家名]_
- 离开游戏：_/cbr team leave_

### 初始化游戏
> _/cbr game init_

![Initialize the game](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Initialize%20the%20game.png)

默认会将玩家传送至大厅
> 在[游戏配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#游戏配置)更改`teleportWhenInitGame`至`false`可禁用

- 一键组单人队伍：_/cbr team build @a 1 true_
- 一键组双人队伍：_/cbr team build @a 2 true_
- 为新玩家（无队伍）组双人队伍：_/cbr team build @a 2 false_

### 开始游戏
> _/cbr game start_

![Start the game](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Start%20the%20game.png)

### 观战游戏
> _/cbr game spectate_

![Spectate game](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Spectate%20game.png)

- 默认需要队伍被淘汰后才能执行
> 在[游戏配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#游戏配置)更改`spectateAfterTeamEliminated`至`false`，可使队伍未被淘汰时依旧能观战
- 默认允许非游戏玩家观战
> 在[游戏配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#游戏配置)更改`onlyGamePlayerSpectate`至`true`可禁止非游戏玩家观战

### 返回至大厅
> _/cbr game toLobby_

![Back to lobby](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Back%20to%20lobby.png)

在任意时候均可手动输入指令执行；或点击游戏结束后的`[观战]`
> **如在游戏中执行，将直接被淘汰**

### 结束游戏
> _/cbr game stop_

![Stop the game](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Stop%20the%20game.png)

提前终止游戏，不会产生赢家

## 修改游戏配置

### 重新读取配置

![Reload all configs from the disk](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Reload%20all%20configs%20from%20the%20disk.png)

使用 _/cbr reload_ 可一键重新读取所有模组配置；也可以使用 _/cbr reload game gamerule_ 等具体类别
- 如果仅有一个配置文件中包含`"default": true`词条，将默认选中，否则不保证默认选中的配置文件，如下所示
```json
[
	{
		"id": 0,
		"default": true, // 👈添加 default
		"name": "BattleRoyale Erangel 881x881",
		"color": "#FFFFFFAA",
		"modConfigManager": {
			// ...
		}
		// 其余内容
	}
]
```

### 一键切换预设配置

![Switch configs to profile](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Switch%20configs%20to%20profile.png)

使用 _/cbr utility profile load [id]_ 一键切换多个配置文件
- 使用[保存配置预设](https://github.com/XColorful/BattleRoyale/wiki/Utility-command#保存配置预设)指令一键保存当前选中的配置组合： _/cbr utility profile save_ 

### 更改大厅位置

![Set the lobby](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Set%20the%20lobby.png)

1. 更改[大逃杀规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#大逃杀规则配置)的`lobbyCenter`
2. [重新读取配置](#重新读取配置)或重启游戏
3. [切换游戏规则配置文件](https://github.com/XColorful/BattleRoyale/wiki/Config-command#大逃杀游戏配置)
```json
[
	{
		"gameId": 0,
		"gameName": "Erangel 100 4",
		"color": "#FFFFFFAA",
		"battleroyale": {
			// ...
			"lobbyCenter": "3816.000000,14.000000,-3624.000000", // 👈修改lobbyCenter
			"lobbyDimension": "555.000000,555.000000,555.000000",
			"lobbyMuteki": true,
			"lobbyHeal": true,
			"lobbyChangeGamemode": true,
			"lobbyTeleportDropInventory": false,
			"lobbyTeleportClearInventory": true,
			// ...
		}
		// 其余内容
	}
]
```

### 切换地图

![Zone offset guide](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Zone%20offset%20guide.png)

1. 使用指令[区域偏移](https://github.com/XColorful/BattleRoyale/wiki/Game-command#区域偏移)修改地图中心坐标，_y_ 分量建议为 0
> 例如地图的中心点在`123,64,456`，那么推荐使用 _/cbr game offset 123.0 0.0 456.0_
2. 如果地图尺寸有变，需要切换[区域配置](https://github.com/XColorful/BattleRoyale/wiki/Zone-config)；或专门制作后[重载配置](https://github.com/XColorful/BattleRoyale/wiki/Reload-command#区域配置)，再[切换配置](https://github.com/XColorful/BattleRoyale/wiki/Config-command#大逃杀游戏配置)

![Modify the zone configs](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Modify%20the%20zone%20configs.png)

区域配置较为复杂，但模组提供了诸多可复用的配置，只需要修改第一个区域的维度（圆形半径、正方形半边长）即可，例如对于`881x881_casual.json`：
- 修改`"fixed":"x,y,z"`的 _x_ 和 _z_ 分量，即可修改区域维度
- 默认生成的区域配置中，后续的区域都已基于`"zoneId": 0`的区域维度进行相对比例的计算，而不需要逐个修改
```json
[
	{
		"zoneId": 0,
		"zoneName": "Blue border",
		// ...
		"zoneFunc": {
			// ...
		},
		"zoneShape": {
			"zoneShapeType": "circle", // 通常为圆形或者方形
			"start": {
				"center": {
					// ...
				},
				"dimension": {
					"dimensionType": "fixed",
					"fixed": "440.5,384.0,440.5", // 👈修改这里
					"randomRange": 0.0,
				},
				// ...
			},
			// ...
		},
		// ...
	}, 
	// 其余区域
]
```
- 修改`"randomRange":正方形半边长`，即可以大地图中心，随机选取小地图
```json
[
	{
		"zoneId": 0,
		"zoneName": "Blue border",
		// ...
		"zoneFunc": {
			// ...
		},
		"zoneShape": {
			"zoneShapeType": "circle", // 通常为圆形或者方形
			"start": {
				"center": {
					"centerType": "fixed",
					"fixed": "0.0,-64.0,0.0",
					"randomRange": 3400.0, // 👈修改这里
					// ...
				},
				// ...
			},
			// ...
		},
		// ...
	}, 
	// 其余区域
]
```

3. 如果修改的区域尺寸差距过大，还需要切换或修改[出生配置](https://github.com/XColorful/BattleRoyale/wiki/Spawn-config)，这决定了游戏开始时玩家刷新的位置

## 更多教程
> 💡点击查看[自定义大逃杀Wiki](https://github.com/XColorful/BattleRoyale/wiki)，包含模组各功能说明

![More tutorial](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/More%20tutorial.png)

整合包以[自定义大逃杀](https://github.com/XColorful/BattleRoyale)为核心，并不局限于单一游戏形式/整合包，但有一些特别的功能：
- 如果你是一个**生存服**服主
> 你可能需要[生存模式大厅](https://github.com/XColorful/BattleRoyale/wiki/Utility-config#生存模式大厅)来跨纬度传送和自动物品管理，以及物资刷新机制的[方块实体白名单](https://github.com/XColorful/BattleRoyale/wiki/Performance-config#公共设置)
> ![Set the lobby](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Set%20the%20lobby.png)
- 如果你的服务器需要占用**记分板**/用指令获取游戏数据
> 修改[统计数据配置](https://github.com/XColorful/BattleRoyale/wiki/Stats-config)以显示自定义侧边栏或利用同步的游戏信息来触发红石电路
> ![Scoreboard](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Scoreboard.png)
- 如果你需要随机[TaCZ枪械](https://github.com/MCModderAnchor/TACZ)大乱斗/**随机物品物资刷新**
> 模组可以[自动生成物资刷新配置](https://github.com/XColorful/BattleRoyale/wiki/Utility-command#生成物资刷新配置文件)，无需手写战利品表
> ![Modify the loot configs](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Modify%20the%20loot%20configs.png)
- 如果你需要在一个存档里设置多个游戏地图
> 了解[区域偏移](https://github.com/XColorful/BattleRoyale/wiki/Game-command#区域偏移)并保存各游戏地图中心坐标
> 
> ![Zone offset and change game map](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Zone%20offset%20and%20change%20game%20map.png)
> 
> 对于不同的[区域配置](https://github.com/XColorful/BattleRoyale/wiki/Zone-config)，可以用`区域控制器`（方块）让玩家自行切换，也可以配合连锁命令方块[指定切换](https://github.com/XColorful/BattleRoyale/wiki/Config-command#大逃杀游戏配置)的[区域配置](https://github.com/XColorful/BattleRoyale/wiki/Zone-config)
> ![Zone controller](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Zone%20controller.png)
- 如果你需要修改成其他玩法（例如魔法大逃杀）
> 你可能需要定制[物资刷新配置](https://github.com/XColorful/BattleRoyale/wiki/Configuration-introduction#物资刷新配置)
- 如果你的服务器 TPS 非常告急，甚至容不得 5ms 的卡顿
> 在[游戏刷新设置](https://github.com/XColorful/BattleRoyale/wiki/Performance-config#游戏刷新设置)尽可能降低物资刷新速率

## 模组开发

如果你是一个开发者/想要深入了解该模组：
- 查看[模组文档](https://github.com/XColorful/BattleRoyale/tree/HEAD/docs)
- 如果你想要监听游戏事件/编写扩展模组，查看[模组扩展教程](https://github.com/XColorful/BattleRoyale/blob/HEAD/docs/architecture/Home.md#模组扩展教程)
- 如果需要深度了解，先阅读模组的[设计哲学](https://github.com/XColorful/BattleRoyale/blob/HEAD/docs/architecture/design/design-philosophy.md)或[快速入门](https://github.com/XColorful/BattleRoyale/blob/HEAD/docs/Quick%20start%20guide.md)，再查看[架构总览](https://github.com/XColorful/BattleRoyale/blob/HEAD/docs/architecture/Home.md)和[API 索引](https://github.com/XColorful/BattleRoyale/blob/HEAD/docs/architecture/api/api-index.md)
- 如果你只是想要获取最新版模组，却又不会写模组：在了解如何[部署环境](https://github.com/XColorful/BattleRoyale/wiki/Deploy-Environment)后克隆模组[Github仓库](https://github.com/XColorful/BattleRoyale)即可手动编译

如需扩展游戏模式，参考死斗模式的代码实现及如何切换，做成扩展模组
> ![Switch to DeathMatch mode](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Switch%20to%20DeathMatch%20mode.png)

# English

Since 0.5.0, a map is included in the modpack to help with quick start
![CBRC tutorial](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/CBRC%20tutorial.png)

## Start game along this path

![Start game path](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Start%20game%20path.png)

Walk around the rainbow carpet in the lobby and pass through multiple command blocks

### Read config
> _/cbr game load_

![Read config](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Read%20config.png)

### Join the game
> _/cbr team join_

![Join the game](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Join%20the%20game.png)

- Join specific team: _/cbr team join [team ID]_
- Invite player to join team: _/cbr team invite [player name]_
- Request to join team: _/cbr team request [player name]_
- Leave the game: _/cbr team leave_

### Initialize the game
> _/cbr game init_

![Initialize the game](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Initialize%20the%20game.png)

Players will be teleported to the lobby by default
> Change `teleportWhenInitGame` to `false` in [Game config](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#Game-config) to disable it
- Auto build solo team: _/cbr team build @a 1 true_
- Auto build dual team: _/cbr team build @a 2 true_
- Build dual team for new players (without teams): _/cbr team build @a 2 false_

### Start the game
> _/cbr game start_

![Start the game](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Start%20the%20game.png)

### Spectate game
> _/cbr game spectate_

![Spectate game](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Spectate%20game.png)

- Execution is only allowed after the team is eliminated by default
> Change `spectateAfterTeamEliminated` to `false` in [Game config](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#Game-config) to allow spectating while the team is not eliminated
- Non-game players are allowed to spectate by default
> Change `onlyGamePlayerSpectate` to `true` in [Game config](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#Game-config) to prohibit non-game players from spectating

### Back to lobby
> _/cbr game toLobby_

![Back to lobby](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Back%20to%20lobby.png)

Execute by manually entering the command at any time; or click `[Spectate]` after the game ends
> **If executed during the game, the player will be eliminated directly**

### Stop the game
> _/cbr game stop_

![Stop the game](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Stop%20the%20game.png)

Terminate the game early; no winner will be generated

## Modify game configs

### Reload configs

![Reload all configs from the disk](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Reload%20all%20configs%20from%20the%20disk.png)

Use _/cbr reload_ to reload all mod configs with one click; specific categories like _/cbr reload game gamerule_ are also available
- If only one config file contains the `"default": true` entry, it will be selected by default; otherwise, the default selected config file is not guaranteed, as shown below
```json
[
	{
		"id": 0,
		"default": true, // 👈Add default
		"name": "BattleRoyale Erangel 881x881",
		"color": "#FFFFFFAA",
		"modConfigManager": {
			// ...
		}
		// Other content
	}
]
```

### Switch to profile configs with one click

![Switch configs to profile](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Switch%20configs%20to%20profile.png)

Use _/cbr utility profile load [id]_ to switch multiple config files with one click
- Use the [Save config profile](https://github.com/XColorful/BattleRoyale/wiki/Utility-command#Save-config-profile) command to save the currently selected config combination: _/cbr utility profile save_ 

### Change the lobby position

![Set the lobby](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Set%20the%20lobby.png)

1. Change `lobbyCenter` in [BattleRoyale gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#BattleRoyale-gamerule)
2. [Reload configs](#Reload-configs) or restart the game
3. [Switch gamerule config file](https://github.com/XColorful/BattleRoyale/wiki/Config-command#BattleRoyale-config)
```json
[
	{
		"gameId": 0,
		"gameName": "Erangel 100 4",
		"color": "#FFFFFFAA",
		"battleroyale": {
			// ...
			"lobbyCenter": "3816.000000,14.000000,-3624.000000", // 👈Modify lobbyCenter
			"lobbyDimension": "555.000000,555.000000,555.000000",
			"lobbyMuteki": true,
			"lobbyHeal": true,
			"lobbyChangeGamemode": true,
			"lobbyTeleportDropInventory": false,
			"lobbyTeleportClearInventory": true,
			// ...
		}
		// Other content
	}
]
```

### Switch map

![Zone offset guide](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Zone%20offset%20guide.png)

1. Use the [Zone offset](https://github.com/XColorful/BattleRoyale/wiki/Game-command#Zone-offset) command to modify the map center coordinates; the _y_ component is recommended to be 0
> For example, if the center point of the map is at `123,64,456`, it is recommended to use _/cbr game offset 123.0 0.0 456.0_
2. If the map size changes, switch the [Zone config](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#English); or [Reload config](https://github.com/XColorful/BattleRoyale/wiki/Reload-command#Zone-config) after manual creation, and then [Switch config](https://github.com/XColorful/BattleRoyale/wiki/Config-command#BattleRoyale-config)

![Modify the zone configs](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Modify%20the%20zone%20configs.png)

Zone configuration is complex, but the mod provides many reusable configs; only the dimensions (circular radius, square half-side length) of the first zone need to be modified, for example, for `881x881_casual.json`:
- Modify the _x_ and _z_ components of `"fixed":"x,y,z"` to change the zone dimensions
- In the default generated zone config, subsequent zones are already calculated based on the relative proportions of the dimensions of `"zoneId": 0`, so they do not need to be modified one by one
```json
[
	{
		"zoneId": 0,
		"zoneName": "Blue border",
		// ...
		"zoneFunc": {
			// ...
		},
		"zoneShape": {
			"zoneShapeType": "circle", // Usually circle or square
			"start": {
				"center": {
					// ...
				},
				"dimension": {
					"dimensionType": "fixed",
					"fixed": "440.5,384.0,440.5", // 👈Modify here
					"randomRange": 0.0,
				},
				// ...
			},
			// ...
		},
		// ...
	}, 
	// Other zones
]
```
- Modify `"randomRange":square half-side length` to randomly select a small map centered on the large map center
```json
[
	{
		"zoneId": 0,
		"zoneName": "Blue border",
		// ...
		"zoneFunc": {
			// ...
		},
		"zoneShape": {
			"zoneShapeType": "circle", // Usually circle or square
			"start": {
				"center": {
					"centerType": "fixed",
					"fixed": "0.0,-64.0,0.0",
					"randomRange": 3400.0, // 👈Modify here
					// ...
				},
				// ...
			},
			// ...
		},
		// ...
	}, 
	// Other zones
]
```

3. If the modified zone size difference is too large, the [Spawn config](https://github.com/XColorful/BattleRoyale/wiki/Spawn-config#English) also needs to be switched or modified, which determines the location where players spawn when the game starts

## More tutorials
> 💡Click to view [Custom BattleRoyale Wiki](https://github.com/XColorful/BattleRoyale/wiki#English), which contains descriptions of various mod functions

![More tutorial](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/More%20tutorial.png)

The modpack is centered on [自定义大逃杀](https://github.com/XColorful/BattleRoyale) and is not limited to a single game form/modpack, but it has some special functions:
- If you are a **survival server** owner
> You may need the [Survival mode lobby](https://github.com/XColorful/BattleRoyale/wiki/Utility-config#Survival-mode-lobby) for cross-dimensional teleportation and automatic item management, as well as the [Block entity whitelist](https://github.com/XColorful/BattleRoyale/wiki/Performance-config#General-Settings)
> ![Set the lobby](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Set%20the%20lobby.png)
- If your server needs to occupy the **scoreboard**/get game data via commands
> Modify the [Stats config](https://github.com/XColorful/BattleRoyale/wiki/Stats-config#English) to display a custom sidebar or use synchronized game information to trigger redstone circuits
> ![Scoreboard](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Scoreboard.png)
- If you need random [TaCZ gun](https://github.com/MCModderAnchor/TACZ) melees/**random item loot generation**
> The mod can [Automatically generate loot configs](https://github.com/XColorful/BattleRoyale/wiki/Utility-command#Generate-loot-spawner-configuration) without manually writing loot tables
> ![Modify the loot configs](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Modify%20the%20loot%20configs.png)
- If you need to set up multiple game maps in one save
> Learn [Zone offset](https://github.com/XColorful/BattleRoyale/wiki/Game-command#Zone-offset) and save the center coordinates of each game map
> 
> ![Zone offset and change game map](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Zone%20offset%20and%20change%20game%20map.png)
> 
> For different [Zone config](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#English), you can use the `Zone controller` (block) to let players switch by themselves, or use chain command blocks to [Specify the switch](https://github.com/XColorful/BattleRoyale/wiki/Config-command#BattleRoyale-config) of the [Zone config](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#English)
> 
> ![Zone controller](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Zone%20controller.png)
- If you need to modify it into other gameplays (e.g., Magic Battle Royale)
> You may need to customize the [Loot configs](https://github.com/XColorful/BattleRoyale/wiki/Configuration-introduction#Loot)
- If your server TPS is extremely critical and cannot even tolerate a 5ms lag
> Reduce the loot generation rate as much as possible in [In-game loot Settings](https://github.com/XColorful/BattleRoyale/wiki/Performance-config#In-game-loot-Settings)

## Mod development

If you are a developer/want to learn more about the mod:
- View [Mod ducumentation](https://github.com/XColorful/BattleRoyale/tree/HEAD/docs)
- If you want to listen to game events/write extension mods, view [Mod Addon Tutorial](https://github.com/XColorful/BattleRoyale/blob/HEAD/docs/architecture/Home.md#Mod-Addon-Tutorial)
- For in-depth understanding, read the [Design Philosophy](https://github.com/XColorful/BattleRoyale/blob/HEAD/docs/architecture/design/design-philosophy.md#English) or [Quick start guide](https://github.com/XColorful/BattleRoyale/blob/HEAD/docs/Quick%20start%20guide.md#English) first, and then view the [Architecture Overview](https://github.com/XColorful/BattleRoyale/blob/HEAD/docs/architecture/Home.md#English) and [API Index](https://github.com/XColorful/BattleRoyale/blob/HEAD/docs/architecture/api/api-index.md#English)
- If you just want to get the latest version of the mod but don't know how to write mods: learn how to [Deploy Environment](https://github.com/XColorful/BattleRoyale/wiki/Deploy-Environment#English), clone the mod [Github repository](https://github.com/XColorful/BattleRoyale) and compile it manually

To extend the game mode, refer to the code implementation of DeathMatch mode and how to switch, and make it into an extension mod
> ![Switch to DeathMatch mode](https://github.com/XColorful/Custom-BattleRoyale-Complete/raw/HEAD/pic/Switch%20to%20DeathMatch%20mode.png)