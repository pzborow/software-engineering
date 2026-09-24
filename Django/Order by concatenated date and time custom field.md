# Order by concatenated date and time custom field

```python
from django.db.models.functions import Concat, Cast
from django.db.models import DateTimeField, CharField, Value
from datetime import datetime

date_time_expr = Cast(Concat('date', Value(' '), 'time', output_field=CharField()), output_field=DateTimeField())

TimeTable.objects.annotate(date_time=date_time_expr).filter(date_time__gte=datetime.now()).order_by('date_time')
```