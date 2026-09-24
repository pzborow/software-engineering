# Zrobienie targz na zdalny serwerze z lokalnych plików

`tar czf - /ścieżka/do/lokalnych/plików | ssh użytkownik@zdalny_host "cat > /ścieżka/na/serwerze/plik.tar.gz"`

`tar czf - /ścieżka/do/lokalnych/plików`: Polecenie tar tworzy skompresowane archiwum (tar.gz) i wypisuje je na standardowe wyjście (stdout) zamiast zapisywać na dysk.
`ssh użytkownik@zdalny_host`: Polecenie ssh służy do zalogowania się na zdalny serwer.
``"cat > /ścieżka/na/serwerze/plik.tar.gz"``: Po stronie zdalnej cat odbiera dane przesłane przez ssh i zapisuje je bezpośrednio do pliku na zdalnym serwerze.