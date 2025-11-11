# Projekt płytki rozwojowej ESP32

Projekt przedstawia schemat wraz z płytką drukowaną prototypowego układu do odblokowywania drzwi, poprzez podłączony moduł czytnika kart RFID oraz ESP32 do komunikacji z serwerem z bazą danych zawierającą dane o akredytacji konkretnej karty. Schemat ideowy prezentuje się następująco:

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

Regulacja wejściowego zasilania do poziomu 3,3V z 1A na wyjściu prezentuje się poniżej. Dobrane wartości komponentów do regulatora wynika z kalkulatora dostarczonego od producenta.
<img width="2056" height="1120" alt="image" src="https://github.com/user-attachments/assets/0b27f01f-0517-40b6-8301-0b98eee7fb72" />

<img width="1925" height="648" alt="image" src="https://github.com/user-attachments/assets/52c9424c-d8e3-4ef2-93ca-f8972ecde0db" />

Złącza programowania oraz żeńskie goldpin do podłączenia modułu kart RFID
<img width="532" height="324" alt="image" src="https://github.com/user-attachments/assets/bc10cc69-d118-4666-a312-a271b73706a9" />

wyprowadzenia pinów ESP32 
<img width="1555" height="1228" alt="image" src="https://github.com/user-attachments/assets/852a0f23-9df4-4921-b2b1-f9743f381d10" />

Obwód sterownika przekaźnika (Wyjście wykonawcze)
<img width="1568" height="372" alt="image" src="https://github.com/user-attachments/assets/f409fbfb-c311-43ad-a14a-5154354a3ad2" />

##
