# 04 · Commissioning and Measurement

[← Back to README](../README.md) · Log: [data/arrival-log.csv](../data/arrival-log.csv)

## Stages
1. **Shadow mode** (2 weeks): log the predicted start and stop times against what Evohome actually did. Target: predicted heat-up within ±15 min of observed.
2. **Pilot:** one UFH zone and two radiator zones live.
3. **All zones.**

## Tests
| Test | Pass when |
|---|---|
| Temporary setpoint over RAMSES | The zone changes setpoint within 1 min; reverts at expiry |
| Supervisor stopped | Zones follow the Evohome baseline schedule |
| Arrival accuracy | ≥ 80 % of occupied periods start within ±0.5 °C of comfort |
| Optimum stop | The zone stays within tolerance until the end of occupancy |

## Metrics (vs the plant-monitoring baseline)
| Metric | Baseline | With optimum start/stop |
|---|---|---|
| Mean arrival error (°C at occupancy start) | | |
| Heating hours per zone per day | | |
| Gas per heating degree-day | | |
| Boiler cycles per hour | | |
