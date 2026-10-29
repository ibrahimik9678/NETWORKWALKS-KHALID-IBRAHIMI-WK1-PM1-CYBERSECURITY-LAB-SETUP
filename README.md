# Cybersecurity Lab Environment Setup

**NetworkWalks Cybersecurity Internship | Week 1 – Project Module 1 (WK1-PM1)**

**Intern:** Khalid Ibrahimi  
**Project:** VirtualBox and Kali Linux Cybersecurity Lab Setup  
**Date:** October 29, 2026

## 1. Project Overview

As part of my NetworkWalks Cybersecurity Internship, I configured a virtual cybersecurity laboratory using Oracle VirtualBox and Kali Linux.

The objective was to create a controlled environment for learning cybersecurity, practicing ethical hacking techniques, and preparing for future penetration testing exercises.

This project involved configuring a virtual machine, setting up network connectivity, enabling file sharing between the host and guest operating systems, and creating a snapshot for recovery.

## 2. Tools and Technologies

| Technology | Configuration |
|---|---|
| Virtualization Platform | Oracle VirtualBox 7.2.22 |
| Guest Operating System | Kali Linux 2026.3 (64-bit) |
| Host Operating System | Windows |
| Virtual Machine RAM | 2048 MB |
| Virtual CPUs | 2 |
| Virtual Disk | 80.09 GB |
| Network Type | NAT Network |
| Network Subnet | 10.0.0.0/24 |
| Kali Linux IP | 10.0.0.2/24 |
| Default Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |

## 3. VirtualBox and Kali Linux Installation

I installed Oracle VirtualBox on my Windows laptop and downloaded the official Kali Linux 2026.3 prebuilt VirtualBox image.

After extracting the downloaded archive, I registered the virtual machine using its `.vbox` configuration file.

The Kali Linux virtual machine was successfully started and configured.

![VirtualBox Manager](1.%20VirtualBox%20Manager.png)

## 4. Network Configuration

I created a custom NAT Network in VirtualBox with the following settings:

- **Network Name:** NatNetwork
- **IPv4 Prefix:** 10.0.0.0/24
- **DHCP Server:** Enabled
- **IPv6:** Disabled

I connected Kali Linux's first network adapter to the configured NAT Network.

![NAT Network Configuration](2.%20NAT%20Network%20Configration.png)

### Static IP Configuration

I configured the Kali Linux network interface `eth0` using NetworkManager.

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.addresses 10.0.0.2/24 ipv4.gateway 10.0.0.1 ipv4.dns "8.8.8.8" ipv4.method manual
```

I then applied the configuration:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

## 5. Network and Internet Verification

I verified the configured IP address using:

```bash
ip -4 addr show eth0
```

I tested internet connectivity and DNS resolution using:

```bash
ping -c 4 8.8.8.8
ping -c 4 google.com
```

**Test Results:**

- Static IP: 10.0.0.2/24
- Google DNS ping: 4 packets transmitted, 4 received
- Google.com ping: 4 packets transmitted, 4 received
- Packet loss: 0%

Both tests completed successfully.

![Static IP and Internet Test](3.%20Static%20IP%20and%20Internet%20Test.png)

## 6. Shared Folder Configuration

I configured a VirtualBox shared folder to exchange files between Windows and Kali Linux.

**Configuration:**

- Windows Host Folder: `D:\Cybermacs\internship lab`
- Shared Folder Name: `internship_lab`
- Kali Linux Mount Point: `/downloads`
- Auto-mount: Enabled

I verified the shared folder using:

```bash
ls -la /downloads
```

The command displayed files from the Windows host folder, confirming successful shared folder access.

![Shared Folder Verification](4.%20Shared%20Folder%20Verification.png)

## 7. Shared Clipboard and Drag-and-Drop Configuration

I enabled bidirectional shared clipboard and drag-and-drop in VirtualBox settings.

I verified shared clipboard functionality by transferring text from Windows into the Mousepad text editor in Kali Linux.

![Shared Clipboard](5.%20Shared%20Clipboard.png)

## 8. Virtual Machine Snapshot

After completing the lab configuration, I created a VirtualBox snapshot.

**Snapshot Name:** `WK1-PM1-Kali-Lab-Setup`

The snapshot preserves the configured lab environment and provides a recovery point for future cybersecurity exercises.

![VirtualBox Snapshot](6.%20Snapshot.png)

## 9. Project Results

The following components were successfully configured and verified:

- Kali Linux virtual machine
- Custom VirtualBox NAT Network
- Static IPv4 addressing
- Internet connectivity and DNS resolution
- Shared clipboard
- Shared folder access
- Virtual machine snapshot

## 10. Learning Outcomes

Through this project, I gained practical experience in:

- Installing and configuring virtual machines
- Understanding NAT networking and IPv4 subnetting
- Managing Linux network connections using `nmcli`
- Configuring static IP addresses and DNS
- Troubleshooting and testing network connectivity
- Sharing files between host and guest operating systems
- Creating virtual machine snapshots for recovery

## 11. Conclusion

This project helped me develop practical skills in virtualization, Linux administration, and network configuration.

I now have a functioning Kali Linux cybersecurity laboratory that I can use for future authorized security testing, networking exercises, and cybersecurity learning activities.

---

**NetworkWalks Cybersecurity Internship – Week 1, Project Module 1**

*All practical activities were performed in my own virtual lab environment for educational purposes.*
