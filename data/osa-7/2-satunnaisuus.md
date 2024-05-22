---
path: '/osa-7/2-satunnaisuus'
title: 'Slumpmässighet'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* känner du till några av funktionerna i `random`-modulen
* kan du använda dig av slumpmässiga tal i dina program.

</text-box>

I den här delen ser vi på modulen `random` i Pythons standardbibliotek. Den här modulen innehåller verktyg för att skapa slumpmässiga tal och för annan funktionalitet med ett slumpmässigt element.

Delarna i den här modulen innehåller flera länkar till standardbibliotekets dokumentation. Vi rekommenderar att du följer länkarna så att du kan bekanta dig med hur dokumentationen ser ut.

## Skapa ett slumpmässigt tal

Funktionen `randint(a, b)` returnerar ett slumpmässigt heltal mellan `a` och `b` (inklusive start- och slutpunkten). Till exempel det här programmet fungerar som en normal tärning:

```python
from random import randint

print("Noppa antaa:", randint(1, 6))
```

Så här kan utskriften se ut:

<sample-output>

Noppa antaa: 4

</sample-output>

Det här programmet kastar en tärning tio gånger:

```python
from random import randint

for i in range(10):
    print("Noppa antaa:", randint(1, 6))
```

Utskriften skulle kunna se ut så här:

<sample-output>

Noppa antaa: 5
Noppa antaa: 4
Noppa antaa: 3
Noppa antaa: 2
Noppa antaa: 3
Noppa antaa: 4
Noppa antaa: 6
Noppa antaa: 4
Noppa antaa: 4
Noppa antaa: 3

</sample-output>

Obs! Det är värt att notera att funktionen `randint` fungerar lite olikt än till exempel extrahering (slicing) eller `range`-funktionen. Funktionsanropet `randint(1, 6)` resulterar i ett nummer mellan 1 och 6, medan anropet `range(1, 6)` resulterar i ett intervall från 1 till 5.

## Flera slumpmässighetsfunktioner

Funktionen `shuffle` blandar elementen i den datastruktur som ges som argument. Till exempel följande program blandar en lista med ord:

```python
from random import shuffle

sanat = ["apina", "banaani", "cembalo"]
shuffle(sanat)
print(sanat)
```

<sample-output>

['banaani', 'apina', 'cembalo']

</sample-output>

Funktionen `choice` returnerar ett slumpmässigt valt element från en datastruktur:

```python
from random import choice

sanat = ["apina", "banaani", "cembalo"]
print(choice(sanat))
```

<sample-output>

'cembalo'

</sample-output>

## Lottorad

Ett vanligt sätt att undersöka slumpmässighet är att se på lottorader. Låt oss lotta ut en vinnande rad. I Finland består lottoraden av sju siffror mellan 1 och 40.

Så här kunde det se ut när vi försöker lotta ut en rad:

```python
from random import randint

for i in range(7):
    print(randint(1, 40))
```

Det här skulle inte fungera i det långa loppet eftersom ett och samma nummer kan dyka upp flera gånger på samma lottorad. Vi måste se till att alla nummer är unika.

Ett sätt är att lagra de lottade siffrorna i en lista. Då lägger vi bara till en ny siffra om siffran inte redan finns i listan. Vi använder oss av en loop som fortsätter tills listans längd är sju:

```python
from random import randint

rivi = []
while len(rivi) < 7:
    uusi = randint(1, 40)
    if uusi not in rivi:
        rivi.append(uusi)

print(rivi)
```

Vi kan också spara lite utrymme genom att använda `shuffle`-funktionen:

```python
from random import shuffle

kaikki = list(range(1, 41))
shuffle(kaikki)
rivi = kaikki[0:7]
print(rivi)
```

Idén här är att vi skapar en lista med siffrorna 1 till 40, lite som att vi skulle ha 40 bollar i en lotterimaskin. Listan blandas sedan, varefter de första sju siffrorna utgör veckans vinnande rad. Nu behöver vi ingen loop.

Modulen `random` innehåller faktiskt ett ännu enklare sätt att skapa vår lottorad: funktionen `sample`. Den returnerar ett slumpmässigt val av en specifik storlek från en given datastruktur:

```python
from random import sample

kaikki_luvut = list(range(1, 41))
rivi = sample(kaikki_luvut, 7)
print(rivi)
```

<programming-exercise name='Lottonumerot' tmcname='osa07-04_lottonumerot'>

Tee funktio `lottonumerot(maara: int, alaraja: int, ylaraja: int)`, joka arpoo annetun määrän satunnaislukuja väliltä `alaraja`...`ylaraja`, tallentaa ne listaan ja palauttaa listan. Lukujen tulee olla palautetussa listassa suuruusjärjestyksessä.

Koska kyseessä ovat lottonumerot, sama numero ei saa esiintyä listassa kahta kertaa.

Esimerkki:

```python
for numero in lottonumerot(7, 1, 40):
    print(numero)
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

## Varifrån kommer dessa slumpmässiga siffror från?

Funktionaliteten i `random`-modulen är baserad på en algoritm som skapar slumpmässiga siffror på basis av ett specifikt startvärde och några matematiska operationer. Startvärdet kallas ofta seed value.

Vi kan själva ge ett sådant värde med `seed`-funktionen:

```python
from random import randint, seed

