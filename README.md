# CMPE230: Environment Setup

Welcome to **CMPE230 Systems Programming**!

Throughout the semester, we will do hands-on exercises involving:

- Unix commands and shell usage
- C/C++ programming
- Assembly programming

For most of the course, you will need access to a **Unix-like environment**, such as Linux or macOS.

There are several ways to obtain such an environment. The main difference between them is **how much of the operating system and hardware is shared with your computer**.

## Which option should I use?

| Option | What runs? | Speed | Setup | Best for |
|---|---|---|---|---|
| **Native Linux / Dual Boot** | Linux runs directly on your hardware | Excellent | More involved | Full Linux experience |
| **WSL** | Linux environment inside Windows | Excellent | Easy | Windows users |
| **Docker** | Isolated Linux container sharing a Linux kernel | Very good | Easy | Course exercises and grading |
| **Virtual Machine** | A complete guest operating system | Good | Moderate | Running a separate OS such as Windows XP |
| **Emulation** | Software imitates another CPU architecture | Slower | More involved | Running x86 software on ARM machines |

---

# 1. Native Linux, Dual Boot, macOS, or WSL

These options give you the most direct Unix-like working environment.

## Native Linux

You can install Linux, such as Ubuntu or Debian, directly on your computer.

In this case:

```text
Hardware
   ↓
Linux
   ↓
Your programs
```

Linux directly controls the computer's hardware and runs its own kernel.

This usually provides the simplest and most complete Linux environment.

## Dual Boot

If you use Windows, you can install Linux alongside Windows.

When the computer starts, you choose which operating system to run:

```text
             ┌── Windows
Hardware ────┤
             └── Linux
```

Only one operating system runs at a time.

Dual boot gives Linux direct access to the hardware, but installation usually requires disk partitioning.

## macOS

macOS is already a Unix-based operating system, so many Unix commands and programming tools work directly from the Terminal.

However, macOS is **not Linux**, so some Linux-specific features, commands, system calls, or `/proc` behavior may differ.

For exercises that specifically require Linux, you can use Docker.

## Windows Subsystem for Linux (WSL)

If you use **Windows 10 or Windows 11**, WSL is usually the easiest way to obtain a Linux environment.

WSL lets you open a Linux shell directly from Windows and use tools such as:

```bash
gcc
g++
gdb
bash
make
```

without rebooting into another operating system.

Conceptually:

```text
Windows
   ↓
WSL
   ↓
Linux environment
   ↓
Your programs
```

Modern WSL versions use a lightweight virtualized Linux kernel, but the integration with Windows is much tighter than with a traditional Virtual Machine.

### Advantages

- Very good performance
- Convenient for Windows users
- Linux tools integrate well with Windows
- No need to reboot between Linux and Windows

### Disadvantages

- Available only on Windows
- A few low-level behaviors may differ from a completely native Linux installation

---

# 2. Docker

Docker is another convenient way to obtain the environment used in CMPE230.

Instead of installing an entire operating system, Docker runs an isolated environment called a **container**.

For example:

```text
Linux
   ↓
Docker
   ↓
CMPE230 container
   ↓
bash, gcc, g++, make, ...
```

A Docker container does **not normally contain its own operating-system kernel**. Instead, multiple containers share the same underlying Linux kernel.

This makes containers much lighter than full Virtual Machines.

We will also use Docker containers to **automatically grade some assignments**, so having Docker installed can be useful even if you already use Linux or WSL.

> **Important:** On Linux, Docker containers can directly use the host Linux kernel. On macOS and Windows, Docker Desktop runs Linux containers inside a small Linux Virtual Machine because macOS and Windows do not provide a Linux kernel.

Conceptually, on macOS:

```text
Mac hardware
     ↓
   macOS
     ↓
Docker Desktop
     ↓
Small Linux VM
     ↓
Linux kernel
     ↓
CMPE230 container
```

You normally do not need to interact with this VM directly; Docker Desktop manages it for you.

## 2.1 Installing Docker

- **Windows/macOS:** Install Docker Desktop.
- **Linux:** Install Docker Engine.

Follow the official Docker installation instructions:

