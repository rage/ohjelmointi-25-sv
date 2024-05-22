---
path: '/osa-2/3-ehtojen-yhdistäminen'
title: 'Kombinera villkor'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* vet du hur man använder operatorerna `and`, `or` och `not` i villkor
* kan du skriva kapslade if-satser.

</text-box>

## Logiska operatorer

Du kan kombinera villkor med de logiska operatorerna `and` och `or`. Operatorn `and` innebär att alla villkor måste vara sanna samtidigt. Operatorn `or` kräver att minst ett av villkoren ska vara sant.

Till exempel villkoret `nummer >= 5 and nummer <= 8` bestämmer att nummer måste samtidigt vara minst fem och högst åtta – alltså mellan fem och åtta.

```python
luku = int(input("Anna luku: "))
if luku >= 5 and luku <= 8:
    print("Luku on välillä 5..8")
```

Villkoret `nummer < 5 or nummer > 8` bestämmer att nummer måste vara mindre än fem eller större än åtta – alltså inte mellan fem till åtta.

```python
luku = int(input("Anna luku: "))
if luku < 5 or luku > 8:
    print("Luku ei ole välillä 5..8")
```

Den här sanningstabellen beskriver hur operatorerna fungerar i olika situationer:

a     | b     | a and b | a or b |
:----:|:-----:|:-------:|:------:|
False | False | False   | False  |
True  | False | False   | True   |
False | True  | False   | True   |
True  | True  | True    | True   |

Ibland kan det vara händigt att veta om något värde inte är sant. Operatorn `not` byter värdet på ett villkor till det motsatta:


a     | not a
:----:|:-----:
True  | False
False | True

Det ovanstående exemplet med talen 5–8 borträknade kan också skrivas så här:

```python
luku = int(input("Anna luku: "))
if not (luku >= 5 and luku <= 8):
    print("Luku ei ole välillä 5..8")
```

Framför allt inom programmering kallas logiska operatorer Boolean-operatorer.


<text-box variant='hint' name='Kombinerade villkor – förenklat'>

Villkoret `x >= a and x <= b` är ett mycket vanligt sätt att bestämma om talet `x` är i intervallet `a` till `b`. Den här strukturen fungerar i flera programmeringsspråk.

Python ger också oss möjligheten att använda oss av ett förenklat uttryckssätt för att kombinera villkor: `a <= x <= b` ger samma resultat som den längre versionen med `and`. Den här notationen är kanske bekant från matematikens värld men den används inte så ofta i Python – kanske för att många andra programmeringsspråk saknar liknande syntax.

</text-box>

## Kombinera och kedja villkor

Det här programmet ber användaren att ge fyra siffror. Sedan kollar programmet vilken siffra som är störst med hjälp av några villkor:

```python
n1 = int(input("Anna luku 1: "))
n2 = int(input("Anna luku 2: "))
n3 = int(input("Anna luku 3: "))
n4 = int(input("Anna luku 4: "))

if n1 > n2 and n1 > n3 and n1 > n4:
    suurin = n1
elif n2 > n3 and n2 > n4:
    suurin = n2
elif n3 > n4:
    suurin = n3
else:
    suurin = n4

print(f" {suurin} on suurin luku.")
```

<sample-output>

Anna luku 1: **2**
Anna luku 2: **4**
Anna luku 3: **1**
Anna luku 4: **1**
4 on suurin luku.

</sample-output>

I exemplet ovan är `n1 > n2 and n1 > n3 and n1 > n4` sant endast då alla tre "delvillkor" är sanna.

<in-browser-programming-exercise name="Iän tarkistus" tmcname="osa02-08_ian_tarkistus">

Tee ohjelma, joka kysyy käyttäjän ikää. Jos ikä ei ole uskottava (se on alle 5 tai mahdoton luku iälle), antaa ohjelma siihen liittyvän kommentin.

Vinkki: tarkastele esimerkkisuorituksia löytääksesi oikean vastineen eri vaihtoehdoille.

