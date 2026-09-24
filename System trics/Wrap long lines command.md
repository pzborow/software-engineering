# Wrap long lines command

`fold`

Przykłady
`fold -w 80 -s text.txt`
-s tells to break at spaces, and not in words.

`ag 41245000 | fold -w 80 | ag 41245000`

Zobacz także
`fmt`

Przykład
`fmt -w 20 <shxp.txt`