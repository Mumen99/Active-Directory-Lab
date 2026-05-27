# Active Directory Help Desk Lab

## Overview

This repository documents my Active Directory Help Desk Lab, a Windows Server home lab built to practice common IT support, systems administration, and help desk troubleshooting tasks.

The lab is designed around a small business-style Active Directory environment using Windows Server, Windows client machines, organizational units, users, groups, Group Policy Objects, file sharing, NTFS permissions, and help desk-style troubleshooting scenarios.

The goal of this project is to build practical experience that applies directly to help desk, IT support, desktop support, junior system administrator, and cybersecurity support roles.

---

## Lab Environment

| Component | Details |
|---|---|
| Hypervisor | VMware Workstation Pro 17 |
| Server OS | Windows Server 2022 |
| Client OS | Windows 10 Enterprise |
| Domain Controller | DC01 |
| Domain | MumenLab.local |
| Client Computer | COMPUTER01 |
| Main Tools | Active Directory Users and Computers, Group Policy Management Console, File Explorer, FSRM, CMD, RDP |
| Main Focus | Active Directory administration, Group Policy, shared folder access, NTFS permissions, and help desk troubleshooting |

---

## Repository Structure

```text
Active-Directory-Lab-GitHub/
│
├── README.md
│
├── Part1-AD-Setup-OUs-Groups-Users/
│   ├── README.md
│   └── screenshots/
│
├── Part2-Group-Policy-Objects/
│   ├── README.md
│   └── screenshots/
│
├── Part3-Client-VM-and-GPO-Testing/
│   ├── README.md
│   └── screenshots/
│
├── Part4-File-Sharing-and-FSRM/
│   ├── README.md
│   └── screenshots/
│
├── Part5-User-Rights-and-Fine-Grained-Password-Policies/
│   ├── README.md
│   └── screenshots/
│
├── Part6-NTFS-vs-Share-Permissions/
│   ├── README.md
│   └── screenshots/
│
└── Part7-Help-Desk-Ticketing-Lab/
    ├── README.md
    └── screenshots/
```

---

## Completed Lab Parts

| Part | Topic | Status |
|---|---|---|
| [Part 1](Part1-AD-Setup-OUs-Groups-Users/) | Active Directory setup, OUs, groups, and users | Complete |
| [Part 2](Part2-Group-Policy-Objects/) | Group Policy Objects | Complete |
| [Part 3](Part3-Client-VM-and-GPO-Testing/) | Client VM domain join and GPO testing | Complete |
| [Part 4](Part4-File-Sharing-and-FSRM/) | File sharing and FSRM | Complete |
| [Part 5](Part5-User-Rights-and-Fine-Grained-Password-Policies/) | User rights and fine-grained password policies | Complete |
| [Part 6](Part6-NTFS-vs-Share-Permissions/) | NTFS vs share permissions | Complete |
| Part 7 | Help desk ticketing lab with osTicket | Planned |

---

## Part 1: Active Directory Setup, OUs, Groups, and Users

In Part 1, I built the foundation of the Active Directory environment.

Main tasks completed:

- Created a Windows Server virtual machine
- Installed Windows Server 2022
- Installed the Active Directory Domain Services role
- Promoted the server to a domain controller
- Created the domain `MumenLab.local`
- Created organizational units
- Created security groups
- Created domain users
- Added users to the correct groups

This part demonstrates the basic setup required for a domain-based Windows environment.

---

## Part 2: Group Policy Objects

In Part 2, I configured Group Policy Objects to manage users and computers in the domain.

Main tasks completed:

- Created and managed GPOs using Group Policy Management Console
- Configured password policy settings
- Configured account lockout policy settings
- Configured mapped network drives
- Configured desktop wallpaper policy
- Restricted Control Panel access
- Disabled removable storage access

This part demonstrates how centralized policies can be used to enforce settings across a domain.

---

## Part 3: Client VM and GPO Testing

In Part 3, I created a Windows client VM and joined it to the domain.

Main tasks completed:

