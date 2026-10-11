# PowerShell for Windows IT Support

A practical beginner's reference for using PowerShell to inspect Windows, troubleshoot common issues, and automate simple tasks.

## Table of Contents

- [1. What Is PowerShell?](#1-what-is-powershell)
- [2. Open PowerShell and Check Your Version](#2-open-powershell-and-check-your-version)
- [3. Command Basics](#3-command-basics)
- [4. Navigation and Files](#4-navigation-and-files)
- [5. Variables and the Pipeline](#5-variables-and-the-pipeline)
- [6. Processes](#6-processes)
- [7. Services](#7-services)
- [8. Network Troubleshooting](#8-network-troubleshooting)
- [9. System Information and Storage](#9-system-information-and-storage)
- [10. Event Logs](#10-event-logs)
- [11. Local Users and Groups](#11-local-users-and-groups)
- [12. Basic Scripts and Reports](#12-basic-scripts-and-reports)
- [13. Script Safety](#13-script-safety)
- [14. Quick Reference](#14-quick-reference)
- [15. Practice Checklist](#15-practice-checklist)
- [16. Official Documentation](#16-official-documentation)

---

## 1. What Is PowerShell?

PowerShell is a command-line shell and scripting language from Microsoft. It helps IT support technicians inspect Windows, diagnose issues, and automate repetitive tasks.

Common uses:

- Inspect running processes and services.
- Browse and read files.
- Check network configuration and connectivity.
- Collect system information.
- Read Windows event logs.
- Automate repeatable tasks with scripts.

PowerShell commands are often called **cmdlets** and usually follow a `Verb-Noun` naming pattern, such as `Get-Process` or `Get-Service`.

> **Learning tip:** Start with commands that only display information. Learn commands that change the system after you understand their effects.

## 2. Open PowerShell and Check Your Version

Open **Windows Terminal** or **PowerShell** from the Start menu. Use **Run as administrator** only when a task requires elevated privileges.

```powershell
# Show the PowerShell version
$PSVersionTable

# Show the current user
whoami

# Show the current directory
Get-Location
```

Windows PowerShell 5.1 and PowerShell 7+ are different versions. Some commands and modules may vary by version and system configuration.

## 3. Command Basics

### Find commands and get help

```powershell
# Find commands with "Service" in the name
Get-Command *-Service

# Read help for a command
Get-Help Get-Service

# View examples
Get-Help Get-Service -Examples
```

### Understand command syntax

```powershell
Get-Process -Name notepad
```

- `Get-Process` is the command.
- `-Name` is a parameter.
- `notepad` is the parameter value.

## 4. Navigation and Files

```powershell
# Show the current folder
Get-Location

# List files and folders
Get-ChildItem

# List items in a specific folder
Get-ChildItem C:\Users

# Include hidden items
Get-ChildItem -Force

# Change folder
Set-Location C:\Windows

# Move up one folder
Set-Location ..

# Go to the current user's home folder
Set-Location $HOME
```

### Create, read, copy, and move practice files

Use a practice folder that you are allowed to modify.

```powershell
# Create a practice folder
New-Item -Path "$HOME\PowerShell-Lab" -ItemType Directory

# Create a text file
New-Item -Path "$HOME\PowerShell-Lab\notes.txt" -ItemType File

# Read the file
Get-Content "$HOME\PowerShell-Lab\notes.txt"

# Copy the file
Copy-Item "$HOME\PowerShell-Lab\notes.txt" "$HOME\PowerShell-Lab\notes-copy.txt"

# Rename or move the copy
Move-Item "$HOME\PowerShell-Lab\notes-copy.txt" "$HOME\PowerShell-Lab\notes-archive.txt"
```

**Caution:** `Remove-Item` deletes files or folders. Verify the exact path before using it, and avoid recursive deletion or wildcards until you fully understand the consequences.

## 5. Variables and the Pipeline

### Variables

Variables store values and begin with `$`.

```powershell
$name = "PowerShell Lab"
$count = 3

$name
$count
```

### Pipeline

The pipeline symbol `|` sends output from one command to another. PowerShell commonly passes structured objects, which can be filtered, sorted, and selected.

```powershell
# List running services
Get-Service | Where-Object Status -eq "Running"

# Sort processes by working-set memory
Get-Process | Sort-Object WorkingSet64 -Descending

# Display selected service properties
Get-Service | Select-Object Name, Status
```

## 6. Processes

A **process** is a running instance of a program. Task Manager and PowerShell can help identify applications using unusual resources.

```powershell
# List processes
Get-Process

# Find a process by name
Get-Process -Name notepad

# Show the 10 processes with the largest working set
Get-Process |
    Sort-Object WorkingSet64 -Descending |
    Select-Object -First 10 Name, Id, WorkingSet64
```

`WorkingSet64` is measured in bytes. A high value does not automatically mean a process is faulty.

### Stop a process

```powershell
Stop-Process -Name notepad
```

Try closing an application normally first. Stopping a process may cause unsaved work to be lost. Do not stop unfamiliar Windows system processes.

## 7. Services

A **service** is a background component that provides a Windows or application function.

```powershell
# List services
Get-Service

# Check the Print Spooler service
Get-Service -Name Spooler

# Show stopped services
Get-Service | Where-Object Status -eq "Stopped"
```

### Start, stop, or restart a service

```powershell
Start-Service -Name Spooler
Stop-Service -Name Spooler
Restart-Service -Name Spooler
```

These commands can require administrator privileges and may affect users or applications. Only change a service when you understand its purpose and are authorized to do so.

**Example — printer troubleshooting**

1. Check the printer's power, connection, selected printer, and print queue.
2. Check the service with `Get-Service -Name Spooler`.
3. Restart it only if appropriate and authorized.
4. Test printing and document the result.

A stopped service is not always a problem; some services are normally stopped until needed.

## 8. Network Troubleshooting

### Inspect network settings

```powershell
# View network configuration
Get-NetIPConfiguration

# View IP addresses
Get-NetIPAddress

# View DNS server settings
Get-DnsClientServerAddress
```

### Test connectivity

```powershell
# Test basic reachability with ICMP
Test-Connection example.com -Count 4

# Test connectivity to a host
Test-NetConnection example.com

# Test a TCP port, such as HTTPS
Test-NetConnection example.com -Port 443

# Look up a DNS name
Resolve-DnsName example.com
```

A failed ping does not always mean the internet is down; some networks block ICMP. A successful test to one host or port does not prove that every service is working.

### Network troubleshooting sequence

1. Check Wi-Fi, Ethernet, airplane mode, and cables.
2. Check whether other devices have the same issue.
3. Inspect IP configuration.
4. Test the gateway and an external destination when appropriate.
5. Check DNS, VPN, proxy, firewall, and organization policies.
6. Record results before changing settings.

Commands such as `ipconfig /release` and `ipconfig /renew` can interrupt connectivity. Use them only when appropriate, especially on devices with static or managed network configurations.

## 9. System Information and Storage

```powershell
# Show Windows and computer information
Get-ComputerInfo

# Show the computer name
$env:COMPUTERNAME

# Show the current user
$env:USERNAME

# Show Windows version and last boot time
Get-CimInstance Win32_OperatingSystem |
    Select-Object Caption, Version, BuildNumber, LastBootUpTime

# Show available volumes
Get-Volume
```

### Check disk space

```powershell
Get-CimInstance Win32_LogicalDisk |
    Select-Object DeviceID, VolumeName,
        @{Name="SizeGB";Expression={[math]::Round($_.Size / 1GB, 2)}},
        @{Name="FreeGB";Expression={[math]::Round($_.FreeSpace / 1GB, 2)}}
```

Low free space can affect updates and the ability to save files. Confirm which volume is affected before taking action. Do not automatically delete files just because a disk is nearly full.

## 10. Event Logs

Windows event logs can provide evidence about errors around the time a problem occurred.

```powershell
# Show the 20 most recent System events
Get-WinEvent -LogName System -MaxEvents 20

# Show the 20 most recent Application events
Get-WinEvent -LogName Application -MaxEvents 20
```

### Find System errors from the last 24 hours

```powershell
Get-WinEvent -FilterHashtable @{
    LogName   = 'System'
    Level     = 2
    StartTime = (Get-Date).AddHours(-24)
} -ErrorAction SilentlyContinue
```

An error event is not automatically the root cause. Compare its timestamp, source, event ID, and message with the reported symptoms.

## 11. Local Users and Groups

On supported Windows configurations, these commands can inspect local accounts:

```powershell
# List local users
Get-LocalUser

# List local groups
Get-LocalGroup

# Inspect a specific local user
Get-LocalUser -Name "someuser"
```

Replace `someuser` with the actual local account name. These commands may not be available in every environment.

Creating accounts, changing passwords, or changing group membership can affect security and access. Perform those tasks only when authorized and according to organizational policy.

## 12. Basic Scripts and Reports

A PowerShell script is a text file that usually uses the `.ps1` extension.

### Example: basic computer report

```powershell
$computerName = $env:COMPUTERNAME
$timestamp = Get-Date
$os = Get-CimInstance Win32_OperatingSystem

Write-Output "Computer: $computerName"
Write-Output "Time: $timestamp"
Write-Output "Operating system: $($os.Caption)"
Write-Output "Version: $($os.Version)"
```

### Export process information to CSV

```powershell
Get-Process |
    Select-Object Name, Id, CPU, WorkingSet64 |
    Export-Csv -Path "$HOME\process-report.csv" -NoTypeInformation
```

Check a report for sensitive information before sharing it. Do not commit passwords, access tokens, recovery keys, or private system information to a public repository.

## 13. Script Safety

Check the current execution policy:

```powershell
Get-ExecutionPolicy
Get-ExecutionPolicy -List
```

Execution policy is not a complete security boundary. Do not change it just to run an unknown script.

Before running a script:
- Read and understand its commands.
- Check where it came from.
- Use a lab environment for practice.
- Avoid unnecessary administrator privileges.
- Be cautious with deletion, permissions, services, networking, and Registry changes.
- Follow your organization's rules.

## 14. Quick Reference

| Task | Command |
|---|---|
| Show current directory | `Get-Location` |
| List files and folders | `Get-ChildItem` |
| Read a text file | `Get-Content` |
| Find commands | `Get-Command` |
| Get command help | `Get-Help Get-Service -Examples` |
| List processes | `Get-Process` |
| List services | `Get-Service` |
| Show network configuration | `Get-NetIPConfiguration` |
| Test a network connection | `Test-NetConnection` |
| Resolve a DNS name | `Resolve-DnsName` |
| Show TCP connections | `Get-NetTCPConnection` |
| Show Windows information | `Get-CimInstance Win32_OperatingSystem` |
| Show volumes | `Get-Volume` |
| Read recent System events | `Get-WinEvent -LogName System -MaxEvents 20` |
| List local users | `Get-LocalUser` |
| List local groups | `Get-LocalGroup` |
| Export results to CSV | `Export-Csv` |

## 15. Practice Checklist

Start with read-only commands and practise on your own computer or a lab.

- [ ] Check the PowerShell version.
- [ ] Display the current user and computer name.
- [ ] List files in a folder.
- [ ] Create and read a practice text file.
- [ ] Copy and rename a practice file.
- [ ] List processes and identify their PIDs.
- [ ] Check the Print Spooler service without changing it.
- [ ] Display network configuration.
- [ ] Test DNS and a TCP port.
- [ ] Check available disk space.
- [ ] Read recent System events.
- [ ] Export a process list to CSV.
- [ ] Write a small script that reports basic computer information.
- [ ] Document what each command does and what its output means.

Do not practise stopping services, changing permissions, or deleting files on a work or shared computer without explicit authorization.

## 16. Official Documentation

- [PowerShell documentation — Microsoft Learn](https://learn.microsoft.com/powershell/)
- [PowerShell overview](https://learn.microsoft.com/powershell/scripting/overview)
- [Windows commands reference](https://learn.microsoft.com/windows-server/administration/windows-commands/windows-commands)
- [Windows documentation](https://learn.microsoft.com/windows/)
