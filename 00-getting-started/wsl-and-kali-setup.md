# Installing WSL (Windows Subsystem for Linux) and Kali Linux on Windows 10 & 11

This write-up walks through setting up **WSL 2** on Windows and installing **Kali Linux** inside it. This is aimed at beginners getting into cybersecurity, penetration testing, or Linux development, and is written so it can stand alone as a GitHub repository README or blog-style guide.

I’ll cover:

* What WSL is and why it matters
* Installing WSL on Windows 11
* Installing WSL on Windows 10
* Installing Kali Linux on WSL
* Post-install setup and verification
* Common issues and fixes

---

## What is WSL and Why Use It?

**Windows Subsystem for Linux (WSL)** lets you run a real Linux environment directly on Windows, without needing a full virtual machine. With **WSL 2**, Linux runs using a lightweight virtualized kernel that gives near-native performance.

Why this is useful:

* No dual booting
* No heavy VM overhead
* Direct access to Linux tools from Windows
* Perfect for cybersecurity labs, scripting, and development

Kali Linux is especially popular because it comes preloaded with hundreds of security and penetration testing tools.

---

## System Requirements

Before starting, make sure:

* You’re running **Windows 10 version 2004+** or **Windows 11**
* Virtualization is enabled in BIOS/UEFI
* You have administrator privileges

To check your Windows version:

1. Press **Win + R**
2. Type `winver`
3. Press Enter

---

## Installing WSL on Windows 11

Windows 11 has the easiest setup.

### Step 1: Open an Administrator Terminal

1. Right-click the **Start Menu**
2. Select **Windows Terminal (Admin)**

### Step 2: Install WSL

Run:

```
wsl --install
```

This command automatically:

* Enables required Windows features
* Installs WSL 2
* Sets WSL 2 as default
* Installs a default Linux distro (usually Ubuntu)

### Step 3: Reboot

Restart your system when prompted.

After reboot, WSL is ready.

---

## Installing WSL on Windows 10

Windows 10 requires a few extra checks but is still straightforward.

### Step 1: Enable Required Features

Open **PowerShell as Administrator** and run:

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Restart your computer after this.

### Step 2: Set WSL 2 as Default

After reboot, open PowerShell (Admin) and run:

```
wsl --set-default-version 2
```

### Step 3: Install the WSL Kernel Update (if needed)

If Windows tells you the kernel is missing:

* Download the **WSL 2 Linux kernel update package** from Microsoft
* Install it like a normal program

---

## Installing Kali Linux on WSL

Once WSL is installed, installing Kali is simple.

### Option 1: Microsoft Store (Recommended)

1. Open the **Microsoft Store**
2. Search for **Kali Linux**
3. Click **Install**

After installation, launch Kali from the Start Menu.

### Option 2: Command Line Install

You can also install it directly from the terminal:

```
wsl --install -d kali-linux
```

---

## First-Time Kali Setup

When Kali launches for the first time:

* You’ll be prompted to create a **username**
* You’ll set a **password** (this is your Linux user password)

Once complete, you’ll be dropped into the Kali shell.

Verify your install:

```
uname -a
lsb_release -a
```

You should see Kali Linux listed.

---

## Updating Kali (Important)

Always update before installing tools:

```
sudo apt update && sudo apt full-upgrade -y
```

This ensures:

* Latest security patches
* Updated tools
* Fewer dependency issues later

---

## Installing Kali Metapackages (Optional)

By default, Kali on WSL installs minimal tools.

Example: install common penetration testing tools

```
sudo apt install kali-linux-default -y
```

For a lighter setup:

```
sudo apt install kali-linux-headless -y
```

Avoid `kali-linux-everything` unless you know what you’re doing — it’s massive.

---

## Using Kali with Windows

Useful tips:

* Access Windows files from Kali:

```
cd /mnt/c/Users/YourUsername
```

* Run Windows commands from Kali:

```
cmd.exe /c dir
```

* Run Kali anytime from Windows Terminal:

```
wsl -d kali-linux
```

---

## Common Issues and Fixes

### WSL Version Is 1 Instead of 2

Check:

```
wsl -l -v
```

If Kali is using WSL 1:

```
wsl --set-version kali-linux 2
```

---

### Virtualization Not Enabled

Symptoms:

* WSL 2 fails to start
* Errors mentioning virtualization

Fix:

* Reboot into BIOS/UEFI
* Enable **Intel VT-x** or **AMD-V / SVM**
* Save and reboot

---

### Kali Fails to Launch

Try:

```
wsl --shutdown
```

Then relaunch Kali.

---

## Final Notes

This setup is ideal for:

* Learning Linux
* Cybersecurity labs
* Scripting and automation
* Bug bounty and pentesting practice

WSL + Kali gives you a clean, fast, and professional environment that’s perfect for showcasing real-world skills to employers.

This repository will continue to grow with:

* Tool setup guides
* Lab write-ups
* Realistic attack walkthroughs

---

**Author:** Christopher Heard
