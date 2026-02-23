# 物资刷新

> 控制物资**刷新内容**的配置为[物资刷新配置](https://github.com/XColorful/BattleRoyale/wiki/Configuration-introduction#物资刷新配置)，本页Wiki是介绍**刷新机制**

## 刷新方式

[自定义大逃杀](https://github.com/XColorful/BattleRoyale)以区块为单位处理物资刷新，每次刷新都进行以下事情：
- 物资刷新会先清理物资刷新器/箱子内物品
- 新刷新物品/实体的NBT将包含当前游戏ID
- 基于当前游戏ID清理实体及掉落物，调整[公共设置](https://github.com/XColorful/BattleRoyale/wiki/Performance-config#公共设置)可以不清理不带游戏ID的物品/实体
- 刷新顺序不保证哪个玩家周围的区块先刷新，但保证**距离玩家近**的区块一定优先于其他**距离玩家远**的区块（以玩家中心作为BFS初始队列）
> [自定义大逃杀](https://github.com/XColorful/BattleRoyale)版本≤0.2.4，若物资刷新发生在战利品箱子打开前，则会被相应位置的战利品覆盖（通常不会全部被覆盖）；若物资刷新发生在战利品箱子打开后，则会照常清理掉箱子内物品

### 物资刷新管理器（手动刷新）
用指令[手动刷新](https://github.com/XColorful/BattleRoyale/wiki/Loot-command)：
- 大逃杀游戏开始后会立即终止未完成的手动刷新，且游戏期间无法手动刷新
- 每次刷新都会生成新的游戏ID（用于进行清理）
- 以指令执行时的模拟距离和玩家列表计算待处理的区块并不再补充，处理期间未加载的区块将跳过

### 游戏物资管理器（自动刷新）
游戏进行时自动刷新，期间无法用指令手动刷新：
- 在[游戏刷新设置](https://github.com/XColorful/BattleRoyale/wiki/Performance-config#游戏刷新设置)调整配置
> 管理器会缓存处理过的区块位置、并缓存每次BFS时玩家中心周围一定范围的区块位置，当下一次BFS时玩家处于这些区块，不会触发BFS
- 每次刷新时不更新游戏ID，单个物资刷新器每局只进行一次刷新
> [自定义大逃杀](https://github.com/XColorful/BattleRoyale)版本≤0.2.4，有可能通过调整参数使原版箱子多次刷新（刷新时没有对原版箱子标记）

## 常见物资刷新问题

- 如物资刷新内容与预期不符，可能需要切换[物资刷新配置](https://github.com/XColorful/BattleRoyale/wiki/Config-command#物资刷新配置)，对新执行物资刷新的区块生效
- 如物资刷新过慢/未刷新，检查[性能配置](https://github.com/XColorful/BattleRoyale/wiki/Performance-config)，通常切换模组生成的默认[服务端配置](https://github.com/XColorful/BattleRoyale/wiki/Config-command#服务端配置)即可
- 如果希望清理自然生成的实体，调整[公共设置](https://github.com/XColorful/BattleRoyale/wiki/Performance-config#公共设置)
- 如果旧刷新的实体未被清理，可能是因为刷新速度慢且在远距离处朝玩家（向中心）移动，从而跳过清理
> 如需修改[性能配置](https://github.com/XColorful/BattleRoyale/wiki/Performance-config)则需要再重载[性能配置](https://github.com/XColorful/BattleRoyale/wiki/Reload-command#性能配置)并[应用选中的服务端配置](https://github.com/XColorful/BattleRoyale/wiki/Config-command#应用选中的服务端配置)后生效

# English

> The configuration for controlling **loot content** is found in [Loot](https://github.com/XColorful/BattleRoyale/wiki/Configuration-introduction#Loot). This Wiki page focuses on describing the **loot  mechanisms**.

## Loot Methods

[Custom Battle Royale](https://github.com/XColorful/BattleRoyale) handles loot generation on a per-chunk basis. Each generate cycle involves the following actions:
- Loot generation will first clear items within loot spawners/chests.
- Newly generated items/entities will have the current game ID included in their NBT data.
- Entities and dropped items are cleared based on the current game ID. You can adjust [Common loot settings](https://github.com/XColorful/BattleRoyale/wiki/Performance-config#Common-loot-settings) to prevent the clearing of items/entities that do not carry a game ID.
- The generation order doesn't guarantee which player's surrounding chunks are processed first, but it does ensure that **chunks closer to a player** are always prioritized over **chunks further away from other players** (using player centers as the initial BFS queue).
> For [Custom BattleRoyale](https://github.com/XColorful/BattleRoyale) versions ≤ 0.2.4, if loot generation occurs before a loot chest is opened, its contents might be partially or fully overwritten by the refresh. If loot refresh occurs after a loot chest is opened, its contents will be cleared as usual.

### Loot Generation Manager (Manual)

Use the [loot command](https://github.com/XColorful/BattleRoyale/wiki/Loot-command#English) to manually trigger a generation:
- Once a BattleRoyale game has started, manual generation in progress are immediately terminated, and no new manual generations can be initiated .
- Each generation generates a new game ID (used for clearing purposes).
- The manager calculates the chunks to be processed based on the simulation distance and player list at the time the command is executed. No further chunks are added to this list during processing, and unloaded chunks are skipped.

### Game Loot Manager (Automatic)

Automatically generate loot during active gameplay; manual generations are disabled during this period:
- Detailed generation parameters can be adjusted in [In-game loot Settings](https://github.com/XColorful/BattleRoyale/wiki/Performance-config#In-game-loot-Settings).
> The manager caches processed chunk locations and also caches player center chunk locations from each BFS cycle. This means a new BFS will not be triggered if players are within these cached center chunks during a subsequent BFS.
- The game ID is not updated during each refresh. Individual loot spawner only generate once per game round.
> For [Custom BattleRoyale](https://github.com/XColorful/BattleRoyale) versions ≤ 0.2.4, it might be possible to allow vanilla chests to generate multiple times by adjusting parameters (does not tag vanilla chests during generation).

## Common loot generation issues

- If loot content doesn't match expectations, you might need to switch [Loot](https://github.com/XColorful/BattleRoyale/wiki/Configuration-introduction#Loot). The new configuration will apply to subsequently chunks.
- If loot generation is too slow or not occurring, check your [Performance config](https://github.com/XColorful/BattleRoyale/wiki/Performance-config#English). Usually, switching to the mod's default [Server config](https://github.com/XColorful/BattleRoyale/wiki/Config-command#Server-config) will resolve this.
- If you wish to clear naturally spawned entities, adjust [General Settings](https://github.com/XColorful/BattleRoyale/wiki/Performance-config#General-Settings).
- If previously generated entities are not being cleared, it might be due to slow generation speeds combined with entities moving towards players (inward) from a far distance, causing them to be skipped during clearing.
> If you modify the [Performance config](https://github.com/XColorful/BattleRoyale/wiki/Performance-config#English), you must then reload the [Performance config](https://github.com/XColorful/BattleRoyale/wiki/Reload-command#Performance-config) and [Apply selected Server config](https://github.com/XColorful/BattleRoyale/wiki/Config-command#Apply-selected-Server-config) for changes to take effect.