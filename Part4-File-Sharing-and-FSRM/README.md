# Active Directory Help Desk Lab - Part 4

## File Sharing, Mapped Drives, and File Server Resource Manager

## Overview

This section documents Part 4 of my Active Directory home lab. In this part, I configured a shared folder on the Windows Server, applied share and NTFS permissions, tested manual network drive mapping from a domain-joined client, created a Group Policy Object to automatically map the shared drive, and used File Server Resource Manager to configure storage management controls.

The goal of this section is to practice common help desk and IT support tasks related to shared folders, mapped drives, permissions, and file server management.

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
| Test User | Mike Paul |
| Main Tools | File Explorer, Active Directory, Group Policy Management Console, File Server Resource Manager, Command Prompt |

---

## Objectives

- Create a shared folder on the Windows Server
- Configure share permissions for domain users
- Configure NTFS permissions for domain users
- Confirm the server hostname
- Manually map a network drive from the client machine
- Confirm that the shared folder is accessible from the client
- Create a Group Policy Object for automatic drive mapping
- Link the drive mapping GPO to the correct Users OU
- Force Group Policy updates using `gpupdate /force`
- Confirm the mapped drive appears after reboot
- Install File Server Resource Manager
- Create a quota for the shared folder
- Configure file screening for the shared folder
- Verify the final quota and file screen configuration

---

## Key Concepts

## Share Permissions vs NTFS Permissions

Windows file sharing uses two important permission types: share permissions and NTFS permissions.

| Permission Type | Applies To | Purpose |
|---|---|---|
| Share Permissions | Network access to the shared folder | Controls access when users connect over the network |
| NTFS Permissions | Folder, subfolders, and files | Controls detailed access to local and network files |

When both permission types are used together, the most restrictive effective permission usually applies. This is important for help desk and IT support because users may report access issues even when one permission type looks correct.

---

## Manual Drive Mapping vs GPO Drive Mapping

A network drive can be mapped manually on a client computer, but this is not efficient for a larger environment.

| Method | Description |
|---|---|
| Manual Drive Mapping | The drive is mapped directly on one client machine |
| GPO Drive Mapping | The drive is mapped automatically for users through Group Policy |

Using a GPO is better for an Active Directory environment because it applies automatically when users log in.

---

## File Server Resource Manager

File Server Resource Manager is a Windows Server tool used to manage storage on file servers.

In this lab, I used it to configure:

- Quotas for storage limits
- File screening to restrict certain file types
- Centralized file server management

---

## 1. Creating the Shared Folder

I created a folder on the Windows Server to use as the network shared folder.

![Create Shared Folder](screenshots/01-create-shared-folder.png)

This folder is used later for testing network access from the client machine.

---

## 2. Configuring Share Permissions

I configured share permissions for the shared folder and added domain users.

![Share Permissions Domain Users](screenshots/02-share-permissions-domain-users.png)

This allows users in the domain to access the shared folder over the network.

---

## 3. Configuring NTFS Permissions

I also checked and configured NTFS permissions on the Security tab.

![NTFS Permissions Domain Users](screenshots/03-ntfs-permissions-domain-users.png)

NTFS permissions provide more detailed control over what users can do inside the folder.

---

## 4. Confirming the Server Hostname

I used the `hostname` command to confirm the server name.

![Hostname Command](screenshots/04-hostname-command.png)

The hostname is important because it is used in the UNC path for the shared folder.

Example path format:

```text
\\SERVERNAME\SharedFolder
```

---

## 5. Manually Mapping the Network Drive

On the client machine, I manually mapped the shared folder as a network drive.

![Map Network Drive Manual](screenshots/05-map-network-drive-manual.png)

This tests whether the client can access the shared folder using the server name and shared folder path.

---

## 6. Confirming the Mapped Drive Works

After mapping the drive, I confirmed that the shared folder appeared in File Explorer.

![Mapped Drive Success](screenshots/06-mapped-drive-success.png)

This confirms that network sharing and permissions are working correctly.

---

## 7. Creating the Map Drive GPO

Next, I created a Group Policy Object for automatic drive mapping.

![Create Map Drive GPO](screenshots/07-create-map-drive-gpo.png)

This GPO is used to automatically map the shared drive for domain users.

---

## 8. Configuring the Map Drive GPO Settings

Inside the GPO, I configured the drive mapping settings under User Configuration preferences.

![Map Drive GPO Settings](screenshots/08-map-drive-gpo-settings.png)

