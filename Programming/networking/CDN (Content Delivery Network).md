A **CDN (Content Delivery Network)** is a network of servers distributed around the world that delivers content (like images, videos, CSS, JavaScript, etc.) to users more quickly and efficiently based on their geographic location.

### Key points:

- **Faster delivery**: Content is served from the nearest server to the user, reducing latency.
    
- **Reduced load**: Takes pressure off your main server by caching static files.
    
- **Improved availability**: If one server goes down, others can take over.
    
- **Better security**: Many CDNs offer DDoS protection and HTTPS support.

### Example:

Instead of loading Bootstrap CSS from your server:
~~~html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
~~~

This uses a **CDN (jsDelivr)** to load the file quickly from a nearby server.

Do you want to know how to use a CDN in a Django or React project?

### In **Django**:

You typically use CDNs for static files like CSS/JS libraries (Bootstrap, jQuery, etc.).

#### Example (in a Django template):
~~~html
<!DOCTYPE html>
<html>
<head>
  <title>My Site</title>
  <!-- Bootstrap from CDN -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
~~~

You can also serve your **own static files** via CDN (like from AWS S3 + CloudFront), but that requires configuration.
