# Cybersecurity & Ethical Hacking Lab — Environment Setup

## 📌 Overview

This repository documents the setup and configuration of a hands-on **cybersecurity and ethical hacking lab environment** built as part of coursework and self-study.

The lab covers virtualization, Kali Linux configuration, network isolation, static IP addressing, and the foundation required for future reconnaissance, vulnerability assessment, and web security exercises.

The primary goal is to build and maintain an **isolated, authorized environment** for safely practicing offensive and defensive security techniques.

---

## 🎯 Lab Objectives

* Build an isolated cybersecurity practice environment using **Oracle VirtualBox**.
* Configure an attack virtual machine (**Kali Linux**) for security testing.
* Set up a custom **NAT Network** with static IP addressing.
* Understand IP addressing, default gateways, subnetting, and DNS in a virtualized lab environment.
* Enable clipboard, drag-and-drop, and file sharing between host and guest operating systems.
* Verify network connectivity and internet access from the attack VM.
* Implement VM snapshots for safe experimentation and quick state rollback.
* Document network topology, configurations, and findings for future reference.

---

## 🛠️ Lab Environment & Specifications

| Component        | Detail                                        |
| ---------------- | --------------------------------------------- |
| **Hypervisor**   | Oracle VirtualBox                             |
| **Host OS**      | Windows                                       |
| **Attack VM**    | Kali Linux                                    |
| **Network Type** | Custom NAT Network (`NATNETWORK`)             |
| **Subnet**       | `10.0.0.0/24`                                 |
| **Lab Purpose**  | Isolated Cybersecurity Practice & Testing Lab |

---

## 🌐 Network Configuration

### Network Topology

```text
                    Internet
                       │
                       ▼
              ┌─────────────────┐
              │  VirtualBox NAT │
              │     Network     │
              │  10.0.0.0/24    │
              └────────┬────────┘
                       │
                Gateway: 10.0.0.1
                       │
              ┌────────┴────────┐
              │                 │
              ▼                 ▼
       ┌─────────────┐   ┌─────────────┐
       │ Kali Linux  │   │ Future      │
       │ Attacker VM │   │ Target VM   │
       │ 10.0.0.2    │   │ 10.0.0.10   │
       └─────────────┘   └─────────────┘
```

### IP Addressing

| Machine / Component     | Role              | IP Address  | Gateway    | Subnet / Netmask        |
| ----------------------- | ----------------- | ----------- | ---------- | ----------------------- |
| **NAT Network Gateway** | Virtual Gateway   | `10.0.0.1`  | —          | `/24` (`255.255.255.0`) |
| **Kali Linux**          | Attacker Machine  | `10.0.0.2`  | `10.0.0.1` | `/24` (`255.255.255.0`) |
| **Future Target VM**    | Vulnerable Target | `10.0.0.10` | `10.0.0.1` | `/24` (`255.255.255.0`) |

> **Note:** The target VM is planned for a future phase of the lab and is not part of the current setup.

---

## 🧰 Planned Toolset

The following tools are planned for future cybersecurity exercises:

* **Nmap** — Network discovery and reconnaissance
* **Wireshark** — Network traffic analysis
* **Burp Suite** — Web application security testing
* **Metasploit Framework** — Security testing and exploitation labs
* **Gobuster** — Directory and resource enumeration
* **Netcat** — Network communication and troubleshooting
* **Python** — Scripting and security automation

---

# 🚀 Phase 1 — Lab Setup & Configuration Walkthrough

## Step 1: Install VirtualBox

Oracle VirtualBox was downloaded and installed as the virtualization platform for the cybersecurity lab.

VirtualBox provides the virtualization layer required to run Kali Linux and future target virtual machines in an isolated environment.

https://github.com/ShaharyarHussain533/ShaharyarHussain533-NETWORKWALKS-Shaharyar-B083-WK1-PM1-CYBERSECURITY-LAB-SETUP/blob/58df5f3b3f612bb5fbd43382a5dda21feef0e1f6/KALI%20DOWNLOAD.png




---

## Step 2: Configure Custom NAT Network

A custom NAT Network named **`NATNETWORK`** was created in VirtualBox.

### Network Configuration

