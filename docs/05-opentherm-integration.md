# 05 · Building On It With OpenTherm

[← Back to README](../README.md)

Once the [OpenTherm stage](https://github.com/the-control-cabinet/opentherm-boiler-control-esphome) is live:

| Interaction | Design |
|---|---|
| **Preheat boost** | During an optimum-start preheat, the supervisor asks the OpenTherm node for a higher flow setpoint (e.g. weather compensation +10 °C) to shorten heat-up |
| **Re-learning** | Heat-up rates change with modulating control, so the model resets its weighting and re-learns |
| **Optimum stop and low-flow running** | With modulation, early setback reduces flow temperature smoothly rather than cycling |
| **Shared signals** | Preheat-active flag and target zones are published to HA for the OpenTherm node to consume |
| **Measurement** | The before/after report separates the savings of B (this repo) and D (OpenTherm) |
