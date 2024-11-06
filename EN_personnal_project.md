## **C++ Redis Client Prototype**

The C++ Redis Client project is a CLI application designed to interface with a Redis server, developed to enhance skills in network programming, RESP protocol, library building, and CMake setup. The application consists of a C++ API based on hiredis, encapsulated as a library, and a CLI adapted from an earlier C version. This CLI allows Redis commands through a custom command-line parser that utilizes `readline`, `getopt`, and function pointers.

### Key Features:
- **Supported Commands**: Basic Redis commands for key-value storage, lists, and hashes, with utility commands like `PING` and `INFO`, structured in BNF format.
- **Docker-based Environment**: Simplified setup and test execution within a Docker network.
- **Testing**: Uses GoogleTest for unit testing, with test cases targeting a Redis instance at `tcp://myredis:6379`.
- **Installation**: Includes Docker instructions, CMake setup for building the API, and CLI setup for manual testing.

The project requires Docker and includes detailed installation and usage steps.

**Keywords**: Redis client, C++, RESP protocol, network programming, CMake, Docker, hiredis, CLI, GoogleTest, library binding

link: https://github.com/QwasarSV/my_cpp_redis_client_575_belus_l_svg

---

## **FTP Server**

This FTP server project implements a multithreaded server for file transfer over TCP/IP, following the FTP protocol (RFC959). The server supports authentication via an "Anonymous" user and includes active and passive modes for data transfer. Users can browse directories independently and perform actions such as uploading, downloading, and listing files.

### Key Features:
- **Multithreading**: Supports multiple concurrent client connections using a thread pool.
- **Command Support**: Implements core FTP commands (`USER`, `PASS`, `CWD`, `PWD`, `LIST`, `PASV`, `PORT`, `RETR`).
- **Modes**: Supports active mode (server initiates data connection) and passive mode (client initiates).
- **Components**: Includes a lexer/parser, FTP server, and client implementation.
- **Protocol Compliance**: Adheres to FTP standards with command handling and structured replies.

### Installation and Usage:
Compile the server using `make`, then run the server specifying the port and path (e.g., `./my_ftp 8080 .`). The client can connect to the server via the provided commands (e.g., `USER anonymous`, `CWD <dir>`).

**Keywords**: FTP server, TCP/IP, multithreading, client-server, active/passive mode, RFC959, command parsing, C

link: https://github.com/QwasarSV/my_ftp_509_belus_l_cwo

---

## **Custom Memory Allocator**

The Custom Memory Allocator project implements a memory management library in C, providing alternatives for `malloc`, `free`, `calloc`, and `realloc` functions. It optimizes memory allocation by requesting large memory chunks through `mmap` and dividing them, reducing the frequency of system calls.

### Key Features:
- **Efficient Memory Management**: Memory is handled within a structured interval tree that tracks page addresses without storing individual allocations.
- **Allocation Structure**: Uses a bitmap and a linked-list system to manage slots, optimizing memory allocation and deallocation.
- **Pointer Handling**: The allocator efficiently finds and releases memory slots, leveraging bitmaps for minimal overhead.
- **Replacement for Standard Library**: The library can be used as a substitute for the standard `malloc` functions with `LD_PRELOAD`.

### Installation and Usage:
Compile with `make` and use `LD_PRELOAD=./libmymalloc.so <command>` to replace system memory functions temporarily. Memory allocation and deallocation follow standard practices, with the library handling memory blocks efficiently in the background.

**Keywords**: Custom malloc, memory management, dynamic allocation, mmap, interval tree, bitmap, linked list, C, LD_PRELOAD

link: https://github.com/QwasarSV/my_malloc_436_belus_l_m1a

---

## **Custom C Memory Allocator for Rust on Solana**

This project involves creating a custom memory allocator in C, compatible with Rust and designed for deployment as a smart contract on the Solana blockchain. The allocator is eBPF-compliant, meaning it adheres to the constraints of the eBPF virtual machine, such as limiting function arguments and avoiding non-deterministic operations.

### Key Features:
- **eBPF Compliance**: The allocator meets eBPF standards, using assembly for direct system calls to bypass limitations in standard libraries.
- **Memory Management Functions**: Implements essential functions (`malloc`, `calloc`, `realloc`, and `free`) for efficient memory allocation.
- **Cross-Language Binding**: The C allocator is bound to Rust using the `bindgen` crate, facilitating Foreign Function Interface (FFI) interactions.
- **Tagged Unions for Safety**: Provides a Rust-friendly interface with a tagged union structure to manage types safely, minimizing the need for `unsafe` code.
- **Integration with Rust**: The allocator integrates with Rust, allowing direct calls in Rust projects and the possibility of replacing Rust’s global allocator.

### Usage and Implementation:
The project uses `LD_PRELOAD` to substitute the system allocator with the custom one and utilizes Rust’s `#[repr(C)]` attribute for compatibility with C structures. Users can allocate memory through raw pointers or the tagged union for enhanced type safety in Rust.

This allocator is designed to function efficiently in the constrained environment of Solana, balancing performance with strict compliance.

**Keywords**: Custom allocator, Rust FFI, eBPF, Solana blockchain, C, memory management, smart contract, cross-compilation

links :
- https://github.com/Lbelus/sdmm
- https://medium.com/@lorris.belus/how-to-create-a-c-custom-memory-allocator-and-use-it-in-rust-16a3a79d8f82
- https://www.linkedin.com/feed/update/urn:li:activity:7235294229902602240/

---

## **Custom Curl Implementation**

The custom curl projects (`my_curl` and `curl_lib`) replicate the functionality of the Unix `curl` command, enabling data fetching over HTTP with custom features. `my_curl` is a simple command-line tool for displaying HTML content, while `curl_lib` is a more advanced library that includes SSL/TLS support, HTTP/HTTPS protocols, and user-agent customization, among other features.

