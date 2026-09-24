# Git clean all unnecessarily files

Usuwa nieśledzone pliki
`git clean -fx`

Resetuje stan plików do gałęzi 	bieżącej gałęzi
`git reset --hard`

To remove directories, run `git clean -f -d` or `git clean -fd`
To remove ignored files, run `git clean -f -X` or `git clean -fX`
To remove ignored and non-ignored files, run `git clean -f -x` or `git clean -fx`