# Azure Active Directory Domain Lab

This lab demonstrates the deployment, configuration, and management of an Active Directory environment in Microsoft Azure. It includes a domain controller (`DC-1`), a Windows 10 client (`Client-1`), and various domain administration tasks such as creating OUs, managing users, setting up Remote Desktop access, and configuring account lockout policies.

---

## Technologies Used

- Microsoft Azure  
- Windows Server 2022  
- Windows 10  
- Active Directory Domain Services (AD DS)  
- DNS  
- Remote Desktop Protocol (RDP)  
- PowerShell / PowerShell ISE  
- Group Policy Management  
- Active Directory Users and Computers (ADUC)  
- Event Viewer  

---

## Lab Objectives

- Deploy a virtualized Active Directory infrastructure in Azure  
- Promote a Windows Server VM to a Domain Controller  
- Join a Windows 10 client to the domain  
- Configure and manage users, OUs, and policies via Active Directory  
- Test Remote Desktop access for standard domain users  
- Implement and test account lockout policies  
- Observe security events using Event Viewer  

---

## Initial Setup

### Phase 1: Deploy and Connect

1. **Deploy DC-1**
   - Windows Server 2022  
   - Static Private IP  
   - Firewall temporarily disabled  

2. **Deploy Client-1**
   - Windows 10  
   - Same virtual network/subnet as DC-1  
   - DNS set to DC-1’s private IP  

3. **Test Connectivity**
   - Ping DC-1 from Client-1  
   - Run `ipconfig /all` to verify DNS settings  

---

## Active Directory Configuration

### 1. Promote DC-1 to a Domain Controller
- Install Active Directory Domain Services on DC-1  
- Create a new forest (e.g., `mydomain.com`)  
- Restart and log in as `mydomain.com\labuser`  

### 2. Create Organizational Units and Admin User
- Create the following OUs:
  - `_EMPLOYEES`  
  - `_ADMINS`  
- Create a new user:
  - **Name**: Jane Doe  
  - **Username**: `jane_admin`  
  - Add `jane_admin` to the **Domain Admins** group  
- Log out and back in as `mydomain.com\jane_admin`  

---

## Join Client to Domain

- Log in to Client-1 as local admin  
- Join `mydomain.com` domain  
- Restart Client-1  
- Verify Client-1 appears in ADUC  
- Move Client-1 to the `_CLIENTS` OU  

---

## Remote Desktop Setup for Domain Users

- Log in to Client-1 as `mydomain.com\jane_admin`  
- Enable Remote Desktop for “Domain Users” in System Properties  
- Test login to Client-1 with a standard domain user  

---

## Bulk User Creation

- On DC-1, open **PowerShell ISE** as administrator  
- Paste and run the user creation script to populate `_EMPLOYEES` OU  
- Verify users appear in ADUC  
- Test logging in to Client-1 with one of the new users  

---

## Account Lockout Policy

### 1. Initial Lockout Test  
- Choose a test user  
- Attempt incorrect login 10 times  

### 2. Configure Lockout Threshold via Group Policy  
- Set lockout threshold to 5 attempts  

### 3. Test and Observe  
- Fail login 6 times  
- Confirm account lockout in ADUC  
- Reset the password and unlock the account  
- Test successful login  

---

## Enable/Disable User Accounts

- Disable a user in ADUC  
- Attempt login and observe the access error  
- Re-enable the account and verify successful login  

---

## Event Log Observation

- Open **Event Viewer** on both DC-1 and Client-1  
- Review:
  - Logon attempts  
  - Lockout events  
  - Account changes  

---

## Skills and Experience Gained

This lab delivers hands-on experience with setting up and managing a foundational Active Directory environment in a cloud-hosted infrastructure. Practical skills developed include:

- Deploying a **Windows Server domain controller** and a **domain-joined Windows 10 client** in Azure  
- Promoting a server to a **Domain Controller** and configuring an Active Directory forest  
- Creating and organizing **Organizational Units (OUs)** for structured administration  
- Managing user accounts, including **privileged access** through security groups  
- Enabling and testing **Remote Desktop access** for domain users  
- Automating user provisioning with **PowerShell scripting**  
- Implementing **account lockout policies** via Group Policy to enhance security posture  
- Using **Event Viewer** to monitor logon activity, account changes, and security events  

These exercises build a core understanding of identity and access management in enterprise IT environments, supporting future roles in system administration, security operations, and cloud infrastructure management.

## Screenshots

All screenshots for this lab can be found in the [screenshots](./screenshots) folder.
