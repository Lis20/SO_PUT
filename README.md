# Operacje na plikach
## 1. Wyszukiwanie plików i katalogów
### Wyszukaj wszystkie pliki lub katalogi w swoim katalogu domowym zaczynające się od kropki:
find ~ -name ".*"

### Wyszukaj wszystkie pliki lub katalogi w swoim katalogu domowym kończące się tyldą (~):
find ~ -name "*~"

### Wyszukaj wszystkie katalogi w swoim katalogu domowym kończące się tyldą (~):
find ~ -type d -name "*~"

### Wyszukaj wszystkie katalogi w swoim katalogu domowym kończące się tyldą (~) lub rozpoczynające się od kropki:
find ~ \( -type d -name "*~" -o -type d -name ".*" \)

### Wyszukaj wszystkie pliki tekstowe o nazwie kończącej się rc i wyświetl ich zawartość za pomocą edytora tekstowego (np. gedit, kate):
find ~ -type f -name "*rc" -exec gedit {} \;

lub dla kate

ind ~ -type f -name "*rc" -exec kate {} \;

## 2. Operacje na katalogu /tmp/test/
### Przejdź do katalogu /tmp/:
cd /tmp/

### Utwórz katalog /tmp/test/ i utwórz w nim pliki asia, basia, casia, dasia, easia, fasia:
mkdir -p /tmp/test/
touch /tmp/test/{asia,basia,casia,dasia,easia,fasia}

### Za pomocą komendy find usuń wszystkie pliki z katalogu /tmp/test/ których nazwy składają się z napisu asia poprzedzonego dowolną literą:
find /tmp/test/ -type f -name "?asia" -delete

### Utwórz pliki i katalogi jak powyżej. Usuń wszystkie pliki z katalogu /tmp/test/ których nazwy składają się z napisu asia poprzedzonego dowolną literą. Niech przed usunięciem pliku komenda find zarząda potwierdzenia od użytkownika:
find /tmp/test/ -type f -name "?asia" -exec rm -i {} \;

# Potoki, strumienie i przekierowania (i)
## cat
### Uruchom komendę cat bez argumentów i wpisz kilka linii (zakończ znakiem końca strumienia):
cat
This is line one.
This is line two.
This is line three.
Ctrl+D

### Za pomocą komendy cat utwórz plik PLIK2 o treści:
cat > PLIK2 <<EOF
We are using Linux daily to UP our productivity.
So UP yours!

        -- Adapted from Pat Paulsen by Joe Sloan
EOF

### Za pomocą komendy cat skopiuj zawartość pliku PLIK2 do PLIK3:
cat PLIK2 > PLIK3

### Za pomocą komendy cat połącz zawartość plików PLIK2 i PLIK1 i zapisz ją do pliku PLIK3:
cat PLIK2 PLIK1 > PLIK3

### Wyświetl zawartość pliku PLIK3 z ponumerowanymi liniami:
cat -n PLIK3
tac

### Uruchom komendę tac bez argumentów i wpisz kilka linii:
tac
Line one.
Line two.
Line three.
Ctrl+D

### Za pomocą komendy tac skopiuj zawartość pliku PLIK2 do PLIK4:
tac PLIK2 > PLIK4

### Wyświetl zawartość pliku PLIK2 za pomocą komendy tac:
tac PLIK2

### Wyświetl zawartość pliku PLIK2 za pomocą komend tac tak, żeby kolejność linii nie była odwrócona:
tac PLIK2 | tac

## Filtry

### Za pomocą komendy ls utwórz plik PLIK5 którego zawartość to lista plików i katalogów w katalogu dev:
ls /dev > PLIK5

### Wyświetl zawartość pliku PLIK5 ze stronnicowaniem za pomocą more:
more PLIK5

### Wyświetl zawartość pliku PLIK5 z przewijaniem za pomocą less:
less PLIK5

### Wyświetl zawartość katalogu /dev ze stronnicowaniem za pomocą more (bez używania dodatkowych plików):
ls /dev | more

### Wyświetl zawartość katalogu /dev z przewijaniem za pomocą less (bez używania dodatkowych plików):
ls /dev | less


## head i tail

### Odczytaj zawartość pliku PLIK5 numerując linie (cat) i wyświetl tylko pierwsze 10 linii (head):
cat -n PLIK5 | head

### Odczytaj zawartość pliku PLIK5 numerując linie (cat) i wyświetl tylko pierwszą linię (head):
cat -n PLIK5 | head -n 1


### Odczytaj zawartość pliku PLIK5 numerując linie (cat) i wyświetl tylko ostatnie 10 linii (tail):
cat -n PLIK5 | tail


### Odczytaj zawartość pliku PLIK5 numerując linie (cat) i wyświetl tylko ostatnią linię (tail):
cat -n PLIK5 | tail -n 1


