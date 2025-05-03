### 🎓 **Zadanie na zajęcia – ASP.NET Core MVC: System Rejestracji Wydarzeń**

#### 📌 **Cel:**

Stworzenie prostej aplikacji webowej w architekturze MVC, która umożliwia zarządzanie wydarzeniami i uczestnikami. Celem ćwiczenia jest praktyczne wykorzystanie kontrolerów, widoków, modeli, walidacji oraz przechowywania danych w pamięci.

---

### 🛠️ **Wymagania funkcjonalne:**

#### 1. **Zarządzanie wydarzeniami:**

* Dodawanie nowego wydarzenia
* Wyświetlanie listy wydarzeń
* Przeglądanie szczegółów wybranego wydarzenia

#### 2. **Zarządzanie uczestnikami:**

* Dodawanie uczestnika do wybranego wydarzenia
* Wyświetlanie listy uczestników przypisanych do danego wydarzenia

---

### 📁 **Struktura projektu:**

#### Modele:

* **Event**

  * `Id` (int)
  * `Title` (string, wymagane, min. 3 znaki)
  * `Date` (DateTime, musi być datą w przyszłości)
  * `Description` (opcjonalna)

* **Participant**

  * `Id` (int)
  * `Name` (string, wymagane)
  * `Email` (string, wymagane, poprawny format)
  * `EventId` (int, identyfikator wydarzenia)

#### Kontrolery:

* `EventsController` – obsługuje wydarzenia (`Index`, `Create`, `Details`)
* `ParticipantsController` – obsługuje uczestników (`Create`, `ListByEvent`)

#### Widoki:

* Razor Views z formularzami i walidacją (przykład użycia `asp-validation-for`, `asp-for` itp.)

---

### ✅ **Walidacja danych:**

Użyj atrybutów walidacyjnych w modelach, np.:

```csharp
[Required]
[MinLength(3)]
public string Title { get; set; }

[Required]
[FutureDate(ErrorMessage = "Data musi być w przyszłości")]
public DateTime Date { get; set; }

[Required]
[EmailAddress]
public string Email { get; set; }
```

*(Atrybut `FutureDate` można napisać jako własny atrybut walidacyjny lub sprawdzić w kontrolerze.)*

---

### 💾 **Przechowywanie danych:**

Dane mają być przechowywane w pamięci przy użyciu statycznych list, np.:

```csharp
public static class InMemoryDatabase
{
    public static List<Event> Events { get; } = new();
    public static List<Participant> Participants { get; } = new();
}
```

---

### 📦 **Uwagi techniczne:**

* Nie korzystamy z bazy danych ani Entity Framework
* Projekt uruchamiany lokalnie jako aplikacja ASP.NET Core MVC
* Kod powinien być czytelny i zgodny z dobrymi praktykami MVC

---



Powodzenia! 💻