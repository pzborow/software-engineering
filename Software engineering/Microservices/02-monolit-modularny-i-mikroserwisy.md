# Monolit, modularny monolit i mikroserwisy

<a id="term-monolit"></a>[Monolit](00-glosariusz.md#monolit) to system wdrażany jako jedna całość. Nie musi być zły. Ma prostsze uruchamianie, prostsze debugowanie, zwykle prostsze transakcje i mniej problemów operacyjnych niż system rozproszony.

Najczęściej pierwszym celem powinien być <a id="term-modularny-monolit"></a>[modularny monolit](00-glosariusz.md#modularny-monolit). To nadal jedna aplikacja i jedno wdrożenie, ale z wyraźnymi modułami, granicami zależności i regułami komunikacji wewnętrznej. Taki system pozwala uczyć się granic domeny bez kosztów sieci i wielu pipeline'ów.

Mikroserwisy warto rozważyć, gdy różne części systemu mają różne tempo zmian, różne wymagania skalowania, różne ryzyka lub są rozwijane przez niezależne zespoły. Jeżeli jeden mały zespół tworzy jeden produkt, mikroserwisy często dodają więcej pracy niż wartości.

Mikroserwisy nie rozwiązują chaosu projektowego. Jeśli zespół nie umie utrzymać granic w monolicie, to w systemie rozproszonym zwykle przeniesie chaos do sieci. Wtedy zamiast modularności powstaje trudniejsza wersja tego samego problemu.

Wybór architektury powinien wynikać z presji biznesowej, nie z mody. Pytanie nie brzmi „czy mikroserwisy są nowoczesne?”, tylko „czy koszt niezależnych usług jest mniejszy niż koszt dalszego rozwijania jednej aplikacji?”.

## Kiedy mikroserwisy mają sens

- kilka zespołów musi pracować niezależnie nad różnymi obszarami,
- fragmenty systemu mają różne wymagania skalowania lub dostępności,
- domena ma wyraźne granice odpowiedzialności,
- organizacja ma dojrzałe CI/CD, monitoring i praktyki operacyjne,
- koszt koordynacji w monolicie jest większy niż koszt rozproszenia.

## Kiedy nie warto

- domena jest jeszcze słabo poznana,
- system buduje jeden mały zespół,
- brakuje automatyzacji wdrożeń i obserwowalności,
- głównym problemem jest bałagan w kodzie, a nie realna potrzeba niezależności,
- zespół oczekuje transakcji i prostego debugowania jak w jednej aplikacji.

## Co zapamiętać

- Monolit nie jest porażką, jeśli jest modularny i utrzymywalny.
- Mikroserwisy są narzędziem do zarządzania niezależnością, nie lekiem na każdy system.
- Zły monolit po rozbiciu często staje się złym systemem rozproszonym.
