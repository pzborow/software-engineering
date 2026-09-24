# Typowe problemy i dalsza nauka

## Opis

Początkujący najczęściej mylą model RDF z formatem, zasób z tekstem, query endpoint z update endpointem oraz lokalny graf z bazą Fuseki. Nauka powinna przechodzić od trójek do SPARQL i dopiero potem do ontologii oraz wdrożeń.

## Kluczowe koncepty

- **Błąd modelu** — niewłaściwe znaczenie trójek.
- **Błąd serializacji** — niepoprawny zapis formatu.
- **Błąd endpointu** — użycie złego adresu lub operacji.
- **Semantyka** — znaczenie pojęć i relacji.
- **Dokumentacja W3C/Jena** — główne źródła standardów i narzędzi.

## Key points

- Najpierw trzeba rozumieć subject, predicate i object.
- Turtle jest dobrym formatem startowym.
- SPARQL warto ćwiczyć na małym grafie.
- Dokumentacja Apache Jena opisuje Fuseki i protokoły.
- Standardy RDF i SPARQL najlepiej sprawdzać w W3C.

## Example

Jeśli zapytanie nie zwraca wyniku, najpierw sprawdzamy namespace, graf, endpoint i dokładny zapis predicate, zanim zmienimy całe zapytanie.

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Tworzymy kilka prostych trójek.
2. Zapisujemy je w Turtle.
3. Odpy­tujemy lokalnie przez RDFLib.
4. Uruchamiamy Fuseki.
5. Ładujemy ten sam graf.
6. Porównujemy wynik lokalny i zdalny.

## Pytania

1. Jaki błąd jest częsty na początku?
2. Czym różni się model od formatu?
3. Co sprawdzić przy pustym wyniku?
4. Od czego zacząć naukę?
5. Gdzie szukać standardów RDF?
6. Gdzie szukać dokumentacji Fuseki?
7. Czy trzeba od razu zaczynać od ontologii?
8. Dlaczego mały graf jest dobry do nauki?
9. Co może powodować błąd endpointu?
10. Jaki jest sens porównania RDFLib i Fuseki?

## Odpowiedzi

1. Mylenie trójki, formatu i endpointu.
2. Model mówi, co dane znaczą, a format jak są zapisane.
3. Namespace, graf, endpoint i predicate.
4. Od trójek i Turtle.
5. W dokumentacji W3C.
6. Na stronie Apache Jena.
7. Nie.
8. Łatwo ręcznie sprawdzić dane i wyniki.
9. Zły adres, metoda lub typ operacji.
10. Sprawdzenie, czy model działa lokalnie i zdalnie.

[Powrót do spisu treści](README.md)
