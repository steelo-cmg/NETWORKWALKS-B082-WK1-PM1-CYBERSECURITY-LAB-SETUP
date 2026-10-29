
# 🖥️ Cybersecurity & Pentesting Lab Setup

**NetworkWalks Cybersecurity Program — Week 1 Project Submission**  
**Author:** Alakhe Ngalo (steelo-cmg)  
**Environment Status:** Fully Operational 🚀

---

## 📌 Project Overview
This project focuses on building a highly controlled, isolated, and resilient virtual cybersecurity laboratory using Oracle VirtualBox and Kali Linux. By utilizing a private virtual network infrastructure, the lab provides a safe playground to run security diagnostics, vulnerability discovery operations, and network reconnaissance tools without exposing the physical host computer or primary home production networks to malicious traffic or instability.

The structural foundation built during this lab establishes a dedicated virtual switch segment, allowing custom targets (such as Windows machines or Metasploitable nodes) to be integrated in future weeks for secure exploitation pipelines.

---

## ⚙️ Lab Configuration Schema
The table below details the real-world engineering metrics verified across the active hypervisor layers and guest operating system instances:

| Component | Configuration Metrics | Ground Truth Verification Source |
| :--- | :--- | :--- |
| **Host OS** | Windows 10 | Hypervisor Environment |
| **Hypervisor** | Oracle VirtualBox | Platform Engine |
| **Security Guest OS**| Kali Linux 2026.1 | `uname -a` Kernel Verification |
| **Kali Allocations** | 2048 MB RAM / 2 vCPUs | Hardware Allocation Profiler |
| **Interface Name** | `eth0` | Linux Network Device Descriptor |
| **Static IP Address**| `10.0.0.2/24` | Verified Active on Local Broadcast Segment |
| **Default Gateway** | `10.0.0.1` | Private NAT Network Virtual Router |
| **DNS Nameserver** | `8.8.8.8` | Google Public DNS Routing Profile |
| **Network Profile** | `NatNetwork` | Multi-VM Isolated Broadcast Segment |

---

# 🪜 Lab Setup Procedure

### Step 1: Environment Preparation (7-Zip & Hypervisor Deployment)
Deployed 7-Zip utility engine to extract the compressed Native VirtualBox Kali Linux build package. Installed the main VirtualBox platform package, followed by the explicit initialization of the Extension Pack to unlock advanced hypervisor device control mapping.

### Step 2: Global NAT Network Provisioning
Constructed an isolated network profile within the global VirtualBox preferences (**File → Tools → Network → NAT Networks**) to build a virtual switch segment matching the infrastructure blueprint:
*   **Network Name:** `NatNetwork`
*   **Network CIDR:** `10.0.0.0/24`
*   **DHCP Server:** Enabled

### Step 3: Appliance Extraction and Local Initialization
Imported the official native Kali Linux image directly into the VirtualBox inventory. Modified the adapter profile properties, ensuring the primary virtual interface card was explicitly attached to the freshly minted `NatNetwork` profile block.

---

# 🔎 Lab Verification Telemetry

With the low-level infrastructure paths constructed, network diagnostics were executed inside the Kali guest instance terminal to verify baseline operational integrity:

| Verification Test | Terminal Command | Ground Truth Result |
| :--- | :--- | :--- |
| **Check Local Link IP** | `ip a` | `inet 10.0.0.2/24` bound cleanly to device `eth0` |
| **Test Gateway Connectivity**| `ping -c 4 10.0.0.1` | **4 packets transmitted, 4 received, 0% packet loss** (Sub-ms latency) |
| **Test Domain Resolution** | `ping -c 4 google.com`| Fully operational external loop return rate via DNS parsing |

```bash
# Executing low-level interface verification probe
kali@kali:~\$ ip a
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP
    link/ether 08:00:27:8a:35:d2 brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.2/24 scope global eth0

# Checking virtual router pathway integrity
kali@kali:~\$ ping -c 4 10.0.0.1
PING 10.0.0.1 (10.0.0.1) 56(84) bytes of data.
64 bytes from 10.0.0.1: icmp_seq=1 ttl=64 time=0.388 ms
64 bytes from 10.0.0.1: icmp_seq=2 ttl=64 time=0.596 ms
64 bytes from 10.0.0.1: icmp_seq=3 ttl=64 time=0.557 ms
64 bytes from 10.0.0.1: icmp_seq=4 ttl=64 time=0.766 ms

--- 10.0.0.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3080ms
rtt min/avg/max/mdev = 0.388/0.576/0.766/0.134 ms
```

