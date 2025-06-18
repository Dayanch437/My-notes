**`django-unfold`** is a modern **admin interface enhancement** package for Django. It replaces the default Django admin interface with a **cleaner**, **responsive**, and **more user-friendly UI** — while keeping full compatibility with Django’s built-in admin system.

### 🔧 What it does:

- Enhances Django’s admin UI (HTML + CSS + JS) without changing your data/models.
    
- Built using modern frontend tools like **Tailwind CSS** and **Alpine.js**.
    
- Gives you a **more beautiful and modern admin interface** with features like:
    
    - Collapsible inlines
        
    - Improved forms
        
    - Sidebar navigation
        
    - Better dark mode support

### ✅ Benefits:

- Drop-in replacement for the default Django admin.
    
- No need to rewrite your admin logic.
    
- Makes the admin more usable for real-world apps.

~~~python
pip install django-unfold
~~~
⚙️ Setup in `settings.py`:
~~~python 
INSTALLED_APPS = [
    "unfold",              # Add this before 'django.contrib.admin'
    "django.contrib.admin",
    ...
]

UNFOLD = {
    "SITE_TITLE": "My Admin",
    "SHOW_HISTORY": True,
    "DARK_MODE": True,
}
~~~
