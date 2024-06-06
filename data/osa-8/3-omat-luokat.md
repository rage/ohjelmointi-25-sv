---
path: '/osa-8/3-omat-luokat'
title: 'Egna klasser'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Vet du hur du definierar dina egna klasser
- Kommer du att kunna skapa objekt baserade på klasser som du själv har definierat
- Vet du hur man skriver en konstruktor
- Är du bekant med parameternamnet `self`
- Vet du vad attribut är och hur de används

</text-box>

En klass definieras med nyckelordet `class`. Syntaxen ser ut enligt följande:

```python
class LuokanNimi:
    # Luokan toteutus
```

Klasser namnges vanligtvis med kamelnotation. Detta innebär att alla ord i klassnamnet skrivs tillsammans, utan mellanslag, och att varje ord börjar med stor bokstav. Följande exempel på klassnamn följer denna konvention:

* `Veckodag`
* `Bankkonto`
* `BibliotekDatabas`
* `PythonKursBetyg`

En enskild klassdefinition bör representera en enskild helhet, vars innehåll bör vara sammanlänkat på något sätt. I mer komplicerade program kan klasser innehålla medlemmar av andra klasser. Till exempel kan klassen `Kurs` innehålla objekt av klasserna `Lektion`, `ÖvningsTillfälle` osv.

Låt oss ta en titt på ett skelett av en klassdefinition. Funktionerna saknas fortfarande vid denna tidpunkt.

```python
class Pankkitili:
    pass
```

Kodstycket ovan talar om för Python att vi här definierar en klass med namnet `Bankkonto`. Klassen innehåller ingen funktionalitet ännu, men vi kan fortfarande skapa ett objekt baserat på klassen.

Låt oss titta på ett program där två variabler läggs till ett `Bankkonto`-objekt: `saldo` och `ägare`. Alla variabler som är kopplade till ett objekt kallas dess attribut, eller mer specifikt, dataattribut, eller ibland instansvariabler.

De attribut som är kopplade till ett objekt kan nås via objektet:

```python
class Pankkitili:
    pass

pekan_tili = Pankkitili()
pekan_tili.omistaja = "Pekka Python"
pekan_tili.saldo = 5.0

print(pekan_tili.omistaja)
print(pekan_tili.saldo)
```

<sample-output>

Pekka Python
5.0

</sample-output>

Dataattributen är endast tillgängliga via det objekt som de är kopplade till. Varje Bankkonto-objekt som skapas baserat på Bankkonto-klassen har sina egna värden kopplade till dataattributen. Dessa värden kan nås genom att hänvisa till objektet i fråga:

```python
tili = Pankkitili()
tili.saldo = 155.50

print(tili.saldo) # Viittaa tilin attribuuttiin saldo
print(saldo) # TÄSTÄ TULEE VIRHE, koska oliomuuttuja ei ole mukana!
```

## Att lägga till en konstruktor

I exemplet ovan såg vi att en ny instans av en klass kan skapas genom att anropa klassens konstruktormetod på följande sätt: `KlassensNamn()`. Ovan kopplade vi sedan dataattribut till objektet separat, men det är ofta bekvämare att skicka dessa initiala värden för attribut direkt när objektet skapas. I exemplet ovan hade vi först ett Bankkonto-objekt utan dessa attribut, och attributen existerade först efter att de uttryckligen hade deklarerats.


Att deklarera attribut utanför konstruktorn leder till en situation där olika instanser av samma klass kan ha olika attribut. Följande kod ger ett fel eftersom vi nu har ett annat `Bankkonto-objekt`, `paulas_konto`, som inte innehåller samma attribut:

```python
class Pankkitili:
    pass

pekan_tili = Pankkitili()
pekan_tili.omistaja = "Pekka"
pekan_tili.saldo = 1400

pirjon_tili = Pankkitili()
pirjon_tili.omistaja = "Pirjo"

print(pekan_tili.saldo)
print(pirjon_tili.saldo) # TÄSTÄ TULEE VIRHE
```

Så istället för att deklarera attribut efter att varje instans av klassen har skapats, är det oftast en bättre idé att initialisera attributens värden när klasskonstruktorn anropas. Eftersom klassdefinitionen Bankkonto för närvarande bara är ett skelett, antas konstruktormetoden implicit av Python-tolkaren, men det är möjligt att definiera egna konstruktormetoder, och det är precis vad vi kommer att göra nu.

En konstruktormetod är en metoddeklaration med det speciella namnet `__init__`, som vanligtvis inkluderas i början av en klassdefinition.

Låt oss ta en titt på en `Bankkonto`-klass med en konstruktormetod tillagd:

