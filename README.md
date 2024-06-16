### Operacje na plikach
## 1. Wyszukiwanie plików i katalogów
# Wyszukaj wszystkie pliki lub katalogi w swoim katalogu domowym zaczynające się od kropki:
find ~ -name ".*"

# Wyszukaj wszystkie pliki lub katalogi w swoim katalogu domowym kończące się tyldą (~):
find ~ -name "*~"

# Wyszukaj wszystkie katalogi w swoim katalogu domowym kończące się tyldą (~):
find ~ -type d -name "*~"

# Wyszukaj wszystkie katalogi w swoim katalogu domowym kończące się tyldą (~) lub rozpoczynające się od kropki:
find ~ \( -type d -name "*~" -o -type d -name ".*" \)

# Wyszukaj wszystkie pliki tekstowe o nazwie kończącej się rc i wyświetl ich zawartość za pomocą edytora tekstowego (np. gedit, kate):
find ~ -type f -name "*rc" -exec gedit {} \;

lub dla kate

ind ~ -type f -name "*rc" -exec kate {} \;

## 2. Operacje na katalogu /tmp/test/
# Przejdź do katalogu /tmp/:
cd /tmp/
# Utwórz katalog /tmp/test/ i utwórz w nim pliki asia, basia, casia, dasia, easia, fasia:
mkdir -p /tmp/test/
touch /tmp/test/{asia,basia,casia,dasia,easia,fasia}

# Za pomocą komendy find usuń wszystkie pliki z katalogu /tmp/test/ których nazwy składają się z napisu asia poprzedzonego dowolną literą:
find /tmp/test/ -type f -name "?asia" -delete

# Utwórz pliki i katalogi jak powyżej. Usuń wszystkie pliki z katalogu /tmp/test/ których nazwy składają się z napisu asia poprzedzonego dowolną literą. Niech przed usunięciem pliku komenda find zarząda potwierdzenia od użytkownika:
find /tmp/test/ -type f -name "?asia" -exec rm -i {} \;
