# Toolchain and Quality Policy

This document defines the minimum supported toolchain, build presets, compiler-warning policy, C/C++ interoperability rules, testing scope, and diagnostic workflow for Lab 00.

The versions listed below are project baselines rather than requirements to always use the latest available release.

## Minimum toolchain

| Tool | Minimum version | Purpose |
| --- | ---: | --- |
| CMake | 3.25 | Configure presets and reproducible native builds |
| GCC | 13 | C17 and C++20 compilation |
| Clang | 18 | C17 and C++20 compilation, sanitizers, and diagnostics |
| Ninja | 1.11 | Fast and consistent local builds |
| clang-tidy | 18 | C and C++ static analysis |
| cppcheck | 2.13 | Complementary static analysis |
| GDB | 13 | Native debugging walkthrough |

Newer compatible versions may be used.

The exact versions used to validate the completed lab must be recorded in the Lab 00 README.

## Verify installed tools

### Linux

```bash
cmake --version
gcc --version
g++ --version
clang --version
clang++ --version
ninja --version
clang-tidy --version
cppcheck --version
gdb --version
```

### Windows PowerShell

```powershell
cmake --version
gcc --version
g++ --version
clang --version
clang++ --version
ninja --version
clang-tidy --version
cppcheck --version
gdb --version
```

The required compiler executables must be available through `PATH`.

## Build presets

The initial project defines the following presets:

| Preset | Compiler | Build type | Diagnostics |
| --- | --- | --- | --- |
| `gcc-debug` | GCC | Debug | Strict warnings |
| `clang-debug` | Clang | Debug | Strict warnings |
| `gcc-release` | GCC | Release | Optimized build |
| `clang-asan` | Clang | Debug | AddressSanitizer and UndefinedBehaviorSanitizer |

## Linux commands

### GCC debug build

```bash
cmake --preset gcc-debug
cmake --build --preset gcc-debug
ctest --preset gcc-debug
```

### Clang debug build

```bash
cmake --preset clang-debug
cmake --build --preset clang-debug
ctest --preset clang-debug
```

### GCC release build

```bash
cmake --preset gcc-release
cmake --build --preset gcc-release
ctest --preset gcc-release
```

### Clang sanitizer build

```bash
cmake --preset clang-asan
cmake --build --preset clang-asan
ctest --preset clang-asan
```

## Windows PowerShell commands

The commands are intentionally equivalent to the Linux workflow.

### GCC debug build

```powershell
cmake --preset gcc-debug
cmake --build --preset gcc-debug
ctest --preset gcc-debug
```

### Clang debug build

```powershell
cmake --preset clang-debug
cmake --build --preset clang-debug
ctest --preset clang-debug
```

### GCC release build

```powershell
cmake --preset gcc-release
cmake --build --preset gcc-release
ctest --preset gcc-release
```

### Clang sanitizer build

```powershell
cmake --preset clang-asan
cmake --build --preset clang-asan
ctest --preset clang-asan
```

Compiler and sanitizer availability can vary according to the Windows toolchain distribution. Any platform-specific limitation must be recorded in the Lab 00 README.

## Warning policy

Project-owned source code must compile without warnings.

Warnings are treated as errors for project targets in Debug and continuous-integration builds.

Third-party dependencies and generated files must not inherit the project warning policy automatically.

### GCC and Clang baseline

The initial warning set is:

```text
-Wall
-Wextra
-Wpedantic
-Wconversion
-Wsign-conversion
-Wshadow
-Wformat=2
-Wundef
-Wnull-dereference
-Wdouble-promotion
-Werror
```

Additional compiler-specific warnings may be enabled when they identify relevant defects without producing unjustified noise.

Warnings must not be disabled globally merely to obtain a successful build. Any suppression must be:

1. narrowly scoped;
2. justified in a source comment or decision record;
3. reviewed for portability consequences.

## C and C++ interoperability

C headers intended for consumption by C++ code must protect declarations with `extern "C"`.

Example:

```c
#ifndef TELEMETRY_FRAME_H
#define TELEMETRY_FRAME_H

#include <stddef.h>
#include <stdint.h>

#ifdef __cplusplus
extern "C" {
#endif

typedef struct telemetry_frame
{
    uint32_t sample_counter;
    int32_t temperature_millicelsius;
    uint16_t relative_humidity_basis_points;
    uint32_t pressure_pascals;
    uint16_t checksum;
} telemetry_frame;

int telemetry_frame_validate(
    const uint8_t* data,
    size_t size,
    telemetry_frame* output);

#ifdef __cplusplus
}
#endif

#endif
```

`extern "C"` controls language linkage. It does not make C and C++ data structures automatically ABI-safe.

The interoperability boundary must therefore use:

- fixed-width integer types;
- explicit buffer sizes;
- plain C-compatible structures;
- documented ownership;
- documented return codes;
- no C++ classes, templates, exceptions, references, or overloaded functions.

At least one automated test must call the C implementation through the public header from C++.

## Required frame tests

The minimal telemetry-frame test suite must cover:

| Test | Expected result |
| --- | --- |
| Valid frame | Accepted and decoded |
| Invalid field or range | Rejected with a deterministic error |
| Truncated frame | Rejected without reading outside the buffer |
| Incorrect checksum | Rejected without modifying valid application state |

Additional boundary tests should cover:

- empty input;
- null output pointer when applicable;
- minimum and maximum supported field values;
- extra trailing bytes;
- unsupported protocol version.

## Sanitizer demonstration

Lab 00 must document one intentionally introduced defect detected by AddressSanitizer or UndefinedBehaviorSanitizer.

Recommended example:

1. introduce an out-of-bounds frame read;
2. build and execute using `clang-asan`;
3. capture the relevant diagnostic;
4. correct the bounds validation;
5. rerun the same test;
6. demonstrate that the sanitizer-enabled test suite passes.

The intentionally defective source must not remain enabled in the final build.

Evidence may be stored in:

```text
docs/sanitizer-demonstration.md
```

The report should contain:

- defect description;
- reproduction command;
- relevant diagnostic excerpt;
- root cause;
- correction;
- verification after correction.

## Static analysis

Run clang-tidy using the compilation database generated by CMake:

```bash
clang-tidy -p build/clang-debug src/*.cpp
```

Run cppcheck against project-owned sources:

```bash
cppcheck \
  --enable=warning,style,performance,portability \
  --error-exitcode=1 \
  --std=c++20 \
  include src tests
```

Windows PowerShell equivalent:

```powershell
cppcheck `
  --enable=warning,style,performance,portability `
  --error-exitcode=1 `
  --std=c++20 `
  include src tests
```

Material findings must be corrected or documented. Findings must not be suppressed without review.

## Continuous integration

The initial CI validates:

- Ubuntu;
- GCC build and tests;
- Clang build and tests;
- strict compiler warnings;
- CTest execution.

This is a small validation workflow, not a production platform matrix.

The workflow must be enabled only after the first compilable Lab 00 implementation is committed.
