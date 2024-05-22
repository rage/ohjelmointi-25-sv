---
path: '/osa-2/2-else-elif'
title: 'Mera om if-satser'
hidden: false
---


<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* kan du skapa grenar inom if-satser
* förstår du skillnaden mellan `if`, `elif` och `else`
* kan du använda restoperatorn `%` i Boolean-uttryck.

</text-box>

Vi tar nu en titt på ett program som ber användaren att ge en siffra och därefter skriver ut ett meddelande vars innehåll beror på om siffran är negativ, positiv eller lika med noll:

```python
luku = int(input("Anna luku: "))

if luku < 0:
    print("Luku on negatiivinen")

if luku >= 0:
    print("Luku on positiivinen tai nolla")
```

Det här verkar något klumpigt och det finns en del upprepning. Vi vill ju bara köra ett av if-blocken eftersom numret alltid är antingen under noll, eller noll eller över. Det vill säga bara ett av villkoren `nummer < 0` och `nummer >= 0` är samtidigt sant. Därför är den fösta if-satsen den enda som behövs – om villkoret är sant är siffran negativ, annars är siffran noll eller över.

I stället för att skapa två if-satser kan vi skapa en gren som körs då alla villkor är osanna. Det här kallas else-sats.

Så här kan vi skriva om det föregående exemplet:

```python
luku = int(input("Anna luku: "))

if luku < 0:
    print("Luku on negatiivinen")
else:
    print("Luku on positiivinen tai nolla")
```

När vi bygger upp en if-else-sats kommer exakt en av grenarna att köras. Se följande bild:

<img src="2_2_1.png">

Obs! Det kan aldrig finnas en else-gren före en if-gren. En if-gren och en else-gren bildar en if-else-sats.

Följande exempel kollar om den siffra användaren anger är jämnt eller inte. Det här kan restoperatorn `%` användas för. Restoperatorn anger resten när två heltal divideras. När ett tal divideras med två är det jämnt då resten är noll. Annars är talet inte jämnt.

```python
luku = int(input("Anna luku: "))

if luku % 2 == 0:
    print("Luku on parillinen")
else:
    print("Luku on pariton")
```

<sample-output>

Anna luku: **5**
Luku on pariton

</sample-output>

Ett annat exempel där strängar jämförs:

```python
oikea = "kissa"
salasana = input("Anna salasana: ")

if salasana == oikea:
    print("Tervetuloa")
else:
    print("Pääsy kielletty")
```

Så här kan det se ut när koden körs:

<sample-output>

Anna salasana: **kissa**
Tervetuloa

</sample-output>

<sample-output>

Anna salasana: **apina**
Pääsy kielletty

</sample-output>


<in-browser-programming-exercise name="Täysi-ikäisyys" tmcname="osa02-04_taysi_ikaisyys" height="400px">

Tee ohjelma, joka kysyy käyttäjän ikää ja kertoo, onko tämä täysi-ikäinen (eli 18-vuotias tai vanhempi).

Esimerkkitulostuksia:

<sample-output>

Kuinka vanha olet? **12**
Et ole täysi-ikäinen!

</sample-output>


<sample-output>

Kuinka vanha olet? **32**
Olet täysi-ikäinen!

</sample-output>

</in-browser-programming-exercise>

## Flera grenar med elif-satser

Ofta finns det fler än två alternativ som ett program måste ta i beaktande. Till exempel resultatet av en fotbollsmatch kan se ut på tre sätt: hemmalaget vinner, bortalaget vinner eller oavgjort.

En if-sats kan bestå av elif-grenar – "else if". Till den här grenen kommer man om villkoret i någon av de tidigare grenarna inte uppfylls.

<img src="2_2_2.png">

Vi kollar på ett program som bestämmer vem som vunnit en match:

```python
maalit_koti = int(input("Kotijoukkueen maalimäärä: "))
maalit_vieras = int(input("Vierasjoukkueen maalimäärä: "))

if maalit_koti > maalit_vieras:
    print("Kotijoukkue voitti!")
elif maalit_vieras > maalit_koti:
    print("Vierasjoukkue voitti!")
else:
    print("Tasapeli!")
```

Programmet kan ge tre olika resultat baserat på de värden som ges:

<sample-output>

Kotijoukkueen maalimäärä: **4**
Vierasjoukkueen maalimäärä: **2**
Kotijoukkue voitti!

</sample-output>

<sample-output>

