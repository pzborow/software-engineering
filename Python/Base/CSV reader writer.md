# CSV reader writer

## Czytanie na szybko
```python
import csv
with open('~/ecrubexport', newline='') as csvfile:
    spamreader = csv.reader(csvfile, delimiter='|', quotechar='"')
    for row in spamreader:
        print(','.join(row))
```

## Pisanie na szybko
```python
import csv
with open('eggs.csv', 'w', newline='') as csvfile:
    spamwriter = csv.writer(csvfile, delimiter=' ',
                            quotechar='|', quoting=csv.QUOTE_MINIMAL)
    spamwriter.writerow(['Spam'] * 5 + ['Baked Beans'])
    spamwriter.writerow(['Spam', 'Lovely Spam', 'Wonderful Spam'])
```

## Czytanie, operacja i zapis

```python
headers = "pk/ne/iaa/iab/naa/nab/data_u".split("/")
import csv
with open('ecrubexport', newline='') as csvin, open('tmp/ecrubexportid', 'w', newline='') as csvout:
    spamreader = csv.reader(csvin, delimiter='|', quotechar='"')
    spamwriter = csv.writer(csvout, delimiter='|', quotechar='"', quoting=csv.QUOTE_MINIMAL)
    spamwriter.writerow(datarow.keys())
    for row in spamreader:
        row = [cell or None for cell in row]
        datarow = dict(zip(headers, [None] + row))
        osoba = BOsoba(**datarow)
        osoba.save()
        datarow['pk'] = osoba.pk
        spamwriter.writerow(datarow.values())
```