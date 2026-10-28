# 01 · Scope and Design

[← Back to README](../README.md)

## Functions
| Function | What it does |
|---|---|
| **Optimum start** | Before each occupied period, starts the zone at the latest time that still reaches the occupied setpoint on time |
| **Optimum stop** | Before each unoccupied period, sets the zone back at the earliest time that keeps it within tolerance until the period ends |
| **Learning** | Updates each zone's heat-up and cool-down rates from real data |
| **Shadow mode** | Predicts and logs, without acting, for validation |

## Inputs and outputs
| Signal | Source |
|---|---|
| Zone temperature and setpoint | RAMSES-II (ramses_cc) |
| Zone heat demand % | RAMSES-II |
| Outdoor temperature | Weather integration / outdoor sensor |
| Occupancy schedule (the **source of truth**) | HA schedule helpers per zone |
| Optional live occupancy | BLE presence (Bermuda): skip preheat for rooms not in use |
| **Output:** temporary zone setpoint | RAMSES-II command to the owning Evohome controller |

## Evohome settings
| Setting | Change | Why |
|---|---|---|
| Built-in optimisation (optimum start/stop) | **Off** ⟨verify where it's set on each controller⟩ | Two optimisers would fight |
| Zone schedules | Set to a **setback baseline** (e.g. economy all day) ⟨decide⟩ | The supervisor raises zones to comfort via temporary setpoints; if the supervisor fails, the house stays at a safe setback |
| Room control, HR92s, UFH | Unchanged | Evohome remains the zone controller |

## Command path and safety
- Commands go over **RAMSES-II** through the gateway, whose transmit side has already been audited (only reads and temporary setpoints are sent).
- **Temporary** setpoints only, with an expiry, so a stuck supervisor can't leave a zone at comfort indefinitely.
- **Fail-safe:** supervisor down means Evohome runs its baseline schedule.
- Sits in the **"plant"** write-access tier of the [security baseline](https://github.com/the-control-cabinet/smart-home-security-baseline).
