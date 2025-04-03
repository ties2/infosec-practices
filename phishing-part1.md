# Phishing Email Analysis - Part 1

## Overview
- **Difficulty:** 5/9
- **Time:** 60 minutes
- **Task:** Analyze a suspicious email header and attachment provided in a `.eml` file. Identify indicators of compromise (IOCs) such as malicious URLs or spoofed sender details. Document findings and suggest initial containment steps.

## Prerequisites
- Sandbox VM (e.g., VirtualBox with Windows/Linux)
- Tools: Text editor, `grep`, VirusTotal API (optional)

## Steps
1. **Open the .eml File**  
   Use a text editor or email client (e.g., Thunderbird) in a sandbox to safely view the email.

2. **Analyze Headers**  
   Examine `From`, `Reply-To`, `Received`, and `X-` headers for inconsistencies (e.g., domain mismatch like `admin@company.com` vs. `Received: evil.com`).

3. **Extract IOCs**  
   Use `grep` or regex (e.g., `http[s]?://[^\s]+`) to pull out URLs or IPs from the body and headers.

4. **Inspect Attachment**  
   If it’s a PDF or DOC, use `strings` or `exiftool` to check for embedded scripts/URLs without opening it.

5. **Verify Malice**  
   Cross-check IOCs against threat intelligence (e.g., VirusTotal).

6. **Document**  
   Create a report (e.g., in Markdown) noting sender, URLs, IPs, and attachment type.

7. **Containment**  
   Suggest blocking sender domain/IPs at the email gateway and quarantining the email.

## Solution
- **Findings:** Spoofed `From` header (`admin@company.com`) and a malicious URL (`http://fake-login.com`).
- **Action:** Recommend blocking the domain and alerting users.

## Notes
- Test in a sandbox to avoid accidental execution of malicious content.
- Use `curl` or `wget` in a controlled environment if verifying URLs.
