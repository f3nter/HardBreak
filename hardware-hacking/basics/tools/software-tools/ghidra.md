# Ghidra

## Theory

Ghidra is a powerful, open-source software reverse engineering (SRE) framework developed by the National Security Agency (NSA). It is designed to analyze and decompile executable files, making it an invaluable tool for pentesters, malware analysts, and security researchers.

#### Key Features

* Multi-Platform Support
  * Ghidra runs on various operating systems, including Windows, macOS, and Linux, providing versatility for different environments.
* Decompiler
  * Converts binary code into a more readable high-level representation, facilitating analysis.
* User-Friendly Interface
  * Offers a modern graphical user interface (GUI) for intuitive navigation and interaction with code.
* Scripting Support
  * Allows users to automate tasks and customize the analysis process using Python or Java.
* Extensive Language Support
  * Supports a wide range of architectures and binary formats, including x86, ARM, MIPS, and more.
* Collaboration Features
  * Supports team environments, allowing multiple users to work on the same project simultaneously.

## Installation

To install Ghidra, follow these steps:

1. Download the latest release from the [Ghidra GitHub repository](https://github.com/NationalSecurityAgency/ghidra/releases).
2. Extract the downloaded archive to your desired location.
3. Ensure you have Java Development Kit (JDK) version 11 or later installed.
4.  Navigate to the Ghidra directory and run the `ghidraRun` script:

    ```bash
    ./ghidraRun
    ```

## Usage

1. Creating a New Project
   1. Launch Ghidra and create a new project to start analyzing binaries.
2. Importing a Binary
   1. Drag and drop or use the file menu to import the binary you wish to analyze.
3. Code Analysis
   1. Once imported, Ghidra will prompt to analyze the binary. Accept the defaults or customize the analysis options.
4. Exploring the Disassembly
   1. Use the Code Browser to navigate through the disassembled code, viewing functions, variables, and control flow.
5. Decompiling
   1. Select a function and use the decompiler view to see a high-level representation of the code, which is easier to understand.

## Resources

*[Ghidra Website](https://ghidra-sre.org/)
*[Ghidra Git repository](https://github.com/NationalSecurityAgency/ghidra/releases)
