# 01 — Lab Architecture

## 1. Purpose

This document defines the architecture of the Windows Server Active Directory & IT Support Lab.

The environment was designed to demonstrate centralized identity management, DNS, Group Policy, departmental access control, and Windows file-server administration in a controlled virtual lab.

---

## 2. Environment

| Component | Configuration |
|---|---|
| Server | Windows Server |
| Server Name | `DC01` |
| Domain | `corp.local` |
| Directory Service | Active Directory Domain Services |
| DNS | Windows DNS |
| Virtualization | Oracle VirtualBox |
| File Sharing | SMB |
| File Permissions | NTFS |

---

## 3. High-Level Architecture

```text
                         +----------------------+
                         |    Windows Server    |
                         |        DC01          |
                         |      corp.local      |
                         +----------+-----------+
                                    |
              +---------------------+---------------------+
              |                     |                     |
       Active Directory            DNS              Group Policy
              |
        +-----+------+
        |            |
       OUs      Security Groups
        |            |
   +----+----+----+----+
   |    |    |    |    |
  IT   HR Finance Sales Management
        |
        +------------------+
                           |
                      File Server
                           |
                  Departmental Shares
```

---

## 4. Identity & Access Flow

```text
User
  ↓
Active Directory
  ↓
Department OU
  ↓
Security Group
  ↓
Department Resource
  ↓
NTFS / SMB Permissions
```

This model separates identity management from resource permissions and provides a scalable administration structure.

---

## 5. Department Structure

```text
corp.local
├── IT
├── HR
├── Finance
├── Sales
└── Management
```

Departmental OUs provide logical organization and create a suitable structure for future Group Policy or delegated administration.

---

## 6. Security Group Model

```text
GG-IT-Users
GG-HR-Users
GG-Finance-Users
GG-Sales-Users
GG-Management-Users
```

Security groups are used as the primary permission-management layer rather than assigning file permissions individually to every user.

---

## 7. File Server Model

```text
C:\CompanyData
├── IT
├── HR
├── Finance
├── Sales
└── Management
```

Example SMB resource:

```text
\\DC01\IT
```

The file-server design separates departmental data and allows permissions to be applied according to organizational roles.

---

## 8. Administrative Services

DC01 provides the core services used in the lab:

- Active Directory Domain Services
- DNS
- User and group management
- Organizational Unit management
- Group Policy
- File sharing
- Access-control administration

---

## 9. Design Principles

The architecture demonstrates:

- Centralized identity management
- Group-based access control
- Least-privilege access
- Departmental separation
- Centralized security policies
- Scalable administration

---

## 10. Evidence

Implementation screenshots are maintained in the repository `Evidence` directory and are linked to their corresponding implementation steps in the main README.