### Odczytaj zawartość pliku PLIK5 numerując linie (cat) i wyświetl tylko 5 linię (head i tail):
cat -n PLIK5 | head -n 5 | tail -n 1
tr


### Utwórz plik PROP zawierający listę nazw następujących własności:
cat > PROP <<EOF
host,
port,
initial barrier,
start barrier,
final barrier,
number of shared objects,
number of clients,
module 1
module 2
EOF

### Za pomocą komendy tr wyświetl zawartość PROP bez znaków interpunkcyjnych:
tr -d '[:punct:]' < PROP

### Wyświetl zawartość PROP jak powyżej, następnie zamień wszystkie spacje na podkreślniki:
tr -d '[:punct:]' < PROP | tr ' ' '_'

### Wyświetl zawartość PROP jak powyżej, następnie zamień wszystkie małe litery na wielkie i zapisz wynik do pliku PROP_GEN:
tr -d '[:punct:]' < PROP | tr ' ' '_' | tr '[:lower:]' '[:upper:]' > PROP_GEN
cut

### Utwórz plik students zawierający listę studentów (uwaga na spacje):
cat > students <<EOF
Imię     Nazwisko        Indeks    Oceny
Adam     Rymski          71711     4    5    3
Tomasz   Filipiuk        71745     4    4
Karol    Effimenko       101023    4    3
Anna     Nowak           71791     3.5  5    5    5
Michał   Korsakow        71921     3.5  3.5  3
Henryk   Wojciechowski   71710     3    3    2
Michał   Cierń           71717     4.5  4    5
Marcin   Kozak           71729     4    4.5  4.5
Ewa      Tomaszewska     71733     4    4.5  5
EOF

### Używając komendy cut wypisz tylko nazwiska studentów:
cut -d ' ' -f 2 students | tr -s ' '

### Używając komendy cut wypisz tylko imiona i nazwiska studentów bez nagłówka:
tail -n +2 students | cut -d ' ' -f 1,2 | tr -s ' '

### Używając komendy cut wypisz tylko numery indeksów i oceny studentów:
cut -d ' ' -f 3- students | tr -s ' '

## sort i uniq

### Wyświetl nazwiska studentów z pliku students w kolejności alfabetycznej za pomocą sort, tr, tail/head, cut:
tail -n +2 students | cut -d ' ' -f 2 | tr -s ' ' | sort

### Wyświetl indeksy studentów z pliku students w kolejności rosnącej:
tail -n +2 students | cut -d ' ' -f 3 | tr -s ' ' | sort -n

### Wyświetl indeksy studentów z pliku students w kolejności malejącej:
tail -n +2 students | cut -d ' ' -f 3 | tr -s ' ' | sort -nr

### Wylosuj nazwisko jednego studenta z pliku students:
tail -n +2 students | cut -d ' ' -f 2 | tr -s ' ' | sort -R | head -n 1

## xargs
### Utwórz plik addr z adresami stron internetowych:
cat > addr <<EOF
http://www.example.com/
http://www.cs.put.poznan.pl/ksiek/
http://www.google.com/
EOF

### Otwórz wszystkie strony zapisane w pliku addr za pomocą dowolnej przeglądarki (xargs):
xargs -a addr -I {} xdg-open {}

## wc
### Policz znaki, słowa i linie znajdujące się w pliku PLIK2:
wc PLIK2

### Policz słowa znajdujące się w pliku PLIK2:
wc -w PLIK2

### Policz litery t znajdujące się w pliku students (tr):
tr -cd 't' < students | wc -c

## tee
### Wypisz otrzymany strumień do strumienia wyjściowego, a także do wskazanych plików:
echo "This is a test message" | tee output.txt


### Dodaj zawartość do pliku bez nadpisywania:
echo "Another test message" | tee -a output.txt


## grep
### Za pomocą grep wyświetl wszystkich studentów którzy uzyskali ocenę 2:
grep ' 2' students

### Wyświetl studentów którzy nie uzyskali żadnej oceny 2:
grep -v ' 2' students

### Wyświetl studentów których imiona zaczynają się na M:
grep '^M' students

### Wyświetl studentów których imiona zaczynają się na M lub A:
grep '^[MA]' students

### Wyświetl studentów których nazwiska zaczynają się na literę z pierwszej połowy alfabetu:
grep '^[A-M]' students

### Wyświetl studentów których nazwiska nie zawierają litery k:
grep -v 'k' students

### Wyświetl studentów których numer indeksu jest sześciocyfrowy:
grep '[0-9]\{6\}' students

### Wyświetl studentów którzy uzyskali ocenę 5 jako ostatnią:
grep ' 5$' students

### Wyświetl studentów którzy uzyskali ocenę 5 jako przedostatnią:
grep ' 5 [0-9]' students

### Wyświetl studentów którzy uzyskali ocenę przynajmniej jedną 3 i mają na imię Michał:
grep 'Michał' students | grep ' 3'

