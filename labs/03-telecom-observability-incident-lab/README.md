# Lab 03 — Telecom Observability and Incident Lab

## Objective

Operate the Lab 02 monitoring application as an observable service using a small and actionable set of metrics, dashboards, alerts, runbooks, and reproducible incidents.

## Scenario

An operations team must identify a remote-site problem, distinguish the symptom from the cause, and respond using telemetry produced by the C++ service.

## Initial stack

* C++20 monitoring service;
* Prometheus-compatible metrics endpoint;
* Prometheus;
* Grafana;
* Grafana Alerting or Alertmanager;
* structured application logs.

OpenTelemetry and OTLP are controlled extensions after the Prometheus baseline is complete.

The initial lab does not require:

* Kubernetes;
* cloud deployment;
* a complete distributed tracing platform;
* long-term metrics storage.

## Initial metric set

```text
telecom_site_cabinet_temperature_celsius
telecom_site_relative_humidity_percent
telecom_site_supply_voltage_volts
telecom_site_tilt_degrees
telecom_site_telemetry_age_seconds
telecom_site_sensor_errors_total
telecom_site_checksum_errors_total
telecom_site_state_transitions_total
telecom_site_restarts_total
telecom_site_up
```

Metric names and labels must be reviewed for:

* explicit units;
* operational usefulness;
* bounded cardinality;
* missing-data behavior.

Device identifiers must not create unbounded label values.

## Initial dashboard

One dashboard with four sections:

1. Site overview.
2. Environmental conditions.
3. Bench power and physical security.
4. Telemetry and service health.

Every panel must answer an operational question.

Decorative, redundant, or unused panels are excluded.

## Initial alerts

No more than five alerts are required:

* `CabinetTemperatureCritical`;
* `SupplyVoltageLow`;
* `TelemetryMissing`;
* `ExcessiveSensorErrors`;
* `UnexpectedSiteRestart`.

Each alert must define:

* severity;
* threshold;
* persistence duration;
* expected impact;
* diagnostic steps;
* recovery evidence;
* short runbook.

## Required incidents

### Incident 01 — Cooling degradation

A gradual temperature increase follows a failed or degraded fan.

### Incident 02 — Supply instability

Falling supply voltage is followed by one or more device restarts.

### Incident 03 — Frozen sensor

Telemetry continues arriving, but a sensor repeats unchanged values and no longer represents the environment.

Each incident report must contain:

* summary;
* timeline;
* detection signal;
* impact;
* investigation;
* root cause;
* contributing factors;
* correction;
* prevention;
* limitations.

## Acceptance criteria

* [ ] Metrics are exposed by or directly derived from the C++ service.
* [ ] Prometheus collects the documented metrics.
* [ ] The dashboard is provisioned from version-controlled files.
* [ ] No more than five initial alerts are enabled.
* [ ] Every enabled alert has a short runbook.
* [ ] The three required incidents are reproducible.
* [ ] Incident reports distinguish symptom, contributing factor, and root cause.
* [ ] Metric-label cardinality is documented.
* [ ] Missing-data behavior is documented.
* [ ] Observability configuration can be recreated from the repository.

## Optional extension

After completion, instrument the C++ service with OpenTelemetry and export telemetry through OTLP without changing the domain model.

This extension must not delay the Prometheus-based completion gate.

## Out of scope

* Kubernetes;
* production cloud deployment;
* multi-region telemetry;
* long-term metrics storage;
* machine learning;
* predictive maintenance;
* a complete Network Operations Center;
* dozens of dashboards;
* dozens of alerts.

## Completion artifact

A reproducible observability environment with a concise dashboard, actionable alerts, short runbooks, and three evidence-based incident reports.

