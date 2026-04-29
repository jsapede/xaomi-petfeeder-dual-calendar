# Changelog - Pet Feeder ESPHome

> Final file: `pet-feeder-esphome.yaml`
> Last update: 2026-04-28

---

## v14.3 - Stable Release (Current)
**Date**: 2026-04-28
**File**: `pet-feeder-esphome.yaml`

### Bug Fixes
- **Feed persistence** (v14.1-14.3): `mcu_done_feeds_bits` (uint16_t) flash-stored
  - Bitmask 0-9 for each feed slot
  - Override status in MCU feedplan parser (force status=0 if bit=1)
  - Day tracking (`last_reset_day`) for midnight reset
- **Single source** (published ONCE): `last_feed_source_str` set conditionally
  - ESP mode → "ESP Schedule X"
  - MCU mode → "MCU Schedule X" (read from `last_feed_source_raw` MIoT SIID 4 PIID 5)
  - Manual → "Manual Feed"
  - Published at end of success event (L811)
- **Anti-double distribution** (v11): `activate_mcu_schedule_delayed` (2-min delay)
  - Checks `last_esp_feed_success_minute` at boot and on ESP→MCU switch
- **Time tolerance** (v14.2): ±1 minute for ESP schedule trigger
- **Status 254 skipped** in `check_scheduled_feeds` (prevents re-trigger)
- **Midnight wrap-around** (v14.1): +1440 min if feed time already passed
- **`feedstart_event`**: No longer changes source (log only)
- **Reset daily total**: input_number + button

### New Features
- `mcu_done_feeds_bits` (uint16_t) - persisted to flash
- `last_esp_feed_success_minute` (int) - persisted to flash
- `last_reset_day` (string) - persisted to flash
- `last_feed_source_raw` (MIoT SIID 4, PIID 5) - raw source from MCU

---

## v13 - ESP Feeds Persisted
- ESP feeds survive MCU plan refreshes
- `mcu_done_feeds` list

---

## v12 - Faster Refresh + MCU Status
- Reduced refresh delays
- Status "in progress" (254) for MCU

---

## v11 - Anti-Double Distribution
- 2-minute delay on ESP→MCU switch
- Prevents duplicate distributions

---

## v10 - MCU/ESP Full Coexistence
- Dynamic source per mode
- Adaptive remaining time
- Status override

---

## v9 - Immediate Sensor Updates
- Sensors update immediately after any action

---

## v8 - Core Stability & Spec Compliance
- Timezone corrected
- Invalid commands removed
- Universal counter (all sources)

---

## v7 - ESP/MCU Select + Dual Mode
- Select "Schedule Engine" (ESP/MCU)
- Switch "Feeding Distribution" (ON/OFF)
- Remaining time calculated based on active mode
- `set_properties 5 9` for status update (decommissioned)
- `raw_feed_plan.update()` immediate

---

## v6 - Basic Dual Mode
- 3 sources: ESP Schedule, MCU Schedule, Manual Feed
- Feed Success binary sensor
- Switch `esp_distribution`
- `feed_status_string` for correct display in ESP mode

---

## v5 - Timezone Fix
- Initial offset set to 2 (instead of 0)
- `check_scheduled_feeds` script
- DST timezone sync

---

## v4 - Base Fixes
- Timezone bug
- `remaining_time` sensor

---

## v3 and earlier
- Initial versions, not preserved
