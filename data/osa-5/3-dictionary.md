---
path: '/osa-5/3-dictionary'
title: 'Lexikon'
hidden: false
---


<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* känner du till datatypen lexikon
* kan du använda lexikon med olika typer av nycklar och värden
* vet du hur man går igenom värden i ett lexikon
* har du koll på olika användningsområden för lexikon.

</text-box>

Listor kan vara händiga i flera situationer, men deras svaga punkt är att elementen hämtas med hjälp av index (0, 1, 2 o.s.v.). Om du vill hitta ett element i en lista måste du alltså veta dess index, eller alternativt gå igenom hela listan.

En ytterligare central datastruktur i Python är lexikon, som vi nu ska se på. I lexikon är elementen indexerade enligt nycklar. Varje nyckel har ett värde. Värden som lagrats i ett lexikon kan hämtas och ändras med hjälp av dess nyckel.

## Att använda lexikon

Det följande visar hur datastrukturen hos lexikon fungerar. Här är ett enkelt lexikon som innehåller översättningar från finska till svenska:

```python
sanakirja = {}

sanakirja["apina"] = "monkey"
sanakirja["banaani"] = "banana"
sanakirja["cembalo"] = "harpsichord"

print(len(sanakirja))
print(sanakirja)
print(sanakirja["apina"])
```

<sample-output>

3
{'apina': 'monkey', 'banaani': 'banana', 'cembalo': 'harpsichord'}
monkey

</sample-output>

Notationen `{}` skapar ett tomt lexikon dit vi kan lägga till element. Tre stycken nyckel-värdepar skapas: `"apina"` är knutet till `"apa"`, `"banaani"` till `"banan"` och `"cembalo`" till `"cembalo"`. Till slut skriver vi ut antalet nyckel-värdepar i lexikonet, lexikonets innehåll samt det värde som tillhör nyckeln `"apina"`.

Efter att vi har skapat ett lexikon kan vi också använda det med indata från användaren:

```python
sana = input("Anna sana: ")
if sana in sanakirja:
    print("Käännös:", sanakirja[sana])
else:
    print("Sanaa ei löytynyt")
```

Märk hur vi använder `in`-operatorn ovan. När vi använder operatorn för variabler med typen lexikon, kollar operatorn om den första operanden finns bland nycklarna i lexikonet. Så här kan det se ut när programmet körs:

<sample-output>

Anna sana: **apina**
Käännös: monkey

</sample-output>

<sample-output>

Anna sana: **pöllö**
Sanaa ei löytynyt

</sample-output>

## Vad kan lagras i ett lexikon?

Datatypen kallas lexikon, men det innebär inte att man bara skulle kunna lagra strängar där. I det här exemplet är nycklarna strängar men värdena är heltal:

```python
tulokset = {}
tulokset["Maija"] = 4
tulokset["Liisa"] = 5
tulokset["Kalle"] = 2
```

Här är nycklarna heltal medan värdena är listor:

```python
listat = {}
listat[5] = [1, 2, 3]
listat[42] = [5, 4, 5, 4, 5]
listat[100] = [5, 2, 3]
```

## Hur nycklar och värden fungerar

Varje nyckel kan endast förekomma en gång i ett lexikon. Om du lägger till ett nytt värde med en nyckel som redan finns i lexikonet, kommer det ursprungliga värdet kopplat till nyckeln att ersättas med det nya värdet:

```python
sanakirja["suuri"] = "big"
sanakirja["suuri"] = "large"
print(sanakirja["suuri"])
```

<sample-output>

large

</sample-output>

Alla nycklar i ett lexikon måste vara oföränderliga. Det betyder att en lista inte kan vara en nyckel, eftersom listor kan ändras på. Den här koden ger till exempel ett fel:

```python
sanakirja[[1, 2, 3]] = 5
```

<sample-output>

TypeError: unhashable type: 'list'

</sample-output>

<text-box variant="hint" name="Hashtabell">

