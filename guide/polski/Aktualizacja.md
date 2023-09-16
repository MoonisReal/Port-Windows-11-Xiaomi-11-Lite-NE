<img align="right" src="https://github.com/ETCHDEV/Port-Windows-11-Xiaomi-11-Lite-NE/blob/main/lisa.png" width="250" alt="Windows 11 działający na Mi 11 Lite NE">.


# Uruchamianie systemu Windows na Mi 11 Lite NE/Mi 11 LE

## Aktualizacja sterownika

### Wymagania wstępne

- Obraz UEFI dla TYLKO partycji montażowej!!!](https://github.com/ETCHDEV/Port-Windows-11-Xiaomi-11-Lite-NE/releases/download/v0.0.1/boot-lisa-install.img)
- [DriverUpdater](https://github.com/WOA-Project/DriverUpdater/releases/latest)
- [Zaktualizowane sterowniki](https://github.com/Icesito68/7xx-Drivers) (kliknij strzałkę Pobierz kod i pobierz jako zip)

#### Uruchom telefon do zmodyfikowanego UEFI img przy użyciu następującego polecenia:
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

#### Teraz zamknij diskpart
``diskpart
exit
```

### Zainstaluj sterowniki

> Zastąp `<lisadriversfolder>` rzeczywistą lokalizacją zaktualizowanego folderu sterowników.

>Rozpakuj pobrany plik zip 
``cmd
.\driverupdater.exe -d <lisadriversfolder>\components\QC7325\Platform -r <lisadriversfolder> -p W:
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

#### Exit diskpart
``diskpart
exit
```

### Teraz możesz uruchomić system Windows, pierwsze uruchomienie po zainstalowaniu sterowników może zająć trochę czasu.


## Zakończone!!!
