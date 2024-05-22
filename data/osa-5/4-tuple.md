---
path: '/osa-5/4-tuple'
title: 'Tuple'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* känner du till datatypen tuple
* kan du skapa tupler av olika typer av värden
* vet du vad skillnaden mellan en lista och tuple är
* kan du nämna några vanliga användningsområden för tupler.

</text-box>

En tuple är en datastruktur som på flera sätt påminner listan. De största skillnaderna mellan dessa två är:

* tupler är inom parenteser `()` medan listor är inom hakparenteser `[]`
* tupler är oföränderliga, medan innehållet i en lista kan ändra.

Den följande kodsnutten skapar en tuple som innehåller koordinaterna för en punkt:

```python
piste = (10, 20)
```

Elementen lagrade i tupler kan kommas åt med index, på samma sätt som med listor:

```python
piste = (10, 20)
print("x-koordinaatti:", piste[0])
print("y-koordinaatti:", piste[1])
```

<sample-output>

x-koordinaatti: 10
y-koordinaatti: 20

</sample-output>

Värden som lagrats i en tuple kan inte ändras efter att en tuple har skapats. Det följande kommer inte att fungera:

```python
piste = (10, 20)
piste[0] = 15
```

<sample-output>

TypeError: 'tuple' object does not support item assignment

</sample-output>

<programming-exercise name='Muodosta tuple' tmcname='osa05-17c_muodosta_tuple'>

Tee funktio `tee_tuple(x: int, y: int, z: int)`, joka muodostaa ja palauttaa parametrinaan saamistaan kokonaisluvuista tuplen seuraavien sääntöjen mukaaan:

1. Tuplen ensimmäinen alkio on parametreista pienin
2. Tuplen toinen alkio on parametreista suurin
3. Tuplen kolmas alkio on parametrien summa

Esimerkki funktion kutsumisesta:

```python

if __name__ == "__main__":
    print(tee_tuple(5, 3, -1))

```

<sample-output>

(-1, 5, 7)

</sample-output>


</programming-exercise>

<programming-exercise name='Vanhin henkilöistä' tmcname='osa05-18_vanhin_henkiloista'>

Tee funktio `vanhin(henkilot: list)`, joka saa parametrikseen listan henkilöitä esittäviä tupleja. Funktio etsii ja palauttaa vanhimman henkilön nimen.

Henkilötuplessa on ensin henkilön nimi merkkijonona ja toisena alkiona henkilön _syntymävuosi_.

Esimerkiksi:

```python
h1 = ("Arto", 1977)
h2 = ("Einari", 1985)
h3 = ("Maija", 1953)
h4 = ("Essi", 1997)
hlista = [h1, h2, h3, h4]

print(vanhin(hlista))
```

<sample-output>

Maija

</sample-output>

</programming-exercise>

<programming-exercise name='Vanhemmat henkilöt' tmcname='osa05-19_vanhemmat_henkilot'>

Oletetaan, että meillä on edelleen käytössä edellisessä tehtävässä esitellyt henkilö-tuplet.

Kirjoita funktio `vanhemmat(henkilot: list, vuosi: int)`, joka palauttaa uuden listan, jolle on tallennettu kaikki _ennen_ annettua vuotta syntyneet henkilöiden nimet parametrina saadulta henkilöiden listalta.

Esimerkiksi:

```python
h1 = ("Arto", 1977)
h2 = ("Einari", 1985)
h3 = ("Maija", 1953)
h4 = ("Essi", 1997)
hlista = [h1, h2, h3, h4]

vanhemmat_henkilot = vanhemmat(hlista, 1979)
print(vanhemmat_henkilot)
```

<sample-output>

