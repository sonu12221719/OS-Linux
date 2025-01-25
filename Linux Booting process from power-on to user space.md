# Linux Booting Process: From Power-On to User Space

## Introduction
The Linux boot process is a sequence of events that takes place when a computer is powered on and prepares the system for user operations. This document explains the detailed step-by-step Linux booting process, starting from when electricity hits the system to reaching a fully functional operating system.

## 1. Power-On and BIOS/UEFI Initialization
### **BIOS (Basic Input/Output System) / UEFI (Unified Extensible Firmware Interface)**
- When power is supplied, the **BIOS/UEFI firmware** is the first program that runs.
- It performs a **Power-On Self Test (POST)** to check CPU, RAM, and connected peripherals.
- BIOS/UEFI searches for a **bootable device** (HDD, SSD, USB, or Network PXE boot).
- Once a bootable device is found, BIOS loads the first sector, called the **MBR (Master Boot Record) or GPT (GUID Partition Table)**.

## 2. Master Boot Record (MBR) or GUID Partition Table (GPT)
- The **MBR (located in the first 512 bytes of the boot disk)** contains:
  - Bootloader code
  - Partition table
  - Signature
- In modern systems, **GPT replaces MBR**, offering better partitioning.
- The MBR/GPT directs control to the bootloader (GRUB in most cases).

## 3. GRUB (Grand Unified Bootloader)
- GRUB is responsible for:
  - Displaying the boot menu (if multiple OS options exist)
  - Loading the selected **kernel** into memory
  - Passing necessary parameters to the kernel
- GRUB configuration file: `/boot/grub/grub.cfg`
- GRUB loads the **kernel** and the **initial RAM disk (initrd or initramfs)**.

## 4. Kernel Initialization
- The **Linux kernel** is loaded into memory and starts execution.
- It performs:
  - **Hardware detection and initialization**
  - **Mounting the root filesystem** (using initrd or initramfs temporarily)
  - **Starting system processes**
- The kernel executes the first user-space process, **init** (or systemd in modern Linux systems).

## 5. Init/Systemd Process
- **init/systemd** is the **parent process** of all other processes.
- It reads configuration files from `/etc/inittab` (SysV init) or systemd targets.
- It determines the **default runlevel/target** and starts services accordingly.

## 6. Runlevel / Systemd Targets
### **Runlevels (SysV init)**
| Runlevel | Mode Description |
|----------|----------------|
| 0 | Halt (Shutdown) |
| 1 | Single-user mode (Recovery mode) |
| 2 | Multi-user mode (without networking) |
| 3 | Multi-user mode (with networking) |
| 4 | Unused (custom use) |
| 5 | Multi-user mode with GUI |
| 6 | Reboot |

### **Systemd Targets (Modern Linux Systems)**
| Target | Description |
|--------|-------------|
| poweroff.target | Shutdown system |
| rescue.target | Single-user mode |
| multi-user.target | Multi-user CLI mode |
| graphical.target | Multi-user GUI mode |
| reboot.target | Reboot system |

## 7. User Space & Login Prompt
- Once the correct **runlevel/target** is reached, the system provides:
  - **Login prompt (CLI mode)** or **GUI desktop environment**
  - Users can now log in and start using the system.

## Summary of Linux Boot Sequence
1. **Power-On → BIOS/UEFI → POST Check**
2. **BIOS/UEFI loads MBR/GPT from the boot device**
3. **MBR/GPT loads GRUB (Bootloader)**
4. **GRUB loads the Linux kernel & initrd/initramfs**
5. **Kernel initializes hardware, mounts root filesystem**
6. **Kernel starts init/systemd (first user-space process)**
7. **init/systemd determines runlevel/target and starts services**
8. **System reaches user space → Login prompt (CLI or GUI)**

## Linux Boot Process Flow Diagram
![Linux Boot Process](https://upload.wikimedia.org/wikipedia/commons/9/9e/Linux_bootup_process.png)

## Conclusion
The Linux booting process is a structured sequence that ensures the system initializes correctly from power-on to a usable state. Understanding this process is essential for troubleshooting boot issues and optimizing system startup.

---