```python
class Pankkitili:

    # Konstruktori
    def __init__(self, saldo: float, omistaja: str):
        self.saldo = saldo
        self.omistaja = omistaja
```

Namnet på konstruktorsmetoden är alltid `__init__`. Lägg märke till de två understrecken på båda sidorna av ordet `init`.

Den första parametern i en konstruktorsdefinition heter alltid `self`. Detta refererar till själva objektet och är nödvändigt för att deklarera alla attribut som är knutna till objektet. Tilldelningen

`self.saldo = saldo`

tilldelar objektets saldoattribut den balans som mottagits som argument. Det är vanligt att använda samma variabelnamn för parametrarna och dataattributen som definieras i en konstruktor, men variabelnamnen `self.saldo` och `saldo` ovan hänvisar till två olika variabler:

* Variabeln `self.saldo` är ett attribut för objektet. Varje Bankkonto-objekt har sitt eget saldo.

* Variabeln `saldo` är en parameter i konstruktorsmetoden `__init__`. Dess värde sätts till det värde som skickas som argument till metoden när konstruktorn kallas (dvs. när en ny insctance av klassen skapas).

Nu när vi har definierat parametrarna för konstruktorsmetoden kan vi skicka de önskade initiala värdena för dataattributen som argument när ett nytt objekt skapas:

```python
class Pankkitili:

    # Konstruktori
    def __init__(self, saldo: float, omistaja: str):
        self.saldo = saldo
        self.omistaja = omistaja

# Parametrille self ei anneta arvoa, vaan Python antaa sen
# automaattisesti
pekan_tili = Pankkitili(100, "Pekka Python")
pirjon_tili = Pankkitili(20000, "Pirjo Pythonen")

print(pekan_tili.saldo)
print(pirjon_tili.saldo)
```

<sample-output>

100
20000

</sample-output>

Det är nu mycket enklare att arbeta med Bankkonto-objekten, eftersom värdena kan skickas när objektet skapas, och de två separata instanserna kan hanteras på ett mer förutsägbart och enhetligt sätt. Att deklarera dataattribut i konstruktorn säkerställer också att attributen verkligen deklareras, och att de önskade initiala värdena alltid ges av programmeraren som använder klassen.

Det är fortfarande möjligt att ändra de initiala värdena för dataattributen senare i programmet:

```python
class Pankkitili:

    # Konstruktori
    def __init__(self, saldo: float, omistaja: str):
        self.saldo = saldo
        self.omistaja = omistaja

pekan_tili = Pankkitili(100, "Pekka Python")
print(pekan_tili.saldo)

# Saldoksi 1500
pekan_tili.saldo = 1500
print(pekan_tili.saldo)

# Lisätään saldoon 2000
pekan_tili.saldo += 2000
print(pekan_tili.saldo)
```

<sample-output>

100
1500
3500

</sample-output>

Låt oss titta på ett annat exempel på klasser och objekt. Vi ska skriva en klass som modellerar en enstaka dragning av lotterinummer:

```python
from datetime import date

class LottoKierros:

    def __init__(self, viikko: int, pvm: date, numerot: list):
        self.viikko = viikko
        self.pvm = pvm
        self.numerot = numerot


# Luodaan uusi lottokierros
kierros1 = LottoKierros(1, date(2021, 1, 2), [1,4,8,12,13,14,33])

# Tulostetaan tiedot
print(kierros1.viikko)
print(kierros1.pvm)

for numero in kierros1.numerot:
    print(numero)
```

<sample-output>

1
2021-01-02
1
4
8
12
13
14
33

</sample-output>

Som du kan se ovan kan attributerna vara av  vilken sort som helst. Här har varje LotteriDragnings objekt attributer av typerna `list` och `date`.


<programming-exercise name='Kirja' tmcname='osa08-06_kirja'>

Tee luokka `Kirja`, jolla on attribuutteina muuttujat `nimi`, `kirjoittaja`, `genre` ja `kirjoitusvuosi` sekä konstruktori, joka alustaa muuttujat.

Luokkaa käytetään seuraavasti:

```python
python = Kirja("Fluent Python", "Luciano Ramalho", "ohjelmointi", 2015)
everest = Kirja("Huipulta huipulle", "Carina Räihä", "elämänkerta", 2010)

print(f"{python.kirjoittaja}: {python.nimi} ({python.kirjoitusvuosi})")
print(f"Kirjan {everest.nimi} genre on {everest.genre}")
```

<sample-output>

Luciano Ramalho: Fluent Python (2015)
Kirjan Huipulta huipulle genre on elämänkerta

</sample-output>

</programming-exercise>

<programming-exercise name='Kirjoita luokat' tmcname='osa08-07_kirjoita_luokat'>