Kotijoukkueen maalimäärä: **0**
Vierasjoukkueen maalimäärä: **6**
Vierasjoukkue voitti!

</sample-output>

<sample-output>

Kotijoukkueen maalimäärä: **3**
Vierasjoukkueen maalimäärä: **3**
Tasapeli!

</sample-output>

I exemplet ovan finns tre grenar varav exakt en körs. En if-sats kan dock bestå av fler än en elif-gren. Dessutom är en else-gren inte obligatorisk.

Det här är också en helt korrekt if-sats:

```python
print("Joulukalenteri")
pvm = input("Mikä päivä nyt on? ")

if pvm == "24.12.":
    print("Nyt on jouluaatto")
elif pvm == "25.12.":
    print("Nyt on joulupäivä")
elif pvm == "26.12.":
    print("Nyt on tapaninpäivä")

print("Kiitos ja hei.")
```

<sample-output>

Joulukalenteri
Mikä päivä nyt on? **25.12.**
Nyt on joulupäivä
Kiitos ja hei.

</sample-output>

Märk att det föregående exemplet saknar else-gren. Om användaren ger ett datum som inte uppfyller villkoret på någon av if- eller elif-grenarna, kommer ingen av grenarna att köras.

<sample-output>

Joulukalenteri
Mikä päivä nyt on? **1.1.**
Kiitos ja hei.

</sample-output>

<in-browser-programming-exercise name=" Suurempi tai yhtäsuuri" tmcname="osa02-05_suurempi_tai_yhtasuuri"  height="400px">

Tee ohjelma, joka kysyy käyttäjältä kaksi kokonaislukua ja tulostaa niistä suuremman. Jos luvut ovat yhtä suuret, ohjelma huomaa myös tämän.

Esimerkkitulostuksia:

<sample-output>

Anna ensimmäinen luku: **5**
Anna toinen luku: **3**
Suurempi luku: 5

</sample-output>

<sample-output>

Anna ensimmäinen luku: **5**
Anna toinen luku: **8**
Suurempi luku: 8

</sample-output>

<sample-output>

Anna ensimmäinen luku: **5**
Anna toinen luku: **5**
Luvut ovat yhtä suuret!

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Vanhempi" tmcname="osa02-06_vanhempi" height="550px">

Tee ohjelma, joka kysyy kahden henkilön nimen ja iän ja tulostaa vanhemman henkilön nimen.

Esimerkkisyötteitä

<sample-output>

Henkilö 1:
Nimi: **Teppo**
Ikä: **26**
Henkilö 2:
Nimi: **Tiina**
Ikä: **27**
Vanhempi on Tiina

</sample-output>

<sample-output>

Henkilö 1:
Nimi: **Antti**
Ikä: **1**
Henkilö 2:
Nimi: **Venla**
Ikä: **1**
Antti ja Venla ovat yhtä vanhoja

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Aakkosjärjestyksessä viimeinen" tmcname="osa02-07_aakkkosjarjestyksessa_viimeinen"  height="500px">

Lukujen lisäksi Python osaa vertailla myös merkkijonojen suuruusjärjestystä. Merkkijono a on pienempi kuin merkkijono b, jos merkkijono a tulee aakkosjärjestyksessä ennen jonoa b.
Huomaa kuitenkin, että tämä pätee varmasti vain kun
- vertaillaan samankokoisia kirjaimia (eli ISOJA tai pieniä kirjaimia) keskenään ja
- vertailtavissa sanoissa on vain englannin kielestä tuttuja kirjaimia (eli a-z tai A-Z).

Tee ohjelma, joka kysyy käyttäjältä kahta sanaa. Ohjelma tulostaa sanoista sen, joka on aakkosjärjestyksessä jälkimmäinen.

Voit olettaa, että sanat on syötetty kokonaan pienillä kirjaimilla.

Esimerkkisuorituksia eri syötteillä:

<sample-output>

Anna 1. sana: **auto**
Anna 2. sana: **mopo**
mopo on aakkosjärjestyksessä viimeinen.

</sample-output>

<sample-output>

Anna 1. sana: **zorro**
Anna 2. sana: **batman**
zorro on aakkosjärjestyksessä viimeinen.

</sample-output>

<sample-output>

Anna 1. sana: **python**
Anna 2. sana: **python**
Annoit saman sanan kahdesti.

</sample-output>

</in-browser-programming-exercise>

<quiz id="19327e67-83e3-5534-aab5-db3d25f3f8dc"></quiz>