Märk ordet "unhashable" i felmeddelandet ovan. Det här är en hänvisning till de inte strukturerna i ett lexikon. Python lagrar innehållet i ett lexikon i en hashtabell. Varje nyckel har ett hashvärde som indikerar var nyckeln finns lagrad i minnet. Felmeddelandet ovan indikerar att en lista inte kan förvandlas till ett hashvärde, och kan därmed inte användas som en nyckel i lexikonet.

Kursen Datastrukturer och algoritmer ger en större insikt i hashtabeller.

</text-box>

Till skillnad från nycklar, kan värden i ett lexikon ändra och därmed kan vilken som helst typ av data lagras som ett värde. Ett och samma värde kan också vara kopplat till flera nycklar i samma lexikon.

<programming-exercise name='Kertaa kymmenen' tmcname='osa05-10b_kertaa_kymmenen'>

Tee funktio `kertaa_kymmenen(alku: int, loppu: int)`, joka muodostaa ja palauttaa uuden sanakirjan. Sanakirjassa on avaimina luvut väliltä `alku`..`loppu`.

Jokaisen avaimen arvona on avain kerrottuna kymmenellä.

Esimerkiksi:

```python
d = kertaa_kymmenen(3, 6)
print(d)
```

<sample-output>

{3: 30, 4: 40, 5: 50, 6: 60}

</sample-output>

</programming-exercise>

<programming-exercise name='Kertomat' tmcname='osa05-11_kertomat'>

Tee funktio `kertomat(n: int)`, joka palauttaa lukujen 1..`n` kertomat sanakirjassa siten, että luku on avain ja luvun kertoma arvo, johon avain viittaa.

Muistutuksena: luvun `n` kertoma `n`! lasketaan kertomalla luku kaikilla itseään pienemmillä positiivisilla kokonaisluvuilla. Luvun 4 kertoma on siis 4 * 3 * 2 * 1 = 24.

Esimerkki käytöstä:

```python
k = kertomat(5)
print(k[1])
print(k[3])
print(k[5])
```

<sample-output>

1
6
120

</sample-output>

</programming-exercise>

## Gå igenom ett lexikon

Den bekanta `for element in samling` -loopen kan också användas för att gå igenom ett lexikon. När det används direkt hos ett lexikon kommer loopen att en för en gå igenom nycklarna i lexikonet. I följande exempel skrivs varje nyckel och respektive värde:

```python
sanakirja = {}

sanakirja["apina"] = "monkey"
sanakirja["banaani"] = "banana"
sanakirja["cembalo"] = "harpsichord"

for avain in sanakirja:
    print("avain:", avain)
    print("arvo:", sanakirja[avain])
```

<sample-output>

avain: apina
arvo: monkey
avain: banaani
arvo: banana
avain: cembalo
arvo: harpsichord

</sample-output>

Ibland behöver du gå igenom allt innehåll i ett lexikon. Då kan du använda metoden `items` som returnerar alla nycklar och värden, ett par i sänder:

```python

for avain, arvo in sanakirja.items():
    print("avain:", avain)
    print("arvo:", arvo)
```

I exemplen ovan märkte du kanske att nycklar behandlas i den ordning som de lagts till i lexikonet. Eftersom nycklarna behandlas enligt deras hashvärden, borde ordningen inte ha någon skillnad i programmen. I flera äldre versioner av Python är det dessutom inte garanterat att ordningen är den samma som nycklarna lagts till.

## Några mer avancerade sätt att använda lexikon

Låt oss kika på en lista med ord:

```python
sanalista = [
  "banaani", "maito", "olut", "juusto", "piimä", "mehu", "makkara",
  "tomaatti", "kurkku", "voi", "margariini", "juusto", "makkara",
  "olut", "piimä", "piimä", "voi", "olut", "suklaa"
]
```

Vi skulle vilja analysera den här ordlistan på olika sätt. Vi är till exempel intresserade av hur många gånger de olika orden förekommer i listan.

