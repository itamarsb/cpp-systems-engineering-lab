# Lab 00 — Modern C/C++ Engineering Baseline

## Objective

Establish a reproducible development, build, test, and diagnostic workflow for the remaining labs.

## Scenario

A native systems project must build consistently with more than one compiler, expose defects early, and provide repeatable commands for developers and continuous integration.

## Required scope

* GCC and Clang on the selected host environment;
* C17 and C++20 compilation;
* CMake with out-of-source builds;
* Ninja as the preferred local generator;
* `Debug` and `Release` configurations;
* strict compiler warnings;
* CTest integration;
* a small C library called from C++;
* AddressSanitizer and UndefinedBehaviorSanitizer;
* `clang-tidy`;
* `cppcheck`;
* GDB debugging walkthrough;
* documented build, test, analysis, and cleanup commands.

## Minimal implementation

The sample program should validate a small telemetry frame or measurement rather than only print `Hello, World!`.

Its purpose is to exercise the engineering toolchain. It should not become a large application.

## Planned structure

```text
00-modern-c-cpp-engineering-baseline/
├── README.md
├── CMakeLists.txt
├── CMakePresets.json
├── include/
├── src/
└── tests/
```

The additional directories will be created when implementation begins.

## Required verification

* build with GCC;
* build with Clang;
* run all tests through CTest;
* demonstrate one sanitizer-detected defect and its correction;
* demonstrate one debugger inspection;
* run static analysis and document material findings.

## Toolchain and quality policy

Minimum tool versions, Linux and Windows commands, build presets, warning rules, C/C++ interoperability requirements, test cases, sanitizer evidence, and the initial CI scope are documented in:

- [Toolchain and Quality Policy](docs/toolchain-and-quality.md)

The CI workflow and executable build presets will be enabled together with the first compilable implementation.

## Acceptance criteria

* [ ] A clean checkout builds using documented commands.
* [ ] C and C++ targets use the intended standards.
* [ ] Warnings are treated as errors for project code.
* [ ] GCC and Clang builds pass.
* [ ] CTest reports all required tests passing.
* [ ] Sanitizer-enabled host tests pass.
* [ ] Static-analysis commands are documented.
* [ ] The C/C++ interoperability boundary is covered by a test.
* [ ] No generated build artifacts are committed.

## Out of scope

* package managers;
* GUI applications;
* networking;
* microcontroller toolchains;
* production CI matrices;
* advanced template metaprogramming.

## Completion artifact

A small but complete native project that becomes the build-quality reference for Labs 01–03.

