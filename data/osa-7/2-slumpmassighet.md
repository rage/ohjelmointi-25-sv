---
path: '/osa-7/2-slumpmassighet'
title: 'Slump'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* känner du till några av funktionerna i `random`-modulen
* kan du använda dig av slumptal i dina program.

</text-box>

I den här delen ser vi på [modulen `random`](https://docs.python.org/3/library/random.html) som finns i Pythons standardbibliotek. Den här modulen innehåller funktioner som gör det möjligt att arbeta med slump i program, till exempel för att skapa slumptal, blanda ordningen på elementen i en datastruktur eller plocka ut slumpmässigt valda element. 

Delarna i den här modulen innehåller flera länkar till [standardbibliotekets dokumentation](https://docs.python.org/3/library/). Kolla gärna upp länkarna så att du kan bekanta dig med hur dokumentationen ser ut.

## Skapa slumptal

Funktionen [`randint(a, b)`](https://docs.python.org/3/library/random.html#random.randint) returnerar ett slumptal mellan `a` och `b` (inklusive start- och slutpunkten). Det här programmet fungerar till exempel som en normal tärning:

```python
from random import randint

print("Tärningen visar:", randint(1, 6))
```

Så här kan utskriften se ut:

<sample-output>

Tärningen visar: 4

</sample-output>

Det här programmet kastar en tärning tio gånger:

```python
from random import randint

for i in range(10):
    print("Tärningen visar:", randint(1, 6))
```

Utskriften skulle kunna se ut så här:

<sample-output>

Tärningen visar: 5
Tärningen visar: 4
Tärningen visar: 3
Tärningen visar: 2
Tärningen visar: 3
Tärningen visar: 4
Tärningen visar: 6
Tärningen visar: 4
Tärningen visar: 4
Tärningen visar: 3

</sample-output>

Obs! Det är värt att notera att funktionen `randint` fungerar lite olikt än till exempel extrahering (slicing) eller `range`-funktionen. Funktionsanropet `randint(1, 6)` resulterar i ett tal mellan 1 och 6, medan anropet `range(1, 6)` resulterar i ett intervall som innehåller värdena 1 till 5.

## Fler funktioner relaterade till slumpmässighet

Funktionen [`shuffle`](https://docs.python.org/3/library/random.html#random.shuffle) blandar elementen i den datastruktur som ges som argument. Till exempel blandar följande program ordningen i en lista med ord:

```python
from random import shuffle

ord = ["apa", "banan", "cembalo"]
shuffle(ord)
print(ord)
```

<sample-output>

['banan', 'apa', 'cembalo']

</sample-output>

Funktionen `choice` returnerar ett slumpmässigt valt element ur en datastruktur:

```python
from random import choice

ord = ["apa", "banan", "cembalo"]
print(choice(ord))
```

<sample-output>

'cembalo'

</sample-output>

## Lottorad

Ett vanligt sätt att undersöka slumpmässighet är att se på lottorader. Låt oss lotta ut en vinnande rad. I Finland består lottoraden av sju siffror mellan 1 och 40.

Så här skulle det kunna se ut om vi försöker lotta ut en rad:

```python
from random import randint

for i in range(7):
    print(randint(1, 40))
```

Det här skulle inte fungera i det långa loppet eftersom ett och samma nummer kan dyka upp flera gånger på samma lottorad. Vi måste se till att alla nummer som dras är unika.

Ett sätt är att lagra de dragna siffrorna i en lista. Då lägger vi bara till ett draget nummer om det inte redan finns i listan. Vi använder oss av en loop som fortsätter tills listans längd är sju, dvs. vi har dragit sju unika lottonummer:

```python
from random import randint

rad = []
while len(rad) < 7:
    ny = randint(1, 40)
    if ny not in rad:
        rad.append(ny)

print(rad)
```

Vi kan också spara lite utrymme genom att använda `shuffle`-funktionen:

```python
from random import shuffle

alla = list(range(1, 41))
shuffle(alla)
rad = alla[0:7]
print(rad)
```

Hur fungerar det här? Idén är att vi skapar en lista med talen 1 till 40, på samma sätt som vi har 40 bollar i en lottomaskin. Efter att listan har blandats kan de första sju siffrorna utgöra veckans vinnande rad, på samma sätt som de första sju bollarna som plockas ur maskinen. Nu behövs alltså ingen loop, utan vi kan direkt plocka ut de sju första talen ur den blandade listan.

Modulen `random` innehåller faktiskt ett ännu enklare sätt att skapa vår lottorad: funktionen [`sample`](https://docs.python.org/3/library/random.html#random.sample). Den returnerar ett givet antal slumpmässigt valda element ur en given datastruktur, i det här fallet sju tal ur en lista med talen 1-40:

```python
from random import sample

alla = list(range(1, 41))
rad = sample(alla, 7)
print(rad)
```

<programming-exercise name='Lottorader' tmcname='osa07-04_lottorader'>

Skapa funktionen `lottorad(siffror: int, nedre: int, ovre: int)` som lottar ut det givna antalet siffror i intervallet `nedre-ovre` och returnerar dessa i en sorterad lista (med start från det minsta talet).

Samma siffra får inte förekomma flera gånger.

Exempel:

```python
for siffra in lottorad(7, 1, 40):
    print(siffra)
```

<sample-output>

4
7
11
16
22
29
38

</sample-output>

</programming-exercise>

## Varifrån kommer slumptalen?

Datorer skapar slumptal med hjälp av en matematisk formel. För att resultatet inte ska bli samma varje gång används ett så kallat frö (engelska: seed) som startvärde. Frövärdet tas ofta från systemtiden, dvs. vad datorns interna klocka visar när slumpgeneratorn körs.

Funktionaliteten i [`random`-modulen](https://docs.python.org/3/library/random.html) är baserad på denna typ av algoritm. Vi kan också själva ange startvärdet med [`seed`](https://docs.python.org/3/library/random.html#random.seed)-funktionen:

```python
from random import randint, seed

seed(1337)
# följande instruktion genererar nu alltid samma tal
print(randint(1, 100))
```

Då vi själva anger `seed`-värdet kommer funktionen att ge samma resultat varje gång den körs. Resultatet kan skilja sig mellan olika Python-versioner, men i grunden kommer slumpmässigheten att försvinna då vi definierar seed-värdet. Funktionaliteten kan dock vara nyttig då vi exempelvis testar program.

<text-box variant="info" name="Sann slumpmässighet">

Egentligen är de siffor som `random`-modulen ger inte slumpmässiga "på riktigt". Matematiskt uträknade slumptal kallas i stället pseudoslumptal. Datorers funktionalitet är förutsebar och i en ideal situation kan man exakt bestämma hur de fungerar. Därför är det mycket svårt att skapa äkta slumptal med en dator. I de flesta situationer räcker det dock bra med pseudoslumptal. När äkta slumptal behövs skapas seed-värdet på basis av någon yttre källa som radioaktiv bakgrundsstrålning, ljudnivå eller lavalampor.

För ytterligare information om slumpmässighet, se [random.org](https://www.random.org/randomness/).

</text-box>

<programming-exercise name='Lösenordsgenerator, del 1' tmcname='osa07-05_losenord_1'>

Skapa en funktion som genererar slumpmässiga lösenord, av vald längd, bestående av bokstäverna a-z.

Exempel:

```python
for i in range(10):
    print(skapa_losenord(8))
```

<sample-output>

lttehepy
olsxttjl
cbjncrzo
dwxqjdgu
gpfdcecs
jabyvgar
xnbbonbl
ktmsjyww
ejhprmel
rjkoacib

</sample-output>

</programming-exercise>

<programming-exercise name='Lösenordsgenerator, del 2' tmcname='osa07-06_losenord_2'>

Förbättra förra uppgiftens funktion. Nu tar den emot två ytterligare argument:

2. om värdet på det andra argumentet är `True` ska lösenordet innehålla minst en siffra
2. om värdet på det tredje argumentet är `True` ska lösenordet innehålla minst ett av tecknen `!?=+-()#`

Lösenordet ska alltid innehålla minst en bokstav. Du kan anta att funktionen anropas med argument som gör det möjligt att skapa det önskade lösenordet. 

Exempel:

```python
for i in range(10):
    print(skapa_bra_losenord(8, True, True))
```

<sample-output>

2?0n+u31
u=m4nl94
n#=i6r#(
da9?zvm?
7h)!)g?!
a=59x2n5
(jr6n3b5
9n(4i+2!
32+qba#=
n?b0a7ey

</sample-output>

</programming-exercise>

<programming-exercise name='Tärningssimulation' tmcname='osa07-07_tarningar'>

Vi skapar nu några funktioner som vi kan använda i spel som kräver en tärning.

Istället för en normal tärning använder vi icke-transitiva tärningar. Se den här [artikeln](https://singingbanana.com/dice/article.htm) och [videon](https://youtu.be/LrIp6CKUlH8) vid behov.

Vi har tre tärningar:

* tärning A med siffrorna 3, 3, 3, 3, 3, 6
* tärning B med siffrorna 2, 2, 2, 5, 5, 5
* tärning C med siffrorna 1, 4, 4, 4, 4, 4

</pre>

Skapa funktionen `kasta(tarning: str)` som kastar den valda tärningen.

Exempel:

```python
for i in range(20):
    print(kasta("A"), " ", end="")
print()
for i in range(20):
    print(kasta("B"), " ", end="")
print()
for i in range(20):
    print(kasta("C"), " ", end="")
```

<sample-output>

3  3  3  3  3  3  3  3  3  3  3  3  3  3  3  3  6  3  6  3
2  2  5  2  2  5  5  2  2  5  2  5  5  5  2  5  2  2  2  2
4  4  4  4  4  1  1  4  4  4  1  4  4  4  4  4  4  4  4  4

</sample-output>

Skapa ännu funktionen `spela(tarning1: str, tarning2: str, ganger: int)` som kastar de valda tärningarna det angivna antalet gånger. Funktionen ska returnera en tupel som berättar antalet vinster med tärning ett respektive två samt antalet oavgjorda rundor.

```python
resultat = spela("A", "C", 1000)
print(resultat)
resultat = spela("B", "B", 1000)
print(resultat)
```

<sample-output>

(292, 708, 0)
(249, 273, 478)

</sample-output>

</programming-exercise>

<programming-exercise name='Slumpmässiga ord' tmcname='osa07-08_slumpmassiga_ord'>

I den här uppgiften har du filen `ord.txt` till ditt förfogande. Filen innehåller engelska ord, ett ord på varsin rad.

Skapa funktionen `ord(n: int, borjar: str)` som returnerar `n` slumpmässigt valda ord som börjar med den valda strängen. Orden ska returneras i en lista.

Om funktionen anropas med argumenten `ord(3, "ca")` kan t.ex. orden cat, car och carbon returneras i listan. Samma ord får inte förekomma flera gånger.

Om tillräckligt många ord inte hittas ska undantaget `ValueError` åstadkommas.

Exempel:

```python
lista = ord(3, "ca")
for ord in lista:
    print(ord)
```

<sample-output>

cat
car
carbon

</sample-output>

</programming-exercise>

<quiz id="8b15ae92-4b54-5fb8-a03b-2aadc4bb789d"></quiz>
