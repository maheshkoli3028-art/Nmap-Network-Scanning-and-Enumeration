# Nmap-Network-Scanning-and-Enumeration
A hands-on network reconnaissance and enumeration project using Nmap on Kali Linux with Metasploitable 2. Includes host discovery, port scanning, service and OS detection, NSE scripts, firewall analysis, and practical scan documentation.
# Nmap Network Scanning and Enumeration Lab

## Table of Contents

1. [Introduction](#1-introduction)
2. [Project Overview](#2-project-overview)
3. [Used Tools](#3-used-tools)
4. [Objectives](#4-objectives)
5. [Lab Environment](#5-lab-environment)
6. [Network Lab Setup](#6-network-lab-setup)
7. [Nmap Introduction](#7-nmap-introduction)
8. [Practical Implementation](#8-practical-implementation)
9. [Open Ports and Services](#9-open-ports-and-services)
10. [Network Topology](#10-network-topology)
11. [Host Details](#11-host-details)
12. [Nmap Output](#12-nmap-output)
13. [Scan Results Analysis](#13-scan-results-analysis)
14. [Learning Outcomes](#14-learning-outcomes)
15. [Conclusion](#15-conclusion)

---

## 1. Introduction

Nmap (Network Mapper) is an open-source tool used for network discovery and security auditing. It helps identify active hosts, open ports, running services, service versions, and operating system information.

This project demonstrates practical network reconnaissance and enumeration using Nmap in an isolated laboratory environment.

The main purpose of this project is to understand how Nmap can be used to discover network devices, identify exposed services, and analyze the potential attack surface of a target system.

---

## 2. Project Overview

This lab uses Kali Linux as the scanning platform and an intentionally vulnerable Metasploitable 2 virtual machine as the target.

The practical work covers host discovery, port scanning, service/version detection, operating system detection, NSE scripts, firewall/packet-filtering analysis, report generation, and Zenmap.

### Project Areas

| Area | Purpose |
|---|---|
| Host Discovery | Identify live hosts in the lab network |
| Port Scanning | Identify accessible TCP ports |
| Service Detection | Determine running services and their versions |
| OS Detection | Estimate the target operating system |
| NSE Scripts | Collect additional service and security information |
| Filtering Analysis | Observe packet-filtering behavior |
| Reporting | Save scan results for documentation |
| Zenmap | Perform Nmap scans through a graphical interface |

---

## 3. Used Tools

The following tools and technologies were used in this project:

| Tool | Purpose |
|---|---|
| Kali Linux | Scanning and security-testing platform |
| Nmap 7.99 | Network scanning and enumeration |
| Metasploitable 2 | Intentionally vulnerable target machine |
| VMware Workstation | Virtualization environment |
| Zenmap | Graphical interface for Nmap |

---

## 4. Objectives

- Understand the basic purpose and operation of Nmap.
- Discover active hosts in an authorized lab network.
- Identify open TCP ports on a target machine.
- Detect running services and their versions.
- Perform basic operating system detection.
- Use selected Nmap Scripting Engine (NSE) scripts.
- Analyze packet-filtering and firewall behavior.
- Save and document scan results.
- Understand how enumeration helps identify a system's exposed attack surface.

---

## 5. Lab Environment

The following laboratory environment was used to perform the practical exercises.

| Component | Example / Role |
|---|---|
| Kali Linux | Scanning and security-testing platform |
| Nmap | Network scanning and enumeration tool |
| Metasploitable 2 | Intentionally vulnerable target VM |
| VMware Workstation | Virtualization environment |
| Zenmap | Graphical interface for Nmap |
| Isolated Virtual Network | Controlled communication between lab VMs |

### Target Information

- **Target Machine:** Metasploitable 2
- **Target IP Address:** `192.168.153.---`
- **Scanning Machine:** Kali Linux
- **Network Environment:** Isolated Virtual Network

---

## 6. Network Lab Setup

An isolated virtual network was created containing two virtual machines:

1. Kali Linux – Used as the scanning machine.
2. Metasploitable 2 – Used as the target machine.

Both machines were configured to communicate through the same virtual network.

Before beginning the scanning process, network connectivity was verified.

### Lab Verification Commands

**Check the IP address of Kali Linux:**

```bash
ip addr
```

**Verify connectivity with Metasploitable 2:**

```bash
ping 192.168.153.---
```

### Screenshot

<!-- Add your network configuration and connectivity screenshots here -->

Network Configuration

<img width="1035" height="575" alt="image" src="https://github.com/user-attachments/assets/adae8e08-3cf2-4cda-9ac3-cf36c9a48489" />

Ping Connectivity

<img width="1035" height="340" alt="image" src="https://github.com/user-attachments/assets/b42ab915-f386-4b3b-9b3a-4ef702cd3aec" />

---

## 7. Nmap Introduction

### 7.1 What is Nmap?

Nmap (Network Mapper) is a network discovery and security auditing utility. It provides different scanning techniques for discovering hosts, ports, and services.

The scan results depend on the target system, network configuration, user privileges, and selected scan options.

### 7.2 Common Nmap Options Used in This Project

| Option | Meaning |
|---|---|
| `-sn` | Host discovery without a normal port scan |
| `-p-` | Scan all TCP ports |
| `-sV` | Detect service and version information |
| `-O` | Attempt operating system detection |
| `-sC` | Run the default NSE script set |
| `-sA` | ACK scan used for filtering/firewall analysis |
| `-oN` | Save output in normal text format |

---

## 8. Practical Implementation

This section explains the practical steps performed using Nmap.

### 8.1 Step 1 – Host Discovery

**Objective:** Check whether the target host is active.

**Command:**

```bash
nmap -sn 192.168.153.129
```

**Explanation:**

This command performs host discovery to determine whether the target machine is reachable on the network without performing a normal port scan.

**Screenshot:**

![Host Discovery](screenshots/01-host-discovery.png)

---

### 8.2 Step 2 – Full TCP Port Scan

**Objective:** Identify accessible TCP ports across the full TCP port range.

**Command:**

```bash
nmap -p- 192.168.153.129
```

**Explanation:**

The `-p-` option instructs Nmap to scan all 65,535 TCP ports on the target machine.

This helps identify open ports and potentially exposed services.

**Screenshot:**

![Full Port Scan](screenshots/02-full-port-scan.png)

---

### 8.3 Step 3 – Service and Version Detection

**Objective:** Identify services running on discovered ports and attempt to determine their versions.

**Command:**

```bash
nmap -sV 192.168.153.---
```

**Explanation:**

The `-sV` option enables service and version detection. It helps identify applications and their versions running on open ports.

**Screenshot:**

![Service Version Detection](screenshots/03-service-version-detection.png)

---

### 8.4 Step 4 – Operating System Detection

**Objective:** Attempt to identify the target operating system using Nmap OS detection.

**Command:**

```bash
sudo nmap -O 192.168.153.---
```

**Explanation:**

The `-O` option enables operating system detection. Nmap analyzes network responses and attempts to estimate the target operating system.

**Screenshot:**

![OS Detection](screenshots/04-os-detection.png)

---

### 8.5 Step 5 – NSE Default Scripts

**Objective:** Run Nmap's default NSE scripts to collect additional information.

**Command:**

```bash
nmap -sC 192.168.153.---
```

**Explanation:**

The `-sC` option runs Nmap's default script set. These scripts can collect additional information about available services and their configurations.

**Screenshot:**

![NSE Default Scripts](screenshots/05-nse-scan.png)

---

### 8.6 Step 6 – Firewall / Packet-Filtering Analysis

**Objective:** Use an ACK scan to examine how ports appear to be filtered by packet-filtering controls.

**Command:**

```bash
sudo nmap -sA 192.168.153.---
```

**Explanation:**

The `-sA` option performs an ACK scan. It helps determine whether ports appear to be filtered by firewall or packet-filtering rules.

**Note:** ACK scans generally classify ports as `unfiltered` or `filtered`. They do not determine whether a port is open or closed.

**Screenshot:**

![Firewall Analysis](screenshots/06-firewall-analysis.png)

---

### 8.7 Step 7 – Combined Scan and Report

**Objective:** Combine default scripts, service/version detection, and OS detection, and save the result to a file.

**Command:**

```bash
sudo nmap -sC -sV -O 192.168.153.--- -oN scan-report.txt
```

**Explanation:**

This command combines multiple Nmap scanning options:

- `-sC`: Runs default NSE scripts.
- `-sV`: Detects service versions.
- `-O`: Attempts operating system detection.
- `-oN`: Saves the output in normal text format.

The scan results are saved in `scan-report.txt`.

**Screenshot:**

![Combined Scan](screenshots/07-combined-scan.png)

---

### 8.8 Step 8 – Save Full Port Scan

**Objective:** Save the full TCP port scan results in a text file.

**Command:**

```bash
sudo nmap -p- 192.168.153.--- -oN port-scan.txt
```

**Explanation:**

This command scans all TCP ports and saves the results in a file named `port-scan.txt`.

**Screenshot:**

![Port Scan Report](screenshots/08-port-scan-report.png)

---

### 8.9 Step 9 – Discover Hosts on the Lab Network

**Objective:** Identify active hosts in the authorized local lab subnet.

**Command:**

```bash
nmap -sn 192.168.153.---/24
```

**Explanation:**

This command performs host discovery across the `192.168.153.0/24` subnet and identifies active devices in the lab network.

**Screenshot:**

![Network Host Discovery](screenshots/09-network-host-discovery.png)

---

### 8.10 Step 10 – Zenmap

**Objective:** Use Zenmap to perform and review Nmap scans through a graphical interface.

**Command:**

```bash
zenmap
```

**Explanation:**

Zenmap is the graphical user interface for Nmap. It allows users to configure scans, execute commands, and review scan results through a visual interface.

**Screenshot:**

![Zenmap Interface](screenshots/10-zenmap.png)

---

## 9. Open Ports and Services

This section documents the open ports and services identified during the Nmap scanning process.

### Screenshot

![Open Ports and Services](screenshots/open-ports-services.png)

---

## 10. Network Topology

The laboratory consists of two virtual machines connected through an isolated virtual network.

### Network Diagram

```text
          Isolated Virtual Network
             192.168.153.0/24
                     |
          +----------+----------+
          |                     |
          |                     |
     Kali Linux           Metasploitable 2
   Scanning Machine         Target Machine
   IP: Kali IP             IP: 192.168.153.---
          |                     |
          +------ Nmap Scan ----+
```

### Screenshot

<!-- Add your VMware network topology screenshot here -->

![Network Topology](screenshots/network-topology.png)

---

## 11. Host Details

This section contains the basic information about the target machine identified during scanning.

| Field | Details |
|---|---|
| Target Name | Metasploitable 2 |
| Target IP Address | 192.168.153.--- |
| Operating System | Add detected OS |
| MAC Address | Add detected MAC address |
| Host Status | Up / Down |
| Virtualization Platform | VMware Workstation |

### Screenshot

![Host Details](screenshots/host-details.png)

---

## 12. Nmap Output

This section contains the output generated during the Nmap scanning process.

### 12.1 Host Discovery Output

<!-- Add host discovery output screenshot here -->

![Host Discovery Output](screenshots/host-discovery-output.png)

### 12.2 Port Scanning Output

<!-- Add port scanning output screenshot here -->

![Port Scanning Output](screenshots/port-scanning-output.png)

### 12.3 Service Detection Output

<!-- Add service detection output screenshot here -->

![Service Detection Output](screenshots/service-detection-output.png)

### 12.4 OS Detection Output

<!-- Add OS detection output screenshot here -->

![OS Detection Output](screenshots/os-detection-output.png)

### 12.5 NSE Script Output

<!-- Add NSE output screenshot here -->

![NSE Output](screenshots/nse-output.png)

### 12.6 Firewall Analysis Output

<!-- Add firewall analysis output screenshot here -->

![Firewall Analysis Output](screenshots/firewall-analysis-output.png)

---

## 13. Scan Results Analysis

The following table summarizes the observations and security relevance of each scan.

| Scan | Important Observation | Security Relevance |
|---|---|---|
| Host Discovery | Identifies whether the host is reachable and may reveal its MAC address | Shows whether a host is active |
| Port Scan | Identifies accessible TCP ports across the full TCP port range | Shows exposed ports |
| Service Detection | Identifies services running on discovered ports and attempts to determine their versions | Identifies potentially exposed services |
| OS Detection | Attempts to identify the target operating system | Provides OS-related information |
| NSE Scan | Runs default NSE scripts to collect additional information | Provides additional enumeration data |
| Filtering Analysis | Uses an ACK scan to examine packet-filtering behavior | Helps understand firewall filtering |

### Overall Observation

The Nmap scans successfully demonstrated how to identify live hosts, open ports, running services, operating system information, additional enumeration details, and packet-filtering behavior.

Overall, the scanning process helped determine the attack surface and potential security exposure of the target system.

---

## 14. Learning Outcomes

Through this project, I gained practical knowledge of network scanning and enumeration using Nmap.

The key learning outcomes include:

- Learned how Nmap is used for network discovery and security auditing.
- Performed host discovery in a controlled laboratory environment.
- Scanned TCP ports and documented open services.
- Used service/version detection and OS detection.
- Used default NSE scripts for additional enumeration.
- Analyzed basic packet-filtering behavior.
- Saved scan results into report files.
- Improved practical understanding of network attack-surface identification.

---

## 15. Conclusion

This project provided practical experience with network reconnaissance and enumeration using Nmap.

The laboratory demonstrated how host discovery, port scanning, service identification, operating system detection, NSE scripts, and filtering analysis can be combined to understand the exposed attack surface of a system.

Through this practical implementation, I improved my understanding of network scanning techniques and the importance of identifying exposed services during security assessments.

**Ethical Consideration:** All scanning activities were performed in an isolated laboratory environment. Nmap scanning should only be conducted against systems and networks for which the tester has explicit authorization.

---
**Project:** Nmap Network Scanning and Enumeration Lab

**Platform:** Kali Linux

**Tool:** Nmap 7.99

**Target:** Metasploitable 2

**Virtualization:** VMware Workstation