Esimerkkitulostuksia:

<sample-output>

Kerro ikäsi? **13**
Ok, olet siis 13-vuotias

</sample-output>

<sample-output>

Kerro ikäsi? **2**
En usko, että osaat kirjoittaa...

</sample-output>

<sample-output>

Kerro ikäsi? **-4**
Taitaa olla virhe

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Veljenpojat" tmcname="osa02-09_veljenpojat">

Tee ohjelma, joka kysyy käyttäjän nimeä. Jos nimeksi syötetään Tupu, Hupu tai Lupu, ohjelma tunnistaa käyttäjän Aku Ankan veljenpojaksi.

Jos nimeksi annetaan Mortti tai Vertti, ohjelma vastaavasti tunnistaa käyttäjän Mikki Hiiren veljenpojaksi.

Esimerkkitulostuksia:

<sample-output>

Anna nimesi: **Mortti**
Olet luultavasti Mikki Hiiren veljenpoika.

</sample-output>

<sample-output>

Anna nimesi: **Hupu**
Olet luultavasti Aku Ankan veljenpoika.

</sample-output>

<sample-output>

Anna nimesi: **Keijo**
Et ole kenenkään tuntemani hahmon veljenpoika.

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Arvosana ja pisteet" tmcname="osa02-10_arvosana_ja_pisteet">

Alla oleva taulukko kuvaa erään kurssin arvosanan muodostumista. Tee ohjelma, joka ilmoittaa kurssiarvosanan annetun taulukon mukaisesti.

pistemäärä   | arvosana
:--:|:----:
< 0 |  mahdotonta!
0-49 | hylätty
50-59 | 1
60-69 | 2
70-79 | 3
80-89| 4
90-100 | 5
\> 100 |  mahdotonta!

Esimerkkitulostuksia:

<sample-output>

Anna pisteet [0-100]: **37**
Arvosana: hylätty

</sample-output>

<sample-output>

Anna pisteet [0-100]: **76**
Arvosana: 3

</sample-output>

<sample-output>

Anna pisteet [0-100]: **-3**
Arvosana: mahdotonta!

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="FizzBuzz" tmcname="osa02-11_fizzbuzz">

Ohjelma kysyy käyttäjältä lukua. Jos luku on jaollinen kolmella, tulostetaan Fizz. Jos luku on jaollinen viidellä, tulostetaan Buzz. Jos luku on jaollinen sekä kolmella, että viidellä, tulostetaan FizzBuzz

Esimerkkitulostuksia:

<sample-output>

Luku: **9**
Fizz

</sample-output>

<sample-output>

Luku: **7**

</sample-output>

<sample-output>

Luku: **20**
Buzz

</sample-output>

<sample-output>

Luku: **45**
FizzBuzz

</sample-output>

</in-browser-programming-exercise>

## Kapslade if-satser

If-satser kan kapslas inom andra if-satser. Till exempel följande program kollar först om en siffra är noll före det kollar om talet är jämnt eller inte.

```python
luku = int(input("Anna luku: "))

if luku > 0:
    if luku % 2 == 0:
        print("Luku on parillinen")
    else:
        print("Luku on pariton")
else:
    print("Luku on negatiivinen")
```

Så här kan programmet fungera:

<sample-output>

Anna luku: **3**
Luku on pariton

Anna luku: **18**
Luku on parillinen

Anna luku: **-4**
Luku on negatiivinen

</sample-output>

När man kapslar if-satser är det kritiskt att indenteringen blir rätt. Indenteringen bestämmer vilka grenar som är länkade ihop. Till exempel en if-gren och en else-gren med samma inledande mellanrum tolkas som grenar av en och samma if-sats.

Ofta kan likadana resultat åstadkommas både med logiska operatorer och kapslade if-satser. Det följande exemplet fungerar helt på samma sätt som det tidigare exemplet:

