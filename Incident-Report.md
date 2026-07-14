\# Incident Report: EICAR Test File Detection



\## Summary

On July 13, 2026, Microsoft Defender detected and quarantined the EICAR Standard Antivirus Test File during a controlled security lab exercise. The file was created intentionally to validate Defender’s real-time and on-access protection capabilities. Detection occurred when the file was accessed, and the threat was successfully quarantined and later removed by user action.



\---



\## Incident Details



\### Incident Type

Malware Detection (EICAR Test File)



\### Date \& Time

July 13, 2026  

Initial Detection: 4:39 PM CDT



\### Affected System

\- \*\*User:\*\* ellih  

\- \*\*Device:\*\* Windows 10/11 workstation  

\- \*\*File Path:\*\* `C:\\Users\\ellih\\Downloads\\eicar.com`



\### Threat Identified

\- \*\*Name:\*\* Virus:DOS/EICAR\_Test\_File  

\- \*\*Severity:\*\* Severe  

\- \*\*Classification:\*\* EICAR Standard Antivirus Test File (non-malicious test string)



\---



\## Timeline of Events



\### 1. File Creation

The EICAR test string was created in Notepad and saved as `eicar.com`.  

Initial attempts saved the file using UTF‑8 encoding, which prevented immediate detection due to the presence of a Byte Order Mark (BOM).



\### 2. On-Access Detection

When the file was opened, Microsoft Defender performed an on-access scan.  

Defender blocked the file from opening and immediately quarantined it.



\### 3. User Review

The detection entry appeared in \*\*Windows Security → Protection history\*\*, showing:

\- Threat name  

\- Severity  

\- File path  

\- Action taken (Quarantined)



A screenshot was captured documenting this detection.



\### 4. Removal Action

The user clicked the \*\*Action\*\* button within Protection History and selected \*\*Remove\*\*.  

Defender confirmed the removal of the quarantined file.  

A second screenshot was captured showing the removal confirmation.



\### 5. PowerShell Verification

Running `Get-MpThreatDetection` returned an entry confirming:

\- The EICAR test file was detected  

\- The action taken was quarantine  

\- The timestamp matched the GUI evidence  



\---



\## Impact Assessment

This was a controlled test and posed \*\*no risk\*\* to the system.  

The EICAR file is a safe, industry-standard antivirus test string and does not contain malicious code.



\---



\## Containment and Eradication

\- Microsoft Defender automatically quarantined the file upon detection.  

\- The user manually removed the quarantined item using the Windows Security interface.  

\- No additional remediation was required.



\---



\## Lessons Learned

\- Encoding matters: UTF‑8 with BOM prevented initial detection, demonstrating how signature-based antivirus engines rely on exact byte patterns.  

\- Defender’s on-access scanning effectively intercepted the file when opened.  

\- Manual scanning provides clear, reproducible evidence for documentation.  

\- Protection History and PowerShell logs offer reliable verification

