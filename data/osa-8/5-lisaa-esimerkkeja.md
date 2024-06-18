---
path: '/osa-8/5-lisaa-esimerkkeja'
title: 'Fler exempel'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Kommer du att kunna skapa mer mångsidiga klasser
- Vet du hur du lägger till en `__str__`-metod i dina klassdefinitioner

</text-box>


## Exempel 1: klassen Rektangel

Låt oss ta en titt på en klass som modellerar en rektangel i ett tvådimensionellt rum:

```python
class Rektangel:
    def __init__(self, vanster_ovre: tuple, hoger_nedre: tuple):
        self.vanster_ovre = vanster_ovre
        self.hoger_nedre = hoger_nedre
        self.bredd = hoger_nedre[0]-vanster_ovre[0]
        self.hojd = hoger_nedre[1]-vanster_ovre[1]

    def area(self):
        return self.bredd * self.hojd

    def omkrets(self):
        return self.bredd * 2 + self.hojd * 2

    def flytta(self, x_andring: int, y_andring: int):
        horn = self.vanster_ovre
        self.vanster_ovre = (horn[0]+x_andring, horn[1]+y_andring)
        horn = self.hoger_nedre
        self.hoger_nedre = (horn[0]+x_andring, horn[1]+y_andring)
```

En ny `Rektangel` skapas med två tuplar som argument. Dessa tuplar innehåller x- och y-koordinaterna för det övre vänstra hörnet och det nedre högra hörnet. Konstruktören beräknar rektangelns höjd och bredd baserat på dessa värden.

Metoderna `area` och `omkrets` beräknar rektangelns area och omkrets baserat på höjd och bredd. Metoden `flytta` flyttar rektangeln med de x- och y-värden som anges som argument.

Rektangeln representeras i ett koordinatsystem där x-koordinaterna ökar från vänster till höger och y-koordinaterna ökar från topp till botten. Detta är ett vanligt sätt att hantera koordinater i programmering eftersom det ofta är enklare och mer naturligt att betrakta datorskärmens övre vänstra hörn som den punkt där x och y är lika med noll.

Följande program testar klassen `Rektangel`:

```python
rektangel = Rektangel((1, 1), (4, 3))
print(rektangel.vanster_ovre)
print(rektangel.hoger_nedre)
print(rektangel.bredd)
print(rektangel.hojd)
print(rektangel.omkrets())
print(rektangel.area())

rektangel.flytta(3, 3)
print(rektangel.vanster_ovre)
print(rektangel.hoger_nedre)
```

<sample-output>

(1, 1)
(4, 3)
3
2
10
6
(4, 4)
(7, 6)

</sample-output>

## Skriva ut ett objekt

När du har ett objekt som skapats från en klass som du själv definierat, är standardreaktionen på att anropa instruktionen `print` med objektet som argument inte särskilt informativt:

```python
rektangel = Rektangel((1, 1), (4, 3))
print(rektangel)
```

Utskriften borde se ut någorlunda så här:

<sample-output>

<__main__.Rektangel object at 0x000002D7BF148A90>

</sample-output>

Vi vill självklart ha mer kontroll över vad som skrivs ut. Det enklaste sättet att göra detta är att lägga till en speciell `__str__`-metod i klassdefinitionen. Dess syfte är att returnera en ögonblicksbild av objektets tillstånd i strängformat. Om klassdefinitionen innehåller en `__str__`-metod är det värde som returneras av metoden, det som skrivs ut när instruktionen `print` körs.

Så låt oss lägga till en `__str__`-metoddefinition i vår `Rektangel`-klass:

```python
class Rektangel:

    # Resten av klassen kommer här såsom ovan

    # Metoden returnerar objektets tillstånd i strängformat
    def __str__(self):
        return f"rektangel {self.vanster_ovre} ... {self.hoger_nedre}"
```

Nu borde `print` instruktionen producera nånting mer användarvänligt:

```python
rektangel = Rektangel((1, 1), (4, 3))
print(rektangel)
```

<sample-output>

rektangel (1, 1) ... (4, 3)

</sample-output>

Metoden `__str__` används kanske oftare för att formulera en strängrepresentation av objektet med `str`-funktionen, som i följande program:

