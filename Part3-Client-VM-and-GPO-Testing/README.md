# Active Directory Help Desk Lab - Part 3

## Client Domain Join and GPO Testing

## Overview

This section documents Part 3 of my Active Directory home lab. In this part, I created a Windows client virtual machine, configured DNS so it could communicate with the domain controller, joined the client to the `MumenLab.local` domain, and tested Group Policy Objects that were created in Part 2.

The goal of this section is to prove that the Active Directory environment is working from a client machine and to test common help desk scenarios such as domain login, Group Policy updates, Control Panel restriction, and account lockout.

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
| Main Tools | Active Directory Users and Computers, Group Policy Management Console, Command Prompt |

---

## Objectives

- Create a Windows client virtual machine
- Attach and install Windows client ISO
- Configure DNS on the client machine
- Confirm network connectivity to the domain controller
- Confirm domain DNS resolution using `nslookup`
- Join the client machine to the Active Directory domain
- Log in using a domain user account
- Confirm the computer object appears in Active Directory
- Move the computer object into the correct Organizational Unit
- Link GPOs to the correct OUs
- Force Group Policy updates using `gpupdate /force`
- Confirm applied policies using `gpresult /r`
- Test Control Panel restriction
- Test Account Lockout Policy
- Unlock a locked user account in Active Directory

---

## Key Concepts

## Domain-Joined Client

A domain-joined client is a workstation that has been added to an Active Directory domain. This allows users to log in using domain accounts instead of only local accounts.

In this lab, the client machine `COMPUTER01` was joined to:

```text
MumenLab.local
```

This allows domain users such as `MUMENLAB\mikepaul` to log in and receive Group Policy settings from the domain controller.

---

## DNS and Active Directory

DNS is very important in Active Directory. A client machine must use the domain controller as its DNS server so it can find and communicate with the domain.

If the client points to the wrong DNS server, domain joining and domain name lookup may fail.

In this lab, I configured the client DNS settings to point to the domain controller IP address.

---

## User GPOs vs Computer GPOs

Some Group Policy Objects apply to users, while others apply to computers.

| GPO Type | Applies To | Example |
|---|---|---|
| User Configuration | Domain user account | Restrict Control Panel, Drive Mapping, Desktop Wallpaper |
| Computer Configuration | Domain-joined computer | Disable USB Devices, Password Policy, Account Lockout Policy |

For GPOs to apply correctly, users and computers need to be placed in the correct Organizational Units.

---

## 1. Creating the Windows Client VM

I created a new Windows client virtual machine in VMware Workstation Pro. This VM is used to test domain joining and Group Policy application.

![Create Client VM](screenshots/01-create-client-vm.png)

---

## 2. Attaching the Client ISO

After creating the client VM, I attached the Windows client ISO file to the virtual CD/DVD drive.

![Attach Client ISO](screenshots/02-attach-client-iso.png)

This allowed the VM to boot into the Windows installation environment.

---

## 3. Installing Windows Client

I installed Windows on the client virtual machine.

![Install Windows Client](screenshots/03-install-windows-client.png)

For this lab, I used a Windows edition that supports domain joining, such as Windows Pro or Windows Enterprise.

---

## 4. Confirming the Client Is Running

After installation, I confirmed that the Windows client VM was running successfully.

![Windows Client Running](screenshots/04-windows-client-running.png)

This client machine is later joined to the `MumenLab.local` domain.

---

## 5. Configuring Static IP and DNS on the Server

On the domain controller, I confirmed the static IP and DNS settings.

![Server Static IP and DNS](screenshots/05-server-static-ip-dns.png)

The domain controller needs a stable IP address because client machines use it for DNS and domain communication.

---

## 6. Configuring DNS on the Client

On the client VM, I configured DNS to point to the domain controller.

![Client DNS Settings](screenshots/06-client-dns-settings.png)

This step is required so the client can find the Active Directory domain.

---

## 7. Testing Connectivity to the Domain Controller

I tested connectivity from the client machine to the domain controller using `ping`.

![Ping Domain Controller](screenshots/07-ping-domain-controller.png)

A successful ping confirms that the client can communicate with the domain controller over the network.

---

## 8. Testing Domain DNS Resolution

I used `nslookup` to confirm that the client could resolve the domain name.

![NSLookup Domain](screenshots/08-nslookup-domain.png)

This confirms that DNS is configured correctly and that the client can locate `MumenLab.local`.

---

## 9. Joining the Client to the Domain

I opened the system properties on the client machine and entered the domain name:

```text
MumenLab.local
```

![Join Client to Domain](screenshots/09-join-client-to-domain.png)

This step adds the Windows client machine to the Active Directory domain.

---

## 10. Domain Join Success

After entering domain administrator credentials, the client successfully joined the domain.

![Domain Join Success](screenshots/10-domain-join-success.png)

This confirms that the client machine can communicate with the domain controller and authenticate against the domain.

---

## 11. Domain Login Screen

After restarting the client, I reached the domain login screen.

![Domain Login Screen](screenshots/11-domain-login-screen.png)

This shows that the machine is now ready for domain user login.

---

## 12. Logging in as a Domain User

I logged in to the client machine using a domain user account.

![Domain User Login](screenshots/12-domain-user-login.png)

The test user used in this section was:

```text
MUMENLAB\mikepaul
```

This confirms that Active Directory authentication is working.

---

## 13. Confirming the Computer Object in Active Directory

After joining the domain, the client computer object appeared in Active Directory Users and Computers.

![Client Computer in AD](screenshots/13-client-computer-in-ad.png)

By default, newly joined computers may appear in the default `Computers` container.

---

## 14. Moving the Client Computer to the Correct OU

I moved the client computer object to the correct Organizational Unit.

![Move Client to OU](screenshots/14-move-client-to-ou.png)

