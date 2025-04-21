~~~python 
server {
    listen 80;
    server_name gyrat.shop;

    # Serve React frontend
    root /srv/Gyrat-shop/frontend/dist;
    index index.html;

    location / {
        try_files $uri /index.html;
    }

    # API requests to Django backend
    location /api/ {
        proxy_pass http://unix:/run/gunicorn.sock;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Admin panel to Django backend
    location /admin/ {
        proxy_pass http://unix:/run/gunicorn.sock;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Django static files
    location /static/ {
        alias /srv/Gyrat-shop/backend/static/;
    }

    # Django media files
    location /media/ {
        alias /srv/Gyrat-shop/backend/media/;
    }

    client_max_body_size 20M;

    # Gzip for performance
    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
    gzip_proxied any;
    gzip_vary on;
    gzip_min_length 1000;
}
~~~
