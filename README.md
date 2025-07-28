
# 🛠️ Task 1.1 – RISC-V Toolchain Setup & Uniqueness Test

## 🧰 Environment Overview

* **Host OS:** Windows
* **VM:** Ubuntu 22.04 LTS on Oracle VirtualBox
* **Resources:** 2 vCPUs, 4 GB RAM, 80 GB Disk
* **Tools Covered:** Spike, Proxy Kernel, Icarus Verilog

---

## 🎯🎯🎯🎯 Task 1 — Install Base Developer Tools

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


## 🎯🎯🎯🎯 Task 2 — Create a clean workspace and capture your home path

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
## 🧾 Command Breakdown
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

## 🎯🎯🎯🎯 Task 3 — Get a prebuilt RISC‑V GCC toolchain

**Why?**
Provides riscv64-unknown-elf-gcc (newlib) to compile bare‑metal/user‑space RISC‑V
programs. Using a prebuilt toolchain avoids a long source build.

### 📦 Req Commands

```bash
wget "https://static.dev.sifive.com/dev-tools/riscv64-unknown-elf-gcc8.3.0-2019.08.0-x86_64-linux-ubuntu14.tar.gz"
tar -xvzf riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linuxubuntu14.tar.gz
```
## 🧾 Command Breakdown
| Command                                                                 | Meaning                         | Purpose                                                                                          |
|-------------------------------------------------------------------------|----------------------------------|--------------------------------------------------------------------------------------------------|
| `wget "https://...tar.gz"`                                              | Web Get                          | Downloads the RISC-V GCC toolchain archive from the specified URL.                              |
| `tar -xvzf riscv64-unknown-elf-gcc8.3.0-2019.08.0-x86_64-linux-ubuntu14.tar.gz` | Extract Compressed Archive       | Unpacks the `.tar.gz` file into the current directory so you can use the toolchain.             |


# 🟥 PERFORMING TASK 3:

## ✅ Goal

Get a prebuilt RISC‑V GCC toolchain.

---

## Executing the Commands:

```bash
wget "https://static.dev.sifive.com/dev-tools/riscv64-unknown-elf-gcc8.3.0-2019.08.0-x86_64-linux-ubuntu14.tar.gz"
tar -xvzf riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linuxubuntu14.tar.gz
```
---
# 🔴 OUTPUT:

<img width="573" height="118" alt="image" src="https://github.com/user-attachments/assets/7b5053db-4bc1-41b6-a7ff-6632d052a72e" />

---

## 🎯🎯🎯🎯 Task 4 — Add toolchain to your PATH (current shell + persistent)

**Why?**
Allows riscv64-unknown-elf-gcc and related binaries to be available without typing
full paths, both now and after you reopen the terminal.

### 📦 Command (current shell):

```bash
export PATH=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-
2019.08.0-x86_64-linux-ubuntu14/bin:$PATH
```

### 📦 Command (persistent for new terminals):

