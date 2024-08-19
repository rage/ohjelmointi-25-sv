---
path: '/osa-9/3-inkapsling'
title: 'Inkapsling'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Vet du vad inkapsling innebär
- Kommer du att kunna skapa privata attribut
- Vet du hur du skapar gettar och sättare för dina attribut

</text-box>

I objektorienterad programmering avser termen klient ett program som använder en klass eller instanser av en klass. En klass erbjuder klienten tjänster genom vilka klienten kan komma åt de objekt som skapats baserat på klassen. Målen här är att

1) användningen av en klass och/eller objekt är så enkel som möjligt ur klientens synvinkel
2) integriteten för varje objekt bevaras hela tiden

Ett objekts integritet innebär att objektets tillstånd alltid förblir acceptabelt. I praktiken innebär detta att värdena på objektets attribut alltid är acceptabla. Ett objekt som representerar ett datum ska till exempel aldrig ha 13 som värde för månaden, ett objekt som representerar en student ska aldrig ha ett negativt tal som värde för uppnådda studiepoäng och så vidare.

Låt oss ta en titt på en klass som heter Studerande:

```python
class Studerande:
    def __init__(self, namn: str, studerandenummer: str):
        self.namn = namn
        self.studerandenummer = studerandenummer
        self.studiepoang = 0

    def tillagg_poang(self, studiepoang):
        if studiepoang > 0:
            self.studiepoang += studiepoang
```

`Studerande` objektet erbjuder sina klienter metoden `tillagg_poang`, som gör det möjligt för klienten att lägga till ett angivet antal studiepoäng till studentens totala antal. Metoden säkerställer att värdet som skickas som argument är över noll. Följande kod lägger till studiepoäng vid tre tillfällen:

```python
oskar = Studerande("Oskar Studerande", "12345")
oskar.tillagg_poang(5)
oskar.tillagg_poang(5)
oskar.tillagg_poang(10)
print("Studiepoäng:", oskar.studiepoang)
```

<sample-output>

Studiepoäng: 20

</sample-output>


Trots metoddefinitionen är det fortfarande möjligt att komma åt attributet `studiepoang` direkt. Detta kunde resultera i ett felaktigt tillstånd där objektets integritet går förlorad:

```python
oskar = Studerande("Oskar Studerande", "12345")
oskar.studiepoang = -100
print("Studiepoäng:", oskar.studiepoang)
```

<sample-output>

Studiepoäng: -100

</sample-output>

## Inkapsling

Ett vanligt inslag i objektorienterade programmeringsspråk är att klasserna kan dölja sina attribut för eventuella kunder. Dolda attribut kallas vanligtvis privata. I Python uppnås denna sekretess genom att lägga till två understreck `__` i början av attributnamnet:

```python
class Bankkort:
    # Attributet nummer är gömt, attributet namn är åtkombart
    def __init__(self, nummer: str, namn: str):
        self.__nummer = nummer
        self.namn = namn
```

Ett privat attribut är inte direkt synligt för klienten. Försök att referera till det orsakar ett fel. I exemplet ovan är attributet namn lätt att komma åt och ändra:

```python
kort = Bankkort("123456","Robert Rik")
print(kort.namn)
kort.namn = "Peter Pank"
print(kort.namn)
```

<sample-output>

Robert Rik
Peter Pank

</sample-output>

Ifall man provar få en utskrift av kortnumret så orsakar det däremot ett fel:

```python
kort = Bankkort("123456","Robert Rik")
print(kort.__nummer)
```

<sample-output>

AttributeError: 'Bankkort' object has no attribute '__nummer'

</sample-output>

Att dölja attribut från klienter kallas inkapsling. Som namnet antyder är attributet "slutet inne i en kapsel". Klienten erbjuds sedan ett lämpligt gränssnitt (engelska: interface) för att komma åt och bearbeta den data som finns lagrad i objektet.

Låt oss lägga till ett annat inkapslat attribut: saldot på kreditkortet. Den här gången lägger vi också till offentligt synliga metoder som gör det möjligt för klienten att komma åt och ändra saldot:

