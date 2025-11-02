# 👻 Ghost in opcode

This repository contains the Proof-of-Concept and research for a 25-year-old architectural blind spot affecting modern reverse engineering tools.

[![SAMPLE X86](https://raw.githubusercontent.com/sapdragon/hint-break/refs/heads/main/images/sample.png)](https://raw.githubusercontent.com/sapdragon/hint-break/refs/heads/main/images/sample.png)

## The Blind Spot

In 1997, Intel patented (US5,701,442) a series of "Hintable NOPs". While most of these have been assigned functions or are correctly parsed, two opcodes — **`0F 1A`** and **`0F 1B`** — remain ghosts in the machine.

CPUs execute these instructions as valid, multi-byte NOPs. However, leading disassemblers like **IDA Pro, x64dbg, and Binary Ninja** fail to recognize them. They interpret valid, executable code as unknown data, breaking static analysis and creating a simple but highly effective method for anti-disassembly.

This fundamental issue has remained largely unnoticed for decades.

## How to Test

You can see the blind spot in action yourself in under a minute.

1.  Grab the pre-compiled binary: `/samples/patched.exe`.
2.  Open it in your favorite disassembler (IDA, Ghidra, etc.).
3.  Navigate to the function.
4.  Observe how the tool fails on the `0F 1A` and `0F 1B` opcodes, showing them as `db 0Fh, 1Ah...`, `undefined`, or `???`, effectively halting the analysis of the function.
5.  Run `patched.exe`. It will execute flawlessly and print a success message, proving the instructions are valid.

## Repository Structure

-   `/src/`: The C++ source code used to generate the test binary.
-   `/samples/`
    -   `patched.exe`: The pre-compiled 64-bit PoC binary.
-   `/papers/`:
    -   `ru.pdf`: The full research paper (Russian).
    -   `en.pdf`: The full research paper (English).

## LICENSE
MIT
