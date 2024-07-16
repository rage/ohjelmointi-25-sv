---
path: '/osa-10/1-klasshierarkier'
title: 'Klasshierarkier'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Vet du vad arv betyder i programmeringssammanhang
- Kommer du att kunna skriva klasser som ärver andra klasser
- Vet du hur arv påverkar egenskaperna i klasser

</text-box>

## Specialklasser för speciella ändamål

Ibland stöter man på en situation där man redan har definierat en klass, men sedan inser att man behöver speciella egenskaper i vissa, men inte alla, instanser av klassen. Och ibland inser man att man har definierat två stycken mycket liknande klasser med bara små skillnader. Som programmerare strävar vi efter att alltid upprepa oss så lite som möjligt, medan vi behåller tydlighet och läsbarhet. Så hur kan vi ta hänsyn till olika implementeringar av liknande objekt?

Låt oss ta en titt på två klassdefinitioner: `Studerande` och `Larare`. Getter- och sättar-metoder har utelämnats tills vidare för att hålla exemplet kort.

```python

class Studerande:

    def __init__(self, namn: str, id: str, epost: str, studiepoang: str):
        self.namn = namn
        self.id = id
        self.epost = epost
        self.studiepoang = studiepoang

class Larare:

    def __init__(self, namn: str, epost: str, rum: str, larande_ar: int):
        self.namn = namn
        self.epost = epost
        self.rum = rum
        self.larande_ar = larande_ar

```

Även i ett avskalat exempel som ovan har vi redan en hel del upprepningar: båda klasserna innehåller attributen `namn` och `epost`. Det vore en bra idé att ha en enda attributdefinition, så att det räcker med en enda funktion för att redigera båda attributen.

Tänk dig till exempel att skolans e-postadress ändras. Alla adresser skulle behöva uppdateras. Vi skulle kunna skriva två separata versioner av i stort sett samma funktion:

```python

def uppdatera_epost(s: Studerande):
    s.epost = s.epost.replace(".com", ".edu")

def uppdatera_epost2(s: Larare):
    s.epost = s.epost.replace(".com", ".edu")

```

Att skriva i stort sett samma sak två gånger är onödig upprepning, för att inte tala om att det fördubblar möjligheterna till fel. Det skulle vara en klar förbättring om vi kunde använda en enda funktion för att arbeta med instanser av båda klasserna.

Båda klasserna har också attribut som är unika för dem. Att bara kombinera alla attribut i en enda klass skulle innebära att alla instanser av klassen då skulle ha onödiga attribut, bara olika för olika instanser. Det verkar inte heller vara en idealisk situation.

## Arv

Objektorienterade programmeringsspråk innehåller vanligtvis en teknik som kallas arv (eng. inheritance). En klass kan ärva egenskaper från en annan klass. Förutom dessa ärvda egenskaper kan en klass också innehålla egenskaper som är unika för den.

Med detta i åtanke är det rimligt att klasserna `Larare` och `Studerande` har en gemensam bas eller föräldraklass `Person`:

 ```python

class Person:

    def __init__(self, namn: str, epost: str):
        self.namn = namn
        self.epost = epost

 ```

Den nya klassen innehåller de egenskaper som delas av de andra två klasserna. Nu kan `Studerande` och `Larare` ärva dessa egenskaper och dessutom lägga till sina egna. :

Syntaxen för arv innebär helt enkelt att basklassens namn läggs till inom parentes på rubrikraden:

 ```python

class Person:

    def __init__(self, namn: str, epost: str):
        self.namn = namn
        self.epost = epost

    def uppdatera_epost_doman(self, ny_doman: str):
        gammal_doman = self.epost.split("@")[1]
        self.epost = self.epost.replace(gammal_doman, ny_doman)

class Studerande(Person):

    def __init__(self, namn: str, id: str, epost: str, studiepoang: str):
        self.namn = namn
        self.id = id
        self.epost = epost
        self.studiepoang = studiepoang

class Larare(Person):

    def __init__(self, namn: str, epost: str, rum: str, larande_ar: int):
        self.namn = namn
        self.epost = epost
        self.rum = rum
        self.larande_ar = larande_ar

# Test
if __name__ == "__main__":
    sam = Studerande("Sam Studerande", "1234", "sam@example.com", 0)
    sam.uppdatera_epost_doman("example.edu")
    print(sam.epost)

    lars = Larare("Lars Lärare", "lars@example.fi", "A123", 2)
    lars.uppdatera_epost_doman("example.ex")
    print(lars.epost)

 ```

