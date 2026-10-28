# 02 · Learning Model

[← Back to README](../README.md) · Data: [data/zone-parameters.csv](../data/zone-parameters.csv)

## Heat-up rate
For each zone, from periods where the zone is calling continuously:

```
rate_up (°C/h) = a + b × (T_room − T_out)      fitted by least squares
```
- Fit per zone, updated weekly with an **exponentially weighted** average so the model adapts to season and furniture changes.
- **Data quality filters:** exclude periods with a window open (step drop), DHW priority (boiler diverted), solar gain (rapid rise with no demand), and setpoint changes mid-heat.

## Cool-down rate
From periods with no demand: an exponential decay towards outdoor temperature.
```
T(t) = T_out + (T0 − T_out) × e^(−t/τ)          fit τ per zone
```

## Zone types differ
| Type | Typical behaviour | Consequence |
|---|---|---|
| Radiators (HR92) | Fast: tens of minutes | Short preheat; useful optimum stop |
| Underfloor (screed) | Slow: hours | Long preheat; optimum stop very effective (big thermal mass) |

## Parameters per zone (logged)
`zone, type, a, b, tau_h, samples, last_update, max_preheat_h, comfort_tolerance_c`
