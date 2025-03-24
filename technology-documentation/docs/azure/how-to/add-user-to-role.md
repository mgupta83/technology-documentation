---
sidebar_position: 1
id: add-user-to-role
title: Assign a User to a Role in Azure AD App Registration
sidebar_label: Assign User to Role
slug: /azure/how-to/add-user-to-role
---

# Assign a User to a Role in Azure AD App Registration

## **Purpose**
This SOP outlines the steps to assign a user to a specific role in an **Azure AD App Registration**. The parameters allow customization based on application requirements.

## **Parameters**
Before following this SOP, gather the following details:

| Parameter | Description | Example |
|-----------|------------|---------|
| **App Name** | Name of the Azure AD App Registration | `MyApp` |
| **Role Name** | Name of the role to assign | `Admin` |
| **User Principal Name (UPN)** | Email or UPN of the user | `user@example.com` |
| **Client ID** | App Registration’s Client ID | `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` |
| **Tenant ID** | Azure AD Tenant ID | `yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy` |

---

## **Procedure**

### **Step 1: Sign in to Azure Portal**
1. Go to [Azure Portal](https://portal.azure.com).
2. Sign in with an **admin account** that has the necessary permissions.

### **Step 2: Locate the Application**
1. Navigate to **Azure Active Directory** → **App registrations**.
2. Search for the **App Name** (`{App Name}`) and click on it.

### **Step 3: Assign a User to a Role**
#### **Using Azure Portal**
1. In the App Registration menu, go to **Enterprise Applications**.
2. Find and select the application (`{App Name}`).
3. Click **Users and groups** → **Add user/group**.
4. Click **Users**, search for the user (`{User Principal Name}`), and select them.
5. Click **Roles**, select the required role (`{Role Name}`), and click **Assign**.

#### **Using Azure PowerShell (Alternative Method)**
If you prefer automation, use the following PowerShell command:
```powershell
Connect-AzureAD
$role = Get-AzureADApplicationRole -ApplicationId "{Client ID}" | Where-Object { $_.DisplayName -eq "{Role Name}" }
$User = Get-AzureADUser -ObjectId "{User Principal Name}"
New-AzureADUserAppRoleAssignment -ObjectId $User.ObjectId -ResourceId "{Client ID}" -Id $role.Id
