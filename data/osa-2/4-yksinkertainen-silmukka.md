---
path: '/osa-2/4-yksinkertainen-silmukka'
title: 'Enkla loopar'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* vet du vad en loop betyder i programmeringssammanhang
* kan du använda dig av en `while True` -loop i dina program
* kommer du att kunna använda dig av `break`-kommandot för att avbryta loopen.

</text-box>

Vi har nu undersökt if-satser. Ett annat viktigt koncept inom programmering är repetition. De här två koncepten är grundläggande strukturer som varje programmerare väntas kunna. De är kontrollstrukturer – de ger dig möjligheten att påverka vilka kodrader körs och när de körs. Medan if-satser låter dig välja mellan olika delar av kod, finns loopar till för att köra en del av koden på nytt. Programmet går alltså tillbaka till en viss rad i koden ett antal gånger. En iteration är en ”runda” av en loop – det vill säga den process då loopens kod körs från början till slutet.

I den här delen presenterar vi en enkel while-loop. Dess struktur påminner om if-satsen. I nästa del dyker vi djupare in i det som loopar kan erbjuda oss.

Vi tar en titt på ett program som ber användaren att ge en siffra som skrivs upp upphöjt med två. Programmet körs tills användaren ger siffran -1:

```python
while True:
    luku = int(input("Anna luku, -1 lopettaa: "))

    if luku == -1:
        break

    print(luku ** 2)

print("Kiitos ja moi!")
```

Så här kan det se ut när programmet körs:

<sample-output>

Anna luku, -1 lopettaa: **2**
4
Anna luku, -1 lopettaa: **4**
16
Anna luku, -1 lopettaa: **10**
100
Anna luku, -1 lopettaa: **-1**
Kiitos ja moi!

</sample-output>

Som du ser ovan, frågar programmet om ett nummer flera gånger. Detta tack vare while-satsen. När användaren anger siffran -1 kommer `break`-kommandot att köras. Loopen avbryts och programmet fortsätter efter while-blocket.

När man arbetar med loopar är det viktigt att loopen avslutas vid något skede. Om man inte tar det här i beaktande kan loopen fortsätta för evigt. Vi ändrar lite på ovanstående exempel för att åstadkomma en sådan här situation:

```python
luku = int(input("Anna luku, -1 lopettaa: "))
while True:
    if luku == -1:
        break

    print(luku ** 2)

print("Kiitos ja moi!")
```

I den här versionen frågar programmet användaren efter siffran utanför loopen. Om användaren ger någon annan siffra än -1 kommer loopen aldrig att avslutas. Vi har en oändlig loop vilket i princip betyder att koden körs oavbrutet, för evigt:

<sample-output>

Anna luku, -1 lopettaa: **2**
4
4
4
4
4
4
4
4
(jatkuu ikuisesti...)

</sample-output>

Följande program har en mycket liknande struktur jämfört med exemplet ovan, men för användaren ser det ganska annorlunda ut. Det här programmet låter användaren fortsätta endast då den korrekta pin-koden 1234 anges:

```python
while True:
    koodi = input("Anna PIN-koodi: ")
    if koodi == "1234":
        break
    print("Väärin... yritä uudelleen")

print("PIN-koodi oikein!")
```

<sample-output>

Anna PIN-koodi: **0000**
Väärin... yritä uudelleen
Anna PIN-koodi: **9999**
Väärin... yritä uudelleen
Anna PIN-koodi: **1234**
PIN-koodi oikein!

</sample-output>

<in-browser-programming-exercise name="Jatketaanko" tmcname="osa02-15_jatketaanko">

Kirjoita edellä olevaa toistolause-esimerkkiä mukaillen ohjelma, joka tulostaa viestin "moi" ja kysyy käyttäjältä "Jatketaanko?" kunnes käyttäjä syöttää merkkijonon "ei". Tämän jälkeen tulostetaan merkkijono "ei sitten" ja suoritus päättyy.

Esimerkkitulostus

<sample-output>

moi
Jatketaanko? **kyllä**
moi
Jatketaanko? **yes**
moi
Jatketaanko? **jawohl**
moi
Jatketaanko? **ei**
ei sitten

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Syötteen rajaus" tmcname="osa02-16_syotteen_rajaus">