```python
rektangel = Rektangel((1, 1), (4, 3))
beskrivning = str(rektangel)
print(beskrivning)
```

<sample-output>

rektangel (1, 1) ... (4, 3)

</sample-output>


Det finns många fler speciella understrukna metoder som kan definieras för klasser. En metod som liknar `__str__`-metoden är `__repr__`-metoden. Dess syfte är att ge en teknisk representation av objektets tillstånd. Vi kommer att stöta på denna metod senare.

<programming-exercise name='Sekuntikello' tmcname='osa08-11a_sekuntikello'>

Uppgiftsbotten innehåller följande ram för klassen `Stoppur`:

```python
class Stoppur:
    def __init__(self):
        self.sekunder = 0
        self.minuter = 0
```

Bygg ut på klassdefinitionen så att den fungerar enligt följande:

```python
klocka = Stoppur()
for i in range(3600):
    print(klocka)
    klocka.tick()
```

<sample-output>

00:00
00:01
00:02
... många fler rader utskrivna
00:59
01:00
01:01
... många, många fler rader utskrivna
59:58
59:59
00:00
00:01

</sample-output>

Metoden `tick` innebär alltså att en sekund läggs till i stoppuret. Det maximala värdet för både sekunder och minuter är 59. Din klassdefinition bör också innehålla en `__str__`-metod, som returnerar en strängrepresentation av stoppurets tillstånd, som visas i exemplet ovan.

**Tips:** Det kan göra det lättare att testa `tick`-metoden om du tillfälligt ställer in startvärdena för sekunder och minuter till något värde närmare 59 i konstruktorn. Om du ändrar de ursprungliga värdena, kom ihåg att ändra tillbaka dem innan du skickar in.

</programming-exercise>

<programming-exercise name='Kello' tmcname='osa08-12_kello'>

Definiera en ny klass `Klocka`, som bygger på Stoppur klassen. Den ska fungera enligt följande:

```python
klocka = Klocka(23, 59, 55)
print(klocka)
klocka.tick()
print(klocka)
klocka.tick()
print(klocka)
klocka.tick()
print(klocka)
klocka.tick()
print(klocka)
klocka.tick()
print(klocka)
klocka.tick()
print(klocka)

klocka.installning(12, 5)
print(klocka)
```

<sample-output>
23:59:55
23:59:56
23:59:57
23:59:58
23:59:59
00:00:00
00:00:01
12:05:00
</sample-output>

Konstruktorn tar alltså ursprungliga värden för timmar, minuter och sekunder som argument. Metoden `tick` för klockan framåt en sekond och metoden `installning` ställer in klockans timmar och minuter och _nollar sekunderna_.

</programming-exercise>

<programming-exercise name='Maksukortti' tmcname='osa08-13_maksukortti'>

På Unicafe, studentkafeterian vid Helsingfors universitet, kan studenterna betala för sin lunch med ett särskilt betalkort.

I den här övningen kommer du att skriva en klass som heter Lunchkort, med syftet att emulera de funktioner som tillhandahålls av Unicafes betalkort.

### Del 1: Strukturen av klassen

Skapa en ny klass med namnet `Lunchkort`.

Skapa först konstruktorn för klassen. Den ska ta det ursprungliga saldot som finns på kortet som ett argument och spara det som ett attribut. Skapa sedan en `__str__`-metod som returnerar en sträng som innehåller saldot: ”Saldot är X euro”. Det tillgängliga saldot ska skrivas ut med en decimals noggrannhet. Se exemplet nedan för användning.

Följande är en ram av klassen:

```python
class Lunchkort:
    def __init__(self, saldo: float):
        self.saldo = saldo

    def __str__(self):
        pass
```

Exempel av användning:

```python
kort = Lunchkort(50)
print(kort)
```

Programmet ovan borde producera följande utskrift:

<sample-output>

Kortets saldo är 50.0 euro

</sample-output>

### Del 2: Betalning av lunch

Implementera följande metoder till din Lunchkort klass:

- `at_formanligt` som minskar saldot med 2.60 euro
- `at_special` som minskar saldot med 4.60 euro

Följande huvudfunktion testar din klass:

```python
kort = Lunchkort(50)
print(kort)

kort.at_formanligt()
print(kort)

kort.at_special()
kort.at_formanligt()
print(kort)
```

