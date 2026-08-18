# Lab 01 — Compact Environmental Telemetry Station

## Objective

Build a compact bench station that acquires validated environmental measurements and sends a documented telemetry stream to a C++ host application.

## Scenario

A remote environmental node must continue operating predictably when a sensor returns invalid data, communication is corrupted, or the device restarts.

## Hardware decision gate

Implementation starts only after documenting:

* available PIC device models;
* development boards or custom boards;
* programmer and debugger models;
* current tool compatibility;
* available BME280 module;
* electrical interface;
* voltage levels;
* bench power arrangement;
* optional MPU6050 and other sensors reserved for later labs.

The selected PIC must be justified through both engineering and industry-relevance reviews.

## Required scope

### Firmware in C

* periodic acquisition from a BME280 or selected equivalent;
* temperature;
* relative humidity;
* atmospheric pressure;
* supply-voltage measurement when safely supported;
* range and plausibility validation;
* explicit sensor-health status;
* monotonic sample counter;
* watchdog when supported;
* restart counter when supported;
* configurable sample interval with safe bounds;
* UART telemetry;
* bounded buffers;
* deterministic formatting.

### Host receiver in C++20

* serial input or file replay;
* frame parsing;
* checksum validation;
* strong measurement types or explicit units;
* dew-point calculation;
* short pressure trend;
* CSV output;
* session summary;
* counts of valid, invalid, missing, and stale samples;
* tests using valid, boundary, truncated, and corrupted fixtures.

## Initial telemetry fields

```text
protocol_version
device_id
sample_counter
temperature_celsius
relative_humidity_percent
pressure_hectopascals
supply_voltage_volts
sensor_status
restart_counter
checksum
```

The exact frame format will be frozen only after the hardware inventory and protocol review.

The protocol must be:

* bounded;
* versioned;
* testable;
* independent from a specific sensor driver.

## Required quality features

* checksum or CRC;
* sensor timeout;
* invalid-reading rejection;
* calibration offsets with documented limits;
* stale-data detection on the host;
* deterministic error codes;
* replayable test fixtures;
* documented behavior for sensor disconnection;
* documented behavior after device restart.

## Required test sessions

1. Normal environmental variation.
2. Sensor unavailable at startup.
3. Sensor stops responding during operation.
4. Truncated or corrupted UART frames.
5. Device restart during a session.

## Acceptance criteria

* [ ] Hardware inventory and target-selection decision are documented.
* [ ] Firmware emits bounded and versioned telemetry.
* [ ] Measurements include explicit units and validity status.
* [ ] The host accepts live input or a recorded equivalent.
* [ ] Valid sessions can be exported to CSV.
* [ ] Malformed frames do not crash or corrupt host state.
* [ ] The five required sessions are reproducible.
* [ ] Protocol parsing has automated host tests.
* [ ] Dew point and pressure trend have automated tests.
* [ ] Firmware and host limitations are documented.

## Out of scope

* rain gauge;
* anemometer;
* wind direction;
* GPS;
* LoRa;
* Wi-Fi;
* cloud services;
* solar charging;
* outdoor enclosure certification;
* weather forecasting;
* machine learning;
* Grafana and Prometheus.

## Completion artifact

A working sensor-to-host telemetry path containing firmware, protocol documentation, host receiver, fixtures, tests, and a concise validation report.

