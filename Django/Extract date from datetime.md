# Extract date from datetime

W pythonie
```ipython
In [48]: a = Manufacturer.objects.get(pk=635).asset_set.all(). \
    ...: filter(title__contains="Infographic").last()
In [49]: a.create_date.date()
Out[49]: datetime.date(2022, 5, 28)

```

W zapytaniu do bazy danych
```ipython
In [47]: Manufacturer.objects.get(pk=635).asset_set.all(). \
    ...: filter(title__contains="Infographic"). \
    ...: annotate(create_at_date=Func(F('create_date'), function='date')). \
    ...: last().create_at_date
Out[47]: datetime.date(2022, 5, 28)
```

W sql
```sql
SELECT *,
       date("assets_asset"."create_date") AS "create_at_date"
FROM "assets_asset"
WHERE ("assets_asset"."deleted_at" IS NULL
       AND "assets_asset"."manufacturer_id" = 635
       AND "assets_asset"."title"::text LIKE %Infographic%
```