# Minecraft Server Configuration Guide

## Overview
This workspace manages a Minecraft 1.21.11 server using Purpur (a high-performance Paper fork), enhanced with custom plugins for gameplay features like advanced enchantments and protocol manipulation.

## Key Components
- **Server Core**: `purpur-1.21.11.jar` with optimized JVM flags in `start.bat`
- **Plugins Directory**: `plugins/` contains jars and configs (e.g., ExcellentEnchants, ProtocolLib)
- **Global Configs**: `server.properties`, `config/paper-global.yml`, `purpur.yml` for server-wide settings

## Enchantment Configuration Pattern
Custom enchantments are defined in individual YAML files under `plugins/ExcellentEnchants/enchants/`.

**Structure Example** (from `double_catch.yml`):
- `Definition`: Metadata like `DisplayName` (MiniMessage formatted), `Description`, `Weight`, `MaxLevel`, `MinCost`/`MaxCost`, `AnvilCost`, `SupportedItems`
- `Distribution`: Flags for `Treasure`, `Tradeable`, `TradeTypes`, `On_Mob_Spawn_Equipment`, etc.
- `Settings`: `Hide_From_List`, `VisualEffects`
- `Probability`: `Trigger_Chance` with `Base`, `Per_Level`, `Capacity`, `Action`

Always use snake_case for enchantment file names (e.g., `double_catch.yml`).

## Server Management Workflows
- **Start Server**: Execute `start.bat` (allocates 8GB RAM with G1GC tuning)
- **Modify Settings**: Edit `server.properties` for core options (e.g., `max-players=15`, `difficulty=hard`)
- **Plugin Configuration**: Update YAML configs in `plugins/*/config.yml` or subdirs
- **Debugging**: Review `logs/latest.log` for errors; restart server after config changes

## Conventions and Patterns
- **Text Formatting**: Use MiniMessage syntax (e.g., `<gray>text</gray>`, `<c:#279CF5>colored</c>`) for display names and descriptions
- **Item Sets**: Reference predefined groups like `fishing_rod`, `sword` in `SupportedItems`/`PrimaryItems`
- **Exclusives**: List incompatible enchantments as `minecraft:vanilla_name` or `excellentenchants:custom_name`
- **Costs**: Follow vanilla enchanting mechanics with `Base` + `Per_Level` multipliers
- **No Builds**: This is a runtime configuration project; changes apply on server restart

## Integration Points
- Plugins communicate via Bukkit/Spigot API; ExcellentEnchants integrates with core enchanting system
- External dependencies managed via plugin jars; update by replacing files and restarting

Reference: [ExcellentEnchants Documentation](https://nightexpressdev.com/excellentenchants/)