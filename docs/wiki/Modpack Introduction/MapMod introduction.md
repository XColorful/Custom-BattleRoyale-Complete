# 小地图

> 小地图模组Wiki：[JourneyMap Documentation](https://teamjm.github.io/journeymap-docs/5.9.x/)

## 常见问题

游玩单人游戏和服务器时保存的目录是不一样的：
- 单人游戏地图文件目录：_./minecraft/journeymap/data/sp/{存档名}_
- 多人游戏地图文件目录：_./minecraft/journeymap/data/mp/{服务器名称}_

对于主世界白天：
- 单人游戏主世界白天：_./minecraft/journeymap/data/sp/{存档名}/overworld/day_
- 多人游戏主世界白天：_./minecraft/journeymap/data/mp/{服务器名称}/overworld/day_
> "overworld"为主世界维度、"day"为白天的地图文件

### 客户端显示问题

#### 同一个服务器，之前的地图没了

如果服务器地图内容没变，可能是服主保留了区块文件但是用了新的存档
- 到多人游戏地图文件目录，通常会有文件夹名称前缀相同的多个文件夹，将旧服务器文件夹内的文件复制到新服务器文件夹中即可

#### 进服务器后大地图是空的

即使服务器和本地的地图相同，游玩服务器时的小地图与本地存档不共享
- 了解本地存档的名称，到单人游戏地图文件目录找名称相同/相似的文件夹，复制文件夹内的文件，在多人游戏地图文件目录里找到名称与服务器名称类似的文件夹，粘贴到该文件夹内

#### 下载好地图，如何显示大地图

- 查找你的按键绑定，打开JourneyMap全屏地图
- 点击下方从右往左第二个按钮（将自动绘制大地图）

# English

> For Map Mod Wiki: [JourneyMap Documentation](https://teamjm.github.io/journeymap-docs/5.9.x/)

## Common Issue

Map data is saved to different directories depending on whether you're playing single-player or on a server:

- Single-player map file directory: _./minecraft/journeymap/data/sp/{save_name}_
- Multiplayer map file directory: _./minecraft/journeymap/data/mp/{server_name}_

For the Overworld during daytime:
- Single-player Overworld daytime: _./minecraft/journeymap/data/sp/{save_name}/overworld/day_
- Multiplayer Overworld daytime: _./minecraft/journeymap/data/mp/{server_name}/overworld/day_
> "overworld" refers to the Overworld dimension, and "day" refers to the daytime map files.

### Client Display Issue

#### My map from a previous session on the same server is gone.

If the server's map content hasn't changed, it's likely the server owner kept the chunk files but started a new save.
- Navigate to your multiplayer map file directory. You'll usually find multiple folders with similar prefixes. Simply copy the files from the old server folder into the new server folder.

#### My full-screen map is empty after joining a server.

Even if the server's map is identical to your local save, the minimap data for server play isn't shared with your single-player saves.
- Identify the name of your local save. Go to the single-player map file directory and find a folder with a similar or identical name. Copy the files from within that folder. Then, in your multiplayer map file directory, find the folder that matches your server's name and paste the copied files into it.

#### How do I display the full-screen map after downloading map data?

- Check your keybindings to open the JourneyMap full-screen map.
- Click the second button from the right at the bottom of the screen (this will automatically draw the large map).