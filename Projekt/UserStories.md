
# 🧾 **User Stories – System warsztatu (ASP.NET Core)**  

### 🔐 **Uwierzytelnianie i role**

---

#### ✅ US1: Jako nowy użytkownik chcę móc się zarejestrować i zalogować.

**Definition of Done (DoD):**
- Formularz rejestracji i logowania działa (Razor Pages lub własne API + widok)
- Dane użytkownika zapisywane przez ASP.NET Identity
- Po zalogowaniu użytkownik ma dostęp do swojego panelu

---

#### ✅ US2: Jako administrator chcę przypisywać role użytkownikom (Mechanik / Recepcjonista / Admin).

**DoD:**
- Lista użytkowników (tylko dla Admina)
- Zmiana roli użytkownika poprzez UI
- Role używane do ograniczania widoczności widoków i akcji

---

### 👤 **Klienci i pojazdy**

---

#### ✅ US3: Jako recepcjonista chcę dodać nowego klienta.

**DoD:**
- Formularz z walidacją (imię i nazwisko, telefon)
- Dane trafiają do bazy
- Klient pojawia się w liście

---

#### ✅ US4: Jako recepcjonista chcę dodać pojazd do klienta.

**DoD:**
- Pojazd przypisany do klienta (relacja 1:N)
- Formularz z polami: marka, model, VIN, rejestracja, rok
- Dane zapisane i wyświetlane na profilu klienta

---

#### ✅ US5: Jako użytkownik chcę dodać zdjęcie pojazdu.

**DoD:**
- Możliwość uploadu obrazu (PNG, JPG)
- Plik zapisany w `wwwroot/uploads`
- Ścieżka obrazu zapisana w encji `Vehicle.ImageUrl`
- Obraz wyświetla się w widoku pojazdu

---

### 🧾 **Zlecenia i czynności serwisowe**

---

#### ✅ US6: Jako recepcjonista chcę utworzyć nowe zlecenie dla pojazdu.

**DoD:**
- Wybór klienta i pojazdu
- Opis problemu
- Przypisanie mechanika
- Domyślny status: „Nowe”

---

#### ✅ US7: Jako mechanik chcę dodawać czynności serwisowe do zlecenia.

**DoD:**
- Formularz: nazwa, koszt robocizny
- Dodanie do zlecenia (relacja 1:N)
- Widoczność w szczegółach zlecenia

---

#### ✅ US8: Jako mechanik chcę dodawać części do czynności serwisowej.

**DoD:**
- Wybór z listy części
- Określenie ilości
- Automatyczne przeliczenie kosztu
- Suma dla całego zlecenia = robocizna + części

---

#### ✅ US9: Jako mechanik chcę zmieniać status zlecenia.

**DoD:**
- Statusy: `Nowe`, `W trakcie`, `Zakończone`, `Anulowane`
- Tylko przypisany mechanik lub Admin może zmienić status
- Data zakończenia ustawiana automatycznie dla „Zakończone”

---

#### ✅ US10: Jako użytkownik chcę komentować zlecenie (wewnętrznie).

**DoD:**
- Komentarz: autor, treść, data
- Komentarze widoczne chronologicznie
- Tylko zalogowani użytkownicy mogą komentować

---

### 📈 **Raporty i katalog części**

---

#### ✅ US11: Jako administrator chcę dodać części zamienne do katalogu.

**DoD:**
- CRUD części: nazwa, typ, cena jednostkowa
- Widoczność tylko dla `Admin` i `Recepcjonista`

---

#### ✅ US12: Jako recepcjonista chcę wygenerować raport kosztów napraw klienta.

**DoD:**
- Lista napraw klienta z sumami kosztów (robocizna + części)
- Filtrowanie po miesiącu / pojeździe
- Widok + opcjonalnie PDF

---

#### ✅ US13: Jako administrator chcę pobrać raport PDF napraw wykonanych w miesiącu.

**DoD:**
- Wybór miesiąca + generowanie zestawienia
- Zawiera: klient, pojazd, suma kosztów, liczba zleceń
- Możliwość pobrania jako `.pdf`

---