```python
class Bankkort:
    def __init__(self, nummer: str, namn: str, saldo: float):
        self.__nummer = nummer
        self.namn = namn
        self.__saldo = saldo

    def tillsatt_pengar(self, mangd: float):
        if mangd > 0:
            self.__saldo += mangd

    def anvand_pengar(self, mangd: float):
        if mangd > 0 and mangd <= self.__saldo:
            self.__saldo -= mangd

    def hamta_saldo(self):
        return self.__saldo
```

```python
kort = Bankkort("123456", "Robert Rik", 5000)
print(kort.hamta_saldo())
kort.tillsatt_pengar(100)
print(kort.hamta_saldo())
kort.anvand_pengar(500)
print(kort.hamta_saldo())
# Detta lyckas inte, eftersom saldot inte är tillräckligt
kort.anvand_pengar(10000)
print(kort.hamta_saldo())
```

<sample-output>

5000
5100
4600
4600

</sample-output>

Saldot kan inte ändras direkt eftersom attributet är privat, men vi har inkluderat metoderna `tillsatt_pengar` och `ta_ut_pengar` för att ändra värdet. Metoden `returnera_saldo` returnerar det värde som lagrats i saldo. Metoderna innehåller några rudimentära kontroller för att bibehålla objektets integritet: till exempel kan kortet inte överdras.

<programming-exercise name='Bil' tmcname='osa09-09_bil'>

Implementera en klass som heter `Bil` och som har två privata, _inkapslade_ variabler: mängden bensin i tanken (0 till 60 liter) och vägmätarställningen (i kilometer). Bilen förbrukar en liter bensin per kilometer.

Klassen ska ha följande metoder:

- `tanka()`, som fyller bensintanken
- `kor(km:int)`, som kör bilen enligt den angivna distansen eller för så länge bensinen i tanken räcker
- `__str__`, som visar en strängrepresentation av bilen enligt exemplet nedan

Exempel på hur klassen fungerar:

```python
bil = Bil()
print(bil)
bil.tanka()
print(bil)
bil.kor(20)
print(bil)
bil.kor(50)
print(bil)
bil.kor(10)
print(bil)
bil.tanka()
bil.tanka()
print(bil)
```

<sample-output>

Bil: har kört 0 km, bensin 0 liter
Bil: har kört 0 km, bensin 60 liter
Bil: har kört 20 km, bensin 40 liter
Bil: har kört 60 km, bensin 0 liter
Bil: har kört 60 km, bensin 0 liter
Bil: har kört 60 km, bensin 60 liter

</sample-output>

**OBS:** Du ombeds att kapsla in mängden bensin som finns kvar och vägmätarställningen. Det ska inte vara möjligt att komma åt dem direkt utanför klassens egna metoder.

</programming-exercise>

## En kort notis om privata attribut, Python och objektorienterad programmering

Det finns sätt att kringgå understryknings `__`-notationen för att dölja attribut, som du kan stöta på om du söker efter material online. Inget Python-attribut är verkligen privat, och det är avsiktligt från skaparna av Pythons. Å andra sidan förväntas en Python-programmerare i allmänhet respektera de riktlinjer för synlighet som anges i klasser, och det krävs en särskild ansträngning för att komma runt dessa. I andra objektorienterade programmeringsspråk, till exempel Java, är privata variabler ofta verkligen dolda, och det är bäst om du tänker på privata Python-variabler som sådana också.

## Getter och sättare

I objektorienterad programmering kallas metoder som är avsedda för att komma åt och ändra attribut vanligtvis för getter och sättare (eng: setters). Inte alla Python-programmerare använder termerna "getter" och "sättare", men konceptet med egenskaper som beskrivs nedan är mycket liknande, vilket är varför vi kommer att använda den allmänt accepterade objektorienterade programmeringsterminologin här.

Ovan skapade vi några offentliga metoder för att komma åt privata attribut, men det finns ett enklare, "pythoniskt" sätt att komma åt attribut. Låt oss ta en titt på en enkel klass som heter `Planbok` med ett enda privat attribut `pengar`:

