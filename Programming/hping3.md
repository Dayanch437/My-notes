### ✅ Recommended Setup for Safe Testing

1. **Use Virtual Machines (VMs)**:
    
    - One VM as the **attacker** (running `hping3`).
        
    - One VM as the **target/server** (e.g., running a web server or ping listener).
        
    - Use VirtualBox or VMware and connect them via a **host-only or internal network**.
        
2. **Install hping3**:
~~~bash
sudo apt update
sudo apt install hping3
~~~
**Simple Flood Example (Local Network Test)**:

#### SYN Flood:
~~~
sudo hping3 -S --flood -p 80 <target_vm_ip>
~~~

### 💣 What Happens During an hping3 Flood Attack?

#### 1. **Packet Crafting**

`hping3` allows the user to create custom network packets (TCP, UDP, ICMP, etc.).

#### 2. **Flooding (Mass Sending)**

When you use the `--flood` option, `hping3` sends **as many packets as possible** without waiting for a response — it's like **spamming** the network.

#### 3. **Target Overload**

The target system:

- **Receives thousands of packets per second**.
    
- Tries to **process, respond, or log** each request.
    
- **Consumes CPU, memory, or bandwidth**.
    
- If overwhelmed, it **slows down** or **crashes** — that's a **Denial of Service** (DoS).
~~~bash
sudo hping3 -S --flood -p 80 <target_ip>

~~~
#### Step-by-step:

1. `-S`: Sends TCP SYN packets (pretend to start a connection).
    
2. `--flood`: Sends them non-stop, as fast as possible.
    
3. The target (e.g., a web server) tries to reply with SYN-ACK.
    
4. Since `hping3` doesn’t complete the handshake, the server waits… again and again.
    
	1. Eventually, the **server runs out of connection slots**, or gets **too slow** to respond to real users.