[ 'Arto', Maija' ]

</sample-output>

</programming-exercise>

## Vad behöver man tupler för?

Tupler är nyttiga i situationer där det finns en samling av värden som är på något sätt sammankopplade. Till exempel då man behandlar x- och y-koordinaterna hos en punkt, är tuplen ett naturligt val eftersom koordinater alltid består av två värden:

```python
piste = (10, 20)
```

Det är tekniskt möjligt att använda en lista för att lagra dessa:

```python
piste = [10, 20]
```

En lista är en samling av element i en viss ordning. Listans storlek kan också ändra. Eftersom vi lagrar koordinaterna för en punkt, vill vi lagra x- och y-koordinaterna specifikt – inte en godtycklig lista med dessa värden.

Eftersom tupler är oföränderliga – till skillnad från listor – kan de användas som nycklar i lexikon. Det följande kodexemplet skapar ett lexikon där koordinater används som nycklar:

```python
pisteet = {}
pisteet[(3, 5)] = "apina"
pisteet[(5, 0)] = "banaani"
pisteet[(1, 2)] = "cembalo"
print(pisteet[(3, 5)])
```

<sample-output>
apina
</sample-output>

Det är inte möjligt att skapa ett liknande lexikon med hjälp av listor:

```python
pisteet = {}
pisteet[[3, 5]] = "apina"
pisteet[[5, 0]] = "banaani"
pisteet[[1, 2]] = "cembalo"
print(pisteet[[3, 5]])
```

<sample-output>

TypeError: unhashable type: 'list'

</sample-output>

## Tupler utan parenteser

Parenteser är inte obligatoriska då man skapar tupler. Följande variabeltilldelningar ger likadana resultat:

```python
luvut = (1, 2, 3)
```

```python
luvut = 1, 2, 3
```

Det innebär att vi enkelt kan returnera flera värden med hjälp av tupler. Ta en titt på följande exempel:

```python
def minmax(lista):
  return min(lista), max(lista)

lista = [33, 5, 21, 7, 88, 312, 5]

pienin, suurin = minmax(lista)
print(f"Pienin luku on {pienin} ja suurin on {suurin}")
```

<sample-output>

Pienin luku on 5 ja suurin on 312

</sample-output>

Funktionen returnerar två värden i en tuple. Return-värdet kan tilldelas till två variabler samtidigt:

```python
pienin, suurin = minmax(lista)
```

Att använda parenteser kan göra notationen tydligare. Till vänster av tilldelningssatsen har vi också en tuple som består av två variabelnamn. Värdena som finns i tuplen som funktionen returnerar tilldelas till dessa två variabler.

```python
(pienin, suurin) = minmax(lista)
```

Du kanske minns metoden `items` från den förra delen. Vi använde den för att komma åt nycklarna och värdena som lagrats i ett lexikon:

```python
sanakirja = {}

sanakirja["apina"] = "monkey"
sanakirja["banaani"] = "banana"
sanakirja["cembalo"] = "harpsichord"

for avain, arvo in sanakirja.items():
    print("avain:", avain)
    print("arvo:", arvo)
```

Tupler finns i bakgrunden här också. Metoden `mitt_lexikon.items()` returnerar varje nyckel-värdepar som en tuple, där det första elementet innehåller nyckeln och det andra värdet.

Ett annat användningsområde för tupler är att byta värden sinsemellan två variabler:

```python
luku1, luku2 = luku2, luku1
```

Tilldelningssatsen ovan svänger på värdena lagrade i variablerna `siffra1` och `siffra2`. Resultatet är detsamma som vi skulle uppnå med hjälp av en hjälpvariabel:

```python
apu = luku1
luku1 = luku2
luku2 = apu
```

<programming-exercise name='Opiskelijarekisteri' tmcname='osa05-20_opiskelijarekisteri'>

Tässä tehtäväsarjassa toteutetaan yksinkertainen opiskelijarekisteri. Ennen ohjelmoinnin aloittamista kannattanee hetki miettiä, minkälaisen tietorakenteen tarvitset ohjelman tallentamien tietojen organisointiin.

#### opiskelijoiden lisäys

Toteuta ensin funktio `lisaa_opiskelija` uuden opiskelijan lisäämiseen sekä ensimmäinen versio funktiosta `tulosta`, joka tulostaa yhden opiskelijan tiedot.

Funktioita käytetään seuraavasti:

```python
opiskelijat = {}
lisaa_opiskelija(opiskelijat, "Pekka")
lisaa_opiskelija(opiskelijat, "Liisa")
tulosta(opiskelijat, "Pekka")
tulosta(opiskelijat, "Liisa")
tulosta(opiskelijat, "Jukka")
```

Ohjelma tulostaa tässä vaiheessa

<sample-output>

<pre>
Pekka:
 ei suorituksia
Liisa:
 ei suorituksia
ei löytynyt ketään nimellä Jukka
</pre>

</sample-output>

#### suoritusten lisäys

Tee funktio `lisaa_suoritus`, jonka avulla opiskelijalle voidaan lisätä kurssin suoritus. Suoritus on tuple, joka koostuu kurssin nimestä ja arvosanasta:

```python
opiskelijat = {}
lisaa_opiskelija(opiskelijat, "Pekka")
lisaa_suoritus(opiskelijat, "Pekka", ("Ohpe", 3))
lisaa_suoritus(opiskelijat, "Pekka", ("Tira", 2))
tulosta(opiskelijat, "Pekka")
```

Opiskelijan tietojen tulostus muuttuu, kun suorituksia on lisätty:

<sample-output>

<pre>
Pekka:
 suorituksia 2 kurssilta:
  Ohpe 3
  Tira 2
 keskiarvo 2.5
</pre>

</sample-output>

#### arvosanojen korotus

Suorituksen lisäämisen pitää toimia siten, että se jättää arvosanan 0 suoritukset huomiotta eikä alenna kurssilla ennestään olevaa arvosanaa:

```python
opiskelijat = {}
lisaa_opiskelija(opiskelijat, "Pekka")
lisaa_suoritus(opiskelijat, "Pekka", ("Ohpe", 3))
lisaa_suoritus(opiskelijat, "Pekka", ("Tira", 2))
lisaa_suoritus(opiskelijat, "Pekka", ("Lama", 0))
lisaa_suoritus(opiskelijat, "Pekka", ("Ohpe", 2))
tulosta(opiskelijat, "Pekka")
```

<sample-output>

<pre>
Pekka:
 suorituksia 2 kurssilta:
  Ohpe 3
  Tira 2
 keskiarvo 2.5
</pre>

</sample-output>

#### kooste opiskelijoista

Tee funktio `kooste`, joka tulostaa koosteen opiskelijoiden suorituksista. Esimerkki:

```python
opiskelijat = {}
lisaa_opiskelija(opiskelijat, "Pekka")
lisaa_opiskelija(opiskelijat, "Liisa")
lisaa_suoritus(opiskelijat, "Pekka", ("Lama", 1))
lisaa_suoritus(opiskelijat, "Pekka", ("Ohpe", 1))
lisaa_suoritus(opiskelijat, "Pekka", ("Tira", 1))
lisaa_suoritus(opiskelijat, "Liisa", ("Ohpe", 5))
lisaa_suoritus(opiskelijat, "Liisa", ("Jtkt", 4))
kooste(opiskelijat)
```

tulostus näyttää seuraavalta

<sample-output>

<pre>
opiskelijoita 2
eniten suorituksia 3 Pekka
paras keskiarvo 4.5 Liisa
</pre>

</sample-output>

</programming-exercise>

<programming-exercise name="Kirjainruudukko" tmcname="osa05-21_kirjainruudukko">

Tämän osan huipentaa suhteellisen haastava ongelmanratkaisua vaativa tehtävä, jonka voi ratkaista monella eri tavalla. Vaikka tehtävä on tupleja käsittelevässä luvussa, tupleja tässä tuskin kannattaa käyttää.

Tee ohjelma, joka tulostaa kirjainruudukon oheisten esimerkkien mukaisesti. Voit olettaa, että kerroksia on enintään 26.

<sample-output>

Kerrokset: **3**
<pre>
CCCCC
CBBBC
CBABC
CBBBC
CCCCC
</pre>

</sample-output>

<sample-output>

Kerrokset: **4**
<pre>
DDDDDDD
DCCCCCD
DCBBBCD
DCBABCD
DCBBBCD
DCCCCCD
DDDDDDD
</pre>

</sample-output>

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!

</programming-exercise>

<quiz id="8342aecc-48cd-5e26-a8ad-6272ba1df02a"></quiz>

Vänligen svara på en kort enkät gällande materialet för den här veckan.

<quiz id="7c3732cd-b37b-5524-9747-0fcf49c917bb"></quiz>
