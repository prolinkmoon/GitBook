# Virtualization

## 🧩 Virtualization (Running VMs on Your Local PC)

You don’t need to rent a server to learn how to run a node. You can use **your own laptop or PC** and create a virtual machine (VM) inside it. This is called **local virtualization**.

***

### 🧠 What is a Virtual Machine?

A **Virtual Machine (VM)** is like a computer inside your computer. It runs its own operating system — like Ubuntu Linux — without touching your main OS.

This lets you:

* Practice using Linux
* Simulate a VPS
* Install and test a node locally

***

### 💻 Common Virtualization Tools

| Tool           | OS Support              | Use Case                             |
| -------------- | ----------------------- | ------------------------------------ |
| **WSL**        | Windows only            | Lightweight Linux shell              |
| **VirtualBox** | Windows / macOS / Linux | Full Linux VM (Ubuntu, Debian, etc.) |
| **VMware**     | Windows / macOS         | More advanced than VirtualBox        |
| **UTM**        | macOS (M1/M2)           | Lightweight VM for Mac               |

***

### ✅ When to Use Local VMs

Use virtualization if you:

* Are still learning
* Don’t want to pay for a server yet
* Want to test commands safely

***

### ⚙️ How to Install a Virtual Machine

#### 🔹 Option 1: WSL (Windows Subsystem for Linux)

**For Windows 10/11 users.**

1. Open PowerShell as Administrator
2.  Run this command:

    ```powershell
    wsl --install
    ```
3. Reboot your PC
4. It will auto-install Ubuntu (or let you choose)
5. After reboot, type `wsl` in Start Menu — your Ubuntu terminal is ready!

> ✅ WSL is fast, easy, and works well for learning CLI and building tools.

***

#### 🔹 Option 2: VirtualBox (Cross-platform)

1. Download VirtualBox from: [https://www.virtualbox.org](https://www.virtualbox.org)
2. Download Ubuntu ISO: [https://ubuntu.com/download/desktop](https://ubuntu.com/download/desktop)
3. Open VirtualBox → New → Name: `Ubuntu Node`
4. Set RAM (at least 2048 MB), CPU (2 cores)
5. Attach ISO in storage settings
6. Start the VM and follow the Ubuntu installation steps

> 🧪 You now have a full Linux environment to test anything.

***

#### 🔹 Option 3: VMware Workstation / Fusion

* Download VMware Workstation Player (Windows/Linux) or Fusion (macOS)
* Install Ubuntu using the same steps as VirtualBox

> VMware is smoother and more feature-rich, but not 100% free.

***

#### 🔹 Option 4: UTM (for Apple Silicon - M1/M2)

1. Download UTM: https://mac.getutm.app
2. Download Ubuntu ARM ISO
3. Create a new virtual machine → choose "Virtualize" → select ISO
4. Configure RAM (2–4 GB), CPU (2–4 cores)
5. Boot and install Ubuntu

> 💡 UTM works well for newer Macs without needing extra tools.

***

### 🚀 After Installation

Once your Linux VM is ready, you can:

* Open the terminal
* Use basic Linux commands (`cd`, `ls`, `apt install`, etc.)
* Try installing a node from a GitHub repo
* Simulate a testnet setup

***

### 📌 Tips

* Always enable virtualization in your BIOS (check your PC settings)
* Allocate enough RAM or it will run slowly
* Use snapshots/checkpoints before testing major things

***

🧠 Virtual machines are perfect for experimenting, learning, and building confidence — before you go live on an actual server or mainnet.

Next up → **"Linux/Ubuntu - Basics"**