```python
class Planbok:
    def __init__(self):
        self.__pengar = 0
```

Vi kan tillägga getter och sättar metoder för att komma åt det privata attributet genom att använda `@property` dekoratorn:

```python
class Planbok:
    def __init__(self):
        self.__pengar = 0

    # Gettermetod
    @property
    def pengar(self):
        return self.__pengar

    # Sättarmetod
    @pengar.setter
    def pengar(self, pengar):
        if pengar >= 0:
            self.__pengar = pengar
```

Först definierar vi en getter-metod som returnerar den summa pengar som för närvarande finns i plånboken. Sedan definierar vi en sättar-metod som sätter ett nytt värde för pengar-attributet och samtidigt ser till att det nya värdet inte är negativt.

De nya metoderna kan användas på följande sätt:

```python
planbok = Planbok()
print(planbok.pengar)

planbok.pengar = 50
print(planbok.pengar)

planbok.pengar = -30
print(planbok.pengar)
```

<sample-output>

0
50
50

</sample-output>

För klienten är det ingen skillnad att använda dessa nya metoder jämfört med att direkt komma åt ett attribut. Parenteser är inte nödvändiga, utan det är helt acceptabelt att ange `planbok.pengar = 50`, som om vi helt enkelt tilldelar ett värde till en variabel. Syftet var faktiskt att dölja (dvs. kapsla in) den interna implementeringen av attributet och samtidigt erbjuda ett enkelt sätt att komma åt och ändra den data som lagras i objektet.

I det föregående exemplet finns dock ett litet problem: klienten meddelas inte om att det inte går att ange ett negativt värde för attributet pengar. När ett värde som anges är uppenbart felaktigt är det vanligtvis en bra idé att skapa ett undantag och på så sätt informera klienten. I det här fallet bör undantaget förmodligen vara av typen `ValueError` för att visa att det angivna värdet var oacceptabelt.

Här har vi en förbättrad version av klassen, tillsammans med lite kod för att testa den:

```python
class Planbok:
    def __init__(self):
        self.__pengar = 0

    # Gettermetod
    @property
    def pengar(self):
        return self.__pengar

    # Sättarmetod
    @pengar.setter
    def pengar(self, pengar):
        if pengar >= 0:
            self.__pengar = pengar
        else:
            raise ValueError("Mängden får inte vara under 0")
```

```python
planbok.pengar = -30
print(planbok.pengar)
```

<sample-output>

ValueError: Mängden får inte vara under 0

</sample-output>

OBS: getter-metoden, dvs `@property-dekoratorn`, måste introduceras före sättar-metoden i koden, annars blir det fel när klassen exekveras. Detta beror på att `@property-dekoratorn` definierar namnet på det "attribut" som erbjuds till klienten. Sättar-metoden, som läggs till med `.setter`, lägger helt enkelt till en ny funktionalitet till den.

<programming-exercise name='Inspelning' tmcname='osa09-10_inspelning'>

Skapa en klass med namnet `Inspelning` som modellerar en enda inspelning. Klassen ska ha en privat variabel: `__langd` av typen heltal.

Implementera följande:

* konstruktorn, som får längden som argument
* en gettermetod `langd`, som returnerar längden av inspelningen
* en sättarmetod, som sätter längden på inspelningen

Klassen används på följande sätt:

```python
the_wall = Inspelning(43)
print(the_wall.langd)
the_wall.langd = 44
print(the_wall.langd)
```

<sample-output>

43
44

</sample-output>

Om argumentet för antingen konstruktorn eller sättar-metoden är under noll, bör detta åstadkomma ett `ValueError`.

