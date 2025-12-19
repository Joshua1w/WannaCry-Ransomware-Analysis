# WannaCry-Ransomware-Analysis
Hands-on malware analysis of WannaCry (Wannacry.exe) in a secure Flare VM lab. Conducted static analysis with DIE and IDA Pro, and dynamic sandbox analysis with ANY.RUN. Findings include file enumeration, encryption, persistence, and ransom note behavior, correlated to MITRE ATT&amp;CK for SOC-aligned insights.

WannaCry Malware Analysis – Technical Walkthrough

This repository documents a complete, hands-on malware analysis of WannaCry (Wannacry.exe), carried out to understand the malware’s structure, behavior, and operational impact using professional static and dynamic analysis techniques. The work reflects a realistic SOC and malware research workflow, emphasizing safe lab design, disciplined analysis, and evidence-based conclusions.
The analysis was performed strictly for educational and defensive purposes, using isolated virtual environments and controlled sandbox platforms.

Analysis Environment and Lab Preparation
The analysis began with the construction of a dedicated malware analysis laboratory using VMware Workstation Pro and a Windows 10 Pro x64 virtual machine. The operating system was installed offline to avoid unintended network communication during setup. System snapshots were taken at multiple stages to ensure repeatability and safe rollback throughout the project.
To allow effective malware execution and analysis, built-in Windows security controls were intentionally disabled. Due to limitations encountered with manual configuration, Windows Defender and related protections were fully removed using the ionuttbara Windows Defender Remover. Windows Update was also disabled to prevent interference during analysis. These actions were deliberate and confined strictly to the isolated virtual environment.
Network configuration was carefully controlled. The virtual machine operated primarily in host-only mode to maintain isolation. NAT networking was enabled temporarily only when required for tool installation and controlled internet access. No malware samples were executed on unrestricted or production networks.

Toolchain and Methodology
The analysis followed a layered approach, beginning with static analysis to understand the malware without execution, followed by dynamic analysis to observe real runtime behavior.
Static analysis was conducted using Detect It Easy (DIE) and IDA Pro. DIE was used to identify the file format, architecture, entropy, and compiler characteristics. IDA Pro was then used to disassemble the binary, analyze control flow, inspect imported APIs, and examine strings and functions to infer program logic.
Dynamic analysis was performed using the ANY.RUN online sandbox, allowing safe observation of the malware’s execution, process behavior, file system interaction, registry modifications, and user-facing impact without risking local compromise.

Static Analysis Findings
Static analysis confirmed that WannaCry is a 32-bit Windows PE executable targeting the x86 architecture. Examination of imports and disassembled code revealed heavy use of standard Windows API functions related to file handling, directory traversal, permission modification, and process execution.
String analysis and function inspection indicated logic for enumerating user directories, identifying target file paths, and manipulating filenames and extensions. References to known WannaCry components such as @WanaDecryptor@.exe and ransom-related artifacts were present within the binary. Control flow analysis showed structured routines responsible for locating files, applying permission changes, and invoking additional scripts and executables.
While static analysis provided insight into the malware’s capabilities and intent, it could not conclusively demonstrate the full execution order or real-world impact, making dynamic analysis essential for confirmation.

Dynamic Analysis Observations
Dynamic execution in ANY.RUN validated and expanded upon the static findings. Upon execution, WannaCry enumerated directories recursively, targeting user-accessible files across the system. Files were encrypted and renamed using known WannaCry extensions, and ransom notes were dropped into affected directories.
The malware executed supporting scripts and launched the ransom interface, confirming its persistence and impact behavior. File permissions and attributes were modified to prevent user access and complicate recovery. These actions collectively demonstrated a complete ransomware lifecycle, from execution to encryption and user notification.
Dynamic analysis conclusively showed how the malware behaves in a live environment, confirming that the capabilities identified statically translate directly into real-world damage.

Static vs Dynamic Analysis Perspective
This project highlights the complementary nature of static and dynamic analysis. Static analysis was essential for understanding how WannaCry is built, what APIs it relies on, and how its internal logic is structured. Dynamic analysis was necessary to observe actual execution, verify encryption behavior, and capture artifacts generated at runtime.
Neither approach alone is sufficient for professional malware analysis. Together, they provide a complete understanding of both intent and impact.

MITRE ATT&CK Alignment
Observed behaviors were mapped to the MITRE ATT&CK framework to contextualize WannaCry’s techniques within an industry-standard threat model. The malware demonstrated techniques spanning execution, persistence, discovery, defense evasion, collection, and impact, including user execution, scripting via command interpreters, file discovery, local data encryption, and internal defacement through ransom messaging.
Mapping these behaviors to ATT&CK allows defenders to translate analysis findings into detection rules, response strategies, and preventative controls within SOC environments.

Defensive and SOC Relevance
The analysis conducted in this repository reflects tasks commonly performed by SOC analysts and malware researchers. The findings can be directly applied to developing SIEM detection logic, EDR behavioral alerts, and incident response playbooks for ransomware threats.
Understanding WannaCry at both the code and behavior level strengthens defensive posture by enabling earlier detection, faster containment, and more effective remediation of similar ransomware families.

Ethical and Legal Disclaimer
All analysis was conducted in isolated environments or controlled online sandboxes. No malware was executed on production systems or uncontrolled networks. This project is intended solely for educational and defensive research purposes.

Author:
Joshua Adeleye
Cybersecurity Analyst
Focus: Threat Detection, Malware Analysis, Blue Team Operations


[Malware analysis Wannacry.exe Malicious activity _ ANY.RUN - Malware Sandbox Online.pdf](https://github.com/user-attachments/files/24257805/Malware.analysis.Wannacry.exe.Malicious.activity._.ANY.RUN.-.Malware.Sandbox.Online.pdf)


<img width="483" height="371" alt="Analysing Ransomware wannacry" src="https://github.com/user-attachments/assets/2d280c1a-a98d-4d2f-9a81-7795f216bfd4" />


<img width="960" height="440" alt="Dynamic Malware Analysis using Any run" src="https://github.com/user-attachments/assets/32d73320-1b71-4406-a29e-a133d7129461" />


<img width="960" height="539" alt="Host only set up " src="https://github.com/user-attachments/assets/a60cba78-6832-49d7-9f9d-a35b4080729e" />
