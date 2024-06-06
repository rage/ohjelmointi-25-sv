---
path: '/osa-12/2-generaattorit'
title: 'Generatorer'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Vet du vad en Python-generator är
- Kommer du  att känna till nyckelordet `yield`
- Kommer du att kunna skriva dina egna generator-funktioner

</text-box>

Vi har redan stött på situationer där vi har att göra med en serie föremål och vi behöver nästa föremål i serien, men vi vill inte nödvändigtvis formulera hela serien fram till den punkten varje gång ett nytt föremål krävs. Vissa rekursiva serier, till exempel Fibonacci-numret, är ett bra exempel på en sådan situation. Om varje funktionsanrop rekursivt genererar hela serien fram till önskad punkt, slutar det med att vi genererar början av serien många gånger om.

Python-generatorer är ett sätt att bara producera nästa föremål i en serie när det behövs, vilket i princip innebär att genereringsprocessen för serien bara körs en gång (för en viss exekvering av ett program). De fungerar i stort sett som vanliga funktioner, eftersom de kan anropas och returnerar värden, men det värde som en generatorfunktion returnerar skiljer sig från en vanlig funktion. En normal funktion ska returnera samma värde varje gång, givet samma argument. En generatorfunktion, å andra sidan, ska komma ihåg sitt nuvarande tillstånd och returnera nästa föremål i serien, som kan skilja sig från föregående föremål.

Precis som det finns många sätt att lösa de flesta programmeringsproblem finns det många sätt att uppnå en funktionalitet som liknar generatorer, men generatorer kan bidra till att göra programmet lättare att förstå och kan i vissa situationer spara minne eller andra beräkningsresurser.

## Nyckelordet yield

En generatorfunktion måste innehålla nyckelordet `yield`, som markerar det värde som funktionen returnerar. Låt oss titta på en funktion som genererar heltal, med början från noll och slut vid ett förutbestämt maxvärde:

```python

def laskuri(maksimi: int):
    luku = 0
    while luku <= maksimi:
        yield luku
        luku += 1

```

Nu kan `raknare`-funktionen skickas som argument till funktionen `nasta()`

```python
if __name__ == "__main__":
    luvut = laskuri(10)
    print("Eka arvo:")
    print(next(luvut))
    print("Toka arvo:")
    print(next(luvut))
```

<sample-output>

Eka arvo:
0
Toka arvo:
1

</sample-output>

Som du kan se i exemplet ovan liknar nyckelordet `yield` nyckelordet `return`: båda används för att definiera ett returvärde. Skillnaden är att `yield` inte "stänger" funktionen på samma sätt som `return`. En generatorfunktion med nyckelordet `yield` håller reda på sitt tillstånd och nästa gång den anropas kommer den att fortsätta från samma tillstånd.

Den här generatorn kräver också ett maxvärde, i exemplet ovan var det `10`. När generatorn får slut på värden kommer den att ge upphov till ett `StopIteration`-undantag:

```python
if __name__ == "__main__":
    luvut = laskuri(1)
    print(next(luvut))
    print(next(luvut))
    print(next(luvut))
```

<sample-output>

0
1
Traceback (most recent call last):
  File "generaattoriesimerkki.py", line 11, in <module>
    print(next(luvut))
StopIteration

</sample-output>

Undantaget kan bli fångat med ett `try`- `except` block:

```python
if __name__ == "__main__":
    luvut = laskuri(1)
    try:
        print(next(luvut))
        print(next(luvut))
        print(next(luvut))
    except StopIteration:
        print("Luvut loppuivat kesken")
```

<sample-output>

0
1
Luvut loppuivat kesken

</sample-output>

Att gå igenom alla objekt i en generator görs enkelt med en `for`-loop:  

```python
if __name__ == "__main__":
    luvut = laskuri(5)
    for luku in luvut:
        print(luku)
```

<sample-output>

0
1
2
3
4
5

</sample-output>

Generatorer behöver inte ha ett definierat maxvärde eller en slutpunkt. De kan generera värden i det oändliga (naturligtvis inom andra beräkningsmässiga och fysiska begränsningar).

