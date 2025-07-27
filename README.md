
# 🛠️ Task 1.1 – RISC-V Toolchain Setup & Uniqueness Test

## 🧰 Environment Overview

* **Host OS:** Windows
* **VM:** Ubuntu 22.04 LTS on Oracle VirtualBox
* **Resources:** 2 vCPUs, 4 GB RAM, 80 GB Disk
* **Tools Covered:** Spike, Proxy Kernel, Icarus Verilog

---

## 🎯 Task 1 — Install Base Developer Tools

**Why?**
These are common build prerequisites like compilers, linkers, autotools, and libraries required for building the RISC‑V simulator, proxy kernel, and related tools. `gtkwave` is also included for waveform viewing in digital design flows.

### 📦 Installation Command

```bash
sudo apt-get install -y git vim autoconf automake autotools-dev curl \
libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex \
texinfo gperf libtool patchutils bc zlib1g-dev libexpat1-dev gtkwave
```

---

## 🧾 Command Breakdown

| Part              | Meaning                                 | Purpose                                                       |
| ----------------- | --------------------------------------- | ------------------------------------------------------------- |
| `sudo`            | SuperUser DO                            | Runs the command with root privileges.                        |
| `apt-get`         | Advanced Package Tool                   | A package manager for installing/updating software on Ubuntu. |
| `install`         | Install subcommand                      | Specifies that packages will be installed.                    |
| `-y`              | Yes to all prompts                      | Automatically agrees to confirmation prompts.                 |
| `git`             | Version control system                  | Used for source code management and collaboration.            |
| `vim`             | Text editor                             | Lightweight command-line editor.                              |
| `autoconf`        | Config script generator                 | Prepares software to be compiled on various systems.          |
| `automake`        | Makefile generator                      | Helps generate portable Makefiles.                            |
| `autotools-dev`   | GNU autotools helpers                   | Provides additional macros and scripts for autotools.         |
| `curl`            | Data transfer tool                      | Transfers data via URLs (used in downloads, API calls).       |
| `\` (backslash)   | Line continuation                       | Continues the command to the next line in the terminal.       |
| `libmpc-dev`      | Multi-precision complex library         | Required for mathematical computations in builds.             |
| `libmpfr-dev`     | Multi-precision floating-point library  | Used in compiler toolchains.                                  |
| `libgmp-dev`      | Arbitrary precision arithmetic library  | Required for many cryptographic and numerical tasks.          |
| `gawk`            | GNU version of AWK                      | Used for text processing during builds.                       |
| `build-essential` | Compiler & essential build tools        | Meta-package including `gcc`, `g++`, `make`, etc.             |
| `bison`           | Parser generator                        | Used in compilers and interpreters.                           |
| `flex`            | Lexical analyzer                        | Used to generate scanners (tokenizers).                       |
| `texinfo`         | Documentation system                    | Generates formatted documentation from source.                |
| `gperf`           | Perfect hash function generator         | Often used in compiler and interpreter tools.                 |
| `libtool`         | Library support scripts                 | Helps manage shared libraries.                                |
| `patchutils`      | Patch file utilities                    | Tools to manipulate patch files.                              |
| `bc`              | Arbitrary precision calculator language | Used in scripting and calculations.                           |
| `zlib1g-dev`      | Compression library                     | Required for handling compressed data in tools.               |
| `libexpat1-dev`   | XML parsing library                     | Lightweight XML parser needed for some tools.                 |
| `gtkwave`         | Waveform viewer                         | Used for viewing digital signals in hardware simulations.     |

---


# 🟥 PERFORMING TASK 1:

## ✅ Goal

Install essential RISC-V development tools using `apt-get` on Ubuntu running inside a VirtualBox VM. These tools are system-wide utilities used for compilation, simulation, and debugging.

---

## 🛠️ Executing the Installation Command

Installation command:

```bash
sudo apt-get install -y git vim autoconf automake autotools-dev curl \
libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex \
texinfo gperf libtool patchutils bc zlib1g-dev libexpat1-dev gtkwave
```


---

## 📋 Terminal Output Summary

* ✅ Most tools were **already installed** and up to date (e.g., `git`, `vim`, `autoconf`, `gawk`).
* 📥 The following **new packages** were installed:

  * `gtkwave`: Waveform viewer for simulation.
  * `libjudydebian1`: Dependency library.
  * `libtk8.6`: GUI toolkit needed for GTKWave.
  * `vim-runtime`: Vim's runtime files.
  * `vim`: Full version of the Vim text editor.

> 📦 Total downloaded: **11.9 MB**
> 💾 Disk space used: **44.7 MB**

---
# 🔴 OUTPUT:
<img width="1050" height="722" alt="image" src="https://github.com/user-attachments/assets/fb4ee879-8143-4562-9037-8c5e5d6cfb2b" />
<img width="1050" height="722" alt="image" src="https://github.com/user-attachments/assets/31e73ee3-8873-4170-b05f-e7f4fcc0356f" />


## 🎯 Task 2 — Create a clean workspace and capture your home path

**Why?**
Keeps everything contained in ~/riscv_toolchain, making it easy to remove, update, or
archive. Storing $pwd (your home) ensures consistent paths for later steps.

### 📦 Req Commands

```bash
cd
pwd=$PWD
mkdir -p riscv_toolchain
cd riscv_toolchain
```
| Command               | Meaning                       | Purpose                                                        |
|-----------------------|-------------------------------|----------------------------------------------------------------|
| `cd`                  | Change Directory              | Moves to the home directory (default location when no path is given). |
| `pwd=$PWD`            | Store Present Working Directory | Saves the current directory path in a variable named `pwd`.    |
| `mkdir -p riscv_toolchain` | Make Directory (if not exists) | Creates a folder called `riscv_toolchain` without error if it already exists. |
| `cd riscv_toolchain`  | Enter Directory               | Navigates into the newly created `riscv_toolchain` folder.      |

# 🟥 PERFORMING TASK 2:

## ✅ Goal

Making directory named riscv_toolchain inside home directory.

---

## Executing the Commands:

```bash
cd
pwd=$PWD
mkdir -p riscv_toolchain
cd riscv_toolchain
```
---
# 🔴 OUTPUT:

<img width="494" height="92" alt="image" src="https://github.com/user-attachments/assets/021dda95-c871-4646-8718-f3a0223ba4d5" />

---