## bc
### Wykonaj obliczenia za pomocą bc:
echo "2 + 2" | bc
echo "scale=2; 6.0 / 4.0" | bc

# Potoki, strumienie i przekierowania (ii)

## Operacje na plikach
### 1. Otwórz w przeglądarce adresy podane w (jakimś) pliku [xargs]
```bash
xargs < lista_adresow.txt xdg-open

### 2. Wyświetl częstotliwości taktowania wszystkich procesorów (w jednej linii) [/proc/cpuinfo xargs]
cat /proc/cpuinfo | grep MHz | awk '{print $4}' | xargs

### 3. Wygeneruj listę wszystkich słów które mają 8 liter, z których 3-cia to litera a, a ostatnią to literą jest y (do krzyżówki?). Wyświetl wyniki wielkimi literami. Zastosuj paginację lub przesuwanie wyników. [/usr/share/dict/words grep]
grep -i '^..a..y$' /usr/share/dict/words | tr '[:lower:]' '[:upper:]' | less

### 4. Wyświetl 20 losowych cyfr [/dev/urandom]
head -c 20 /dev/urandom | tr -dc '0-9' | fold -w 20

### 5. Wygeneruj 6 losowych 8-o znakowych haseł [fold]
fold -w 8 /dev/urandom | head -n 6 | awk '{print toupper($0)}'

### 6. Podaj nazwę użytkownika który jest zalogowany najdłużej/najkrócej [sort who]
who | awk '{print $1}' | sort | uniq -c | sort -nr

### 7. Wypisz adres fizyczny (MAC) karty sieciowej komputera [ifconfig grep]
ifconfig | grep -oE '([0-9A-Fa-f]{2}:){5}([0-9A-Fa-f]{2})'

### 8. Wypisz wszyskie adresy IP komputera [ifconfig grep]
ifconfig | grep -oE '\b([0-9]{1,3}\.){3}[0-9]{1,3}\b'

### 9. Wypisz 5 najpopularniejszych komend z historii [.bash_history sort uniq]
grep -v '^#' ~/.bash_history | sort | uniq -c | sort -nr | head -n 5

### 10. Wypisz nazwy wszystkich zwykłych plików i linków w katalogu bieżącym [ls]
ls -l | grep '^-' | awk '{print $9}'

### 11. Sprawdź który z użytkowników otworzył najwięcej plików (i ile to ich jest) [lsof sort uniq]
lsof | awk '{print $3}' | sort | uniq -c | sort -nr

### 12. Wypisz 5 najpopularniejszych rozszerzeń plików (bez katalogów) w swoim katalogu domowym [ls sort uniq]
ls -p ~ | grep -v / | awk -F . '{if (NF > 1) {print $NF}}' | sort | uniq -c | sort -nr | head -n 5

### 13. Jak wyżej, tylko typy plików (mimetype) zamiast rozszerzeń [sort uniq file]
file --mime-type * | awk '{print $2}' | sort | uniq -c | sort -nr

### 14. Policz linie kodu we wszystkich plikach katalogu z projektem (znaki \n) [find wc xargs]
find ./projekt -type f -exec cat {} + | wc -l

### 15. Jak wyżej, tylko policz średniki zamiast znaków nowej linii. [find tr xargs]
find ./projekt -type f -exec cat {} + | tr -cd ';' | wc -c

### 16. Jak wyżej, tylko wypisz wiadomość na końcu z liczbą średników (np. “Semicolons: 644”) [echo wc xargs]
echo "Semicolons: $(find ./projekt -type f -exec cat {} + | tr -cd ';' | wc -c)"

### 17. Wypisz informacje o copyright ze wszystkich plików z kodem w katalogu (po rozszerzeniu) [find cat xargs]
find ./kod -type f -exec cat {} + | grep -i copyright

### 18. Policz wszystkie pliki ukryte w swoim katalogu domowym [grep ls wc]
ls -a ~ | grep -v '^\.$' | grep '^\.' | wc -l

### 19. Wypisz wartość 2^n dla n=1..100 [bc echo xargs]
seq 1 100 | xargs -I{} echo "2^{}" | bc

### 20. Wylicz średnią ocen dla każdego ze studentów w pliku przyklad.csv [xargs echo bc]
awk -F, '{sum=0; for(i=2; i<=NF; i++) sum+=$i; print $1, sum/(NF-1)}' przyklad.csv

### 21. Wypisz wszystkie pliki i katalogi z katalogu /proc do pliku tymczasowego (np. /tmp/proc.log) i na ekran, ale nie pokazuj błędów. Włącz paginację albo przemieszczanie się po wynikach. [find tee /dev/null]
find /proc -maxdepth 1 -exec ls -d {} + 2>/dev/null | tee /tmp/proc.log | less