Kirjoita ohjelma, joka kysyy käyttäjältä lukuja. Mikäli luku on negatiivinen (eli pienempi kuin nolla), käyttäjälle tulostetaan viesti "Epäkelpo luku" ja käyttäjältä kysytään uutta lukua. Jos taas luku on nolla, lukujen lukeminen lopetetaan ja ohjelma poistuu toistolauseesta.

Mikäli luku on positiivinen, ohjelma tulostaa luvun neliöjuuren käyttäen `sqrt`-funktiota, joka on tuotu ohjelmaan `import`-lauseella. Esimerkki funktion käytöstä:

```python
# Tämä pitää olla ohjelman alussa, jotta sqrt toimii
from math import sqrt

print(sqrt(9))
```

<sample-output>

3.0

</sample-output>

Esimerkki ohjelman suorituksesta:

<sample-output>

Syötä luku: **16**
4.0
Syötä luku: **4**
2.0
Syötä luku: **-3**
Epäkelpo luku
Syötä luku: **1**
1.0
Syötä luku: **0**
Lopetetaan...

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Lähtölaskenta" tmcname="osa02-17_lahtolaskenta">

Tehtäväpohjassa olevan ohjelman

```python
luku = 5
print("Lähtölaskenta!")
while True:
  print(luku)
  luku = luku - 1
  if luku > 0:
    break

print("Nyt!")
```

olisi tarkoitus toimia seuraavasti:

<sample-output>

Lähtölaskenta!
5
4
3
2
1
Nyt!

</sample-output>

Korjaa ohjelmassa oleva ongelma.

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Salasana uudelleen" tmcname="osa02-18_salasana_uudelleen">

Tee ohjelma, joka kysyy käyttäjältä salasanaa ja tämän jälkeen pyytää toistamaan salasanan niin kauan, kunnes käyttäjä syöttää ensimmäisenä annetun salasanan uudelleen.

<sample-output>

Salasana: **sekred**
Toista salasana: **salainen**
Ei ollut sama!
Toista salasana: **enmuistaenää123**
Ei ollut sama!
Toista salasana: **sekred**
Käyttäjätunnus luotu!

</sample-output>

</in-browser-programming-exercise>

## Loopar och hjälpvariabler

Vi gör föregående exemplet en aning mer realistiskt. Det här exemplet tillåter användaren endast tre försök att ge korrekt pin-kod.

Programmet består av två hjälpvariabler: `forsok` håller reda på hur många gånger användaren angett en pin-kod och `lyckades` är antingen `True` eller `False` beroende på om användaren ger den korrekta koden eller inte.

```python
yritykset = 0

while True:
    tunnus = input("Anna PIN-koodi: ")
    yritykset += 1

    if tunnus == "1234":
        onnistui = True
        break

    if yritykset == 3:
        onnistui = False
        break

    # tänne tullaan jos väärin JA ei ole jo kolmea yritystä
    print("Väärin... yritä uudelleen")

if onnistui:
    print("PIN-koodi oikein!")
else:
    print("Liian monta yritystä...")
```

<sample-output>

Anna PIN-koodi: **0000**
Väärin... yritä uudelleen
Anna PIN-koodi: **1234**
PIN-koodi oikein!

</sample-output>

<sample-output>

Anna PIN-koodi: **0000**
Väärin... yritä uudelleen
Anna PIN-koodi: **9999**
Väärin... yritä uudelleen
Anna PIN-koodi: **4321**
Liian monta yritystä...

</sample-output>

Loopen avslutas antingen om pin-koden är korrekt eller då maxantalet försök har uppnåtts. Efterföljande if-sats kollar variabeln `lyckades` värde och skriver ut ett meddelande baserat på värdet.

## Print-satser för debuggning i loopar

Att introducera loopar i ett program ökar på möjligheten för buggar. Därför är det viktigt att senast nu utnyttja print-satser i debuggningssyfte – dem såg vi på i den första delen av den pågående modulen.

Vi kikar på ett nästan identiskt program som i det föregående exemplet. Dock finns det en märkbar skillnad:

```python
yritykset = 0

while True:
    tunnus = input("Anna PIN-koodi: ")
    yritykset += 1

    if yritykset == 3:
        onnistui = False
        break

    if tunnus == "1234":
        onnistui = True
        break

    print("Väärin... yritä uudelleen")

if onnistui:
    print("PIN-koodi oikein!")
else:
    print("Liian monta yritystä...")
```

