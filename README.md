# Managing-Password-Security
# 🔐 Active Directory Password Policy Management Lab

## 📌 Overview

This lab demonstrates how to view and modify the **Active Directory Default Domain Password Policy** using **Windows PowerShell**. The goal is to strengthen domain security by implementing password policies that align more closely with security best practices and recommendations from **NIST SP 800-63B**.

---

# 🎯 Objectives

- View the current Active Directory domain password policy.
- Import the Active Directory PowerShell module.
- Configure stronger password requirements.
- Configure account lockout settings.
- Verify the updated policy.
- Understand how password policies improve enterprise security.

---

# 🖥️ Lab Environment

- **Operating System:** Windows Server
- **Machine:** DC10
- **Domain:** Structureality
- **User:** Structureality\Administrator
- **Tool:** Windows PowerShell (Administrator)
- **Technology:** Active Directory Domain Services (AD DS)

---

# 📚 Scenario

After performing password spraying, dictionary attacks, and brute-force attacks against the organization's environment, it became clear that the existing password policy was too weak.

To reduce the risk of credential attacks, the domain password policy is updated according to stronger security standards based on **NIST Digital Identity Guidelines (SP 800-63B).**

---

# 🔍 Step 1 – Open PowerShell

Launch **Windows PowerShell** as Administrator.

Import the Active Directory module:

```powershell
Import-Module ActiveDirectory
```

---

# 🔍 Step 2 – View Current Password Policy

Display the current Active Directory password policy.

```powershell
Get-ADDefaultDomainPasswordPolicy
```

### Existing Configuration

| Setting | Value |
|---------|-------|
| Lockout Duration | 15 Minutes |
| Complexity Enabled | True |
| Minimum Password Age | 3 Days |
| Lockout Threshold | 0 (Disabled) |
| Maximum Password Age | 42 Days |
| Minimum Password Length | 7 Characters |

---

# 🔐 Step 3 – Configure Stronger Password Policy

### Set Lockout Observation Window

```powershell
Set-ADDefaultDomainPasswordPolicy -Identity structureality -LockoutObservationWindow 00:15:00
```

---

### Set Lockout Duration

```powershell
Set-ADDefaultDomainPasswordPolicy -Identity structureality -LockoutDuration 00:15:00
```

---

### Set Account Lockout Threshold

Lock the account after **3 failed login attempts**.

```powershell
Set-ADDefaultDomainPasswordPolicy -Identity structureality -LockoutThreshold 3
```

---

### Set Maximum Password Age

```powershell
Set-ADDefaultDomainPasswordPolicy -Identity structureality -MaxPasswordAge 365.00:00:00
```

---

### Set Minimum Password Age

```powershell
Set-ADDefaultDomainPasswordPolicy -Identity structureality -MinPasswordAge 3.00:00:00
```

---

### Set Minimum Password Length

```powershell
Set-ADDefaultDomainPasswordPolicy -Identity structureality -MinPasswordLength 12
```

---

# ✅ New Password Policy

| Setting | New Value |
|---------|-----------|
| Lockout Observation Window | 15 Minutes |
| Lockout Duration | 15 Minutes |
| Lockout Threshold | 3 Attempts |
| Maximum Password Age | 365 Days |
| Minimum Password Age | 3 Days |
| Minimum Password Length | 12 Characters |
| Password Complexity | Enabled |

---

# 🔍 Step 4 – Verify the Configuration

Run:

```powershell
Get-ADDefaultDomainPasswordPolicy
```

Verify that all updated settings appear correctly.

---

# 🔄 Optional: Force Users to Change Password

Remove the "Password Never Expires" setting.

```powershell
Get-ADUser -Filter * | Set-ADUser -PasswordNeverExpires $False
```

Require users to change their password at the next logon.

```powershell
Get-ADUser -Filter * | Set-ADUser -ChangePasswordAtLogon $True
```

---

# 🛡️ Security Benefits

- Prevents password spraying attacks.
- Reduces brute-force attack success.
- Enforces stronger passwords.
- Implements account lockout protection.
- Increases overall Active Directory security.
- Aligns with NIST password recommendations.
- Improves enterprise identity protection.

---

# 📖 PowerShell Commands Used

```powershell
Import-Module ActiveDirectory

Get-ADDefaultDomainPasswordPolicy

Set-ADDefaultDomainPasswordPolicy -Identity structureality -LockoutObservationWindow 00:15:00

Set-ADDefaultDomainPasswordPolicy -Identity structureality -LockoutDuration 00:15:00

Set-ADDefaultDomainPasswordPolicy -Identity structureality -LockoutThreshold 3

Set-ADDefaultDomainPasswordPolicy -Identity structureality -MaxPasswordAge 365.00:00:00

Set-ADDefaultDomainPasswordPolicy -Identity structureality -MinPasswordAge 3.00:00:00

Set-ADDefaultDomainPasswordPolicy -Identity structureality -MinPasswordLength 12

Get-ADDefaultDomainPasswordPolicy

Get-ADUser -Filter * | Set-ADUser -PasswordNeverExpires $False

Get-ADUser -Filter * | Set-ADUser -ChangePasswordAtLogon $True
```

---

# ✅ Skills Demonstrated

- Active Directory Administration
- Windows PowerShell
- Domain Password Policy Management
- Account Lockout Configuration
- Enterprise Identity Security
- Password Hardening
- NIST SP 800-63B Best Practices
- Windows Server Administration
- Security Policy Enforcement

---

## ⭐ Key Takeaway

This lab demonstrates how to strengthen an Active Directory environment by implementing secure password and account lockout policies with PowerShell. These configurations help defend against common credential-based attacks such as password spraying, brute-force, and dictionary attacks while improving compliance with modern cybersecurity best practices.
