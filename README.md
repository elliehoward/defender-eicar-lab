\# Microsoft Defender EICAR Detection Lab



\## Overview

This lab demonstrates how Microsoft Defender detects the EICAR Standard Antivirus Test File, a safe, industry‑approved string used to verify antivirus functionality. You will create the EICAR file, observe Defender’s real‑time or on‑access detection, and collect evidence of the detection event.



\## Objectives

\- Create a valid EICAR test file  

\- Save it in a monitored directory  

\- Trigger Microsoft Defender detection  

\- Capture logs and screenshots  

\- Understand real‑time vs on‑access scanning behavior  



\---



\## Prerequisites

\- Windows 10 or Windows 11  

\- Microsoft Defender Antivirus enabled  

\- Real-time protection turned on  

\- No third‑party antivirus installed  

\- Ability to run PowerShell  



\---



\## Lab Steps



\### 1. Open Notepad

Use \*\*Notepad\*\* only. Other editors may add formatting or encoding that breaks the EICAR signature.



\### 2. Paste the EICAR Test String

Paste the following \*\*exact\*\* string with no extra spaces or newlines:

```

X5O!P%@AP\[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H\*

```



\### 3. Save the File as ANSI

1\. Go to \*\*File → Save As\*\*  

2\. Change \*\*Encoding\*\* to \*\*ANSI\*\*  

3\. Save the file as:  

```

eicar.com

```

4\. Save it to a monitored folder such as \*\*Downloads\*\* or \*\*Desktop\*\*



Saving as ANSI ensures the file is stored as plain ASCII, which is required for Defender to recognize the EICAR signature.



\### 4. Observe Defender’s Behavior

Microsoft Defender may react in one of two ways:



\#### \*\*Real-Time Detection (on-write)\*\*

Defender immediately removes or quarantines the file as soon as it is saved.



\#### \*\*On-Access Detection (on-open)\*\*

Defender blocks and removes the file when you attempt to open it.  

This still demonstrates real-time protection.



\### 5. Optional: Trigger a Manual Scan

Right-click the file → \*\*Scan with Microsoft Defender\*\*  

This guarantees a visible detection event for screenshots.



\---



\## Evidence Collection



\### 1. Protection History

Navigate to:  

\*\*Windows Security → Virus \& threat protection → Protection history\*\*  

Look for entries referencing \*\*EICAR-Test-File\*\*.



\### 2. PowerShell Logs

Run:



```powershell

Get-MpThreatDetection

```

This displays detection events, timestamps, and actions taken.



\### 3. Quarantine Folder

Defender stores quarantined items here:

```

C:\\ProgramData\\Microsoft\\Windows Defender\\Quarantine

```

Files appear encrypted and renamed, but timestamps will match the detection event.



\## Expected Results

\- The EICAR file is blocked, removed, or quarantined



\- A detection entry appears in Protection History



\- PowerShell logs show an EICAR detection event



\- Screenshots document the detection process



\## Notes

\- Saving the file with UTF‑8 encoding may prevent detection due to the presence of a BOM (Byte Order Mark).



\- On-access detection is normal and still demonstrates Defender’s real-time protection.



\- Manual scanning is acceptable for lab documentation and screenshots.

