### 1. 🧠 **Python Execution Model**

- Your `.py` file is compiled into **bytecode** (`.pyc` files inside `__pycache__/`)
    
- Then bytecode is executed by the **Python Virtual Machine (PVM)** — a stack-based interpreter
    
- This process is invisible but crucial for performance and introspection
    

> In Django, every time you start the server (`runserver`), Python recompiles changed code and reloads it in the PVM.


### 2. 📦 **Modules, Packages & Import System**

- When you do `import` in Python/Django:
    
    - Python looks in `sys.path` (including `site-packages`, project root)
        
    - It compiles `.py` into `.pyc` if needed
        
    - Loads it into memory using import hooks (`__import__()` or `importlib`)
        

Django uses this heavily to:

- Load apps (`INSTALLED_APPS`)
    
- Load middleware dynamically
    
- Load management commands



### 3. ⚙️ **Object Model**

In Python:

- **Everything is an object**, including functions, modules, and classes
    
- Everything is an **instance of a class**
    
    - `type(5)` → `<class 'int'>`
        
    - `type(int)` → `<class 'type'>`
        

> Django uses metaclasses (`ModelBase`) to dynamically create model classes during startup.

### 4. 🔄 **Memory Management & Garbage Collection**

- Python uses **reference counting** + a **cyclic garbage collector**
    
- Objects are destroyed when ref count = 0
    
- `gc` module handles cleanup of circular references (like linked models or views)
    

> Improper reference handling in Django (e.g., in long-lived objects or signals) can cause memory leaks.

---
### 5. 🔀 **Async in Python**

- Python 3 has built-in `async` and `await` (event loop via `asyncio`)
    
- Django now supports async views and middleware (from 3.1+)


```from django.http import JsonResponse
import asyncio

async def my_async_view(request):
    await asyncio.sleep(1)
    return JsonResponse({"status": "done"})

```

### 6. 🧵 **Threads vs Async vs Processes**

- **Threading**: Useful for I/O-bound tasks (e.g. file uploads)
    
- **AsyncIO**: Lightweight, great for handling many concurrent requests
    
- **Multiprocessing**: Good for CPU-bound tasks (like image processing)
    

> Django itself is sync by default, but WSGI servers (like Gunicorn) or ASGI (for async) handle threading/processes.


### 7. 🧰 Useful Python Features for Django Devs

| Feature                           | Why It's Useful                              |
| --------------------------------- | -------------------------------------------- |
| `@property`, `@cached_property`   | For computed model fields                    |
| `*args`, `**kwargs`               | Used in class-based views, model inheritance |
| `functools.lru_cache`             | Cache-heavy DB calls                         |
| `inspect`, `getattr`, `setattr`   | Dynamic admin/serializer tools               |
| `contextlib.contextmanager`       | Custom file/db context managers              |
| `__call__`, `__new__`, `__init__` | For factories, singleton patterns            |
| `__str__`, `__repr__`             | Better model representations                 |
