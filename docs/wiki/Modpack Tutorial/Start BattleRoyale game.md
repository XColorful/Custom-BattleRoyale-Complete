# 开始大逃杀游戏

> 详细指令Wiki：[大逃杀指令](https://github.com/XColorful/BattleRoyale/wiki/Game-command)

## 常见问题排除
在开始大逃杀游戏前有必要了解几个常见问题：

- 队伍规模不符合预期：[查询选定游戏配置](https://github.com/XColorful/BattleRoyale/wiki/Game-command#查询选定游戏配置)并检查[大逃杀规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#大逃杀规则配置)
- 大厅位置错误：[查询选定游戏配置](https://github.com/XColorful/BattleRoyale/wiki/Game-command#查询选定游戏配置)并检查[大逃杀规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#大逃杀规则配置)
> 如果修改了配置，需要视作进行了[修改大逃杀配置](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/Edit-CBR-configuration)，并需要[切换配置](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/Switch-configuration)

## 一般步骤

> 尽管[自定义大逃杀](https://github.com/XColorful/BattleRoyale)提供了一键[开始游戏](https://github.com/XColorful/BattleRoyale/wiki/Game-command#开始游戏)的可能，你仍应该了解开始游戏前的各个阶段

### 读取配置
> 通常情况下直接初始化游戏即可，非自动执行时一般为调试问题或者启用大厅传送

执行[读取配置](https://github.com/XColorful/BattleRoyale/wiki/Game-command#读取配置)指令
- 成功读取将使[传送至大厅](https://github.com/XColorful/BattleRoyale/wiki/Game-command#传送至大厅)生效，若[游戏配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#游戏配置)中未启用保留队伍分配或修改了[大逃杀规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#大逃杀规则配置)的队伍规模，将导致重置队伍

### 初始化游戏

执行[初始化游戏](https://github.com/XColorful/BattleRoyale/wiki/Game-command#初始化游戏)指令
- 如在[大逃杀规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#大逃杀规则配置)中启用自动加入游戏，则自动执行一次队伍分配，并且新加入服务器的玩家也会新建队伍或发送入队请求
- [原版规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#原版规则配置)仅在此阶段应用一次且发生在自动分配队伍之后
- 立即对游戏玩家应用[原版规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#原版规则配置)设定的游戏模式，并传送至大厅
- 在此阶段预计算出生信息（位置、随机偏移等），不在日志中显示
> 可以在这个阶段与玩家商量原版规则，临时修改而无需[重载配置](https://github.com/XColorful/BattleRoyale/wiki/Reload-command)，不在开始游戏时应用原版规则是刻意为之

提醒玩家使用[队伍管理](https://github.com/XColorful/BattleRoyale/wiki/Team-command)指令而不是原版队伍指令
> [自定义大逃杀](https://github.com/XColorful/BattleRoyale)的队伍管理独立于原版队伍系统

### 开始游戏

执行[开始游戏](https://github.com/XColorful/BattleRoyale/wiki/Game-command#开始游戏)
- 若没有足够数量的队伍，则立即结束游戏
- 记录参与游戏玩家的游戏模式，并再次应用[原版规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#原版规则配置)设定的游戏模式
- 使用[原版出生类型](https://github.com/XColorful/BattleRoyale/wiki/Spawn-config#原版出生类型)会立即将所有玩家传送至场地内，如启用地面传送则一定时间内区块未加载/玩家不在游戏维度将把玩家“吊在空中”，直至超过最大时限或者该区块确实没有能着陆的地面/虚空，并且未在时限内传送的玩家（通常为掉线）将不再传送
- 开始游戏后，取消游戏玩家与非游戏玩家互相直接造成的伤害，如在[大逃杀规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#大逃杀规则配置)中启用记录统计数据则开始记录[大逃杀统计数据](https://github.com/XColorful/BattleRoyale/wiki/BattleRoyale-stats)

## 开始游戏后常见问题

### 结束游戏的方式

- 使用指令手动[结束游戏](https://github.com/XColorful/BattleRoyale/wiki/Game-command#结束游戏)
- 当剩余队伍数量满足条件时自动结束游戏
- 当达到[大逃杀规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#大逃杀规则配置)最大游戏时长后自动结束游戏
> [游戏配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#游戏配置)中可设置游戏结束后是否传送胜利玩家回大厅、是否保留队伍分配

### 物资刷新

见[常见物资刷新问题](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/Loot-introduction#常见物资刷新问题)

### 区域

该类别的问题较为复杂，详细见[区域](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/Zone-introduction#常见区域问题)介绍

### 离开游戏

- 当游戏开始后，[离开队伍](https://github.com/XColorful/BattleRoyale/wiki/Team-command#离开队伍)即离开游戏，立即被淘汰但仍然接收队伍信息、需要指令切换[客户端配置](https://github.com/XColorful/BattleRoyale/wiki/Config-command#客户端配置)中的[显示配置](https://github.com/XColorful/BattleRoyale/wiki/Display-config)手动隐藏
- 玩家离开服务器/不在游戏维度超过[游戏配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#游戏配置)最大离线时长后被强制淘汰

### 客户端问题

- 枪械物品显示不正确：见[客户端显示错误](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/GunMod-introduction#客户端显示错误)
- 不显示小地图：见[客户端显示问题](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/MapMod-introduction#客户端显示问题)

# English

> Detailed Command Wiki: [Game Command](https://github.com/XColorful/BattleRoyale/wiki/Game-command#English)

## Common Troubleshooting
Before starting a Battle Royale game, it's essential to understand a few common issues:

- Team size not as expected: [Query selected game config](https://github.com/XColorful/BattleRoyale/wiki/Game-command#Query-selected-game-config) and check [BattleRoyale gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#BattleRoyale-gamerule).
- Lobby location is incorrect: [Query selected game config](https://github.com/XColorful/BattleRoyale/wiki/Game-command#Query-selected-game-config) and check [BattleRoyale gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#BattleRoyale-gamerule).
> If you've modified the configuration, it should be treated as having performed a [Edit CBR configuration](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/Edit-CBR-configuration#English) and requires [Switch configuration](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/Switch-configuration#English)

## General Steps

> Although [Custom BattleRoyale](https://github.com/XColorful/BattleRoyale) offers the possibility of a one-click [Start-game](https://github.com/XColorful/BattleRoyale/wiki/Game-command#Start-game), you should still understand the various stages before starting the game.

### Load Configuration

> Typically, you can just initialize the game. When not automatically executed, it's generally for debugging issues or enabling lobby teleportation.

Execute the [Read Configuration](https://github.com/XColorful/BattleRoyale/wiki/Game-command#Read-Configuration) command:
- A successful load will enable [Teleport to lobby](https://github.com/XColorful/BattleRoyale/wiki/Game-command#Teleport-to-lobby). If the [Game config](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#Game-config) does not have 'keep team assignment' enabled or if the team size in [BattleRoyale gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#BattleRoyale-gamerule) is modified, it will result in team reset.

### Initialize Game

Execute the [Initialize the game](https://github.com/XColorful/BattleRoyale/wiki/Game-command#Initialize-the-game) command:
- If 'auto-join game' is enabled in [BattleRoyale gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#BattleRoyale-gamerule), team assignment will be performed automatically once, and newly joined players will also create new teams or send join requests.
- [Vanilla gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#Vanilla-gamerule) is applied only once at this stage and occurs after automatic team assignment.
- Immediately applies the game mode set in [Vanilla gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#Vanilla-gamerule) to game players and teleports them to the lobby.
- Pre-calculates spawn information (location, random offset, etc.) at this stage; not displayed in logs.
> You can discuss vanilla rules with players at this stage and make temporary modifications without [reload configurations](https://github.com/XColorful/BattleRoyale/wiki/Reload-command#English); it's intentional that the vanilla rules aren't applied when starting the game.

Remind players to use [Team command](https://github.com/XColorful/BattleRoyale/wiki/Team-command#English) commands instead of vanilla team commands.
> [Custom BattleRoyale's](https://github.com/XColorful/BattleRoyale) team management is independent of the vanilla team system.

### Start Game

Execute [Start game](https://github.com/XColorful/BattleRoyale/wiki/Game-command#Start-game):

- If there are not enough teams, the game ends immediately.
- Records the game mode of participating players and re-applies the game mode set in [Vanilla gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#Vanilla-gamerule).
- Using [Vanilla spawn types](https://github.com/XColorful/BattleRoyale/wiki/Spawn-config#Vanilla-spawn-types) will immediately teleport all players into the arena. If ground teleportation is enabled and chunks are not loaded or players are not in the game dimension within a certain time, players will be "suspended in the air" until the maximum time limit is exceeded or there is truly no ground/void to land on in that chunk. Players not teleported within the time limit (usually due to disconnection) will not be teleported again.
- After the game starts, direct damage between game players and non-game players is canceled. If 'record statistics' is enabled in [BattleRoyale gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#BattleRoyale-gamerule), [BattleRoyale stats](https://github.com/XColorful/BattleRoyale/wiki/BattleRoyale-stats#English) will begin to be recorded.

## Common Issues After Starting the Game

### Ways to End the Game

- Manually [End the game](https://github.com/XColorful/BattleRoyale/wiki/Game-command#End-the-game) using a command.
- Game ends automatically when the remaining team count meets the conditions.
- Game ends automatically when the maximum game duration set in [BattleRoyale gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#BattleRoyale-gamerule) is reached.
> In [Game config](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#Game-config), you can set whether to teleport winning players back to the lobby after the game ends and whether to retain team assignments.

### Loot Generation

See [Common loot generation issues](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/Loot-introduction#Common-loot-generation-issues).

### Zones

Issues in this category are more complex; for details, see [Zones](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/Zone-introduction#Common-zone-issue) introduction.

### Leaving the Game

- After the game starts, [Leave the team](https://github.com/XColorful/BattleRoyale/wiki/Team-command#Leave-the-team) means leaving the game; you are immediately eliminated but still receive team information. You need to manually hide it by switching [Display config](https://github.com/XColorful/BattleRoyale/wiki/Display-config#English) in [Client config](https://github.com/XColorful/BattleRoyale/wiki/Config-command#Client-config).
- Players are forcibly eliminated if they leave the server or are not in the game dimension for longer than the maximum offline duration set in [Game config](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#Game-config).

### Client Issues

- Incorrect display of gun items: See [Client display errors](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/GunMod-introduction#Client-display-errors).
- Minimap not displayed: See [Client display issues](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/MapMod-introduction#Client-display-issues).