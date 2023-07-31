<img align="right" src="https://github.com/ETCHDEV/Port-Windows-11-Xiaomi-11-Lite-NE/blob/main/lisa.png" width="250" alt="Windows 11 Running On a Mi 11 Lite NE">


# Uruchamianie systemu Windows na Xiaomi Mi 11 Lite NE / Mi 11 LE

## Rozwiązywanie problemów


## Urządzenie może uruchomić system Android, ale nie bootloader

### Wymagania wstępne:

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
- [parted do patynowania dysku](https://www.mediafire.com/file/s9bjano4pezphou/parted/file)

Jest to spowodowane partycjami o nazwach woluminów, których program ładujący nie może obsłużyć, aby to naprawić:

- Uruchom do TWRP/OF lub dowolnego niestandardowego recovery, które obsługuje szyfrowanie urządzenia/może uzyskać dostęp do partycji danych i obsługuje adb

- Skopiuj parted do telefonu i wprowadź powłokę adb za pomocą następujących poleceń:
```cmd
adb push parted /cache/
adb shell "chmod 755 /cache/parted"
adb shell
```

- Uruchom parted
```sh
cd /cache
./parted /dev/block/sda
```

- Uruchom ```print```, aby wyświetlić listę wszystkich partycji

- Poszukaj partycji, które mają spacje w nazwach, np. „Basic Data Partition” i zanotuj ich numer woluminu

- Teraz uruchom ```rm <vol number>``` np. ```rm 35``` (Upewnij się, że usunąłeś obie utworzone partycje Windows)

- Jeśli usunąłeś partycję 34 i 35, postępuj zgodnie z [Instrukcją instalacji](./partition-en.md) z kroku Tworzenie partycji ESP (w zależności od pogody, Twoje urządzenie ma 128 GB lub 256 GB)
