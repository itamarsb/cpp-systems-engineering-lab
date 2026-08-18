# Lab 02 — Telecom Site Infrastructure Monitor

## Objective

Build a C++20 application that determines the operational state of a remote telecommunications site from live or replayed infrastructure telemetry.

## Scenario

A tower, small-cell cabinet, shelter, or remote telecommunications site needs local monitoring of:

* environmental conditions;
* low-voltage bench power;
* cooling;
* physical condition;
* enclosure access;
* telemetry health;
* device availability.

This lab models site-support infrastructure.

It does not implement or access:

* a 5G Radio Access Network;
* a cellular core;
* licensed RF spectrum;
* carrier-owned equipment;
* subscriber traffic.

## Required input signals

| Area               | Signals                                        |
| ------------------ | ---------------------------------------------- |
| Environment        | Cabinet temperature and humidity               |
| Bench power        | Low-voltage supply and simulated battery state |
| Physical condition | Tilt or vibration                              |
| Access             | Door or enclosure state                        |
| Cooling            | Fan state or simulated tachometer              |
| Telemetry          | Heartbeat, sample age, and checksum errors     |
| Device health      | Uptime and restart count                       |

Inputs may be produced by:

* Lab 01 hardware;
* safe low-voltage bench circuits;
* versioned replay files.

## Operational states

```cpp
enum class SiteState
{
    normal,
    warning,
    critical,
    degraded,
    telemetry_lost,
    maintenance
};
```

State transitions must be deterministic.

Thresholds, hysteresis, timeout behavior, and recovery conditions must be documented and tested.

## Required C++ components

* validated measurement representation;
* site configuration;
* telemetry decoder boundary;
* state-evaluation engine;
* event record;
* clock abstraction for deterministic timeout tests;
* replay source;
* command-line report;
* structured log output.

## Required scenarios

1. Normal site operation.
2. Cabinet overheating after cooling failure.
3. Falling supply voltage followed by device restart.
4. Unexpected door opening.
5. Abnormal tilt or vibration.
6. Frozen sensor values or missing heartbeat.
7. Corrupted or out-of-order telemetry.

Normal operation and at least five failure scenarios are required for completion.

The remaining scenarios may stay as optional extensions.

## Example interface

```bash
telecom-site-monitor replay data/normal-operation.csv
telecom-site-monitor replay data/cabinet-overheating.csv
telecom-site-monitor replay data/power-failure.csv
telecom-site-monitor report --session latest
```

## Acceptance criteria

* [ ] The application builds using the Lab 00 quality baseline.
* [ ] Live or replayed telemetry is accepted through a defined interface.
* [ ] Normal operation is reproducible.
* [ ] At least five failure scenarios are reproducible.
* [ ] State transitions are deterministic.
* [ ] Hysteresis, timeouts, and recovery rules are tested.
* [ ] Sensor faults are distinguished from actual site conditions.
* [ ] Structured events contain timestamp, source, severity, and reason.
* [ ] Malformed or out-of-order data do not crash the application.
* [ ] A session report summarizes states, transitions, and faults.
* [ ] No feature implies access to real carrier systems or licensed RF operation.

## Out of scope

* 5G RAN implementation;
* cellular core implementation;
* RF transmission;
* spectrum analysis;
* real carrier integration;
* high-voltage systems;
* tower battery systems;
* SNMP;
* Modbus;
* CAN;
* cellular modem integration;
* multi-site fleet management;
* predictive maintenance;
* Grafana dashboards;
* alert routing.

## Completion artifact

A deterministic and tested C++ site-monitoring application with replayable operational and failure scenarios.

