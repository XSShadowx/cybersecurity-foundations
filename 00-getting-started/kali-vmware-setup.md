# Kali Linux Setup Using VMware Workstation Pro (ISO Installation)

This guide provides a **full, from-scratch walkthrough** for installing **Kali Linux inside VMware Workstation Pro** using the **official Kali Linux Installer ISO**.

> This guide intentionally links to official vendor and distribution documentation.
> When in doubt, always defer to upstream sources.


This method intentionally avoids prebuilt VMware images. Installing from ISO forces you to understand how Linux systems are installed, configured, and maintained — a critical skill for anyone pursuing cybersecurity, penetration testing, or system administration.

---

## Why Use VMware Workstation Pro?

VMware Workstation Pro is now **free for personal use**, making it one of the best virtualization platforms available to beginners and professionals alike.

A full virtual machine is preferred over WSL when:

* You need kernel-level access
* You want realistic privilege escalation practice
* You rely on snapshots and rollback
* You are working with exploit development or system internals

This setup mirrors how labs and enterprise environments are commonly built.

---

## Hardware and System Requirements

Minimum requirements:

* Windows 10 or Windows 11 (64-bit)
* CPU with virtualization support (Intel VT-x or AMD-V)
* 8 GB RAM
* 40 GB free disk space

Recommended:

* 16 GB RAM or more
* SSD storage
* 4 CPU cores available for the VM

---

## Step 1: Enable Virtualization in BIOS/UEFI

Before installing VMware, virtualization **must** be enabled at the firmware level. Without this, VMware Workstation Pro will either fail to start virtual machines or fall back to limited functionality.

Official references:

