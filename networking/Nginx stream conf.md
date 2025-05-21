~~~nginx
stream {
    server {
        listen 8008;
        proxy_pass 138.124.24.96:443;
        proxy_connect_timeout 10s;
        proxy_timeout 300s;
    }
}
~~~
