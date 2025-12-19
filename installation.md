# Malware Analysis Lab Setup

This project uses a secure, isolated malware analysis lab to study **WannaCry (Wannacry.exe)** safely.

## Environment
- VMware Workstation Pro
- Windows 10 Pro x64 (isolated)
- Flare VM installed via Mandiant script

## Setup Steps
1. Mount Windows ISO on on the workstation vmware and install offline using `OOBE\BYPASSNRO`without requiring a microsoft account and connecting to the internet.
2. Take a snapshot of the clean system. 
3. Disable Windows Defender using [Windows Defender Remover](https://github.com/ionuttbara/windows-defender-remover).
4. Configure network settings on VM: start with Host-only, then NAT for internet access.
5. Download and install Flare VM via the official mandiant script:
```powershell
(New-Object Net.WebClient).DownloadFile('https://raw.githubusercontent.com/mandiant/flare-vm/main/install.ps1',"$([Environment]::GetFolderPath("Desktop"))\install.ps1")

Take a snapshot after Flare VM setup (lab ready for malware analysis).
This ensures a controlled, revertible environment for safe malware handling.
