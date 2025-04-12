
# 🧑‍🔧 Projekt zaliczeniowy – ASP.NET Core  
## **System zarządzania warsztatem samochodowym 2.0**

---

## 🧠 **Cel projektu**

Zaprojektuj i zaimplementuj aplikację webową do obsługi warsztatu samochodowego. Aplikacja powinna umożliwiać:

- zarządzanie klientami i pojazdami,
- zlecenia serwisowe z czynnościami i częściami,
- przypisywanie zadań mechanikom,
- komentowanie zleceń,
- generowanie raportów PDF,
- dodawanie zdjęć pojazdów,
- filtrowanie i raportowanie napraw.

Projekt powinien mieć przejrzystą strukturę, modularność, oraz używać nowoczesnych narzędzi: **EF Core**, **Dependency Injection**, **Mapperly**, **Identity**, **Swagger**, **Razor Pages, MVC (lub frontend SPA)**.

---

## 🧑‍🤝‍🧑 Zespół
- Zespół: **2 osoby**
- Praca nad repozytorium GitHub / GitLab (wymagana historia commitów)

---

## ✅ **Wymagania funkcjonalne**

| Moduł                 | Wymagania                                                                 |
|-----------------------|---------------------------------------------------------------------------|
| 🔐 Uwierzytelnianie   | Rejestracja, logowanie (ASP.NET Identity), role: `Admin`, `Mechanik`, `Recepcjonista` |
| 👤 Klienci            | CRUD klientów, wyszukiwanie, lista pojazdów klienta                      |
| 🚘 Pojazdy            | CRUD, zdjęcie pojazdu (upload), VIN, rejestracja                         |
| 🧾 Zlecenia           | Tworzenie zleceń, statusy, przypisywanie mechaników                      |
| 🔧 Czynności          | Lista czynności: opis + koszt robocizny                                  |
| ⚙️ Części             | Wybór części z katalogu, ilość, koszt                                     |
| 💬 Komentarze         | Komentarze wewnętrzne do zleceń (historia przebiegu)                     |
| 📦 Katalog części     | CRUD części, tylko dla `Admin` / `Recepcjonista`                         |
| 📈 Raporty            | Koszt napraw danego klienta / pojazdu / miesiąca + eksport do PDF        |

---

## 🧱 **Modele danych (przykładowe)**

```csharp
class Customer { ... }
class Vehicle { string ImageUrl; ... }
class ServiceOrder { Status, AssignedMechanic, List<ServiceTask>, List<Comment> }
class ServiceTask { Description, LaborCost, List<UsedPart> }
class Part { Name, UnitPrice }
class UsedPart { Part, Quantity }
class Comment { Author, Content, Timestamp }
```

---

## 🛠️ **Wymagania techniczne**

| Obszar                  | Szczegóły                                                                 |
|-------------------------|---------------------------------------------------------------------------|
| **ASP.NET Core**        | Wersja 7 lub 8                                                            |
| **EF Core**             | Code First + migracje, SQLite lub SQL Server                             |
| **Identity**            | Logowanie, role, autoryzacja                                              |
| **Mapperly**            | Mapowanie DTO ↔️ encje np. Mapperly                                 |
| **DI**                  | Serwisy biznesowe (`ICustomerService`, `IOrderService`, ...)              |
| **Swagger**             | Dokumentacja API                                                          |
| **Upload plików**       | Zdjęcie pojazdu (np. do `/wwwroot/uploads`)                              |
| **PDF**    | Generowanie raportów jako PDF                 |
| **Frontend**            | Razor Pages + Bootstrap (opcjonalnie SPA: React/Blazor/Angular)           |
| **Testy**  | testy jednostkowe (xUnit/NUnit)                                |

---

## 🗂️ **Struktura projektu**

```
/WorkshopManager
├── Controllers/
├── DTOs/
├── Models/
├── Services/
├── Mappers/             // Mapperly mappery
├── Views/
├── wwwroot/
│   └── uploads/         // zdjęcia pojazdów
├── Data/
├── Program.cs
```



## ✅ Co należy oddać?

- Repozytorium GitHub z historią commitów
- Działająca aplikacja ASP.NET Core
- Migracje + seed danych (lub dump bazy)
- `README.md` z opisem projektu, logowania, rolami


---

## 📌 Wskazówki

- Wszystkie dane domenowe mapuj za pomocą **Mapperly**
- Używaj **DataAnnotations** do walidacji
- Dbaj o **separację warstw**: logika w serwisach, nie w kontrolerach