Ett lexikon fungera väl för att hålla reda på sådan här information. I exemplet nedan går vi igenom orden i listan. Vi använder sedan orden som nycklar i ett lexikon som vi skapat, så att värdet som är kopplat till varje nyckel indikerar hur många gånger det specifika ordet har förekommit:

```python
def lukumaarat(lista):
    sanat = {}
    for sana in lista:
        # jos sana ei ole vielä tullut vastaan, alusta avaimen arvo
        if sana not in sanat:
            sanat[sana] = 0
        # kasvata sanan esiintymislukumäärää
        sanat[sana] += 1
    return sanat

# kutsutaan funktiota
print(lukumaarat(sanalista))
```

Programmet skriver ut det följande:

<sample-output>

{'banaani': 1, 'maito': 1, 'olut': 3, 'juusto': 2, 'piimä': 3, 'mehu': 1, 'makkara': 2, 'tomaatti': 1, 'kurkku': 1, 'voi': 2, 'margariini': 1, 'suklaa': 1}

</sample-output>

Om vi då skulle vela ordna orden enligt den första bokstaven i varje ord? Här kunde vi också kunna använda lexikon:

```python
def alkukirjaimen_mukaan(lista):
    ryhmat = {}
    for sana in lista:
        alkukirjain = sana[0]
        # alusta alkukirjaimeen liittyvä lista kun kirjain tulee vastaan 1. kerran
        if alkukirjain not in ryhmat:
            ryhmat[alkukirjain] = []
        # lisää sana alkukirjainta vastaavalle listalle
        ryhmat[alkukirjain].append(sana)
    return ryhmat

ryhmat = alkukirjaimen_mukaan(sanalista)

for avain, arvo in ryhmat.items():
    print(f"kirjaimella {avain} alkavat sanat: ")
    for sana in arvo:
        print(sana)
```

Funktionens struktur liknar mycket den som finns i det tidigare exemplet, men den här gången är värden lagrade i form av listor. Programmet skriver ut det följande:

<sample-output>

kirjaimella b alkavat sanat:
  banaani
kirjaimella m alkavat sanat:
  maito
  mehu
  makkara
  margariini
  makkara
kirjaimella o alkavat sanat:
  olut
  olut
  olut
kirjaimella j alkavat sanat:
  juusto
  juusto
kirjaimella p alkavat sanat:
  piimä
  piimä
  piimä
kirjaimella t alkavat sanat:
  tomaatti
kirjaimella k alkavat sanat:
  kurkku
kirjaimella v alkavat sanat:
  voi
  voi
kirjaimella s alkavat sanat:
  suklaa

</sample-output>

<programming-exercise name='Histogrammi' tmcname='osa05-12_histogrammi'>

Tee funktio `histogrammi`, joka saa parametrina merkkijonon ja tulostaa merkkijonon eri kirjainten lukumäärää kuvaavan histogrammin, jossa kirjaimen jokaista esiintymää kohti tulostuu yksi tähti kirjaimen riville.

Esimerkiksi kutsuttaessa `histogrammi("abba")` tulostus on:

<sample-output>

<pre>
a **
b **
</pre>

</sample-output>

Vastaavasti kutsuttaessa `histogrammi("saippuakauppias")` tulostus on:

<sample-output>

<pre>
s **
a ****
i **
p ****
u **
k *
</pre>

</sample-output>

</programming-exercise>

<programming-exercise name='Puhelinluettelo, versio 1' tmcname='osa05-13_puhelinluettelo_versio1'>

Tee puhelinluettelo, joka toimii seuraavasti:

<sample-output>