Den här versionen fungerar konstigt när användaren anger den korrekta koden på det tredje försöket:

<sample-output>

Anna PIN-koodi: **0000**
Väärin... yritä uudelleen
Anna PIN-koodi: **9999**
Väärin... yritä uudelleen
Anna PIN-koodi: **1234**
Liian monta yritystä...

</sample-output>

Nu borde vi alltså reda ut det här problemet. Några `print`-satser borde hjälpa oss att debugga – så låt oss lägga till sådana i loopen:

```python
while True:
    print("whilen lohko alkaa:")
    tunnus = input("Anna PIN-koodi: ")
    yritykset += 1

    print("yritykset:", yritykset)
    print("ehto1:", yritykset == 3)
    if yritykset == 3:
        onnistui = False
        break

    print("tunnus:", tunnus)
    print("ehto2:", tunnus == "1234")
    if tunnus == "1234":
        onnistui = True
        break

    print("Väärin... yritä uudelleen")
```

<sample-output>

whilen lohko alkaa:
Anna PIN-koodi: **2233**
yritykset: 1
ehto1: False
tunnus: 2233
ehto2: False
Väärin... yritä uudelleen
whilen lohko alkaa:
Anna PIN-koodi: **4545**
yritykset: 2
ehto1: False
tunnus: 4545
ehto2: False
Väärin... yritä uudelleen
whilen lohko alkaa:
Anna PIN-koodi: **1234**
yritykset: 3
ehto1: True
Liian monta yritystä...

</sample-output>

Från utskriften ovan märker vi att under den tredje iterationen kommer villkoret i den första if-satsen att vara sant och därmed hinner vi aldrig fram till den andra if-satsen i och med att loopen avslutas. Därmed kontrolleras koden aldrig:

```python
  while True:
    # ....

    # tämä lohko on liian aikaisin
    if yritykset == 3:
        onnistui = False
        break

    # tänne ei päästä enää kolmannella yrityksellä...
    if tunnus == "1234":
        onnistui = True
        break
```

Ordningen på if-satser eller grenar inom if-satser är vanliga orsaker till buggar – framför allt inom loopar. Debuggning med hjälp av print-satser hjälper förvånansvärt ofta.

<in-browser-programming-exercise name="PIN ja yritysten määrä" tmcname="osa02-19_pin_ja_yritysten_maara">

Tee sovellus, joka kysyy käyttäjältä PIN-koodia niin kauan, kunnes käyttäjä antaa oikean PIN-koodin _4321_. Ohjelma kertoo yritysten lukumäärän:

<sample-output>

PIN-koodi: **3245**
Väärin
PIN-koodi: **1234**
Väärin
PIN-koodi: **0000**
Väärin
PIN-koodi: **4321**
Oikein, tarvitsit 4 yritystä

</sample-output>

Tulostus on hieman erilainen jos PIN-koodi on oikea heti ensimmäisellä yrityksellä:

<sample-output>

PIN-koodi: **4321**
Oikein, tarvitsit vain yhden yrityksen!

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Seuraava karkausvuosi" tmcname="osa02-20_seuraava_karkausvuosi">

Tee ohjelma, joka kyselee käyttäjältä vuosilukua ja kertoo, milloin on seuraava karkausvuosi.

<sample-output>

Vuosi: **2019**
Vuotta 2019 seuraava karkausvuosi on 2020

</sample-output>

Jos käyttäjän syöttämä vuosi on karkausvuosi (kuten 2020), ohjelma ei kerro tätä vuotta vaan sitä seuraavan karkausvuoden:

<sample-output>

Vuosi: **2020**
Vuotta 2020 seuraava karkausvuosi on 2024

</sample-output>

</in-browser-programming-exercise>

## Kombinera strängar med `+`-operatorn

Exemplet ovan använde hjälpvariabeln `forsok` för att hålla koll på hur många gånger användaren försökt skriva in en kod:

```python
yritykset = 0

while True:
    tunnus = input("Anna PIN-koodi: ")
    yritykset += 1
    # ...
```

Variabeln tilldelas värdet noll utanför loopen och varje iteration ökar på siffran med ett.

Något liknande kan man också göra med strängar. Programmet kan till exempel hålla koll på de pin-koder användaren angett:

