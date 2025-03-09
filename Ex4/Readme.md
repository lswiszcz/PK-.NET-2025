# **Zadanie: Aplikacja do zarządzania biblioteką w C# (.NET)**  

## **Cel zadania**  
Celem zadania jest zaprojektowanie i zaimplementowanie aplikacji konsolowej w języku C# w technologii .NET, która będzie symulować zarządzanie biblioteką. Zadanie skupia się na zastosowaniu paradygmatu programowania obiektowego (OOP), w tym na wykorzystaniu **abstrakcji, enkapsulacji, dziedziczenia i polimorfizmu**.

## **Opis aplikacji**  
Aplikacja powinna umożliwiać zarządzanie zbiorami bibliotecznymi oraz obsługę wypożyczeń i zwrotów książek. Użytkownicy będą mogli:  
1. **Dodawać książki** do biblioteki.  
2. **Wyświetlać listę książek** dostępnych w bibliotece.  
3. **Wypożyczać książki**, jeśli są dostępne.  
4. **Zwrot książki** do biblioteki.  

Dodatkowo, aplikacja powinna uwzględniać obsługę e-booków jako osobnego typu książek.

---

## **Wymagania funkcjonalne**  

### **1. Struktura klas**
- **Klasa `Book` (bazowa)**  
  - Powinna posiadać właściwości: `Id`, `Title`, `Author`, `IsAvailable`.  
  - Powinna mieć metodę `DisplayInfo()`, wyświetlającą podstawowe informacje o książce.  
- **Klasa `EBook` (dziedziczy po `Book`)**  
  - Powinna posiadać dodatkową właściwość `FileFormat` (np. PDF, EPUB).  
- **Klasa `Library`**  
  - Powinna zawierać kolekcję książek.  
  - Metody:
    - `AddBook(Book book)` – dodaje książkę do biblioteki.
    - `ListAvailableBooks()` – zwraca listę dostępnych książek.
    - `BorrowBook(int bookId, string borrowerName)` – oznacza książkę jako wypożyczoną.
    - `ReturnBook(int bookId)` – oznacza książkę jako zwróconą.

### **2. Obsługa wyjątków**  
- Jeśli użytkownik spróbuje wypożyczyć książkę, która jest już wypożyczona, powinien otrzymać komunikat o błędzie.  
- Jeśli użytkownik spróbuje zwrócić książkę, która nie była wypożyczona, system powinien to obsłużyć.

### **3. Interfejs `IBookOperations`**  
- Zdefiniuj interfejs `IBookOperations`, który będzie zawierał metody:
  - `BorrowBook(int bookId, string borrowerName)`.
  - `ReturnBook(int bookId)`.  
- Klasa `Library` powinna implementować ten interfejs.

### **4. Testy jednostkowe**  
- Napisz testy jednostkowe dla metod `BorrowBook()` i `ReturnBook()`, sprawdzające poprawność działania tych funkcji.

---

## **Wskazówki implementacyjne**  
1. **Stosuj enkapsulację** – pola klas powinny być prywatne, a dostęp do nich realizowany za pomocą właściwości.  
2. **Wykorzystaj polimorfizm** – klasa `EBook` powinna nadpisywać metodę `DisplayInfo()`, dodając informację o formacie pliku.  
3. **Stosuj dziedziczenie** – `EBook` powinien rozszerzać `Book`, dodając nowe właściwości.  
4. **Zaimplementuj interfejsy** – `Library` powinna implementować interfejs `IBookOperations`.  

---

## **Kryteria oceny**  
✅ **Poprawność implementacji klas i metod** (zgodność z wymaganiami).  
✅ **Zastosowanie zasad OOP** (abstrakcja, enkapsulacja, dziedziczenie, polimorfizm).  
✅ **Obsługa wyjątków** (błędy powinny być odpowiednio obsłużone).  
✅ **Jakość kodu** (czytelność, przestrzeganie konwencji).  
✅ **Obecność testów jednostkowych** (testy dla `BorrowBook()` i `ReturnBook()`).  


---
## **Przykład uruchomienia**

```csharp
Library library = new Library();

// Dodanie książek do biblioteki
Book book1 = new Book("C# Programming", "John Doe", "12345");
Book book2 = new Book("Design Patterns", "Gamma et al.", "67890");
library.AddBook(book1);
library.AddBook(book2);

// Rejestracja czytelnika
Reader reader = new Reader(1, "Alice", "alice@example.com");
library.RegisterReader(reader);

// Wypożyczenie książki
if (library.BorrowBook("12345", reader))
{
    Console.WriteLine("Book borrowed successfully.");
}
else
{
    Console.WriteLine("Book is not available.");
}

// Zwrot książki
if (library.ReturnBook("12345", reader))
{
    Console.WriteLine("Book returned successfully.");
}
else
{
    Console.WriteLine("Failed to return book.");
}
```