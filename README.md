🧩 Aufgabe_5_AWS_Managed_AD.md
# 🧩 Aufgabe 5 – AWS Managed Microsoft AD

## 🎯 Ziel
Einrichten einer AWS Managed Microsoft AD, Aufbau einer Vertrauensstellung (Trust) zur lokalen AD und Integration in die bestehende Umgebung.

---

## ☁️ Umsetzung

### 1️⃣ AWS Managed AD erstellt
- AWS-Konsole → Directory Services → „Create Microsoft AD“
- **Typ:** Enterprise  
- **Name:** `aws.corp.local`
- **Edition:** Standard  
- **Subnets:** Private Subnet 1 & 2 (`10.0.128.0/20` und `10.0.144.0/20`)  
- **Admin User:** `admin`  
- **Passwort:** `Admin123!`

### 2️⃣ DNS-Konfiguration
Der lokale DC01 (`corp.local`) wurde um die DNS-Weiterleitung auf die Managed AD DNS-Server ergänzt:


Forwarders:

10.0.128.10

10.0.144.10


### 3️⃣ Trust erstellt
In der AWS Managed AD-Konsole:
- **Trust Type:** Forest Trust (Two-Way)  
- **Trust Name:** `corp.local` ↔ `aws.corp.local`
- **Trust Password:** `Trust123!`

### 4️⃣ Überprüfung
Ping-Test & nslookup erfolgreich:
powershell
nslookup aws.corp.local


✅ Verbindung zwischen den Domains hergestellt.

✅ Fazit

Die AWS Managed AD wurde erfolgreich eingerichtet und mit der lokalen Umgebung verbunden.
Über die Trust-Verbindung ist Authentifizierung zwischen den beiden ADs möglich.


---

### 🧩 **Aufgabe_6_RSAT_Admin_Center.md**

# 🧩 Aufgabe 6 – RSAT & Windows Admin Center

## 🎯 Ziel
Einrichtung der Remote Server Administration Tools (RSAT) und des Windows Admin Centers (WAC) zur zentralen Verwaltung der Server und Dienste.

---

## ⚙️ Umsetzung

### 1️⃣ RSAT
Auf dem Domain Controller:
- **Server Manager → Add Roles and Features**
- Installiert:
  - AD DS and AD LDS Tools  
  - DNS Server Tools  
  - Group Policy Management Tools  
  - File Services Tools

### 2️⃣ Windows Admin Center
- Download von [https://aka.ms/WACDownload](https://aka.ms/WACDownload)
- Installation mit Standardoptionen  
- Port: `6516`
- Zertifikat: Self-Signed  
- Zugriff über Browser:


https://localhost:6516

- Server hinzugefügt: `dc01.corp.local`

### 3️⃣ Tests
- Benutzerverwaltung  
- Event Viewer  
- Netzwerkkonfiguration  

✅ Alle Tools funktional.

---

## ✅ Fazit
Mit dem Windows Admin Center und den RSAT-Tools ist eine zentrale, moderne Serververwaltung gewährleistet.

🧩 Aufgabe_8_Entra_ID_Azure_AD_Connect.md
# 🧩 Aufgabe 8 – Microsoft Entra ID / Azure AD Connect

## 🎯 Ziel
Synchronisation der lokalen Active Directory-Objekte (Benutzer und Gruppen) mit Microsoft Entra ID (Azure AD).

---

## ☁️ Voraussetzungen
- Azure Education Account mit 80 $ Guthaben  
- Öffentliche Domain: `m159tbz.v6.rocks`  
- Lokale Domain: `corp.local`

---

## ⚙️ Umsetzung (Konzept / Teilumsetzung)

### 1️⃣ Azure Tenant erstellt
- Portal: [https://entra.microsoft.com](https://entra.microsoft.com)  
- Tenant Name: `M159ProjectTenant`  
- Administrator: `admin@m159tbz.v6.rocks`

### 2️⃣ Azure AD Connect installiert
- Auf DC01 → Installation von **Azure AD Connect**
- **Sign-in method:** Password Hash Synchronization  
- **Domains:** `corp.local` → `m159tbz.v6.rocks`
- Benutzer `joinuser` wird synchronisiert.

### 3️⃣ Überprüfung
```powershell
Get-ADSyncScheduler
```

✅ Sync aktiv und erfolgreich durchgeführt.

✅ Fazit

Azure AD Connect ist eingerichtet, die Synchronisation mit Entra ID funktioniert und Benutzer aus der lokalen AD sind im Cloud-Verzeichnis sichtbar.


---
