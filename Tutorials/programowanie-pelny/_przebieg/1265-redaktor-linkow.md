# Krok 1265 · redaktor_linków

Węzeł: `review_links` · dział: 4 · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom: początkujący.
Dział 04 „Dane i zmienne” ma linki z fraz do innych miejsc tutorialu. Dla każdego zdecyduj, czy zostaje (keep):
- zostaje, gdy czytelnik w tym miejscu może chcieć sprawdzić cel i po kliknięciu dostanie to, o czym mówi fraza;
- odpada, gdy fraza to ogólnik albo zapowiedź ramowa („na razie nie piszemy kodu”), cel jest przypadkowy albo
  nie mówi tego, co obiecuje fraza, albo link tylko rozprasza.
Nie usuwaj linku tylko dlatego, że cel jest blisko: to już sprawdzono. reason: krótko.

LINKI:
[ref-45] fraza: „wyjaśnimy przy typach danych” (w przód, nazwy rodzajów danych w Pythonie)
  zdanie: Dane trzeba też gdzieś przechowywać, żeby użyć ich więcej niż raz. Do tego służy zmienna, którą poznasz w następnej sekcji. To, jak Python nazywa poszczególne rodzaje danych, wyjaśnimy przy typach danych.
  cel: [Czym jest typ danych] Słowo `class` na razie pomiń, ważna jest nazwa po nim. Oto podstawowe typy Pythona:

[ref-46] fraza: „Pamiętasz, że dane trzeba gdzieś przechowywać” (wstecz, poprzednia sekcja o danych zapowiedziała potrzebę przechowywania danych, czyli zmienną)
  zdanie: Pamiętasz, że dane trzeba gdzieś przechowywać, żeby użyć ich więcej niż raz. Właśnie do tego służy zmienna. Zamiast wpisywać `45.5` w kilku miejscach, nadajesz kwocie nazwę i posługujesz się nią. To trochę jak komórka w arkuszu, którą nazwałeś „kwota”, a potem odwołujesz się do niej po nazwie.
  cel: [Czym jest dana] Dana to każda informacja, na której pracuje program: imię, kwota, data, odpowiedź „tak” lub „nie”. Program bez danych nie miałby czego liczyć ani wypisać. W arkuszu kalkulacyjnym danymi są wartości w komórkach: nazwisko w jednej, kwota w drugiej. W programie jest podobnie, tylko że dane zapisujesz wprost w kodzie albo dostajesz z zewnątrz. ```python # poza kanonem print("Ania") # tekst: imię print(45.5) # liczba: kwota print(True) # prawda albo fałsz: czy zapłaco

[ref-47] fraza: „Dokładniej opiszemy to przy przypisaniu” (w przód, znak = i przypisanie wartości do zmiennej)
  zdanie: Znak `=` nie oznacza tu „równa się” jak w matematyce. Znaczy: „zapisz to, co po prawej, pod nazwą po lewej”. Dokładniej opiszemy to przy przypisaniu.
  cel: [Przypisanie wartości do zmiennej] Zapisujesz je znakiem `=`. Po lewej stoi nazwa, po prawej wartość: `kwota = 45.5`. To nie jest równanie ze szkoły, tylko polecenie: „weź to, co po prawej, i połóż pod nazwą po lewej”. Jeśli zmienna jeszcze nie istniała, Python ją tworzy. Jeśli istniała, podmienia jej wartość, tak jak przy pudełku z etykietą.

[ref-50] fraza: „imię „Ania” nie do podzielenia przez 2” (wstecz, imienia nie da się podzielić przez 2)
  zdanie: Liczbę można podzielić, tekstu nie. To ta sama myśl co imię „Ania” nie do podzielenia przez 2. Python zatrzyma się z komunikatem `TypeError`.
  cel: [Czym jest dana] Każda z tych trzech wartości to jedna dana, ale każda jest innego rodzaju. Rodzaj danej decyduje o tym, co program może z nią zrobić. Do liczby 45.5 da się dodać 10 albo ją podzielić. Imienia „Ania” nie da się podzielić przez 2, bo to nie ma sensu; można je co najwyżej wypisać, porównać z innym albo połączyć z innym tekstem. Prawda lub fałsz odpowiada na pytanie tak/nie.

[ref-52] fraza: „Tym zajmiemy się osobno.” (w przód, łączenie tekstów plusem)
  zdanie: Uwaga na plus: przy liczbach dodaje, a przy tekstach skleja je w jeden. Tym zajmiemy się osobno.
  cel: [Łączenie tekstów] Program łączy teksty operatorem `+`, który skleja je w jeden, dokładnie w takiej kolejności i z takimi znakami, jakie mu podasz. Ta operacja nazywa się sklejaniem tekstów (konkatenacją). Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno, więc oto ono.

[ref-54] fraza: „tak jak `kwota = 45.5` w „Wspólnej Kasie”” (wstecz, zmienna kwota z wcześniejszego przykładu)
  zdanie: W programie ułamek dziesiętny zapisujemy z kropką, nie z przecinkiem, tak jak `kwota = 45.5` w „Wspólnej Kasie”.
  cel: [Czym jest zmienna] Zmienna to nazwane miejsce w pamięci programu, w którym leży jedna dana. Dzięki nazwie możesz tę daną wielokrotnie odczytać, użyć w obliczeniach albo zastąpić inną. Pamiętasz, że dane trzeba gdzieś przechowywać, żeby użyć ich więcej niż raz. Właśnie do tego służy zmienna. Zamiast wpisywać `45.5` w kilku miejscach, nadajesz kwocie nazwę i posługujesz się nią. To trochę jak komórka w arkuszu, którą nazwałeś „kwota”, a potem odwołujesz się do niej po nazwie. ```python imie =

