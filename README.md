# Week 1 – Project Module 1: Cybersecurity Lab Setup Using VirtualBox and Kali Linux

## 1. Project Overview

As part of my cybersecurity internship, I completed the initial setup of a cybersecurity testing lab using Oracle VirtualBox and Kali Linux.

The main objective of this assignment was to create a virtual environment for cybersecurity practice, configure network connectivity, assign a static IPv4 address to Kali Linux, and prepare the environment for future ethical hacking and security testing exercises.

This repository documents my lab configuration, network verification, screenshots, and troubleshooting experience.

## 2. Objectives

- Install and configure Oracle VirtualBox.
- Import and configure Kali Linux as a virtual machine.
- Create a custom NAT Network using the `10.0.0.0/24` subnet.
- Configure Kali Linux with the required static IP address `10.0.0.2/24`.
- Verify gateway and internet connectivity.
- Check VirtualBox clipboard, drag-and-drop, and shared-folder settings.
- Create a virtual machine snapshot for recovery.

## 3. System Specifications

The following are the specifications of my laptop and the software used for this lab setup.

| Component | Configuration |
|---|---|
| Host Operating System | Microsoft Windows 11 Home Single Language |
| Windows Version | 10.0.26200 (Build 26200) |
| Processor | AMD Ryzen 7 7445HS with Radeon 740M Graphics |
| CPU Cores | 6 Cores, 12 Logical Processors |
| Installed RAM | 16 GB |
| Virtualization Software | Oracle VirtualBox 7.2.6 |
| VirtualBox Build | r172322 |
| Virtual Machine OS | Kali GNU/Linux Rolling 2026.1 |
| Linux Kernel | 6.18.12+kali-amd64 |

## 4. Lab Network Configuration

The lab uses a custom NAT Network to connect the Kali Linux virtual machine to the network and provide internet access.

| Network Parameter | Configuration |
|---|---|
| Network Name | Cybersecurity-lab |
| Network Mode | NAT Network |
| IPv4 Network Prefix | `10.0.0.0/24` |
| Kali Linux Interface | `eth0` |
| Kali Linux IPv4 Address | `10.0.0.2/24` |
| Default Gateway | `10.0.0.1` |
| DNS Servers | `1.1.1.1`, `8.8.8.8` |

The host laptop's network configuration was not changed to match the lab subnet. The static IPv4 address was configured inside the Kali Linux virtual machine.

## 5. Implementation Procedure

### Step 1: Install VirtualBox

Installed Oracle VirtualBox on my Windows 11 laptop to create and manage virtual machines for cybersecurity practice.

### Step 2: Import Kali Linux

Downloaded and configured the Kali Linux virtual machine in VirtualBox.

The installed Kali Linux environment was verified using:

```bash
cat /etc/os-release
uname -r
```

### Step 3: Create the NAT Network

Created a custom NAT Network named `Cybersecurity-lab` and configured the IPv4 network prefix as:

```text
10.0.0.0/24
```

This subnet provides the addressing range for the virtual lab.

### Step 4: Configure the Kali Linux VM

Configured the Kali Linux virtual machine to use the custom NAT Network through its virtual network adapter.

The required network configuration was applied inside Kali Linux using NetworkManager.

### Step 5: Configure the Static IPv4 Address

Initially, the `eth0` interface displayed an IPv6 address but did not have an IPv4 address.

To resolve this, configured the wired connection with a static IPv4 address using:

```bash
sudo nmcli connection modify "Wired connection 1" \
ipv4.method manual \
ipv4.addresses 10.0.0.2/24 \
ipv4.gateway 10.0.0.1 \
ipv4.dns "1.1.1.1 8.8.8.8"
```

Reactivated the connection:

```bash
sudo nmcli connection up "Wired connection 1"
```

### Step 6: Verify Network Configuration

Used the following commands to inspect the network interface and routing table:

```bash
ip -br addr
ip route
nmcli connection show
```

The Kali Linux interface successfully displayed the configured IPv4 address:

```text
eth0    UP    10.0.0.2/24
```

The routing table showed the default gateway as `10.0.0.1`.

### Step 7: Test Network Connectivity

Tested connectivity to the gateway and an external IP address:

