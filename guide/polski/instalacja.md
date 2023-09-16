<img align="right" src="https://github.com/ETCHDEV/Port-Windows-11-Xiaomi-11-Lite-NE/blob/main/lisa.png" width="250" alt="Windows 11 działający na Mi 11 Lite NE">.


# Uruchamianie systemu Windows na Mi 11 Lite NE/Mi 11 LE

## Instalacja systemu Windows

### Wymagania wstępne

- [Obraz Windows na ARM (zalecany Windows 11)](https://uupdump.net/)
- Najnowszy obraz UEFI skompilowany z kodu źródłowego edk2-msm](https://github.com/edk2-porting/edk2-msm)
- [Obraz UEFI do TYLKO instalacji systemu Windows!!!](https://github.com/ETCHDEV/Port-Windows-11-Xiaomi-11-Lite-NE/releases/download/v0.0.1/boot-lisa-install.img)
- [DriverUpdater](https://github.com/WOA-Project/DriverUpdater/releases/latest)
- [Sterowniki](https://github.com/Icesito68/7xx-Drivers) (kliknij strzałkę Pobierz kod i pobierz jako zip)

#### Uruchom telefon ze zmodyfikowanego obrazu UEFI za pomocą następującego polecenia:
``cmd
fastboot boot boot-lisa-install.img
```
#### Po uruchomieniu do UEFI, wybierz menu rozruchowe UEFI, a następnie wybierz ostatnią opcję (opcja SCSI Disk)

### Przypisywanie liter do dysków
#### Uruchom menedżera dysków Windows z CMD jako administrator
> Gdy Mi 11 Lite NE zostanie wykryty jako dysk SCSI

``cmd
diskpart
```

### Przypisywanie litery montażowej do woluminów Windows i BOOT

#### Wybierz wolumin Windows telefonu
> Użyj `list volume`, aby go znaleźć, jest to ten o nazwie "WINLISA". Zwróć uwagę na numer woluminu.
``diskpart
wybierz wolumin <numer>
assign letter=w
```
#### Teraz wybierz głośność ESP telefonu
> Użyj `list volume`, aby go znaleźć, jest to ten o nazwie "ESPLISA". Zwróć uwagę na numer woluminu.

``diskpart
wybierz wolumin <numer>
assign letter=s
```
#### Teraz zamknij diskpart
``diskpart
exit
```

### Instalacja
> Zastąp `<path/to/install.wim>` rzeczywistą ścieżką do pliku install.wim, 
> `install.wim` znajduje się w folderze sources wewnątrz ISO (może być również nazwany `install.esd`), 
> Można go uzyskać poprzez zamontowanie lub rozpakowanie ISO.

> Ponieważ dotyk na urządzeniu nie działa, musisz użyć narzędzi takich jak NTlite, aby edytować ISO w celu utworzenia lokalnego konta administracyjnego.

``cmd
dism /apply-image /ImageFile:<ścieżka/do/install.wim> /index:1 /ApplyDir:W:\
```

### Tworzenie plików bootloadera Windows

``cmd
bcdboot W:\Windows /s S: /f UEFI
```

### Zainstaluj sterowniki

> Zastąp `<lisadriversfolder>` rzeczywistą lokalizacją folderu sterowników.

>Rozpakuj pobrany plik zip 
``cmd
.\driverupdater.exe -d <lisadriversfolder>\definitions\Desktop\ARM64\Internal\lisa.txt -r <lisadriversfolder> -p W:
```
  
## Zezwalaj na niepodpisane sterowniki

> Jeśli tego nie zrobisz, otrzymasz BSOD

> S: jest partycją ESP
``cmd
cd S:\EFI\Microsoft\Boot
bcdedit /store BCD /set "{default}" testingigning on
bcdedit /store BCD /set "{default}" nointegritychecks on
bcdedit /store BCD /set "{default}" recoveryenabled no
bcdedit /store BCD /set "{default}" bootstatuspolicy IgnoreAllFailures
```

### Unassign disk letters
> Aby nie pozostały tam po odłączeniu urządzenia

Otwórz CMD jako administrator:
``cmd
diskpart
```

#### Nieprzypisywanie woluminów telefonu:
> Użyj `list volume` aby go znaleźć, jest to ten o nazwie "WINLISA"

``diskpart
wybierz wolumin <numer>
usuń literę w
```

#### Teraz wybierz głośność ESP telefonu
> Użyj `list volume`, aby go znaleźć, jest to ten o nazwie "ESPLISA".

``diskpart
select volume <numer>
usuń literę s
```

#### Exit diskpart
``diskpart
exit
```

## Uruchom system Windows
### Teraz uruchom najnowszy skompilowany img UEFI:
``cmd
fastboot boot boot-lisa.img
```

### Wybierz pierwszą opcję systemu Windows do uruchomienia

### Jeśli Windows zrestartował się po instalacji androida, po prostu przejdź do fastboot i uruchom img.
(Nie polecam flashowania uefi img do rozruchu, ponieważ obecnie nie ma wsparcia dla większości urządzeń i ich sterowników)

### Możesz uruchamiać programy umieszczając skrypt wsadowy w folderze startowym.

## Gotowe!
