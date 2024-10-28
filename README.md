# Simple Port Scanner in Python 🔍

This repository walks you through creating a Simple Port Scanner using Python. A port scanner is a tool that helps check which ports are open on a target host. Open ports can give insights into what services are running, which is useful for testing and auditing networks.

> **Disclaimer**: This port scanner is intended for educational purposes. Only scan systems you have permission to test.

---

## Prerequisites

1. **Python 3.6+**: Make sure Python is installed. If not, you can download it from [python.org](https://www.python.org/downloads/).
2. **Basic understanding of networking**: Knowing how ports and IP addresses work will be helpful.
3. **Permission**: Ensure you have permission to scan the target machine.

## Step 1: Create a New Python File

Clone or download this repository, or open your terminal and create a new Python file:

```bash
mkdir SimplePortScanner
cd SimplePortScanner
touch port_scanner.py
```
## Step 2: Import the Required Libraries
For this project, we’ll use Python's socket library, which is built-in and lets us create connections to different ports.
```bash
# port_scanner.py
import socket
```
## Step 3: Set Up Target IP and Port Range
Define the IP address or hostname you want to scan, as well as the port range (e.g., ports 1-1024).
```bash
# Target and port range
target = input("Enter the target IP address or hostname: ")
start_port = int(input("Enter the starting port number: "))
end_port = int(input("Enter the ending port number: "))
```
## Step 4: Create the Scanning Function
This function will attempt to connect to each port in the specified range and determine if it’s open or closed.
```bash
def scan_port(port):
    """Scan a single port to see if it's open."""
    try:
        # Create a socket connection
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(1)  # Set timeout for each port scan
        
        # Try to connect to the target and port
        result = sock.connect_ex((target, port))
        
        # If result is 0, the port is open
        if result == 0:
            print(f"Port {port} is open")
        sock.close()
        
    except Exception as e:
        print(f"Error scanning port {port}: {e}")
```
## Step 5: Scan Each Port in the Specified Range
Now that we have a function to scan a single port, let’s call it in a loop to scan all ports in the specified range.
```bash
print(f"\nScanning {target} from port {start_port} to {end_port}...")

for port in range(start_port, end_port + 1):
    scan_port(port)

```
## Step 6: Run the Program
Once everything is set up, run the program:
```bash
python3 port_scanner.py
```
Enter the IP or hostname and the port range you want to scan. For example:
```bash
Enter the target IP address or hostname: 192.168.1.1
Enter the starting port number: 1
Enter the ending port number: 1024
```
The scanner will display open ports on the specified target.

## Additional Improvements
Consider adding these features to expand your scanner:

Threading: Use threading to speed up scans by checking multiple ports simultaneously.
Service Identification: Use socket.getservbyport(port) to identify which service typically runs on open ports.

Happy scanning! 🖥️

