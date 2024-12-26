# Binaries

﻿In computing, binaries are files compiled from source code. For example, you run a binary when launching an executable file on your computer. At one point in time, this application would've been programmed in a programming language such as C#. It is then compiled, and the compiler translates the code into machine instructions.

Binaries have a specific structure depending on the operating system they are designed to run. For example, Windows binaries follow the Portable Executable (PE) structure, whereas on Linux, binaries follow the Executable and Linkable Format (ELF). This is why, for example, you cannot run a .exe file on MacOS. With that said, all binaries will contain at least:

 - 1) A code section: This section contains the instructions that the CPU will execute

 - 2) A data section: This section contains information such as variables, resources (images, other data), etc

 - 3) Import/Export tables: These tables reference additional libraries used (imported) or exported by the binary. Binaries often rely on libraries to perform functions. For example, interacting with the Windows API to manipulate files