Tänk dock på att det bara fungerar att genomkorsa en generator med en `for`-loop om generatorn avslutas vid någon punkt. Om generatorn är uppbyggd på en oändlig loop kommer en enkel `for`-loop att orsaka en oändlig exekvering, precis som en `while`-loop utan slut- eller brytvillkor.

<programming-exercise name='Parilliset luvut' tmcname='osa12-08_parilliset'>

Kirjoita generaattorifunktio `parilliset(alku: int, maksimi: int)`, joka saa parametrikseen alkuarvon ja maksimin. Funktio tuottaa alkuarvosta lähtien parillisia lukuja. Kun saavutetaan maksimi, generaattori pysähtyy.

Kaksi esimerkkiä funktion käytöstä:

```python
luvut = parilliset(2, 10)
for luku in luvut:
    print(luku)
```

<sample-output>

2
4
6
8
10

</sample-output>

```python
luvut = parilliset(11, 21)
for luku in luvut:
    print(luku)
```

<sample-output>

12
14
16
18
20

</sample-output>

</programming-exercise>

<programming-exercise name='Alkuluvut' tmcname='osa12-09_alkuluvut'>

Alkuluvuksi sanotaan kokonaislukua, joka on vähintään 2 ja jaollinen ainoastaan 1:llä ja itsellään. Ensimmäiset alkuluvut ovat 2, 3, 5, 7, 11 ja 13.

Kirjota generaattorifunktio `alkuluvut()`, joka luo uuden generaattorin. Generaattori palauttaa yksi kerrallaan alkulukuja järjestyksessä 2:sta alkaen. Huomaa, että generaattori ei pysähdy koskaan, vaan palauttaa lisää lukuja niin kauan kuin niitä pyydetään.

Esimerkiksi:

```python
luvut = alkuluvut()
for i in range(8):
    print(next(luvut))
```

<sample-output>

2
3
5
7
11
13
17
19

</sample-output>

Vinkki: Voit tarkastaa, onko luku _x_ alkuluku, silmukalla, joka käy läpi luvut 2:sta lukuun _x_–1 asti. Jos jokin näistä luvuista jakaa _x_:n, niin se ei ole alkuluku.

</programming-exercise>


## Generator comprehensions

Du behöver inte nödvändigtvis en funktionsdefinition för att skapa en generator. Vi kan använda en struktur som liknar en list comprehension istället. Den här gången använder vi runda parenteser för att beteckna en generator i stället för en lista eller en ordlista: 

```python
# Generaattori palauttaa 2:n potensseja
neliot = (x ** 2 for x in range(1, 64))

print(neliot)

for i in range(5):
    print(next(neliot))
```

<sample-output>

<generator object &lt;genexpr&gt; at 0x000002B4224EBFC0>
1
4
9
16
25

</sample-output>

I följande exempel skriver vi ut delsträngar av det engelska alfabetet, var och en tre tecken lång. Detta skriver ut de första 10 objekten i generatorn:

```python
alijonot = ("abcdefghijklmnopqrstuvwxyz"[i : i + 3] for i in range(24))

# tulostetaan ensimmäiset 10 alijonoa
for i in range(10):
    print(next(alijonot))
```

<sample-output>

abc
bcd
cde
def
efg
fgh
ghi
hij
ijk
jkl

</sample-output>

<programming-exercise name='Satunnaiset sanat' tmcname='osa12-10_satunnaiset_sanat'>

Tee funktio `sanageneraattori(kirjaimet: str, pituus: int, maara: int)`, joka muodostaa ja palauttaa annettujen parametrien avulla satunnaisia sanoja tuottavan generaattorin.

Satunnainen sana muodostetaan valitsemalla `pituus` kappaletta kirjaimia valikoimasta `kirjaimet`. Sama kirjain saa esiintyä sanassa monta kertaa.

Generaattori palauttaa `maara` kappaletta sanoja ennen kuin se pysähtyy.

Esimerkki funktion kutsumisesta:

```python
sanagen = sanageneraattori("abcdefg", 3, 5)
for sana in sanagen:
    print(sana)
```

<sample-output>

dbf
baf
ead
fga
ccc

</sample-output>

Huom! Voit ratkaista tehtävän itse valitsemallasi tavalla (eli käyttäen joko generaattorikoostetta tai "perinteistä" generaattoria).

</programming-exercise>
