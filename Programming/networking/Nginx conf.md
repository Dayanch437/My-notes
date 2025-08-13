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

~~~bash
server {
    listen 80;
    server_name yourdomain.com; # or IP like 34.55.178.211

    root /srv/book-com/book-competition-app/dist;
    index index.html;

    # Serve static assets (CSS, JS, images, etc.)
    location / {
        try_files $uri /index.html;
    }

    # Optional: caching for static files
    location ~* \.(?:ico|css|js|gif|jpe?g|png|woff2?|eot|ttf|svg)$ {
        expires 6M;
        access_log off;
        add_header Cache-Control "public";
    }
}
~~~


~~~bash
server {
    listen 81;
    server_name your.domain.com;  # replace with your domain or IP

    # Serve static files collected by Django
    location /static/ {
        alias /srv/book-com/backend/static/;
        expires 30d;
        access_log off;
    }

    # Serve media files uploaded by users
    location /media/ {
        alias /srv/book-com/backend/media/;
        expires 30d;
        access_log off;
    }

    # API and all other Django requests
    location / {
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        # Add CORS headers to all responses
        add_header 'Access-Control-Allow-Origin' '*' always;
        add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS, PUT, DELETE, PATCH' always;
        add_header 'Access-Control-Allow-Headers' 'Authorization, Content-Type' always;

        # Handle preflight OPTIONS request for CORS
        if ($request_method = OPTIONS) {
            return 204;
        }

        proxy_pass http://127.0.0.1:8000;  # Gunicorn server address
        proxy_redirect off;
    }
}
~~~
