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
