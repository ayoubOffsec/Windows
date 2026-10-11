# Windows Basics — Complete Beginner's Guide
## 1. Introduction
What is Windows?
Windows is an operating system developed by Microsoft. An operating system (OS) manages computer hardware and software and provides a platform for applications to run.
Windows helps manage:
- The CPU, RAM, storage, and connected devices.
- Applications and their processes.
- Files, folders, and permissions.
- User accounts and security settings.
- Network connections.
- System updates, recovery, and troubleshooting.
Main goals of this guide
By the end of this guide, you should be able to:
- Explain the main components of Windows.
- Understand users, groups, permissions, processes, and services.
- Recognize important system folders and tools.
- Understand basic networking concepts.
- Perform safe first-line troubleshooting.
- Know when to escalate a problem instead of making risky changes.
This guide focuses on practical Windows fundamentals and IT support. It is not an advanced Windows internals or malware-analysis manual.

## 2. Basic Computer Concepts
Hardware
Hardware is the physical part of a computer.
- CPU (Central Processing Unit): Executes instructions.
- RAM (Random Access Memory): Temporary working memory used by running programs.
- Storage (SSD/HDD): Keeps Windows, applications, and files when the computer is turned off.
- GPU: Processes graphics and visual output.
- Network adapter: Connects the computer to a network.
- Peripherals: Devices such as keyboards, mice, monitors, and printers.
Software
Software is a set of instructions that runs on a computer.
- Operating system: Windows.
- Applications: Browsers, office programs, and other user applications.
- Drivers: Software that allows Windows to communicate with hardware.
- Utilities: Tools used to configure, monitor, or repair the system.
RAM vs. storage
RAM is temporary and is used while programs are running. Storage keeps data long-term. A computer can have plenty of free storage but still run slowly because RAM or CPU resources are exhausted.

## 3. Windows Architecture — The Big Picture
Windows contains several cooperating components.
- User mode: Most applications run here with restrictions designed to isolate them from critical system operations.
- Kernel mode: Core operating-system components and many drivers run with highly privileged access.
- Windows kernel: Manages essential low-level operations, including scheduling and memory management.
- Device drivers: Enable communication with hardware.
- Windows APIs: Interfaces applications use to request operating-system functions.
- Services: Background components that provide particular functions.
- File system: Organizes data stored on disks.
A simplified example: an application requests that a document be printed; Windows coordinates the application, printing components, driver, and printer.
For beginner IT support, understand each component's role. Deep study of system calls, kernel internals, and memory structures can wait.

## 4. Windows Editions, Installation, and Updates
Common editions
Windows editions can differ in features and management capabilities. Windows Home is aimed mainly at personal use; Pro includes additional business-oriented features, which can include joining a domain or using certain remote-management capabilities. Exact features vary by Windows version and configuration.
Windows installation and activation
Windows may be installed from approved installation media. After installation, device drivers, updates, activation, user accounts, and security settings may need attention.
Activation verifies the Windows license status. Activation problems are not always the same as installation problems.
Windows Update
Windows Update delivers supported operating-system updates, including security fixes and reliability improvements.
Good practice:
- Install updates through supported Windows settings or organizational IT procedures.
- Save work before restarting.
- Check whether a restart is pending.
- If an update fails, record the error code and review the update history.
- Do not download system updates from unknown websites.
Drivers and compatibility
A missing or faulty driver can cause a device not to work correctly. Prefer Windows Update, the computer manufacturer's support page, or the device manufacturer's official source. Avoid third-party driver-download sites of uncertain reputation.

## 5. Users, Groups, and Sign-in
User accounts
A user account gives a person or service an identity on Windows.
Common account types:
- Local account: Exists on that Windows device.
- Microsoft account: Uses a Microsoft identity and may connect supported settings and services.
- Work or school account: May be managed by an organization.
- Service account: An identity used by a service or application.
Standard user vs. administrator
- Standard user: Intended for everyday work with limited system-changing privileges.
- Administrator: Can perform more system-level tasks, subject to Windows security controls and organizational policy.
Use the least privilege necessary. Do not make every user an administrator just to avoid diagnosing a permissions problem.
User Account Control (UAC)
UAC helps prevent unauthorized changes by prompting for approval or administrator credentials when an operation requires elevated privileges.
Groups
Groups make it easier to assign permissions to multiple users. For example, access can be granted to a group rather than separately to every employee.
Sign-in problems
Possible causes include an incorrect password, a locked account, a disconnected work network, a profile issue, or an account-management policy. Follow the organization's identity-verification and password-reset process; never ask users to reveal their passwords.

