---
path: '/osa-8/3-egna-klasser'
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
class KlassNamn:
    # Klassdefinitionen
```

Klasser namnges vanligtvis med kamelnotation. Detta innebär att alla ord i klassnamnet skrivs tillsammans, utan mellanslag, och att varje ord börjar med stor bokstav. Följande exempel på klassnamn följer denna konvention:

* `Veckodag`
* `Bankkonto`
* `BiblioteksDatabas`
* `PythonKursBetyg`

En enskild klassdefinition bör representera en enskild helhet, vars innehåll bör vara sammanlänkat på något sätt. I mer komplicerade program kan klasser innehålla medlemmar av andra klasser. Till exempel kan klassen `Kurs` innehålla objekt av klasserna `Lektion`, `ÖvningsTillfälle` osv.

Låt oss ta en titt på strukturen för en klassdefinition. 

```python
class Bankkonto:
    pass
```

Koden ovan talar om för Python att vi här definierar en klass med namnet `Bankkonto`. Klassen innehåller ingen funktionalitet ännu, men vi kan redan skapa ett objekt baserat på klassen.

Låt oss titta på ett program där två variabler läggs till ett `Bankkonto`-objekt: `saldo` och `ägare`. Alla variabler som är kopplade till ett objekt kallas dess _attribut_, eller mer specifikt, _dataattribut_, eller ibland _instansvariabler_.

De attribut som är kopplade till ett objekt kan nås via objektet:

```python
class Bankkonto:
    pass

peters_konto = Bankkonto()
peters_konto.agare = "Peter Python"
peters_konto.saldo = 5.0

print(peters_konto.agare)
print(peters_konto.saldo)
```

<sample-output>

Peter Python
5.0

</sample-output>

Dataattributen är endast tillgängliga via det objekt som de är kopplade till. Varje Bankkonto-objekt som skapas baserat på Bankkonto-klassen har sina egna värden kopplade till dataattributen. Dessa värden kan nås genom att hänvisa till objektet i fråga:

```python
konto = Bankkonto()
konto.saldo = 155.50

print(konto.saldo) # Detta refererar till dataattributen saldo, som är kopplad till kontot
print(saldo) # DETTA ORSAKAR ETT FEL, eftersom det inte finns någon sådan oberoende variabel, och objektreferensen saknas
```

## Att lägga till en konstruktor

I exemplet ovan såg vi att en ny instans av en klass kan skapas genom att anropa klassens konstruktormetod på följande sätt: `KlassensNamn()`. Ovan kopplade vi sedan dataattribut till objektet separat, men det är ofta bekvämare att skicka dessa initiala värden för attribut direkt när objektet skapas. I exemplet ovan hade vi först ett Bankkonto-objekt utan dessa attribut, och attributen existerade först efter att de uttryckligen hade deklarerats.


Att deklarera attribut utanför konstruktorn leder till en situation där olika instanser av samma klass kan ha olika attribut. Följande kod ger ett fel eftersom vi nu har ett annat `Bankkonto-objekt`, `pernillas_konto`, som inte innehåller samma attribut:

```python
class Bankkonto:
    pass

peters_konto = Bankkonto()
peters_konto.agare = "Peter"
peters_konto.saldo = 1400

pernillas_konto = Bankkonto()
pernillas_konto.agare = "Pernilla"

print(peters_konto.saldo)
print(pernillas_konto.saldo) # DETTA ORSAKAR ETT FEL
```

Istället för att deklarera attribut efter att varje instans av klassen har skapats, är det därför oftast en bättre idé att initialisera attributens värden när konstruktorn anropas. Eftersom klassdefinitionen Bankkonto för närvarande bara är en ram, antas konstruktormetoden implicit av Python-tolkaren, men det är möjligt att definiera egna konstruktormetoder, och det är precis vad vi kommer att göra nu.

En konstruktormetod är en metoddeklaration med det speciella namnet `__init__`, som vanligtvis inkluderas i början av en klassdefinition.

Låt oss ta en titt på en `Bankkonto`-klass där vi nu även definierat en konstruktor:

```python
class Bankkonto:

    # Konstruktorn
    def __init__(self, saldo: float, agare: str):
        self.saldo = saldo
        self.agare = agare
