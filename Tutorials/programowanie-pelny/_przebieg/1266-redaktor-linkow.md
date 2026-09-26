# Krok 1266 · redaktor_linków

Węzeł: `review_links` · dział: 5 · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom: początkujący.
Dział 05 „Operacje i decyzje” ma linki z fraz do innych miejsc tutorialu. Dla każdego zdecyduj, czy zostaje (keep):
- zostaje, gdy czytelnik w tym miejscu może chcieć sprawdzić cel i po kliknięciu dostanie to, o czym mówi fraza;
- odpada, gdy fraza to ogólnik albo zapowiedź ramowa („na razie nie piszemy kodu”), cel jest przypadkowy albo
  nie mówi tego, co obiecuje fraza, albo link tylko rozprasza.
Nie usuwaj linku tylko dlatego, że cel jest blisko: to już sprawdzono. reason: krótko.

LINKI:
[ref-64] fraza: „Skoro `nazwa_wyjazdu` jest tekstem” (wstecz, zmienna z wcześniejszego przykładu, której tu nie zdefiniowano; sens zbliżony do faktu, że tekstu nie da się dzielić)
  zdanie: Odejmowanie, dzielenie, `//`, `%` i `**` mają sens tylko na liczbach. Skoro `nazwa_wyjazdu` jest tekstem, `nazwa_wyjazdu / 2` kończy się błędem `TypeError`. Wyjątkiem są `+` i `*`, które na tekście działają inaczej: sklejają i powtarzają.
  cel: [Czym jest dana] Każda z tych trzech wartości to jedna dana, ale każda jest innego rodzaju. Rodzaj danej decyduje o tym, co program może z nią zrobić. Do liczby 45.5 da się dodać 10 albo ją podzielić. Imienia „Ania” nie da się podzielić przez 2, bo to nie ma sensu; można je co najwyżej wypisać, porównać z innym albo połączyć z innym tekstem. Prawda lub fałsz odpowiada na pytanie tak/nie.

[ref-65] fraza: „Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno” (wstecz, sklejanie tekstów plusem zapowiedziane przy działaniach matematycznych)
  zdanie: Program łączy teksty operatorem `+`, który skleja je w jeden, dokładnie w takiej kolejności i z takimi znakami, jakie mu podasz. Ta operacja nazywa się sklejaniem tekstów (konkatenacją). Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno, więc oto ono.
  cel: [Działania matematyczne w programie] Program wykonuje te same działania co kalkulator: dodawanie, odejmowanie, mnożenie i dzielenie, a do tego dzielenie całkowite, resztę z dzielenia i potęgowanie. Zapisujesz je za pomocą operatorów arytmetycznych, czyli znaków, które mówią Pythonowi, jakie działanie wykonać na liczbach. | Działanie | Operator | |---|---| | dodawanie | `+` | | odejmowanie | `-` | | mnożenie | `*` | | dzielenie | `/` | | dzielenie całkowite | `//` | | reszta z dzielenia | `%` | | potęgowan

[ref-67] fraza: „pojedynczy znak `=` to przypisanie” (wstecz, przypisanie jako zapisanie wartości w zmiennej)
  zdanie: Uwaga na `==`: pojedynczy znak `=` to przypisanie, czyli zapisanie wartości w zmiennej. Dopiero podwójny pyta „czy są równe?” i niczego nie zmienia.
  cel: [Przypisanie wartości do zmiennej] Przypisanie to instrukcja, która zapisuje wartość pod nazwą zmiennej. Dzięki niej program zapamiętuje daną i może do niej wrócić w dalszej części kodu. Zapisujesz je znakiem `=`. Po lewej stoi nazwa, po prawej wartość: `kwota = 45.5`. To nie jest równanie ze szkoły, tylko polecenie: „weź to, co po prawej, i połóż pod nazwą po lewej”. Jeśli zmienna jeszcze nie istniała, Python ją tworzy. Jeśli istniała, podmienia jej wartość, tak jak przy pudełku z etykietą. Przypisanie działa o

[ref-68] fraza: „Tekst `"45.5"` i liczba 45.5 to różne typy” (wstecz, tekst w cudzysłowie to nie liczba)
  zdanie: Dwa ostatnie wyniki pokazują, że porównanie jest ścisłe. Wielka i mała litera to różne znaki, więc `"Ania"` i `"ania"` się różnią. Tekst `"45.5"` i liczba 45.5 to różne typy, więc też nie są równe, choć wyglądają podobnie.
  cel: [Liczba a tekst] Liczba to wartość, na której program liczy. Tekst to ciąg znaków, który program przechowuje, wypisuje, porównuje i skleja. Zapis decyduje o tym, z czym mamy do czynienia: `45.5` bez cudzysłowu to liczba, a `"45.5"` w cudzysłowie to tekst, czyli cztery znaki: 4, 5, kropka, 5.