komento (1 hae, 2 lisää, 3 lopeta): **2**
nimi: **pekka**
numero: **040-5466745**
ok!
komento (1 hae, 2 lisää, 3 lopeta): **2**
nimi: **emilia**
numero: **045-1212344**
ok!
komento (1 hae, 2 lisää, 3 lopeta): **1**
nimi: **pekka**
040-5466745
komento (1 hae, 2 lisää, 3 lopeta): **1**
nimi: **maija**
ei numeroa
komento (1 hae, 2 lisää, 3 lopeta): **2**
nimi: **pekka**
numero: **09-22223333**
ok!
komento (1 hae, 2 lisää, 3 lopeta): **1**
nimi: **pekka**
09-22223333
komento (1 hae, 2 lisää, 3 lopeta): **3**
lopetetaan...

</sample-output>

Huomaa, että jokaiseen nimeen voi liittyä vain yksi puhelinnumero. Jos samalle henkilölle lisätään uusi numero, se korvaa aiemmin lisätyn numeron.

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!

</programming-exercise>

<programming-exercise name='Puhelinluettelo, versio 2' tmcname='osa05-14_puhelinluettelo_versio2'>

Tee puhelinluettelosta paranneltu versio, missä jokaisella henkilöllä voi olla useampia puhelinnumeroita. Ohjelma toimii kuten edellisessä tehtävässä, mutta nyt se listaa jokaisen numeron:

<sample-output>

komento (1 hae, 2 lisää, 3 lopeta): **2**
nimi: **pekka**
numero: **040-5466745**
ok!
komento (1 hae, 2 lisää, 3 lopeta): **2**
nimi: **emilia**
numero: **045-1212344**
ok!
komento (1 hae, 2 lisää, 3 lopeta): **1**
nimi: **pekka**
040-5466745
komento (1 hae, 2 lisää, 3 lopeta): **1**
nimi: **maija**
ei numeroa
komento (1 hae, 2 lisää, 3 lopeta): **2**
nimi: **pekka**
numero: **09-22223333**
ok!
komento (1 hae, 2 lisää, 3 lopeta): **1**
nimi: **pekka**
040-5466745
09-22223333
komento (1 hae, 2 lisää, 3 lopeta): **3**
lopetetaan...

</programming-exercise>

## Att ta bort nycklar och värden från ett lexikon

Det är naturligtvis möjligt att ta bort nyckel-värdepar från ett lexikon. Det finns två sätt att göra det här. Det första sättet är att använda kommandot `del`:

```python
henkilokunta = {"Antti": "lehtori", "Emilia": "professori", "Arto": "Lehtori"}
del henkilokunta["Arto"]
print(henkilokunta)
```

<sample-output>

{'Antti': 'lehtori', 'Emilia': 'professori'}

</sample-output>

Om du försöker använda `del`-kommandot för att ta bort en nyckel som inte finns i listan, kommer ett fel att uppstå:

```python
henkilokunta = {"Antti": "lehtori", "Emilia": "professori", "Arto": "lehtori"}
del henkilokunta["Jukka"]
```

<sample-output>

<pre>
>>> del henkilokunta["Jukka"]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'Jukka'
</pre>

</sample-output>

Därmed lönar det sig att kolla om en nyckel existerar före du försöker avlägsna den från listan:

```python
henkilokunta = {"Antti": "lehtori", "Emilia": "professori", "Arto": "lehtori"}
if "Jukka" in henkilokunta:
  del henkilokunta["Jukka"]
  print("Poistettiin")
else:
  print("Poistettavaa henkilöä ei löytynyt henkilökunnasta")
```

Ett annat sätt att ta bort element från listan är att använda metoden `pop`:

```python
henkilokunta = {"Antti": "lehtori", "Emilia": "professori", "Arto": "lehtori"}
poistettu = henkilokunta.pop("Arto")
print(henkilokunta)
print("Poistettiin", poistettu)
```

<sample-output>

{'Antti': 'lehtori', 'Emilia': 'professori'}
Poistettiin lehtori

</sample-output>

Metoden `pop` returnerar också värdet på elementet som togs bort.

