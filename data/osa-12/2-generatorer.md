---
path: '/osa-12/2-generatorer'
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

def raknare(maximum: int):
    tal = 0
    while tal <= maximum:
        yield tal
        tal += 1

```

Nu kan `raknare`-funktionen skickas som argument till funktionen `next()`

```python
if __name__ == "__main__":
    talen = raknare(10)
    print("Första värde:")
    print(next(talen))
    print("Andra värde:")
    print(next(talen))
```

<sample-output>

Första värde:
0
Andra värde:
1

</sample-output>

Som du kan se i exemplet ovan liknar nyckelordet `yield` nyckelordet `return`: båda används för att definiera ett returvärde. Skillnaden är att `yield` inte "stänger" funktionen på samma sätt som `return`. En generatorfunktion med nyckelordet `yield` håller reda på sitt tillstånd och nästa gång den anropas kommer den att fortsätta från samma tillstånd.

Den här generatorn kräver också ett maxvärde, i exemplet ovan var det `10`. När generatorn får slut på värden kommer den att ge upphov till ett `StopIteration`-undantag:

```python
if __name__ == "__main__":
    talen = raknare(1)
    print(next(talen))
    print(next(talen))
    print(next(talen))
```

<sample-output>

0
1
Traceback (most recent call last):
  File "generatorexempel.py", line 11, in <module>
    print(next(talen))
StopIteration

</sample-output>

Undantaget kan bli fångat med ett `try`- `except` block:

```python
if __name__ == "__main__":
    talen = raknare(1)
    try:
        print(next(talen))
        print(next(talen))
        print(next(talen))
    except StopIteration:
        print("Talen tog slut")
```

<sample-output>

0
1
Talen tog slut

</sample-output>

Att gå igenom alla objekt i en generator görs enkelt med en `for`-loop:

```python
if __name__ == "__main__":
    talen = raknare(5)
    for tal in talen:
        print(tal)
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

<programming-exercise name='Jämna tal' tmcname='osa12-08_jamna'>

Skapa generatorfunktionen `jamna(borjan: int, maximum: int)`, som tar två heltal som argument. Funktionen ska producera jämna tal börjandes från `borjan` och slutandes vid, senast, `maximum`.

Två exempel på användning av funktionen:

```python
talen = jamna(2, 10)
for tal in talen:
    print(tal)
```

<sample-output>

2
4
6
8
10

</sample-output>

```python
talen = jamna(11, 21)
for tal in talen:
    print(tal)
```

<sample-output>

12
14
16
18
20

</sample-output>

</programming-exercise>

<programming-exercise name='Primtal' tmcname='osa12-09_primtal'>

Ett primtal är ett tal som är delbart endast med sig självt och talet 1. Enligt konvention definieras primtal som positiva heltal från talet 2 och uppåt. De sex första primtalen är 2, 3, 5, 7, 11 och 13.

Skapa en generatorfunktion `primtal()` som skapar en ny generator. Generatorn ska returnera nya primtal, ett efter ett i sekvens, från 2 framåt. OBS: den här generatorn avslutas aldrig. Den kommer att generera tal så länge som de behövs.

Till exempel

```python
talen = primtal()
for i in range(8):
    print(next(talen))
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

**Tips:** du kan använda en loop för att granska ifall ett tal är ett primtal. Ifall vi granskar talet `x` skulle loopen gå igenom talen `2` till `x-1`. Ifall `x` är dividerbart med någon av dessa, är det inte ett primtal.

</programming-exercise>


## Generator comprehensions

Du behöver inte nödvändigtvis en funktionsdefinition för att skapa en generator. Vi kan använda en struktur som liknar en list comprehension istället. Den här gången använder vi runda parenteser för att beteckna en generator i stället för en lista eller en ordlista:

```python
# Generatorn returnerar kvadraten av heltal
kvadrat = (x ** 2 for x in range(1, 64))

print(kvadrat)

for i in range(5):
    print(next(kvadrat))
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
delstrangar = ("abcdefghijklmnopqrstuvwxyz"[i : i + 3] for i in range(24))

# skriver ut 10 första delsträngarna
for i in range(10):
    print(next(delstrangar))
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

<programming-exercise name='Slumpmässiga ord' tmcname='osa12-10_slumpmassiga_ord'>

Skapa funktionen `ordgenerator(bokstaver: str, langd: int, antal: int)`, som returnerar en ny generator som genererar nya, slumpmässiga ord baserat på de angiva parametrarna.

Ett slumpmässigt ord är genererat genom att välja från en sträng av `bokstaver` så många bokstäver som är indikerade av argumentet `langd`. Samma bokstav kan förekomma flera gånger i ett slumpmässigt ord.

Generatorn returnerar så många ord som specifierades i argumentet `antal` innan dess terminering.

Exempel på användning av generatorn:

```python
ordgen = ordgenerator("abcdefg", 3, 5)
for ord in ordgen:
    print(ord)
```

<sample-output>

dbf
baf
ead
fga
ccc

</sample-output>

OBS: Det är upp till dig hur du implementerar denna funktion. Du kan använda en "traditionell" generator eller en generator comprehension lika väl.

</programming-exercise>
