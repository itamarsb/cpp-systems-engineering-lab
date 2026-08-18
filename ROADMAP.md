# Roadmap

This roadmap keeps the initial learning path small, sequential, and completion-oriented.

The durations are planning ranges, not deadlines.

## Working rules

1. Keep only one active lab at a time.
2. Complete the required acceptance criteria before starting the next lab.
3. Treat optional extensions as backlog items, not hidden requirements.
4. Reuse stable protocols and components instead of rewriting them without a clear reason.
5. Apply the dual review defined in `docs/engineering-standards.md` before material scope or technology changes.
6. Record decisions, limitations, and unsupported use cases honestly.
7. Do not claim production readiness or safety certification.

## Phase 0 — Engineering foundation

### Lab 00 — Modern C/C++ Engineering Baseline

**Goal:** establish a reproducible native development, build, test, and diagnostic workflow shared by the remaining labs.

**Target duration:** 1–2 weeks.

**Completion gate:**

* GCC and Clang builds;
* automated tests;
* strict compiler diagnostics;
* sanitizers;
* static analysis;
* documented build and test commands.

## Phase 1 — Sensor-to-host telemetry

### Lab 01 — Compact Environmental Telemetry Station

**Goal:** collect validated environmental data on a bench microcontroller and consume it in a C++ host application.

**Target duration:** 3–5 weeks after hardware selection.

**Completion gate:**

* selected hardware documented;
* firmware collects and validates environmental measurements;
* node emits bounded and versioned telemetry;
* host application validates and stores the data;
* valid and malformed sessions can be replayed;
* automated host tests pass.

## Phase 2 — Telecommunications infrastructure scenario

### Lab 02 — Telecom Site Infrastructure Monitor

**Goal:** model the operational state of a remote telecommunications site using real or replayed telemetry.

**Target duration:** 3–5 weeks.

**Completion gate:**

* normal operation is reproducible;
* at least five fault scenarios are reproducible;
* operational state transitions are deterministic;
* hysteresis and timeouts are tested;
* malformed telemetry does not corrupt application state;
* session reports are generated.

## Phase 3 — Observability and incident response

### Lab 03 — Telecom Observability and Incident Lab

**Goal:** operate the C++ monitor as an observable service with actionable dashboards, alerts, and incident investigations.

**Target duration:** 3–4 weeks.

**Completion gate:**

* metrics are exposed by the C++ service;
* Prometheus collects the required metrics;
* one concise Grafana dashboard is provisioned;
* no more than five initial alerts are enabled;
* each alert has a short runbook;
* three incidents are reproducible and documented.

## Deferred backlog

The following items do not block the initial roadmap:

* additional meteorological sensors;
* rain gauge;
* anemometer and wind direction;
* LoRa, Wi-Fi, GPS, or cloud connectivity;
* binary telemetry protocol;
* OpenTelemetry Collector and OTLP;
* multi-site monitoring;
* modem or SNMP integration;
* predictive maintenance;
* ARM and STM32;
* RTOS and Zephyr;
* aviation and aerospace specialization;
* marine specialization.

## Review checkpoints

| Checkpoint                   | Review question                                                                          |
| ---------------------------- | ---------------------------------------------------------------------------------------- |
| Before Lab 01 implementation | Which PIC, programmer, board, and sensors have current tool support?                     |
| Before protocol freeze       | Is the protocol bounded, versioned, testable, and hardware-independent?                  |
| Before Lab 02 implementation | Are the site variables realistic without implying access to a carrier network?           |
| Before Lab 03 implementation | Which minimum metrics and alerts support the defined incidents?                          |
| After Lab 03                 | Which specialization offers the best value: ARM, telecom expansion, aviation, or marine? |

## Definition of initial-path completion

The initial path is complete when:

* all four lab READMEs reflect implemented behavior;
* build and test commands are reproducible;
* the hardware inventory and selected target are documented;
* the telemetry protocol has valid and malformed fixtures;
* tests cover normal, boundary, timeout, and failure cases;
* dashboards and alerts are provisioned from versioned files;
* three incidents can be reproduced and explained;
* limitations and future work are recorded.