Både `Studerande` och `Larare` ärver klassen `Person`, så båda har de egenskaper som definieras i klassen Person, inklusive metoden `uppdatera_epost_doman`. Samma metod fungerar för instanser av båda de härledda klasserna.

 Låt oss titta på ett annat exempel. Vi har en `Bokhylla` som ärver klassen `BokLada`:

 ```python
class Bok:
    """ Klassen modellerar en enkel bok """
    def __init__(self, namn: str, forfattare: str):
        self.namn = namn
        self.forfattare = forfattare


class BokLada:
    """ Klassen modellerar en låda för böcker """

    def __init__(self):
        self.bocker = []

    def tillsatt_bok(self, bok: Bok):
        self.bocker.append(bok)

    def lista_bocker(self):
        for bok in self.bocker:
            print(f"{bok.namn} ({bok.forfattare})")

class Bokhylla(BokLada):
    """ Klassen modellerar en hylla för böcker """

    def __init__(self):
        super().__init__()

    def tillsatt_bok(self, bok: Bok, paikka: int):
        self.bocker.insert(paikka, bok)


 ```

 Klassen `Bokhylla` innehåller metoden `tillsatt_bok`. En metod med samma namn finns definierad i basklassen `BokLada`. Detta kallas överstyrning (eng. overriding): om en härledd klass har en metod med samma namn som basklassen, överstyr den härledda versionen originalet i instanser av den härledda klassen.

 Tanken i exemplet ovan är att en ny bok som läggs till i en Bok låda alltid hamnar högst upp, men med en Bokhylla kan du själv ange platsen. Metoden `lista_bocker` fungerar likadant för båda klasserna, eftersom det inte finns någon överordnad metod i den härledda klassen.

 Låt oss prova dessa klasser:

 ```python

if __name__ == "__main__":
    # Vi skapar några böcker för testning
    b1 = Bok("7 bröder", "Aleksis Kivi")
    b2 = Bok("Sinuhe", "Mika Waltari")
    b3 = Bok("Okänd soldat", "Väinö Linna")

    # Vi skapar en BokLada och tillsätter böckerna
    lada = BokLada()
    lada.tillsatt_bok(b1)
    lada.tillsatt_bok(b2)
    lada.tillsatt_bok(b3)

    # Vi skapar en Bokhylla och tillsätter böckerna (alltid till början av hyllan)
    hylla = Bokhylla()
    hylla.tillsatt_bok(b1, 0)
    hylla.tillsatt_bok(b2, 0)
    hylla.tillsatt_bok(b3, 0)


    # Skriver ut
    print("I lådan:")
    lada.lista_bocker()

    print()

    print("I hyllan:")
    hylla.lista_bocker()

 ```

 <sample-output>

I lådan:
7 bröder (Aleksis Kivi)
Sinuhe (Mika Waltari)
Okänd soldat (Väinö Linna)

I hyllan:
Okänd soldat (Väinö Linna)
Sinuhe (Mika Waltari)
7 bröder (Aleksis Kivi)

 </sample-output>

Klassen Bokhylla har alltså också tillgång till metoden `lista_bocker`. Genom ärvning är metoden medlem i alla klasser som kommer från klassen `BokLada`.

## Arv och räckvidd av egenskaper

 En härledd klass ärver alla egenskaper från sin basklass. Dessa egenskaper är direkt åtkomliga i den härledda klassen, såvida de inte har definierats som privata i basklassen (med två understreck före egenskapens namn).

 Eftersom attributen för en Bokhylla är identiska med en BokLada, fanns det ingen anledning att skriva om konstruktorn för Bokhylla. Vi anropade helt enkelt basklassens konstruktor:

 ```python

 class Bokhylla(BokLada):

    def __init__(self):
        super().__init__()

```

Alla egenskaper i basklassen kan nås från den härledda klassen med funktionen `super()`. Argumentet `self` utelämnas från metodanropet, eftersom Python lägger till det automatiskt.

Men vad händer om attributen inte är identiska; kan vi fortfarande använda basklassens konstruktor på något sätt? Låt oss titta på en klass som heter `Avhandling` och som ärver klassen `Bok`. Den härledda klassen kan fortfarande anropa konstruktören från basklassen:

```python

class Bok:
    """ Klassen modellerar en enkel bok """

    def __init__(self, namn: str, forfattare: str):
        self.namn = namn
        self.forfattare = forfattare


class Avhandling(Bok):
    """ Klassen modellerar en magisteravhandling """

    def __init__(self, namn: str, forfattare: str, vitsord: int):
        super().__init__(namn, forfattare)
        self.vitsord = vitsord

```

Konstruktorn i `Avhandling`-klassen anropar konstruktorn i basklassen `Bok` med argumenten för `namn` och `forfattare`. Dessutom anger konstruktören i den härledda klassen värdet för attributet `vitsord`. Detta kan naturligtvis inte vara en del av basklassens konstruktor, eftersom basklassen inte har något sådant attribut.

Ovanstående klass kan användas på följande sätt:


