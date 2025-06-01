### 1. **`ForeignKey`** (One-to-Many)

A `ForeignKey` is used to create a one-to-many relationship. Each instance of the model that defines the `ForeignKey` will be related to one instance of another model, but the related model can be linked to many instances of the first model
~~~python 
class Author(models.Model):
    name = models.CharField(max_length=100)

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
~~~

### 2. **`ManyToManyField`** (Many-to-Many)

A `ManyToManyField` is used to create a many-to-many relationship, where both models can have multiple related instances. Django automatically handles the intermediary table.

~~~python 
class Student(models.Model):
    name = models.CharField(max_length=100)

class Course(models.Model):
    name = models.CharField(max_length=100)
    students = models.ManyToManyField(Student)
~~~

### 3. **`OneToOneField`** (One-to-One)

A `OneToOneField` creates a one-to-one relationship, meaning that each instance of the model that defines it will have a unique related instance of another model.
~~~python
class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    bio = models.TextField()
~~~

### 4. **`GenericForeignKey`** (Generic Relations)

Django provides the `GenericForeignKey` field as part of the `contenttypes` framework. This allows models to be related to any other model without a direct foreign key. It is useful when you need a generic relationship with multiple models.
~~~python
from django.contrib.contenttypes.fields import GenericForeignKey
from django.contrib.contenttypes.models import ContentType

class Tag(models.Model):
    name = models.CharField(max_length=100)

class TaggedItem(models.Model):
    content_type = models.ForeignKey(ContentType, on_delete=models.CASCADE)
    object_id = models.PositiveIntegerField()
    content_object = GenericForeignKey('content_type', 'object_id')
~~~
These are the most common relationships in Django. Each of them is typically paired with `on_delete=models.CASCADE` or another `on_delete` behavior to define how related data is handled when an instance is deleted.