```bash
echo 'export PATH=$HOME/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-
2019.08.0-x86_64-linux-ubuntu14/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

## 🧾 Command Breakdown

| Step | Command                                                                                                                                              | Purpose / Explanation                                                                                                                                              |
|------|------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1    | `export PATH=$(pwd)/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH`                                         | Temporarily adds the RISC-V toolchain's `bin` directory to the `PATH`. Effective only for the current shell session. Use `$(pwd)` for current directory.          |
| 2    | `echo 'export PATH=$HOME/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH' >> ~/.bashrc`                      | Appends the path to `.bashrc` so it's set automatically in all future terminal sessions. `$HOME` points to the user’s home directory.                              |
| 3    | `source ~/.bashrc`                                                                                                                                   | Reloads `.bashrc` in the current shell so changes take effect immediately without restarting the terminal.                                                         |


# 🟥 PERFORMING TASK 4:

# 🔴 OUTPUT AFTER EXECUTING THE COMMANDS:

<img width="1197" height="97" alt="image" src="https://github.com/user-attachments/assets/f19500e9-efdf-4fb2-b5ce-a49228121067" />

<img width="1204" height="706" alt="image" src="https://github.com/user-attachments/assets/0ccf47cf-369f-4e1f-a944-4aae4d8df167" />

---

## 🎯🎯🎯🎯 Task 5 — Install Device Tree Compiler (DTC)

**Why?**
Some RISC‑V components expect DTC to be present; it’s a common dependency in
SoC/simulator flows.

### 📦 Command:

```
sudo apt-get install -y device-tree-compiler
```

## 🧾 Command Breakdown


| Component                  | Meaning / Function                                                                 |
|----------------------------|-------------------------------------------------------------------------------------|
| `sudo`                     | Executes the command with superuser (admin) privileges.                            |
| `apt-get`                  | Debian/Ubuntu package management tool for installing, updating, and removing packages. |
| `install`                  | Specifies that a package should be installed.                                      |
| `-y`                       | Automatically confirms the installation prompts (non-interactive).                |
| `device-tree-compiler`     | The name of the package to install; provides the `dtc` tool.                      |

---                                                      |


# 🟥 PERFORMING TASK 5:

# 🔴 OUTPUT AFTER EXECUTING THE COMMAND:

<img width="1185" height="471" alt="image" src="https://github.com/user-attachments/assets/6333c695-af01-47fc-9024-5dabc5d2bd09" />

---

## 🎯🎯🎯🎯 Task 6 — Build and install Spike (RISC‑V ISA simulator)

**Why?**
Spike is the reference ISA simulator. You’ll run your compiled RISC‑V ELF on Spike to
validate correctness. Installing into the same prefix keeps everything together.

### 📦 Command:

```
cd $pwd/riscv_toolchain
git clone https://github.com/riscv/riscv-isa-sim.git
cd riscv-isa-sim
mkdir -p build && cd build
../configure --prefix=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc8.3.0-2019.08.0-x86_64-linux-ubuntu14
make -j$(nproc)
sudo make install
```

## 🧾 Command Breakdown

+---------------------------------------------------------+---------------------------------------------------------------+
| Command                                                 | Explanation                                                   |
+---------------------------------------------------------+---------------------------------------------------------------+
| cd $pwd/riscv_toolchain                                 | Change to the working directory where toolchain is located.   |
|                                                         | `$pwd` holds the base directory path.                         |
+---------------------------------------------------------+---------------------------------------------------------------+
| git clone https://github.com/riscv/riscv-isa-sim.git    | Clone the official Spike (riscv-isa-sim) GitHub repository.   |
|                                                         | This brings the source code to your local machine.            |
+---------------------------------------------------------+---------------------------------------------------------------+
| cd riscv-isa-sim                                        | Move into the cloned Spike source code directory.             |
+---------------------------------------------------------+---------------------------------------------------------------+
| mkdir -p build && cd build                              | Create a separate build directory and move into it.           |
|                                                         | Keeps build files separate from source code (clean structure).|
+---------------------------------------------------------+---------------------------------------------------------------+
| ../configure --prefix=$pwd/riscv_toolchain/             | Configure the build system and set installation path.         |
| riscv64-unknown-elf-gcc8.3.0-2019.08.0...               | This prefix tells it where to install compiled binaries.      |
+---------------------------------------------------------+---------------------------------------------------------------+
| make -j$(nproc)                                         | Compile the code using all available CPU cores.               |
|                                                         | `$(nproc)` gets the number of CPU threads for faster build.   |
+---------------------------------------------------------+---------------------------------------------------------------+
| sudo make install                                       | Install the compiled Spike binaries to the configured path.   |
|                                                         | `sudo` is needed if installation path needs admin access.     |
+---------------------------------------------------------+---------------------------------------------------------------+

---                                                      |

# 🟥 PERFORMING TASK 5:

# 🔴 OUTPUT AFTER EXECUTING THE COMMANDS:

<img width="1185" height="471" alt="image" src="https://github.com/user-attachments/assets/6333c695-af01-47fc-9024-5dabc5d2bd09" />

---