Metoden `pop` kommer också i vanliga fall att ge ett fel om nyckeln som man försöker ta bort saknas i lexikonet. Det här kan man dock undvika genom att som ett andra argument ge till funktionen ett return-värde som funktionen kan returnera då en nyckel saknas. Värdet `None` kan till exempel användas här:

```python
henkilokunta = {"Antti": "lehtori", "Emilia": "professori", "Arto": "lehtori"}
poistettu = henkilokunta.pop("Jukka", None)
if poistettu == None:
  print("Poistettavaa henkilöä ei löytynyt henkilökunnasta")
else:
  print("Poistettiin", poistettu)
```

<sample-output>

Poistettavaa henkilöä ei löytynyt henkilökunnasta

</sample-output>

Obs! Om du vill tömma ett lexikon och försöker göra det med en for-loop…

```python
henkilokunta = {"Antti": "lehtori", "Emilia": "professori", "Arto": "lehtori"}
for avain in henkilokunta:
  del henkilokunta[avain]
```

…kommer du att få ett felmeddelande:

<sample-output>

RuntimeError: dictionary changed size during iteration

</sample-output>

När man går igenom en samling med en for-loop, kan man inte ändra på samlingens innehåll så länge for-loopen är igång.

Lyckligtvis har lexikon en inbyggd metod som kan användas istället:

```python
henkilokunta.clear()
```

<programming-exercise name='Sanakirjan kääntö' tmcname='osa05-15_sanakirjan_kaanto'>

Kirjoita funktio `kaanna(sanakirja: dict)`, joka saa parametrikseen sanakirjan ja kääntää sen niin, että arvoista tulee avaimia ja päinvastoin.

Esimerkki funktion käytöstä:

```python
s = {1: "eka", 2: "toka", 3: "kolmas", 4: "neljas"}
kaanna(s)
print(s)
```

<sample-output>

{"eka": 1, "toka": 2, "kolmas": 3, "neljas": 4}

</sample-output>

