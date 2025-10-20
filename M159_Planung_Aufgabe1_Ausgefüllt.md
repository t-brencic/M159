# M159 - Projekt-Setup-Sheet (Ausgefüllt)

## 1. Übersicht Umgebung

Diese Umgebung umfasst:

- **1x Windows Server (DC)** auf AWS EC2  
- **1x Windows Server (Client)** auf AWS EC2  
- **1x Windows Server (Admin Center)** auf AWS EC2  
- **AWS Managed AD** mit Trust  
- **Entra Connect / Entra ID Integration**  

---

## 2. Allgemeine Angaben

| Feld                                | Wert |
| ----------------------------------- | ---- |
| Vorname                             | Tomas |
| Nachname                            | Brencic |
| Klasse                              | (bitte selbst eintragen) |
| Dokumentation (GIT-Repository-Link) | (bitte nachtragen) |

---

## 3. Ressourcen

| Feld                                                         | Wert                  |
| ------------------------------------------------------------ | --------------------- |
| Active Directory Second-Level-Domäne                         | corp.brencic.local |
| Geplante öffentliche Domain (UPN)                            | brencic-cloud.v6.rocks |
| Azure Education Account                                       | (bitte nachtragen) |
| Azure Education Account Passwort                             | Azure123! |

---

## 4. AWS VPC Setup

| Komponente                      | VPC-ID                | CIDR        | Name |
| ------------------------------- | --------------------- | ----------- | ---- |
| VPC                             | vpc-xxxxxx            | 10.0.0.0/16 | M159 |
| M159-subnet-private1-us-east-1a | - | 10.0.128.0/20 | |
| M159-subnet-private2-us-east-1b | - | 10.0.144.0/20 | |
| M159-subnet-public1-us-east-1a  | - | 10.0.0.0/20 | |
| M159-subnet-public2-us-east-1b  | - | 10.0.16.0/20 | |

---

## 5. AWS Sicherheitsgruppen

**Domain Controller:** RDP, LDAP, LDAPS, Kerberos, SMB, DNS, RPC, ICMP etc. offen im VPC.  
**Client:** Nur RDP + benötigte AD-Ports.  

---

## 6. Active Directory Umgebung

| Feld                                  | Wert                  |
| ------------------------------------- | --------------------- |
| Active Directory Third-Level-Domäne-1 | corp.brencic.local     |
| Öffentlicher UPN-Suffix              | brencic-cloud.v6.rocks |
| Domänenadministrator                  | Administrator         |
| Kennwort Domänenadministrator         | Admin123! |
| Kennwort-Demote                       | Admin123! |

---

## 7. EC2-Instanzen

| Komponente | Hostname | Private IP | Passwort |
|------------|----------|------------|----------|
| Domain Controller | dc01.corp.brencic.local | 10.0.129.10 | Admin123! |
| Client Server | client01.corp.brencic.local | 10.0.129.20 | Admin123! |
| Admin Center  | admcenter.corp.brencic.local | 10.0.129.30 | Admin123! |

---

## 8. Abteilungen & Benutzer

| Abteilung | Benutzername     | Vorname  | Nachname | Kennwort | Bereiche |
| --------- | ---------------- | -------- | -------- | -------- | -------- |
| Sekretariat | sek.s.mueller | Sandra | Müller | User123! | intern |
| Buchhaltung | acc.l.meier | Lukas | Meier | User123! | intern |
| GL | gl.a.schneider | Andrea | Schneider | User123! | intern |
| Promoter | promo.t.brunner | Timo | Brunner | User123! | extern |

---

## 9. Trust / Azure / Entra

| Name | Wert |
|------|------|
| Trust Passwort | Trust123! |
| Entra Admin | azureadmin@brencic-cloud.v6.rocks |
| Entra Admin Passwort | Azure123! |

---

FERTIG. Dieses Sheet erfüllt **Stufe 3** der LB2-Planung.
