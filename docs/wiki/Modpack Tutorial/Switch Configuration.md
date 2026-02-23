# 切换配置

> 详细指令Wiki：[切换配置](https://github.com/XColorful/BattleRoyale/wiki/Config-command)

## 一般步骤

[自定义大逃杀](https://github.com/XColorful/BattleRoyale)的配置文件设计为支持任意数量的预设（见[配置设计](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/Edit-CBR-configuration#配置设计)的说明）、而大多数单个预设文件内可准备多个配置，因此选中**配置文件（预设文件）** 后可能需要再选中特定的配置：
- 先用指令切换**配置文件**
- 再用指令选中文件内的**单个配置**，由于允许名称重复，你需要查看配置的唯一ID（个别配置类型直接以文件为单个配置的则不需要）
- _"default": true_ 仅用于[重载配置](https://github.com/XColorful/BattleRoyale/wiki/Reload-command)时选中并应用配置，手动更换配置文件时无效果
> 如果切换配置失败，可能是修改配置文件后忘记要[重载配置](https://github.com/XColorful/BattleRoyale/wiki/Reload-command)

## 切换大逃杀配置

- 使用指令[大逃杀游戏配置](https://github.com/XColorful/BattleRoyale/wiki/Config-command#大逃杀游戏配置)切换游戏规则、出生、区域**预设文件**
- 切换预设文件后，再使用[切换大逃杀选中配置](https://github.com/XColorful/BattleRoyale/wiki/Config-command#切换大逃杀选中配置)选中文件内配置（如无该配置的指令则属于个别不需要此操作的类型）
- 可以使用指令[查询选定游戏配置](https://github.com/XColorful/BattleRoyale/wiki/Game-command#查询选定游戏配置)
> [切换配置文件](https://github.com/XColorful/BattleRoyale/wiki/Config-command)不会立即[切换大逃杀选中配置](https://github.com/XColorful/BattleRoyale/wiki/Config-command#切换大逃杀选中配置)
- 切换[服务端配置](https://github.com/XColorful/BattleRoyale/wiki/Config-command#服务端配置)后也需要[应用选中的服务端配置](https://github.com/XColorful/BattleRoyale/wiki/Config-command#应用选中的服务端配置)

## 非大逃杀配置

- 使用指令切换[物资刷新配置](https://github.com/XColorful/BattleRoyale/wiki/Config-command#物资刷新配置)，影响地图内箱子等物资刷新
> 使用配置文件内哪个配置取决于箱子/物资刷新器设置的属性，原版箱子默认使用lootId: 0，如无lootId对应的配置则跳过刷新

# English

> Detailed Command Wiki: [Switch Configuration](https://github.com/XColorful/BattleRoyale/wiki/Config-command#English)

## General Steps

The configuration files for [Custom BattleRoyale](https://github.com/XColorful/BattleRoyale) are designed to support an arbitrary number of presets (see explanation in [Configuration Design](https://github.com/XColorful/Custom-BattleRoyale-Complete/wiki/Edit-CBR-configuration#Configuration-design)). Most individual preset files can also contain multiple configurations. Therefore, after selecting a **configuration file (preset file)**, you might need to select a specific configuration within that file:
- First, use a command to switch the **configuration file**.
- Then, use a command to select a **single configuration** within the file. Since names can be duplicated, you need to check the configuration's unique ID (individual configuration types that directly use the file as a single configuration do not require this step).
- _"default": true_ is only used to select and apply the configuration when [reloading configurations](https://github.com/XColorful/BattleRoyale/wiki/Reload-command#English); it has no effect when manually changing configuration files.
> If configuration switching fails, it might be because you forgot to [reload configurations](https://github.com/XColorful/BattleRoyale/wiki/Reload-command#English) after modifying the configuration file.

## Switching BattleRoyale Configurations

- Use the command [BattleRoyale config](https://github.com/XColorful/BattleRoyale/wiki/Config-command#BattleRoyale-config) to switch game rules, spawn, and zone **preset files**.
- After switching the preset file, use [Switch BattleRoyale selected config](https://github.com/XColorful/BattleRoyale/wiki/Config-command#Switch-BattleRoyale-selected-config) to select a configuration within the file (if there's no specific command for that configuration, it belongs to a type that doesn't require this step).
- You can use the command [Query selected game config](https://github.com/XColorful/BattleRoyale/wiki/Game-command#Query-selected-game-config).
> [Switch config file](https://github.com/XColorful/BattleRoyale/wiki/Config-command#Switch-config-file) will not immediately [Switch BattleRoyale selected config](https://github.com/XColorful/BattleRoyale/wiki/Config-command#Switch-BattleRoyale-selected-config)
- After switching [Server Config](https://github.com/XColorful/BattleRoyale/wiki/Config-command#Server-config), you also need to [Apply selected Server config](https://github.com/XColorful/BattleRoyale/wiki/Config-command#Apply-selected-Server-config).
    

## Non-BattleRoyale Configurations

- Use the command to switch [Loot config](https://github.com/XColorful/BattleRoyale/wiki/Config-command#Loot-config), which affects loot generation in chests and other sources within the map.
> Which configuration within the file is used depends on the properties set for the chest/loot spawner. Vanilla chests default to using lootId: 0; if no configuration corresponds to the lootId, generation is skipped.