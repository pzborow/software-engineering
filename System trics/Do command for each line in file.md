# Do command for each line in file

`<file xargs -I % curl %`

`<file xargs -I % curl http://example.com/persons/%.tar`

`cat eans.txt |  xargs -I % ag %`

`cat eans.txt |  xargs -I % sh -c "echo %; ag \"%\" -l"`

[source](https://unix.stackexchange.com/questions/3593/using-xargs-with-input-from-a-file)