Kirjoita alla pyydetyt luokat. Jokaisen luokan alle on kuvattu attribuuttien nimet ja tyypit.

Kirjoita jokaiselle luokalle myös konstruktori, jossa attribuutit annetaan siinä järjestyksessä kuin ne on kuvauksessa annettu.

1. Luokka Muistilista
- attribuutti otsikko (merkkijono)
- attribuutti merkinnat (lista)

2. Luokka Asiakas
- attribuutti tunniste (merkkijono)
- attribuutti saldo (desimaaliluku)
- attribuutti alennusprosentti (kokonaisluku)

3. Luokka Kaapeli
- attribuutti malli (merkkijono)
- attribuutti pituus (desimaaliluku)
- attribuutti maksiminopeus (kokonaisluku)
- attribuutti kaksisuuntainen (totuusarvo)

</programming-exercise>

## Användning av objekt från egengjorda klasser

Objekt som bildas från dina egna klassdefinitioner skiljer sig inte från andra Python-objekt. De kan skickas som argument och returnera värden precis som alla andra objekt. Vi kan till exempel skriva hjälpfunktioner för att arbeta med bankkonton: 

```python
# funktio luo uuden tiliolion ja palauttaa sen
def avaa_tili(nimi: str):
    uusi_tili =  Pankkitili(0, nimi)
    return uusi_tili

# funktio asettaa parametrina saamansa rahasumman parametrina olevalle tilille
def laita_rahaa_tilille(tili: Pankkitili, summa: int):
    tili.saldo += summa

pekan_tili = avaa_tili("Pekka Python")
print(pekan_tili.saldo)

laita_rahaa_tilille(pekan_tili, 500)

print(pekan_tili.saldo)
```

<sample-output>

0
500

</sample-output>

<programming-exercise name='Muodosta lemmikki' tmcname='osa08-07b_muodosta_lemmikki'>

Määrittele luokka `Lemmikki`. Luokalla on konstruktori, jossa annetaan arvot attribuuteille `nimi`, `laji` ja `syntymavuosi` tässä järjestyksessä.

Kirjoita sitten luokan ulkopuolelle funktio `uusi_lemmikki(nimi: str, laji: str, syntymavuosi: int)`, joka luo ja palauttaa uuden `Lemmikki`-tyyppisen (eli `Lemmikki`-luokkaa vastaavan) olion.

Esimerkki funktion kutsumisesta:

```python
musti = uusi_lemmikki("Musti", "koira", 2017)
print(musti.nimi)
print(musti.laji)
print(musti.syntymavuosi)
```

<sample-output>

Musti
koira
2017

</sample-output>

</programming-exercise>

<programming-exercise name='Vanhempi kirja' tmcname='osa08-08_vanhempi_kirja'>

Tee funktio `vanhempi_kirja(kirja1: Kirja, kirja2: Kirja)`, joka saa parametriksi kaksi `Kirja`-oliota. Funktio kertoo, kumpi kirjoista on vanhempi.

Funktiota käytetään seuraavasti:

```python
python = Kirja("Fluent Python", "Luciano Ramalho", "ohjelmointi", 2015)
everest = Kirja("Huipulta huipulle", "Carina Räihä", "elämänkerta", 2010)
norma = Kirja("Norma", "Sofi Oksanen", "rikos", 2015)

vanhempi_kirja(python, everest)
vanhempi_kirja(python, norma)
```

<sample-output>

Huipulta huipulle on vanhempi, se kirjoitettiin 2010
Fluent Python ja Norma kirjoitettiin 2015

</sample-output>

</programming-exercise>

<programming-exercise name='Genren kirjat' tmcname='osa08-09_genren_kirjat'>

Tee funktio `genren_kirjat(kirjat: list, genre: str)`, joka saa parametriksi listan `Kirja`-olioita sekä genren kertovan merkkijonon.

Funktio _palauttaa_ uuden listan, jolle se laittaa parametrina olevista kirjoista ne, joilla on haluttu genre.

Funktiota käytetään seuraavasti:

```python
python = Kirja("Fluent Python", "Luciano Ramalho", "ohjelmointi", 2015)
everest = Kirja("Huipulta huipulle", "Carina Räihä", "elämänkerta", 2010)
norma = Kirja("Norma", "Sofi Oksanen", "rikos", 2015)

kirjat = [python, everest, norma, Kirja("Lumiukko", "Jo Nesbø", "rikos", 2007)]

print("rikoskirjoja ovat")
for kirja in genren_kirjat(kirjat, "rikos"):
    print(f"{kirja.kirjoittaja}: {kirja.nimi}")
```

<sample-output>

rikoskirjoja ovat
Sofi Oksanen: Norma
Jo Nesbø: Lumiukko

</sample-output>

</programming-exercise>