## 6. Files, Folders, Drives, and File Systems
Files and folders
A file stores data. A folder organizes files and other folders. A file extension often indicates the file type, such as .txt, .pdf, or .jpg, but an extension alone does not prove a file is safe.
Common Windows locations
- C:\Windows — Windows system files.
- C:\Program Files — commonly stores installed 64-bit applications.
- C:\Program Files (x86) — commonly stores 32-bit applications on 64-bit Windows.
- C:\Users — user profiles and personal folders.
- C:\Users\<username>\Desktop — the user's desktop files.
- C:\Users\<username>\Documents — documents.
- C:\Users\<username>\Downloads — downloaded files.
- %TEMP% — the current user's temporary-file location in many situations.
Do not delete unfamiliar files from Windows system directories.
Drives and partitions
A physical disk can contain one or more partitions. Windows assigns drive letters such as C: to many accessible volumes. A low-storage warning can affect updates, application performance, and the ability to save files.
File systems
- NTFS: Commonly used for Windows system and internal data volumes; supports permissions and other advanced features.
- FAT32: Widely compatible, but a single file cannot exceed 4 GiB.
- exFAT: Often used for removable storage and supports large files.
File attributes and hidden files
Files can have attributes such as read-only or hidden. Hidden does not mean protected or malicious. Change attributes only when you understand why they are set.

## 7. NTFS Permissions and Access
Permissions determine what a user or group can do with a file or folder.
Common permissions include:
- Read: View or read content.
- Write: Create or change data, depending on the permission and context.
- Modify: Read, write, and delete content, subject to effective permissions.
- Full Control: Broad control, including changing permissions, subject to the security context.
Permission inheritance
A folder can pass permissions to child files and folders. The final permissions a user receives can depend on inherited permissions, explicit permissions, group membership, and other access rules.
ACLs
An Access Control List (ACL) contains access rules for an object. When a user cannot open a file, investigate the path, account, group membership, and effective permissions before changing access.
Safe support practice
- Confirm the user should have access.
- Grant the minimum access required.
- Avoid broad permissions such as giving everyone Full Control.
- Follow company policy for shared folders and sensitive data.

## 8. Processes, Threads, CPU, and Memory
Process
A process is a running instance of a program. It has a process identifier (PID), resources, and a virtual address space.
Thread
A thread is a sequence of execution within a process. A process can contain multiple threads.
Useful terms
- PID: Process identifier.
- CPU usage: The share of processor capacity being used.
- Memory usage: RAM currently used or attributed to a process.
- Parent process: A process that created another process.
- Virtual memory: An address-space and memory-management abstraction used by Windows.
- Handle: A reference used by a process to access a system object.
- Security token: Information Windows uses to represent a process or user's security identity and privileges.
For everyday support, focus on identifying resource usage and application hangs. Detailed analysis of handles, tokens, and memory structures is advanced material.
Safe troubleshooting
Use Task Manager to check whether CPU, memory, disk, or network activity is unusually high. Do not end unfamiliar system processes just because their names look unusual. Save work before closing an unresponsive application when possible.

## 9. Windows Services
A service is a background component that provides a function for Windows or an application. Services may run without a normal desktop window.
Examples include:
- Windows Update: Supports update operations.
- Print Spooler: Manages print jobs.
- DHCP Client: Supports obtaining network configuration through DHCP.
- Windows Audio: Supports Windows audio functionality.
Service states
A service can be Running, Stopped, or in a transition state such as Starting or Stopping.
Startup types
Depending on the service and Windows version, startup configuration may include:
- Automatic: Intended to start automatically.
- Automatic (Delayed Start): Starts automatically after other startup activity.
- Manual: Can be started when needed, including by another component.
- Disabled: Cannot normally be started until its configuration is changed.
Not every service should be running all the time. Do not change a service's startup type without understanding its role and the impact.
Example
If printing fails, check the printer connection, selected printer, queue, driver, and Print Spooler service. Restarting a service may help in some cases, but it is not a universal fix.