```

Namnet på konstruktorn är alltid `__init__`. Lägg märke till de två understrecken på båda sidorna av ordet `init`.

Den första parametern i en konstruktorsdefinition heter alltid `self`. Detta refererar till själva objektet och är nödvändigt för att deklarera alla attribut som är knutna till objektet. Tilldelningen

`self.saldo = saldo`

tilldelar objektets saldoattribut det sald som tagits emot som argument. Det är vanligt att använda samma variabelnamn för parametrarna och dataattributen som definieras i en konstruktor, men variabelnamnen `self.saldo` och `saldo` ovan hänvisar till två olika variabler:

* Variabeln `self.saldo` är ett attribut för objektet. Varje Bankkonto-objekt har sitt eget saldo.

* Variabeln `saldo` är en parameter i konstruktorsmetoden `__init__`. Dess värde sätts till det värde som skickas som argument när konstruktorn anropas (dvs. när en ny instans av klassen skapas).

När vi har definierat parametrarna för konstruktorsmetoden kan vi skicka de önskade initiala värdena för dataattributen som argument när ett nytt objekt skapas:

```python
class Bankkonto:

    # Konstruktorn
    def __init__(self, saldo: float, agare: str):
        self.saldo = saldo
        self.agare = agare

# Parametern self ges inget värde, utan Python ger ett sådant automatiskt
peters_konto = Bankkonto(100, "Peter Python")
pernillas_konto = Bankkonto(20000, "Pernilla Pythonson")

print(peters_konto.saldo)
print(pernillas_konto.saldo)
```

<sample-output>

100
20000

</sample-output>

Det är nu mycket enklare att arbeta med Bankkonto-objekten, eftersom värdena kan skickas när objektet skapas, och de två separata instanserna kan hanteras på ett mer förutsägbart och enhetligt sätt. Att deklarera dataattribut i konstruktorn säkerställer också att attributen verkligen deklareras, och att de önskade initiala värdena alltid ges av programmeraren som använder klassen.

Det är fortfarande möjligt att ändra de initiala värdena för dataattributen senare i programmet:

```python
class Bankkonto:

    # Konstruktorn
    def __init__(self, saldo: float, agare: str):
        self.saldo = saldo
        self.agare = agare

peters_konto = Bankkonto(100, "Peter Python")
print(peters_konto.saldo)

# Ändra saldot till 1500
peters_konto.saldo = 1500
print(peters_konto.saldo)

# Vi lägger till 2000 till saldot
peters_konto.saldo += 2000
print(peters_konto.saldo)
```

<sample-output>

100
1500
3500

</sample-output>

Låt oss titta på ett annat exempel på klasser och objekt. Vi ska skriva en klass som modellerar lotteridragning:

```python
from datetime import date

class LotteriDragning:

    def __init__(self, vecka: int, datum: date, nummer: list):
        self.vecka = vecka
        self.datum = datum
        self.nummer = nummer


# Vi skapar ett nytt LotteriDragning-objekt
runda1 = LotteriDragning(1, date(2021, 1, 2), [1,4,8,12,13,14,33])

# Vi skriver ut resultatet
print(runda1.vecka)
print(runda1.datum)

for nummer in runda1.nummer:
    print(nummer)
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

Som du kan se ovan kan attributen vara av vilken typ som helst. Här har varje LotteriDragning-objekt attribut av typerna `list` och `date`.


<programming-exercise name='Bok' tmcname='osa08-06_bok'>

Skapa klassen `Bok`, som har variablerna `namn`, `forfattare`, `genre` och `ar`, tillsammans med en konstruktor som anger ursprungsvärden åt dessa attribut.

Klassen ska fungera enligt följande:

```python
python = Bok("Fluent Python", "Luciano Ramalho", "programmering", 2015)
aventyr = Bok("Äkta Äventyr", "Petter Persson", "självbiografi", 1956)

print(f"{python.forfattare}: {python.namn} ({python.ar})")
print(f"Boken {aventyr.namn}s genre är {aventyr.genre}")
```

<sample-output>

Luciano Ramalho: Fluent Python (2015)
Boken Äkta Äventyrs genre är självbiografi

</sample-output>

</programming-exercise>

<programming-exercise name='Skriv klasser' tmcname='osa08-07_skriv_klasser'>

Skapa de tre klasserna som anges nedan. Varje klass ska ha exakt samma namn och typer av attribut som anges i listan.

