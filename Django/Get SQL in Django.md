# Get SQL in Django

For `QuerySet`

```ipdb
>>> queryset = MyModel.objects.all()
>>> print(queryset.query)
SELECT "myapp_mymodel"."id", ... FROM "myapp_mymodel"
```

All sqls

```ipdb
from django.db import connections
connections['default'].queries
```
Musi być włączony DEBUG = True