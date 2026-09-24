# Tmux with session name

Podłączenie do istniejącej sesji 
`tmux attach -t etim`

Tworzenie sesji o zadanej nazwie
W terminalu  `tmux new -s etim` , bez przełączania sessji, czyli można użyć wewnątrze tmux `tmux new -s name -d`
W istniejącej sesjii `Ctrl-B :new -s <name>`

Wylistowanie sesji
W terminalu `tmux list-sessions` lub `tmux ls`, aby się przełączyć w trakcie `Ctrl+B, s`

Zmiana nazwy w podłączonej sesji
Przejść do list poleceń wewnątrz tmux, `Prefix, :`, zwyczajowo `Ctrl+B, :`
`rename-session new-session-name`

Zmiana nazwy przed podłączeniem
`tmux rename-session -t old-session-name new-session-name`

Tmux, nie jest dostarczony z podpowiadaniem w bash, aby stało się to możliwe
`https://unix.stackexchange.com/questions/604554/what-allows-bash-to-autocomplete-tmux-sub-commands`
[source](https://unix.stackexchange.com/questions/604554/what-allows-bash-to-autocomplete-tmux-sub-commands)

[tricks](https://stackoverflow.com/questions/16398850/create-new-tmux-session-from-inside-a-tmux-session)

Sesja ssh z domyślnym startem tmux
```
Host tmux.pzdevel
    HostName pzdevel
    User pzborow
	RequestTTY yes 
    RemoteCommand tmux new -A -s default
```