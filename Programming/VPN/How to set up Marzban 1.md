	
## ✅ [[Marzban]] Setup – Step-by-Step (Ubuntu 20.04+)

### ⚙️ Requirements

- A **fresh Ubuntu VPS** (not behind NAT like OpenVPN panels)
    
- **Root access**
    
- A **domain name** pointing to your server’s IP (e.g., `yourdomain.com`)
    
- **Ports 80 and 443 open**


~~~bash
sudo bash -c "$(curl -sL https://github.com/Gozargah/Marzban-scripts/raw/master/marzban.sh)" @ install
~~~
  Then install [[caddy server ]]
~~~bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https  
curl -fsSL https://dl.cloudsmith.io/public/caddy/stable/gpg.key | sudo tee /usr/share/keyrings/caddy-keyring.asc  
echo "deb [signed-by=/usr/share/keyrings/caddy-keyring.asc] https://dl.cloudsmith.io/public/caddy/stable/deb/debian any-version main" | sudo tee /etc/apt/sources.list.d/caddy.list  
sudo apt update  
sudo apt install caddy -y
~~~

~~~bash 
sudo nano /etc/caddy/Caddyfile
~~~

~~~bash
your-domain.com {
    reverse_proxy localhost:8000
}
~~~


~~~bash
sudo systemctl restart caddy
~~~

marzban node installation

~~~python
sudo bash -c "$(curl -sL https://github.com/Gozargah/Marzban-scripts/raw/master/marzban-node.sh)" @ install
~~~