This is important because Group Policy settings are often linked to specific OUs.

---

## 15. Confirming the Client Is in the Correct OU

After moving the computer object, I confirmed that `COMPUTER01` was inside the correct Computer OU.

![Client in Correct OU](screenshots/15-client-in-correct-ou.png)

This allows computer-based GPOs to apply correctly.

---

## 16. Linking GPOs to the Correct OUs

In Group Policy Management Console, I linked the GPOs to the correct OUs.

![Link GPOs to OU](screenshots/16-link-gpos-to-ou.png)

User-based GPOs were linked to the Users OU, while computer-based GPOs were linked to the Computer OU or domain level when required.

### Example GPO Placement

| GPO | Linked To | Reason |
|---|---|---|
| Restrict Control Panel | Users OU | Applies to domain users |
| Drive Mapping | Users OU | Applies when users log in |
| Desktop Wallpaper | Users OU | Applies to the user desktop |
| Disable USB Devices | Computer OU | Applies to the workstation |
| Account Lockout Policy | Domain level | Applies to domain user authentication |

---

## 17. Testing Control Panel Before Group Policy Update

Before forcing a Group Policy update, I tested Control Panel access on the client.

![Control Panel Before GPUpdate](screenshots/17-control-panel-before-gpupdate.png)

At this point, Control Panel was still accessible because the policy had not refreshed yet.

---

## 18. Running GPUpdate Force

To apply the latest Group Policy settings immediately, I ran:

```text
gpupdate /force
```

![Run GPUpdate Force](screenshots/18-run-gpupdate-force.png)

This forces the client machine to refresh Group Policy instead of waiting for the default refresh interval.

---

## 19. Confirming Control Panel Is Blocked

After running `gpupdate /force`, I tested Control Panel again.

![Control Panel Blocked](screenshots/19-control-panel-blocked.png)

The policy blocked access to Control Panel, confirming that the `Restrict Control Panel` GPO was working.

---

## 20. Confirming Applied GPOs with GPResult

I used `gpresult /r` to confirm which Group Policy Objects were applied to the logged-in domain user.

![GPResult Output](screenshots/20-gpresult-output.png)

The output showed that user-based GPOs were applied to Mike Paul, including:

```text
Restrict Control-Panel
Drive Mapping
Desktop Wallpaper
```

This confirms that the user account was in the correct OU and receiving the expected policies.

---

## 21. Testing Account Lockout Policy

To test the Account Lockout Policy, I attempted to log in as Mike Paul using the wrong password multiple times.

![Account Locked Login Screen](screenshots/21-account-locked-login-screen.png)

After reaching the configured lockout threshold, the account was locked.

### Account Lockout Configuration

| Setting | Value |
|---|---|
| Account lockout threshold | 5 invalid logon attempts |
| Account lockout duration | 15 minutes |
| Reset account lockout counter after | 15 minutes |

This simulates a common help desk issue where a user is locked out after entering the wrong password too many times.

---

## 22. Confirming the Locked Account in Active Directory

On the domain controller, I opened Active Directory Users and Computers and checked the account properties for Mike Paul.

![Mike Paul Account Locked in ADUC](screenshots/22-mike-paul-account-locked-aduc.png)

The account was shown as locked, confirming that the Account Lockout Policy worked.

---

## 23. Logging in After Account Unlock

After unlocking the account in Active Directory, I logged back in successfully as Mike Paul.

![Mike Paul Login After Unlock](screenshots/24-mike-paul-login-after-unlock.png)

This confirms that the help desk account unlock process was successful.

---

## Help Desk Relevance

This lab section demonstrates several tasks that are directly related to help desk and IT support roles.

| Help Desk / IT Task | Lab Example |
|---|---|
| Domain joining | Joined a Windows client to the Active Directory domain |
| DNS troubleshooting | Configured DNS and tested domain resolution |
| User login support | Logged in using a domain user account |
| Computer object management | Moved the workstation object to the correct OU |
| Group Policy troubleshooting | Used `gpupdate /force` and `gpresult /r` |
| Access restriction testing | Confirmed Control Panel was blocked by GPO |
| Account lockout support | Tested and verified account lockout behavior |
| Account unlock support | Unlocked a domain user account in ADUC |

These are common responsibilities in entry-level help desk and IT support roles.

---

## Lessons Learned

Through this part of the lab, I learned how a Windows client joins and communicates with an Active Directory domain.

I also learned how important DNS is for domain joining and Group Policy application. If the client DNS settings are incorrect, the client may fail to locate the domain controller or resolve the domain name.

This section also helped me understand how GPOs are tested in a real environment. I used `gpupdate /force` to apply policies immediately and `gpresult /r` to verify which policies were applied to the user.

The account lockout test was especially useful because it represents a realistic help desk scenario where a user is locked out and needs IT support to regain access.

---

## Next Steps

In the next part of this lab, I plan to configure file sharing and permissions.

Planned tasks include:

- Create shared folders on the server
- Configure share permissions
- Configure NTFS permissions
- Use security groups to control folder access
- Test access with different domain users
- Troubleshoot permission issues
- Document the process using help desk-style scenarios

---

## Project Status

Part 3 is complete.

Completed items:

- Created a Windows client VM
- Installed Windows client OS
- Configured DNS for domain communication
- Tested connectivity to the domain controller
- Tested DNS resolution with `nslookup`
- Joined the client machine to the domain
- Logged in as a domain user
- Confirmed the client computer object in Active Directory
- Moved the client computer object to the correct OU
- Linked GPOs to the correct OUs
- Forced Group Policy updates with `gpupdate /force`
- Verified applied policies with `gpresult /r`
- Tested Control Panel restriction
- Tested Account Lockout Policy
- Confirmed and resolved a locked user account
