### 🔹 `aggregate()`

- Calculates **summary values** over the **entire queryset**.
    
- Returns a **single dictionary** of values.
    

#### Example:
```python
from django.db.models import Avg, Max, Count
from myapp.models import Student

Student.objects.aggregate(
    average_score=Avg('score'),
    max_score=Max('score'),
    total_students=Count('id')
)

```
➡️ Output:
```bash
{'average_score': 85.4, 'max_score': 100, 'total_students': 25}

```
### 🔹 `annotate()`

- Adds **aggregated values** to **each row** in the queryset.
    
- Useful when you want to group or calculate values **per object**.
#### Example:
~~~pyhton 
from django.db.models import Count
from myapp.models import Teacher

Teacher.objects.annotate(
    total_students=Count('student')
)
~~~
