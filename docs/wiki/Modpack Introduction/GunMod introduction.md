# 枪械

> 枪械模组Wiki：[永恒枪械工坊](https://tacwiki.mcma.club/zh/)

整合包公开时的TaCZ模组使用TaCZ1.1.4的文档

## 常见枪械问题

### 客户端显示错误

TaCZ1.1.4枪械资源文件复制到 _./minecraft/tacz_ 下
> 假如下载枪包压缩包名称为 _pubg_gun_pack.zip_，则最终效果应形如 _./minecraft/tacz/pubg_gun_pack.zip_

当服务端更新/追加了新的枪包，需要客户端也在相同目录下复制同样的文件
- 枪械物品完全为紫黑色则很可能本地没有安装枪包
- 枪械贴图错误很可能是枪包更新，而客户端没有更新枪包文件

### 物资刷新问题

主要参考[物资刷新器](https://github.com/XColorful/BattleRoyale/wiki/Example-command#物资刷新器)额外生成的TaCZ物资刷新配置

#### 枪械物品刷新示例
对于没刷新物品/射击模式异常
- 将你在游戏内看到的 _GunId_ 替换下方"ak47"
- 需要添加 _GunFireMode_，否则开火后会提示异常
```json
{
	"lootType": "item",
	"item": "tacz:modern_kinetic_gun",
	"count": 1,
	"nbt": "{GunId:\"tacz:ak47\",GunFireMode:\"AUTO\"}"
}
```

#### 方便地刷新子弹
- 方案1：用[多个刷新](https://github.com/XColorful/BattleRoyale/wiki/General-loot-config#多个刷新)，对每把枪都复制粘贴，模板：
```json
{
	"lootType": "multi",
	"entries": [
		{
			"lootType": "item",
			"item": "tacz:modern_kinetic_gun",
			"count": 1,
			"nbt": "{GunId:\"tacz:\",GunFireMode:\"AUTO\"}"
		},
		{
			"lootType": "item",
			"item": "tacz:ammo",
			"count": 30,
			"nbt": "{AmmoId:\"tacz:\"}"
		}
	]
}
```
- 方案2：枪械数量众多时按子弹类型分类，外层用[多个刷新](https://github.com/XColorful/BattleRoyale/wiki/General-loot-config#多个刷新)，内部用[加权刷新](https://github.com/XColorful/BattleRoyale/wiki/General-loot-config#加权刷新)，模板：
```json
{
	"lootType": "multi",
	"entries": [
		{
			"lootType": "weight",
			"entries": [
				{
					"weight": 0, // 修改权重
					"entry": {
						// 添加物品
					},
					"weight": 0,
					"entry": {
						// 添加物品
					},
					"weight": 0,
					"entry": {
						// 添加物品
					}
				}
			]
		},
		{
			"lootType": "item",
			"item": "tacz:ammo",
			"count": 30,
			"nbt": "{AmmoId:\"tacz:\"}"
		}
	]
}
```

#### 刷新的大狙是全自动射击模式
- 把 _GunFireMode_ 的"AUTO"修改为"SEMI"或者"BURST"
```json
{
	"lootType": "item",
	"item": "tacz:modern_kinetic_gun",
	"count": 1,
	"nbt": "{GunId:\"tacz:m700\",GunFireMode:\"SEMI\"}"
}
```

# English

> Gun mod Wiki: [Timeless and Classics guns Wiki](https://tacwiki.mcma.club/)

The TaCZ mod used when the modpack was released follows the TaCZ 1.1.4 documentation.

## Common gun issue

### Client display errors

TaCZ 1.1.4 gun resource files should be copied to _./minecraft/tacz/_.
> For example, if the downloaded gun pack compressed file is named _pubg_gun_pack.zip_, the final result should look like _./minecraft/tacz/pubg_gun_pack.zip_.

When the server updates or adds new gun packs, the client also needs to copy the same files to the same directory.
- If gun items are completely purple and black, it's very likely that the gun pack is not installed locally.
- Incorrect gun textures are likely due to a gun pack update, and the client has not updated the gun pack files.

### Loot generation issues

Primarily refer to the additionally generated [Loot Spawner](https://github.com/XColorful/BattleRoyale/wiki/Example-command#Loot-spawner) TaCZ loot configuration.

#### Gun item generation example
For items not generating or abnormal firing modes:
- Replace "ak47" below with the _GunId_ you see in-game.
- You need to add _GunFireMode_, otherwise an error will be prompted after firing.
```json
{
	"lootType": "item",
	"item": "tacz:modern_kinetic_gun",
	"count": 1,
	"nbt": "{GunId:\"tacz:ak47\",GunFireMode:\"AUTO\"}"
}
```

#### Conveniently Generating Ammo

- Method 1: Use [Multiple loot](https://github.com/XColorful/BattleRoyale/wiki/General-loot-config#Multiple-loot), copy-pasting for each gun. Template:
```json
{
	"lootType": "multi",
	"entries": [
		{
			"lootType": "item",
			"item": "tacz:modern_kinetic_gun",
			"count": 1,
			"nbt": "{GunId:\"tacz:\",GunFireMode:\"AUTO\"}"
		},
		{
			"lootType": "item",
			"item": "tacz:ammo",
			"count": 30,
			"nbt": "{AmmoId:\"tacz:\"}"
		}
	]
}
```
- Method 2: When there are many guns, categorize them by ammo type. Use [Multiple loot](https://github.com/XColorful/BattleRoyale/wiki/General-loot-config#Multiple-loot) for the outer layer, and [Weighted loot](https://github.com/XColorful/BattleRoyale/wiki/General-loot-config#Weighted-loot) for the inner part. Template:
```json
{
	"lootType": "multi",
	"entries": [
		{
			"lootType": "weight",
			"entries": [
				{
					"weight": 0, // Change weight
					"entry": {
						// Add item
					},
					"weight": 0,
					"entry": {
						// Add item
					},
					"weight": 0,
					"entry": {
						// Add item
					}
				}
			]
		},
		{
			"lootType": "item",
			"item": "tacz:ammo",
			"count": 30,
			"nbt": "{AmmoId:\"tacz:\"}"
		}
	]
}
```

#### Generated Sniper Rifles have Full-Auto Firing Mode
- Change _GunFireMode_ from "AUTO" to "SEMI" or "BURST".
```json
{
	"lootType": "item",
	"item": "tacz:modern_kinetic_gun",
	"count": 1,
	"nbt": "{GunId:\"tacz:m700\",GunFireMode:\"SEMI\"}"
}
```