```bash
ping -c 4 10.0.0.1
ping -c 4 1.1.1.1
```

Both tests returned four successful replies with zero packet loss.

DNS resolution was also tested using:

```bash
ping -c 4 google.com
```

The DNS test should be recorded as successful only after confirming the actual command output.

### Step 8: Check VirtualBox Integration Settings

Checked the available settings for shared clipboard, drag-and-drop, and shared folders.

The `General → Advanced` menu mentioned in the assignment guide was not visible in my VirtualBox interface. I documented this difference rather than claiming that the unavailable settings were enabled.

The availability and operation of clipboard integration, drag-and-drop, and the shared Downloads folder require separate verification.

### Step 9: Create a VM Snapshot

The assignment requires a snapshot of the configured Kali Linux virtual machine.

After completing and verifying the lab, create a snapshot named:

```text
Week1-Kali-Lab-Setup
```

A snapshot provides a recovery point before proceeding to future cybersecurity practicals.

**Status:** Update this section after creating and verifying the snapshot in VirtualBox.

## 6. Screenshots and Evidence

The following screenshots document the key stages of the lab setup.

### Screenshot 1: NAT Network Configuration

<img width="1917" height="1015" alt="01-nat-network" src="https://github.com/user-attachments/assets/7525cb82-5302-47c4-9759-7e559f2aa461" />


Shows the custom NAT Network and the configured IPv4 prefix `10.0.0.0/24`.

### Screenshot 2: Kali Linux VM Settings

<img width="1906" height="1021" alt="02-kali-vm-settings" src="https://github.com/user-attachments/assets/7562961e-226d-4ac8-b865-b0caca3210d6" />


Shows the actual Kali Linux virtual machine settings, including its network adapter configuration.

### Screenshot 3: Kali IP and Connectivity Verification

<img width="1920" height="1080" alt="03-kali-connectivity" src="https://github.com/user-attachments/assets/b12e95fa-108d-4e55-9156-30c44d57cc8e" />


Shows the Kali Linux IPv4 address, routing information, and network connectivity test results.

### Screenshot 4: Virtual Machine Snapshot

<img width="1917" height="1007" alt="04-kali-snapshot" src="https://github.com/user-attachments/assets/a3f9e586-5cc6-4e77-b6ed-6dbc69ba9c96" />


Shows the saved snapshot of the Kali Linux virtual machine.

## 7. Challenges and Troubleshooting

Issue 1: Kali Linux Had No IPv4 Address

Problem: Initially, the eth0 interface displayed only an IPv6 address.

Solution: Used NetworkManager to configure the static IPv4 address, gateway, and DNS servers. Reactivated the connection and verified the resulting configuration.

Result: Kali Linux successfully obtained the configured address 10.0.0.2/24, and gateway and external IP connectivity tests passed.

Issue 2: General → Advanced Was Not Available

Problem: The VirtualBox interface did not display the General → Advanced option mentioned in the assignment guide.

Action taken: Checked the settings available in my installed VirtualBox version. Clipboard, drag-and-drop, and shared-folder functionality must be verified separately before marking these requirements as complete.

## 8. Learning Outcomes

Through this assignment, I gained practical experience with:

- Virtual machine installation and configuration.
- IPv4 addressing and subnetting fundamentals.
- NAT Network configuration in VirtualBox.
- Static IP configuration using NetworkManager.
- Default gateways and DNS configuration.
- Linux network troubleshooting and connectivity verification.
- Virtual machine snapshots and recovery planning.

## 9. Conclusion

This assignment provided hands-on experience in preparing a virtual cybersecurity lab using Oracle VirtualBox and Kali Linux. Configuring the static IP address and testing network connectivity helped strengthen my understanding of Linux networking and basic troubleshooting.

The lab provides a foundation for future cybersecurity exercises, including network analysis, vulnerability assessment, and ethical hacking in authorized environments.

## 10. References

- Oracle VirtualBox: https://www.virtualbox.org/
- Kali Linux: https://www.kali.org/

---

**Author:** Iniya K

**Internship:** Networkwalks

**Assignment:** Week 1 – Project Module 1

**Repository Purpose:** Documentation of my cybersecurity lab setup and verification process.
