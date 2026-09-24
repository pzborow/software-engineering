# Extract date from datetime, count objects by date

```python
Manufacturer.objects.get(pk=635).asset_set.all(). \
filter(title__contains="Infographic"). \
annotate(create_at_date=Func(F('create_date'), function='date')). \
values('create_at_date').annotate(count=Count('id'))
```