```python

# Testar
if __name__ == "__main__":
    avhandling = Avhandling("Python och Universum", "Peter Python", 3)

    # Skriv ut attributens värden
    print(avhandling.namn)
    print(avhandling.forfattare)
    print(avhandling.vitsord)

```

<sample-output>

Python och Universum
Peter Python
3

</sample-output>

Även om en härledd klass överstyr en metod i sin basklass kan den härledda klassen fortfarande anropa den åsidosatta metoden i basklassen. I följande exempel har vi ett grundläggande `Bonuskort` och ett särskilt `Platinumkort` för särskilt lojala kunder. Metoden `rakna_bonus` är åsidosatt i den härledda klassen, men den åsidosatta metoden anropar basmetoden:

```python

class Produkt:

    def __init__(self, namn: str, pris: float):
        self.namn = namn
        self.pris = pris

class Bonuskort:

    def __init__(self):
        self.kopta_produkter = []

    def tillsatt_produkt(self, produkt: Produkt):
        self.kopta_produkter.append(produkt)

    def rakna_bonus(self):
        bonus = 0
        for produkt in self.kopta_produkter:
            bonus += produkt.pris * 0.05

        return bonus

class Platinumkort(Bonuskort):

    def __init__(self):
        super().__init__()

    def rakna_bonus(self):
        # Anropar metoden i basklassen...
        bonus = super().rakna_bonus()

        # ...och tillsätter ännu fem procent till totalet
        bonus = bonus * 1.05
        return bonus


```

Bonusen för ett Platinumkort beräknas alltså genom att anropa den överstyrda metoden i basklassen och sedan lägga till 5 procent extra till basresultatet. Ett exempel på hur dessa klasser används:

```python
if __name__ == "__main__":
    kort = Bonuskort()
    kort.tillsatt_produkt(Produkt("Bananer", 6.50))
    kort.tillsatt_produkt(Produkt("Mandariner", 7.95))
    bonus = kort.rakna_bonus()

    kort2 = Platinumkort()
    kort2.tillsatt_produkt(Produkt("Bananer", 6.50))
    kort2.tillsatt_produkt(Produkt("Mandariner", 7.95))
    bonus2 = kort2.rakna_bonus()

    print(bonus)
    print(bonus2)
```

<sample-output>

0.7225
0.7586250000000001

</sample-output>

<programming-exercise name='Bärbar dator' tmcname='osa10-01_barbar_dator'>

I uppgiftsbotten finns en klassdefinition för en `Dator`, som har attributen `modell` och `snabbhet`.

Skapa klassen `BarbarDator`, som _ärver_ klassen `Dator`. Den nya klassens konstruktor ska ta ett tredgje argument, `vikt`, av typen heltal.

Skapa också en `__str__`-metod i klassdefinitionen. Se exemplet nedan för det förväntade formatet av strängen som skrivs ut.

Exempel:

```python
barbar = BarbarDator("NoteBook Pro15", 1500, 2)
print(barbar)
```

<sample-output>

NoteBook Pro15, 1500 MHz, 2 kg

</sample-output>

</programming-exercise>

<programming-exercise name='Spelmuseum' tmcname='osa10-02_spelmuseum'>

I uppgiftsbotten finns klassdefinitioner för `Datorspel` och `Spelforrad`. Spelforrads-objekt används för att förvara Datorspel-objekt.

Bekanta dig med dessa klasser. Definiera sedan klassen `Spelmuseum`, som ärver klassen `Spelforrad`.

Spelmuseum-klassen ska _överstyra_ metoden `lista_spel()`, så att den returnerar en lista av endast de spel som är gjorda innan år 1990.

Dessutom ska den nya klassen ha en konstruktor som _anropar konstruktorn från överklassen Spelforrad_. Konstruktorn tar inga argument.

Exempel:

```python
museum = Spelmuseum()
museum.tillsatt_spel(Datorspel("Pacman", "Namco", 1980))
museum.tillsatt_spel(Datorspel("GTA 2", "Rockstar", 1999))
museum.tillsatt_spel(Datorspel("Bubble Bobble", "Taito", 1986))
for spel in museum.lista_spel():
    print(spel.namn)
```

<sample-output>

Pacman
Bubble Bobble

</sample-output>

</programming-exercise>

<programming-exercise name='Arean' tmcname='osa10-03_arean'>