---

# 🐞 Problems Encountered & Solutions (Real Engineering Debugging)

### Problem 1: High-Level Connection Manager DB Corruption (GUI Profile Lock)
*   **Symptom:** Executing standard high-level `nmcli` connection cycling scripts threw persistent timeouts, resulting in the interface dropping completely and rendering the `inet` IPv4 block missing under device `eth0`.
*   **Root Cause:** The desktop environment's graphical "Wired connection 1" mapping cache became desynchronized from the virtualization runtime environment.
*   **Remediation Action:** Dropped down to low-level kernel commands using the `ip` tool suite to inject static parameters straight into the active hardware space, bypassing the broken GUI database layer:
    ```bash
    sudo ip addr flush dev eth0
    sudo ip link set eth0 up
    sudo ip addr add 10.0.0.2/24 dev eth0
    sudo ip route add default via 10.0.0.1 dev eth0
    ```

### Problem 2: Hypervisor Attachment Layer Mismatch & Virtual Cable Disconnect
*   **Symptom:** Gateway diagnostic pings consistently failed with an explicit `Destination Host Unreachable` alarm string.
*   **Root Cause:** Auditing the VirtualBox VM hardware runtime panel revealed the instance was erroneously set to `Bridged Adapter` instead of `NAT Network`. Additionally, the `Virtual Cable Connected` hardware checkbox was physically unchecked (unplugged).
*   **Remediation Action:** Altered the hardware attachment properties back to the private `NatNetwork` switch profile, checked the cable linkage box to complete the physical layer circuit, and forced a configuration refresh.

### Problem 3: Out of Sync Runtime State inside VirtualBox Global Preferences
*   **Symptom:** Linux NetworkManager repeatedly threw an error indicating that the static IP configuration could not be reserved.
*   **Root Cause:** The hypervisor's user interface layer fell out of synchronization with the background host service register (`VBoxSVC.exe`), causing the virtual router engine to drop address mapping allocations.
*   **Remediation Action:** Clicked **Apply** within the global tool preferences panel, gracefully terminated the VM, used the Windows Host Task Manager to kill the background `VBoxSVC.exe` process task, and initialized a clean boot sequence to force-reload the operational configuration.

---

# 💡 What I Learned

*   **Low-Level vs High-Level Linux Networking:** Discovered how to safely bypass broken high-level NetworkManager daemons (`nmcli`) by interacting directly with the Linux kernel network engine using manual `ip link` and `ip route` hooks.
*   **Hypervisor Layer Dependency:** Mastered the structural dependencies between guest OS configurations and the underlying hypervisor. A guest configuration is only as resilient as its physical layer parameters (such as the Virtual Cable Connection status and proper NAT Network switch profiling).
*   **The Power of Methodical Isolation:** Solidified a strong troubleshooting methodology—moving sequentially up the OSI model (Hardware Cable Status → Virtual Switch Assignment → Kernel Device IP Bindings → Subnet Gateway Routing Paths) rather than guessing solutions blindly.

---

# 🔐 Security & Ethical Use
This infrastructure is constructed strictly for defensive educational research and ethical skill development inside a sandboxed virtual laboratory environment. All security scanning, configuration audits, and verification exercises are executed solely on hardware and network blocks completely owned by the author.

---

# 🔗 Tools & Reference Repositories
*   **7-Zip Extraction Engine:** https://7-zip.org
*   **Oracle VirtualBox Hypervisor Engine:** https://virtualbox.org
*   **Official Kali Linux Operating Systems:** https://kali.org
*   **Submission Root Directory:** [://github.com](https://://github.com)

---

# 👤 Author Profile

**Alakhe Ngalo (steelo-cmg)**  
Cybersecurity Specialist — Batch B082  
NetworkWalks Academy