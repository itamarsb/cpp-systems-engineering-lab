# Engineering Standards and Dual Review

This document defines the quality gate for roadmap, architecture, language, dependency, and hardware decisions.

## Review A — Modern C/C++ engineering

A proposal passes the engineering review when the applicable questions have satisfactory answers.

### Language and toolchain

* Is the selected language appropriate for the target?
* Does the real compiler support every required language feature?
* Is C17 used where C is the practical firmware target?
* Is C++20 used for host applications?
* Is C++17 compatibility considered when embedded reuse is expected?
* Are vendor-specific extensions isolated and documented?
* Are compiler and toolchain versions recorded?

### Design and resources

* Are ownership and lifetime explicit?
* Does C++ code prefer RAII and value semantics?
* Are buffers bounded?
* Are all external inputs validated?
* Are units and measurement ranges explicit?
* Are timestamp and timeout semantics documented?
* Are invalid, missing, stale, and unavailable data distinguished?
* Is hardware-specific code separated from protocol and domain logic?
* Are dynamic allocation, exceptions, RTTI, and concurrency decisions explicit for constrained targets?

### Verification

* Are normal cases tested?
* Are boundary values tested?
* Are malformed and truncated inputs tested?
* Are timeout and recovery conditions tested?
* Do strict compiler warnings fail the build?
* Are sanitizers used on host-compatible code?
* Are static-analysis findings reviewed instead of blindly suppressed?
* Are acceptance criteria measurable and reproducible?

### Maintainability

* Is the smallest sufficient dependency set used?
* Can another developer build and test the lab from its README?
* Are test data, configuration, dashboards, and alerts versioned?
* Are unsupported use cases and limitations stated honestly?
* Does every optional feature remain outside the completion gate?

## Review B — Industry and domain relevance

A proposal passes the relevance review when it develops transferable skills supported by current evidence.

### Evidence sources

* current employer job descriptions;
* official engineering publications;
* official compiler and hardware documentation;
* official protocol and observability documentation;
* current embedded and infrastructure open-source projects;
* documentation for the exact selected device and programmer.

### Relevance questions

* Does the work strengthen C, C++, embedded Linux, RTOS, drivers, BSPs, telemetry, networking, integration, testing, or verification skills?
* Is the scenario realistic for telecommunications, infrastructure, aerospace, aviation, or marine work?
* Does the implementation demonstrate engineering judgment beyond a generic tutorial?
* Is the technology current enough to justify learning?
* If the target is older, does it still teach a durable and transferable concept?
* Can the result be explained to both software and hardware engineers?
* Does the project avoid unsupported claims about certification, carrier access, production readiness, or safety?

## Decision record

Material decisions should be summarized in the lab README or in a short Architecture Decision Record.

Use the following structure:

```text
Decision:

Context:

Alternatives considered:

Engineering review:

Industry relevance review:

Consequences:

Revisit trigger:
```

## Current language policy

| Target                       | Default            | Rationale                                                       |
| ---------------------------- | ------------------ | --------------------------------------------------------------- |
| Host application             | C++20              | Modern standard library, native tooling, and application design |
| Portable host library        | C++17 or C++20     | Selected according to embedded reuse requirements               |
| PIC 8-bit or 16-bit firmware | C17 when supported | Practical compiler and resource constraints                     |
| PIC32 or ARM firmware        | C17 and/or C++17   | Determined by compiler, device, and lab requirements            |
| Experimental features        | C++23 or later     | Allowed only after both reviews                                 |

The project does not equate modern C++ with maximum feature usage.

Clarity, predictable behavior, strong types, safe ownership, controlled resources, and testability take priority.

