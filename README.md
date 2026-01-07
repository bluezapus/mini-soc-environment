# MINI SOC ENVIRONMENT (ELK + SYSMON)

Status: **In Progress (Detection Engineering Phase)**

roadmap:  [Roadmap Progres](roadmap)

---
Refer to the documentation below for detailed explanations:

- [Architecture Overview ](docs/alur-log)
- [Log & Telemetry Flow](docs/arsitektur)
- [Portfolio Scope](docs/scope-portofolio)
## 1️ UBUNTU 22.04 LTS — **SOC CORE / GATEWAY**

Rule
- SOC Core √
- Router (L3 Gateway) √
- Firewall
- VPN Termination 
- Log Ingestion & Analysis √

**Network:**
- `eth0` → Management / VPN  
    IP: `10.10.10.10/24`
- `eth1` → Internal Monitoring  
    IP: `192.168.100.1/24`
- **IP forwarding: ENABLED**
    
- **Firewall FORWARD: DROP by default**
    
**Installed Software:**
- Elasticsearch **9.2.3** (TLS ON) √
- Kibana **9.2.3** (TLS ON) √
- Logstash (TLS ON) √
- WireGuard (VPN)
- ufw firewall

**Security Requirements:**
- HTTPS only (no HTTP) √
- Elasticsearch bind **internal only** √
- Kibana exposed **VPN only**
- Static IP (NO DHCP) √
---
## 2️ WINDOWS 10 — **VICTIM / ENDPOINT**
**Peran:**
- Endpoint victim √
- Telemetry source √
- Detection target √

**Network:**
- Single NIC
- IP: `192.168.100.10/24`
- Gateway: `192.168.100.1`
- **NO VPN**
- **NO second NIC**
- Static IP

**Installed Software:**
- Sysmon √
- Winlogbeat / Elastic Agent √
- (Optional) Attack simulation tools

**Log Destination:**
- Logstash → `192.168.100.1:5044` (TLS) √

---
## 3️ ARMBIAN (SBC) — **INTERNAL TICKETING**
**Peran:**
- SOC Ticketing System
- Incident tracking
- Internal service    

**Network:**
- Single NIC
- IP: `192.168.100.20/24`
- Gateway: `192.168.100.1`
- **Internal only**
- Static IP

**Installed Software:**
- Nginx
- PHP
- MariaDB
- osTicket

**Security:**
- NOT internet-facing
- NOT VPN-exposed
- Access only via Ubuntu SOC

---
## 4️ KALI LINUX — **ATTACKER / RED TEAM**
**Peran:**
- External attacker
- Red Team simulation
- SOC validation

**Network:**
- NO LAN access
- VPN only (WireGuard)
- VPN IP: `10.10.10.50/24`

**Access Allowed:**
- Kibana → `https://10.10.10.10:5601`
- Mythic (if used)
- SSH to Ubuntu SOC

**Security:**
- Cannot directly reach `192.168.100.0/24`
- Must go through SOC gateway
---
## 5️ SWITCH — **LAYER 2 ONLY**
**Peran:**
- Port expansion for internal network

**Connected Devices:**
- Ubuntu eth1
- Windows Victim
- Armbian

**Rules:**
- NO routing
- NO DHCP
- NO firewall
- NO management logic

## SECURITY PRINCIPLES APPLIED
- Network Segmentation
- Zero Trust (VPN-only access)
- TLS everywhere
- Static IP for deterministic logging
- Least Exposure

---
## EXPLICITLY NOT USED

- DHCP Server
- Hub
- Additional Router
- Dual-NIC on Victim
- Plain HTTP
- Direct attacker access to internal LAN