The mapped drive was configured using the shared folder path and a drive letter.

---

## 9. Linking the GPO to the Users OU

I linked the drive mapping GPO to the Users OU.

![Map Drive GPO Linked Users OU](screenshots/09-map-drive-gpo-linked-users-ou.png)

This allows the policy to apply to domain users in that OU.

---

## 10. Forcing Group Policy Update on the Client

On the client machine, I ran:

```text
gpupdate /force
```

![GPUpdate Force Client](screenshots/10-gpupdate-force-client.png)

This forces the client to refresh Group Policy immediately.

---

## 11. Confirming the Mapped Drive After Reboot

After rebooting the client, I confirmed that the mapped drive still appeared.

![Mapped Drive After Reboot](screenshots/11-mapped-drive-after-reboot.png)

This shows that the mapped drive is now being applied through Group Policy instead of only being manually mapped.

---

## 12. Installing File Server Resource Manager

I installed File Server Resource Manager using Server Manager.

![Install FSRM Role](screenshots/12-install-fsrm-role.png)

This tool is used to manage quotas and file screening on shared folders.

---

## 13. Opening File Server Resource Manager

After installation, I opened File Server Resource Manager.

![FSRM Opened](screenshots/13-fsrm-opened.png)

This console provides centralized tools for managing file server storage.

---

## 14. Creating a Quota for the Shared Folder

I created a quota for the shared folder.

![Create Quota Shared Folder](screenshots/14-create-quota-shared-folder.png)

The quota limits how much storage the shared folder can use. This helps prevent users from filling up server storage.

---

## 15. Creating a File Screen

I created a file screen for the shared folder.

![Create File Screen](screenshots/15-create-file-screen.png)

File screening can be used to block certain file types from being saved in the shared folder.

---

## 16. Confirming the Final Quota Configuration

I confirmed that the quota was created in File Server Resource Manager.

![Final Quotas](screenshots/16-final-quotas.png)

This verifies that storage limits were configured for the shared folder.

---

## 17. Confirming the Final File Screen Configuration

I confirmed that the file screen was created in File Server Resource Manager.

![Final File Screen](screenshots/17-final-file-screen.png)

This verifies that file type restrictions were configured for the shared folder.

---

## Help Desk Relevance

This lab section demonstrates several tasks that are directly related to help desk and IT support roles.

| Help Desk / IT Task | Lab Example |
|---|---|
| Shared folder setup | Created a shared folder on Windows Server |
| Permission troubleshooting | Configured share and NTFS permissions |
| Network path troubleshooting | Used the server hostname and UNC path |
| Drive mapping support | Manually mapped a network drive on the client |
| Group Policy support | Created and linked a drive mapping GPO |
| User environment support | Confirmed the mapped drive appears after reboot |
| File server administration | Installed and used File Server Resource Manager |
| Storage management | Created a quota for the shared folder |
| File restriction management | Created a file screen for blocked file types |

These are common responsibilities in help desk, desktop support, and junior system administration roles.

---

## Lessons Learned

Through this part of the lab, I learned how shared folders are created and accessed in an Active Directory environment.

I also learned the difference between share permissions and NTFS permissions. Share permissions control network access to the shared folder, while NTFS permissions provide more detailed control over folders and files.

This section also helped me understand why Group Policy is useful for drive mapping. Instead of manually mapping drives for each user, a GPO can automatically apply the mapped drive when users log in.

Finally, I practiced using File Server Resource Manager to manage file server storage with quotas and file screening. This is useful for preventing shared folders from using too much storage and for controlling what file types users can save.

---

## Next Steps

In the next part of this lab, I plan to continue building help desk and system administration scenarios.

Possible next additions include:

- Create department-specific shared folders
- Use security groups to control folder access
- Test different permissions with different users
- Troubleshoot denied access issues
- Document user access requests and permission changes
- Add help desk-style troubleshooting notes

---

## Project Status

Part 4 is complete.

Completed items:

- Created a shared folder
- Configured share permissions
- Configured NTFS permissions
- Confirmed the server hostname
- Manually mapped the shared folder from the client
- Confirmed the mapped drive worked
- Created a drive mapping GPO
- Configured GPO drive map settings
- Linked the GPO to the Users OU
- Ran `gpupdate /force`
- Confirmed the mapped drive after reboot
- Installed File Server Resource Manager
- Created a quota for the shared folder
- Created a file screen for the shared folder
- Verified the final quota configuration
- Verified the final file screen configuration
