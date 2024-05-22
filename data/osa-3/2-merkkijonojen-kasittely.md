---
path: '/osa-3/2-merkkijonojen-kasittely'
title: 'Behandla strängar'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* kan du använda operatorerna `+` och `*` med strängar
* vet du hur man tar reda på längden hos en sträng
* vet du vad strängindexering betyder
* kan du hitta en delsträng i en sträng.

</text-box>

## Strängoperationer

Strängar kan kombineras med `+`-operatorn:

```python
alku = "esi"
loppu = "merkki"
sana = alku+loppu
print(sana)
```

<sample-output>

esimerkki

</sample-output>

Operatorn `*` kan också användas med strängar då den andra operanden är ett heltal. Strängoperanden kommer då att upprepas det antal gånger som specificeras av heltalet. Till exempel följande skulle fungera:

```python
sana = "apina"
print(sana*3)
```

<sample-output>

apinaapinaapina

</sample-output>

Med hjälp av att kombinera strängoperationer med en loop kan vi skriva ett program som ritar en pyramid:

```python
n = 10 # pyramidin kerrosten määrä
rivi = "*"

while n > 0:
    print(" " * n + rivi)
    rivi += "**"
    n -= 1
```

Så här ser utskriften ut:

```x
          *
         ***
        *****
       *******
      *********
     ***********
    *************
   ***************
  *****************
 *******************
```

Kommandot `print` inom loopen skriver ut en rad som börjar med `n` mellanslag följt av värdet som är lagrat i variabeln `rad`. Sedan läggs två stjärnor till i slutet av variabeln `rad` och variabeln `n`:s värde subtraheras med ett.

<in-browser-programming-exercise name="Monta jonoa" tmcname="osa03-05a_monistetut_jonot">

Kirjoita ohjelma, joka kysyy käyttäjältä merkkijonon ja määrän ja tulostaa sitten annettua merkkijonoa annetun määrän. Tulostuksen tulee tapahtua yhdelle riville yhteen pötköön.

Esimerkkisuoritus:

<sample-output>

Anna merkkijono: **heippa**
Anna määrä: **4**
heippaheippaheippaheippa

</sample-output>

</in-browser-programming-exercise>

## Längden på en sträng och dess index

Funktionen `len` returnerar antalet tecken i en sträng som ett heltal. Till exempel `len("hej")` returnerar 3 eftersom det finns tre tecken i strängen `hej`.

Följande program ber användaren att ge en sträng och skriver sedan ut ned med "understrykning". Programmet skriver alltså ut en andra rad som innehåller så många streck (`-`) som det finns tecken i den givna strängen:

```python
mjono = input("Anna merkkijono: ")
print(mjono)
print("-"*len(mjono))
```

<sample-output>

Anna merkkijono: **Moi kaikki!**

<pre>
Moi kaikki!
-----------
</pre>

</sample-output>

Strängens längd innehåller alla tecken i strängen – också mellanslag. Till exempel längden på strängen `hej igen` är 8.

<in-browser-programming-exercise name="Pidempi jono" tmcname="osa03-05b_pidempi_jono">

Kirjoita ohjelma, joka kysyy käyttäjältä kaksi merkkijonoa ja tulostaa jonoista pidemmän (ts. sen, jossa on enemmän merkkejä). Jos jonot ovat yhtä pitkiä tulostetaan viesti "Jonot ovat yhtä pitkät"

Esimerkkisuorituksia:

<sample-output>

Anna jono 1: **moi**
Anna jono 2: **heippa**
heippa on pidempi

</sample-output>

<sample-output>

Anna jono 1: **moikkelis koikkelis**
Anna jono 2: **heipparallaa**
moikkelis koikkelis on pidempi

</sample-output>

<sample-output>

Anna jono 1: **moi**
Anna jono 2: **hei**
Jonot ovat yhtä pitkät

</sample-output>

</in-browser-programming-exercise>

Eftersom strängar i grunden är sekvenser av tecken kan också vilken som helst specifik bokstav i en sträng hämtas. Operatorn `[]` hittar tecknet vid ett specifikt index som ges mellan parenteserna.