- Created a Windows client virtual machine
- Configured DNS to point to the domain controller
- Joined the client to `MumenLab.local`
- Logged in using a domain user account
- Verified the computer object in Active Directory
- Moved the computer object to the correct OU
- Linked GPOs to the correct OUs
- Used `gpupdate /force` to refresh policies
- Used `gpresult /r` to confirm applied policies
- Tested Control Panel restriction
- Tested account lockout and unlock behavior

This part demonstrates real endpoint administration and policy troubleshooting.

---

## Part 4: File Sharing and FSRM

In Part 4, I configured Windows file sharing and File Server Resource Manager.

Main tasks completed:

- Created a shared folder
- Configured share permissions
- Configured NTFS permissions
- Accessed a shared folder using a UNC path
- Mapped a network drive manually
- Created a mapped drive GPO
- Tested mapped drive deployment on the client
- Installed File Server Resource Manager
- Created a storage quota
- Created a file screen
- Verified FSRM configuration

This part demonstrates shared folder management, mapped drive deployment, and basic file server controls.

---

## Part 5: User Rights and Fine-Grained Password Policies

In Part 5, I configured user rights assignments and fine-grained password policies.

Main tasks completed:

- Created a user rights assignment GPO
- Configured deny log on locally settings
- Configured Remote Desktop logon settings
- Tested restricted logon behavior
- Opened Active Directory Administrative Center
- Created fine-grained password policies
- Applied password settings objects to specific users or groups

This part demonstrates access control, logon restriction, and password policy management.

---

## Part 6: NTFS vs Share Permissions

In Part 6, I focused on Windows file sharing permissions and realistic folder access scenarios.

Main tasks completed:

- Reviewed the difference between share permissions and NTFS permissions
- Configured read-only access for Marketing Interns
- Configured HR folder access for HR Staff only
- Configured vendor upload access using restrictive permissions
- Configured IT department access to a software folder
- Disabled inheritance on a sensitive subfolder
- Removed inherited permissions
- Applied explicit permissions to Senior IT

This part is directly relevant to help desk work because shared folder access issues are common in real IT support environments.

---

## Planned Part 7: Help Desk Ticketing Lab

The next major section will be a practical help desk ticketing lab using osTicket.

Planned tasks:

- Install and configure osTicket
- Create help desk agents
- Create departments
- Create help topics
- Create SLA plans
- Create realistic support tickets
- Document troubleshooting steps
- Resolve tickets using the Active Directory lab

Planned ticket scenarios:

- Password reset
- Account unlock
- New user onboarding
- User offboarding
- Add user to a security group
- User cannot access shared folder
- User cannot access mapped drive
- User has incorrect folder permissions
- User cannot log in due to account or GPO issue

This section will connect the technical Active Directory tasks to a realistic help desk workflow.

---

## Skills Demonstrated

| Skill Area | Examples |
|---|---|
| Active Directory Administration | Users, groups, OUs, domain join, computer objects |
| Group Policy | Password policy, account lockout, drive mapping, restrictions |
| Windows Server Administration | Domain controller setup, file sharing, FSRM |
| Windows Client Administration | Domain login, DNS configuration, policy testing |
| File Server Support | Share permissions, NTFS permissions, mapped drives |
| Access Troubleshooting | User rights, group membership, folder permissions |
| Help Desk Readiness | Account unlocks, access requests, shared folder issues |
| Documentation | Step-by-step README files with screenshots |

---

## Why This Lab Matters

This lab shows practical experience with tasks commonly handled by help desk and IT support teams.

Examples include:

- Creating and managing user accounts
- Assigning users to security groups
- Troubleshooting domain login issues
- Applying and testing Group Policy
- Managing shared folder access
- Understanding NTFS and share permissions
- Investigating why users can or cannot access resources
- Documenting technical work clearly

These skills are important for entry-level IT support, help desk, desktop support, junior system administrator, and cybersecurity support roles.

---

## Current Project Status

Completed:

- Part 1: Active Directory setup
- Part 2: Group Policy Objects
- Part 3: Client VM and GPO testing
- Part 4: File sharing and FSRM
- Part 5: User rights and fine-grained password policies
- Part 6: NTFS vs share permissions

Planned:

- Part 7: Help desk ticketing lab using osTicket
