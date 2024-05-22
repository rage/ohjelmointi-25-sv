---
path: '/osa-7/6-lisaa-pythonista'
title: 'Flera funktionaliteter i Python'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* har du bekantat dig med några fler funktionaliteter i Python.

</text-box>

För att knyta ihop den här kursen, ska du ännu få en lista av nyttiga funktionaliteter som Python har att erbjuda.

## If-satser på en rad

Följande satser ger samma resultat:

```python
if x%2 == 0:
    print("parillinen")
else:
    print("pariton")
```

```python
print("parillinen" if x%2 == 0 else "pariton")
```

I det senare exemplet har vi en if-sats i enradsformat: `a if [villkor] else b`. Värdet för uttrycket blir `a` då villkoret är sant och `b` i övriga fall. På engelska kallas detta ternary operator.

If-satser kan användas då man vill tilldela något värde baserat på ett villkor. Till exempel om du har variablerna `x` och `y` och vill antingen öka eller ändra på `y`:s värde baserat på `x` paritet (jämnt/udda tal), kan du använda en normal if-else-sats:

```python
if x%2 == 0:
    y += 1
else:
    y = 0
```

Eller så kan du göra det hela med en rad kod:

```python
y = y + 1 if x%2 == 0 else 0
```

## Ett ”tomt” block

Du minns kanske att block inte kan vara tomma i Python. Om du behöver ett block som inte gör någonting – till exempel då du testar någon annan funktionalitet – kan du använda `pass`-kommandot. Du kan till exempel skapa en funktion som inte gör någonting:

```python
def testi():
    pass
```

Funktionen kommer att returnera direkt. Om `pass`-kommandot lämnas bort, kommer koden att ge ett fel, eftersom block inte kan vara tomma.

```python
def testi():
```

## Loopar med else-block

I Python kan loopar också ett `else`-block. Koden inom det här blocket körs då loopen avslutas normalt.

Till exempel här går vi igenom en lista med siffror. Om det finns ett jämnt tal i listan, kommer ett meddelande att skrivas ut och loopen avslutas. Om det inte finns några jämna tal, kommer loopen att avslutas vanligt, men ett annat meddelande skrivs ut:

```python
lista = [3,5,2,8,1]
for x in lista:
    if x%2 == 0:
        print("löytyi parillinen", x)
        break
else:
    print("ei löytynyt parillista")
```

Ett mera traditionellt sätt att göra det här är att använda en hjälpvariabel som minns om en viss typ av element har hittats:

```python
lista = [3,5,2,8,1]
loytyi = False
for x in lista:
    if x%2 == 0:
        print("löytyi parillinen", x)
        loytyi = True
        break
if not loytyi:
    print("ei löytynyt parillista")
```

Att använda en for-else-sats sparar oss den tid som skulle krävas för att skapa en hjälpvariabel och logiken kring den.

## Standardvärde för en parameter

I Python kan funktioners parametrar ha ett standardvärde. Det används då ett argument inte ges till en funktion då den anropas. Se följande exempel:

```python
def tervehdi(nimi="Emilia"):
    print("Moikka,", nimi)

tervehdi()
tervehdi("Erkki")
tervehdi("Matti")
```

<sample-output>

Moikka, Emilia
Moikka, Erkki
Moikka, Matti

</sample-output>

Obs! En tom sträng är fortfarande en sträng. Standardvärdet kommer inte att användas om en tom sträng ges som argument till en funktion.

## Ändrande antal parametrar

Du kan också definiera att en funktion har ett ändrande antal parametrar, genom att lägga till en asterisk för parameternamnet. Alla argument som ges till funktionen lagras i en tuple som kan kommas åt genom den namngivna parametern.

Följande funktion räknar antalet argument som getts samt summan av dem:

```python
def testi(*lista):
    print("Annoit", len(lista), "parametria")
    print("Niiden summa on", sum(lista))

testi(1, 2, 3, 4, 5)
```

<sample-output>

Annoit 5 parametria
Niiden summa on 15

</sample-output>

<programming-exercise name='Oma ohjelmointikieli' tmcname='osa07-18_oma_ohjelmointikieli'>

Tässä tehtävässä toteutetaan oman ohjelmointikielen suorittaja. Voit käyttää tehtävässä kaikkia kurssilla oppimiasi taitoja.

Ohjelma muodostuu riveistä, joista jokainen on yksi seuraavista:

* `PRINT [arvo]`: tulostaa annetun arvon
* `MOV [muuttuja] [arvo]`: asettaa muuttujaan annetun arvon
* `ADD [muuttuja] [arvo]`: lisää muuttujaan annetun arvon
* `SUB [muuttuja] [arvo}`: vähentää muuttujasta annetun arvon
* `MUL [muuttuja] [arvo]`: kertoo muuttujan annetulla arvolla
* `[kohta]:`: määrittelee kohdan, johon voidaan hypätä muualta
* `JUMP [kohta]`: hyppää annettuun kohtaan
* `IF [ehto] JUMP [kohta]`: jos ehto pätee, hyppää annettuun kohtaan
* `END`: lopettaa ohjelman

