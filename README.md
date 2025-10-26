# Izveštaj o statičkoj analizi i metriki koda

Ovaj izveštaj se odnosi na projekat *calculator-java*.

## 1. LOC (broj linija koda)

| Fajl             | Linije koda (SLOC) |
|-----------------|---------------------|
| Calculator.java | 134                 |
| Start.java      | ~19                 |

Ukupno: oko **154** linija koda (bez praznih linija i komentara).

## 2. Neformalna statička analiza

Format: *fajl – linija – zapažanje*

 Calculator.java

Calculator.java – L6 – Globalna statička promenljiva finalResult → nepotrebno globalno stanje, nije thread-safe; rezultat treba vraćati iz metode, ne čuvati u polju.

Calculator.java – L24 & L78 – Imena metoda Run/Calculate počinju velikim slovom → kršenje Java konvencije (treba run, calculate). Nije funkcionalna greška, ali je velika stilska.

Calculator.java – L28–38 – Pretpostavlja da je izraz neprazan i da charAt(0) postoji. Prazan string ili null ruši program (StringIndexOutOfBoundsException). Nedostaje osnovna validacija ulaza (trim, prazno, nedozvoljeni znakovi).

Calculator.java – L64–68 – Rukovanje greškama: vraća se string "ERROR" iz evaluateExpression. Mešaju se podaci i poruke o grešci; umesto toga baciti izuzetak (npr. NumberFormatException) ili koristiti rezultat sa statusom.

Calculator.java – L10–13 & kroz ceo kod – Računanje u float → značajan gubitak preciznosti u kalkulatoru. Za aritmetiku treba bar double ili još bolje BigDecimal (posebno za deljenje/zaokruživanje).

Calculator.java – L74–186 (metoda Calculate)  Veoma duga i rekurzivna metoda sa stalnim mutiranjem listi i remove() pozivima. 


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

