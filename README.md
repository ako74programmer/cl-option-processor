# cl-option-processor

### Wyjaśnienie kodu

#### 1. **Cel programu**
Ten kod to skrypt napisany w języku CL (Control Language), używanym w systemach IBM iSeries. Jego celem jest przetwarzanie określonego parametru wejściowego (`&OPTION`) i wykonywanie odpowiednich działań na jego podstawie. Dodatkowo obsługuje on błędy, monitoruje pewne operacje oraz umożliwia wielokrotne wykonywanie operacji w zależności od odpowiedzi użytkownika.

#### 2. **Dane wejściowe**
Program przyjmuje jeden parametr wejściowy `&OPTION`, który jest pojedynczym znakiem (`A`, `B`, lub `C`). Parametr ten decyduje o dalszym przebiegu programu.

#### 3. **Dane wyjściowe**
- Komunikaty informacyjne dla użytkownika, takie jak np. "Action for Option A executed" lub "An error occurred".
- W przypadku błędów lub nieprawidłowych danych wejściowych, wyświetlane są odpowiednie komunikaty.
- Możliwe jest wielokrotne wykonanie programu, jeśli użytkownik wybierze opcję restartu (`R`).

#### 4. **Logika i algorytm**
Program działa w kilku krokach:
1. **Inicjalizacja zmiennych:** Definiuje zmienne, takie jak `&OPTION` (parametr wejściowy), `&STATUS` (status działania programu), czy `&RETRYNBR` (licznik prób).
2. **Sprawdzanie poprawności parametru:** Za pomocą podprogramu `CHECKPARAM` weryfikowane jest, czy parametr `&OPTION` został przekazany. Jeśli nie, wyświetla komunikat o braku parametru i kończy działanie.
3. **Przetwarzanie parametru:** Na podstawie wartości `&OPTION` ustawia zmienną `&STATUS`:
   - `A` -> `Option A selected`
   - `B` -> `Option B selected`
   - `C` -> `Option C selected`
   - Jeśli wartość jest inna, przekierowuje do etykiety `ERROR`.
4. **Wykonywanie działań:** Korzystając z konstrukcji `SELECT`, program wykonuje odpowiednią akcję dla wybranej opcji (`A`, `B`, `C`) lub wyświetla komunikat o błędzie, jeśli status jest nieprawidłowy.
5. **Obsługa błędów:** Monitoruje operacje, takie jak usunięcie obiektu (`DLTOBJ`), i przechwytuje błędy, np. gdy obiekt nie istnieje (`MONMSG`).
6. **Zapętlenie:** Program pozwala użytkownikowi wielokrotnie go uruchamiać. W odpowiedzi na komunikat użytkownik może wybrać:
   - `R` (restart programu) – resetuje licznik prób i ponownie uruchamia.
   - `C` (cancel) – kończy działanie programu.
7. **Zakończenie:** Program kończy się komunikatem o pomyślnym zakończeniu lub błędzie, w zależności od przebiegu.

#### 5. **Ważne przepływy logiczne i przekształcenia danych**
- **Walidacja:** Podprogram `CHECKPARAM` weryfikuje, czy parametr został przekazany. To kluczowy krok, by uniknąć błędów w późniejszych etapach.
- **Warunkowe operacje:** Za pomocą instrukcji `IF` i `SELECT`, program przetwarza dane wejściowe i wykonuje odpowiednie działania.
- **Zapętlenie i obsługa użytkownika:** Licznik `&RETRYNBR` kontroluje maksymalną liczbę prób, a interakcja z użytkownikiem pozwala na wybór dalszych kroków (restart lub zakończenie).
- **Monitorowanie błędów:** Instrukcja `MONMSG` przechwytuje błędy, co zapobiega przerwaniu działania programu przez nieprzewidziane problemy.

### Podsumowanie
Program realizuje podstawowy system przetwarzania danych wejściowych z kontrolą błędów i interakcją z użytkownikiem. Jest elastyczny dzięki obsłudze wielu opcji i możliwości ponownego uruchamiania. Mechanizmy takie jak zapętlenie i monitorowanie błędów czynią go odpornym na typowe problemy w środowisku operacyjnym IBM iSeries.