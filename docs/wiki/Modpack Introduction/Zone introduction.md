# 区域

> 详细的区域Wiki：[区域配置](https://github.com/XColorful/BattleRoyale/wiki/Zone-config)

## 区域机制介绍

> [自定义大逃杀](https://github.com/XColorful/BattleRoyale)的区域机制较[PUBGMC](https://github.com/Toma1O6/PUBGMC)更丰富，并且各个区域间相互独立，因此上手更复杂

[自定义大逃杀](https://github.com/XColorful/BattleRoyale)的单个区域将**功能**和**形状**进行拆分，需要自行排列组合使用[区域功能词条](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#区域功能词条)和[区域形状词条](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#区域形状词条)
- 在[单个配置](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#单个配置)调整区域生成延迟、持续时间、颜色
- [区域功能词条](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#区域功能词条)设定区域功能及tick频率，也影响区域形状处的变化时间
- [区域形状词条](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#区域形状词条)设定一个完整的区域变化过程，也控制区域功能的判定范围
> 如果任一参数的效果与预期不符，请在[大逃杀规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#大逃杀规则配置)中启用记录统计数据并结合[大逃杀统计数据](https://github.com/XColorful/BattleRoyale/wiki/BattleRoyale-stats)排查问题

## 简述区域配置

### 区域颜色
在[单个配置](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#单个配置)中调整，[自定义大逃杀](https://github.com/XColorful/BattleRoyale)通用颜色格式为 _\#RRGGBB_ 或 _\#RRGGBBAA_
- 建议提前跟玩家声明各个颜色/透明度代表的意思（比如用不透明蓝色区域表示边界，用低透明绿色区域表示下一圈的提示）
- 避免用过多的区域组成鲜艳的颜色，玩家可以调整[区域渲染配置](https://github.com/XColorful/BattleRoyale/wiki/Render-config#区域渲染配置)并[应用选中的客户端配置](https://github.com/XColorful/BattleRoyale/wiki/Config-command#应用选中的客户端配置)

### 区域延迟
在[单个配置](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#单个配置)中调整
- 使用叠加延迟可以只计算区域之间的相对延迟
> [自定义大逃杀](https://github.com/XColorful/BattleRoyale)中除非Wiki特别说明，否则时间单位均为tick

### 区域功能
[区域功能词条](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#区域功能词条)设定的功能将在区域存在期间按固定频率生效
- 区域功能触发延迟并不能超过tick频率
- [烟花区](https://github.com/XColorful/BattleRoyale/wiki/Zone-simple-function#烟花区)、[粒子区](https://github.com/XColorful/BattleRoyale/wiki/Zone-simple-function#粒子区)若刻意配置不当将大幅增加**带宽消耗**，还可能造成服务端、客户端卡顿
- [无敌区](https://github.com/XColorful/BattleRoyale/wiki/Zone-simple-function#无敌区)单次提供的无敌时长有特定上限，这是模组作者刻意为之
- 应当提前设计好区域的存在时长，避免不必要的性能浪费

### 区域形状
[区域形状词条](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#区域形状词条)包含一个简单**线性**的运动过程，需要在区域生成时就确定起止点的位置、维度（边长、半径等），否则区域生成失败，并且后续依赖该区域信息的区域生成在绝大多数情况下都会生成失败
- 使用单个向量(x,y,z)表示维度：对于[二维判定形状](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#二维判定形状)，y分量表示从区域底面往上的高度；对于[立体判定形状](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#立体判定形状)，y分量表示从区域中心往上、下的距离（例如[球](https://github.com/XColorful/BattleRoyale/wiki/Zone-3D-shape#球)的半径）
- 如果需要维度为负数或者不符合x、z的特定顺序等，需要使用[坏形状](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#坏形状)，并了解各个形状的反转逻辑（示例配置后会列举关键代码，如[圆形](https://github.com/XColorful/BattleRoyale/wiki/Zone-2D-shape#圆形)需要仅x或z为负数才反转）

### 建议规范
- 将大逃杀游戏过程出现的区域分阶段，若同时需要多个区域则强烈推荐用[多功能区](https://github.com/XColorful/BattleRoyale/wiki/Game-config-add-on#多功能区)的规范
- 推荐仅边界区域使用绝对坐标而后续区域均使用相对坐标，能更好地搭配[区域偏移](https://github.com/XColorful/BattleRoyale/wiki/Game-command#区域偏移)，提升泛用性的同时减少潜在的问题
- 边界区域ID为0且使用不透明颜色，后生成的区域使用更大的区域ID
- 提前计算好区域持续时长（何时可以结束），避免增加不必要的性能开销
- 立体形状如[正方体](https://github.com/XColorful/BattleRoyale/wiki/Zone-3D-shape#正方体)，用相对偏移将区域降低一些以保证覆盖玩家脚底

## 常见区域问题

### 非性能问题

首先按**是否看见了区域**分为两类进行排查：

#### 看见了区域

- 区域位置错误，各个区域相对位置也错误：[区域配置](https://github.com/XColorful/BattleRoyale/wiki/Zone-config)配置错误或者未选中预期的配置
- 区域位置错误，各个区域相对位置正确：很可能是因为使用了错误的[区域偏移](https://github.com/XColorful/BattleRoyale/wiki/Game-command#区域偏移)
- 区域判定范围内外颠倒：使用了[区域配置](https://github.com/XColorful/BattleRoyale/wiki/Zone-config)的[坏形状](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#坏形状)，允许当边长为负数或次序颠倒等情况下更改判定范围，以[二维判定形状](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#二维判定形状)中的属性为例

#### 没看见区域

> 即使与区域之间遮挡很少，各个角度不一定都看得见，且区域被遮挡的情况不一定符合眼前的建筑/地形

##### 一个简单的方式
请确保在[大逃杀规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#大逃杀规则配置)中启用了记录大逃杀游戏统计数据，在你认为应该出现该区域的时候[结束游戏](https://github.com/XColorful/BattleRoyale/wiki/Game-command#结束游戏)/达到[大逃杀规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#大逃杀规则配置)最大游戏时长自动结束游戏，检查[大逃杀统计数据](https://github.com/XColorful/BattleRoyale/wiki/BattleRoyale-stats)：
- 如果没有该区域编号的信息，则还未达到该区域生成时间
- 如果区域生成失败，则会记录其生成的游戏时间，这可以用来排查对于区域生成延迟的计算错误

##### 区域包含随机性/没有启用统计数据/服务器活动结束了
按以下顺序排查：
- 如果在[大逃杀规则配置](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#大逃杀规则配置)中启用了记录大逃杀游戏统计数据，检查[大逃杀统计数据](https://github.com/XColorful/BattleRoyale/wiki/BattleRoyale-stats)，获得区域信息
- 如果服务器还未关闭，执行[查询选定游戏配置](https://github.com/XColorful/BattleRoyale/wiki/Game-command#查询选定游戏配置)得知优先检查哪一个配置文件
- 如果区域生成失败，日志文件里会有警告，通常是因为某个[单个配置](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#单个配置)错误，或者该区域的生成依赖一个先前未生成/生成失败的区域
- 检查[区域配置](https://github.com/XColorful/BattleRoyale/wiki/Zone-config)
> [自定义大逃杀](https://github.com/XColorful/BattleRoyale)的各个区域相互独立，请仔细计算[单个配置](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#单个配置)里区域生成延迟（单位为tick）是否符合预期的出场顺序

### 性能问题

#### 区域生成后卡顿

一般一个区域不足以造成卡顿，如果排查不出其他原因，这里提供一些参考：
- 区域功能对**服务端**性能的影响从高到低：粒子区 ≈ 烟花区 > 安全区/不安全区 > 效果区 > 能量区/无敌区 >> 无功能区
- 区域形状对**服务端**性能的影响影响排序：星形（边界处） > 正多边形（边界处） > 椭球/椭圆 > 正方体/长方体/正方形/长方形 > 球/圆形 ≈ 正多边形/星形（非边界处）
- 区域形状对**客户端**性能的影响影响排序：椭球/椭圆/球/圆形 >> 星形 ≈ 正多边形 ≈ 正方体/长方体 ≈ 正方形/长方形
> 实际可能会对不同类型的区域设置不同的参数，从而导致该排序失效

#### 不知道哪个区域造成卡顿

如果实在需要同时存在非常多的区域，这里提供一点优化方案：
- 精确错开区域tick时间：均摊计算开销
- 减少带宽消耗：降低模拟距离或减少粒子频率/增加粒子冷却
- 对于长时间存在的边界区域（玩家始终在区域内），降低tick频率，增加区域伤害

# English

> For detailed Zone Wiki: [Zone config](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#English)

## Introduction to Zone Mechanics

> [Custom BattleRoyale](https://github.com/XColorful/BattleRoyale#English)'s zone mechanics are richer and more complex than those in [PUBGMC](https://github.com/Toma1O6/PUBGMC), as each zone operates independently. Therefore, it might take more effort to master.

In [Custom BattleRoyale](https://github.com/XColorful/BattleRoyale#English), a single zone's **function** and **shape** are separated. You need to combine them using [Zone function entry](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#Zone-function-entry) and [Zone shape entry](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#Zone-shape-entry).
- Adjust zone generation delay, duration, and color in [Single zone config](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#Single-zone-config).
- [Zone function entry](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#Zone-function-entry) define zone functionalities and their tick frequency, also affect how often changes within the zone's shape are applied.
- [Zone shape entry](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#Zone-shape-entry) define a complete zone transformation process, also control the effective area for zone functionalities.
> If the effect of any parameter doesn't match your expectations, please enable data recording in [BattleRoyale gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#BattleRoyale-gamerule) and use [BattleRoyale stats](https://github.com/XColorful/BattleRoyale/wiki/BattleRoyale-stats#English) to troubleshoot the issue.

## Brief Overview of Zone Configuration

### Zone Color
Adjustable in [Single zone config](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#Single-zone-config). The common color format for [Custom BattleRoyale](https://github.com/XColorful/BattleRoyale#English) is _\#RRGGBB_ or _\#RRGGBBAA_.
- It's recommended to inform players beforehand what each color/opacity represents (e.g., use opaque blue for boundaries, or low-opacity green for the next zone's hint).
- Avoid using too many zones to create overly vibrant colors. Players can adjust [Zone render config](https://github.com/XColorful/BattleRoyale/wiki/Render-config#Zone-render-config) and [Apply selected Client config](https://github.com/XColorful/BattleRoyale/wiki/Config-command#Apply-selected-Client-config).

### Zone Delay
Adjustable in [Single zone config](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#Single-zone-config).
- Using cumulative delays allows for calculating only the relative delay between zones.
> In [Custom BattleRoyale](https://github.com/XColorful/BattleRoyale#English), unless explicitly stated otherwise in the Wiki, all time units are in ticks.

### Zone Function
Functions set by [Zone function entry](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#Zone-function-entry) will take effect at a fixed frequency while the zone exists.
- Zone function trigger delay cannot exceed the tick frequency.
- [Firework zone](https://github.com/XColorful/BattleRoyale/wiki/Zone-simple-function#Firework-zone) and [Particle zone](https://github.com/XColorful/BattleRoyale/wiki/Zone-simple-function#Particle-zone), if improperly configured, can significantly increase **bandwidth consumption** and potentially cause server and client lag.
- [Muteki zone](https://github.com/XColorful/BattleRoyale/wiki/Zone-simple-function#Muteki-zone) provide a specific maximum duration of invincibility per use, which is an intentional design choice by the mod author.
- You should plan the zone's duration in advance to avoid unnecessary performance waste.

### Zone Shape
[Zone shape entry](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#Zone-shape-entry) define a simple **linear** movement process. The start and end points (including dimensions like side length, radius, etc.) must be determined when the zone is generated; otherwise, zone generation will fail, and subsequent zones dependent on this information will also fail to generate in most cases.
- Use a single vector (x,y,z) to represent dimensions: For [2D shape](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#2D-shape), the y-component represents the height from the bottom of the zone upwards; for [3D shape](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#3D-shape), the y-component represents the distance up and down from the center of the zone (e.g., the radius of a [Sphere](https://github.com/XColorful/BattleRoyale/wiki/Zone-3D-shape#Sphere)).
- If negative dimensions or a specific order of x, z is required, you need to use a [Bad Shape](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#Bad-Shape) and understand the inversion logic for each shape (key code examples will be listed after sample configurations; for example, a [Circle](https://github.com/XColorful/BattleRoyale/wiki/Zone-2D-shape#Circle) only inverts if either x or z is negative, not both).

### Recommended Practices
- Categorize zones that appear during a Battle Royale game into phases. If multiple zones are needed simultaneously, it's strongly recommended to follow the [Multifunctional Zone](https://github.com/XColorful/BattleRoyale/wiki/Game-config-add-on#Multifunctional-Zone) standard.
- It's recommended to use absolute coordinates only for boundary zones, and relative coordinates for subsequent zones. This pairs well with [Zone offset](https://github.com/XColorful/BattleRoyale/wiki/Game-command#Zone-offset), enhancing versatility while reducing potential issues.
- The boundary zone ID should be 0 and use an opaque color. Subsequent zones should use larger Zone IDs.
- Calculate the zone's duration (when it should end) in advance to avoid unnecessary performance overhead.
- For 3D shapes like a [Cube](https://github.com/XColorful/BattleRoyale/wiki/Zone-3D-shape#Cube), use relative offsets to lower the zone slightly to ensure it covers players' feet.

## Common zone issue

### Non-Performance Issues

First, troubleshoot by categorizing whether **the zone is visible**:

#### Zone is Visible

- Incorrect zone position, or incorrect relative positions between zones: This indicates an error in the [Zone config](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#English) or that the intended configuration was not selected.
- Incorrect zone position, but correct relative positions between zones: Most likely due to an incorrect [Zone offset](https://github.com/XColorful/BattleRoyale/wiki/Game-command#Zone-offset) being applied.
- Zone judgment inside/outside is inverted: This occurs when using a [Bad Shape](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#Bad-Shape) from the [Zone config](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#English), which allows changing the judgment area when side lengths are negative or order is inverted. Refer to the properties in [2D shape](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#2D-shape) as an example.

#### Zone is Not Visible

> Even with minimal obstruction, zones may not be visible from all angles, and the obstructed view might not align with the surrounding structures/terrain.

##### A Simple Approach
Ensure that recording Battle Royale game statistics is enabled in [BattleRoyale gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#BattleRoyale-gamerule). When you believe the zone should appear, [End the game](https://github.com/XColorful/BattleRoyale/wiki/Game-command#End-the-game) or let the game automatically end at the maximum game duration set in [BattleRoyale gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#BattleRoyale-gamerule). Then, check the [BattleRoyale stats](https://github.com/XColorful/BattleRoyale/wiki/BattleRoyale-stats#English):
- If there is no information about that zone ID, it means the zone generation time has not yet been reached.
- If zone generation failed, it will record the game time of its generation. This can be used to troubleshoot errors in calculating zone generation delays.

##### Zone Contains Randomness/Statistics Not Enabled/Server Activity Ended
Troubleshoot in the following order:
- If recording Battle Royale game statistics is enabled in [BattleRoyale gamerule](https://github.com/XColorful/BattleRoyale/wiki/Gamerule-config#BattleRoyale-gamerule), check [BattleRoyale stats](https://github.com/XColorful/BattleRoyale/wiki/BattleRoyale-stats#English) to obtain zone information.
- If the server has not yet shut down, execute [Query selected game config](https://github.com/XColorful/BattleRoyale/wiki/Game-command#Query-selected-game-config) to determine which configuration file to prioritize checking.
- If zone generation failed, there will be warnings in the log file, usually because an [Single zone config](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#Single-zone-config) is incorrect, or the zone's generation depends on a previously ungenerated or failed zone.
- Check [Zone config](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#English).
> Each zone in [Custom BattleRoyale](https://github.com/XColorful/BattleRoyale#English) is independent. Please carefully calculate the [Single zone config](https://github.com/XColorful/BattleRoyale/wiki/Zone-config#Single-zone-config) zone generation delay (in ticks) to match the expected appearance order.

### Performance Issues

#### Lag after Zone Generation

Typically, a single zone is not enough to cause lag. If you cannot find other causes, here are some references:
- Zone function impact **on server** performance (from high to low): Particle zone ≈ Firework zone > Safe/Unsafe zone > Effect zone > Boost/Muteki zone >> No function zone.
- Zone shape impact **on server** performance (from high to low): Star Shape (at boundary) > Regular Polygon (at boundary) > Ellipsoid/Ellipse > Cube/Cuboid/Square/Rectangle > Sphere/Circle ≈ Regular Polygon/Star Shape (not at boundary).
- Zone shape impact **on client** performance (from high to low): Ellipsoid/Ellipse/Sphere/Circle >> Star Shape ≈ Regular Polygon ≈ Cube/Cuboid ≈ Square/Rectangle.
> Actual settings might vary for different types of zones, which could invalidate this specific order.

#### Unsure Which Zone is Causing Lag

If you truly need many zones to exist simultaneously, here are some optimization strategies:
- Precisely stagger zone tick times: Distribute calculation overhead evenly.
- Reduce bandwidth consumption: Lower the simulation distance or decrease particle frequency/increase particle cooldown.
- For long-lasting boundary zones (where players are always within the zone): Lower the tick frequency and increase zone damage.