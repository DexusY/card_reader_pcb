# Projekt płytki rozwojowej ESP32

Projekt przedstawia schemat wraz z płytką drukowaną prototypowego układu do odblokowywania drzwi, poprzez podłączony moduł czytnika kart nfc oraz ESP32 do komunikacji z serwerem z bazą danych zawierającą dane o akredytacji konkretnej karty. Schemat ideowy prezentuje się następująco:

## 
Główne cechy

* **Mikrokontroler:** ESP32-WROOM-32E (U2) 
* **Zasilanie:** Wejście 12V przez złącze śrubowe (J1) 
* **Regulator napięcia:** Wbudowana przetwornica step-down 3.3V (U1 - TPSM82916VCER)
* **Złącze programowania/SPI:** Wyprowadzone 8-pinowe złącze (J2) [cite: 1418] z pinami UART, SPI oraz liniami do trybu programowania
* **Wskaźniki LED:** Trzy programowalne diody LED (zielona, żółta, czerwona)
* **Zabezpieczenia:** Dioda Schottky (D1) chroniąca przed odwrotną polaryzacją.
* **Filtrowanie:** Dławik ferrytowy (FB1) na wyjściu 3.3V dla czystszego zasilania.

## 
Podział schematu

Projekt można podzielić na trzy główne bloki funkcjonalne.

### 1. Sekcja zasilania

Obwód otrzymuje zasilanie **12V** przez złącze śrubowe `J1`. Napięcie to jest najpierw chronione przed odwrotną polaryzacją przez diodę Schottky `D1`.

Sercem tej sekcji jest moduł przetwornicy DC-DC (buck) `U1` (**TPSM82916VCER**)[cite: 1515], który efektywnie obniża napięcie 12V do **3.3V**.
* Kondensatory `C1` i `C2` filtrują napięcie wejściowe.
* Napięcie wyjściowe 3.3V jest stabilizowane przez dużą liczbę kondensatorów (`C3`-`C10`).
* Rezystory `R1` (15.2k) i `R2` (4.87k) tworzą dzielnik napięcia dla pinu sprzężenia zwrotnego (`FB`), ustawiając napięcie wyjściowe na ~3.3V.
* Dławik ferrytowy `FB1`  dodatkowo filtruje zasilanie 3.3V trafiające do modułu ESP32.

### 2. Mikrokontroler (ESP32)

Centralnym punktem projektu jest moduł `U2` (**ESP32-WROOM-32E**).
* Jest on zasilany bezpośrednio z przefiltrowanej linii **3.3V**.
* Obwód "Auto-Reset" (składający się z `R6` i `C11`) jest podłączony do pinu `EN`. Pozwala to na automatyczne wprowadzenie modułu w tryb programowania przez narzędzia takie jak `esptool`.

### 3. Peryferia (Złącza i Diody LED)

#### Złącze programowania i SPI (J2)

8-pinowe złącze `J2` udostępnia kluczowe piny do komunikacji i programowania:
* **Pin 1 (`EN`):** Linia Enable/Reset
* **Pin 2 (`IO0`):** Linia do wyboru trybu Boot
* **Pin 3 (`TXD0`):** UART TX
* **Pin 4 (`RXD0`):** UART RX
* **Pin 5 (`to_MISO`):** SPI MISO (GPIO13)
* **Pin 6 (`to_SCK`):** SPI SCK (GPIO14)
* **Pin 7 (`to_MOSI`):** SPI MOSI (GPIO12)
* **Pin 8 (`to_NSS`):** SPI CS/NSS (GPIO15)

#### Diody LED użytkownika

Trzy diody LED są podłączone do pinów GPIO modułu ESP32 i mogą być dowolnie kontrolowane przez użytkownika:
* **D2 (Zielona):** Podłączona do `IO21` przez rezystor `R3` (50Ω)
* **D3 (Żółta):** Podłączona do `IO19` przez rezystor `R4` (100Ω)
* **D4 (Czerwona):** Podłączona do `IO18` przez rezystor `R5` (100Ω)

## 
Lista głównych komponentów

| Oznaczenie | Komponent | Opis |
| :--- | :--- | :--- |
| U1 | `TPSM82916VCER` | Przetwornica DC-DC step-down 12V na 3.3V |
| U2 | `ESP32-WROOM-32E`  | Moduł Mikrokontrolera Wi-Fi/Bluetooth |
| J1 | `Screw_Terminal_01x02`  | Główne złącze zasilania 12V |
| J2 | `Conn_01x08`  | Złącze programowania / SPI |
| D1 | `D_Schottky`  | Dioda zabezpieczająca przed odwrotną polaryzacją |
| D2, D3, D4 | `LED`  | Diody LED użytkownika (Zielona, Żółta, Czerwona) |
| FB1 | `FerriteBead`  | Dławik ferrytowy do filtrowania 3.3V |
| R1, R2 | Rezystory | Dzielnik napięcia dla U1  |
| R3, R4, R5 | Rezystory | Ograniczenie prądu dla diod LED  |
| R6, C11 | R/C | Obwód auto-resetu dla U2  |

## 
Jak używać

1.  Podłącz stabilizowane źródło zasilania **12V DC** do złącza śrubowego `J1`.
2.  Użyj programatora UART-USB (np. FTDI) i podłącz go do pinów `GND`, `TXD0`, `RXD0`, `EN` i `IO0` na złączu `J2`.
3.  Użyj oprogramowania `esptool.py` lub Arduino IDE / PlatformIO, aby wgrać swój kod. Obwód auto-resetu powinien automatycznie wprowadzić moduł w tryb programowania.
4.  Wykorzystaj piny `IO21`, `IO19` i `IO18`  do sterowania diodami LED.