## 10. Windows Registry
The Registry is a hierarchical database that stores configuration information for Windows, hardware, users, and applications.
Common root keys include:
- HKEY_LOCAL_MACHINE (HKLM) — machine-wide configuration.
- HKEY_CURRENT_USER (HKCU) — configuration for the current user.
- HKEY_CLASSES_ROOT (HKCR) — file associations and class-registration information.
The Registry can be viewed with Registry Editor (regedit).
Safety: Incorrect edits can cause application or system problems. Before making a change, verify the exact key and value, document the original setting, follow approved procedures, and make a suitable backup where appropriate. Do not use random Registry tweaks from unknown sources.

## 11. Boot Process and Sign-in — Basic Overview
The boot process starts the computer and loads Windows. In simplified terms:
1. Firmware initializes hardware and selects a boot device.
2. Windows Boot Manager starts the Windows loading process.
3. Windows loads essential system components and drivers.
4. Windows reaches the sign-in screen.
5. After sign-in, the user environment and startup applications load.
Problems may occur at different stages: no power, no display, a boot-device error, repeated restarts, a blue screen, or a sign-in failure.
Before advanced recovery actions, record the exact error and determine whether the issue began after an update, hardware change, or new driver. Use recovery tools according to the device owner's or organization's procedures.

## 12. Storage, Disks, and Device Management
Storage basics
A disk may contain multiple partitions or volumes. Common storage problems include:
- Low free space.
- A disconnected external drive.
- File-system errors.
- A disk that is not detected.
- A failing storage device.
Back up important data before attempting repairs that may affect a disk.
Device Manager
Device Manager shows detected hardware and its driver status. A warning symbol can indicate a device or driver problem, but the exact status and error code should be checked.
Typical first steps:
- Check physical connections and power.
- Check the device status and error code.
- Install supported driver updates from trusted sources.
- Restart if appropriate.
- Escalate suspected hardware failure.
Do not uninstall a device or driver casually, especially if it is required for network access or remote support.

## 13. Built-in Windows Tools
Task Manager
Useful for:
- Checking running applications and processes.
- Reviewing CPU, memory, disk, and network usage.
- Closing a frozen application.
- Reviewing startup applications.
Settings
Used to manage display, sound, network, accounts, Windows Update, installed applications, and many other settings.
Control Panel
Still provides access to some traditional configuration tools, depending on Windows version.
File Explorer
Used to browse files, folders, drives, and network locations.
Device Manager
Used to inspect hardware devices and drivers.
Services console
Opened with services.msc. Used to inspect service status and configuration.
Event Viewer
Opened with eventvwr.msc. Shows logs from Windows and applications. Logs may contain useful timestamps, event IDs, sources, and error details. An error entry does not automatically mean it caused the problem; correlate it with the time and symptoms.
Resource Monitor
Provides more detailed information about CPU, memory, disk, and network activity.
Disk Management
Opened with diskmgmt.msc. Used to inspect disks, partitions, and volumes. Avoid formatting, deleting, or resizing partitions unless the impact is understood and data is backed up.
System Information
Opened with msinfo32. Displays details about hardware and the Windows environment.
System Configuration
Opened with msconfig. Can be useful in specific diagnostic scenarios, but changing boot settings without a clear plan can make the system harder to start.

## 14. Networking Fundamentals
What is a network?
A network allows devices to communicate and share resources, such as internet access, printers, and files.
Important concepts
- IP address: Identifies a network interface on an IP network.
- Subnet mask / prefix: Defines the network portion of an IP configuration.
- Default gateway: The router or next hop used to reach other networks.
- DNS: Resolves domain names, such as example.com, to IP addresses.
- DHCP: Automatically provides network configuration to clients.
- MAC address: A link-layer address associated with a network interface.
- TCP: A transport protocol that provides reliable, ordered delivery.
- UDP: A transport protocol with lower overhead that does not provide TCP's delivery guarantees.
- Port: A number used to identify a service or application endpoint.
- Firewall: Filters network traffic according to rules.
Common network symptoms
- No network connection.
- Connected to Wi-Fi but no internet access.
- One website does not load.
- A network drive or printer is unavailable.
- A connection fails because a service or port is blocked.
Basic diagnostic sequence
1. Check Wi-Fi, Ethernet, airplane mode, and physical connections.
2. Check whether other devices have the same problem.
3. Inspect the IP configuration.
4. Test connectivity to the gateway and an external IP address when appropriate.
5. Test DNS resolution.
6. Check VPN, proxy, firewall, and organizational policies.
7. Record the results before making changes.
A single failed ping does not prove the internet is down; some devices and networks block ICMP traffic.