[ref-55] fraza: „Wcześniej pisaliśmy po prostu „rodzaj danych”” (wstecz, wcześniejsze określenie „rodzaj danych” użyte w dziale o danych)
  zdanie: Typ danych to rodzaj wartości, który mówi Pythonowi, czym ta wartość jest i jakie działania są na niej dozwolone. Wcześniej pisaliśmy po prostu „rodzaj danych”, teraz mamy na to fachową nazwę.
  cel: [Czym jest dana] Dana to każda informacja, na której pracuje program: imię, kwota, data, odpowiedź „tak” lub „nie”. Program bez danych nie miałby czego liczyć ani wypisać. W arkuszu kalkulacyjnym danymi są wartości w komórkach: nazwisko w jednej, kwota w drugiej. W programie jest podobnie, tylko że dane zapisujesz wprost w kodzie albo dostajesz z zewnątrz. ```python # poza kanonem print("Ania") # tekst: imię print(45.5) # liczba: kwota print(True) # prawda albo fałsz: czy zapłaco

[ref-56] fraza: „tylko cztery znaki: 4, 5, kropka, 5” (wstecz, "45.5" w cudzysłowie to tekst, nie kwota)
  zdanie: Typ ma każda wartość, także ta ukryta w zmiennej. Python rozpoznaje go po zapisie: cudzysłów oznacza tekst, cyfry z kropką ułamek, a `True` lub `False` prawdę albo fałsz. Dlatego `"45.5"` to tylko cztery znaki: 4, 5, kropka, 5, a nie pieniądze. Typ sprawdzisz funkcją `type()`.
  cel: [Liczba a tekst] Liczba to wartość, na której program liczy. Tekst to ciąg znaków, który program przechowuje, wypisuje, porównuje i skleja. Zapis decyduje o tym, z czym mamy do czynienia: `45.5` bez cudzysłowu to liczba, a `"45.5"` w cudzysłowie to tekst, czyli cztery znaki: 4, 5, kropka, 5.

[ref-57] fraza: „imienia nie podzielisz przez 2” (wstecz, imienia nie da się podzielić)
  zdanie: Typ decyduje o tym, co program może zrobić z wartością. Dlatego imienia nie podzielisz przez 2, a kwotę tak. Typem `bool` zajmiemy się osobno, w kolejnej sekcji.
  cel: [Czym jest dana] Każda z tych trzech wartości to jedna dana, ale każda jest innego rodzaju. Rodzaj danej decyduje o tym, co program może z nią zrobić. Do liczby 45.5 da się dodać 10 albo ją podzielić. Imienia „Ania” nie da się podzielić przez 2, bo to nie ma sensu; można je co najwyżej wypisać, porównać z innym albo połączyć z innym tekstem. Prawda lub fałsz odpowiada na pytanie tak/nie.

[ref-59] fraza: „Ta sama zasada, co przy `"45.5"`” (wstecz, cudzysłów zmienia wartość w tekst)
  zdanie: Zapisuje się je z wielkiej litery i bez cudzysłowu. Ta sama zasada, co przy `"45.5"`: `True` to wartość logiczna, a `"True"` w cudzysłowie to tylko tekst z czterech liter.
  cel: [Liczba a tekst] Liczba to wartość, na której program liczy. Tekst to ciąg znaków, który program przechowuje, wypisuje, porównuje i skleja. Zapis decyduje o tym, z czym mamy do czynienia: `45.5` bez cudzysłowu to liczba, a `"45.5"` w cudzysłowie to tekst, czyli cztery znaki: 4, 5, kropka, 5.

[ref-60] fraza: „Zmienną logiczną podmieniasz jak każdą inną: po drugim przypisaniu `True` znika” (wstecz, podmiana wartości zmiennej, tak jak przy zmianie kwoty)
  zdanie: Zmienną logiczną podmieniasz jak każdą inną: po drugim przypisaniu `True` znika, a jej miejsce zajmuje `False`.
  cel: [Czym jest zmienna] Wartość zmiennej może się zmieniać w trakcie działania programu, stąd nazwa: po `kwota = 60` stara kwota znika, a nowa zajmuje jej miejsce. Nazwa zostaje ta sama. W „Wspólnej Kasie” takie zmienne w `rozlicz.py` opisują pojedynczy wydatek: kto zapłacił, ile i czy już się rozliczył.

[ref-61] fraza: „Jak to zapisać, pokażemy przy instrukcji warunkowej” (w przód, zapisywanie decyzji na podstawie wartości logicznej)
  zdanie: Konsekwencja: taka wartość służy programowi do podejmowania decyzji. Na podstawie `zaplacono` program będzie mógł wybrać, czy przypomnieć o długu. Jak to zapisać, pokażemy przy instrukcji warunkowej.
  cel: [Instrukcja warunkowa „jeśli… to…”] Warunek to zwykle porównanie z poprzedniej sekcji, bo daje `True` albo `False`. Jeśli wynik to `True`, Python wykonuje zapisane pod spodem linie. Jeśli `False`, pomija je i idzie dalej.

[ref-62] fraza: „tak jak przy pudełku z etykietą” (wstecz, model zmiennej jako pudełka z etykietą, w którym wartość można podmienić)
  zdanie: Zapisujesz je znakiem `=`. Po lewej stoi nazwa, po prawej wartość: `kwota = 45.5`. To nie jest równanie ze szkoły, tylko polecenie: „weź to, co po prawej, i połóż pod nazwą po lewej”. Jeśli zmienna jeszcze nie istniała, Python ją tworzy. Jeśli istniała, podmienia jej wartość, tak jak przy pudełku z etykietą.
  cel: [Zmienna jako pudełko z etykietą] Zmienną można porównać do pudełka z etykietą: etykieta to nazwa, a w środku leży jedna dana, czyli wartość zmiennej (to, co aktualnie jest w pudełku). Program szuka pudełka po etykiecie i zagląda do środka. ```text etykieta: kwota etykieta: imie ┌──────────┐ ┌──────────┐ │ 45.5 │ │ "Ania" │ └──────────┘ └──────────┘ ``` Porównanie tłumaczy trzy rzeczy. Pudełko mieści jedną wartość naraz, więc nowa wartość wypiera star
````

## Odpowiedź

````json
{
  "items": [
    {
      "id": "ref-45",
      "keep": true,
      "reason": "Zapowiedź konkretnej treści: cel wprowadza nazwy typów Pythona."
    },
    {
      "id": "ref-46",
      "keep": false,
      "reason": "Cel to definicja danej, nie mówi o potrzebie przechowywania; zdanie i tak wyjaśnia to samo."
    },
    {
      "id": "ref-47",
      "keep": true,
      "reason": "Cel dokładnie opisuje przypisanie znakiem =, jak obiecuje fraza."
    },
    {
      "id": "ref-50",
      "keep": true,
      "reason": "Cel zawiera dokładnie ten przykład z imieniem Ania i dzieleniem przez 2."
    },
    {
      "id": "ref-52",
      "keep": true,
      "reason": "Cel to sekcja o łączeniu tekstów plusem, dokładnie to, co zapowiada fraza."
    },
    {
      "id": "ref-54",
      "keep": false,
      "reason": "Cel to ogólna definicja zmiennej; nie pokazuje kwota = 45.5 w Wspólnej Kasie, a czytelnik nie potrzebuje sprawdzać."
    },
    {
      "id": "ref-55",
      "keep": false,
      "reason": "Cel to definicja danej, a fraza odsyła do wcześniejszego sformułowania „rodzaj danych”; cel wprawdzie o rodzaju mówi, ale link tylko rozprasza przy definicji typu."
    },
    {
      "id": "ref-56",
      "keep": true,
      "reason": "Cel wyjaśnia różnicę między 45.5 a \"45.5\" tymi samymi słowami."
    },
    {
      "id": "ref-57",
      "keep": false,
      "reason": "Duplikat myśli z ref-50 w pobliżu; link powtarza ten sam cel i rozprasza."
    },
    {
      "id": "ref-59",
      "keep": true,
      "reason": "Cel wyjaśnia zasadę cudzysłowu, do której odwołuje się fraza."
    },
    {
      "id": "ref-60",
      "keep": true,
      "reason": "Cel mówi wprost o podmianie wartości zmiennej (kwota = 60)."
    },
    {
      "id": "ref-61",
      "keep": true,
      "reason": "Cel to instrukcja warunkowa, o której mówi fraza."
    },
    {
      "id": "ref-62",
      "keep": false,
      "reason": "Fraza stoi zaraz po opisie podmiany wartości; cel to model pudełka, ale link jest w zdaniu tłumaczącym to samo i tylko odsyła w bok."
    }
  ]
}
````
