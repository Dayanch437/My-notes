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