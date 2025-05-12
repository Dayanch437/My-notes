To clean up Django migrations while keeping the initial migrations and your virtual environment files, follow these steps:

## Recommended Approach

1. **Delete migration files** (except `__init__.py`):
~~~bash
find . -path "*/migrations/*.py" -not -name "__init__.py" -delete
find . -path "*/migrations/*.pyc" -delete
~~~
**Delete the database** (or just the migration tables if you want to keep your data):
~~~bash
rm db.sqlite3  # if using SQLite
# Or for other databases, you may need to drop and recreate it
~~~
**Recreate migrations**:
~~~bash
python manage.py makemigrations
python manage.py migrate
~~~
