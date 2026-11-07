# NETWORKWALKS--ELENI-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP

<p align="center">
  <img src="https://img.shields.io/badge/Status-Completed-2ea44f?style=flat-square" alt="Project status: completed" />
  <img src="https://img.shields.io/badge/VirtualBox-7.2-183A61?style=flat-square&logo=virtualbox&logoColor=white" alt="VirtualBox 7.2" />
  <img src="https://img.shields.io/badge/Kali%20Linux-2026.2-557C94?style=flat-square&logo=kalilinux&logoColor=white" alt="Kali Linux 2026.2" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square" alt="Network 10.0.0.0/24" />
</p>

## Overview

This project documents the setup and verification of an isolated cybersecurity lab using Oracle VirtualBox and Kali Linux. The Kali VM is connected to a VirtualBox NAT Network, providing outbound connectivity and a shared private network for future lab machines.

A clean VM snapshot was created as a recovery point before future exercises.

> **Status:** Setup and baseline verification completed. Additional target machines and security exercises can be added in future projects.

## Lab architecture

The lab currently contains a Kali Linux VM. Future target machines can be attached to the same NAT Network for authorized testing.

## Configuration

| Component | Configuration |
| --- | --- |
| Host operating system | Windows 10 |
| Host memory | 8 GB |
| Processor | Intel Core i7 |
| Hypervisor | VirtualBox 7.2 |
| Security VM | Kali Linux 2026.2 |
| Kali VM memory | 2,048 MB |
| Virtual network | NAT Network (`NatNetwork`) |
| IPv4 network | `10.0.0.0/24` |
| Kali IPv4 address | `10.0.0.2/24` |
| Default gateway | `10.0.0.1` |
| DNS server | `8.8.8.8` |
| Planned address range for future VMs | `10.0.0.3–10.0.0.99` |

The NAT Network was configured with DHCP enabled and IPv6 disabled. Kali was assigned the documented address `10.0.0.2/24`.

## Setup completed

1. Installed 7-Zip to extract the Kali VM package.
2. Installed VirtualBox.
3. Created a NAT Network named `NatNetwork` with the prefix `10.0.0.0/24`, DHCP enabled, and IPv6 disabled.
4. Imported the Kali Linux VM, allocated 2,048 MB of memory, and connected its first adapter to `NatNetwork` using the Intel PRO/1000 MT Desktop adapter.
5. Configured the Kali network settings and a shared folder for transferring files between the host and VM.
6. Created the baseline snapshot **Clean Kali - Network Setup**.

## Verification

The lab was checked for local addressing, gateway access, Internet connectivity, DNS resolution, Nmap availability, and snapshot recovery.

| Check | Command or action | Expected result |
| --- | --- | --- |
| Confirm IP configuration | `ip a` | Kali shows `10.0.0.2/24` |
| Check gateway reachability | `ping 10.0.0.1` | Replies received |
| Check outbound connectivity | `ping 8.8.8.8` | Replies received |
| Check DNS resolution | `nslookup networkwalks.com` | Domain resolves |
| Confirm Nmap availability | `nmap --version` | Version information displayed |
| Check snapshot recovery | Restore the baseline snapshot, then run `ip a` | Baseline configuration is restored |

Configured network values:

```text
IPv4 address: 10.0.0.2/24
Gateway:      10.0.0.1
DNS:          8.8.8.8
```

## Troubleshooting notes

### Internet access after setting an address

Connectivity may depend on the Kali and NetworkManager configuration. During setup, this command was used as a workaround:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

Connection names vary. Identify the active connection on your system before applying a command that names a specific connection.

### Virtualization support disabled

The VM initially could not start because hardware virtualization was disabled in firmware. Enabling Intel VT-x in BIOS/UEFI and restarting the computer resolved the issue.

## What I learned

- A VirtualBox NAT Network lets attached VMs communicate with one another while providing network address translation for outbound connectivity.
- Virtual network adapter settings determine how a VM communicates with other virtual machines and external networks.
- IP addresses, subnet masks, gateways, and DNS settings each affect network communication and should be verified.
- A clean snapshot provides a known-good restore point before experimental work.
- Recording configuration, verification steps, and troubleshooting makes a lab easier to reproduce and maintain.

## Responsible use

This lab is for education and authorized security testing. Only test systems you own or have explicit permission to assess.

## Tools and resources

- [7-Zip](https://www.7-zip.org/download.html)
- [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Kali Linux](https://www.kali.org/get-kali/)

## Author

**Eleni Yigrem**  

## Project details

- **Program:** Cybersecurity at Networkwalks
- **Week:** 01
- **Project:** Cybersecurity & Pentesting Lab Setup

