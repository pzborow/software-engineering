# Npm i Node version

Podsumowanie kroków, które należy wykonać, aby zmienić wersje Node.js i npm na twoim komputerze Ubuntu, korzystając z **nvm** (Node Version Manager). Jest to zalecana metoda, ponieważ zapewnia dużą elastyczność i pozwala na łatwe zarządzanie wieloma wersjami Node.js i npm.

### Krok 1: Instalacja nvm

Pierwszym krokiem jest instalacja nvm, która umożliwi łatwe zarządzanie wersjami Node.js. Możesz to zrobić za pomocą jednego z poniższych poleceń w terminalu:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

lub

```bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

Po zakończeniu instalacji, zamknij i otwórz terminal, aby załadować nvm, lub wykonaj:

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```

### Krok 2: Instalacja i użycie odpowiedniej wersji Node.js

Następnie zainstaluj potrzebną wersję Node.js za pomocą nvm. Możesz zainstalować dowolną wersję, którą potrzebujesz:

```bash
nvm install <wersja_node>
nvm use <wersja_node>
```

Na przykład, aby zainstalować i używać wersji 12.22.9, wpisz:

```bash
nvm install 12.22.9
nvm use 12.22.9
```

### Krok 3: Instalacja odpowiedniej wersji npm

Po zainstalowaniu i wybraniu odpowiedniej wersji Node.js, możesz zaktualizować npm do żądanej wersji:

```bash
npm install -g npm@<wersja_npm>
```

Na przykład, aby zainstalować wersję 8.5.1 npm:

```bash
npm install -g npm@8.5.1
```

### Krok 4: Sprawdzenie zainstalowanych wersji

Po zainstalowaniu wersji Node.js i npm, upewnij się, że instalacja przebiegła pomyślnie, sprawdzając ich wersje:

```bash
node -v
npm -v
```

### Krok 5: Ustawienie domyślnej wersji Node.js

Jeśli chcesz, aby określona wersja Node.js była używana domyślnie przy każdym otwarciu terminala, ustaw ją jako domyślną w nvm:

```bash
nvm alias default <wersja_node>
```

Na przykład:

```bash
nvm alias default 12.22.9
```
