# Victron-ESPHome

ESPHome component to monitor a Victron device via VE.Direct / UART TTL

## Supported devices

All Victron devices providing a VE.Direct port.

## Requirements

* [ESPHome 2021.10 or higher](https://github.com/esphome/esphome/releases).
* Generic ESP32 or ESP8266 board

## Schematics

Attention: The TX voltage of the VE.Direct interface depends on the product. Some are 5V, others 3.3V!
https://www.victronenergy.com/live/vedirect_protocol:faq#q4is_the_vedirect_interface_33_or_5v


```
                UART-TTL
┌────────────────┐                ┌──────────────────┐
│           GND 1│<-------------->│1 GND             │
│ Victron    TX 3│--------------->│3 D8   ESP32/     │
│ Charger    RX 2│                │       ESP8266    │
│            5V 4│                │                  │
└────────────────┘                └──────────────────┘

# UART-TTL jack (JST-PH 2.0mm pinch)
┌─── ─────── ────┐
│                │
│ 1    2   3  4  │
│GND  RX  TX VCC │
└────────────────┘
```

If you are unsure about to pin order please measure the voltage between GND and VCC (5V). If you measure a positive voltage you know the position of VCC and GND!

### JST-PH 2.0 jack

|   Pin   |    Purpose   |  ESP/Consumer  |
| :-----: | :----------- | :------------- |
|  **1**  |   **GND**    |       GND      |
|    2    |      RX      | Not Connected  |
|  **3**  |    **TX**    |     D8 (RX)    |
|    4    |      5V      |                |

<a href="images/VE pinout.jpg" target="_blank">
<img src="images/VE pinout.jpg" width="50%">
</a>

The `uart_id` and `victron_id` is optional if you use a single UART / victron device. All sensors are optional.

The victron device pushs one status message per second.

The available numeric sensors are:
- `max_power_yesterday`
- `max_power_today`
- `yield_total`
- `yield_yesterday`
- `yield_today`
- `panel_voltage`
- `panel_power`
- `battery_voltage`
- `battery_voltage_2`
- `battery_voltage_3`
- `battery_current`
- `battery_current_2`
- `battery_current_3`
- `day_number`
- `charging_mode_id`
- `error_code`
- `tracking_mode_id`
- `load_current`
- `ac_out_voltage`
- `ac_out_current`
- `ac_out_apparent_power`
- `device_mode_id`
- `warning_code`
- `battery_temperature`
- `instantaneous_power`
- `consumed_amp_hours`
- `state_of_charge`
- `time_to_go`
- `depth_of_the_deepest_discharge`
- `depth_of_the_last_discharge`
- `depth_of_the_average_discharge`
- `number_of_charge_cycles`
- `number_of_full_discharges`
- `cumulative_amp_hours_drawn`
- `min_battery_voltage`
- `max_battery_voltage`
- `last_full_charge`
- `number_of_automatic_synchronizations`
- `number_of_low_main_voltage_alarms`
- `number_of_high_main_voltage_alarms`
- `number_of_low_auxiliary_voltage_alarms`
- `number_of_high_auxiliary_voltage_alarms`
- `min_auxiliary_battery_voltage`
- `max_auxiliary_battery_voltage`
- `amount_of_discharged_energy`
- `amount_of_charged_energy`

The available text sensors are:
- `charging_mode`
- `error`
- `tracking_mode`
- `firmware_version`
- `device_type`
- `device_mode`
- `warning`
- `alarm_condition_active`
- `alarm_reason`
- `model_description`

Binary sensors:

- `load_state`
- `relay_state`
