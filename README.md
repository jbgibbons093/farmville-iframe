# Farmville Portals Controller

Master controller iframe for Farmville game in Portals.

## Usage

This iframe is designed to be embedded in a Portals space. It handles:

- HUD display (gold, level, XP)
- Crop management (24 plots with timers)
- Marketplace (buy/sell)
- Crafting system
- Animal tracking
- Auto-replant functionality

## Portals Integration

In your Portals space, create an iframe task that loads:
```
https://YOUR_USERNAME.github.io/farmville-iframe/
```

## Message Protocol

### From Portals to Iframe:
- `init_[gold]_[level]_[xp]` - Initialize game state
- `harvest_attempt_[plotId]` - Player trying to harvest
- `collect_cow_[id]` - Collect from cow
- `collect_sheep_[id]` - Collect from sheep
- `collect_pig_[id]` - Collect from pig
- `collect_hive_[id]` - Collect honey

### From Iframe to Portals:
- `setvar_[name]_[value]` - Set a variable
- `show_[objectName]` - Show an object
- `hide_[objectName]` - Hide an object
- `sound_[filename]` - Play a sound
- `notify_[message]` - Show notification

## License

MIT
