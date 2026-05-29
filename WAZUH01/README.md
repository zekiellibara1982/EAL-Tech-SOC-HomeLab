# WAZUH01 — Wazuh SIEM Server

**Wazuh · Ubuntu Server 22.04 · VMware · SIEM · Log Monitoring · Threat Detection**

Hi,

In this hands-on project I deploy and configure Wazuh — a free and open source SIEM (Security Information and Event Management) platform — on an Ubuntu Server virtual machine running on my Intel NUC.

Wazuh is the eyes of my SOC home lab. It collects logs from every machine in the network, detects suspicious activity, and sends alerts that I investigate as a SOC Analyst. This is exactly the kind of tool a SOC Analyst uses on their first day at a Canadian company.

This is **Phase 1** of my full EAL Tech SOC Home Lab.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Environment](#environment)
3. [How Wazuh Works](#how-wazuh-works)
4. [What Was Built](#what-was-built)
5. [Phase 1 — Ubuntu Server Setup](#phase-1--ubuntu-server-setup)
6. [Phase 2 — Wazuh Installation](#phase-2--wazuh-installation)
7. [Phase 3 — Dashboard Configuration](#phase-3--dashboard-configuration)
8. [Errors and Troubleshooting](#errors-and-troubleshooting)
9. [Key Concepts Demonstrated](#key-concepts-demonstrated)
10. [Tools and Technologies](#tools-and-technologies)
11. [Project Status](#project-status)

---

## Project Overview

The goal of this project is to deploy a working SIEM server that monitors all security events across my home lab network.

In a real company — when an employee logs in at 3am from a strange location, or when someone tries 10 wrong passwords in a row — the SIEM catches it and sends an alert to the SOC Analyst on duty. The SOC Analyst then investigates and decides if it is a real threat.

I built exactly that — a Wazuh SIEM server running on Ubuntu, hosted on my Intel NUC (EAL-002), connected to the same network as my Active Directory environment, monitoring all Windows login events, file changes, and suspicious activity in real time.

---

## Environment

### Physical Hardware

| Asset ID | Device | RAM | Role |
|---|---|---|---|
| EAL-002 | Intel NUC8i5BEH | 16GB | SOC Monitoring Host — runs Wazuh |
| EAL-005 | HP Aruba Managed Switch | — | Network Core — VLAN 30 for security tools |

### Virtual Machine

| VM ID | VM Name | OS | RAM | Storage | IP Address | VLAN |
|---|---|---|---|---|---|---|
| VM-005 | WAZUH01 | Ubuntu Server 22.04 | 8GB | 100GB | 192.168.30.10 | VLAN 30 |

### Network Design

| VLAN | Name | Purpose |
|---|---|---|
| VLAN 30 | Security | SOC monitoring tools — monitors all other VLANs |

---

## How Wazuh Works

Think of Wazuh like a **CCTV system for your network.**

Every camera (agent) sends footage (logs) back to the main recording room (Wazuh server). If something suspicious happens — the system sends an alert to the security guard (SOC Analyst) immediately.

### The Monitoring Flow

```
1. Windows event happens on CLIENT01
   (failed login, file change, new process)
         |
2. Wazuh Agent on CLIENT01 captures the event
         |
3. Agent sends the log to WAZUH01 at 192.168.30.10
         |
4. Wazuh analyses the log against detection rules
         |
5. If suspicious -- ALERT created in Wazuh dashboard
         |
6. SOC Analyst (me) reviews the alert and investigates
```

### Key Terms

| Term | Simple Meaning |
|---|---|
| SIEM | Collects and analyses logs from all machines |
| Wazuh Agent | Small program installed on each VM that sends logs |
| Log | A record of everything that happens on a computer |
| Alert | A notification that something suspicious was detected |
| Rule | A pattern Wazuh looks for — e.g. 5 failed logins in 1 minute |
| Dashboard | The web interface where SOC Analysts review alerts |

---

## What Was Built

- [x] Created WAZUH01 VM on Intel NUC (EAL-002)
- [x] Installed Ubuntu Server 22.04
- [x] Installed Wazuh Manager
- [x] Installed Wazuh Dashboard
- [x] Accessed Wazuh web dashboard
- [x] Documented full build log with screenshots
- [ ] Install Wazuh Agent on DC01
- [ ] Install Wazuh Agent on CLIENT01, CLIENT02, CLIENT03
- [ ] Install Sysmon on all Windows VMs
- [ ] Connect all agents to WAZUH01
- [ ] Test first alert from Active Directory

---

## Phase 1 — Ubuntu Server Setup

| Step | Task | Status |
|---|---|---|
| 1 | Download Ubuntu Server 22.04 ISO | ✅ Done |
| 2 | Create WAZUH01 VM in VMware | ✅ Done |
| 3 | Install Ubuntu Server 22.04 | ✅ Done |
| 4 | Set static IP 192.168.30.10 | ✅ Done |
| 5 | Update Ubuntu packages | ✅ Done |

---

## Phase 2 — Wazuh Installation

| Step | Task | Status |
|---|---|---|
| 1 | Add Wazuh repository | ✅ Done |
| 2 | Install Wazuh Manager | ✅ Done |
| 3 | Install Wazuh Indexer | ✅ Done |
| 4 | Install Wazuh Dashboard | ✅ Done |
| 5 | Start all Wazuh services | ✅ Done |

---

## Phase 3 — Dashboard Configuration

| Step | Task | Status |
|---|---|---|
| 1 | Access Wazuh dashboard via browser | ✅ Done |
| 2 | Login with admin credentials | ✅ Done |
| 3 | Connect first agent | ⏳ To Do — waiting for AD01 |
| 4 | Create first detection rule | ⏳ To Do |
| 5 | Investigate first real alert | ⏳ To Do |

---

## Errors and Troubleshooting

> 📄 Full details in [WAZUH01 Build Log](./WAZUH01_Build_Log_May23_2026.pdf)

| Date | Error | Cause | Fix |
|---|---|---|---|
| May 2026 | See full build log PDF for all errors and fixes | — | — |

---

## Key Concepts Demonstrated

- **SIEM deployment** — installing and configuring Wazuh on Ubuntu Server
- **Log collection** — understanding how agents send events to the SIEM
- **Alert analysis** — reading and investigating security alerts in the dashboard
- **VLAN isolation** — keeping security tools on a separate network segment
- **Linux server administration** — installing packages, managing services
- **SOC workflow** — detect alert → investigate → document → respond

---

## Tools and Technologies

| Tool | Version | Purpose |
|---|---|---|
| VMware Workstation | 16 Pro | Runs WAZUH01 VM on Intel NUC |
| Ubuntu Server | 22.04 LTS | Operating system for Wazuh |
| Wazuh Manager | 4.7.5 | SIEM engine — processes and analyses logs |
| Wazuh Indexer | 4.7.5 | Stores all log data |
| Wazuh Dashboard | 4.7.5 | Web interface for viewing alerts |
| Sysmon | Latest | Deep Windows event logging on client VMs |

---

## Project Status

| Component | Status |
|---|---|
| WAZUH01 VM — Ubuntu Server | ✅ Complete |
| Wazuh Installation | ✅ Complete |
| Wazuh Dashboard | ✅ Complete |
| Full Build Log | ✅ Complete |
| Wazuh Agents on Windows VMs | ⏳ Waiting for AD01 |
| First Real Alert | ⏳ To Do |

---

*Part of the EAL Tech SOC Home Lab · EAL Tech IT Consulting · Ezekiel A. Libara · Toronto, Canada · 2026*