```python
tunnukset = ""
yritykset = 0

while True:
    tunnus = input("Anna PIN-koodi: ")
    yritykset += 1
    tunnukset += tunnus + ", "
    # ...
```

Hjälpvariabeln kan tilldelas värdet `””` – det vill säga en tom sträng:

```python
tunnukset = ""
```

För varje iteration blir strängen längre i och med att koden användaren angett läggs till i slutet av strängen tillsammans med ett komma och ett mellanslag.

```python
    tunnus = input("Anna PIN-koodi: ")
    tunnukset += tunnus + ", "
```

Om användaren anger koderna 1111 2222 1234 kommer värdet på `koder` till slut att vara:

<sample-output>

1111, 2222, 1234,

</sample-output>


<in-browser-programming-exercise name="Tarina" tmcname="osa02-21_tarina">

### Osa 1

Tee ohjelma, joka pyytää käyttäjää syöttämään sanoja. Kun käyttäjä syöttää sanan `loppu`, ohjelma tulostaa sanoista muodostuneen tarinan ja suoritus päättyy.

<sample-output>

Anna sana: **Olipa**
Anna sana: **kerran**
Anna sana: **pieni**
Anna sana: **talo**
Anna sana: **preerialla**
Anna sana: **loppu**
Olipa kerran pieni talo preerialla

</sample-output>

### Osa 2

Muokkaa edellisen tehtävän ohjelmaa niin, että sanojen syöttäminen päättyy, jos käyttäjä syöttää sanan `loppu` tai käyttäjä syöttää saman sanan kaksi kertaa peräkkäin.

<sample-output>

Anna sana: **Alussa**
Anna sana: **oli**
Anna sana: **suo**
Anna sana: **kuokka**
Anna sana: **ja**
Anna sana: **Jussi**
Anna sana: **Jussi**
Alussa oli suo kuokka ja Jussi

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Lukujen käsittelyä" tmcname="osa02-22_lukujen_kasittelya">

Tee ohjelma, joka pyytää käyttäjää syöttämään kokonaislukuja. Ohjelma pyytää lukuja niin kauan kunnes käyttäjä syöttää nollan.

<sample-output>

Syötä kokonaislukuja, 0 lopettaa:
Luku: **5**
Luku: **22**
Luku: **9**
Luku: **-2**
Luku: **0**

</sample-output>

### Osa 1: lukumäärä

Syötteiden lukemisen jälkeen ohjelman tulee tulostaa syötettyjen lukujen lukumäärä. Syötteen loppumisesta kertovaa nollaa ei tule ottaa huomioon lukumäärässä.

Tarvitset tässä uuden muuttujan, jonka avulla pidät kirjaa luettujen lukujen määrästä.

<sample-output>

... lukujen kysely
Lukuja yhteensä 4

</sample-output>

### Osa 2: summa

Laajenna ohjelmaa siten, että se tulostaa syötettyjen lukujen summa. Syötteen loppumisesta kertovaa nollaa ei tule ottaa huomioon summan laskemisessa.

Ohjelman tulostus laajenee seuraavasti:

<sample-output>

... lukujen kysely
Lukuja yhteensä 4
Lukujen summa 34

</sample-output>

### Osa 3: keskiarvo

Laajenna ohjelmaa siten, että se tulostaa syötettyjen lukujen keskiarvon. Syötteen loppumisesta kertovaa nollaa ei tule ottaa huomioon keskiarvon laskemisessa. Voit olettaa, että käyttäjä syöttää aina vähintään yhden luvun.

<sample-output>

... lukujen kysely
Lukuja yhteensä 4
Lukujen summa 34
Lukujen keskiarvo 8.5

</sample-output>

#### Osa 4: positiiviset ja negatiiviset

Laajenna ohjelmaa siten, että se tulostaa positiivisten ja negatiivisten lukujen lukumäärät

<sample-output>

... lukujen kysely
Lukuja yhteensä 4
Lukujen summa 34
Lukujen keskiarvo 8.5
Positiivisia 3
Negatiivisia 1

</sample-output>

</in-browser-programming-exercise>

<quiz id="4ba8f15f-2ddd-5630-b244-9b83ca0f0cb6"></quiz>

Vänligen svara på en kort enkät som behandlar den här veckans material.

<quiz id="38336a14-1f2f-59fb-8cc6-5afb36381005"></quiz>
