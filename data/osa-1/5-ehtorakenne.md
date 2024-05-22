---
path: "/osa-1/5-ehtorakenne"
title: "If-satser"
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* kan du använda dig av en enkel if-sats när du programmerar
* vet du vad ett Boolean-värde är
* kan du uttrycka villkor med hjälp av jämförelseoperatorer.

</text-box>

Hittills har vi skapat program där koden körts rad för rad från början till slut. Istället för att köra varje kodrad när programmet är igång är det ofta nyttigt att ha delar i programmet som endast körs i vissa situationer.

Till exempel följande program verifierar att användaren är tillräckligt gammal:

```python
ika = int(input("Kuinka vanha olet? "))

if ika > 17:
    print("Olet täysi-ikäinen!"
    print("Tässä siis sinulle ikiomaksi GTA6.")

print("Seuraava asiakas, kiitos!")
```

När användaren är över 17 år, borde det se ut så här när programmet körs:

<sample-output>

Kuinka vanha olet? **18**
Olet täysi-ikäinen!
Tässä siis sinulle ikiomaksi GTA6.
Seuraava asiakas, kiitos!

</sample-output>

Däremot, om användaren är 17 eller yngre, ser utskriften ut så här:

<sample-output>

Kuinka vanha olet? **16**
Seuraava asiakas, kiitos!

</sample-output>

Dessa exempel visar hur ett värde som getts till programmet påverkar vilka delar av koden som körs. Programmet innehåller en if-sats med kod som körs enbart då ett definierat villkor uppfylls.

<img src="1_6.png">

I en if-sats följs nyckelordet `if` med ett villkor som till exempel kan vara en jämförelse av två värden. Koden som följer körs endast då villkoret uppfylls.

Notera kolontecknet. Om det saknas…

```python
ika = 10

# kaksoispiste unohtui seuraavan rivin lopusta
if ika > 17
    print("Olet täysi-ikäinen.")
```

…orsakas ett fel när programmet körs:

<sample-output>
<pre>
File "ohjelma.py", line 3
  if ika > 17
            ^
SyntaxError: invalid syntax
</pre>
</sample-output>

## Jämförelseoperatorer

Det är vanligt att man vill jämföra två värden sinsemellan. Här följer en tabell över de vanligaste jämförelseoperatorerna i Python:

| Operator | Betydelse                | Exempel  |
|:--------:|--------------------------|----------|
| `==`     | Är lika med              | `a == b` |
| `!=`     | Är inte lika             | `a != b` |
| `>`      | Större än                | `a > b`  |
| `>=`     | Större än eller lika med | `a >= b` |
| `<`      | Mindre än                | `a < b`  |
| `<=`     | Mindre än eller lika med | `a <= b` |

Vi tar nu en titt på ett program som skriver ut olika saker baserat på det värde som användaren anger. Här har vi if-satser som kan uppfyllas då värdet är negativt, positivt eller lika med noll:

```python
luku = int(input("Anna luku: "))

if luku < 0:
    print("Luku on negatiivinen.")

if luku > 0:
    print("Luku on positiivinen.")

if luku == 0:
    print("Luku on nolla.")
```

Här har vi tre exempel med olika indata:

<sample-output>

Anna luku: **15**
Luku on positiivinen.

</sample-output>

<sample-output>

Anna luku: **-18**
Luku on negatiivinen.

</sample-output>

<sample-output>

Anna luku: **0**
Luku on nolla.

</sample-output>

## Indentering

Python känner igen att en kodsnutt hör till en if-sats då varje rad är indenterad på samma sätt. Det här betyder att det finns mellanrum i början av varje kodrad som hör till if-satsen. Mellanrummet ska vara det samma för varje rad.

Exempelvis:

````python
salasana = input("Anna salasana: ")

if salasana == "kissa":
    print("Tiesit salasanan!")
    print("Olet siis joko oikea käyttäjä...")
    print("...tai melkoinen hakkerivelho.")

print("Ohjelman suoritus päättyi. Kiitos ja hei!")
````

Du kan använda Tab-tangenten för att lägga till mellanrum där det behövs.

<img src="1_6_keyboard.png">

Dessutom kan flera texteditorer automatiskt indentera den följande raden när Enter-tangenten trycks efter ett kolon. Du får bort indenteringen genom att använda Backspace-tangenten i början av en rad.

<img src="1_6_keyboard2.png">
<small><center>
Näppäimistökuvien alkuperä:
 <a href="https://pixabay.com/users/Clker-Free-Vector-Images-3736/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=311803">Clker-Free-Vector-Images</a> from <a href="https://pixabay.com/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=311803">Pixabay</a>
</center></small>

<in-browser-programming-exercise name="Orwell" tmcname="osa01-21_orwel">

Tee ohjelma, joka kysyy käyttäjältä kokonaisluvun ja tulostaa merkkijonon "Orwell" jos luku on täsmälleen 1984. Muussa tapauksessa ohjelma ei tulosta mitään.

<sample-output>

Anna luku: **2020**

