# Binaries

﻿In computing, binaries are files compiled from source code. For example, you run a binary when launching an executable file on your computer. At one point in time, this application would've been programmed in a programming language such as C#. It is then compiled, and the compiler translates the code into machine instructions.

Binaries have a specific structure depending on the operating system they are designed to run. For example, Windows binaries follow the Portable Executable (PE) structure, whereas on Linux, binaries follow the Executable and Linkable Format (ELF). This is why, for example, you cannot run a .exe file on MacOS. With that said, all binaries will contain at least:

 - 1) A code section: This section contains the instructions that the CPU will execute

 - 2) A data section: This section contains information such as variables, resources (images, other data), etc

 - 3) Import/Export tables: These tables reference additional libraries used (imported) or exported by the binary. Binaries often rely on libraries to perform functions. For example, interacting with the Windows API to manipulate files

# Multi-Stage Binaries

Recent trends in cyber security have seen the rise of attackers using what's known as "Multi-stage binaries" in their campaigns - especially malware. These attacks involve using multiple binaries responsible for different actions rather than one performing the entire attack. Usually, an attack involving various binaries will look like the following:

 - Stage 1 - Dropper: This binary is usually a lightweight, basic binary responsible for actions such as enumerating the operating system to see if the payload will work. Once certain conditions are verified, the binary will download the second - much more malicious - binary from the attacker's infrastructure.

 - Stage 2 - Payload: This binary is the "meat and bones" of the attack. For example, in the event of ransomware, this payload will encrypt and exfiltrate the data.

Sophisticated attackers may further split actions of the attack chain (e.g., lateral movement) into additional binaries. Using multiple stages helps evade detection and makes the analysis process more difficult.

For example, a small, more "harmless" initial binary is likelier to evade detection via email filtering than a fully-fledged binary that performs malicious actions such as encryption. Additionally, splitting these functions into multiple stages gives the attacker much more control (i.e. only downloading specific stages once conditions such as time have been met).