Inkludera också en konstruktor i varje klass. Konstruktorn ska ta de ursprungliga värdena för attributen som sina argument, i den ordning som anges nedan.

1. Klass Minneslista
- attribut rubrik (sträng)
- attribut inlagg (lista)

2. Klass Kund
- attribut id (sträng)
- attribut saldo (decimaltal)
- attribut rabatt (heltal)

3. Klass Kabel
- attribut modell (sträng)
- attribut langd (decimaltal)
- attribut maximal_hastighet (heltal)
- attribut dubbelriktad (Boolesk)

</programming-exercise>

## Användning av objekt från egengjorda klasser

Objekt som bildas från dina egna klassdefinitioner skiljer sig inte från andra Python-objekt. De kan skickas som argument och returnera värden precis som alla andra objekt. Vi kan till exempel skriva hjälpfunktioner för att arbeta med bankkonton:

```python
# funktionen skapar ett nytt bankkonto-objekt och returnerar det
def oppna_konto(namn: str):
    nytt_konto =  Bankkonto(0, namn)
    return nytt_konto

# denna funktion lägger till det belopp som anges som argument till saldot som anges som argument
def lagg_in_pengar_pa_kontot(konto: Bankkonto, summa: int):
    konto.saldo += summa

peters_konto = oppna_konto("Peter Python")
print(peters_konto.saldo)

lagg_in_pengar_pa_kontot(peters_konto, 500)

print(peters_konto.saldo)
```

<sample-output>

0
500

</sample-output>

<programming-exercise name='Skapa husdjur' tmcname='osa08-07b_skapa_husdjur'>

Definiera klassen `Husdjur`. Klassen har en konstruktor, som tar värden till attributen `namn`, `ras` och `fodelsear` i den ordningen.

Skapa sedan en funktion med namnet `nytt_husdjur(namn: str, ras: str, fodelsear: int)` _utanför klassdefinitionen_, som skapar och returnerar ett `Husdjur`-objekt (alltså av `Husdjur`-klassen definierad ovan).

Exempel på funktionens användning:

```python
molly = nytt_husdjur("Molly", "hund", 2017)
print(molly.namn)
print(molly.ras)
print(molly.fodelsear)
```

<sample-output>

Molly
hund
2017

</sample-output>

</programming-exercise>

<programming-exercise name='Äldre bok' tmcname='osa08-08_aldre_bok'>

Skapa funktionen `aldre_bok(bok1: bok, bok2: bok)`, som får som argument två objekt av typen `Bok`. Funktionen berättar vilkendera bok som är äldre. Ifall båda böckerna är publicerades samma år ska meddelandet som skrivs ut vara annorlunda.

Funktionen fungerar enligt följande:

```python
python = Bok("Fluent Python", "Luciano Ramalho", "programmering", 2015)
aventyr = Bok("Äkta Äventyr", "Petter Persson", "självbiografi", 1956)
norma = Bok("Norma", "Sofi Oksanen", "brott", 2015)

aldre_bok(python, aventyr)
aldre_bok(python, norma)
```

<sample-output>

Äkta Äventyr är äldre, den publicerades 1956
Fluent Python och Norma publicerades 2015

</sample-output>

</programming-exercise>

<programming-exercise name='Genrens böcker' tmcname='osa08-09_genrens_bocker'>

Skapa funktionen `genrens_bocker(bocker: list, genre: str)`, som får som argument en lista med `Bok`-objekt såväl som en sträng som representerar genren.

Funktionen returnerar _en ny_ lista, som innehåller böckerna med den specifierade genren från den originella listan.

Funktionen fungerar på följande sätt:

```python
python = Bok("Fluent Python", "Luciano Ramalho", "ohjelmointi", 2015)
aventyr = Bok("Äkta Äventyr", "Petter Persson", "självbiografi", 1956)
norma = Bok("Norma", "Sofi Oksanen", "rikos", 2015)

bocker = [python, aventyr, norma, Bok("Snögubben", "Jo Nesbø", "brott", 2007)]

print("Böcker i brottsgenren:")
for bok in genrens_bocker(bocker, "brott"):
    print(f"{bok.forfattare}: {bok.namn}")
```

<sample-output>

Böcker i brottsgenren:
Sofi Oksanen: Norma
Jo Nesbø: Snögubben

</sample-output>

</programming-exercise>
