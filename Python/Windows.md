# Windows

Ustawić `path`
`%USERPROFILE%\AppData\Local\Programs\Python\Python312`

Wyświetlić ścieżkę powershell
`echo $env:path`

Virtualenv
`pip install virtualenv`

W projekcie
`virtualenv env`

Aktywacja
`env\Scripts\activate.bat`

Aplikacja bez konsoli, same okna
`*.pyw`

W power shell 
```
start .\MyCoolbmp.bmp
#Opens in MSPaint

start .\SomeNotes.txt
#Opens in Notepad

start .\SomeJason.json
#Opens in Visual Studio, go ahead and grab a coffee...
```

Uruchomienie notepad++
`start notepad++ .\demo.pyw`

Powershell i aliasy
`Set-Alias -Value 'C:\Program Files\Notepad++\notepad++.exe' -Name 'NotePad'`
`Set-Alias -Value 'C:\Program Files\Notepad++\notepad++.exe' -Name 'edit'`
`Set-Alias -Value 'C:\Program Files (x86)\FreeCommander XE\FreeCommander.exe' -Name 'FreeCommander'`
`Set-Alias -Value 'C:\Program Files\Double Commander' -Name 'DoubleCommander'`
`Set-Alias -Value 'C:\Program Files\Double Commander' -Name 'doublecmd'`

Aby było te pernamente
`notepad $profile`

Gdy nie można uruchomić ps1, to uruchomić PowerShell jako administrator i
`Set-ExecutionPolicy RemoteSigned`
W przypadku gdy nie można jako administrator
`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`
To też rozwiązuje problem z `.\env\Scripts\activate`

Otwarcie eplorera
`explorer .`

Wygląda, że linki działają
```
mklink <c:\nameoflinktocreate> <c:\alreadyexistingFILE>
mklink /d <c:\nameoflinktocreate> <c:\alreadyexistingFOLDER>
```

Wskazania na systemowe foldery
`$env:userprofile\Downloads`
`$env:userprofile\Documents`
				