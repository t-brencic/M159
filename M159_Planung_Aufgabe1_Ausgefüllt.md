# 🧩 Modul 159 – Active Directory & Cloud Setup

## 👤 Name: Tomas Brencic  

---

# 🧠 Aufgabe 1 – Planung, AD- & Cloud-Setup

## 🧠 Übersicht der Umgebung
Die erstellte Umgebung besteht aus zwei Windows Server 2022 Instanzen auf AWS EC2:

| Komponente | Rolle | Hostname | IP-Adresse | Subnetz | Sichtbarkeit |
|-------------|--------|-----------|-------------|-----------|----------------|
| **DC01** | Domain Controller (Active Directory) | `dc01.corp.local` | `10.0.12.229` | `M159-subnet-private1-us-east-1a` | Intern |
| **CLIENT01** | Windows Client (Server Core Variante) | `client01.corp.local` | `10.0.12.230` | `M159-subnet-public1-us-east-1a` | Öffentlich (RDP) |

🟢 **Ziel:** Der Client tritt der AD-Domain `corp.local` bei und kann mit dem Domain Controller kommunizieren.

---

## ☁️ AWS-Setup

### 1️⃣ VPC erstellen
- **CIDR:** `10.0.0.0/16`  
- **Subnets:**  
  - `10.0.12.0/20` (Private)  
  - `10.0.128.0/20` (Public)

### 2️⃣ Security Groups

#### 🧱 DC Security Group
| Port | Protokoll | Beschreibung |
|------|------------|--------------|
| 3389 | TCP | RDP Remote Access |
| 389 | TCP/UDP | LDAP |
| 445 | TCP | SMB |
| 88 | TCP/UDP | Kerberos |
| 53 | TCP/UDP | DNS |
| 135, 49152–65535 | TCP | RPC |
| ICMP | – | Ping |

#### 🧱 Client Security Group
| Port | Protokoll | Beschreibung |
|------|------------|--------------|
| 3389 | TCP | RDP |
| 88 | TCP | Kerberos |
| 445 | TCP | SMB |
| 53 | TCP/UDP | DNS |
| 135, 49152–65535 | TCP | RPC |
| ICMP | – | Ping |

---

## 💻 Windows-Grundkonfiguration

### 1️⃣ Hostname setzen
```powershell
Rename-Computer -NewName "DC01" -Restart
Rename-Computer -NewName "CLIENT01" -Restart

### 2️⃣ Netzwerkadapter konfigurieren
  -  IPv6 deaktivieren
  -  Statische IPv4-Adresse vergeben
  -  DNS-Server beim Client → DC01 (10.0.12.229)
