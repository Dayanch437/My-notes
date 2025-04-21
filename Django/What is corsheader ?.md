`django-cors-headers` is a Django app that helps handle **CORS**.

### 🔍 What is CORS?

**CORS = Cross-Origin Resource Sharing**
It controls **which websites are allowed to access your backend API**.

### 🧠 Why do you need it?

Imagine:

- Your **Django backend** runs at `http://localhost:8000`
    
- Your **frontend** (React, Flutter web, etc.) runs at `http://localhost:3000`
    

When the frontend tries to request data from the backend, the browser **blocks** the request unless your backend explicitly **allows** it — that's where `corsheaders` helps.

### 🛠️ What does `django-cors-headers` do?

- Adds special **CORS headers** to your responses.
    
- These headers tell the browser: **“Yes, I allow requests from this frontend”**
    

Example response header added:
~~~http
Access-Control-Allow-Origin: http://localhost:3000
~~~

### ✅ Summary

|Feature|Purpose|
|---|---|
|CORS|Security rule in browsers for cross-origin requests|
|`django-cors-headers`|A Django tool to manage CORS rules easily|
|Main job|Add correct headers to let your frontend access the backend|

### ✅ 1. Install the package

Run this in your terminal:
~~~bash
pip install django-cors-headers
~~~


### ✅ 2. Add to `INSTALLED_APPS`

In `settings.py`, add `'corsheaders'` at the top of `INSTALLED_APPS`:
~~~bash
INSTALLED_APPS = [
    'corsheaders',
    'django.contrib.admin',
    'django.contrib.auth',
    ...
]
~~~

### ✅ 3. Add middleware

In `settings.py`, add the middleware at the **top** of the `MIDDLEWARE` list:
~~~bash 
MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',  # Must be at the top
    'django.middleware.common.CommonMiddleware',
    ...
]
~~~

### ✅ 4. Allow origins (choose one)

#### Option A: Allow **all** origins (for development only!):
~~~bash
CORS_ALLOW_ALL_ORIGINS = True
~~~

Option B: Allow specific domains:
~~~bash
CORS_ALLOWED_ORIGINS = [
    "http://localhost:3000",  # React / Vue / etc.
    "http://127.0.0.1:3000",
    "http://yourfrontend.com",
]
~~~
### ✅ 5. (Optional) Allow credentials (cookies, tokens)

If you're using authentication like session or JWT in headers:
~~~bash
CORS_ALLOW_CREDENTIALS = True
~~~

✅ 6. Done! Restart your Django server
~~~bash 
python manage.py runserver
~~~


`CORS_ALLOW_CREDENTIALS = True` means:

> "Allow the frontend to send **cookies**, **authorization headers**, or **TLS client certificates** in requests."

---

### 💡 Why would you use it?

You need it when:

- Your **frontend** uses:
    
    - Login sessions (`SessionAuthentication`)
        
    - JWT tokens in headers (`Authorization: Bearer <token>`)
        
    - CSRF-protected forms
        
- Your backend needs to **know who is making the request**
    

---

### 📦 Example

#### Without `CORS_ALLOW_CREDENTIALS = True`:

- Request with token or cookie → **Blocked by browser**
    
- Backend doesn't receive user info
    

#### With `CORS_ALLOW_CREDENTIALS = True`:

- Cookies or tokens are allowed → **Browser includes them in the request**
    
- Backend can check auth and respond correctly
    

---

### ⚠️ Important Note

If you enable `CORS_ALLOW_CREDENTIALS = True`, **you must not** use `CORS_ALLOW_ALL_ORIGINS = True`. Instead, use `CORS_ALLOWED_ORIGINS` with specific domains.

Like this:

~~~bash
CORS_ALLOW_CREDENTIALS = True

CORS_ALLOWED_ORIGINS = [
    "http://localhost:3000",
    "https://your-frontend.com",
]
~~~