Indexet syftar till ett ställe i strängen och börjar från talet noll. Det första tecknet i en sträng har indexet 0 medan nästa tecken har indexet 1 och så vidare.

<img src="3_2_1.png">

Det här programmet…

```python

mjono = input("Anna merkkijono: ")
print(mjono[0])
print(mjono[1])
print(mjono[3])

```

…skulle skriva ut följande:

<sample-output>

Anna merkkijono: **apina**
a
p
n

</sample-output>

Eftersom det första tecknet i en sträng har indexet noll, har det sista tecknet indexet längd (`len`) - 1. Följande program skriver ut det första och sista tecknet i en sträng:

```python
mjono = input("Anna merkkijono: ")
print("Ensimmäinen: " + mjono[0])
print("Viimeinen: " + mjono[len(mjono) - 1])
```

<sample-output>

Anna merkkijono: **testi**
Ensimmäinen: t
Viimeinen: i

</sample-output>

Det här programmet går igenom varje tecken i en sträng – från det första till det sista:

```python
mjono = input("Anna merkkijono: ")
kohta = 0
while kohta < len(mjono):
    print(mjono[kohta])
    kohta += 1
```

<sample-output>

Anna merkkijono: **testi**
t
e
s
t
i

</sample-output>

Man kan också använda negativa index för att komma åt tecknen i en sträng från börjande från det sista tecknet.

Det sista tecknet i en sträng har alltså indexet -1, det näst sista indexet -2 och så vidare. Du kan tänka att `str[-1]` är en genväg för `str[len(str) – 1]`.

<img src="3_2_2.png">

Ovanstående exempel kan förenklas med negativ indexering.

```python
mjono = input("Anna merkkijono: ")
print("Ensimmäinen: " + mjono[0])
print("Viimeinen: " + mjono[-1])
```

<sample-output>

Anna merkkijono: **testi**
Ensimmäinen: t
Viimeinen: i

</sample-output>

## IndexError: string index out of range

Om du har testat på exemplen ovan har du kanske stött på felmeddelandet `IndexError`. Det här felet uppstår då du försöker använda ett index som inte finns i en sträng.

```python
mjono = input("Anna merkkijono: ")
print("Kymmenes merkki: " + mjono[9])
```

<sample-output>

Anna merkkijono: **ohjelmoinnin perusteet**
Kymmenes merkki: n

</sample-output>

<sample-output>

Anna merkkijono: **python**

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range

</sample-output>

Ibland orsakas indexeringsfel av en bugg i koden. Det är till exempel relativt vanligt att man försöker indexera för långt då man försöker komma åt det sista tecknet i en sträng:

```python
mjono = input("Anna merkkijono: ")
print("Viimeinen merkki: " + mjono[len(mjono)])
```

Eftersom strängindexeringen börjar med noll kommer det sista tecknet att ha indexet `len(str) - 1`.

Det finns situationer där programmet borde förbereda sig för fel orsakade av indata från användaren:

```python
mjono = input("Anna merkkijono: ")
if len(mjono) > 0:
    print("Ensimmäinen merkki: " + mjono[0])
else:
    print("Merkkijono on tyhjä eli ensimmäistä merkkiä ei ole")
```

I exemplet ovan skulle en sträng med längden noll ha orsakat problem om programmeraren inte skulle ha lagt till en längdkontroll i koden. En sträng med längden noll är en tom sträng. I det här fallet kan vi orsaka en sådan med att helt enkelt trycka på tangenten Enter utan att skriva något annat.

<in-browser-programming-exercise name="Lopusta alkuun" tmcname="osa03-05c_lopusta_alkuun">

Kirjoita ohjelma, joka kysyy käyttäjältä merkkijonon ja tulostaa sitten merkkijonon merkit allekkain käänteisessä järjestyksessä lopusta alkuun.

Esimerkkisuoritus:

<sample-output>

Anna merkkijono: **heippa**
a
p
p
i
e
h

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Toinen ja toiseksi viimeinen" tmcname="osa03-06_toinen_ja_toiseksi_viimeinen">


Tee ohjelma, joka kysyy käyttäjältä sanan ja kertoo, ovatko sen toinen ja toiseksi viimeinen merkki samoja.

