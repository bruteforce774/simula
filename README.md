# GNU Cim - Simula Compiler

This is a preserved copy of the GNU Cim compiler (version 3.37), a compiler for the Simula programming language.

## Historical Significance

Simula, developed in the 1960s at the Norwegian Computing Center in Oslo by Kristen Nygaard and Ole-Johan Dahl, is recognized as the first object-oriented programming language. It introduced fundamental concepts such as classes, objects, inheritance, and virtual methods that influenced virtually all modern OOP languages including C++, Java, and Python.

## Authors and Attribution

**Original Authors:**
- Sverre Hvammen Johansen, Department of Informatics, University of Oslo
- Terje Mjoes, Hydro Data, Oslo
- Stein Krogdahl, Department of Informatics, University of Oslo

**Licence:** GNU General Public Licence (see COPYING file)

**Original Sources:**
- University of Oslo Faculty of Mathematics: https://www.mn.uio.no/tjenester/it/hjelp/programvare/simula/implementation/cim/
- GNU Project page: https://www.gnu.org/software/cim/

**Note:** This repository is an unofficial preservation effort. The original code has not been maintained since 2005.

## Compilation Instructions

The original source code uses older C programming conventions (K&R style) that modern GCC compilers treat as errors. To compile successfully on modern systems, you need to use specific compiler flags.

### Prerequisites

- GCC compiler
- Standard build tools (make, autoconf, etc.)
- Linux/Unix system (tested on Fedora)

### Building from Source

1. **Configure the build** with appropriate compiler flags:

   ```bash
   CFLAGS="-O2 -std=gnu89 -Wno-implicit-int -Wno-implicit-function-declaration -Wno-return-mismatch" \
   LDFLAGS=-s \
   ./configure --prefix=/path/to/installation/directory
   ```

   Replace `/path/to/installation/directory` with your desired installation location (e.g., `$HOME/cim-compiler`).

2. **Compile:**

   ```bash
   make
   ```

   Note: You will see warnings during compilation. This is expected for this legacy codebase.

3. **Install:**

   ```bash
   make install
   ```

### Explanation of Compiler Flags

- `-O2`: Optimization level 2
- `-std=gnu89`: Use the C89/C90 standard (compatible with the code's era)
- `-Wno-implicit-int`: Suppress errors about missing return types
- `-Wno-implicit-function-declaration`: Suppress errors about undeclared functions
- `-Wno-return-mismatch`: Suppress errors about return type mismatches

These flags allow the 2005-era code to compile with modern GCC versions that have stricter defaults.

## Setting Up Library Path

After installation, you need to configure the runtime library path so compiled Simula programs can find the CIM runtime library.

### Temporary (current session only):

```bash
export LD_LIBRARY_PATH=/path/to/installation/directory/lib:$LD_LIBRARY_PATH
```

### Permanent (add to ~/.bashrc):

```bash
echo 'export LD_LIBRARY_PATH=/path/to/installation/directory/lib:$LD_LIBRARY_PATH' >> ~/.bashrc
source ~/.bashrc
```

Replace `/path/to/installation/directory` with the actual path you used during configuration.

## Usage Example

### Hello World Program

Create a file `helloworld.sim`:

```simula
BEGIN
   OutText("Hello, World!");
   OutImage;
END
```

### Compile and Run

```bash
# Set library path (if not already in your environment)
export LD_LIBRARY_PATH=/path/to/installation/directory/lib:$LD_LIBRARY_PATH

# Compile
/path/to/installation/directory/bin/cim helloworld.sim

# Run
./helloworld
```

Output:
```
Hello, World!
```

## Verifying Installation

To verify the CIM runtime library is accessible:

```bash
ldd ./helloworld
```

You should see `libcim.so.3` with a path (not "not found"):
```
libcim.so.3 => /path/to/installation/directory/lib/libcim.so.3 (0x...)
```

## Known Issues

- This code has not been maintained since 2005
- Compiler warnings are expected during build (can be ignored)
- Requires specific compiler flags for modern GCC compatibility
- Runtime library path must be configured manually

## Additional Resources

- [Simula on Wikipedia](https://en.wikipedia.org/wiki/Simula)
- [University of Oslo CS Department](https://www.mn.uio.no/ifi/english/)
- Original documentation included in the `doc/` directory

## Contributing

This is a historical preservation project. If you discover issues with compilation on modern systems or have improvements to the build process, please open an issue or pull request.

---

**Preserved by:** [Daniel Andreas Wang/bruteforce774]  
**Date:** December 2025