[Docker installation documentation](https://docs.docker.com/engine/install/)

After installation, make sure Docker is running.

## 2.2 Pulling the CMPE230 Image

The course provides a preconfigured **Ubuntu 24.04** Docker image.

Open a terminal and run:

```bash
docker pull gokceuludogan/cmpe230-spring26:latest
```

An **image** is a template containing the files, programs, libraries, and configuration needed for the course.

You can think of it as:

```text
Docker image
     ↓
template
     ↓
Docker container
```

The image itself does not represent a running system. When you run the image, Docker creates a **container** from it.

## 2.3 Running the Container

Run:

```bash
docker run -it --rm gokceuludogan/cmpe230-spring26:latest
```

The options mean:

```text
-it     interactive terminal
--rm    remove the container after you exit
```

After running the command, you should see a Linux shell prompt.

Commands you type there execute **inside the container** rather than directly on your host operating system.

For example:

```bash
uname -a
ls /proc
gcc --version
```

will show information about the Linux environment available to the container.

## 2.4 Using VS Code with Docker

If you use Visual Studio Code, you can work directly inside the container using the **Dev Containers** extension.

1. Install the [Dev Containers extension](https://code.visualstudio.com/docs/devcontainers/containers).
2. Open your project folder in the container.
3. VS Code will use the compilers, libraries, shell, and tools installed inside the Docker environment.

You can then edit files normally in VS Code while your programs execute inside the CMPE230 Linux container.

> If you encounter Docker problems or would like to build the image yourself, see `containers/README.md`.

---

# 3. Virtual Machines

A **Virtual Machine (VM)** behaves like a separate computer running inside your computer.

For example:

```text
Physical computer
      ↓
Host OS
      ↓
Virtualization software
      ↓
Virtual Machine
      ↓
Guest OS
      ↓
Programs
```

Unlike a Docker container, a VM runs a **complete guest operating system with its own kernel**.

For example, on Windows you could run:

```text
Windows
   ↓
VirtualBox
   ↓
Ubuntu VM
   ↓
Linux kernel
   ↓
Your programs
```

or:

```text
macOS
   ↓
Virtualization software
   ↓
Windows VM
   ↓
Windows kernel
   ↓
Your programs
```

The software that creates and manages Virtual Machines is called a **hypervisor**. VirtualBox, VMware, and the virtualization systems used internally by Docker Desktop are examples.

Because a VM contains a complete operating system, it usually requires more memory, disk space, and startup time than a Docker container.

## Course Virtual Machines

We provide [preconfigured `.ova` files](https://zenodo.org/records/7654639) that can be imported into [VirtualBox](https://www.virtualbox.org/):

- **Ubuntu VM:** `CMPE230-Spring23-Ubuntu.ova`
- **Windows XP VM:** `CMPE230-Spring23-XP.ova`

The Ubuntu VM can provide a complete Unix/Linux environment.

The Windows XP VM is useful for some of our **x86 assembly exercises**.

### Advantages

- Runs a complete operating system
- Strong isolation from the host operating system
- Useful when a course exercise requires a specific OS

### Disadvantages

- Uses more RAM and disk space than Docker
- Slower to start
- Some performance overhead
- Architecture compatibility can be a problem

> **Important:** These `.ova` images are designed for **x86 processors**. They do not run directly on Apple Silicon Macs, which use the ARM architecture.

---

# 4. Emulation

Virtualization normally assumes that the guest and host use compatible CPU architectures.

For example:

```text
x86 computer
     ↓
x86 Virtual Machine
```

However, newer Macs with Apple Silicon use the **ARM** architecture.

If you need to run an old **x86 operating system**, such as Windows XP, software can instead **emulate an x86 processor**.

For example:

```text
Apple Silicon Mac
       ↓
ARM processor
       ↓
QEMU / UTM
       ↓
emulated x86 processor
       ↓
Windows XP
```

The emulator translates instructions from one CPU architecture to another.

This provides more flexibility, but it is usually slower than virtualization because CPU instructions may need to be translated while the program runs.

If you need Windows XP on an Apple Silicon Mac, see:

[`XP_UTM.md`](XP_UTM.md)

### Advantages

- Can run software built for a different CPU architecture
- Useful for old operating systems and software

### Disadvantages

- Slower than native execution or virtualization
- More complicated to configure
- Usually unnecessary for normal C/C++ and Unix exercises

---

# Docker vs. Virtual Machine vs. Emulation

These three concepts are easy to confuse.

## Docker container

A container isolates **processes and their environment**, but normally shares a kernel with other containers.

```text
Linux kernel
   ├── Container A
   ├── Container B
   └── Container C
```

It is lightweight and starts quickly.

## Virtual Machine

A VM represents an entire virtual computer and therefore has its **own operating-system kernel**.

```text
Hardware
   ↓
Hypervisor
   ├── VM 1 → Linux kernel
   └── VM 2 → Windows kernel
```

It provides stronger separation but requires more resources.

## Emulator

An emulator can imitate a **different CPU architecture**.

```text
ARM CPU
   ↓
x86 emulator
   ↓
x86 operating system
```

This is useful when the software you need cannot run on your computer's CPU architecture.

---

# Why Do We Provide So Many Options?

Different parts of CMPE230 have different requirements.

### Most Unix and C/C++ exercises

You can use:

```text
Linux
macOS
WSL
Docker
Linux VM
```

### Windows XP / legacy x86 assembly exercises

On an x86 computer:

```text
Windows XP Virtual Machine
```

On an ARM computer such as an Apple Silicon Mac:

```text
Windows XP through QEMU / UTM emulation
```

### Automated assignment grading

We may use:

```text
Docker
```

Using the provided CMPE230 Docker image therefore helps ensure that your program runs in an environment similar to the grading environment.

---

# Troubleshooting & Support

If you encounter a problem:

1. Open an issue in this repository or post on Piazza.
2. Include:
   - Your operating system, for example Windows 11, macOS, or Ubuntu.
   - Your processor architecture if relevant: **x86-64** or **ARM/Apple Silicon**.
   - The steps you followed before the error occurred.
   - The exact command you ran.
   - The complete error message or a screenshot.

Providing this information will make debugging much easier.

---

# Summary

The simplest way to think about the available options is:

```text
Native Linux
    Linux runs directly on the computer.

WSL
    Convenient Linux environment integrated with Windows.

Docker
    Lightweight isolated environment.
    Containers share a Linux kernel.
    Useful for CMPE230 and assignment grading.

Virtual Machine
    A complete virtual computer.
    Runs its own operating system and kernel.

Emulation
    Can additionally imitate another CPU architecture.
    Useful for running x86 Windows XP on ARM machines.
```

### Recommended setup

**Linux users:**  
Use your native Linux installation. Docker is also required for testing assignments.

**Windows users:**  
Use **WSL** for everyday work and Docker when needed for grading or course containers.

**Intel Mac users:**  
Use macOS for general Unix work and Docker when a Linux environment is required.

**Apple Silicon Mac users:**  
Use macOS and Docker for most exercises. Use **UTM/QEMU** when an old x86 environment such as Windows XP is specifically required.