<sample-output>

Anna sana: **python**
Toinen ja toiseksi viimeinen kirjain eroavat

</sample-output>

<sample-output>

Anna sana: **pascal**
Toinen ja toiseksi viimeinen kirjain on a

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Risuaitaviiva" tmcname="osa03-09_risuaitaviiva">

Tee ohjelma, joka piirtää käyttäjän määräämän levyisen risuaitaviivan.

<sample-output>

Leveys: **3**
<pre>
###
</pre>

</sample-output>

<sample-output>

Leveys: **8**
<pre>
########
</pre>

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Risuaitasuorakulmio" tmcname="osa03-10_risuaitanelio">

Laajenna edellistä niin, että käyttäjä syöttää myös piirrettävien rivien määrän

<sample-output>

Leveys: **10**
Korkeus: **3**
##########
##########
##########

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Alleviivaus" tmcname="osa03-11_alleviivaus">

Tee ohjelma, joka pyytää käyttäjältä merkkijonoja ja tulostaa kunkin merkkijonon oheisen esimerkin mukaisesti alleviivattuna. Ohjelman suoritus päättyy, kun käyttäjä syöttää tyhjän merkkijonon, eli merkkijonon jonka pituus on 0.

<sample-output>

Anna merkkijono: **Moi kaikki!**
<pre>
Moi kaikki!
-----------
</pre>
Anna merkkijono: **Tämä on testijono**
<pre>
Tämä on testijono
-----------------
</pre>
Anna merkkijono: **a**
<pre>
a
-
</pre>
Anna merkkijono:

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Tasaus oikeaan" tmcname="osa03-12_tasaus_oikeaan">

Tee ohjelma, joka kysyy käyttäjältä merkkijonon ja tulostaa sen niin, että tulostetuksi tulee tasan 20 merkkiä. Jos merkkijono on lyhyempi, alkuun tulee tarvittava määrä tähtiä `*`.

Voit olettaa, että syötetyssä merkkijonossa on enintään 20 merkkiä.

<sample-output>

Sana: **python**
<pre>
**************python
</pre>

</sample-output>

<sample-output>

Sana: **pitkämerkkijono**
<pre>
*****pitkämerkkijono
</pre>

</sample-output>

<sample-output>

Sana: **tosipitkämerkkijono**
<pre>
*tosipitkämerkkijono
</pre>

</sample-output>


</in-browser-programming-exercise>

<in-browser-programming-exercise name="Sanalaatikko" tmcname="osa03-13_sanalaatikko">

Tee ohjelma, joka kysyy käyttäjältä sanaa ja tulostaa sanan tähtiraameihin, joissa sana on keskellä. Raamien leveys on 30 merkkiä, ja voit olettaa, että sana mahtuu raameihin.

Huom! Jos sanan pituus on pariton, voit tulostaa sanan kumpaan tahansa mahdollisista keskikohdista.

<sample-output>

Sana: **koe**
<pre>
******************************
*            koe             *
******************************
</pre>

</sample-output>

<sample-output>

Sana: **python**
<pre>
******************************
*           python           *
******************************
</pre>

</sample-output>

</in-browser-programming-exercise>


## Delsträngar

En delsträng av en sträng är en sekvens av tecken som formar en del av den ursprungliga delen. Till exempel strängen `exempel` innehåller delsträngarna `exem`, `mpe`, `el` med flera. I Python kallas extrahering av delsträngar slicing.

Om du vet vad det inledande och avslutande indexet för en delsträng är, kan du extrahera (slice) delsträngen med notationen `[a:b]`. Då kommer delsträngen att börja vid index `a` och ta slut vid det sista tecknet före indexet `b` – det vill säga inklusive den första bokstaven men exklusive den sista. Du kan tänka att indexen är streck ritade på den vänstra sidan av det indexerade tecknet – som vi illustrerar nedan:

<img src="3_2_3.png">

Låt oss kika lite mer på extraherade (sliced) strängar:

