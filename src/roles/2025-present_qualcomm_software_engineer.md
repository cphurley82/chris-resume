# Qualcomm – Software Engineer (2025–Present)

## Scope

- SoC virtual platform development and embedded software engineering in a large cross‑functional environment
- Collaboration across firmware, validation, and platform/tooling stakeholders
- Emphasis on high‑quality engineering practices, CI automation, and developer experience

## Responsibilities

- Design, implement, and review production C++/SystemC components for simulation and bring‑up
- Build automated tests and integrate with CI to improve feedback time and reliability
- Partner with adjacent teams (firmware, validation, platform) to clarify interfaces and unblock development
- Drive documentation and process improvements that lower onboarding and maintenance costs

## Achievements

- Brought up a full SoC virtual platform and integrated it into CI with a documented workflow, enabling faster addition of new platforms
- Built a SystemC unit test framework (GoogleTest + CMake + CI) supporting parallel execution and code quality gates
- Standardized code formatting and style checks with automated linting/formatting in CI, reducing review churn and inconsistencies
- Implemented platform‑aware register mapping selection in boot flows to handle generational differences without ad‑hoc patches
- Debugged and resolved early boot hangs by instrumenting the boot path and correcting register sequencing; enabled stable firmware/OS boot in simulation
- Improved CI reproducibility by pinning artifacts and toolchain inputs to specific revisions, reducing flakiness and bisect time
- Designed and validated a dynamic address decoder (tree/router‑based) that scales to large address maps with O(log N) lookup; verified with shared unit tests and synthetic benchmarks
- Contributed upstream to open‑source SystemC libraries to enable modern C++ and better CI integration
- Automated documentation publishing from Markdown to internal wiki via CI to keep platform docs current and discoverable
- Supported onboarding and mentored teammates on workflows, CI, and modeling practices
- Enabled consistent pre‑silicon firmware validation by integrating Trusted Firmware‑A (TF‑A) and UEFI boot flows into the virtual platform for early regression detection
- Updated simulation and build toolchains with C++20 features and formatting rules (clang‑format, clang‑tidy) coordinating updates across CI jobs
- Established artifact provenance and reproducibility using version tags and Git submodule pinning for components
- Refactored AMBA‑PV decode path to use a router abstraction (scc::router + TLM‑2.0 sockets) reducing worst‑case linear scans and improving boot performance on large maps
- Introduced layered test taxonomy (unit / component / integration / boot scenario) with selective CI scheduling to optimize pipeline duration while increasing coverage
- Authored contributor guides and coding standards (SystemC model patterns, socket usage, memory map conventions) lowering onboarding time for new engineers
- Worked with both Arm and RISC‑V processor simulation.
- Implemented CPU ID (e.g., Arm MIDR) based platform feature selection to keep common boot logic portable across SoC generations

## Keywords

C/C++, SystemC, TLM‑2.0, Python, CMake, GoogleTest, CI/CD, virtual platform, Arm, RISC‑V, TF‑A, UEFI, OpenSBI, Linux, address decoding, documentation automation, code review, clang‑format, clang‑tidy, Clang/LLVM 17, C++20
