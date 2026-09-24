# Timezone now pytz utc local

```ipdb
In [1]: import pytz

In [2]: from django.utils import timezone

In [3]: timezone.now()
Out[3]: datetime.datetime(2024, 1, 4, 16, 25, 28, 780809, tzinfo=datetime.timezone.utc)

In [4]: timezone.localtime(timezone.now())
Out[4]: datetime.datetime(2024, 1, 4, 16, 25, 39, 396761, tzinfo=zoneinfo.ZoneInfo(key='UTC'))

In [5]: timezone.activate(pytz.timezone("Europe/Warsaw"))

In [6]: timezone.localtime(timezone.now())
Out[6]: datetime.datetime(2024, 1, 4, 17, 25, 49, 301809, tzinfo=<DstTzInfo 'Europe/Warsaw' CET+1:00:00 STD>)
```