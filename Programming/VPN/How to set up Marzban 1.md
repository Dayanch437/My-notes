			
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

~~~python
-----BEGIN CERTIFICATE----- MIIEnDCCAoQCAQAwDQYJKoZIhvcNAQENBQAwEzERMA8GA1UEAwwIR296YXJnYWgw IBcNMjUwNTIwMTIzMDI3WhgPMjEyNTA0MjYxMjMwMjdaMBMxETAPBgNVBAMMCEdv emFyZ2FoMIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAooGmQFsg8Ix7 S8tfK6IYMFrdqqsSEA6jwsjEpWhRRbsX5RnxmaJ6hf8EkVcjtAPdz/SwW/66OTOk nX/yn+hgWV5Dse8u/+w70aE/u1P9DFT20Anbzdk//9VFl2dQsfkArZHnZo/9Z9tT QwURqJOU+X62Uaa2Gtj/QfupqIVY84hE40RuOe8yzVVV2nVLqXRjZmDbToMnzpuD btyZIfvOwAY8QjxR6tSNyl+ui6ERf09guPdcBYa95kji/yLlDDyfkfixmAXFJM9Y vbh3Ww3eAt2K76i4cmg6qsS1RYmMXA3iyaHAmsjMGWTTjgiLiTRHGT16rFezL6s2 4KZXWDeKECMt4QUAqLcCzuUpjuPPmZqxZm7E/xm2e6whB8nL2vimIWz6jeShRqJG n715KBBTRjZEQcIkMoJWvobv141lqX5WTh1vl4yNEAox4xtNxYQVoemvDB6/qHgK 6fM5GeRfoGbBYfcK3Kq2svZKiisE2WkZYSUwgt+AltDLaoUACVRHuN85s+atZvk8 p/QovQK96L4drZI7lk7Beztk5uN5jA7ZiL86SVmIWbNA2HIuLImbeRGzZvjQg9n3 6opZurOCcq5iajH7wx5k1TGK+84LBNbqrjFsSNMp0sIripuBH1qBizR6kRAKHTji aGgb1igPbINVj7jbSdVsX6TGXxJwRKMCAwEAATANBgkqhkiG9w0BAQ0FAAOCAgEA inOkm0I6zLqArF7Er5I8NEknSHC0NRr7X8gBB6eMRyIft0KhWxAiwxcD+s/YUOPe vk+WxPGUShrSKXu18Bv83mRhK0Hx2/wOvx+CFzggcE99KUKIbFdd3r1FRNGX/iu7 z/UG7atn+IReP9B6YYpauZ+3t3NrGxLlB+vwwQzrOaC/UTteHjEbFjbSUiD9lN1C SowoRwyNFbsA47icp3zTvofncfY+X5tPXh6Zg4JRLWpOQvfS4Gpd734z01BUeIi1 GDHyDy3xRtGT40D4a9thy9HQcRmF6syAZYHoSYVAJPJmg2zkPXYfeNj4xvM7JgWQ fW3r2tvzIJ4P8PL9qtus9VtQVvTyygQM9+Zz1UAfDYl1Axl5wHOhBRePooJqqZel uxfuBd+KSk4OPoTJ4MJ2FzdOBU1GAoynHxj+Cb6BxuQON9E0fF9ZQydTj4i9eGXr eH+OE8ly6gz26EmlCS/PBzAfeczWfPCfFGgY3c9+stkVqDTFkKRcLqrkdpQb/ZoE Eei/P4dt9oGqzI4LCMZiAJM77nf55+GXRKzcPO/oPOyZv1oInmspNGhis3cQo3Hn 7dp9ITPKGoqstwTwG6nCZXBPTyVC+FdEj0kxEgDgt4SlHH6sT9SxRs5AcUqN9Oyd 2qL3bACzrCwhW8stEG/ey8HW8WFb2CUlQUq+CqAl79g=
-----END CERTIFICATE-----
~~~