## 15. Basic PowerShell and Command-Line Awareness
PowerShell is a command-line shell and scripting language for managing Windows. Command Prompt (cmd.exe) is another command-line environment.
This section introduces their role; detailed command syntax belongs in a separate PowerShell reference.
Examples of common PowerShell commands:
- Get-Process — lists processes.
- Get-Service — lists services.
- Get-ChildItem — lists files and folders.
- Get-NetIPConfiguration — shows network configuration.
- Test-NetConnection — tests selected network connectivity.
- Get-Help Get-Service — displays help for a command.
Examples of common Command Prompt commands:
- ipconfig — displays or manages IP configuration.
- ping — tests ICMP reachability.
- nslookup — queries DNS.
- tracert — traces a network path.
- whoami — displays the current identity.
Use elevated terminals only when necessary. Read a command's help and understand its effect before running commands that delete files, change permissions, stop services, or alter network settings.

## 16. Windows Security Fundamentals
Microsoft Defender and antivirus protection
Microsoft Defender Antivirus provides malware protection on supported Windows configurations. Check protection status through Windows Security or approved organizational tools.
Windows Firewall
Windows Firewall filters network traffic according to configured rules. Disabling it to fix connectivity is not a safe default troubleshooting step.
Windows Update
Security updates help address vulnerabilities. Keep devices updated according to the organization's policy.
Least privilege
Users and applications should have only the permissions needed for their tasks.
Screen lock and account safety
Use appropriate sign-in protections, lock unattended devices, and follow approved password and multi-factor authentication practices.
Backups
Keep important data backed up according to its value and sensitivity. A backup should be recoverable, not merely present.
Safe downloads
Use trusted official sources. Do not run unknown attachments, scripts, or executables simply because someone says they are required.

## 17. Applications, Installation, and Startup
Installing and removing applications
Use trusted installers, Microsoft Store where appropriate, or an organization's software-management system. Confirm application compatibility and licensing.
Startup applications
Some applications start automatically when a user signs in. Too many startup applications can slow sign-in. Review them through Task Manager or Settings, but do not disable unknown security or business applications without checking their purpose.
Application troubleshooting
When an application fails:
1. Record the exact error.
2. Check whether the issue affects one user or multiple users.
3. Restart the application and, if appropriate, the computer.
4. Check available updates and system requirements.
5. Check relevant Event Viewer entries.
6. Use the application's repair or reinstall procedure if approved.
7. Protect user data and settings before reinstalling.

## 18. Backup, Restore, and Recovery
Backup
A backup is a separate copy of important data that can be restored after accidental deletion, hardware failure, or another incident. Follow organizational rules for approved storage and sensitive information.
Restore points
System Protection can create restore points containing selected system settings and configuration information. A restore point is not a substitute for a personal-file backup.
Recovery options
Depending on the Windows version and device, recovery options may include Startup Repair, System Restore, uninstalling a recent update, or Reset this PC.
Before recovery:
- Record the symptoms and error messages.
- Check whether important files are backed up.
- Confirm whether BitLocker or other recovery credentials may be needed.
- Get approval when working on an organization's device.
- Understand that reset or reinstall options may remove applications, settings, or files.

## 19. Troubleshooting Methodology
Good troubleshooting is a repeatable process rather than random trial and error.
Step 1: Identify the problem
Ask:
- What exactly does not work?
- What is the full error message?
- When did it start?
- Did anything change recently?
- Does it affect one application, one user, or multiple devices?
Step 2: Check the basics
Check power, cables, Wi-Fi, available disk space, sign-in status, and obvious configuration issues.
Step 3: Reproduce and narrow the problem
Try to determine whether the issue is consistent. Compare with another user, application, device, or network only when safe and appropriate.
Step 4: Gather evidence
Use relevant tools such as Task Manager, Event Viewer, Device Manager, Settings, or PowerShell. Record exact errors, timestamps, and test results.
Step 5: Form a hypothesis
Choose a likely cause based on evidence. Change one thing at a time when practical so that the result is interpretable.
Step 6: Apply a safe fix
Use an approved, reversible change where possible. Avoid disabling security controls, deleting system files, or changing the Registry without a justified plan.
Step 7: Verify
Confirm the original task works, not just that an error disappeared. Check that the fix did not create another problem.
Step 8: Document
Record the symptom, cause if known, tests performed, fix, result, and any follow-up actions. Escalate when the issue exceeds your permissions or knowledge.

