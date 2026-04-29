# Pet Feeder ESPHome

ESPHome configuration for the **Xiaomi Smart Pet Food Feeder** (mmgg.feeder.fi1).

Compatible with Home Assistant [dispenser-schedule-card](https://github.com/cristianchelu/dispenser-schedule-card).

## Features

- **Dual Mode**: Selectable ESP or MCU scheduler from HA interface
- **HA Card**: Compatible with dispenser-schedule-card (real-time status)
- **Persistence**: Feed status survives reboots (flash bitmask)
- **Anti-Double**: Protection when switching ESP⇔MCU (2-min delay)
- **Auto Timezone**: DST tracking via Home Assistant
- **Daily Total Reset**: Button + input_number (0-50)
- **3 Sources**: ESP Schedule, MCU Schedule, Manual Feed

## Versions

**Current: v14.3** - Stable release. See [CHANGELOG.md](CHANGELOG.md) for history.

## Installation

```bash
# 1. Copy secrets template
cp secrets.yaml.example secrets.yaml

# 2. Edit with your values
nano secrets.yaml

# 3. Compile
esphome compile pet-feeder-esphome.yaml

# 4. Upload
esphome run pet-feeder-esphome.yaml
```

## HA Configuration

### Selectors
| Entity | Options | Description |
|--------|---------|-------------|
| `select.schedule_engine` | ESP / MCU | Scheduler selection |

### Switches
| Entity | Description |
|--------|-------------|
| `switch.feeding_distribution` | Global distribution ON/OFF |

### Sensors
| Entity | Description |
|--------|-------------|
| `sensor.dispensed_today` | Total portions today |
| `sensor.remaining_time_until_next_feed` | Minutes until next feed |
| `text_sensor.last_feed_source` | Last feed source |
| `text_sensor.raw_feed_plan` | Formatted plan for card |

## Directory Structure

```
pet-feeder-esphome/
├── pet-feeder-esphome.yaml    ← Main configuration
├── secrets.yaml               ← Secrets (gitignored)
├── secrets.yaml.example       ← Secrets template
├── (esphome-miot fetched via external_components at compile time)
├── README.md
├── CHANGELOG.md
├── LICENSE
└── .gitignore
```

## License

MIT
