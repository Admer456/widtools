# WatIsDeze Tools
A [Nail & Crescent](https://github.com/PalmliX/NaC) bsp compiler toolset based on [QBism Q2Tools-220](https://github.com/qbism/q2tools-220) commit: 94056d8

# Enhancements:
- None as of yet.

# Build from source:
Linux-  Makefiles for 32-bit and 64-bit builds of Linux and Windows are included. Assuming a 64-bit build environment, packages lib32z1 and lib32z1-dev are needed to build 32-bit.

Cross-compile- Required packages: mingw-w64, mingw-w64-i686-dev, gcc-multilib.  Pre-compiled Windows dependency libraries are included in /mgw-sdk (borrowed from Q2PRO SDK), or download and build them from scratch.

Windows- Visual Studio sln is included. VS compiler fixes (MaxEd)