</sample-output>

<sample-output>

Anna luku: **1984**
Orwell

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Itseisarvo" tmcname="osa01-22_itseisarvo">

Kirjoita ohjelma, joka lukee käyttäjältä kokonaisluvun. Mikäli luku on pienempi kuin 0, ohjelma tulostaa luvun kerrottuna luvulla -1. Muulloin ohjelma tulostaa käyttäjän syöttämän luvun. Alla on muutamia esimerkkejä ohjelman odotetusta toiminnasta.

<sample-output>

Anna luku: **-7**
Luvun itseisarvo on 7

</sample-output>

<sample-output>

Anna luku: **1**
Luvun itseisarvo on 1

</sample-output>

<sample-output>

Anna luku: **-99**
Luvun itseisarvo on 99

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Keittoa vai ei" tmcname="osa01-23_keittoa_vai_ei">

Kirjoita ohjelma, joka kysyy ensin käyttäjän nimen. Jos nimi on mikä tahansa muu kuin "Jerry", ohjelma kysyy keittoannosten lukumäärän ja kertoo sitten kokonaishinnan. Yksi annos maksaa 5,90.

Kaksi esimerkkisuoritusta:

<sample-output>

Mikä on nimesi: **Kramer**
Kuinka monta annosta keittoa: **2**
Kokonaishinta on 11.8
Seuraava!

</sample-output>

<sample-output>

Mikä on nimesi: **Jerry**
Seuraava!

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Luvun suuruusluokka" tmcname="osa01-24_luvun_suuruusluokka">

Tee ohjelma, joka lukee käyttäjältä kokonaisluvun ja kertoo sitten sen suuruusluokan oheisten esimerkkisuoritusten mukaisesti:

<sample-output>

Anna luku: **950**
Luku on pienempi kuin 1000
Kiitos!

</sample-output>

<sample-output>

Anna luku: **59**
Luku on pienempi kuin 1000
Luku on pienempi kuin 100
Kiitos!

</sample-output>

<sample-output>

Anna luku: **2**
Luku on pienempi kuin 1000
Luku on pienempi kuin 100
Luku on pienempi kuin 10
Kiitos!

</sample-output>

<sample-output>

Anna luku: **1123**
Kiitos!

</sample-output>


</in-browser-programming-exercise>


## Boolean-värden och -uttryck

Alla villkor i en if-sats resulterar i ett sanningsvärde, det vill säga sant eller falskt. Till exempel villkoret `a < 5` är sant då `a` är mindre än fem och falskt då `a` är fem eller större.

Denna typ av värden kallas alltså Boolean-värden (efter matematikern George Boole). I Python representerar datatypen `bool` ett sanningsvärde. Variabler av typen `bool` kan endast ha ett av följande värden: `True` (sant) och `False` (falskt).

En kodsnutt som resulterar i något av de ovan nämnda värdena kallas Boolean-uttryck. Ett villkor i en if-sats är alltid ett Boolean-uttryck och kan i flera situationer användas som synonym för ordet villkor.

Resultatet av ett Boolean-uttryck kan lagras i en variabel på samma sätt som vilken som helst annan numerisk räkneoperation:

```python
a = 3
ehto = a < 5
print(ehto)
if ehto:
    print("a on pienempi kuin 5")
```

<sample-output>

True
a on pienempi kuin 5

</sample-output>

Pythons nyckelord `True` och `False` kan också användas direkt som sådana. I det följande exemplet körs `print`-kommandot alltid, eftersom värdet på villkoret är `True`:

```python
ehto = True
if ehto:
    print("Tänne tullaan aina")
```

<sample-output>

Tänne tullaan aina

</sample-output>

Man kan tycka att det inte i ovanstående exempel verkar vara en så nyttig funktion. Senare under kursens lopp ska vi se på situationer där vi kan ha mera nytta av Boolean-variabler.

<in-browser-programming-exercise name="Laskin" tmcname="osa01-25_laskin">

Tee ohjelma, joka kysyy käyttäjältä ensin kaksi lukua ja sen jälkeen komennon. Jos komento on joko _summa_, _tulo_ tai _erotus_, ohjelma laskee syötteille kyseisen operaation tuloksen. Muussa tapauksessa ohjelma ei tulosta mitään.

Esimerkkitulostuksia:

<sample-output>

Luku 1: **10**
Luku 2: **17**
Komento: **summa**

10 + 17 = 27

</sample-output>

<sample-output>

Luku 1: **4**
Luku 2: **6**
Komento: **tulo**

4 * 6 = 24

</sample-output>

<sample-output>

Luku 1: **4**
Luku 2: **6**
Komento: **erotus**

4 - 6 = -2

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Lämpötilat" tmcname="osa01-26_lampotilat">

Tee ohjelma, joka kysyy käyttäjältä lämpötilan fahrenheit-asteina, ja tulostaa sitten lämpötilan celsius-asteina. Jos lämpötila celsius-asteina on pienempi kuin 0, ohjelma tulostaa lisäksi viestin "Paleltaa!".

