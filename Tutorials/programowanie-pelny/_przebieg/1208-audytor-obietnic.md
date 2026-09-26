# Krok 1208 · audytor_obietnic

Węzeł: `settle_promises` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem obietnic w tutorialu: Programowanie od podstaw. Wcześniej w tekście padła obietnica:
„Usuwamy ją w warsztacie poniżej.” (zapowiedź poprawienia błędnej ostatniej linii w warsztacie).
Która z dalszych sekcji ją spełnia? Podaj section_id albo zostaw puste, gdy żadna.

DALSZE SEKCJE:
[sec-08-dane-wejsciowe-programu] Dane wejściowe programu (dział 08): Dane wejściowe to wartości przychodzące do programu z zewnątrz (od użytkownika, z pliku, z innego programu), dzięki czemu kod zostaje ten sam, a dane się zmieniają.
[sec-08-dane-wyjsciowe-programu] Dane wyjściowe programu (dział 08): Dane wyjściowe to wynik, który program oddaje na zewnątrz (ekran, plik, inny program), a dobre wyjście jest opisane tak, by zrozumiał je człowiek.
[sec-08-pytanie-uzytkownika-o-informacje] Pytanie użytkownika o informację (dział 08): Funkcja input wypisuje pytanie i zwraca odpowiedź użytkownika zawsze jako tekst, więc liczbę trzeba zamienić przez float().
[sec-08-czym-jest-plik] Czym jest plik (dział 08): Plik przechowuje dane na dysku po zakończeniu programu, a program otwiera go przez open (najlepiej z with) w trybie czytania, zapisu lub dopisywania i pamięta, że dostaje z niego tekst.
[sec-08-czym-jest-interfejs-uzytkownika] Czym jest interfejs użytkownika (dział 08): Interfejs użytkownika to wszystko, przez co człowiek rozmawia z programem: pytania, które program zadaje, i wyniki, które pokazuje, więc powinny być jasne dla kogoś, kto nie zna kodu.
[sec-08-po-co-sprawdzac-dane-uzytkownika] Po co sprawdzać dane użytkownika (dział 08): Sprawdzaj dane od użytkownika zaraz po wpisaniu, bo człowiek może wpisać coś nieoczekiwanego, a zły wpis powinien dostać komunikat i drugą szansę.
[sec-09-blad-skladni-a-blad-logiczny] Błąd składni a błąd logiczny (dział 09): Błąd składni zatrzymuje program przed startem z komunikatem, a błąd logiczny daje po cichu zły wynik, który musisz wychwycić sam.
[sec-09-jak-czytac-komunikat-o-bledzie] Jak czytać komunikat o błędzie (dział 09): Komunikat czytaj od dołu: ostatnia linia mówi, co się stało, a ślad nad nią wskazuje plik i numer linii, gdzie to szukać.
[sec-09-czym-jest-testowanie-programu] Czym jest testowanie programu (dział 09): Test to zapisane oczekiwanie: znasz poprawny wynik z góry, a komputer sprawdza go za Ciebie po każdej zmianie kodu.
[sec-09-czym-jest-debugowanie] Czym jest debugowanie (dział 09): Debugowanie to zawężanie miejsca błędu przez sprawdzanie, co program faktycznie robi, np. wartości wypisane przez print, aż znajdziesz pierwszy krok, w którym rzeczywistość rozjeżdża się z oczekiwaniem.
[sec-09-po-co-zapisywac-wersje-kodu] Po co zapisywać wersje kodu (dział 09): Commit zapisuje działającą wersję kodu z opisem, dzięki czemu zawsze możesz do niej wrócić i sprawdzić, kiedy coś się zepsuło.
[sec-09-szukanie-rozwiazan-w-internecie] Szukanie rozwiązań w internecie (dział 09): Szukaj po ostatniej linii komunikatu i nazwie języka, oceniaj źródła i nigdy nie wklejaj skopiowanego kodu bez zrozumienia.
[sec-10-programy-uzywane-na-co-dzien] Programy używane na co dzień (dział 10): Programy, których używasz codziennie, to te same proste klocki (dane, decyzje, pętle, funkcje, pliki) w większej skali i z ładniejszym interfejsem.
[sec-10-strona-internetowa-a-aplikacja-mobilna] Strona internetowa a aplikacja mobilna (dział 10): Strona otwiera się w przeglądarce bez instalacji, a aplikacja mobilna jest zainstalowana w telefonie i lepiej korzysta z jego możliwości, ale obie działają według schematu wejście, przetwarzanie, wyjście.
[sec-10-od-pomyslu-do-dzialajacego-programu] Od pomysłu do działającego programu (dział 10): Buduj program małymi kawałkami: opisz, napisz, sprawdź, zapisz commit, dopiero potem dokładaj następny.
[sec-10-umiejetnosci-poza-kodowaniem] Umiejętności poza kodowaniem (dział 10): Pisanie kodu to część pracy programisty; równie ważne są rozumienie problemu, komunikacja, cierpliwość i umiejętność uczenia się.
[sec-10-od-czego-zaczac-nauke] Od czego zacząć naukę (dział 10): Naukę zacznij od jednego małego, własnego problemu i jednego języka, a kod pisz i uruchamiaj regularnie, po kawałku.
[sec-10-automatyzacja-prostych-zadan] Automatyzacja prostych zadań (dział 10): Automatyzuj małe, częste zadania o jasnych regułach: raz opisane w pętli i funkcji działają tak samo dla trzech danych i dla tysiąca.
````

## Odpowiedź

````json
{
  "section_id": "sec-09-czym-jest-debugowanie"
}
````