I uppgiftsbotten finns en klassdefinition för `Rektangel` som representerar en [rektangelform](https://sv.wikipedia.org/wiki/Rektangel). Klassen används på följande sätt:

```python
rektangel = Rektangel(2, 3)
print(rektangel)
print("area:", rektangel.area())
```

<sample-output>

rektangel 2x3
area: 6

</sample-output>

## Kvadrat

Skapa en klass `Kvadrat` som ärver klassen `Rektangel`. Sidorna på en [kvadrat](https://sv.wikipedia.org/wiki/Kvadrat) har alla samma längd, alltså är den en speciell sort av rektangel. Den nya klassen ska inte innehålla nya attribut!

Kvadrat-objekt används på följande sätt:

```python
kvadrat = Kvadrat(4)
print(kvadrat)
print("area:", kvadrat.area())
```

<sample-output>

kvadrat 4x4
area: 16

</sample-output>

</programming-exercise>

<programming-exercise name='Ordspel' tmcname='osa10-04_ordspel'>

Uppgiftsbotten innehåller klassdefinitionen för en `Ordspel`, som erbjuder enkel funktionalitet för att spela olika ordbaserade spel:

```python
import random

class Ordspel():
    def __init__(self, rundor: int):
        self.vinster1 = 0
        self.vinster2 = 0
        self.rundor = rundor

    def rundans_vinnare(self, spelare1_ord: str, spelare2_ord: str):
        # vi lottar ut en vinnare
        return random.randint(1, 2)

    def spela(self):
        print("Ordspel:")
        for i in range(1, self.rundor+1):
            print(f"runda {i}")
            svar1 = input("spelare1: ")
            svar2 = input("spelare2: ")

            if self.rundans_vinnare(svar1, svar2) == 1:
                self.vinster1 += 1
                print("spelare 1 vann")
            elif self.rundans_vinnare(svar1, svar2) == 2:
                self.vinster2 += 1
                print("spelare 2 vann")
            else:
                pass # oavgjort

        print("spelet är över, vinster:")
        print(f"spelare 1: {self.vinster1}")
        print(f"spelare 2: {self.vinster2}")
```

Spelet spelas enligt följande:

```python
s = Ordspel(3)
s.spela()
```

Exempel:

<sample-output>

Ordspel:
runda 1
spelare1: **långtord**
spelare2: **??**
spelare 2 vann
runda 2
spelare1: **jag är bäst**
spelare2: **va?**
spelare 1 vann
runda 3
spelare1: **vem vinner**
spelare2: **jag**
spelare 1 vann
spelet är över, vinster:
spelare 1: 2
spelare 2: 1

</sample-output>

I denna ”grundläggande” version av spelet avgörs vinnaren slumpmässigt. Spelarnas insatser har ingen inverkan på resultatet.

## Längsta ordet vinner

Definiera en klass som heter `LangstaOrdet`. Det är en version av spelet där den som skriver in det längsta ordet i varje omgång vinner.

Den nya versionen av spelet implementeras genom att ärva `Ordspel`-klassen. Metoden `rundans_vinnare` bör också överstyras på lämpligt sätt. Den nya klassen är uppbyggd på följande sätt:

```python
class LangstaOrdet(Ordspel):
    def __init__(self, rundor: int):
        super().__init__(rundor)

    def rundans_vinnare(self, spelare1_ord: str, spelare2_ord: str):
        # koden som avgör vinnaren här
```

Exempel på hur spelet fungerar:

```python
s = LangstaOrdet(3)
s.spela()
```

<sample-output>

Ordspel:
runda 1
spelare1: **kort**
spelare2: **långtord**
spelare 2 vann
runda 2
spelare1: **ord**
spelare2: **va?**
runda 3
spelare1: **jag är bäst**
spelare2: **nej jag!**
spelare 1 vann
spelet är över, vinster:
spelare 1: 1
spelare 2: 1

</sample-output>

## Flest vokaler vinner

Definiera en annan Ordspel-klass med namnet `FlestVokaler`. I den här versionen av spelet vinner den som har klämt in flest vokaler i sitt ord.

## Sten sax påse

Definiera slutligen klassen `StenSaxPase` som låter dig spela ett spel av [Sten, sax, påse](https://sv.wikipedia.org/wiki/Sten,_sax,_p%C3%A5se).

Spelets regler är följande:

- sten vinner påse (stenen kan förstöra saxen men saxen kan inte klippa stenen)
- påse vinner sten (påsen kan omsluta stenen)
- sax vinner påse (saxen kan klippa påsen)

Om inmatningen från en spelare är ogiltig förlorar den omgången. Om båda spelarna skriver in något annat än sten, sax eller påse blir resultatet oavgjort.

Exempel på hur spelet spelas:

```python
s = StenSaxPase(4)
s.spela()
```

<sample-output>

Ordspel:
runda 1
spelare1: **sten**
spelare2: **sten**
runda 2
spelare1: **sten**
spelare2: **påse**
spelare 2 vann
runda 3
spelare1: **sax**
spelare2: **påse**
spelare 1 vann
runda 4
spelare1: **påse**
spelare2: **dynamit**
spelare 1 vann
spelet är över, vinster:
spelare 1: 2
spelare 2: 1

</sample-output>

</programming-exercise>