[ref-70] fraza: „porównanie z poprzedniej sekcji” (wstecz, operatory porównania dające True lub False)
  zdanie: Warunek to zwykle porównanie z poprzedniej sekcji, bo daje `True` albo `False`. Jeśli wynik to `True`, Python wykonuje zapisane pod spodem linie. Jeśli `False`, pomija je i idzie dalej.
  cel: [Porównywanie wartości] Program porównuje wartości operatorami porównania. To znaki takie jak `==` czy `>`, które zestawiają dwie wartości i zwracają wynik `True` albo `False`, czyli wartość logiczną. | Zapis | Znaczenie | |---|---| | `a == b` | równe | | `a != b` | różne | | `a < b`, `a > b` | mniejsze, większe | | `a <= b`, `a >= b` | mniejsze lub równe, większe lub równe | Uwaga na `==`: pojedynczy znak `=` to przypisanie, czyli zapisanie wartości w zmiennej. Dopier

[ref-72] fraza: „jak w poprzedniej sekcji, działa zawsze” (wstecz, ostatni print bez wcięcia wykonuje się zawsze)
  zdanie: Warunek `kwota > 100` jest fałszywy, więc Python pominął pierwszy wcięty blok i wykonał ten pod `else`. Gdyby kwota wynosiła 150, wypisałoby się tylko „Bardzo duża kwota”. Oba bloki nigdy nie wykonają się naraz. Ostatni `print` nie ma wcięcia, więc, jak w poprzedniej sekcji, działa zawsze.
  cel: [Instrukcja warunkowa „jeśli… to…”] Pierwszy warunek jest prawdziwy, więc jego linia się wykonała. Drugi jest fałszywy, więc jego wcięta linia została pominięta. Ostatni `print` nie ma wcięcia, więc należy do całego programu i wykonuje się zawsze.

[ref-74] fraza: „tak jak w porównywaniu wartości” (wstecz, pełny zapis warunku porównania po obu stronach and/or)
  zdanie: Każdy z połączonych warunków zapisujemy w całości, tak jak w porównywaniu wartości. Wynik można wypisać albo wstawić do `if`:
  cel: [Porównywanie wartości] Program porównuje wartości operatorami porównania. To znaki takie jak `==` czy `>`, które zestawiają dwie wartości i zwracają wynik `True` albo `False`, czyli wartość logiczną. | Zapis | Znaczenie | |---|---| | `a == b` | równe | | `a != b` | różne | | `a < b`, `a > b` | mniejsze, większe | | `a <= b`, `a >= b` | mniejsze lub równe, większe lub równe | Uwaga na `==`: pojedynczy znak `=` to przypisanie, czyli zapisanie wartości w zmiennej. Dopier
````

## Odpowiedź

````json
{
  "items": [
    {
      "id": "ref-64",
      "keep": false,
      "reason": "Cel to ogólne omówienie rodzajów danych; fraza jest nawiązaniem do zmiennej, nie obietnicą konkretnej treści."
    },
    {
      "id": "ref-65",
      "keep": false,
      "reason": "Cel to tabela działań matematycznych, a w niej nie ma sklejania tekstów obiecanego przez frazę."
    },
    {
      "id": "ref-67",
      "keep": true,
      "reason": "Cel wyjaśnia przypisanie `=`, czyli dokładnie to, co mówi fraza."
    },
    {
      "id": "ref-68",
      "keep": true,
      "reason": "Cel tłumaczy różnicę między `45.5` a `\"45.5\"`, więc pasuje do frazy."
    },
    {
      "id": "ref-70",
      "keep": true,
      "reason": "Cel to omówienie operatorów porównania dających True/False; czytelnik może chcieć je sprawdzić."
    },
    {
      "id": "ref-72",
      "keep": true,
      "reason": "Cel pokazuje, że ostatni print bez wcięcia wykonuje się zawsze, jak mówi fraza."
    },
    {
      "id": "ref-74",
      "keep": true,
      "reason": "Cel podaje pełny zapis porównań, do którego odsyła fraza."
    }
  ]
}
````