Ohjelmaa suoritetaan rivi kerrallaan ensimmäisestä rivistä aloittaen. Ohjelma päättyy, kun vastaan tulee komento `END` tai suoritus menee ohjelman viimeisen rivin yli.

Jokaisessa ohjelmassa on 26 muuttujaa, joiden nimet ovat `A`...`Z`. Jokaisen muuttujan arvo on 0 ohjelman alussa. Merkintä `[muuttuja]` viittaa tällaiseen muuttujaan.

Kaikki ohjelman käsittelemät arvot ovat kokonaislukuja. Merkintä `[arvo]` viittaa joko muuttujaan tai kokonaislukuna annettuun arvoon.

Merkintä `[kohta]` on mikä tahansa kohdan nimi, joka muodostuu pienistä kirjaimista `a`...`z` sekä numeroista `0`...`9`. Kahdella kohdalla ei saa olla samaa nimeä.

Merkintä `[ehto]` tarkoittaa ehtoa muotoa `[arvo] [vertailu] [arvo]`. Tässä `[vertailu]` on aina yksi seuraavista: `==`, `!=`, `<`, `<=`, `>` tai `>=`.

Tee funktio `suorita(ohjelma)`, jolle annetaan ohjelma listana. Jokainen listan alkio on yksi ohjelman rivi. Funktion tulee palauttaa listana kaikki `PRINT`-komentojen tulokset ohjelman suorituksen aikana.

Voit olettaa, että funktiolle annettu ohjelma on oikeanmuotoinen, eli funktion ei tarvitse toteuttaa virheenkäsittelyä.

Tehtävästä on saatavilla kaksi pistettä: saat yhden pisteen, jos komennot `PRINT`, `MOV`, `ADD`, `SUB`, `MUL` ja `END` toimivat, ja vielä toisen pisteen, jos myös loput silmukoihin liittyvät komennot toimivat.

Esimerkki 1:

```python
ohjelma1 = []
ohjelma1.append("MOV A 1")
ohjelma1.append("MOV B 2")
ohjelma1.append("PRINT A")
ohjelma1.append("PRINT B")
ohjelma1.append("ADD A B")
ohjelma1.append("PRINT A")
ohjelma1.append("END")
tulos = suorita(ohjelma1)
print(tulos)
```

<sample-output>

[1, 2, 3]

</sample-output>

Esimerkki 2:

```python
ohjelma2 = []
ohjelma2.append("MOV A 1")
ohjelma2.append("MOV B 10")
ohjelma2.append("alku:")
ohjelma2.append("IF A >= B JUMP loppu")
ohjelma2.append("PRINT A")
ohjelma2.append("PRINT B")
ohjelma2.append("ADD A 1")
ohjelma2.append("SUB B 1")
ohjelma2.append("JUMP alku")
ohjelma2.append("loppu:")
ohjelma2.append("END")
tulos = suorita(ohjelma2)
print(tulos)
```

<sample-output>

[1, 10, 2, 9, 3, 8, 4, 7, 5, 6]

</sample-output>

Esimerkki 3 (kertoma):

```python
ohjelma3 = []
ohjelma3.append("MOV A 1")
ohjelma3.append("MOV B 1")
ohjelma3.append("alku:")
ohjelma3.append("PRINT A")
ohjelma3.append("ADD B 1")
ohjelma3.append("MUL A B")
ohjelma3.append("IF B <= 10 JUMP alku")
ohjelma3.append("END")
tulos = suorita(ohjelma3)
print(tulos)
```

<sample-output>

[1, 2, 6, 24, 120, 720, 5040, 40320, 362880, 3628800]

</sample-output>

Esimerkki 4 (alkuluvut):

```python
ohjelma4 = []
ohjelma4.append("MOV N 50")
ohjelma4.append("PRINT 2")
ohjelma4.append("MOV A 3")
ohjelma4.append("alku:")
ohjelma4.append("MOV B 2")
ohjelma4.append("MOV Z 0")
ohjelma4.append("testi:")
ohjelma4.append("MOV C B")
ohjelma4.append("uusi:")
ohjelma4.append("IF C == A JUMP virhe")
ohjelma4.append("IF C > A JUMP ohi")
ohjelma4.append("ADD C B")
ohjelma4.append("JUMP uusi")
ohjelma4.append("virhe:")
ohjelma4.append("MOV Z 1")
ohjelma4.append("JUMP ohi2")
ohjelma4.append("ohi:")
ohjelma4.append("ADD B 1")
ohjelma4.append("IF B < A JUMP testi")
ohjelma4.append("ohi2:")
ohjelma4.append("IF Z == 1 JUMP ohi3")
ohjelma4.append("PRINT A")
ohjelma4.append("ohi3:")
ohjelma4.append("ADD A 1")
ohjelma4.append("IF A <= N JUMP alku")
tulos = suorita(ohjelma4)
print(tulos)
```

<sample-output>

[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]

</sample-output>

</programming-exercise>

Vänligen svara på kursfeedbacksenkäten här nedan. Enkätens resultat hjälper oss att utveckla och förbättra den här kursen.

<quiz id="e5513330-0599-5fa0-bfd0-a2d40a89773e"></quiz>