Detta borde ge följande utskrift:

<sample-output>

Kortets saldo är 50.0 euro
Kortets saldo är 47.4 euro
Kortets saldo är 40.2 euro

</sample-output>

Se till att kortets saldo inte kan bli under 0:

```python
kort = Lunchkort(4)
print(kort)

kort.at_formanligt()
print(kort)

kort.at_formanligt()
print(kort)
```

<sample-output>

Kortets saldo är 4.0 euro
Kortets saldo är 1.4 euro
Kortets saldo är 1.4 euro

</sample-output>

Kortets saldo får alltså inte minska ifall det inte finns tillräckligt med pengar på det.

### Del 3: Sätta in pengar på kortet

Lägg till metoden `tillsatt_pengar` till `Lunchkort`-klassen.

Metoden ska öka saldot på kortet med mängden angivet som argument.

```python
kort = Lunchkort(10)
print(kort)
kort.tillsatt_pengar(15)
print(kort)
kort.tillsatt_pengar(10)
print(kort)
kort.tillsatt_pengar(200)
print(kort)
```

<sample-output>

Kortets saldo är 10.0 euro
Kortets saldo är 25.0 euro
Kortets saldo är 35.0 euro
Kortets saldo är 235.0 euro

</sample-output>

Ifall kortet försöker laddas med en negativ mängd ska metoden [åstadkomma ett undantag](/osa-6/3-virheet#poikkeusten-tuottaminen) av typen `ValueError`:

```python
kort = Lunchkort(10)
kort.tillsatt_pengar(-10)
```

<sample-output>

File "testi.py", line 3, in lunchkort
ValueError: Det går inte att lägga till mindre än noll

</sample-output>

**OBS:** metoden ska _åstadkomma_ ett undantag, se [del 6](/osa-6/3-virheet#poikkeusten-tuottaminen) i materialet hur man gör. Metoden får under inga omständigheter själv skriva ut nånting!

### Del 4: Flera kort

Skapa ett huvudprogram, som innehåller följande händelser:

- Skapa Peters kort. Kortets ursprungliga saldo är 20 euro
- Skapa Mattes kort. Kortets ursprungliga saldo är 30 euro
- Peter äter en special
- Matte äter förmånligt
- _Kortens saldon skrivs ut (På varsin rad, med ägarens namn i början av raden)_
- Peter tillsätter 20 euro på kortet
- Matte äter en special
- _Kortens saldon skrivs ut (På varsin rad, med ägarens namn i början av raden)_
- Peter äter förmånligt
- Peter äter förmånligt
- Matte tillsätter 50 euro på kortet
- _Kortens saldon skrivs ut (På varsin rad, med ägarens namn i början av raden)_

Huvudprogrammets ram:

```python
peters_kort = Lunchkort(20)
mattes_kort = Lunchkort(30)
# resten av huvudprogrammet
```

Utskriften borde vara följande:

<sample-output>

Peter: Kortets saldo är 15.4 euro
Matte: Kortets saldo är 27.4 euro
Peter: Kortets saldo är 35.4 euro
Matte: Kortets saldo är 22.8 euro
Peter: Kortets saldo är 30.2 euro
Matte: Kortets saldo är 72.8 euro

</sample-output>

</programming-exercise>

## Exempel 2: Uppgiftslista

Följande klass `Uppgiftslista` modellerar en lista med uppgifter:

```python
class Uppgiftslista:
    def __init__(self):
        self.uppgifter = []

    def tillsatt(self, namn: str, prioritet: int):
        self.uppgifter.append((prioritet, namn))

    def hamta_nasta(self):
        self.uppgifter.sort()
        # Metoden pop tar bort och returnerar sista föremålet på listan
        uppgift = self.uppgifter.pop()
        # Returnerar det andra föremålet i tupeln, alltså uppgiftens namn
        return uppgift[1]

    def sammanlagt(self):
        return len(self.uppgifter)

    def rensa_uppgifter(self):
        self.uppgifter = []
```

Metoden `tillagg_uppgift` lägger till en ny uppgift på listan. Varje uppgift har också en prioritet, som används för att sortera uppgifterna. Metoden `hamta_nasta` tar bort och returnerar den uppgift som har högst prioritet i listan. Metoden `sammanlagt` finns också, som returnerar antalet uppgifter i listan, och slutligen metoden `rensa_uppgifter`, som rensar uppgiftslistan.

Inom objektet lagras uppgifterna i en lista. Varje uppgift består av en tupel som innehåller uppgiftens prioritet och dess namn. Prioritetsvärdet lagras först, så att den uppgift som har högst prioritet hamnar sist i listan då den sorteras. Därför kan vi sedan helt enkelt använda `pop`-metoden för att hämta och ta bort det högst prioriterade objektet.

Ta en titt på följande program med uppgiftslistan i handling: 

```python
lista = Uppgiftslista()
lista.tillsatt("studier", 50)
lista.tillsatt("motion", 60)
lista.tillsatt("städning", 10)
print(lista.sammanlagt())
print(lista.hamta_nasta())
print(lista.sammanlagt())
lista.tillsatt("dejt", 100)
print(lista.sammanlagt())
print(lista.hamta_nasta())
print(lista.hamta_nasta())
print(lista.sammanlagt())
lista.rensa_uppgifter()
print(lista.sammanlagt())
```

<sample-output>

3
motion
2
3
dejt
studier
1
0

</sample-output>

<programming-exercise name='Sarja' tmcname='osa08-14_sarja'>

### Del 1: Klassen Serie

Skapa klassen `Serie`, som fungerar enligt följande:

```python
dexter = Serie("Dexter", 8, ["Crime", "Drama", "Mystery", "Thriller"])
print(dexter)
```

<sample-output>

Dexter (8 säsonger)
genret: Crime, Drama, Mystery, Thriller
inga betygsättningar

</sample-output>

Konstruktorn ska ta titeln, antalet säsonger och en lista med genrer för serien som sina argument.

**Tips:** när du behöver en sträng från en lista med strängar, där du vill separera med en karaktär av ditt val, kan du använda `join` metoden på följande sätt:

```python
lista = ["Crime", "Drama", "Mystery", "Thriller"]
strang = ", ".join(lista)
print(strang)
```

<sample-output>

Crime, Drama, Mystery, Thriller

</sample-output>

### Del 2: Betygsättningar

Skapa en metod `betygsatt(betyg: int)`, med vilken man kan ge ett betyg mellan heltalen 0 och 5. Också metoden `__str__` ska ändras som så, att ifall det finns några betyg ska metoden skriva ut mängden betyg och deras medeltal med en decimals noggranhet.

```python
dexter = Serie("Dexter", 8, ["Crime", "Drama", "Mystery", "Thriller"])
dexter.betygsatt(4)
dexter.betygsatt(5)
dexter.betygsatt(5)
dexter.betygsatt(3)
dexter.betygsatt(0)
print(dexter)
```

<sample-output>

Dexter (8 esityskautta)
genret: Crime, Drama, Mystery, Thriller
Betyg 5, medeltal 3.4 poäng

</sample-output>

### Del 3: Sökning av serier

Skapa två funktioner `betyg_minst(betyg: float, serier: list)` och `innehallar_genren(genre: str, serier: list)`, med vilka det är möjligt att hitta serier på listan.

Metoderna fungerar på följande sätt:

```python
s1 = Serie("Dexter", 8, ["Crime", "Drama", "Mystery", "Thriller"])
s1.betygsatt(5)

s2 = Serie("South Park", 24, ["Animation", "Comedy"])
s2.betygsatt(3)

s3 = Serie("Friends", 10, ["Romance", "Comedy"])
s3.betygsatt(2)

serier = [s1, s2, s3]

print("betyg minst 4.5:")
for serie in betyg_minst(4.5, serier):
    print(serie.namn)

print("genre Comedy:")
for serie in innehallar_genren("Comedy", serier):
    print(serie.namn)
```

<sample-output>

betyg minst 4.5:
Dexter

genre Comedy:
South Park
Friends

</sample-output>

Observera att ovanstående kod och testerna för denna övning antar att din klass innehåller attributet `namn`. Ifall du använder något annat attribut för att hänvisa till namnet på serien, bör du ändra det innan du skickar in uppgifterna.

</programming-exercise>

Vänligen svara på en snabb enkät om veckans material:

<quiz id="05b480cc-49ea-51e4-a971-d03209a54d5b"></quiz>