**Huomaa**, että [tämä](/osa-5/2-viittaukset#parametrina-olevan-listan-muokkaaminen) pitää paikkansa myös parametrina oleville sanakirjoille!

Jos kohtaat tehtävässä ongelmia, katso [visualisaattorilla](http://www.pythontutor.com/visualize.html#mode=edit) mitä koodisi tekee.

</programming-exercise>

<programming-exercise name='Luvut sanoina' tmcname='osa05-16_luvut_sanoina'>

Kirjoita funktio `lukukirja()`, joka palauttaa uuden sanakirjan. Palautettu rakenne sisältää avaimina luvut nollasta 99:ään. Sanakirjan arvoina ovat luvut kirjaimin kirjoitettuna. Katso esimerkkiä alla:

```python
luvut = lukukirja()
print(luvut[2])
print(luvut[11])
print(luvut[45])
print(luvut[99])
print(luvut[0])
```

<sample-output>

kaksi
yksitoista
neljäkymmentäviisi
yhdensänkymmentäyhdeksän
nolla

</sample-output>

HUOM! Älä muodosta jokaista lukusanaa yksitellen, vaan mieti, miten voisit hyödyntää silmukoita ja sanakirjaa jotenkin ratkaisussasi!

</programming-exercise>

## Använda lexikon för strukturerade data

Lexikon fungerar bra för att strukturera data. Följande kodsnutt skapar ett lexikon som innehåller information om en person:

```python
henkilo = {"nimi": "Pirjo Python", "pituus": 154, "paino": 61, "ikä:" 44}
```

Här har vi alltså en person som heter Peppa Python. Hennes längd är 154, vikt 61 och ålder 44. Samma information kunde också lagras i skilda variabler:


```python
nimi = "Pirjo Python"
pituus = 154
paino = 61
ika = 44
```

Fördelen med lexikon är att det är en samling. Det samlar relaterade data under en variabel och det är enkelt att komma åt den information man är ute efter. Samma funktionalitet erbjuds också av listor:

```python
henkilo = ["Pirjo Python", 153, 61, 44]
```

Men med listor måste programmeraren minnas vilket index används för vilken information. Det finns inget som indikerar att `person[2]` innehåller vikten och `person[3]` åldern hos en person. När man använder lexikon, undviker man det här problemet eftersom all information finns lagrad under namngivna nycklar.

Om vi antar att det finns flera personer som definierats i samma format, kan vi komma åt deras information på följande sätt:

```python
henkilo1 = {"nimi": "Pirjo Python", "pituus": 154, "paino": 61, "ikä": 44}
henkilo2 = {"nimi": "Pekka Pythonen", "pituus": 174, "paino": 103, "ikä": 31}
henkilo3 = {"nimi": "Pedro Python", "pituus": 191, "paino": 71, "ikä": 14}

henkilot = [henkilo1, henkilo2, henkilo3]

for henkilo in henkilot:
    print(henkilo["nimi"])

yhteispituus = 0
for henkilo in henkilot:
    yhteispituus += henkilo["pituus"]

print("Keskipituus on", yhteispituus / len(henkilot))
```

<sample-output>

Pirjo Python
Pekka Pythonen
Pedro Python
Keskipituus on 173.0

</sample-output>

<programming-exercise name='Elokuvarekisteri' tmcname='osa05-17_elokuvarekisteri'>

Kirjoita funktio `lisaa_elokuva(rekisteri: list, nimi: str, ohjaaja: str, vuosi: int, pituus: int)`, joka lisää yhden elokuvaolion elokuvarekisteriin.

Rekisteri on toteutettu listana, ja jokainen listan alkio on yksi sanakirja. Sanakirjassa on seuraavat avaimet:

* nimi
* ohjaaja
* vuosi
* pituus

Arvot tulevat metodin parametreina.

Esimerkki:

```python
rekisteri = []
lisaa_elokuva(rekisteri, "Pythonin viemää", "Pekka Python", 2017, 116)
lisaa_elokuva(rekisteri, "Python lentokoneessa", "Renny Pytholin", 2001, 94)
print(rekisteri)
```

<sample-output>

[{"nimi": "Pythonin viemää", "ohjaaja": "Pekka Python", "vuosi": 2017, "pituus": 116}, {"nimi": "Python lentokoneessa", "ohjaaja": "Renny Pytholin", "vuosi": 2001, "pituus": 94}]

</sample-output>

</programming-exercise>

<programming-exercise name='Etsi elokuvat' tmcname='osa05-17b_etsi_elokuvat'>

Kirjoita funktio `etsi_elokuvat(rekisteri: list, hakusana: str)`, joka käsittelee edellisessä tehtävässä luotua elokuvarekisteriä. Funktio muodostaa uuden listan, jolle kopioidaan rekisteristä ne elokuvat, joiden nimestä löytyy hakusana. Pienet ja isot kirjaimet eivät merkitse haussa, joten hakusanalla `paj` pitää löytyä sekä elokuva `Tappajahai` että elokuva `Pajatoiminnan historia`.

Esimerkki:

```python
rekisteri = [{"nimi": "Pythonin viemää", "ohjaaja": "Pekka Python", "vuosi": 2017, "pituus": 116},
{"nimi": "Python lentokoneessa", "ohjaaja": "Renny Pythonen", "vuosi": 2001, "pituus": 94},
{"nimi": "Koodaajien yö", "ohjaaja": "M. Night Python", "vuosi": 2011, "pituus": 101}]

lista = etsi_elokuvat(rekisteri, "python")
print(lista)
```

<sample-output>

[{"nimi": "Pythonin viemää", "ohjaaja": "Pekka Python", "vuosi": 2017, "pituus": 116}, {"nimi": "Python lentokoneessa", "ohjaaja": "Renny Pythonen", "vuosi": 2001, "pituus": 94}]

</sample-output>

</programming-exercise>

<quiz id="87776053-a318-5e02-a931-2c68cdac8e99"></quiz>
