# LVM Extend Resize Virtual

Rozszeżenie dysku virtualnego
`vgdisplay` Sprawdzenie dostępnego miejsca na Volume Group aby odczytać odczytać ile jest wolnej przestrzeni (Free PE/Size)

`lvdisplay`  aby sprawdzić rozmiar Logical Volume

Zwiększenie na 100 dostępnej przestrzeni
`lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv`

`lvdisplay`  ponowne sprawdzenie Logical Volume

`resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv`

Jak rozszeżyć virtualny dysk i dostosować partycje można doczytać [tu](https://packetpushers.net/ubuntu-extend-your-default-lvm-space/)