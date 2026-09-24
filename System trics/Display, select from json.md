# Display, select from json

## Najprosztrzy listing json wraz ze sformatowaniem
Listuje zawartość JSON
`cat media/grohe_global_import/pl-webprint_20220715-210018.json |jq '.'|less`

## Wyświetlenie zawartości pojedyńczego klucza
Proste filtrowanie po kluczu stringowym z cyframi
`jq '."23996001"'`


## Pobranie kilku elementów ze słownika/ obiektu
Dla pojedyńczego klucza

`cat pl-webprint_20220715-210018.json |jq 'to_entries | map(select(.key=="06170000")) | from_entries'`

`cat pl-webprint_20220715-210019.json |jq 'to_entries | map(select([.key] | inside(["0617000", "06706000", "06707000", "06428000"]))) | from_entries'`

Dla kilku kluczy


## Bardziej zaawansowane filtrowanie
Załóżmy taki json
```json
{
  "values": {
    "root_module": {
      "resources": [
         {
          "address": "aws_iam_access_key.circleci",
          "values": {
            "id": "XXXXXXXXXXXX",
            "secret": "XXXXXXXXXXXX"
          }
        },
        {
          "address": "other",
          "values": {
            "id": "YYYYYYYYY",
            "secret": "YYYYYY"
          }
        }
      ]
    }
  }
}
```
Chcemy tylko te `resources` które spełniają warunek `adres` równa się `aws_iam_access_key.circleci`
`jq '.values.root_module.resources | map(select(.address == "aws_iam_access_key.circleci"))'`
`map` iteruje po liście, `select` wybiera elementy, bez tego dostaniem `true` lub `false`

Przykład zaawansowany
`cat history/nl-webprint_20221111-180011.json |jq 'to_entries | map(select([.key] | inside(["39950000", "23996001", "36325002", "36327002", "36330002", "36439001", "36421001", "36422001" ]))) |  map(.value) | map({"product": .product.material, "etim_class": .sap.A454})' | less`
`to_entries` tworzy listę obiektów z kluczami`key`, `value`,  `map` przetwarza elementy po kolei, `select` wybiera elemety pasujęca do warunku. `inside` sprawdza czy wejściowa tablica zawarta jest w podanej tablicy (czy istnieje ekwiwalen pythonowego `in`?). Na wyjściu jest tablica, `map(.value)` wybiera tylko obiekty z klucza `value` , ostatni `map` tworzy listę obiektów z kluczami `product` i `etim_class` W wyniku otrzymuje
```json
[
  {
    "product": "23996001",
    "etim_class": null
  },
  {
    "product": "36439001",
    "etim_class": null
  },
  {
    "product": "36422001",
    "etim_class": null
  },
  {
    "product": "36421001",
    "etim_class": null
  },
  {
    "product": "36330002",
    "etim_class": null
  },
  {
    "product": "36327002",
    "etim_class": null
  },
  {
    "product": "36325002",
    "etim_class": null
  },
  {
    "product": "39950000",
    "etim_class": "EC011550"
  }
]
```

Funkcja odwrotna do `to_entries` to `from_entries` Poniżej przykład wybrania tylko pasującego elementu objektu
`cat be-webprint_20230224-190014.json | jq 'to_entries | map(select(.key == "34567000")) | from_entries'`
```json
{
  "06170000": {...}
}
```

## Inne narzędzia

Narzędzie do eksploracje JSON
`fx any.json`
Poruszenie przypomina VIM
