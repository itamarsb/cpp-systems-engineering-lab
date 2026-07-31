# cpp-systems-engineering-lab
HHands-on experiments with Modern C++, C interoperability, systems programming, native applications, telemetry, and embedded systems.


This repository documents a progressive collection of hands-on experiments
focused on modern C++, interoperability with C, native software development,
systems programming, telemetry, and embedded systems.

The laboratory is intended as a long-term learning environment rather than a
fixed course. New experiments are added as concepts emerge from open-source
contributions, systems engineering studies, and personal projects.


## Structure

```markdown

cpp-systems-engineering-lab/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── labs/
│   ├── 01-development-environment/
│   ├── 02-first-native-application/
│   ├── 03-cpp-build-process/
│   ├── 04-c-and-cpp-interoperability/
│   └── 05-command-line-arguments/
│
├── examples/
│
├── notes/
│
└── resources/

```

---

## Lab 01 — C++ Development Environment

Environment setup:

- GCC;
- Clang;
- MSVC;
- CMake;
- Ninja;
- VS Code;
- C/C++ extensions;
- compilation on Windows and subsequently on Linux;
- verification of installed versions.

Result:

```c++
#include <iostream>

int main()
{
    std::cout << "C++ Systems Engineering Lab\n";
    return 0;
}
```

The value of this lab will be present in the complete tutorial on the environment, compilation, and execution, and not just in the code.


---


## Lab 02 — From Source Code to Native Binary

Show the entire workflow:

```text
source code
    ↓
preprocessing
    ↓
compilation
    ↓
assembly
    ↓
linking
    ↓
native executable

```

This lab would explain:

- `.cpp` file;
- object file;
- linker;
- static and dynamic libraries;
- symbols;
- native executable;
- the difference between compilation and interpretation.


---

