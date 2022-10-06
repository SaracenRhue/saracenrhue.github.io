---
title: Chocolatey
date: 2022-10-06 +0000
categories: [tutorial, install, packagemanager]
tags: [tutorial, install, packagemanager, windows, shell]
---

Chocolatey is a package manager for Windows. It is similar to apt, yum, and other package managers.

## Install

Open a powershell as administrator and run the following command:

```powershell
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

Before you can use Chocolatey, you need to restart your shell.

## Usage

### check available packages

```powershell
choco search <package>
```

### install a package

```powershell
choco install <package>
```

### uninstall a package

```powershell
choco uninstall <package>
```

[Chocolatey](https://chocolatey.org/)
