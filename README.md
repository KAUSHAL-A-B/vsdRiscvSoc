
# 🛠️ Task 1 – RISC-V Toolchain Setup & Uniqueness Test

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
<img width="1118" height="333" alt="image" src="https://github.com/user-attachments/assets/37af2f69-b150-44e8-a652-5f11ad8b59ef" />
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

| Command                                                                 | Explanation                                                                                          |
|-------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| `cd $pwd/riscv_toolchain`                                              | Navigate to your working directory where the RISC-V toolchain is being set up.                      |
| `git clone https://github.com/riscv/riscv-isa-sim.git`                 | Clone the Spike (RISC-V ISA simulator) source code from the official GitHub repository.             |
| `cd riscv-isa-sim`                                                     | Enter the cloned `riscv-isa-sim` directory.                                                          |
| `mkdir -p build && cd build`                                          | Create a `build` directory (if it doesn't exist) and move into it. Keeps build files separate.      |
| `../configure --prefix=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc8.3.0-2019.08.0-x86_64-linux-ubuntu14` | Configure the build system. `--prefix` tells where to install Spike binaries.                       |
| `make -j$(nproc)`                                                      | Compile the code using all available CPU cores for faster build. `$(nproc)` auto-detects CPU count. |
| `sudo make install`                                                    | Install Spike binaries to the given `--prefix` directory. `sudo` is required for system-wide access.|
                                                       |


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

| Command                                                                 | Explanation                                                                                          |
|-------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| cd $pwd/riscv_toolchain                                                 | Navigate to the RISC-V toolchain workspace directory.                                                |
| git clone https://github.com/riscv/riscv-isa-sim.git                    | Clone the Spike ISA simulator repository from GitHub.                                                |
| cd riscv-isa-sim                                                        | Enter the cloned directory for Spike.                                                                |
| mkdir -p build && cd build                                              | Create and enter a `build` directory to keep build files isolated.                                   |
| ../configure --prefix=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc...  | Configure the build with installation path set to your toolchain directory.                         |
| make -j$(nproc)                                                         | Compile using all CPU cores (faster build). `$(nproc)` detects number of processors.                |
| sudo make install                                                       | Install the built binaries into the specified directory (requires sudo for access).                 |
                                                   |

# 🟥 PERFORMING TASK 6:

# 🔴 OUTPUT AFTER EXECUTING THE COMMANDS:

<img width="1194" height="723" alt="image" src="https://github.com/user-attachments/assets/891ce3f7-e342-4ece-9096-8eebdce1b7b0" />
....
<img width="1190" height="712" alt="image" src="https://github.com/user-attachments/assets/3c1d48aa-e70d-47bf-a64f-aff0ce52554a" />
<img width="1190" height="712" alt="image" src="https://github.com/user-attachments/assets/56ac31da-e830-437d-8760-c334d3b47be8" />
<img width="1154" height="236" alt="image" src="https://github.com/user-attachments/assets/3a7daca9-1741-42ea-bb56-ced2a3baaafb" />
<img width="1113" height="179" alt="image" src="https://github.com/user-attachments/assets/fcdccaf7-5df5-4468-87af-7e10ee1e08c9" />
<img width="1019" height="360" alt="image" src="https://github.com/user-attachments/assets/44612749-24cf-4feb-89d4-efb0e1437561" />
---

## 🎯🎯🎯🎯 Task 7 — Build and install the RISC‑V Proxy Kernel (riscv-pk)

**Why?**
pk provides a minimal runtime so you can run newlib ELF binaries under Spike with
'spike pk ./your_prog'. It bridges your compiled program to the simulator

### 📦 Commands:

```
cd $pwd/riscv_toolchain
git clone https://github.com/riscv/riscv-pk.git
cd riscv-pk
mkdir -p build && cd build
../configure --prefix=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc8.3.0-2019.08.0-x86_64-linux-ubuntu14 --host=riscv64-unknown-elf
make -j$(nproc)
sudo make install

```

## 🧾 Command Breakdown

| Command                                                                                                                | Explanation                                                                                                                   |
|------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| cd $pwd/riscv_toolchain                                                                                                | Move to your RISC-V toolchain workspace directory.                                                                            |
| git clone https://github.com/riscv/riscv-pk.git                                                                        | Clone the RISC-V Proxy Kernel (PK) source code from GitHub.                                                                  |
| cd riscv-pk                                                                                                            | Enter the `riscv-pk` directory that was just cloned.                                                                          |
| mkdir -p build && cd build                                                                                            | Create a `build` directory (to keep build files separate from source) and move into it.                                      |
| ../configure --prefix=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc8.3.0-2019.08.0-x86_64-linux-ubuntu14 --host=riscv64-unknown-elf | Configure the build system with the install location and specify the target architecture (`riscv64-unknown-elf`).            |
| make -j$(nproc)                                                                                                        | Compile the Proxy Kernel using all available CPU cores (parallel build).                                                     |
| sudo make install                                                                                                      | Install the compiled binaries to the specified location (requires superuser privileges).                                     |


# 🟥 PERFORMING TASK 7:
 
# 🔴 OUTPUT AFTER EXECUTING THE COMMANDS:

<img width="1214" height="727" alt="image" src="https://github.com/user-attachments/assets/c79cd085-25ec-41bd-b732-f4a215e207eb" />
<img width="1214" height="727" alt="image" src="https://github.com/user-attachments/assets/d39bf6ab-8c4d-4c9a-bf17-fc3f667e7b9d" />
...................................................................................................................................
<img width="1214" height="727" alt="image" src="https://github.com/user-attachments/assets/a29bd9a1-41f3-464e-beb8-3247af600682" />
<img width="1214" height="727" alt="image" src="https://github.com/user-attachments/assets/9afb692d-b380-4e8d-9f83-90b9fc89939e" />


## 🎯🎯🎯🎯 Task 8 — Ensure the cross bin directory is in PATH

**Why?**
Some installs place pk and related utilities into a nested riscv64-unknown-elf/bin.
Adding this ensures pk is found by 'which pk'.

### 📦 Command (current shell):

```
export PATH=$PWD/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-
2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf/bin:$PATH

```
### 📦 Command (persistent):

```
echo 'export PATH=$HOME/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-
2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf/bin:$PATH' >>
~/.bashrc
source ~/.bashrc
```

## 🧾 Command Breakdown

| Command                                                                                                                     | Purpose                                                                                          | Notes                                                                                         |
|-----------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| `export PATH=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf/bin:$PATH` | Temporarily adds the RISC-V toolchain to the current shell's `PATH`.                            | ❌ Incorrect usage — `$pwd` is invalid. Use `$PWD` instead.                                   |
| `export PATH=$PWD/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf/bin:$PATH` | ✅ Correct version — temporarily sets toolchain path for **current session only**.              | Useful for quick testing or one-time builds.                                                  |
| `echo 'export PATH=$HOME/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf/bin:$PATH' >> ~/.bashrc` | Appends the export command to `.bashrc` for permanent availability in future sessions.          | Make sure the path is correct and accessible via `$HOME`.                                     |
| `source ~/.bashrc`                                                                                                          | Reloads `.bashrc` to apply changes without restarting the terminal.                             | Required after modifying `.bashrc`.                                                           |
                                    |


# 🟥 PERFORMING TASK 8:
 
# 🔴 OUTPUT AFTER EXECUTING THE COMMANDS:

<img width="956" height="47" alt="image" src="https://github.com/user-attachments/assets/ac20e8fb-642b-491c-b543-f1034ddb211a" />


## 🎯🎯🎯🎯 Task 10 — Quick sanity checks
**Why?**
Why: Confirms the toolchain and simulator are visible and runnable from your shell.

### 📦 Commands

```
which riscv64-unknown-elf-gcc
riscv64-unknown-elf-gcc -v
which spike
spike --version || spike -h
which pk

```

## 🧾 Command Breakdown

| Command                          | Purpose                                                                 | Expected Output / Notes                                                                 |
|----------------------------------|-------------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| `which riscv64-unknown-elf-gcc` | Shows the full path to the RISC-V GCC compiler binary.                  | Verifies if the toolchain is correctly added to `$PATH`.                                |
| `riscv64-unknown-elf-gcc -v`    | Displays version and configuration of the RISC-V GCC.                   | Confirms toolchain installation and compiler build details.                             |
| `which spike`                   | Checks if the `spike` RISC-V simulator is installed and in `$PATH`.     | Returns path like `/usr/local/bin/spike` if properly installed.                         |
| `spike --version` or `spike -h`| Displays version or help menu of `spike`.                               | If not found, it means `spike` is either not installed or not exported in `$PATH`.      |
| `which pk`                      | Locates the `pk` (proxy kernel) binary.                                 | Shows path like `/path/to/riscv-pk/build/pk`.                                           |


# 🟥 PERFORMING TASK 10:
 
# 🔴 OUTPUT AFTER EXECUTING THE COMMANDS:
<img width="1199" height="342" alt="image" src="https://github.com/user-attachments/assets/ca3af004-5c6b-4813-9314-2be1c11e90d0" />
<img width="1195" height="707" alt="image" src="https://github.com/user-attachments/assets/1c3b298b-a855-4c12-9a75-4ff4ef31faa3" />
<img width="1195" height="707" alt="image" src="https://github.com/user-attachments/assets/b3da497d-10c8-42a5-8eee-53fb90f6d705" />



## 🎯🎯🎯🎯 Final Deliverable: A Unique C Test (Username & Machine Dependent)


### 📦 Commands

```
riscv64-unknown-elf-gcc -O2 -Wall -march=rv64imac -mabi=lp64 \
 -DUSERNAME="$(id -un)" -DHOSTNAME="$(hostname -s)" \
 unique_test.c -o unique_test

spike pk ./unique_test
```                                          


# 🟥 PERFORMING TASK 10:
 
# 🔴 OUTPUT AFTER EXECUTING THE COMMANDS:

<img width="1197" height="221" alt="image" src="https://github.com/user-attachments/assets/78b3c744-cca9-4174-9069-7b6d4d348528" />




