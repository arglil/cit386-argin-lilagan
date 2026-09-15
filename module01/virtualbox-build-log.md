# CIT 386 Module 1 - VirtualBox Build Log

## Host Computer

- Make and model: Dell Latitude 5320
- Processor: Intel Core i7-1185G7 @ 3.00 GHz
- Memory: 32 GB RAM
- Operating system: Windows 11 Pro
- BIOS mode: UEFI
- Virtualization: Enabled in BIOS/UEFI

Virtualization was disabled when I first tried to set up the VM. I went into the BIOS/UEFI settings and enabled it. After restarting the laptop, VirtualBox worked correctly.

## Virtual Machine Settings

- VM name: CIT386-VM01
- Guest OS: Ubuntu Linux 64-bit
- Ubuntu version: Ubuntu Server 26.04.1 LTS
- Memory: 4 GB
- Processors: 2
- Disk size: 25 GB
- Disk format: VDI
- Disk type: Dynamically allocated

## Reasons for My Settings

I named the VM CIT386-VM01 so I could easily identify it as my CIT 386 VM.

I chose Ubuntu Server because it works well for networking and cloud labs.

I chose 4 GB of memory because my laptop has 32 GB. This gives the VM enough memory while leaving plenty of memory for Windows.

I chose 2 processors because it gives the VM enough processing power without using all of my laptop's CPU resources.

I chose a 25 GB disk because it gives me enough space for Ubuntu and my class work.

I used the VDI format because it is VirtualBox's virtual disk format. I chose dynamically allocated storage so the disk only uses the physical storage it needs instead of taking the full 25 GB immediately.

## Virtual Disk

Full path:

`C:\Users\lilag\VirtualBox VMs\CIT386-VM01\CIT386-VM01.vdi`

- Virtual disk size: 25 GB
- Current file size: 5.53 GB
- Size on disk: 5.53 GB

The virtual disk can grow up to 25 GB, but it currently uses only 5.53 GB on my laptop because it is dynamically allocated.

## Problem I Had

The VM did not work correctly at first because virtualization was disabled on my laptop. I enabled virtualization in the BIOS/UEFI and restarted the computer. After that, I was able to create and run the VM.

## Result

I successfully created the VirtualBox VM, installed Ubuntu Server, and logged into the server.