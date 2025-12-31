# general-makefile
General purpose linux C makefile for easy project management.

---

## Important

This makefile has only been tested on linux and probably won't work on other OS.

---

## Features

- Convenient project initialization with `init`.
- Automatic detection of source (`.c`) files in `src/` directory and subdirectories.
- Automatic include path detection for all subdirectories in `include/`.
- Support for static libraries (`.a`) in `lib/` and external libraries specified in `EXT_LIBS`.
- Compilation of source files ordered by modification date.
- Dependency tracking with `-MMD -MP`.
- Safe cleaning of object files, executables, and project directories.
- Easy to run the application with or without arguments.
- Built-in `help` target to list available Makefile commands.

---

## Directory Structure
```
.
├── include/ # Header files
├── src/ # Source files
├── obj/ # Object files (auto-generated)
├── lib/ # Libraries (.a) to link
├── build/ # Executable output
├── docs/ # Documentation
└── Makefile # This Makefile
```
All directories are automatically created by the `init` target.

---

## Makefile Variables

- `COMPILER` – Compiler to use (default: `gcc`)
- `CFLAGS` – Compiler flags (default: `-Wall`)

- `EXE_NAME` – Name of the output executable (default: `app_name`)

- `SRC_EXTENSION` - Extension of the source files (default :`.c`)
- `SRC_DIR` – Source directory (only **one allowed**)
- `OBJ_DIR` – Object files directory (only **one allowed**)
- `INCLUDE_DIR` – Include directory (all subdirectories are automatically added)

- `LIB_DIR` – Directory for static libraries
- `EXT_LIBS` – List of external libraries to link (without `lib` prefix)

- `BUILD_DIR` – Output directory for the executable
- `RUN_ARGS` – Optional arguments to pass when running the program

- `INSTALL_DIR_PREFIX` - Directory of the installation
- `INSTALL_BIN_DIR` - Subdirectory of the prefix where the binary will be located

---

## Usage

### Initialize project

```bash
make init
```
Creates the project folder structure and adds a main.c to the src directory.

### Compilation

```bash
make build
```
Compiles the project. Recompile only if modification date is newer.

```bash
make build_clean
```
Clean compilation of the project. Deletes all object files and the excutable, then it compiles.


### Runing the program

```bash
make run
```
Runs the program without any arguments.

```bash
make run_args
```
Runs the program with the arguments stored in the `RUN_ARGS` variable.

Can also be called in the following way:
```bash
make run_args RUN_ARGS="arg1 arg2"
```

### Deleting files

```bash
make clean
```
Deletes all object and dependency files.

```bash
make clean_exe
```
Deletes executable file.

```bash
make clean
```
Deletes all object and dependency files and the executable file.

```bash
make delete_all
```
Deletes **ALL** the project.
This includes every single file and folder included in the original directories created when initializing project.

### Installation

```bash
make install
```
Installs app to the specified path in variables `INSTALL_DIR_PREFIX` and `INSTALL_BIN_DIR`.

```bash
make install_path
```
Adds installation path to ~/.bashrc if it does not exist

```bash
make uninstall
```
Removes app from the specified path in variables `INSTALL_DIR_PREFIX` and `INSTALL_BIN_DIR`.

### Help

```bash
make help
```
Prints some info related to each target of the makefile.

---

## Planned features
- More testing
- Support for tests
- Build modes (example: debug)
- Versioning

---

## Notes
In Windows WSL there might be some problems with time like the following:
```bash
make: Warning: File `main.c` has modification time 381 s in the future
make: warning:  Clock skew detected.  Your build may be incomplete.
```
This is not related to the makefile itself and its a known WSL issue.
Check this [issue](https://github.com/microsoft/WSL/issues/4677) for more information.

This makefile has been tested in Linux based systems only (more precisely Ubuntu and Arch linux).
The compiler used for testing is gcc, other compilers haven't been tested.