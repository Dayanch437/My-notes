**Celery** is a Python library used to run **asynchronous tasks** in the background (outside the main request/response cycle). Common use cases:

- Sending emails
    
- Generating reports
    
- Running scheduled tasks (like cron)
    
- Long-running processes (e.g. image processing, ML)

### 🛠 How Celery Works (Simple Flow)

1. **Your Django app** sends a task to a **message broker** (like Redis or RabbitMQ).
    
2. **Celery workers** pick up the task and execute it in the background.
    
3. You can optionally store task results in a database.

### 🔧 Basic Setup in Django with Redis

#### 1. **Install dependencies**

```python
pip install celery redis

```

2. **Create `celery.py` in your Django project directory (same level as `settings.py`)**

~~~python
# myproject/celery.py
import os
from celery import Celery

os.environ.setdefault("DJANGO_SETTINGS_MODULE", "myproject.settings")

app = Celery("myproject")
app.config_from_object("django.conf:settings", namespace="CELERY")
app.autodiscover_tasks()
~~~

3. **In `__init__.py` of project**
	
~~~python
# myproject/__init__.py
from .celery import app as celery_app
__all__ = ("celery_app",)
~~~

4. **Configure Celery in `settings.py`**
~~~python
CELERY_BROKER_URL = "redis://localhost:6379/0"
CELERY_ACCEPT_CONTENT = ["json"]
CELERY_TASK_SERIALIZER = "json"
~~~

5. **Create a task in an app**
~~~python 
# myapp/tasks.py
from celery import shared_task
import time

@shared_task
def slow_add(x, y):
    time.sleep(5)
    return x + y
~~~

6. **Run Celery worker**
~~~python
celery -A myproject worker --loglevel=info
~~~

7. **Call the task**
~~~python
from myapp.tasks import slow_add
slow_add.delay(2, 3)  # Runs in background
~~~

🧠 Summary

| Component      | Purpose                        |
| -------------- | ------------------------------ |
| Celery         | Runs background tasks          |
| Redis          | Message broker (queues tasks)  |
| `@shared_task` | Makes a function a Celery task |
| `.delay()`     | Executes task asynchronously   |