```python
mjono = "saippuakauppias"

print(mjono[0:3])
print(mjono[4:10])

# jos alkukohta puuttuu, se on oletuksena 0
print(mjono[:3])

# jos loppukohta puuttuu, se on oletuksena merkkijonon pituus
print(mjono[4:])
```

<sample-output>

sai
puakau
sai
puakauppias

</sample-output>

<text-box variant='hint' name='Halvöppna intervall'>

I Python är intervallet `[a:b]` i halvöppet då vi behandlar strängar. Det här innebär att tecknet i det inledande indexet `a` inkluderas i intervallet medan tecknet i det avslutande indexet `b` lämnas bort. Varför så?

Det finns ingen tydlig orsak till detta. Det är helt enkelt en vana som har sitt ursprung i andra programmeringsspråk.

Halvöppna intervall kan kännas jobbiga men i praktiken har de sina nyttiga sidor. Du kan till exempel enkelt räkna längden på en delsträng med `b - a`. Å andra sidan måste du komma ihåg att tecknet i slutet vid indexet `b` inte kommer att inkluderas i delsträngen.

</text-box>

<in-browser-programming-exercise name="Osajonot 1" tmcname="osa03-07_osajonot1">

Tee ohjelma, joka kysyy käyttäjältä merkkijonon ja tulostaa sitten kaikki sen ensimmäisestä merkistä alkavat osajonot pituusjärjestyksessä.

Esimerkkitulostus:

<sample-output>

Anna merkkijono: **testi**
t
te
tes
test
testi

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Osajonot 2" tmcname="osa03-08_osajonot2">

Tee ohjelma, joka kysyy käyttäjältä merkkijonon ja tulostaa sitten kaikki sen viimeiseen merkkiin päättyvät osajonot pituusjärjestyksessä.

Esimerkkitulostus:

<sample-output>

Anna merkkijono: **testi**
i
ti
sti
esti
testi

</sample-output>

</in-browser-programming-exercise>

## Söka efter delsträngar

Operatorn `in` berättar oss om en sträng innehåller en specifik delsträng. Boolean-uttrycket `a in b` är sant om `b` innehåller delsträngen `a`.

Till exempel den här kodsnutten…

```python
mjono = "testi"

print("t" in mjono)
print("x" in mjono)
print("est" in mjono)
print("ets" in mjono)
```

…skriver ut följande:

<sample-output>

True
False
True
False

</sample-output>

Programmet nedan låter användaren söka efter delsträngar i en sträng som är hårdkodad i programmet:

```python
mjono = "saippuakauppias"

while True:
    osa = input("Mitä etsit? ")
    if osa in mjono:
        print("Löytyi")
    else:
        print("Ei löytynyt")
```

<sample-output>

Mitä etsit? **kaup**
Löytyi
Mitä etsit? **abc**
Ei löytynyt
Mitä etsit? **ippu**
Löytyi
...

</sample-output>

<in-browser-programming-exercise name="Löytyvätkö vokaalit" tmcname="osa03-13b_loytyvatko_vokaalit">

Tee ohjelma, joka kysyy käyttäjältä merkkijonon ja tulostaa sitten tiedon löytyvätkö vokaalit a, e ja o merkkijonosta.

Voit olettaa, että merkkijono on syötetty kokonaan pienillä kirjaimilla. Katso mallia esimerkkitulostuksesta.

Esimerkkitulostus:

<sample-output>

Anna merkkijono: **heippa sulle**
a löytyy
e löytyy
o ei löydy

</sample-output>

<sample-output>

Anna merkkijono: **moi**
a ei löydy
e ei löydy
o löytyy

</sample-output>


</in-browser-programming-exercise>

Operatorn `in` returnerar ett Boolean-värde. Det berättar oss alltså bara att en delsträng existerar i en sträng, men baserat på den informationen vet vi inte var delsträngen befinner sig. Däremot kan metoden `find` hos strängar användas för det här syftet. Som argument ger man delsträngen som söks efter. Tillbaka får vi ett värde som indikerar det första indexet där delsträngen hittades – eller `-1` om delsträngen inte hittas i strängen.

Så här fungerar det:

<img src="3_2_4.png">

Några exempel där vi använder `find`:

