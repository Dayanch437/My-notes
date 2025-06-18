- **VPN Type**: IPsec IKEv2 using Pre-Shared Key (PSK)
    
- **Server OS**: Ubuntu (or Debian-based)
    
- **Router**: Should support IPsec IKEv2 with PSK
    
- **Goal**: Route traffic between router (LAN) and VPN server (remote LAN)

🧰 Step 1: Install StrongSwan on Server

~~~python
sudo apt update
sudo apt install strongswan strongswan-pki -y
~~~

## 🧾 Step 2: Configure IPsec

Edit the IPsec configuration file:

~~~bash
sudo nano /etc/ipsec.conf
~~~
Paste:
~~~ini
config setup
    charondebug="ike 1, knl 1, cfg 0"

conn routervpn
    auto=add
    keyexchange=ikev2
    authby=psk
    type=tunnel

    left=%any
    leftid=@vpn-server
    leftsubnet=10.0.0.0/24      # VPN server’s internal subnet

    right=<ROUTER_PUBLIC_IP>
    rightid=@router
    rightsubnet=192.168.1.0/24  # Router's LAN subnet

    ike=aes256-sha1-modp1024
    esp=aes256-sha1
    dpdaction=restart
    dpddelay=30s
    dpdtimeout=120s
~~~
Replace `<ROUTER_PUBLIC_IP>` with your router's actual public IP.
🔑 Step 3: Set Pre-Shared Key (PSK)
~~~bash
sudo nano /etc/ipsec.secrets
~~~
Example:
~~~bash
@vpn-server @router : PSK "YourStrongSharedKey123"
~~~
## 🔁 Step 4: Restart StrongSwan

Check which service is used:
~~~ bash
systemctl list-units | grep strongswan
~~~

Then restart the matching one:
~~~bash
sudo systemctl restart strongswan-starter
~~~
or
~~~bash
sudo systemctl restart strongswan-swanctl
~~~

🔍 Step 5: Enable IP Forwarding

~~~bash
sudo nano /etc/sysctl.conf
~~~

Uncomment or add:

~~~bash
net.ipv4.ip_forward = 1

~~~

Apply:
~~~bash
sudo sysctl -p
~~~

## 🔥 Step 6: Configure Firewall (ufw/iptables)

### Allow IPsec Ports

~~~bash
sudo ufw allow 500,4500/udp
sudo ufw allow esp
~~~

NAT for VPN subnet
~~~bash
sudo iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -o eth0 -j MASQUERADE
~~~

Make it persistent:
~~~bash
sudo apt install iptables-persistent
sudo netfilter-persistent save
~~~

## 📶 Step 7: Configure Your Router (Client Side)

In your router's IPsec/IKEv2 settings:

- **Remote Gateway**: `<VPN_SERVER_PUBLIC_IP>`
    
- **PSK**: `YourStrongSharedKey123`
    
- **Local ID**: `@router`
    
- **Remote ID**: `@vpn-server`
    
- **Local Subnet**: `192.168.1.0/24`
    
- **Remote Subnet**: `10.0.0.0/24`
    
- **IKE Phase 1**: AES-256 / SHA1 / MODP1024
    
- **IKE Phase 2 (ESP)**: AES-256 / SHA1
    
- **DPD**: Enable with 30s delay, 120s timeout


✅ Final Checks

On server:
~~~bash
sudo ipsec statusall
~~~
- Look for “INSTALLED, TUNNEL” and traffic counters.
    
- On router:  
    Check logs or dashboard for “IPsec tunnel connected”.