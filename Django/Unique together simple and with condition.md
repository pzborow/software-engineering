# Unique together simple and with condition

/## Proste
```python
class MyModel(models.Model):
  field1 = models.CharField(max_length=50)
  field2 = models.CharField(max_length=50)

  class Meta:
    unique_together = ('field1', 'field2',)
```

## Z warunkiem

```python
from django.db import models
from django.db.models import Q
from django.db.models.constraints import UniqueConstraint

class Badger(models.Model):
    required = models.ForeignKey(Required, ...)
    optional = models.ForeignKey(Optional, null=True, ...)
    key = models.CharField(db_index=True, ...)

    class Meta:
        constraints = [
            UniqueConstraint(fields=['required', 'optional', 'key'],
                             name='unique_with_optional'),
            UniqueConstraint(fields=['required', 'key'],
                             condition=Q(optional=None),
                             name='unique_without_optional'),
        ]
```