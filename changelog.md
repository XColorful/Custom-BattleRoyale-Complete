### 0.5.x

#### 0.5.5
- Additonally write/remove gameId to ItemEntity's item
- Add suggests to register command
- Replace lobby teleport sound from dimension to teleport

Fix:
- Fix crash on stopping server if deathmatch config not loaded yet
- Fix missing GamePlayerDeathFinishEvent (Issue #57)
- Send subtitle packet before title packet

Config:
- Add showDeathMessages to gamerule config
- Add new Events to example AllFunction config

1.21.1neoforge:
- Fix ItemEntry not write custom_data

#### 0.5.4

- Auto give wooden sword (for activating CBR addon datapack) when first login
- Reduce zone transparency in zone configs
- Give login item to respawned player
- Give survival lobby item

Optimize:
- Smooth zone rendering (no more jittering)
- Optimize custom event dispatching

Fix:
- Fix PlayerRevive crash issue
- Fix clearInventoryAtStart cannot be disabled

Other:
- Add built-in void dimension (battleroyale:world)
- Restrict lobby protection message to the triggering player

#### 0.5.3

Right-click wooden sword in creative mode to enable modpack's function!

- Add CBR addon, TaCZ Armor Scaling mod
- Disable PlayerRevive sounds
- Disable JourneyMap death point
- Load _CBRC resource pack_ by default

1.21.1neoforge:
- Move JourneyMap minimap to right corner