### Key Features:
- **HTTP Requests**: Uses socket programming to handle HTTP GET and POST requests and display server responses.
- **User Agents**: Allows selection of various user agents, with support for adding custom ones.
- **Cookie Management**: Implements Netscape cookie jar format, parsing domain, path, expiration, and secure flags.
- **API Endpoints**: Provides functions to interact with web APIs, with examples for LinkedIn profile data fetching.
- **Python Integration**: Supports Python extensions with a virtual environment setup, enabling API interactions through Python scripts. /!\ Compilation with python present issue with ssl_read implementation in a custom assembly/c readline. /!\

### Installation and Usage:
Compile `my_curl` with `make` and run it as `./my_curl <URL>`. For `curl_lib`, install via `python3 setup.py build` and use Python functions to interact with web services, demonstrating login and data retrieval.

This project demonstrates a low-level HTTP client, enhancing web data retrieval capabilities and offering API endpoint exploration.

**Keywords**: Custom curl, HTTP requests, SSL/TLS, user agents, cookie management, LinkedIn API, Python integration, C, networking

links:
- https://github.com/Lbelus/curl_lib
- https://github.com/QwasarSV/my_curl_368_belus_l_zr1

---

## **Custom UNIX Shell in C**

This project implements a custom UNIX command interpreter, `my_zsh`, in C. The shell reads, parses, and executes commands entered by the user, mimicking basic shell behavior. It supports command execution via `execve` and built-in commands, including `echo`, `cd`, `setenv`, `unsetenv`, `env`, `exit`, `pwd`, and `which`.

### Key Features:
- **Command Execution**: Parses user input and executes commands using `execve`, supporting environment variables and PATH-based commands.
- **Built-in Commands**: Implements several UNIX built-ins, allowing users to interact with the environment, navigate directories, and manage variables.
- **Customizable Prompt**: Displays a prompt in the format `[what_you_want]>`.
- **Error Handling**: Provides feedback for invalid commands and handles errors gracefully.

### Installation and Usage:
Clone the repository, compile using `make`, and launch the interpreter with `./my_zsh`. The shell displays a prompt where users can enter commands, and it outputs results or error messages as needed. Built-in commands and `/bin` utilities are supported, allowing flexible interaction.

**Keywords**: Custom shell, command interpreter, execve, built-in commands, PATH, environment variables, error handling, C

link:
- https://github.com/QwasarSV/my_zsh_402_belus_l_u1y

---

## **Largest Square Finder (my_bsq)**
This C project locates the largest square within a grid containing obstacles, using dynamic programming to optimize calculations. The algorithm parses the grid into a matrix, applies a dynamic programming approach to identify square sizes, and stores values in a DP matrix for efficiency. The final output highlights the maximum square size and its coordinates.

**Keywords**: Dynamic programming, obstacle grid, largest square, matrix manipulation, C

link: https://github.com/Qwasar

SV/my_bsq_294_belus_l_gtc

---

## **Basic Calculator (my_bc)**
A basic calculator in C, handling integer-only calculations with operations (`+`, `-`, `*`, `/`, `%`) and parentheses. It converts expressions from infix to postfix notation using the Shunting Yard algorithm, then evaluates them in Reverse Polish Notation (RPN). This approach simplifies operator precedence and ensures accuracy in calculations.

**Keywords**: Basic calculator, integer operations, Shunting Yard algorithm, RPN, C

link : https://github.com/QwasarSV/my_bc_296_belus_l_ynf

---

## **Blockchain CLI (my_blockchain)**
This C-based CLI project prototypes a blockchain, simulating nodes and blocks. It supports adding, removing, and listing nodes and blocks, synchronizing chains, and displaying errors for incorrect operations. It includes a consensus algorithm based on the longest valid chain for conflict resolution. The CLI also includes options to save and quit, with visual indicators of synchronization status.

**Keywords**: Blockchain, CLI, node management, consensus algorithm, longest chain, C

link: https://github.com/QwasarSV/my_blockchain_173_belus_l_nmq

---

## **Custom Readline (my_readline)**
The goal of this C project is to implement a custom version of the `readline` function to read files line-by-line, managing a dynamic buffer. After experimentation with circular buffers and buffer resizing, the function now efficiently reads input by refreshing the buffer based on the cursor position. This custom readline handles variable line lengths and ensures compatibility with different file inputs.

**Keywords**: Custom readline, dynamic buffer, line-by-line reading, file handling, C

link: https://github.com/QwasarSV/my_readline_172_belus_l_6f-

---

## **Custom Tar Utility (my_tar)**
This project reproduces basic functionalities of the Unix `tar` command, allowing users to archive, append, update, list, and extract files. Built iteratively, each functionality represents a milestone in the development process. The CLI supports flags (`-cf`, `-rf`, `-uf`, `-tf`, `-xf`) to manage archives in 512-byte blocks. Future updates could include recursive directory handling and optimized file selection.

**Keywords**: Tar utility, archiving, file management, CLI, flags, iterative development, C

link: https://github.com/QwasarSV/my_tar_166_belus_l_egy

---

## **Custom Printf (my_printf)**
This project implements a custom `printf` function in C, handling variable arguments and supporting common format specifiers (`%c`, `%s`, `%d`, `%o`, `%u`, `%x`, `%p`). Using custom functions for character output, string handling, and integer conversion, this `printf` returns the character count and replicates standard `printf` functionality with precise type matching.

**Keywords**: Custom printf, variadic function, format specifiers, character output, integer conversion, C

link : https://github.com/Lbelus/my_qwasar_lib/tree/main/c/my_printf_70028_vfhfqu

---