| Setting          | Value         |
| ---------------- | ------------- |
| **Network Name** | `NATNETWORK`  |
| **Network CIDR** | `10.0.0.0/24` |
| **Gateway**      | `10.0.0.1`    |
| **DHCP**         | Enabled       |

The NAT Network allows the virtual machines to communicate with each other while providing controlled internet connectivity through VirtualBox.

---

## Step 3: Import Kali Linux VM

The official **Kali Linux VirtualBox image** was imported into VirtualBox and configured as the designated attacker machine for the lab.

Kali Linux provides the security-focused operating system and tools required for future penetration testing and security assessment exercises.

---

## Step 4: Configure VM Network Adapter

The Kali Linux VM's **Adapter 1** was configured to connect directly to the custom `NATNETWORK`.

### Network Adapter Configuration

| Setting             | Value        |
| ------------------- | ------------ |
| **Adapter**         | Adapter 1    |
| **Attached To**     | NAT Network  |
| **Network Name**    | `NATNETWORK` |
| **Cable Connected** | Enabled      |

This places the Kali VM inside the isolated `10.0.0.0/24` lab network.

---

## Step 5: Enable Clipboard, Drag & Drop, and Shared Folders

To improve workflow efficiency between the Windows host and Kali Linux guest, the following VirtualBox features were configured:

| Feature              | Configuration              |
| -------------------- | -------------------------- |
| **Shared Clipboard** | Bidirectional              |
| **Drag & Drop**      | Bidirectional              |
| **Shared Folder**    | Windows `Downloads` folder |
| **Access**           | Full Access                |
| **Auto-Mount**       | Enabled                    |

These features make it easier to transfer files and information between the host and the cybersecurity lab environment.

---

## Step 6: Configure Static IP on Kali Linux

The Kali Linux network interface was manually configured with a static IP address within the lab subnet.

### Static Network Configuration

| Setting        | Value                  |
| -------------- | ---------------------- |
| **Method**     | Manual                 |
| **IP Address** | `10.0.0.2`             |
| **Netmask**    | `24` (`255.255.255.0`) |
| **Gateway**    | `10.0.0.1`             |
| **DNS Server** | `8.8.8.8`              |

The static address ensures that the Kali VM can consistently be reached at `10.0.0.2` during future lab exercises.

---

## Step 7: Verify Network Configuration

The network configuration was verified from the Kali Linux terminal using standard Linux networking commands.

### Check Network Interfaces

```bash
ip a
```

This command was used to verify that the Kali Linux network interface was assigned the expected IP address.

### Check Routing

```bash
ip route
```

This verifies that the default gateway is configured correctly.

### Test Gateway Connectivity

```bash
ping -c 4 10.0.0.1
```

This tests connectivity between Kali Linux and the VirtualBox NAT Network gateway.

### Test Internet Connectivity

```bash
ping -c 4 8.8.8.8
```

This verifies external network connectivity.

### Test DNS Resolution

```bash
ping -c 4 google.com
```

This can be used to verify that DNS resolution is functioning correctly.

---

## 📸 Screenshots

Screenshots documenting the lab setup and configuration can be added below.

### VirtualBox NAT Network

*Add screenshot here.*

### Kali Linux Network Adapter

*Add screenshot here.*

### Kali Linux IP Configuration

*Add screenshot here.*

### Network Connectivity Test

*Add screenshot here.*

---

## 💾 VM Snapshots

VirtualBox snapshots will be used throughout the lab to preserve known-good configurations.

Snapshots allow the environment to be restored quickly after testing, configuration changes, or potentially destructive security exercises.

Recommended snapshot points include:

1. **Fresh Kali Installation**
2. **Network Configuration Complete**
3. **Tools Installed**
4. **Before Security Testing**
5. **Before Major Configuration Changes**

---

## 🔐 Security & Isolation Considerations

The lab is designed to provide a controlled environment for cybersecurity experimentation.

* Security testing should only be performed against systems for which explicit authorization has been provided.
* Vulnerable target machines should remain within the designated lab network.
* Snapshots should be taken before potentially destructive exercises.
* Network configurations should be reviewed before introducing additional virtual machines.
* No unauthorized systems should be targeted from the lab environment.



## 👤 Author

**Syed Shaharyar Hussain**

*Cybersecurity Enthusiast*





**Project Status:** 🟢 Phase 1 — Environment Setup Complete
