# 📘 Zadanie: Aplikacja REST API do zarządzania książkami

---

## 🎯 Cel zadania

Celem zadania jest stworzenie prostej aplikacji webowej z użyciem **ASP.NET Core Minimal API**, która umożliwia zarządzanie kolekcją książek. Dane będą przechowywane w lokalnej bazie danych **SQLite** przy użyciu **Entity Framework Core**. Testowanie funkcji odbywa się za pomocą narzędzia **Postman**.

---

## ✅ Wymagania funkcjonalne

Aplikacja ma udostępniać REST API realizujące następujące funkcje:

| Funkcja                            | Metoda | Endpoint             | Opis |
|------------------------------------|--------|----------------------|------|
| Pobierz listę książek              | GET    | `/api/books`         | Zwraca wszystkie książki z bazy |
| Pobierz książkę po ID              | GET    | `/api/books/{id}`    | Zwraca szczegóły książki o podanym ID |
| Dodaj nową książkę                 | POST   | `/api/books`         | Dodaje książkę na podstawie danych z żądania |
| Zaktualizuj istniejącą książkę     | PUT    | `/api/books/{id}`    | Edytuje książkę na podstawie danych z żądania |
| Usuń książkę                       | DELETE | `/api/books/{id}`    | Usuwa książkę o podanym ID z bazy |

### 🔸 Model danych `Book`
```csharp
public class Book
{
    public int Id { get; set; }
    public string Title { get; set; } = string.Empty;
    public string Author { get; set; } = string.Empty;
    public int PublishedYear { get; set; }
    public bool IsRead { get; set; }
}
```

---

## 🛠️ Wymagania techniczne

- Platforma: **.NET 8** lub nowszy
- Typ aplikacji: **ASP.NET Core (Minimal API)**
- Baza danych: **SQLite**
- OR/M: **Entity Framework Core (Code First)**
- Testowanie API: **Postman**
- Brak interfejsu webowego – tylko REST API

---

## 🗂️ Struktura projektu

```
BookApi/
├── Models/
│   └── Book.cs
├── Data/
│   └── BooksDbContext.cs
├── Program.cs
├── books.db (tworzony automatycznie)
```

---

## 🚀 Instrukcje wykonania

### 1. Utwórz nowy projekt
```bash
dotnet new web -n BookApi
cd BookApi
```

### 2. Dodaj paczki NuGet
```bash
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Microsoft.EntityFrameworkCore.Sqlite
```

### 3. Dodaj model `Book.cs`
**Plik:** `Models/Book.cs`

```csharp
public class Book
{
    public int Id { get; set; }
    public string Title { get; set; } = string.Empty;
    public string Author { get; set; } = string.Empty;
    public int PublishedYear { get; set; }
    public bool IsRead { get; set; }
}
```

### 4. Dodaj kontekst EF
**Plik:** `Data/BooksDbContext.cs`

```csharp
public class BooksDbContext : DbContext
{
    public BooksDbContext(DbContextOptions<BooksDbContext> options) : base(options) { }

    public DbSet<Book> Books => Set<Book>();
}
```

### 5. Skonfiguruj `Program.cs`

```csharp
using Microsoft.EntityFrameworkCore;
using BookApi.Models;
using BookApi.Data;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddDbContext<BooksDbContext>(options =>
    options.UseSqlite("Data Source=books.db"));

var app = builder.Build();

using (var scope = app.Services.CreateScope())
{
    var db = scope.ServiceProvider.GetRequiredService<BooksDbContext>();
    db.Database.EnsureCreated();
}

app.MapGet("/api/books", async (BooksDbContext db) => (...));

app.MapGet("/api/books/{id}", async (int id, BooksDbContext db) => (...));

app.MapPost("/api/books", async (Book book, BooksDbContext db) =>
{
    (...)
});

app.MapPut("/api/books/{id}", async (int id, Book input, BooksDbContext db) =>
{
    (...)
});

app.MapDelete("/api/books/{id}", async (int id, BooksDbContext db) =>
{
    (...)
});

app.Run();
```

---

## 🔎 Testowanie API w Postmanie

1. Uruchom projekt:
```bash
dotnet run
```

2. Otwórz Postmana i utwórz kolejne zapytania:

---

### ✅ GET `/api/books`
- **Opis:** Pobiera wszystkie książki
- **Body:** Brak

---

### ✅ GET `/api/books/{id}`
- **Opis:** Pobiera książkę o danym ID  
- **Przykład:** `/api/books/1`

---

### ✅ POST `/api/books`
- **Opis:** Dodaje nową książkę  
- **Body (JSON):**
```json
{
  "title": "Clean Code",
  "author": "Robert C. Martin",
  "publishedYear": 2008,
  "isRead": true
}
```

---

### ✅ PUT `/api/books/{id}`
- **Opis:** Aktualizuje książkę  
- **Body (JSON):**
```json
{
  "title": "Clean Code (Updated)",
  "author": "Robert C. Martin",
  "publishedYear": 2010,
  "isRead": true
}
```

---

### ✅ DELETE `/api/books/{id}`
- **Opis:** Usuwa książkę o podanym ID

---

## 🧪 Kryteria zakończenia

✅ Aplikacja się kompiluje i działa  
✅ Wszystkie endpointy API są dostępne i poprawnie działają  
✅ Testy w Postmanie zakończone powodzeniem  
✅ Projekt zawiera pełny kod + instrukcję uruchomienia  
✅ Baza danych SQLite tworzona automatycznie przy starcie

