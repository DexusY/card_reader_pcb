# Projekt płytki rozwojowej ESP32

Projekt przedstawia schemat wraz z płytką drukowaną prototypowego układu do odblokowywania drzwi, poprzez podłączony moduł czytnika kart nfc oraz ESP32 do komunikacji z serwerem z bazą danych zawierającą dane o akredytacji konkretnej karty. Schemat ideowy prezentuje się następująco:

##
Schemat Ideowy
<img width="2286" height="800" alt="image" src="https://github.com/user-attachments/assets/ece6e792-529c-4407-8832-0c5f57d89a61" />

##

## 
Główne Cechy

* **Mikrokontroler:** ESP32-WROOM-32E (U2) 
* **Zasilanie:** Wejście 12V przez złącze śrubowe (J1) 
* **Regulator napięcia:** Wbudowana przetwornica step-down 3.3V (U1 - LMR51610-Q1)
* **Złącze programowania:** Wyprowadzone 5 pinów do zaprogramowania ESP32, przy podłączonym zasilaniu całego układu 
* **Wskaźniki LED:** Trzy programowalne diody LED (zielona, żółta, czerwona), do sygnalizowania stanów
* **Brzęczyk:**
* **Przekaźnik:**
* **Zabezpieczenia:** Dioda Schottky (D1) chroniąca przed odwrotną polaryzacją.
* **Filtrowanie:** Dławik ferrytowy (FB1) na wyjściu 3.3V dla czystszego zasilania.

## 
Podział schematu

##