* Intel Virtualization Technology (VT-x): [https://www.intel.com/content/www/us/en/support/articles/000005486/processors.html](https://www.intel.com/content/www/us/en/support/articles/000005486/processors.html)
* AMD Virtualization (AMD-V / SVM): [https://www.amd.com/en/support/kb/faq/pa-01](https://www.amd.com/en/support/kb/faq/pa-01)

Vendor BIOS access keys vary by manufacturer. Common keys include **DEL**, **F2**, **F10**, and **ESC**.

After enabling virtualization, save changes and reboot.

Before installing VMware, ensure virtualization is enabled.

1. Reboot your system
2. Enter BIOS/UEFI (usually **DEL**, **F2**, **F10**, or **ESC**)
3. Locate CPU or Advanced settings
4. Enable:

   * **Intel Virtualization Technology (VT-x)** or
   * **SVM Mode / AMD-V**
5. Save and reboot

If virtualization is disabled, VMware will not function correctly.

---

## Step 2: Install VMware Workstation Pro

VMware Workstation Pro is officially free for **personal use**.

Official download page:

* VMware Workstation Pro: [https://www.vmware.com/products/workstation-pro.html](https://www.vmware.com/products/workstation-pro.html)

Installation notes:

* Use the Windows installer
* Select the personal use license when prompted
* Default installation options are sufficient for most users

After installation, launch VMware Workstation Pro to confirm it opens without errors.

1. Navigate to the official VMware website
2. Download **VMware Workstation Pro** for Windows
3. Select the **Free for Personal Use** option
4. Run the installer
5. Accept defaults unless you have specific requirements
6. Reboot if prompted

After installation, launch VMware to confirm it opens without errors.

---

## Step 3: Download the Kali Linux Installer ISO

Always download Kali images directly from the official source.

Official Kali download pages:

* Kali Linux Downloads: [https://www.kali.org/get-kali/](https://www.kali.org/get-kali/)
* Kali Installer ISO documentation: [https://www.kali.org/docs/installation/](https://www.kali.org/docs/installation/)

Select:

* **Installer** → **Kali Linux Installer (64-bit)**

Do not use:

* Live ISO (meant for temporary sessions)
* Prebuilt VMware images (skip installation fundamentals)

Verify checksums when possible to ensure image integrity.

1. Go to the official Kali Linux website
2. Navigate to **Downloads → Installer**
3. Download the **Kali Linux Installer ISO** (64-bit)

Important notes:

* Do **not** download the Live ISO
* Do **not** use the prebuilt VMware image

The installer ISO provides a full Debian-style installation with complete control.

---

## Step 4: Create a New Virtual Machine

VMware VM creation documentation:

* VMware New Virtual Machine Wizard: [https://docs.vmware.com/en/VMware-Workstation-Pro/index.html](https://docs.vmware.com/en/VMware-Workstation-Pro/index.html)

Creation steps:

1. Open **VMware Workstation Pro**

2. Click **Create a New Virtual Machine**

3. Choose **Typical (recommended)**

4. Select **Installer disc image file (ISO)**

5. Browse to the Kali Linux ISO

6. Continue and allow VMware OS detection if prompted

7. Open **VMware Workstation Pro**

8. Click **Create a New Virtual Machine**

9. Choose **Typical (recommended)**

10. Select **Installer disc image file (ISO)**

11. Browse to the Kali ISO you downloaded

12. Continue

If VMware detects the OS automatically, allow it to proceed.

---

## Step 5: Virtual Machine Hardware Configuration

Use the following recommended settings:

* **Operating System:** Linux
* **Version:** Debian GNU/Linux (latest available)
* **Processors:** 2–4 cores
* **Memory:** 8 GB (4 GB minimum)
* **Network:** NAT
* **Disk Size:** 40–80 GB
* **Disk Type:** Single file preferred

These settings balance performance and stability for lab use.

---

## Step 6: Kali Linux Installation Process

Kali installation follows the standard Debian installer workflow.

Official documentation:

* Kali Linux Installation Guide: [https://www.kali.org/docs/installation/hard-disk-install/](https://www.kali.org/docs/installation/hard-disk-install/)

Boot steps:

1. Power on the VM
2. Select:

   ```
   Graphical Install
   ```

Follow on-screen prompts for language, location, keyboard, and networking.

Disk partitioning reference:

* Debian Guided Partitioning: [https://www.debian.org/releases/stable/amd64/apcs04.en.html](https://www.debian.org/releases/stable/amd64/apcs04.en.html)

1. Power on the VM
2. At the boot menu, select:

   ```
   Graphical Install
   ```

### Installation Steps

* Choose language, location, and keyboard layout
* Configure networking (DHCP is sufficient)
* Set hostname (e.g., `kali`)
* Create a user account and strong password

### Disk Partitioning

Select:

* **Guided – use entire disk**
* **All files in one partition**

This is recommended for beginners and lab environments.

Proceed with installation until completion.

---

## Step 7: Install the GRUB Bootloader

When prompted:

* Install GRUB to the default disk
* Accept the recommended option

GRUB is required to boot Kali properly.

---

## Step 8: First Boot and System Update

After rebooting into Kali:

```bash
sudo apt update && sudo apt full-upgrade -y
```

This ensures:

* Latest security patches
* Updated repositories
* Reduced tool errors later

Reboot once updates complete.

---

## Step 9: Install VMware Tools (Critical)

VMware Tools documentation:

* VMware Tools Overview: [https://docs.vmware.com/en/VMware-Tools/index.html](https://docs.vmware.com/en/VMware-Tools/index.html)

Why this matters:

* Enables dynamic resolution
* Improves mouse and keyboard handling
* Allows clipboard and drag-and-drop

Dependency reference:

* Linux kernel headers: [https://wiki.debian.org/Headers](https://wiki.debian.org/Headers)

Install prerequisites:

```bash
sudo apt install -y build-essential dkms linux-headers-$(uname -r)
```

VMware Tools improves:

* Display resolution
* Mouse capture
* Clipboard sharing
* System performance

### Install Dependencies

```bash
sudo apt install -y build-essential dkms linux-headers-$(uname -r)
```

### Install Tools

From the VMware menu:

```
VM → Install VMware Tools
```

Mount the CD and run the installer inside Kali.

Reboot after installation.

---

## Step 10: Take a Clean Snapshot

Before installing tools or starting labs:

1. Shut down the VM
2. Take a snapshot
3. Name it:

   ```
   Clean Kali ISO Install
   ```

Snapshots allow instant rollback if something breaks.

---

## Common Issues and Troubleshooting

### Black Screen or Low Resolution

* Ensure VMware Tools is installed
* Verify display settings inside Kali

### VM Fails to Start

* Check virtualization is enabled in BIOS
* Disable Hyper-V if conflicts occur

### Slow Performance

* Increase RAM or CPU cores
* Ensure host system is not overcommitted

---

## Security and Ethics Reminder

This environment is intended for **education and authorized testing only**.

Never run tools against systems you do not own or have explicit permission to test.

---

**Environment Type:** Virtual Machine
**Installation Method:** Manual ISO install
**Skill Level:** Beginner to Intermediate
**Use Case:** Labs, exploit development, realistic practice
