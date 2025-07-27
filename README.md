Task1.1 - RISC-V Toolchain Setup Tasks & Uniqueness Test

Ubuntu VirtualBox on Windows • Spike • Proxy Kernel • Icarus Verilog

Windows: Ubuntu 22.04 LTS in Oracle VirtualBox (2vCPUs, 4 GB RAM, 80 GB disk).

Task 1 — Install base developer tools
Why: These are common build prerequisites (compilers, linkers, autotools) and libraries
required by the RISC‑V simulator, proxy kernel, and other tooling. GTKWaves is included for
waveform viewing in digital design flows.

>>sudo apt-get install -y git vim autoconf automake autotools-dev curl \

Command explanation: 
1. sudo
Meaning: "SuperUser DO"

Purpose: Runs the following command with administrative (root) privileges. Necessary because installing software modifies system files.

2. apt-get
Meaning: Advanced Package Tool (command-line interface)

Purpose: A package manager used on Debian-based systems (like Ubuntu) to install, update, or remove software packages.

3. install
Meaning: A subcommand of apt-get

Purpose: Tells apt-get to install one or more packages.

4. -y
Meaning: Yes to all prompts

Purpose: Automatically agrees to any confirmation prompts (e.g., "Do you want to continue? [Y/n]"), so the install proceeds without manual input.

5. git
Meaning: A version control system

Purpose: Installs Git, used for tracking changes in source code and collaborating on projects.

6. vim
Meaning: A text editor

Purpose: Installs Vim, a powerful command-line-based text editor.

7. autoconf
Meaning: A tool for generating configuration scripts

Purpose: Installs Autoconf, which helps prepare software source code for compilation on different systems.

8. automake
Meaning: A tool for automatically generating Makefile.in files

Purpose: Installs Automake, part of the GNU build system, used to maintain portable makefiles.

9. autotools-dev
Meaning: Development files for GNU autotools

Purpose: Installs helper scripts and macros used with Autoconf and Automake.

10. curl
Meaning: A command-line tool for transferring data with URLs

Purpose: Installs Curl, used to make network requests (e.g., downloading files, accessing APIs).

11. \ (backslash)
Meaning: Line continuation character

Purpose: Tells the shell to continue the command on the next line, making long commands easier to read.
 libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex \
 texinfo gperf libtool patchutils bc zlib1g-dev libexpat1-dev gtkwave
