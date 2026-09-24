# Search in json files with formatting

`ag 41245000 -l | xargs -I {} sh -c 'echo {}; cat {} | jq '.' | ag 41245000'`