```python
luku = int(input("Anna luku: "))

if luku > 0 and luku % 2 == 0:
    print("Luku on parillinen")
elif luku > 0 and luku % 2 != 0:
    print("Luku on pariton")
else:
    print("Luku on negatiivinen.")
```

Man kan inte på rak arm säga vilkendera lösning är bättre. Situationen bestämmer ofta hur det lönar sig att bygga upp if-satsen på ett logiskt sätt. I det här exemplet tycker flera personer att versionen med kapsling är mera intuitiv.

<in-browser-programming-exercise name="Karkausvuosi" tmcname="osa02-12_karkausvuosi">

Vuosi on karkausvuosi, jos se on jaollinen 4:llä. Kuitenkin jos vuosi on jaollinen 100:lla, se on karkausvuosi vain silloin, kun se on jaollinen myös 400:lla.

Tee ohjelma, joka lukee käyttäjältä vuosiluvun, ja tarkistaa, onko vuosi karkausvuosi.

<sample-output>

Anna vuosi: **2011**
Vuosi ei ole karkausvuosi.

</sample-output>

<sample-output>

Anna vuosi: **2020**
Vuosi on karkausvuosi.

</sample-output>

<sample-output>

Anna vuosi: **1800**
Vuosi ei ole karkausvuosi.

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Aakkosjärjestyksessä keskimmäinen" tmcname="osa02-13_aakkosjarjestyksessa_keskimmainen">

Tee ohjelma, joka kysyy käyttäjältä kolme kirjainta. Ohjelma tulostaa kirjaimista aakkosjärjestyksessä keskimmäisen.

Voit olettaa, että kirjaimet ovat joko kaikki isoja tai kaikki pieniä kirjaimia.

Esimerkkisuorituksia:

<sample-output>

Anna 1. kirjain: x
Anna 2. kirjain: c
Anna 3. kirjain: p
Keskimmäinen kirjain on p

</sample-output>

<sample-output>

Anna 1. kirjain: C
Anna 2. kirjain: B
Anna 3. kirjain: A
Keskimmäinen kirjain on B

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Lahjaverolaskuri" tmcname="osa02-14_lahjaverolaskuri"  height="500px">

[Verottajan mukaan](https://www.vero.fi/henkiloasiakkaat/omaisuus/lahja/) lahja tarkoittaa sitä, että omaisuus siirtyy toiselle henkilölle ilman korvausta. Lahjasta pitää maksaa lahjaveroa, jos samalta lahjanantajalta saatujen lahjojen arvo on kolmen vuoden aikana 5 000 euroa tai enemmän.

Kun lahja tulee lähimmiltä sukulaisilta, lahjaveron määrä määräytyy seuraavan taulukon [mukaan](https://www.vero.fi/henkiloasiakkaat/omaisuus/lahja/lahjaverolaskuri/):

Lahja	| Vero alarajalla|	Veroprosentti ylimenevästä
:--:|:----:|:----:
5 000 — 25 000 |	100	|8
25 000 — 55 000	| 1 700|	10
55 000 — 200 000|	4 700	|12
200 000 — 1 000 000	|22 100|	15
1 000 000 —	|142 100|	17

Esimerkiksi 6000 euron lahjasta tulee maksaa veroa 180 euroa (100 + (6000-5000) * 0.08) ja 75000 euron lahjasta tulee maksaa veroa 7100 euroa (4700 + (75000-55000) * 0.12).

Tee ohjelma, joka laskee lahjaveron lähimpien sukulaisten antamalle lahjalle. Alla on muutama esimerkki ohjelman toiminnasta.

<sample-output>

Lahjan suuruus? **3500**
Ei veroa!

</sample-output>

<sample-output>

Lahjan suuruus? **5000**
Vero: 100.0 euroa

</sample-output>

<sample-output>

Lahjan suuruus? **27500**
Vero: 1950.0 euroa

</sample-output>

</in-browser-programming-exercise>

<quiz id="97b08ca9-2b58-51d5-a457-2727652ed83e"></quiz>
