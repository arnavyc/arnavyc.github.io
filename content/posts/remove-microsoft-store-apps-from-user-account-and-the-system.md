---
title: "Remove Microsoft Store apps from User Account and the System"
categories:
  - Windows
  - PowerShell
date: 2021-09-13T12:22:17+05:30
draft: false
---

This post shows how to remove Microsoft Store apps form User Account and the System.

# Provisioned Apps

## Get list of provisioned Microsoft Store apps

To get list of all provisioned apps, run the following command in PowerShell \(or PowerShell Core\):

```powershell
$ Get-ProvisionedAppxPackage -Online
```

## Remove provisioned apps you don't require

To remove unwanted provisioned apps, run the following command in an elevated PowerShell \(or PowerShell Core\):

```powershell
$ Remove-ProvisionedAppxPackage -Online -PackageName <Package Name>
```

replacing `<Package Name>` with the name of package you want to remove.

# Installed apps

## Get list of all installed apps

To get a list of all installed apps for your user account, run the following command:

```powershell
$ Get-AppxPackage -Online
```

For getting list of all installed apps for all users, append `'-AllUsers'` to the command.

## Remove each unwanted app for your user account

To remove each unwanted app for your user account, run the command:

```powershell
$ Remove-AppxPackage -PackageName <Package Name>
```

replacing `<Package Name>` with name of package you want to remove.

To remove an app for all users, append `'-AllUsers'` to the command.
