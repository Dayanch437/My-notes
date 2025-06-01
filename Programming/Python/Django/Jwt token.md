### 🔐 What is `simple-jwt`?

`djangorestframework-simplejwt` is a Django package that provides **JWT (JSON Web Token) authentication** for Django REST Framework (DRF).

### 🧠 What is JWT?

JWT is a secure way to handle **user login/authentication** in APIs.

- A user logs in with username & password
    
- Server returns a **token** (like a key)
    
- The frontend saves the token and sends it with every API request

### ✅ What does `simple-jwt` do?

It helps Django to:

- Create JWT **access** and **refresh** tokens
    
- Verify and decode tokens on every request
    
- Support login/logout using JWT
    
- Support token refresh (get new access token)

### 📦 Example Flow:

1. **User logs in:**
~~~http
POST /api/token/
{ "username": "dayanch", "password": "1234" }
~~~

→ returns:
~~~json
{
  "access": "abc123...",
  "refresh": "def456..."
}
~~~
- **Frontend stores `access` token** (in localStorage or memory)
- **Frontend calls protected API:**
~~~http
GET /api/user-data/
Authorization: Bearer abc123...
~~~
**If token expires**, refresh it:
~~~http
POST /api/token/refresh/
{ "refresh": "def456..." }
~~~

⚙️ How to install and use?

~~~bash
pip install djangorestframework-simplejwt
~~~

Then in `settings.py`:

~~~
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ),
}
~~~

In your main `urls.py` (e.g., `project/urls.py`):
~~~bash 
from django.urls import path
from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
)

urlpatterns = [
    # JWT token URLs
    path('api/token/', TokenObtainPairView.as_view(), name='token_obtain_pair'),
    path('api/token/refresh/', TokenRefreshView.as_view(), name='token_refresh'),
]
~~~

In `settings.py`, add:
~~~bash
from datetime import timedelta

SIMPLE_JWT = {
    'ACCESS_TOKEN_LIFETIME': timedelta(minutes=15),
    'REFRESH_TOKEN_LIFETIME': timedelta(days=7),
    'AUTH_HEADER_TYPES': ('Bearer',),
}
~~~
