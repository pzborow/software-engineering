# Find and Replace in Files

`find ./ -type f -exec sed -i 's/old_string/new_string/g' {} \;`

For global case insensitive:
`find ./ -type f -exec sed -i 's/old_string/new_string/gI' {} \;`

Aby pominąć folder `.git`
`find ./ -type f | grep git/ -v | xargs -i@ sed -i 's/gifts/resumes/g' @`