---
path: '/osa-3/3-mer-om-loopar'
title: 'Mera om loopar'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* vet du när `break`-instruktionen behövs för att avsluta en loop
* kan du använda `continue`-instruktionen för att fortsätta till nästa iteration
* förstår du hur nästlade loopar fungerar.

</text-box>

## `break`-instruktionen

Du har redan bekantat dig med `break`-instruktionen. Det kan användas för att direkt avsluta en loop. Ett exempel på ett användningsområde är då man ber användaren om någon information och loopen ska avslutas när ett visst värde matats in.

Samma funktionalitet kan skapas utan `break`-instruktionen genom att formulera ett lämpligt villkorsuttryck för while-loopen. Följande två program ber användaren mata in tal som adderas ihop tills användaren matar in -1.

```python
# version 1 med break-instruktion

summa = 0

while True:
    tal = int(input("Ge ett tal, -1 avslutar programmet: "))
    if tal == -1:
        break
    summa += tal

print (f"Summan är {summa}")
```

```python
# version 2 utan break-instruktion

summa = 0
tal = 0

while tal != -1:
    tal = int(input("Ge ett tal, -1 avslutar programmet: "))
    if tal != -1:
        summa += tal

print (f"Summan är {summa}")
```

Båda programmen ger samma utskrift med samma indata, exempelvis:

<sample-output>

Ge ett tal, -1 avslutar programmet: **2**
Ge ett tal, -1 avslutar programmet: **4**
Ge ett tal, -1 avslutar programmet: **5**
Ge ett tal, -1 avslutar programmet: **3**
Ge ett tal, -1 avslutar programmet: **-1**
Summan är 14

</sample-output>

Båda programmen är alltså identiska till sin funktionalitet, men den första metoden är ofta enklare eftersom villkoret `tal == 1` endast finns på ett ställe och variabeln `tal` inte behöver initieras utanför loopen.

`break`-instruktionen kan kombineras med ett lämpligt villkor. Till exempel körs följande loop så länge som summan av talen är högst 100, men avslutas också då man matar in -1.

Så här kan det se ut när programmet körs:

```python
summa = 0

while summa <= 100:
    tal = int(input("Ge ett tal, -1 avslutar programmet: "))
    if tal == -1:
        break
    summa += tal

print (f"Summan är {summa}")
```

Exempel:

<sample-output>

Ge ett tal, -1 avslutar programmet: **15**
Ge ett tal, -1 avslutar programmet: **8**
Ge ett tal, -1 avslutar programmet: **21**
Ge ett tal, -1 avslutar programmet: **-1**
Summan är 44

</sample-output>

<sample-output>

Ge ett tal, -1 avslutar programmet: **15**
Ge ett tal, -1 avslutar programmet: **8**
Ge ett tal, -1 avslutar programmet: **21**
Ge ett tal, -1 avslutar programmet: **45**
Ge ett tal, -1 avslutar programmet: **17**
Summan är 106

</sample-output>

I det första exemplet avslutas loopen eftersom användaren matar in -1. I det andra exemplet avslutas loopen eftersom summan blir större än 100.

Som alltid inom programmering finns det flera sätt att uppnå samma resultat. Följande program fungerar på samma sätt som de två exemplen ovan:

```python
summa = 0

while True:
    tal = int(input("Ge ett tal, -1 avslutar programmet: "))
    if tal == -1:
        break
    summa += tal
    if summa > 100:
        break

print (f"Summan är {summa}")
```

## `continue`-instruktionen

Ett annat sätt att påverka hur en loop körs är `continue`-instruktionen. Det får loopen att hoppa till början av kodblocket, det vill säga så att villkoret kollas innan följande iteration körs. Det är alltså ett sätt att avbryta en given runda/iteration av loopen, utan att avbryta hela loopen. 

<img src="3_3.png">

Till exempel adderar följande program de tal som användaren matar in, men bara då det givna talet är mindre än tio. Om talet är tio eller större, hoppar man till början av loopen utan att lägga till talet.

```python
summa = 0

while True:
    tal = int(input("Ge ett tal, -1 avslutar programmet: "))
    if tal == -1:
        break
    if tal >= 10:
        continue
    summa += tal

print (f"Summan är {summa}")
```

<sample-output>

Ge ett tal, -1 avslutar programmet: **4**
Ge ett tal, -1 avslutar programmet: **7**
Ge ett tal, -1 avslutar programmet: **99**
Ge ett tal, -1 avslutar programmet: **5**
Ge ett tal, -1 avslutar programmet: **-1**
Summan är 16

</sample-output>

## Nästlade loopar

Precis som med if-satser kan loopar placeras innanför andra loopar. Till exempel använder sig följande program av en loop för att fråga efter ett tal av användaren. Innanför denna loop finns en annan loop som räknar ner från det givna talet till ett:

```python
while True:
    tal = int(input("Ge ett tal: "))
    if tal == -1:
        break
    while tal > 0:
        print(tal)
        tal -= 1
```

<sample-output>

Ge ett tal: **4**
4
3
2
1
Ge ett tal: **3**
3
2
1
Ge ett tal: **6**
6
5
4
3
2
1
Ge ett tal: **-1**

</Sample-output>

I nästlade loopar är det bra att märka att `break` och `continue` endast påverkar den innersta loopen de finns i. Det föregående exemplet skulle kunna skrivas så här:

