# Dokumenty i organizacja indeksu

Dokument Elasticsearch jest obiektem JSON opisującym pojedynczy fragment danych. <a id="term-index"></a>[Indeks](00%20Glossary%20Elasticsearch.md#index) grupuje dokumenty, które mają podobne zastosowanie wyszukiwawcze, ale nie musi być kopią jednej tabeli relacyjnej.

## Struktura dokumentu

Dokument może zawierać pola proste, tablice i obiekty zagnieżdżone:

```json
{
  "name": "John Doe",
  "age": 30,
  "address": {
    "city": "Anytown",
    "country": "US"
  },
  "interests": ["search", "python"]
}
```

Każde pole powinno mieć typ wynikający z operacji, które aplikacja wykona. Tekst do wyszukiwania pełnotekstowego, statusy do dokładnych filtrów, a liczby i daty do zakresów oraz sortowania.

## Obiekt a nested

Zwykły object jest wygodny dla struktur hierarchicznych, ale tablica obiektów może wymagać typu `nested`, gdy trzeba zachować relacje pól tego samego elementu. Jeżeli zapytanie ma łączyć autora i jego kraj, nie dopuść do połączenia autora z kraju innego elementu tablicy.

## Organizacja przez indeksy

Indeks powinien grupować dokumenty, które mają wspólny mapping, cykl życia i sposób wyszukiwania. Nie twórz osobnego indeksu dla każdej drobnej kategorii bez powodu. Nadmiar indeksów i shardów zwiększa koszt klastra.

Dane o bardzo różnych zasadach wyszukiwania lepiej rozdzielić, nawet jeśli pochodzą z jednego systemu źródłowego. Z kolei dokumenty często czytane razem można świadomie zdenormalizować, aby uniknąć kosztownych połączeń po stronie aplikacji.

## Operacje na dokumentach

Dokument można indeksować, odczytywać, aktualizować i usuwać przez jego ID. Search działa na indeksie i może zwrócić wiele dokumentów według query, filtrów i sortowania.

```http
GET products/_doc/book-42

DELETE products/_doc/book-42
```

Biblioteka `elasticsearch-py` udostępnia te same operacje z poziomu Pythona, ale nie zmienia zasad mappingu, refreshu ani wyboru query.

## Co zapamiętać

- Dokument jest JSON-em, a indeks organizuje dokumenty pod wspólny sposób wyszukiwania.
- Obiekty i tablice trzeba projektować z uwzględnieniem semantyki zapytań.
- `nested` jest potrzebny, gdy relacje pól w jednym elemencie tablicy mają znaczenie.
- Indeksy powinny mieć świadomy zakres, mapping i cykl życia.
- Dokument może być zdenormalizowany, jeśli poprawia odczyt i ranking.
