# BSK 2025Z - Zadanie 5: Pi-Hole (Symulacja Docker)

Repozytorium zawiera rozwiązanie Zadania Praktycznego nr 5 z przedmiotu Bezpieczeństwo Systemów Komputerowych (Semestr 25Z).

## Realizacja **Scenariusza 2**: Symulacja w oprogramowaniu wirtualizacyjnym.

## 👥 Zespół
* Łukasz Krajewski
* Tomasz Kutrzeba
* Marcin Stróżyński

## 🛠️ Architektura
Projekt wykorzystuje **Docker Compose** do zestawienia odseparowanej podsieci (`172.20.0.0/16`) zawierającej dwa kontenery:
1.  **Pi-hole (`172.20.0.2`)**: Serwer DNS pełniący rolę sinkhole dla reklam i trackerów.
2.  **Klient (`172.20.0.3`)**: Kontener oparty na Alpine Linux, skonfigurowany tak, aby wymuszać ruch DNS przez Pi-hole.

## 🚀 Instrukcja uruchomienia

### 1. Wymagania wstępne
* Zainstalowany Docker oraz Docker Compose.

### 2. Uruchomienie środowiska
W katalogu głównym projektu wykonaj polecenie:
```bash
docker-compose up -d

```

### 3. Konfiguracja początkowa (Ważne!)

Ze względu na specyfikę najnowszej wersji obrazu Pi-hole, hasło administratora oraz listy blokowania należy zainicjować ręcznie po pierwszym uruchomieniu.

**Ustawienie hasła do panelu:**

```bash
docker exec -it pihole pihole setpassword 'admin'

```

**Aktualizacja list blokowania (Gravity):**

1. Wejdź na `http://localhost/admin` (Logowanie hasłem: `admin`).
2. Przejdź do **Tools** -> **Update Gravity**.
3. Kliknij przycisk **Update**.

## ✅ Weryfikacja działania (Testy)

Aby potwierdzić działanie blokady, należy wejść do terminala klienta i wykonać zapytania DNS.

1. Wejście do kontenera klienta:

```bash
docker exec -it simulation-client sh

```

2. Test poprawnej rezolucji (powinien zwrócić poprawne IP):

```bash
nslookup wikipedia.org

```

3. Test blokowania reklam (powinien zwrócić `0.0.0.0`):

```bash
nslookup flurry.com

```

## 📂 Struktura plików

* `docker-compose.yml` - Definicja infrastruktury (IaC).
* `README.md` - Dokumentacja projektu.
* `commands.txt` - Użyte komendy.
