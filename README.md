
## `FerrumOS`

---

### Description

`FerrumOS` is an experimental operating system written in **Rust**. It utilizes the **Limine** bootloader for initial system startup and runs within the **QEMU** emulator for development and testing.

### Features

* **4-Level Paging**: `./kernel/src/memory` - Implements 4-Level paging for virtual memory management.
* **Heap Allocation**: `./kernel/src/allocator` - Contains implementations for various allocation algorithms, including: *Bump*, *Linked List*, and *Fixed Size Blocks*.
* **Interrupts**: `./kernel/src/interrupts` - Uses an external crate to set up an Interrupt Descriptor Table (IDT) and provides handlers for multiple interrupts. It supports both *LAPIC* and *IO-APIC*.
* **Drivers**: `./kernel/src/drivers`
    * **ACPI** and **APIC** parsers for hardware discovery and management.
    * **VGA** and **Linear Framebuffer** for graphics support.
    * **Text Writer** to enable text output on the screen.
        * **PSF Font** parser for custom fonts.
        * **ANSII Parser** that currently supports colored text and cursor manipulation.
    * **ATA** driver for communication with persistent storage devices.
* **Async/Await**: `./kernel/src/task` - Implements a simple executor and a keyboard task to enable **cooperative multitasking**.
* **Timers**: `./kernel/src/timers` - Implements different timers for calibration and general use, supporting **PIT**, **HPET**, and **APIC** timers.
* **File System**: `./kernel/src/fs` - Implements an **ext2fs** file system that supports reading and writing files, creating and removing files and directories, and listing directory contents.
* **Shell**: `./kernel/src/shell` - A minimal shell built for feature testing and basic interaction.

### How to Run

To run `FerrumOS`, you'll need QEMU and the Rust `nightly` toolchain.

#### Prerequisites

* **QEMU**: Ensure you have QEMU installed on your system.
* **Rust Nightly**: Make sure you have the Rust `nightly` toolchain installed. You can install it via `rustup`:
    ```bash
    rustup toolchain install nightly
    rustup default nightly # Or manage with `rustup override set nightly` in the project directory
    ```
    *(Note: Using `rustup override set nightly` in your project directory is often preferred to avoid changing your global default Rust toolchain.)*

#### Building and Running the OS

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/Mufafa98/FerrumOS.git
    cd FerrumOS
    ```
2.  **Build and run the kernel**:
    Use the provided `Makefile` to easily build and run `FerrumOS` in QEMU.

    * To build and run in **release** mode:
        ```bash
        make run
        ```
    * To build and run in **debug** mode:
        ```bash
        make run MODE=d
        ```
---