seed(1337)
# tästä tulee aina sama satunnaisluku
print(randint(1, 100))
```

Om vi har funktioner som baserar sig på slumpmässighet och har valt ett seed-värde, kommer funktionen att ge samma resultat varje gång den körs. Resultatet kan skilja sig mellan olika Python-versioner, men i grunden kommer slumpmässigheten att försvinna då vi definierar seed-värdet. Funktionaliteten kan dock vara nyttig då vi exempelvis testar på vårt program.

<text-box variant="info" name="Sann slumpmässighet">

För att vara korrekt, är de siffor som `random`-modulen ger inte i verkligheten slumpmässiga. Istället är de skenbart slumpmässiga (pseudorandom). Datorers funktionalitet är förutsebar och i en ideal situation kan man exakt bestämma hur de fungerar. Därmed är det mycket svårt att skapa sant slumpmässiga tal med en dator. I flera situationer räcket skenbart slumpmässiga tal. När sant slumpmässiga tal behövs skapas seed-värdet på basis av någon yttre källa som radioaktiv bakgrundsstrålning, ljudnivå eller lavalampor.

För ytterligare information om slumpmässighet, se random.org.

</text-box>

<programming-exercise name='Salasanan arpoja, osa 1' tmcname='osa07-05_salasanan_arpoja_1'>

Tee funktio, jonka avulla on mahdollista luoda halutun pituisia satunnaisista pienistä kirjaimista (väliltä a-z) muodostettuja salasanoja.

Esimerkki:

```python
for i in range(10):
    print(luo_salasana(8))
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

<programming-exercise name='Salasanan arpoja, osa 2' tmcname='osa07-06_salasanan_arpoja_2'>

Tee paranneltu versio edellisen tehtävän funktiosta. Funktio saa nyt kolme parametria:

* jos toinen parametri on `True`, salasanassa on myös (yksi tai useampi) numero
* jos kolmas parametri on `True`, salasanassa on myös (yksi tai useampi) erikoismerkki joukosta `!?=+-()#`

Salasanassa täytyy olla parametreista riippumatta aina vähintään yksi kirjain. Voit olettaa, että funktiota kutsutaan aina parametreilla, joilla on mahdollista tuottaa halutunlaisia salasanoja.

Esimerkki:

```python
for i in range(10):
    print(luo_hyva_salasana(8, True, True))
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

<programming-exercise name='Noppasimulaatio' tmcname='osa07-07_noppasimulaatio'>

Tehdään tässä tehtävässä muutamia funktioita, joita on mahdollista käyttää nopanheittoon liittyvissä peleissä.

Normaalin nopan sijaan tehtävässä käytetään ns. epätransitiivisia noppia, joista on lisää tietoa esim. [tässä artikkelissa](https://singingbanana.com/dice/article.htm) tai [tässä videossa](https://www.youtube.com/watch?v=LrIp6CKUlH8).

Käytössä on kolme noppaa:

- Nopassa A on numerot 3, 3, 3, 3, 3, 6
- Nopassa B on numerot 2, 2, 2, 5, 5, 5
- Nopassa C on numerot 1, 4, 4, 4, 4, 4

</pre>

Tee funktio `heita(noppa: str)`, joka heittää parametrinsa kertomaa noppaa. Esimerkki:

```python
for i in range(20):
    print(heita("A"), " ", end="")
print()
for i in range(20):
    print(heita("B"), " ", end="")
print()
for i in range(20):
    print(heita("C"), " ", end="")
```

<sample-output>

3  3  3  3  3  3  3  3  3  3  3  3  3  3  3  3  6  3  6  3
2  2  5  2  2  5  5  2  2  5  2  5  5  5  2  5  2  2  2  2
4  4  4  4  4  1  1  4  4  4  1  4  4  4  4  4  4  4  4  4

</sample-output>

Tee vielä funktio `pelaa(noppa1: str, noppa2: str, kertaa: int)` joka heittää kokonaisluvun kertoman määrän parametreina olevia noppia. Funktio palauttaa tuplen, joka kertoo nopan 1 voittojen lukumäärän, nopan 2 voittojen lukumäärän ja tasapelien lukumäärän.

```python
tulos = pelaa("A", "C", 1000)
print(tulos)
tulos = pelaa("B", "B", 1000)
print(tulos)
```

<sample-output>

(292, 708, 0)
(249, 273, 478)

</sample-output>

</programming-exercise>

<programming-exercise name='Satunnaiset sanat' tmcname='osa07-08_satunnaiset_sanat'>

Tehtäväpohjassa on annettu tiedosto `sanat.txt`, joka sisältää englannin kielen sanoja, yksi sana joka rivillä.

Kirjoita funktio `sanat(n: int, alku: str)`, joka palauttaa listassa `n` kappaletta satunnaisia sanoja tiedostosta. Kaikkien palautettujen sanojen tulee alkaa annetulla merkkijonolla.

Jos funktiota esim. kutsuttaisiin parametreilla `sanat(3, "ca")`, se voisi palauttaa listassa esim. sanat "cat", "car" ja "carbon". Sama sana ei saa esiintyä listassa kahdesti.

Jos annetulla merkkijonolla alkavia sanoja ei löydy tarpeeksi annetun kokoisen ryhmän muodostamiseen, funktio tuottaa poikkeuksen `ValueError`.

Esimerkki:

```python
lista = sanat(3, "ca")
for sana in lista:
    print(sana)
```

<sample-output>

cat
car
carbon

</sample-output>

</programming-exercise>

<quiz id="1a7d3d96-42a9-55a7-b3b5-fba27e14751e"></quiz>
