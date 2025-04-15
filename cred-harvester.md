
# Python: Credential Harvester Detector

**Objective**: Create a Python script to analyze a PCAP file for credential harvesting attempts and flag suspicious activity.

**Difficulty**: 8/9  
**Time**: 40 minutes

## Steps

1. **Setup**  
   - Import the required library:  
     ```python
     import scapy.all as scapy
     ```

2. **Load PCAP**  
   - Read the PCAP file into memory:  
     ```python
     packets = scapy.rdpcap('traffic.pcap')
     ```

3. **Filter POST**  
   - Iterate through packets to find HTTP POST requests:  
     ```python
     for p in packets:
         if p.haslayer(scapy.Raw) and 'POST' in p[scapy.Raw].load.decode(errors='ignore'):
             # Process packet
     ```

4. **Extract**  
   - Search the payload for credentials (e.g., `user`, `pass`):  
     ```python
     payload = p[scapy.Raw].load.decode(errors='ignore')
     if 'user' in payload.lower() or 'pass' in payload.lower():
         # Extract relevant data
     ```

5. **Flag**  
   - Print the source IP and suspicious payload if credentials are found:  
     ```python
     print(f"Suspicious activity from {p[scapy.IP].src}: {payload}")
     ```

6. **Test**  
   - Run the script on a sample PCAP containing a login attempt to verify it flags credential harvesting.

## Solution

The script flags suspicious activity, e.g., `192.168.1.10` sending credentials in a POST request, identifying potential credential harvesting.
