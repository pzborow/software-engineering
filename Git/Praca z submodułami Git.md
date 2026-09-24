# Praca z submodułami Git

Dodawanie
`git submodule add git@gitlab.roza.dev:framework/exporters.git`

Kasowanie
Delete the relevant line from the .gitmodules file.
Delete the relevant section from .git/config.
Run` git rm --cached pathtosubmodule` (no trailing slash).
Commit the superproject.
Delete the now untracked submodule files.

Klonowanie
`git clone --recurse-submodules`

`git submodule update --init --recursive`