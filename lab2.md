#lab2
## 1.1 MD5
``` bash
# 1. Pobierz dane
RESPONSE=$(curl -s http://127.0.0.1:10001/hash)
SESSION_ID=$(echo $RESPONSE | jq -r '.session_id')
WORD=$(echo $RESPONSE | jq -r '.word')

# 2. Oblicz hash (używając OpenSSL jak w instrukcji [cite: 236])
# Ważne: echo -n zapobiega dodaniu znaku nowej linii
HASH=$(echo -n "$WORD" | openssl dgst -md5 | awk '{print $2}')

# 3. Wyślij odpowiedź
curl -X POST -H "Content-Type: application/json" \
     -d "{\"session_id\": \"$SESSION_ID\", \"hash\": \"$HASH\"}" \
     http://127.0.0.1:10001/submit
```
## 1.2 SHA-256
```bash
HASH=$(echo -n "$WORD" | openssl dgst -sha256 | awk '{print $2}')
```
## 1.3 SHA-512 
```bash
HASH=$(echo -n "$WORD" | openssl dgst -sha512 | awk '{print $2}')
```
