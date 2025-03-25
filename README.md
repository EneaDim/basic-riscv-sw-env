# RISC-V Project Build System

This README provides an overview of the build system for this RISC-V project, detailing the `config.mk` file and the associated `Makefile`. Together, these files facilitate the cross-compilation of RISC-V applications, managing the toolchain, source files, and build processes.

## Overview

The project is structured to support the development of RISC-V applications using a cross-compilation toolchain. The `config.mk` file contains configuration settings for the toolchain and project structure, while the `Makefile` defines the build targets and rules for compiling, assembling, and generating output files.

## `config.mk`

The `config.mk` file is a configuration file that sets up the environment for cross-compiling RISC-V applications. It includes essential settings for the toolchain, compiler options, source files, and directory structure.

### Key Sections

1. **Toolchain Settings**
  . **CROSS_COMPILE**: Prefix for the RISC-V cross-compiler toolchain (default: `riscv64-unknown-elf`).
  . **Compiler and Tools**: Defines the compiler (`CC`), assembler (`AS`), linker (`LD`), object copy tool (`OBJCOPY`), and disassembler (`DISASSEMBLY`).
2. **Architecture Settings**
  . **ISA**: Instruction Set Architecture (default: `rv64gc`).
  . **ABI**: Application Binary Interface (default: `lp64`).
3. **Compiler Optimizations**
  . **COPT**: Compiler optimization flags (default: `-Os`).
4. **Linker Settings**
  . **LINKER**: Path to the linker script (default: `linker/linker.ld`).
5. **Project Settings**
  . **PROGRAM**: Name of the program to be built (default: `hello_world`).
  . **Directory Structure**: Defines directories for build artifacts (`BUILD_DIR`), common sources (`COMMON_DIR`), and main application sources (`MAIN_DIR`).
6. **Source Files**
  . **COMMON_SRCS**: Common C source files.
  . **MAIN_SRCS**: Main application C source files.
  . **EXTRA_SRCS**: Additional source files that can be specified.
7. **Include Directories**
  . **COMMON_INCS**: Include path for common headers.
  . **MAIN_INCS**: Include path for main application headers.
## `Makefile`

The `Makefile` utilizes the settings defined in `config.mk` to manage the build process. It defines various targets for compiling the application, generating different output formats, and cleaning up build artifacts.

### Key Targets

- **application**: The main target that builds the application, generating ELF, assembly, binary, VMEM, and disassembly files.

- **ELF Target**: 
   **$(PROGRAM).elf**: Compiles the object files into an ELF executable.

- **Assembly Target**: 
   **$(PROGRAM).S**: Compiles the source files into assembly code.

- **Object File Compilation**: 
   **%.o: %.c**: Compiles C source files into object files.
   **%.o: %.S**: Compiles assembly source files into object files.

- **Binary and Disassembly Generation**: 
   **%.bin**: Generates a binary file from the ELF executable.
   **%.dis**: Generates a disassembly from the ELF executable.
   **%.vmem**: Generates a VMEM file from the binary file.

- **Spike ISA Simulator**: 
   **spike**: Runs the compiled ELF file in the Spike ISA simulator and logs the output.

- **File Management**: 
   **reorder_files**: Moves generated object files and assembly files to the build directory.
   **clean**: Cleans up generated files and directories.

## Usage

To use the build system, follow these steps:

1. Ensure that the `config.mk` file is included in your `Makefile`:
2. Setup the config.mk file: Modify the config.mk file to configure the toolchain, program name, and any other settings as needed for your project.

3. Run make application: Execute the command to build the application and generate the necessary output files.
