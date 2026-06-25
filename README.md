# PassThrough — Fabric 1.21.1 Port

Click through entities to place blocks behind them.

## Features
- Toggle with `/passthrough` command or a configurable keybind (set in Controls)
- Item whitelist: only trigger pass-through when holding certain items
- "Allow Attacking" mode: left-click still hits entities
- Chat notifications when toggling
- Config saved to `config/passthrough.json`

## Config (config/passthrough.json)
```json
{
  "masterEnabled": false,
  "allowAttacking": false,
  "showNotifications": true,
  "firstLaunch": true,
  "whitelist": []
}
```
- `whitelist`: list of item registry names (e.g. `"minecraft:stick"`). Empty = all items.

## Building
1. Requires Java 21+
2. Run `./gradlew build`
3. JAR will be in `build/libs/PassThrough-1.0.0+1.21.11.jar`

## How it works
Mixins into `GameRenderer#updateTargetedEntity` and redirects the
`World#getOtherEntities` call to return an empty list when pass-through
is active, causing the raytrace to hit blocks instead of entities.