```python
while True:
    tal = int(input("Ge ett tal: "))
    if tal == -1:
        break
    while True:
        if tal <= 0:
            break
        print(tal)
        tal -= 1
```

Här avslutar den andra `break`-instruktionen endast den inre loopen som används för att skriva ut talen.

## Hjälpvariabler med loopar

Vi har redan använt oss av hjälpvariabler – som ökar eller minskar för varje iteration av en loop – flera gånger, så följande program borde till sin struktur se ganska bekant ut. Programmet skriver ut alla jämna tal från noll fram till det tal som användaren angett:

```python
grans = int(input("Ge ett tal: "))
i = 0
while i < grans:
    print(i)
    i += 2
```

<sample-output>

Ge ett tal: **8**
0
2
4
6

</sample-output>

Hjälpvariabeln `i` har tilldelats värdet 0 före loopen, som ökar på talet med två för varje iteration.

När man använder kapslade loopar kan det uppstå ett behov för en ny hjälpvariabel för den inre loopen. Följande program skriver ut en "sifferpyramid" baserat på det tal som användaren angett:

```python
tal = int(input("Ge ett tal: "))
while tal > 0:
    i = 0
    while i < tal:
        print(f"{i} ", end="")
        i += 1
    print()
    tal -= 1
```

<sample-output>

Ge ett tal: **5**
0 1 2 3 4
0 1 2 3
0 1 2
0 1
0

</sample-output>

I programmet använder den yttre loopen hjälpvariabeln `tal` som minskar med ett tills dess värde blir 0. Hjälpvariabeln `i` tilldelas värdet 0 före man fortsätter till den inre loopen – varje gång den yttre loopen upprepas.

Den inre loopen använder sig av hjälpvariabeln `i` som ökar med talet 1 för varje iteration av den inre loopen. Den inre loopen fortsätter tills `i` är lika med `tal`, och skriver ut varje värde hos `i` med mellanslag emellan. När loopen avslutas skapar `print`-instruktionen i den yttre loopen en ny rad.

I och med att värdet på `tal` minskar för varje iteration av den yttre loopen, kommer antalet iterationer hos den inre loopen att minska. Vid varje upprepning blir sifferraden kortare, vilket bildar "pyramiden".

Nästlade loopar kan vara svårtolkade vid första anblicken, men det är viktigt att förstå hur de fungerar. Du kan använda dig av Python Tutors [visualiseringsverktyg](https://pythontutor.com/visualize.html) för att bättre förstå hur ovanstående exempel fungerar. Kopiera koden till kodfönstret och följ med hur utskriften formas och hur hjälpvariablernas värden ändras medan programmet körs.

<in-browser-programming-exercise name="Multiplikationstabell" tmcname="osa03-15b_multiplikationstabell">

Skapa ett program som ber om ett positivt heltal av användaren. Programmet ska skriva ut multiplikationsoperationer ända upp till det talet, enligt följande exempel: 

<sample-output>

Ge ett tal: 2
1 x 1 = 1
1 x 2 = 2
2 x 1 = 2
2 x 2 = 4

</sample-output>

<sample-output>

Ge ett tal: 3
1 x 1 = 1
1 x 2 = 2
1 x 3 = 3
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
3 x 1 = 3
3 x 2 = 6
3 x 3 = 9

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Ordens första bokstäver" tmcname="osa03-16_forsta_bokstaverna">

Skapa ett program som ber användaren mata in en mening. Programmet skriver därefter ut den första bokstaven i varje ord på sin egen rad.

Exempel:

<sample-output>

Ge en mening: **Kira gillade klara glaskulor**
K
g
k
g

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Fakulteter" tmcname="osa03-17_fakulteter">

Skapa ett program som ber användaren mata in ett heltal. Om talet är negativt eller noll, avslutas programmet. I övriga fall skriver programmet ut talets fakultet.

Fakulteten beräknas genom att multiplicera talet med sig själv samt alla mindre positiva heltal. Fakulteten för 5 är t.ex. `1 * 2 * 3 * 4 * 5 = 120`.

Exempel:

<sample-output>

Ge ett tal: **3**
Talets 3 fakultet är 6
Ge ett tal: **4**
Talets 4 fakultet är 24
Ge ett tal: **-1**
Tack och hej!

</sample-output>

<sample-output>

Ge ett tal: **1**
Talets 1 fakultet är 1
Ge ett tal: **0**
Tack och hej!

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Sväng paren" tmcname="osa03-18_svang_paren">

Skapa ett program som skriver ut tal från 1 till det tal användaren matat in. Talen ska komma i turvis omvänd ordning som i följande exempel: 

<sample-output>

Ge ett tal: **5**
2
1
4
3
5

</sample-output>

<sample-output>

Ge ett tal: **6**
2
1
4
3
6
5

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Turvis" tmcname="osa03-19_turvis">

Skapa ett program som ber användaren mata in ett tal. Programmet ska skriva ut talen turvis enligt följande exempel:

<sample-output>

Ge ett tal: **5**
1
5
2
4
3

</sample-output>

<sample-output>

Ge ett tal: **6**
1
6
2
5
3
4

</sample-output>

</in-browser-programming-exercise>

<quiz id="345431e9-53dd-5f83-a3c1-ef53e7adf424"></quiz>
