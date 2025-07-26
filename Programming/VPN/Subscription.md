~~~javascript
function doGet(e) {
  var url = e.parameter.url;

  if (!url) {
    return ContentService.createTextOutput("Missing 'url' parameter");
  }

  try {
    var response = UrlFetchApp.fetch(url);
    var contentType = response.getHeaders()['Content-Type'] || 'text/plain';
    var content = response.getContentText();

    return ContentService
      .createTextOutput(content)
      .setMimeType(getMimeType(contentType));
  } catch (err) {
    return ContentService.createTextOutput("Error: " + err)
      .setMimeType(ContentService.MimeType.TEXT);
  }
}

function getMimeType(contentType) {
  if (contentType.includes("html")) return ContentService.MimeType.HTML;
  if (contentType.includes("json")) return ContentService.MimeType.JSON;
  if (contentType.includes("xml")) return ContentService.MimeType.XML;
  return ContentService.MimeType.TEXT;
}

~~~
	
~~~bash
docker cp marzban-marzban-1:/code/app/telegram/utils/shared.py ./shared.py
~~~

~~~bash
nano shared.py
~~~

~~~bash
./shared.py docker cp marzban-marzban-1:/code/app/telegram/utils/shared.py 
~~~

~~~bash
docker restart marzban-marzban-1
~~~
Telegram user info boot
~~~bash
@userinfobot
~~~



~~~python
	sudo bash -c "$(curl -sL https://github.com/Gozargah/Marzban-scripts/raw/master/marzban-node.sh)" @ install
~~~

~~~bash
{
  "inbounds": [
    {
      "tag": "TROJAN + TCP",
      "listen": "0.0.0.0",
      "port": 30,
      "protocol": "trojan",
      "settings": {
        "clients": []
      },
      "streamSettings": {
        "network": "tcp",
        "tcpSettings": {},
        "security": "none"
      },
      "sniffing": {
        "enabled": true,
        "destOverride": [
          "http",
          "tls"
        ]
      }
    },
    {
      "tag": "SHADOWSOCKS TCP",
      "listen": "0.0.0.0",
      "port": 24,
      "protocol": "shadowsocks",
      "settings": {
        "clients": [],
        "network": "tcp,udp"
      }
    },
    {
      "tag": "VLESS TCP",
      "listen": "0.0.0.0",
      "port": 18,
      "protocol": "vless",
      "settings": {
        "clients": [],
        "decryption": "none"
      },
      "streamSettings": {
        "network": "tcp",
        "tcpSettings": {},
        "security": "none"
      },
      "sniffing": {
        "enabled": true,
        "destOverride": [
          "http",
          "tls"
        ]
      }
    },
    {
      "tag": "VLESS WS",
      "listen": "0.0.0.0",
      "port": 80,
      "protocol": "vless",
      "settings": {
        "clients": [],
        "decryption": "none"
      },
      "streamSettings": {
        "network": "ws",
        "wsSettings": {},
        "security": "none"
      },
      "sniffing": {
        "enabled": true,
        "destOverride": [
          "http",
          "tls"
        ]
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {},
      "tag": "DIRECT"
    },
    {
      "protocol": "blackhole",
      "tag": "BLOCK"
    },
    {
      "tag": "DNS-External",
      "protocol": "dns",
      "settings": {
        "address": "8.8.8.8",
        "port": 53
      }
    },
    {
      "tag": "warp",
      "protocol": "socks",
      "settings": {
        "servers": [
          {
            "address": "127.0.0.1",
            "port": 25355
          }
        ]
      }
    }
  ],
  "routing": {
    "domainStrategy": "AsIs",
    "rules": [
      {
        "type": "field",
        "port": 53,
        "network": "tcp,udp",
        "outboundTag": "DNS-External"
      },
      {
        "domain": [
          "localhost"
        ],
        "outboundTag": "BLOCK",
        "type": "field"
      },
      {
        "type": "field",
        "outboundTag": "warp",
        "protocol": [
          "bittorrent"
        ]
      }
    ]
  }
}
~~~
