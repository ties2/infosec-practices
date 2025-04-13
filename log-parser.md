
# Python: Log Parser for IOCs

**Objective**: Create a Python script to parse a syslog file for Indicators of Compromise (IOCs), such as IPs and domains, and output them to a CSV file.

**Difficulty**: 6/9  
**Time**: 25 minutes

## Steps

1. **Script Setup**  
   - Import required libraries:  
     ```python
     import re
     import csv
     ```

2. **Read Log**  
   - Open and read the syslog file:  
     ```python
     with open('syslog', 'r') as f:
         lines = f.readlines()
     ```

3. **Extract IOCs**  
   - Use regex to find IPs and domains in each line:  
     ```python
     ips = re.findall(r'\d+\.\d+\.\d+\.\d+', line)
     domains = re.findall(r'[a-zA-Z0-9-]+\.[a-z]{2,}', line)
     ```

4. **Write CSV**  
   - Create a CSV file with headers for IPs and domains:  
     ```python
     with open('iocs.csv', 'w') as f:
         writer = csv.writer(f)
         writer.writerow(['IP', 'Domain'])
     ```

5. **Loop**  
   - Iterate through log lines, extract IOCs, and append to the CSV:  
     ```python
     with open('iocs.csv', 'a') as f:
         writer = csv.writer(f)
         for line in lines:
             ips = re.findall(r'\d+\.\d+\.\d+\.\d+', line)
             domains = re.findall(r'[a-zA-Z0-9-]+\.[a-z]{2,}', line)
             for ip, domain in zip(ips, domains):
                 writer.writerow([ip, domain])
     ```

6. **Test**  
   - Run the script on a sample syslog file and verify the `iocs.csv` output contains the expected IPs and domains.

## Solution

The Python script successfully parses the syslog file and outputs a CSV (`iocs.csv`) containing extracted IPs and domains as Indicators of Compromise.
