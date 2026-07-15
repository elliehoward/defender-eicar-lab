# Findings



## Overview

This document summarizes the results of the Microsoft Defender EICAR Detection Lab. It includes observed behavior, detection events, and evidence collected during testing.



---



## EICAR File Creation

I created the EICAR test file using Notepad and saved it as `eicar.com` with **ANSI encoding** to ensure the file matched the exact ASCII signature required for detection.



The EICAR test string used:



```

X5O!P%@AP\[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H\*

```



---



## Observed Defender Behavior



### Initial Save Behavior

- When the file was saved as **UTF‑8**, Microsoft Defender did **not** immediately detect or remove it.

- This occurred because UTF‑8 encoding adds a **Byte Order Mark (BOM)**, altering the signature and preventing detection.



### On-Access Detection

- When attempting to reopen the file, Microsoft Defender performed an **on-access scan**.

- Defender blocked the file from opening and displayed an error indicating the file contained a virus.

- Immediately after the block, the file was quarantined.



This confirms that real-time protection was functioning, even though detection occurred on-access rather than on-write.



### ANSI Save Behavior

- After recreating the file and saving it as **ANSI**, Defender recognized the EICAR signature correctly.

- The file remained visible until manually scanned.

- Right-clicking the file and selecting \*\*Scan with Microsoft Defender\*\* triggered an immediate detection event.



---



## Evidence Collection



### 1. Protection History (Detection Event)

Microsoft Defender successfully detected the EICAR test file and quarantined it.  

In the Windows Security **Protection history**, the entry displayed:



- **Threat name:** Virus:DOS/EICAR\_Test\_File  

- **Action:** Quarantined  

- **Severity:** Severe  

- **Affected item:** `C:\Users\ellih\Downloads\eicar.com`  

- **Timestamp:** Matching the moment the file was opened or scanned  



A screenshot was captured showing the full detection entry in Protection History.



### 2. Removal Action (User-Initiated)

After reviewing the detection entry, I clicked the **Action** button within Protection History.  



Defender provided the option to **Remove** the quarantined file.  

I selected this option, and Defender confirmed the removal.



A second screenshot was captured showing the removal confirmation, demonstrating that the quarantined EICAR file was successfully deleted from the system.



### 3. PowerShell Verification

To further validate the detection, I ran:



```powershell

Get-MpThreatDetection

```

The output included an entry for EICAR-Test-File, confirming:



- The threat was detected



- The action taken was quarantine



- The detection timestamp aligned with the Protection History entry



- This provides command-line evidence supporting the GUI-based detection.



---

## Summary of Findings

- Defender detected and quarantined the EICAR test file



- Protection History clearly documented the threat



- The user-initiated removal action was completed and captured



- PowerShell logs confirmed the detection event



Together, these artifacts demonstrate that Microsoft Defender’s real-time and on-access protection mechanisms functioned as expected.



---

## Conclusion

The lab confirmed that Microsoft Defender’s real-time protection is functioning as expected. Both on-access and manual scans successfully detected and removed the EICAR test file. Encoding played a significant role in detection behavior, demonstrating how signature-based antivirus engines rely on exact byte patterns.



