# CodeAlpha_Network_Sniffer
## **Project: Basic Network Sniffer in Python**  

### **Description**  
A **Network Sniffer** is a tool that captures and analyzes network packets in real time. This project helps understand how data flows in a network by intercepting packets at the data link layer (Ethernet).  

In this project, we use **Python** and the **socket library** to create a **raw socket** that listens for all incoming network traffic. The script extracts and displays important details like **MAC addresses** and **protocol types** from captured packets.  

This tool is useful for **network monitoring, security analysis, and debugging network issues**.  

---

### **How It Works**
1. The script creates a **raw socket** using Python's `socket` module.
2. It continuously **listens for incoming network packets**.
3. Extracts **source MAC, destination MAC, and protocol type** from the Ethernet frame.
4. Prints the extracted information in a human-readable format.
5. The process runs in a loop until the user stops it manually (`Ctrl + C`).

---

### **How to Use**  
1. Install Python (if not installed).
2. Run the script with **administrator/root privileges**:
   ```
   sudo python3 network_sniffer.py
   ```
3. View the live captured packets on your terminal.

---

### **Code Example**  
```python
import socket
import struct

# Create a raw socket to capture packets
sniffer = socket.socket(socket.AF_PACKET, socket.SOCK_RAW, socket.ntohs(3))

print("Sniffing network traffic... Press Ctrl+C to stop.")

try:
    while True:
        raw_data, addr = sniffer.recvfrom(65535)  # Receive packet
        dest_mac, src_mac, eth_proto = struct.unpack("!6s6sH", raw_data[:14])

        # Convert MAC addresses to human-readable format
        dest_mac = ':'.join(format(byte, '02x') for byte in dest_mac)
        src_mac = ':'.join(format(byte, '02x') for byte in src_mac)

        print(f"Source MAC: {src_mac}, Destination MAC: {dest_mac}, Protocol: {eth_proto}")

except KeyboardInterrupt:
    print("\nStopping sniffer...")
    sniffer.close()
```

---

### **Requirements**
- **Python 3.x** installed  
- **Administrator/root access** to run raw sockets  
- Works on **Linux/macOS** (For Windows, use `WinPcap` with `scapy`)

---

### **Future Enhancements**
✅ Add support for **IP, TCP, and UDP packet analysis**  
✅ Save captured data to a **log file**  
✅ Create a **GUI-based sniffer** for better visualization  

---



This project is a great **starting point** for learning **network security and packet analysis**. 🚀
