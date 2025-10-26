# Izveštaj o statičkoj analizi i metriki koda

Ovaj izveštaj se odnosi na projekat *calculator-java*.

## 1. LOC (broj linija koda)

| Fajl             | Linije koda (SLOC) |
|-----------------|---------------------|
| Calculator.java | 134                 |
| Start.java      | ~20                 |

Ukupno: oko **154** linija koda (bez praznih linija i komentara).

## 2. Neformalna statička analiza

Format: *fajl – linija – zapažanje*

 Calculator.java

- linija 7 – koristi se `float` za rezultat, preciznije je `double`.
- linije 12–21 – unutrašnja klasa samo za operatore, moglo je jednostavnije sa konstantama.
- linija 23 – `ToString()` ne prati Java konvenciju (`toString`).
- linija 30 – `Run()` bi trebalo da bude `run()` (konvencija imenovanja).
- linija 42 – nema provere praznog stringa pre `charAt(0)`, može izazvati grešku.
  previše `static` metoda, otežava testiranje i kasniji razvoj.
  nema validacije neispravnih izraza (slova, dva operatora zaredom, prazno itd.)
  nema obrade podele nulom.

 Start.java

- `main` metoda radi i unos i računanje → bolje je odvojiti logiku.
- nema `try/catch` za greške prilikom računanja.
- `Scanner` se ne zatvara.
- poruke su direktno u kodu (hardcodirane).

3. Zaključak

Kod je funkcionalan za osnovne operacije, ali nedostaje validacija ulaza i obrada grešaka.  
Upotreba `static` metoda ograničava proširenje i testiranje.  
Moguća poboljšanja:
- koristiti `double` umesto `float`
- proveriti ispravnost izraza pre računanja
- preimenovati metode prema Java konvenciji
- odvojiti unos/ispis od logike
- dodati rukovanje izuzecima i zatvaranje resursa

LOC je izmeren ručno pregledom fajlova i na osnovu GitHub prikaza SLOC-a za `Calculator.java`.  
Za `Start.java` je procena napravljena ručno na osnovu sadržaja fajla, jer je mali i jednostavan.

