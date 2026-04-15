# Hello World - Aplikacja z Docker Compose

Aplikacja demonstracyjna łącząca Docker Compose, PostgreSQL i Azure Blob Storage.


# Azure App CI/CD

![CI Status](https://github.com/RostyslavDm/azure-app-2/workflows/CI%20-%20Backend%20Tests/badge.svg)


## Funkcjonalności

### 👥 Baza danych PostgreSQL
- Automatyczne tworzenie tabeli `users` (name, surname, creation_date)
- Dodawanie użytkowników przez formularz
- Wyświetlanie listy użytkowników

### 📦 Azure Blob Storage
- Upload plików PDF do Blob Storage
- Lista wszystkich uploadowanych plików
- Automatyczne generowanie unikalnych nazw plików

## Struktura

- **Frontend** - strona HTML z formularzami do zarządzania użytkownikami i plikami PDF
- **Backend** - API w Pythonie (Flask) obsługujące PostgreSQL i Azure Blob Storage
- **Nginx** - reverse proxy kierujący ruch do odpowiednich serwisów

## Wymagania

Utwórz plik `.env` w głównym katalogu projektu:

```env
DATABASE_URL=postgresql://user:password@host:port/database
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;AccountName=YOUR_ACCOUNT;AccountKey=YOUR_KEY;EndpointSuffix=core.windows.net
AZURE_STORAGE_CONTAINER=demo-container
```

## Uruchomienie

```bash
docker-compose up --build
```

## Dostęp

- Aplikacja: http://localhost:8080
- Backend (bezpośrednio): http://localhost:5000/api/health

### API Endpoints

**Użytkownicy:**
- `GET /api/db/users` - pobierz listę użytkowników
- `POST /api/db/users` - dodaj użytkownika (JSON: {name, surname})

**Blob Storage:**
- `POST /api/blob/upload` - upload pliku PDF (multipart/form-data)
- `GET /api/blob/list` - lista plików w Blob Storage

## Zatrzymanie

```bash
docker-compose down
```

## Architektura

```
Przeglądarka
    ↓
Nginx (port 8080)
    ├─→ / → Frontend (nginx:80)
    └─→ /api → Backend (Flask:5000)
```
