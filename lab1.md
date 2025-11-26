# bsk
## 0.1 Wyświetl wszystkie informacje użytkownika Alice
```bash
curl -s http://localhost:5000/user/alice | jq '.'
```
## 0.2 Wyświetl imię i nazwisko użytkownika Alice
```bash
curl -s http://localhost:5000/user/alice | jq '.name'
```
## 0.3 Wyświetl adres e-mail użytkownika Bob
```bash
curl -s http://localhost:5000/user/bob | jq '.email'
```
## 0.4 Wyświetl wiek użytkownika Alice
```bash
curl -s http://localhost:5000/user/alice | jq '.age'
```
## 0.5Wyświetl nazwę miasta, w którym mieszka użytkownik Bob
```bash
curl -s http://localhost:5000/user/bob | jq '.city'
```
## 0.6Wyświetl hobby użytkownika Alice
```bash
curl -s http://localhost:5000/user/alice | jq '.hobbies'
```
## 0.7 Sprawdź, czy jednym z hobby użytkownika Bob są gry  Zwraca true jeśli tak, false jeśli nie
```bash
curl -s http://localhost:5000/user/bob | jq '.hobbies | contains(["games"])'
```
## 0.8 Wyświetl pierwsze hobby użytkownika Alice
```bash
curl -s http://localhost:5000/user/alice | jq '.hobbies[0]'
```
## 0.9 Sprawdź, ile hobby ma użytkownik Bob, a ile użytkownik Alice
```bash
curl -s http://localhost:5000/user/alice | jq '.hobbies | length'
curl -s http://localhost:5000/user/bob | jq '.hobbies | length'
```
## 0.10 Wyświetl nazwę i miasto jako "Alice Smith (Warsaw)", a potem "Alice Smith from Warsaw"
```bash
# Wersja 1
curl -s http://localhost:5000/user/alice | jq -r '"\(.name) (\(.city))"'

# Wersja 2 (zmodyfikowana)
curl -s http://localhost:5000/user/alice | jq -r '"\(.name) from \(.city)"'
```
## 0.11 Wyświetl wszystkie przedmioty oraz same nazwy
```bash
curl -s http://localhost:5000/items | jq '.'
curl -s http://localhost:5000/items | jq '.[].name'
```
## 0.12 Wyświetl przedmioty droższe niż 20 pln
```bash
curl -s http://localhost:5000/items | jq 'map(select(.price > 20))'
```
## 0.13 Wyświetl przedmioty tańsze niż 30 pln
```bash
curl -s http://localhost:5000/items | jq 'map(select(.price < 30))'
```
## 0.14 Posortuj przedmioty według ceny rosnąco i malejąco
```bash
# Rosnąco
curl -s http://localhost:5000/items | jq 'sort_by(.price)'

# Malejąco
curl -s http://localhost:5000/items | jq 'sort_by(.price) | reverse'
```
## 0.15 Pobierz sumę cen wszystkich przedmiotów
```bash
curl -s http://localhost:5000/items | jq 'map(.price) | add'
```
## 0.16 Wyświetl przedmioty, których nazwa zawiera "item"
```bash
curl -s http://localhost:5000/items | jq 'map(select(.name | contains("item")))'
```
## 0.17 Wyświetl przedmioty w przedziale cenowym 10-30 pln
```bash
curl -s http://localhost:5000/items | jq 'map(select(.price >= 10 and .price <= 30))'
```
## 0.18 Wyświetl użytkowników, którzy mają więcej niż 2 hobby  Uwaga: Ten serwer nie posiada endpointu /users zwracającego listę wszystkich na raz, więc to zapytanie zakłada, że mamy dostęp do pełnego obiektu JSON opisanego w zadaniu.
```bash
echo '{ "alice": {...}, "bob": {...} }' | jq 'to_entries | map(select(.value.hobbies | length > 2)) | .[].key'
```
## 0.19 Wyślij request POST (endpoint /echo)
```bash
curl -X POST -d "Test Echo" http://localhost:5000/echo
```
## 0.20 Dodaj nowy przedmiot (POST /items)
```bash
curl -X POST -H "Content-Type: application/json" \
     -d '{"id": 5, "name": "NowyItem", "price": 40.00}' \
     http://localhost:5000/items
# Sprawdzenie:
curl -s http://localhost:5000/items | jq '.'
```
## 0.21 Aktualizuj cenę przedmiotu nr 1 (PUT)
```bash
curl -X PUT -H "Content-Type: application/json" \
     -d '{"price": 19.99}' \
     http://localhost:5000/items/1
```
## 0.22 Usuń przedmiot o numerze 3 (DELETE)
```bash
curl -X DELETE http://localhost:5000/items/3
```
## 0.23 Wyświetl przedmiot o największej cenie
```bash
curl -s http://localhost:5000/items | jq 'max_by(.price)'
```
## 0.24 Wyświetl przedmioty z ceną podwyższoną o 10% (symulacja wyświetlania)
```bash
curl -s http://localhost:5000/items | jq 'map(.price *= 1.1)'
```
## 0.25 Pobierz nazwy wszystkich użytkowników i ich wiek (Wywołanie dla poszczególnych endpointów)
```bash
curl -s http://localhost:5000/user/alice | jq '{name, age}'
curl -s http://localhost:5000/user/bob | jq '{name, age}'
```
## 0.26 Wyświetl hobby Alice jako string połączony przecinkami
```bash
curl -s http://localhost:5000/user/alice | jq -r '.hobbies | join(", ")'
```
## 0.27 Pobierz pierwszy i ostatni przedmiot z listy
```bash
curl -s http://localhost:5000/items | jq '.[0], .[-1]'
```
## 0.28 Sprawdź, czy są przedmioty droższe niż 100 pln
```bash
curl -s http://localhost:5000/items | jq 'any(.price > 100)'
```
## 0.29 Utwórz nowy przedmiot i wyświetl listę
```bash
curl -X POST -H "Content-Type: application/json" \
     -d '{"id": 6, "name": "SuperOlek", "price": 120.00}' \
     http://localhost:5000/items
curl -s http://localhost:5000/items | jq '.'
```
## 0.30 Zaktualizuj przedmiot id=2 i wyświetl listę
```bash
curl -X PUT -H "Content-Type: application/json" \
     -d '{"name": "UpdatedItem", "price": 88.00}' \
     http://localhost:5000/items/2
curl -s http://localhost:5000/items | jq '.'
```














