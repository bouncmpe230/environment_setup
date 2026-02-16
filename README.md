# CMPE230: Environment Setup

Welcome to the **CMPE230 Systems Programming** course! Throughout this semester, we'll be doing a variety of hands-on exercises, including **Unix command practice**, **C/C++ programming** and **Assembly programming**. To ensure everyone can participate effectively, you will need access to a Unix-like environment (e.g., **Ubuntu**, **Debian**, or **macOS**) for most of our sessions.

Below are the recommended ways to set up your development environment, in order of effectiveness:


## 1. Native Installation / Dual Boot / WSL
- **Native Installation**: You can install Linux (e.g., Ubuntu) directly on your computer. This provides the most integrated experience, but it requires partitioning your hard drive.
- **Dual Boot**: If you're already on Windows, you can have both Windows and Linux on your machine, choosing which to run at startup.
- **Windows Subsystem for Linux (WSL)**: If you are a Windows 10 or 11 user, installing WSL is a convenient option. It's effectively a Linux environment running within Windows, allowing you to use Linux commands without leaving Windows.

**Pros**: Full access to hardware, consistent performance, no virtualization overhead.  

**Cons**: Installation can be more time-consuming or require disk partitioning (for native/dual boot).



## 2. Docker (Containerization)
For those who **cannot or prefer not** to install Linux natively (or WSL), **Docker** is the next best option. We will also use Docker containers to **grade some of your projects** automatically, so having Docker set up is especially convenient.  

> **Note**: If you're on **macOS** or **Windows**, Docker Desktop is available. On **Linux**, you can install Docker Engine directly.

### 2.1 Installing Docker
1. Visit the official [Docker Engine installation page](https://docs.docker.com/engine/install/).
2. Follow the instructions for your operating system to install and **start** the Docker service.

### 2.2 Pulling the CMPE230 Image
Open your terminal and run:
```bash
docker pull gokceuludogan/cmpe230_spring25:latest
```
This downloads our Ubuntu 24.04-based container image, preconfigured for CMPE230.


### 2.3 Running the Container
Once the image is downloaded, start a container with:

```bash
docker run -it --rm gokceuludogan/cmpe230_spring25:latest
```
- -it keeps an interactive terminal, so you can type commands inside Ubuntu.
- --rm ensures the container is removed when you exit.
Now you should see a Linux shell prompt inside the container. You can practice your Unix commands here.



### 2.4 Using VSCode with Docker
If you use Visual Studio Code, there is a helpful extension called Remote - Containers:
1. Install [Remote - Containers](https://code.visualstudio.com/docs/devcontainers/containers) from the VSCode Extension Marketplace.
2. You can open a folder inside the Docker container directly. This way, you get all the VSCode features, just as if you were coding on a local machine. 

> **Note**: If you encounter any problems or would like to build your own Docker image, see `containers/README.md` for detailed instructions.


   
## 3. Virtualization (VirtualBox, VMware)
As an alternative, you can also run a virtual machine. We provide [preconfigured .ova files](https://zenodo.org/records/7654639) (for both Ubuntu and Windows XP), which you can import into [VirtualBox](https://www.virtualbox.org/):
- **Ubuntu VM**: CMPE230-Spring23-Ubuntu.ova (still suitable for a Unix environment).
- **Windows XP VM**: CMPE230-Spring23-XP.ova (needed for our x86 assembly labs).
  

**Pros**: Offers isolation (your host system remains untouched) and can run multiple OSes side by side.

**Cons**: Some performance overhead, potential compatibility issues on ARM-based systems (e.g., new MacBooks).

> **Note**: These images are only for x86 architectures and do not work on Apple Silicon (ARM) Macs without additional emulation.




## 4. Emulation (QEMU)
If you're on a machine that isn't x86 (such as Apple Silicon) and you must run Windows XP or x86 Linux, you can consider QEMU for emulation. This is more complex and typically less performant. See [the instructions](XP_UTM.md) to run Windows XP on MacOS with Apple Silicon using UTM.  

**Pros**: Can emulate different CPU architectures, flexible. 

**Cons**: Setup is more involved; performance is slower than native or Docker.



## Why So Many Options?
* Most of the course can be done in a Unix environment for C programming, shell scripting, etc.
* We have a few labs/sessions requiring Windows XP for x86 assembly, which is why a VM or emulator might be necessary.
* Docker is widely used in industry and great for quickly setting up consistent environments and we'll also use it to auto-grade your assignments.


## Troubleshooting & Support
If you face any issues:
1. Open an issue in this repository or post on the Piazza forum. 
2. Include:
    * Your operating system (e.g., Windows 10, macOS Ventura, Ubuntu 22.04).
    * What steps you followed when the error occurred.
    * A screenshot or copy of the error message.


# Summary
1. **Preferred approach:** Use a Unix-based OS directly or via WSL if on Windows.
2. **Next best:** Use Docker to run our pre-configured Ubuntu 24.04 container (same setup we'll use for grading).
3. **If you need Windows XP for x86 assembly labs:** Use VirtualBox or QEMU if you're on Apple Silicon.
4. Ask questions if you get stuck. We're here to help!
 
