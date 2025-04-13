
# Python: Network Scanner for Open Ports

**Objective**: Create a Python script to scan a subnet for open ports and log the results to a file.

**Difficulty**: 7/9  
**Time**: 35 minutes

## Steps

1. **Setup**  
   - Import the required library:  
     ```python
     import socket
     ```

2. **Scan**  
   - Define a function to check if a port is open on a given IP:  
     ```python
     def scan(ip, port):
         s = socket.socket()
         s.settimeout(1)
         return s.connect_ex((ip, port)) == 0
     ```

3. **Loop**  
   - Iterate through IPs in the subnet and a list of common ports, logging open ports:  
     ```python
     for i in range(1, 255):
         ip = f'192.168.1.{i}'
         for p in [22, 80, 443]:
             if scan(ip, p):
                 print(f'{ip}:{p} open')
     ```

4. **Log**  
   - Write scan results to a file (`scan.log`):  
     ```python
     with open('scan.log', 'a') as f:
         for i in range(1, 255):
             ip = f'192.168.1.{i}'
             for p in [22, 80, 443]:
                 if scan(ip, p):
                     f.write(f'{ip}:{p} open\n')
     ```

5. **Test**  
   - Run the script on a lab network to verify it detects and logs open ports correctly.

## Solution

The script scans the subnet `192.168.1.0/24` for open ports (22, 80, 443) and logs results to `scan.log`, e.g., `192.168.1.10:80 open`.
