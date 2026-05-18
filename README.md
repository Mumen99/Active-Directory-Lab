# Active Directory Help Desk Lab

## Overview

This repository documents my Active Directory home lab built using VMware Workstation Pro, Windows Server 2022, and Windows client machines. The goal of this project is to practice Windows system administration and help desk tasks in a realistic virtual lab environment.

The lab is organized into multiple parts, starting with the initial domain setup and continuing into Group Policy, client domain joining, permissions, and troubleshooting scenarios.

This project is designed to demonstrate practical skills relevant to help desk, IT support, and junior system administration roles.

---

## Lab Environment

| Component | Details |
|---|---|
| Hypervisor | VMware Workstation Pro 17 |
| Server OS | Windows Server 2022 |
| Domain Controller | DC01 |
| Domain | MumenLab.local |
| Client OS | Windows 10/11 |
| Main Tools | Active Directory Users and Computers, Group Policy Management Console |

---

## Project Parts

| Part | Description | Status |
|---|---|---|
| [Part 1: AD Setup, OUs, Groups, and Users](Part1-AD-Setup-OUs-Groups-Users/) | Created the Windows Server VM, installed Active Directory Domain Services, promoted the server to a domain controller, and created OUs, groups, and users. | Complete |
| [Part 2: Group Policy Objects](Part2-Group-Policy-Objects/) | Create and configure basic Group Policy Objects such as password policy, account lockout policy, drive mapping, desktop wallpaper, Control Panel restrictions, and USB storage restrictions. | Planned |
| [Part 3: Client VM and GPO Testing](Part3-Client-VM-and-GPO-Testing/) | Join a Windows client VM to the domain, log in as domain users, and test the configured Group Policy settings. | Planned |

---

## Skills Demonstrated

- Windows Server 2022 administration
- Active Directory Domain Services
- Domain controller setup
- Organizational Unit management
- User and group administration
- Group Policy Object configuration
- Windows client domain joining
- Help desk troubleshooting scenarios
- Basic access control and permissions
- Technical documentation

---

## Help Desk Relevance

This lab focuses on tasks commonly performed in help desk and IT support environments, including:

- Creating user accounts
- Managing group membership
- Organizing users and computers in Active Directory
- Applying password and lockout policies
- Supporting domain-joined workstations
- Troubleshooting user access issues
- Documenting technical work clearly

---

## Project Status

This project is currently in progress.

Completed:

- Part 1: AD setup, OUs, groups, and users

Planned:

- Part 2: Group Policy Objects
- Part 3: Client VM and GPO testing
- Future: shared folders, NTFS permissions, password resets, account unlocks, and ticket-style troubleshooting examples