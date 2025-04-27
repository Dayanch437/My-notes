To write a custom action in a Django REST Framework (DRF) `ViewSet`, you use the `@action` decorator from `rest_framework.decorators`. Here's a simple example:
1. **Import the decorator**
~~~python 
from rest_framework.decorators import action
from rest_framework.response import Response
~~~
2. **Define the action inside your ViewSet**
~~~python
from rest_framework.viewsets import ModelViewSet
from .models import Product
from .serializers import ProductSerializer

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    @action(detail=True, methods=['get'])  # detail=True means it uses pk (e.g. /products/1/my_action/)
    def my_action(self, request, pk=None):
        product = self.get_object()
        data = {"message": f"This is a custom action for {product.name}"}
        return Response(data)
~~~

3. **Use in router**
~~~python 
GET /products/1/my_action/
~~~
		