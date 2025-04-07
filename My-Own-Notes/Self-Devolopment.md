
**"Do what you can, with what you have, where you are."** — Theodore Roosevelt


{
  "admission_major": 1,
  "exam_dates": [
    {
      "region": 2,
      "date_of_exam": "20.02.2025",
      "subject": 3
    },
    {
      "region": 2,
      "date_of_exam": "20.02.2020",
      "subject": 5
    }
  ]
}





## **1. Introduction to Networking**

- **Definition**: Connecting two or more devices to share data and resources.
    
- **Goals**:
    
    - Resource sharing (printers, files)
        
    - Communication (emails, chat)
        
    - Centralized data management
        
- **Advantages**:
    
    - Cost-efficiency
        
    - Scalability
        
    - Remote access
        

---

## **2. Network Components**

- **Devices**:
    
    - **Router**: Forwards data between networks.
        
    - **Switch**: Connects devices in LAN and forwards data based on MAC addresses.
        
    - **Hub**: Broadcasts data to all devices (less efficient than a switch).
        
    - **Modem**: Converts digital to analog signals (and vice versa) for Internet.
        
    - **Access Point (AP)**: Extends wireless coverage.
        
- **End Devices**:
    
    - Computers, phones, IoT devices
        
- **Transmission Media**:
    
    - **Wired**: Twisted pair, Coaxial cable, Fiber optic
        
    - **Wireless**: Wi-Fi, Bluetooth, Infrared, Satellite
        

---

## **3. Network Topologies**

- **Bus**: One main cable; simple, but one failure can take down network.
    
- **Star**: Central switch/hub; scalable and easy to troubleshoot.
    
- **Ring**: Data travels in a circular fashion; each node connects to two others.
    
- **Mesh**: Every device connected to every other device; reliable but expensive.
    
- **Hybrid**: Combination of above (common in enterprise networks).
    

---

## **4. Types of Networks**

- **PAN**: Small (Bluetooth devices).
    
- **LAN**: Single building or home.
    
- **WLAN**: Wireless LAN (Wi-Fi).
    
- **MAN**: City-sized network (university campuses).
    
- **WAN**: Spans countries or continents (Internet).
    
- **SAN**: Storage Area Network (used in data centers).
    
- **VPN**: Private encrypted connection over public networks.
    

---

## **5. OSI Model (7-Layer Model)**

1. **Physical**: Cables, switches, signals
    
2. **Data Link**: MAC address, Ethernet, ARP
    
3. **Network**: IP addressing, Routing (IP, ICMP)
    
4. **Transport**: TCP (reliable), UDP (fast)
    
5. **Session**: Establishing/maintaining sessions
    
6. **Presentation**: Data format, encryption, compression
    
7. **Application**: End-user services (HTTP, FTP, DNS)
    

---

## **6. TCP/IP Model (4-Layer Model)**

- **Link Layer**: Ethernet, ARP, Wi-Fi
    
- **Internet Layer**: IP, ICMP, routing
    
- **Transport Layer**: TCP, UDP
    
- **Application Layer**: HTTP, HTTPS, FTP, SMTP, DNS
    

---

## **7. IP Addressing**

- **IPv4**: 32-bit (e.g., 192.168.1.1)
    
- **IPv6**: 128-bit (e.g., fe80::1)
    
- **Subnetting**: Dividing networks; uses subnet mask
    
- **CIDR**: Classless Inter-Domain Routing (e.g., 192.168.1.0/24)
    
- **Private IP ranges**:
    
    - Class A: 10.0.0.0/8
        
    - Class B: 172.16.0.0/12
        
    - Class C: 192.168.0.0/16
        

---

## **8. Routing and Switching**

- **Routing**: Choosing best path between networks
    
    - **Static Routing**: Manually configured
        
    - **Dynamic Routing**: Protocol-based (RIP, OSPF, BGP)
        
- **Switching**:
    
    - **Layer 2**: MAC-based forwarding
        
    - **VLANs**: Logically separate networks
        
    - **Layer 3 Switches**: Combine routing and switching
        

---

## **9. Network Security**

- **Threats**: DoS, Man-in-the-Middle, spoofing, phishing
    
- **Defense**:
    
    - **Firewalls**: Filter traffic
        
    - **VPNs**: Secure tunnels
        
    - **Encryption**: TLS/SSL, AES
        
    - **Antivirus and IDS/IPS**
        

---

## **10. Networking Tools**

- `ping`: Check host availability
    
- `traceroute` / `tracert`: Path taken by packets
    
- `ipconfig` / `ifconfig`: Network configuration
    
- `nslookup`: DNS resolution
    
- `netstat`: Active connections
    
- `nmap`: Network scanner
    
- `tcpdump` / `Wireshark`: Packet sniffer
    

---

## **11. Wireless Networking**

- **Wi-Fi Standards**: 802.11a/b/g/n/ac/ax
    
- **Frequencies**: 2.4 GHz vs 5 GHz
    
- **Encryption**:
    
    - WEP (weak)
        
    - WPA/WPA2 (secure)
        
    - WPA3 (latest)
        
- **SSID**: Network name
    
- **Channel**: Frequency slot to avoid interference
    

---

## **12. Troubleshooting Basics**

- Check cables and power
    
- Use `ping`, `tracert`, `ipconfig`
    
- Check DNS issues
    
- Restart modem/router
    
- Use safe mode or static IP to isolate problems