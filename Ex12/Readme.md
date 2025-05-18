## 🧪 Zadanie praktyczne: Analiza słownictwa w tekstach literackich (Projekt Gutenberg)

### 🎯 Cel:

Zaprojektuj i zaimplementuj aplikację konsolową w języku C#, która:

* **asynchronicznie pobiera** wybrane dzieła literackie z Projektu Gutenberg (dostępne jako pliki tekstowe online),
* **równolegle przetwarza teksty**, zliczając wystąpienia słów,
* wykorzystuje **synchronizację** dostępu do wspólnych struktur danych,
* generuje raport z 10 najczęściej używanych słów w całej kolekcji.

---

### 📘 Dane wejściowe:

Aplikacja ma pobierać i analizować **następujące teksty literackie**:

1. Frankenstein – [https://www.gutenberg.org/files/84/84-0.txt](https://www.gutenberg.org/files/84/84-0.txt)
2. Alicja w Krainie Czarów – [https://www.gutenberg.org/files/11/11-0.txt](https://www.gutenberg.org/files/11/11-0.txt)
3. Przygody Sherlocka Holmesa – [https://www.gutenberg.org/files/1661/1661-0.txt](https://www.gutenberg.org/files/1661/1661-0.txt)
4. Moby Dick – [https://www.gutenberg.org/files/2701/2701-0.txt](https://www.gutenberg.org/files/2701/2701-0.txt)

---

### 🧑‍💻 Wymagania funkcjonalne:

1. **Pobieranie danych:**

   * użyj `HttpClient` i `async/await`,
   * pobierz każdy plik osobno, a następnie przejdź do przetwarzania.

2. **Przetwarzanie danych równolegle:**

   * dla każdego tekstu zlicz słowa (ignorując wielkość liter),
   * dane łącz do jednej współdzielonej kolekcji,
   * użyj `Parallel.ForEach`, `Task.Run`, lub `PLINQ`.

3. **Synchronizacja:**

   * użyj `ConcurrentDictionary<string, int>` lub `lock` na `Dictionary<string, int>`.

4. **Raport:**

   * wypisz 10 najczęstszych słów w całej analizie,
   * podaj czas pobierania i czas przetwarzania (`Stopwatch`).

---

### 🧩 Wskazówki:

* Pomiń znaki interpunkcyjne (`.,!?:;"'`) przy dzieleniu tekstu.
* Użyj `.ToLowerInvariant()` do normalizacji słów.
* Nie analizuj całego pliku, odetnij nagłówek i stopkę Gutenberga (dla ambitnych).
* Zastosuj `Task.WhenAll()` przy pobieraniu danych.

---

### 🧪 Przykład raportu końcowego:

```
Najczęstsze słowa:
1. the: 16824
2. and: 9532
3. to: 7983
4. of: 7344
5. a: 6091
6. in: 5822
7. that: 4933
8. he: 4291
9. was: 4115
10. it: 3998

Czas pobierania: 3.21 sekundy  
Czas przetwarzania: 1.74 sekundy
```

---

### 📤 Co należy oddać:

* Plik `.cs` lub projekt `.NET`.
* Zrzuty ekranu z wynikami działania.
* Krótki opis: jakie metody zostały użyte (Task, Parallel, synchronizacja).
* Dodatkowo (dla chętnych): obsługa `CancellationToken`, różne strategie synchronizacji (lock vs ConcurrentDictionary), analiza wydajności.

---

### 💬 Pytania do refleksji (obowiązkowe):

* Jakie techniki zostały użyte do przetwarzania równoległego?
* Dlaczego synchronizacja była konieczna?
* Jak wyglądałby ten kod bez równoległości? Co by się zmieniło?
* Jak można jeszcze poprawić wydajność?

