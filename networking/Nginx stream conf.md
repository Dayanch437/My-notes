~~~bash
stream {
    server {
        listen 8008;
        proxy_pass 138.124.24.96:443;
        proxy_connect_timeout 10s;
        proxy_timeout 300s;
    }
    server {
        listen 8000;
        proxy_pass 213.226.125.245:26347;
        proxy_connect_timeout 10s;
        proxy_timeout 300s;
    }
    server {
        listen 445;
        proxy_pass 172.105.80.57:1080;
        proxy_connect_timeout 10s;
        proxy_timeout 300s;
    }
    server {
        listen 444;
        proxy_pass 172.105.80.57:17040;
        proxy_connect_timeout 10s;
        proxy_timeout 300s;
    }
}
~~~

