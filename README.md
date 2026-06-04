# Quick Pinger // Cyberpunk Enterprise Edition

**Quick Pinger** to nowoczesne, mobilne narzędzie diagnostyczne napisane w języku **Java** dla systemu Android. Aplikacja służy do badania struktury, stabilności oraz opóźnień sieci lokalnych i globalnych w czasie rzeczywistym. 

Projekt został zrealizowany w unikalnej estetyce **Premium Dark / Cyberpunk**, integrując wielowątkową analizę danych sieciowych niskiego poziomu z bogatym systemem mikro-interakcji (multimedia, haptic feedback).

---

## 🎯 Cel i Zastosowanie Projektu
Aplikacja została stworzona w ramach przedmiotu *Pracownia programowania aplikacji mobilnych* (Nauczyciel: Adam Marciniak). 

Głównym celem technologicznym było wdrożenie asynchronicznego zarządzania zasobami systemowymi, stabilna obsługa wątków tła (izolacja operacji I/O od głównego wątku UI) oraz zaprezentowanie zaawansowanego projektowania interfejsów użytkownika (Custom UI/UX) przy użyciu komponentów materialnych.

---

## 🛠️ Główna Funkcjonalność (Premium Features)

Aplikacja została wyposażona w 5 unikalnych modułów inżynieryjnych:

1. **Moduł Diagnostyki Wielowątkowej (Ultra-Ping):** Zamiast pojedynczego zapytania, aplikacja wykonuje w tle serię 5 następujących po sobie testów `isReachable`. Na podstawie zebranych danych algorytm oblicza i wyświetla zaawansowaną statystykę w czasie rzeczywistym w formacie: `AVG (Średni) // MIN // MAX` oraz procentową stratę pakietów (`Loss`).
2. **Akustyczny Sondaż Sieciowy (Audio Feedback):** Integracja z systemowym generatorem fal `ToneGenerator`. Aplikacja wydaje dynamiczne dźwięki o zmiennej częstotliwości i długości w zależności od stanu sieci. Niski ping generuje krótki, wysoki sygnał radaru, natomiast awaria hosta (Offline) wywołuje ciężki, niski dźwięk ostrzegawczy.
3. **Haptyczna Informacja Zwrotna (Taktylny Odzew):** Projekt wykorzystuje systemowy silnik wibracyjny (`Vibrator`). Pomyślna diagnostyka potwierdzana jest subtelnym, mikro-kliknięciem urządzenia (20ms). Wykrycie braku połączenia (Timeout) generuje agresywny, przerywany schemat wibracji ostrzegawczych.
4. **Inteligentny Cyber-Randomizer (Szybki Wybór):** Zaimplementowana lista predefiniowanych hostów premium (m.in. Google DNS, Cloudflare DNS, bramy sieciowe oraz dedykowane serwery gier online). Pozwala na natychmiastowe testowanie stabilności połączenia bez konieczności ręcznego wpisywania adresu IP.
5. **Kinetyczny Rejestr Zdarzeń (Log System):** Wykorzystanie pamięci lokalnej `SharedPreferences` do stworzenia cyklicznego bufora historii operacji. Ostatnie 5 unikalnych testów jest stale zapisywanych i wyświetlanych w formie tekstowego logu systemowego pod panelem głównym.

---

## 🎨 Specyfikacja UI/UX (Warstwa Wizualna)
* **Głębia Ciemnego Trybu:** Tło główne w kolorze `#0B0B0F` połączone z elementami neonowego fioletu (`#8B5CF6`), co minimalizuje zmęczenie oczu i nadaje aplikacji nowoczesny styl.
* **Reactive Views:** Pole tekstowe `EditText` posiada dynamiczny selektor (Custom Drawable) — podczas wpisywania adresu jego ramka rozświetla się neonową poświatą.
* **Status LED:** Specjalny, okrągły komponent graficzny symulujący fizyczną diodę LED na obudowie serwera (Pomarańczowy: Diagnostyka, Zielony: Online, Czerwony: Offline).
* **Czcionka Monospace:** Opóźnienia sieciowe (ms) wyświetlane są za pomocą czcionki o stałej szerokości znaków, imitując profesjonalną konsolę administratora lub terminal Linux.

---

## 🔒 Bezpieczeństwo i Stabilność Kodu
* **Odseparowanie Wątków:** Wszystkie operacje sieciowe I/O są izolowane od głównego wątku za pomocą `ExecutorService`, co całkowicie eliminuje krytyczny błąd `NetworkOnMainThreadException`.
* **Walidacja Danych Wejściowych:** Aplikacja natychmiast wykrywa puste zapytania, blokuje wykonanie pustej pętli i informuje użytkownika za pomocą komunikatu `Toast: "Adres IP / URL nie może być pusty!"`.
* **Zarządzanie Wyjątkami:** Każdy błąd hosta, nieprawidłowy format domeny czy nagłe zerwanie połączenia Wi-Fi jest przechwytywane przez blok `try-catch`, bezpiecznie przekazywane do wątku głównego przez `runOnUiThread()` i odpowiednio wizualizowane.

---

## 📦 Wymagania i Uprawnienia
Do poprawnego działania aplikacja wymaga dostępu do sieci. W pliku `AndroidManifest.xml` zaimplementowano odpowiednią regułę:
```xml
<uses-permission android:name="android.permission.INTERNET" />