## 20. Common Beginner Troubleshooting Scenarios
Scenario A: The computer is slow
1. Check Task Manager for CPU, memory, and disk usage.
2. Identify applications consuming unusual resources.
3. Check free storage and pending restarts.
4. Review recent changes and startup applications.
5. Check for relevant errors or hardware warnings.
6. Verify performance after a safe change.
Do not assume every slow computer has a virus.
Scenario B: The internet does not work
1. Check Wi-Fi or Ethernet and airplane mode.
2. See whether other devices are affected.
3. Inspect IP settings.
4. Test gateway connectivity where appropriate.
5. Test DNS resolution.
6. Check VPN or proxy settings and organizational restrictions.
7. Record findings before resetting network settings.
Scenario C: A printer does not print
1. Check power, connection, paper, and error lights.
2. Confirm the correct printer is selected.
3. Check the print queue.
4. Check whether the printer is reachable.
5. Inspect the Print Spooler service if relevant.
6. Check the driver and test print after the fix.
Scenario D: An application will not open
1. Capture the exact error.
2. Check whether the application is already running.
3. Restart the application and check for updates.
4. Check available disk space and permissions.
5. Review relevant event logs.
6. Repair or reinstall only when appropriate and after protecting user data.
Scenario E: A user cannot access a file
1. Confirm the correct file path.
2. Check whether the file or network location is available.
3. Confirm the user's identity and expected access.
4. Review permissions and group membership.
5. Check whether the file is locked, encrypted, or restricted by policy.
6. Grant only approved, necessary access.
Scenario F: A USB device is not detected
1. Check the cable, port, power, and device.
2. Try another known-good port or cable when appropriate.
3. Check Device Manager and the device status.
4. Check for supported driver updates.
5. Consider hardware failure if the device is not detected elsewhere.
Scenario G: Windows Update fails
1. Record the error code.
2. Check internet access and available storage.
3. Restart if a restart is pending.
4. Review update history and relevant logs.
5. Follow official Microsoft guidance for the specific error.
6. Avoid deleting system folders or using untrusted repair tools.

## 21. Event Logs and Documentation
Event Viewer records events from Windows components and applications. Useful details may include:
- Date and time.
- Event source.
- Event ID.
- Severity.
- Error message.
A warning or error is not automatically the root cause. Compare its timestamp with when the problem occurred and look for supporting evidence.
Simple support-note template
Issue:
Affected user/device:
Date and time:
Symptoms and exact error:
Recent changes:
Checks performed:
Findings:
Action taken:
Verification result:
Escalation or follow-up:
Avoid putting passwords, recovery keys, personal information, or other secrets in public notes or GitHub repositories.

## 22. Practical Learning Checklist
Use this checklist to confirm your understanding.
- [ ] Explain what an operating system does.
- [ ] Identify CPU, RAM, storage, and network adapter roles.
- [ ] Explain the difference between a process and a service.
- [ ] Explain standard users, administrators, and UAC.
- [ ] Understand basic NTFS permissions and inheritance.
- [ ] Recognize important Windows directories.
- [ ] Explain what the Registry is and why edits are risky.
- [ ] Open and use Task Manager.
- [ ] Open Device Manager and interpret a device warning.
- [ ] Open Event Viewer and locate events around a problem's timestamp.
- [ ] Explain IP address, gateway, DNS, and DHCP.
- [ ] Use basic read-only commands to gather information.
- [ ] Follow a structured troubleshooting process.
- [ ] Document a problem and verify a fix.
- [ ] Identify when to stop and escalate a problem.

## 23. Recommended Official References
- Microsoft Support
- Microsoft Learn
- Windows client documentation
- Windows Security documentation
- PowerShell documentation
Prefer current official documentation when following repair instructions because steps can vary by Windows version.
Conclusion
Windows fundamentals are the foundation of practical IT support. The goal is not to memorize every internal detail, but to understand how the system is organized, use its built-in tools safely, collect evidence, diagnose likely causes, apply controlled fixes, and verify the outcome.
A useful next step is to keep this document as the conceptual reference, maintain a separate PowerShell command reference, and record real troubleshooting scenarios in a dedicated troubleshooting document.
