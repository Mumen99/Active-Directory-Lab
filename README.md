# Active Directory Help Desk Lab

## Overview

This repository documents my Active Directory home lab built using VMware Workstation Pro, Windows Server 2022, and a Windows client machine. The goal of this project is to practice Windows system administration, help desk support, Group Policy management, file sharing, permissions, and security policy tasks in a realistic virtual lab environment.

The lab is organized into multiple parts, starting with the initial domain setup and continuing into Group Policy, client domain joining, file sharing, File Server Resource Manager, user rights assignment, fine-grained password policies, service accounts, advanced file sharing permissions, inheritance, access-based enumeration, and common help desk support scenarios.

This project is designed to demonstrate practical skills relevant to help desk, IT support, desktop support, and junior system administration roles.

---

## Lab Environment

| Component | Details |
|---|---|
| Hypervisor | VMware Workstation Pro 17 |
| Server OS | Windows Server 2022 |
| Domain Controller | DC01 |
| Domain | MumenLab.local |
| Client OS | Windows 10 Enterprise |
| Client Name | COMPUTER01 |
| Main Tools | Active Directory Users and Computers, Group Policy Management Console, Active Directory Administrative Center, File Server Resource Manager, Command Prompt, Remote Desktop Connection |

---

## Project Parts

| Part | Description | Status |
|---|---|---|
| [Part 1: AD Setup, OUs, Groups, and Users](Part1-AD-Setup-OUs-Groups-Users/) | Created the Windows Server VM, installed Active Directory Domain Services, promoted the server to a domain controller, and created OUs, groups, and users. | Complete |
| [Part 2: Group Policy Objects](Part2-Group-Policy-Objects/) | Created and configured Group Policy Objects, including password policy, account lockout policy, drive mapping, desktop wallpaper, Control Panel restrictions, and removable storage restrictions. | Complete |
| [Part 3: Client VM and GPO Testing](Part3-Client-VM-and-GPO-Testing/) | Joined a Windows client VM to the domain, logged in as a domain user, moved the computer object into the correct OU, tested GPO application, verified policies with `gpresult`, and tested account lockout behavior. | Complete |
| [Part 4: File Sharing and FSRM](Part4-File-Sharing-and-FSRM/) | Created a shared folder, configured share and NTFS permissions, manually mapped a network drive, automated drive mapping through GPO, and used File Server Resource Manager for quotas and file screening. | Complete |
| [Part 5: User Rights and Fine-Grained Password Policies](Part5-User-Rights-and-Fine-Grained-Password-Policies/) | Configured user rights assignment policies, tested local and Remote Desktop logon restrictions, and created fine-grained password policies using Active Directory Administrative Center. | Complete |
| Part 6: Service Accounts and Single-Purpose Computers | Planned section for implementing service accounts and single-purpose computer scenarios in the Windows Server home lab. | Planned |
| Part 7: NTFS vs Share Permissions | Planned section for deeper file sharing permissions, including the difference between NTFS permissions and share permissions. | Planned |
| Part 8: Effective Permissions and Inheritance | Planned section for advanced file sharing topics, including permission inheritance and effective access testing. | Planned |
| Part 9: Access-Based Enumeration | Planned section for configuring access-based enumeration so users only see shared folders they have permission to access. | Planned |
| Part 10: Common Help Desk Tasks | Planned section for realistic help desk workflows such as password resets, account unlocks, group membership changes, user support, access troubleshooting, and ticket-style documentation. | Planned |

---

## Skills Demonstrated

- Windows Server 2022 administration
- Active Directory Domain Services
- Domain controller setup
- Organizational Unit management
- User and group administration
- Group Policy Object creation and linking
- Password and account lockout policy configuration
- Windows client domain joining
- DNS troubleshooting for domain communication
- Group Policy testing with `gpupdate` and `gpresult`
- File sharing and network drive mapping
- Share permissions and NTFS permissions
- File Server Resource Manager configuration
- Quota and file screening management
- User Rights Assignment configuration
- Remote Desktop access control
- Fine-Grained Password Policy configuration
- Help desk troubleshooting scenarios
- Technical documentation

---

## Help Desk Relevance

This lab focuses on tasks commonly performed in help desk, desktop support, and junior system administration environments.

| Help Desk / IT Task | Lab Example |
|---|---|
| User account administration | Created and organized domain users |
| Group management | Created security groups and added users to groups |
| OU management | Organized users and computers into OUs |
| Password policy support | Configured and tested password requirements |
| Account lockout support | Tested account lockout and unlock behavior |
| Workstation support | Joined a Windows client to the domain |
| DNS troubleshooting | Fixed client DNS settings for domain communication |
| Group Policy support | Created, linked, updated, and tested GPOs |
| Access restriction testing | Blocked Control Panel and removable storage through GPO |
| Network drive support | Manually and automatically mapped shared drives |
| File share support | Configured shared folders and permissions |
| Storage management | Configured quotas and file screening with FSRM |
| Server access control | Restricted local and Remote Desktop logons |
| Security administration | Created fine-grained password policies for different groups |
| Planned help desk workflows | Password resets, account unlocks, access requests, group membership changes, and ticket-style troubleshooting |

---

## Repository Structure

```text
Active-Directory-Lab/
├── README.md
├── Part1-AD-Setup-OUs-Groups-Users/
│   ├── README.md
│   └── screenshots/
├── Part2-Group-Policy-Objects/
│   ├── README.md
│   └── screenshots/
├── Part3-Client-VM-and-GPO-Testing/
│   ├── README.md
│   └── screenshots/
├── Part4-File-Sharing-and-FSRM/
│   ├── README.md
│   └── screenshots/
├── Part5-User-Rights-and-Fine-Grained-Password-Policies/
│   ├── README.md
│   └── screenshots/
├── Part6-Service-Accounts-and-Single-Purpose-Computers/
│   ├── README.md
│   └── screenshots/
├── Part7-NTFS-vs-Share-Permissions/
│   ├── README.md
│   └── screenshots/
├── Part8-Effective-Permissions-and-Inheritance/
│   ├── README.md
│   └── screenshots/
├── Part9-Access-Based-Enumeration/
│   ├── README.md
│   └── screenshots/
└── Part10-Common-Help-Desk-Tasks/
    ├── README.md
    └── screenshots/
```

---

## Project Status

This project is currently in progress.

Completed:

- Part 1: AD setup, OUs, groups, and users
- Part 2: Group Policy Objects
- Part 3: Client VM and GPO testing
- Part 4: File sharing, mapped drives, and File Server Resource Manager
- Part 5: User rights assignment and fine-grained password policies

Planned:

- Part 6: Service accounts and single-purpose computers
- Part 7: NTFS vs share permissions
- Part 8: Effective permissions and inheritance
- Part 9: Access-based enumeration
- Part 10: Common help desk tasks and ticket-style troubleshooting examples

---

## Summary

This project demonstrates a practical Active Directory environment with real help desk and system administration workflows. It includes domain setup, user and group management, Group Policy configuration, domain client testing, shared folder access, mapped drives, storage controls, and security policy enforcement.

Future parts will expand the lab into service accounts, advanced permissions, access-based enumeration, and common help desk tasks such as password resets, account unlocks, access requests, and troubleshooting user issues.

The lab is designed to show hands-on experience with tools and tasks commonly used in entry-level IT support and junior system administration roles.
