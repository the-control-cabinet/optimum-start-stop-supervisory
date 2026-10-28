# 03 · Algorithms

[← Back to README](../README.md)

## Optimum start
```
needed_rise  = T_comfort − T_room_now
rate         = a + b × (T_room_now − T_out_forecast)
preheat_time = needed_rise / rate × safety_factor (1.1)
start_time   = occupancy_start − clamp(preheat_time, 0, max_preheat)
```
- Recalculated every 10 minutes during the window before occupancy, so the start time tracks the actual weather.
- **Max preheat:** e.g. 2 h radiators, 6 h UFH ⟨tune⟩.
- **Already warm** (needed_rise ≤ 0): no preheat.

## Optimum stop
```
allowed_drop = T_comfort − (T_comfort − tolerance)       e.g. 1.0 °C
coast_time   = −τ × ln(1 − allowed_drop / (T_room − T_out))
stop_time    = occupancy_end − clamp(coast_time, 0, max_early_stop)
```
- **Max early stop:** e.g. 1 h radiators, 3 h UFH ⟨tune⟩.
- Disabled when the outdoor temperature is extreme (frost risk, or a very cold night).

## Fall-backs
| Condition | Behaviour |
|---|---|
| Model has too few samples | Use a fixed default offset per zone type |
| Stale zone temperature | No supervisor action; Evohome baseline applies |
| RAMSES command not acknowledged | Retry, then alert |
| Supervisor offline | Evohome baseline schedule |