Ifall du inte minns hur man åstadkommer undantag, kan du kolla in
[modul 6](https://rage.github.io/ohjelmointi-24-sv/osa-6/3-fel) av materialet.

</programming-exercise>

Följande exempel har en klass med två privata attribut, tillsammans med getter och sättare för båda. Prova programmet med olika värden som skickas som argument:

```python
class Spelare:
    def __init__(self, namn: str, spelnummer: int):
        self.__namn = namn
        self.__spelnummer = spelnummer

    @property
    def namn(self):
        return self.__namn

    @namn.setter
    def namn(self, namn: str):
        if namn != "":
            self.__namn = namn
        else:
            raise ValueError("Namnet kan inte vara tomt")

    @property
    def spelnummer(self):
        return self.__spelnummer

    @spelnummer.setter
    def spelnummer(self, spelnummer: int):
        if spelnummer > 0:
            self.__spelnummer = spelnummer
        else:
            raise ValueError("Spelnumret måste vara ett positivt heltal")
```

```python
spelare = Spelare("Fredrik Fotare", 10)
print(spelare.namn)
print(spelare.spelnummer)

spelare.namn = "Fia Futis"
spelare.spelnummer = 11
print(spelare.namn)
print(spelare.spelnummer)
```

<sample-output>

Fredrik Fotare
10
Fia Futis
11

</sample-output>

Som avslutning på detta avsnitt ska vi titta på en klass som modellerar en enkel dagbok. Alla attribut är privata, men de hanteras genom olika gränssnitt: dagbokens ägare har getter- och sättar-metoder, men dagboksposterna behandlas med "traditionella" metoder. I det här fallet är det vettigt att neka klienten all tillgång till dagbokens interna datastruktur. Endast de offentliga metoderna är direkt synliga för klienten.

Inkapsling säkerställer också att den interna implementeringen av klassen kan ändras när som helst, förutsatt att det offentliga gränssnittet förblir intakt. Klienten behöver inte veta eller bry sig om huruvida den interna datastrukturen är baserad på listor, ordlistor eller något helt annat.

```python
class Dagbok:
    def __init__(self, agare: str):
        self.__agare = agare
        self.__inlagg = []

    @property
    def agare(self):
        return self.__agare

    @agare.setter
    def agare(self, agare):
        if agare != "":
            self.__agare = agare
        else:
            raise ValueError("Ägaren kan inte vara tom")

    def tillsatt_inlagg(self, inlagg: str):
        self.__inlagg.append(inlagg)

    def skriv_ut(self):
        print("Totalt", len(self.__inlagg), "inlägg")
        for inlagg in self.__inlagg:
            print("- " + inlagg)
```

```python
dagbok = Dagbok("Peter")
dagbok.tillsatt_inlagg("Idag åt jag gröt")
dagbok.tillsatt_inlagg("Idag lärde jag mig objekt-orienterad programmering")
dagbok.tillsatt_inlagg("Idag lade jag mig tidigt")
dagbok.skriv_ut()
```

<sample-output>

Totalt 3 inlägg
- Idag åt jag gröt
- Idag lärde jag mig objekt-orienterad programmering
- Idag lade jag mig tidigt

</sample-output>

<programming-exercise name='Väderstation' tmcname='osa09-11_vaderstation'>

Skapa en klass med namnet Vaderstation som används för att lagra observationer om vädret. Klassen bör ha följande offentliga attribut:

* en konstruktor som tar namnet på stationen som sitt argument
* metoden `tillsatt_observation(observation: str)`, som lägger till en observation till slutet av listan
* metoden `senaste_observation()`, som returnerar den senaste observationen som lagts till i listan. Om det ännu inte finns några observationer bör metoden returnera en _tom sträng_.
* metoden `observationernas_antal()`, som returnerar det totala antalet observationer
* metoden `__str__`, som returnertar stationens namn och det totala antalet observationer liksom exemplet nedan.

Alla attribut ska vara inkapslade, så att de inte kan nås direkt. Det är upp till dig hur du implementerar klassen, så länge som det allmänna gränssnittet är exakt som beskrivet ovan.

Exempel på hur klassen ska fungera:

```python
station = Vaderstation("Gumtäkt")
station.tillsatt_observation("Regn 10mm")
station.tillsatt_observation("Soligt")
print(station.senaste_observation())

station.tillsatt_observation("Åskväder")
print(station.senaste_observation())

print(station.observationernas_antal())
print(station)
```

<sample-output>

Soligt
Åskväder
3
Gumtäkt, 3 observationer

</sample-output>

</programming-exercise>