Kaavan fahrenheit-asteiden muuntamiseksi celsius-asteiksi voit etsiä esimerkiksi googlaamalla.

Kaksi esimerkkisuoritusta:

<sample-output>

Anna lämpötila (F): **101**
101 fahrenheit-astetta on 38.333333333333336 celsius-astetta

Anna lämpötila (F): **21**
21 fahrenheit-astetta on -6.111111111111111 celsius-astetta
Paleltaa!

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Palkka" tmcname="osa01-27_palkka">

Tee ohjelma, joka kysyy tuntipalkkaa, työskenneltyjen tuntien määrää ja viikonpäivää. Ohjelma tulostaa palkan, joka on tuntipalkka kertaa tuntien määrä muina päivinä paitsi sunnuntaisin, jolloin tuntipalkka on kaksinkertainen.

<sample-output>

Tuntipalkka: **8.5**
Työtunnit: **3**
Viikonpäivä: **maanantai**
Palkka 25.5 euroa

</sample-output>

<sample-output>

Tuntipalkka: **12.5**
Työtunnit: **10**
Viikonpäivä: **sunnuntai**
Palkka 250.0 euroa

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Korjaa ohjelma: Korkoa kortille" tmcname="osa01-28_korjaaa_ohjelma_korkoa_kortille">

Ohjelmassa lasketaan bonuskortin saldoon vuoden lopussa lisättävä bonuspistemäärä seuraavan kaavan mukaisesti:

* Jos bonuspisteitä on alle sata, korkona saa 10 % lisää pisteitä
* Muussa tapauksessa korkona saa 15 % lisää pisteitä

Ohjelma siis toimii esim. näin:

<sample-output>

Kuinka paljon pisteitä? **55**
Sait 10 % bonusta
Pisteitä on nyt 60.5

</sample-output>

Ohjelma toimii kuitenkin jollain syötteillä oudosti:

<sample-output>

Kuinka paljon pisteitä? **95**
Sait 10 % bonusta
Sait 15 % bonusta
Pisteitä on nyt 120.175

</sample-output>

Korjaa ohjelma niin, että bonusta tulee joko 10 % tai 15 %, ei koskaan molempia.

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Huomiset vaatteet" tmcname="osa01-29_huomisen_vaatteet">

Tee ohjelma, joka kysyy huomisen sääennusteen ja suosittelee sen mukaista pukeutumista.

Suositus vaihtelee sen mukaan, onko lämpötila yli 20 astetta, yli 10 astetta vai yli 5 astetta. Myös sade vaikuttaa suositukseen.

Ohjelma toimii seuraavasti:

<sample-output>

Kerro huominen sääennuste:
Lämpötila: **21**
Sataako (kyllä/ei): **ei**
Pue housut ja t-paita

</sample-output>

<sample-output>

Kerro huominen sääennuste:
Lämpötila: **11**
Sataako (kyllä/ei): **ei**
Pue housut ja t-paita
Ota myös pitkähihainen paita

</sample-output>

<sample-output>

Kerro huominen sääennuste:
Lämpötila: **7**
Sataako (kyllä/ei): **ei**
Pue housut ja t-paita
Ota myös pitkähihainen paita
Pue päälle takki

</sample-output>

<sample-output>

Kerro huominen sääennuste:
Lämpötila: **3**
Sataako (kyllä/ei): **kyllä**
Pue housut ja t-paita
Ota myös pitkähihainen paita
Pue päälle takki
Suosittelen lämmintä takkia
Kannattaa ottaa myös hanskat
Muista sateenvarjo!

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Toisen asteen yhtälön ratkaiseminen" tmcname="osa01-30_toisen_asteen_yhtalo">

Pythonin `math`-moduulissa on funktio `sqrt`, jolla voi laskea luvun neliöjuuren. Voit käyttää sitä ohjelmassa seuraavasti:

```python
from math import sqrt

print(sqrt(9))
```

Ohjelma tulostaa:

<sample-output>

3.0

</sample-output>

Kirjoita ohjelma, joka ratkaisee toisen asteen yhtälön ax²+bx+c. Ohjelmalle annetaan arvot a, b ja c, ja sen tulee laskea juuret (eli ratkaisut) kaavalla

x = (-b ± sqrt(b²-4ac))/(2a).

Voit olettaa, että yhtälöllä on kaksi juurta, jolloin yllä oleva kaava toimii.

Esimerkkituloste:

<sample-output>

Anna a: **1**
Anna b: **2**
Anna c: **-8**

Juuret ovat 2.0 ja -4.0

</sample-output>

</in-browser-programming-exercise>

Kertauskysely tämän osan asioihin liittyen:

<quiz id="6a20ae0e-38b3-5fb3-93c4-ebd70162fbb6"></quiz>

Vänligen svara på en kort enkät om materialet i den här veckans modul. Du får ett poäng när du fyllt i enkäten.

<quiz id="63e241aa-f451-5dd6-b06e-a363703cdc6c"></quiz>