```python
mjono = "testi"

print(mjono.find("t"))
print(mjono.find("x"))
print(mjono.find("est"))
print(mjono.find("ets"))
```

<sample-output>

0
-1
1
-1

</sample-output>

Ovanstående delsträngsexempel gjort med `find`:

```python
mjono = "saippuakauppias"

while True:
    osa = input("Mitä etsit? ")
    kohta = mjono.find(osa)
    if kohta >= 0:
        print(f"Löytyi kohdasta {kohta}")
    else:
        print("Ei löytynyt")
```

<sample-output>

Mitä etsit? **kaup**
Löytyi kohdasta 7
Mitä etsit? **abc**
Ei löytynyt
Mitä etsit? **ippu**
Löytyi kohdasta 2
...

</sample-output>

<text-box variant='hint' name='Metoder'>

Vi använde ovan metoden `find` hos strängar. Metoder fungerar ganska lika jämfört med funktioner som vi såg på i den föregående modulen. Skillnaden mellan dem är att metoder alltid är kopplade till det objekt som de kallas på. Objektet är den entitet som namnges före metoden som kallas. I det här fallet är objektet strängen där metoden söker efter delsträngen som ges som argument till metoden.

</text-box>

<in-browser-programming-exercise name="Ensimmäisen osajonon haku" tmcname="osa03-13c_osajonon_haku">

Tee ohjelma, joka kysyy käyttäjältä merkkijonoa ja yksittäistä merkkiä. Ohjelma tulostaa merkkijonosta löytyvän ensimmäisen kolmen merkin pituisen osajonon, jonka alkukirjain on käyttäjän syöttämä merkki. Voit olettaa, että merkkijono on vähintään kolmen merkin pituinen.

<sample-output>

Sana: **apinatalo**
Merkki: **a**
api

</sample-output>

<sample-output>

Sana: **banaani**
Merkki: **n**
naa

</sample-output>

<sample-output>

Sana: **tomaatti**
Merkki: **x**

</sample-output>

<sample-output>

Sana: **python**
Merkki: **n**

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Kaikkien osajonojen haku" tmcname="osa03-14_osajonojen_haku">

Tee edellisestä ohjelmasta laajennettu versio, joka tulostaa _kaikki merkkijonon sisältämät kolmen merkin pituiset osajonot_, joiden alkukirjain on käyttäjän syöttämä merkki. Voit olettaa, että merkkijono on vähintään kolmen merkin pituinen.

<sample-output>

Sana: **apinatalo**
Merkki: **a**
api
ata
alo

</sample-output>

<sample-output>

Sana: **banaani**
Merkki: **n**
naa

</sample-output>

**Vihje** seuraava esimerkki saattaa antaa jotain inspiraatiota eräästä tavasta miten tätä tehtävää voi lähestyä

```python
sana = input("Sana: ")
while True:
    if len(sana) == 0:
        break
    print(sana)
    sana = sana[2:]
```

<sample-output>

Sana: **apinatalo**
apinatalo
inatalo
atalo
alo
o

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Toinen esiintymä" tmcname="osa03-15_toinen_esiintyma">

Tee ohjelma, joka etsii merkkijonosta osajonon toisen esiintymän. Jos toista (tai edes ensimmäistä) esiintymää ei löydy, ohjelma tulostaa tästä tiedon.

Määritellään tässä yhteydessä, että esiintymät _eivät_ voi mennä päällekkäin, merkkijonossa `aaaa` osajonon `aa` toinen esiintymä löytyy siis indeksin 2 kohdalta.

Muutama esimerkkisuoritus:

<sample-output>

Anna merkkijono: **abcabc**
Anna osajono: **ab**
Osajonon toinen esiintymä on kohdassa 3.

</sample-output>

<sample-output>

Anna merkkijono: **saippuakauppias**
Anna osajono: **a**
Osajonon toinen esiintymä on kohdassa 6.

</sample-output>

<sample-output>

Anna merkkijono: **aybabtu**
Anna osajono: **ba**
Osajono ei esiinny merkkijonossa kahdesti.

</sample-output>

</in-browser-programming-exercise>

<quiz id="e292f94e-9004-5e1b-9149-83a4e810c770"></quiz>
