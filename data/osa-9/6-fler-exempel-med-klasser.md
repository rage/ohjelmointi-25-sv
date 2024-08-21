---
path: '/osa-9/6-fler-exempel-med-klasser'
title: 'Fler exempel med klasser'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Är du bekant med några fler exempel på klasser och objekt
- Kan du använda standardvärden för parametrar i dina metoder

</text-box>

Följande exempel består av två klasser. Klassen `Punkt` är en modell för en punkt i ett tvådimensionellt rum. Klassen `Stracka` är en modell för ett linjesegment mellan två punkter. Koden nedan är kommenterad, läs gärna kommentarerna för att förstå hur klasserna fungerar.

```python
import math

class Punkt:
    """ Klassen representerar en punkt i ett tvådimensionellt rum """

    def __init__(self, x: float, y: float):
        # Attributen är offentliga, eftersom vilket värde som helst kan användas som värde för x och y.
        self.x = x
        self.y = y

    # Denna klassmetod returnerar en ny punkt vid origo (0, 0)
    # Det är möjligt att returnera en ny instans av klassen inifrån klassen
    @classmethod
    def origo(cls):
        return Punkt(0, 0)

    # Klassmetoden skapar en ny punkt baserad på den givna punkten
    # Den nya punkten är en spegelbild av den givna punkten på en eller båda axlarna.
    # Till exempel är punkten (1, 3) speglad på x-axeln (1, -3)
    @classmethod
    def spegelbild(cls, punkt, spegla_x: bool, spegla_y: bool):
        x = punkt.x
        y = punkt.y
        if spegla_x:
            y = -y
        if spegla_y:
            x = -x

        return Punkt(x, y)

    def __str__(self):
        return f"({self.x}, {self.y})"

class Stracka:
    """ Klassen modellerar en sträcka i ett tvådimensionellt rum """

    def __init__(self, borjan: Punkt, slut: Punkt):
        # Dessa attribut är offentliga eftersom två valfria punkter kan accepteras
        self.borjan = borjan
        self.slut = slut

    # Denna metod använder Pythagoras sats för att beräkna längden på sträckan
    def langd(self):
        summa = (self.slut.x - self.borjan.x) ** 2 + (self.slut.y - self.borjan.y) ** 2
        return math.sqrt(summa)

    # Metoden returnerar mitten av sträckan
    def medelpunkt(self):
        medelx = (self.borjan.x + self.slut.x) / 2
        medely = (self.borjan.y + self.slut.y) / 2
        return Punkt(medelx, medely)

    def __str__(self):
        return f"{self.borjan} ... {self.slut}"
```

```python
punkt = Punkt(1,3)
print(punkt)

origo = Punkt.origo()
print(origo)

punkt2 = Punkt.spegelbild(punkt, True, True)
print(punkt2)

stracka = Stracka(punkt, punkt2)
print(stracka.langd())
print(stracka.medelpunkt())
print(stracka)
```

<sample-output>

(1, 3)
(0, 0)
(-1, -3)
6.324555320336759
(0.0, 0.0)
(1, 3) ... (-1, -3)

</sample-output>

## Standardvärden för parametrar

I Python-programmering kan du i allmänhet ange ett standardvärde för alla parametrar. Standardvärden kan användas i både funktioner och metoder.

Om en parameter har ett standardvärde behöver du inte inkludera ett värde som ett argument när du anropar funktionen. Om ett argument anges ignoreras standardvärdet. Om inte, används standardvärdet.

Default-värden används ofta i konstruktörer. Om man kan förvänta sig att all information inte är tillgänglig när ett objekt skapas är det bättre att inkludera ett standardvärde i definitionen av konstruktörsmetoden än att tvinga klienten att ta hand om problemet. Detta gör det enklare att använda klassen ur klientens synvinkel, men det säkerställer också objektets integritet. Med ett fastställt standardvärde kan vi t.ex. vara säkra på att ett "tomt" värde alltid är detsamma, såvida inte klienten specifikt vill ange något annat. Om ett standardvärde inte anges är det upp till kunden att tillhandahålla ett "tomt" värde. Det kan t.ex. vara en tom sträng `""`, det speciella tomma objektet `None` eller strängen `"inte angivet"`.

Låt oss ta en titt på ännu en klass som representerar en studerande. När ett nytt Studerande-objekt skapas måste klienten ange ett namn och ett studerandenummer. Studerandenumret är privat och ska inte ändras i efterhand. Dessutom har ett Studerande-objekt attribut för studiepoäng och anteckningar, vilka har standardvärden som anges i konstruktorn. Nya värden kan skickas som argument till konstruktören, men de kan också utelämnas så att standardvärdena används istället. Titta gärna på kommentarerna i koden för att bättre förstå vad varje metod gör.

```python
class Studerande:
    """ Modellerar en endaste studerande """

    def __init__(self, namn: str, studerandenummer: str, studiepoang:int = 0, anteckningar:str = ""):
        # Kallar sättar-metoden
        self.namn = namn

        if len(studerandenummer) < 5:
            raise ValueError("Studerandenumret ska ha minst 5 tecken")

        self.__studerandenummer = studerandenummer

        # Kallar sättar-metoden
        self.studiepoang = studiepoang

        self.__anteckningar = anteckningar

    @property
    def namn(self):
        return self.__namn

    @namn.setter
    def namn(self, namn):
        if namn != "":
            self.__namn = namn
        else:
            raise ValueError("Namnet kan inte vara tomt")

    @property
    def studerandenummer(self):
        return self.__studerandenummer

    @property
    def studiepoang(self):
        return self.__studiepoang

    @studiepoang.setter
    def studiepoang(self, sp):
        if sp >= 0:
            self.__studiepoang = sp
        else:
            raise ValueError("Studiepoäng kan inte vara ett negativt tal")

    @property
    def anteckningar(self):
        return self.__anteckningar

    @anteckningar.setter
    def anteckningar(self, anteckningar):
        self.__anteckningar = anteckningar

    def sammanfattning(self):
        print(f"Studerande {self.__namn} ({self.studerandenummer}):")
        print(f"- studiepoäng {self.__studiepoang}")
        print(f"- anteckningar: {self.anteckningar}")
```

```python
# Skickar endast namnet och studerandenumret
studerande1 = Studerande("Sam Studerande", "12345")
studerande1.sammanfattning()

# Skickar namnet, studerandenummer och studiepoäng
studerande2 = Studerande("Saul Studerande", "54321", 25)
studerande2.sammanfattning()

# Skickar alla uppgifter
studerande3 = Studerande("Sara Studerande", "99999", 140, "tillägstid i tenter")
studerande3.sammanfattning()

# Skickar anteckningar, men inte studiepoäng
# Obs: parametern måste nu bli namngiven när argumenten inte är i ordning
studerande4 = Studerande("Saga Studerande", "98765", anteckningar="avlägsen studieår 20-21")
studerande4.sammanfattning()
```

<sample-output>

Studerande Sam Studerande (12345):
- studiepoäng 0
- anteckningar:
Studerande Saul Studerande (54321):
- studiepoäng 25
- anteckningar:
Studerande Sara Studerande (99999):
- studiepoäng 140
- anteckningar: tillägstid i tenter
Studerande Saga Studerande (98765):
- studiepoäng 0
- anteckningar: avlägsen studieår 20-21

</sample-output>

OBS: Det finns ingen sättar-metod för attributet `studerande_nummer` eftersom det inte är meningen att studerandenumret ska ändras.

Det finns en ganska betydande hake när man använder standardvärden för parametrar. Följande exempel som modellerar ännu en typ av studerande kommer att belysa detta mer:

```python
class Studerande:
    def __init__(self, namn, gjorda_kurser=[]):
        self.namn = namn
        self.gjorda_kurser = gjorda_kurser

    def tillsatt_prestation(self, kurs):
        self.gjorda_kurser.append(kurs)
```

```python
studerande1 = Studerande("Sam Studerande")
studerande2 = Studerande("Saul Studerande")

studerande1.tillsatt_prestation("ItP")
studerande1.tillsatt_prestation("Tira")

print(studerande1.gjorda_kurser)
print(studerande2.gjorda_kurser)
```

<sample-output>

['ItP', 'Tira']
['ItP', 'Tira']

</sample-output>

Om du lägger till slutförda kurser i Sams lista läggs dessa kurser också till i Sauls lista. Faktum är att dessa två är exakt samma lista, eftersom Python återanvänder referensen som lagras i standardvärdet. Att skapa de två nya Studerande-objekten i exemplet ovan är likvärdigt med följande:

```python
kurser = []
studerande1 = Studerande("Sam Studerande", kurser)
studerande2 = Studerande("Saul Studerande", kurser)
```

Standardvärdena för parametrar bör aldrig vara instanser av mer komplicerade, föränderliga datastrukturer, t.ex. listor. Problemet kan kringgås genom att göra följande ändringar i konstruktorn för klassen `Studerande`:

```python
class Studerande:
    def __init__(self, namn, gjorda_kurser=None):
        self.namn = namn
        if gjorda_kurser is None:
            self.gjorda_kurser = []
        else:
            self.gjorda_kurser = gjorda_kurser

    def tillsatt_prestation(self, kurs):
        self.gjorda_kurser.append(kurs)
```

```python
studerande1 = Studerande("Sam Studerande")
studerande2 = Studerande("Saul Studerande")

studerande1.tillsatt_prestation("ItP")
studerande1.tillsatt_prestation("Tira")

print(studerande1.gjorda_kurser)
print(studerande2.gjorda_kurser)
```

<sample-output>

['ItP', 'Tira']
[]

</sample-output>

## Den stora finalen

Fastän följande övning avslutar den här delen av materialet, så har de tekniker som krävs för att lösa den redan behandlats i avsnittet som heter [Objekt som attribut](https://rage.github.io/ohjelmointi-24-sv/osa-9/2-objekt-som-attribut). Du behöver inte använda `@property`-dekoratorn eller standardvärden för parametrar i den här övningen. Den här övningen är mycket lik övningarna "en presentask" och "den kortaste personen i rummet".

<programming-exercise name='Sak, Resväska och Lastutrymme' tmcname='osa09-15_sak_resvaska_lastutrymme'>

I den här uppgiftsserien kommer du skapa klasserna `Sak`, `Resvaska` och `Lastutrymme`, vilka låter dig öva vidare på att jobba på objekt som innehåller referenser till andra objekt.

## Sak

Skapa klassen `Sak`, som används för att skapa saker av olika sorter. Varje sak har ett namn och en vikt (i kg).

Klassen ska fungera enligt följande:

```python
bok = Sak("ABC bok", 2)
telefon = Sak("Nokia 3210", 1)

print("Bokens namn:", bok.namn())
print("Bokens vikt:", bok.vikt())

print("Bok:", bok)
print("Telefon:", telefon)
```

Programmets utskrift borde vara följande:

<sample-output>

Bokens namn: ABC bok
Bokens vikt: 2
Bok: ABC bok (2 kg)
Telefon: Nokia 3210 (1 kg)

</sample-output>

En `Sak` ska alltså innehålla metoderna `vikt` och `namn`, som returnerar värden som lagras i dessa attribut.

Namnet och vikten ska vara inkapslade inom klassen. Följande ska inte fungera:

```python
bok = Sak("ABC bok", 2)
bok.vikt = 10
```

## Resväska

Skapa klassen `Resvaska`. Det ska vara möjligt att packa saker i resväskan. En räsväska har dessutom en maximal vikt för saker som lagras i den.

Lägg till följande till klassen:

- en konstruktor, som tar maximal vikt som ett argument
- metoden `tillsatt_sak`, som lägger till saken givet som argument till resväskan. Metoden har inget returvärde.
- metoden `__str__`, som returnerar en sträng i formatet "x saker (y kg)"

Klassen ska se till att den sammanlagda vikten av de föremål som förvaras i en `Resvaska` inte överstiger den maximala vikt som har ställts in för den instansen. Om den maximala vikten skulle överskridas när `tillsatt_sak`-metoden anropas, ska det nya föremålet inte läggas till i resväskan.

Klassen ska fungera enligt följande:

```python
bok = Sak("ABC bok", 2)
telefon = Sak("Nokia 3210", 1)
tegelsten = Sak("Tegelsten", 4)

resvaska = Resvaska(5)
print(resvaska)

resvaska.tillsatt_sak(bok)
print(resvaska)

resvaska.tillsatt_sak(telefon)
print(resvaska)

resvaska.tillsatt_sak(tegelsten)
print(resvaska)
```

Programmets utskrift borde vara följande:

<sample-output>

0 saker (0 kg)
1 saker (2 kg)
2 saker (3 kg)
2 saker (3 kg)

</sample-output>

## Språkvård

Meddelandet ”1 saker” är inte särskilt grammatiskt. Istället borde det stå ”1 sak”. Gör de ändringar som krävs i din `__str__`-metod.

Föregående exempel borde nu skriva ut:

<sample-output>

0 saker (0 kg)
1 sak (2 kg)
2 saker (3 kg)
2 saker (3 kg)

</sample-output>

## Alla saker

Tillägg följande metoder till definitionen av din `Resvaska`-klass:

- `skriv_ut_saker`, som skriver ut alla saker som lagras i resväskan
- `vikt`, som returnerar ett heltalsnummer som representerar den totala vikten av sakerna i resväskan

Klassen borde nu fungera med följande program:

```python
bok = Sak("ABC bok", 2)
telefon = Sak("Nokia 3210", 1)
tegelsten = Sak("Tegelsten", 4)

resvaska = Resvaska(10)
resvaska.tillsatt_sak(bok)
resvaska.tillsatt_sak(telefon)
resvaska.tillsatt_sak(tegelsten)

print("I resväskan finns följande saker:")
resvaska.skriv_ut_saker()
vikt_tot = resvaska.vikt()
print(f"Totalvikt: {vikt_tot} kg")
```

Ovanstående programs utskrift borde ge följande resultat:

<sample-output>

I resväskan finns följande saker:
ABC bok (2 kg)
Nokia 3210 (1 kg)
Tegelsten (4 kg)
Totalvikt: 7 kg

</sample-output>

Om du har implementerat din `Resvaska`-klass med fler än två instansvariabler, gör de ändringar som krävs så att varje instans endast har två dataattribut: den maximala vikten och en lista över föremålen i den.

## Den tyngsta saken

Lägg till en ny metod i din `Resvaska`-klass: `tyngsta_saken` ska returnera den `sak` som är tyngst. Om det finns två eller flera föremål med samma vikt kan metoden returnera vilket som helst av dessa. Metoden ska returnera en referens till ett objekt. Om resväskan är tom ska metoden returnera `None`.

Din klass borde nu fungera med följande program:

```python
bok = Sak("ABC bok", 2)
telefon = Sak("Nokia 3210", 1)
tegelsten = Sak("Tegelsten", 4)

resvaska = Resvaska(10)
resvaska.tillsatt_sak(bok)
resvaska.tillsatt_sak(telefon)
resvaska.tillsatt_sak(tegelsten)

tyngsta = resvaska.tyngsta_saken()
print(f"Tyngsta saken: {tyngsta}")
```

Programmets utskrift borde nu vara följande:

<sample-output>

Tyngsta saken: Tegelsten (4 kg)

</sample-output>

## Lastutrymme

Skapa klassen `Lastutrymme`, som har följande metoder:

- en konstruktor, som får en maximalvikt
- metoden `tillsatt_resvaska`, som lägger till resväskan den får som argument till lastutrymmet
- metoden `__str__`, som returnerar en sträng i formatet "x resväskor, rum för y kg"

Klassen bör se till att den sammanlagda vikten av de föremål som lagras i ett `Lastutrymme` inte överstiger den maximala vikt som har ställts in för den instansen. Om den maximala vikten skulle överskridas när `tillsatt_resvaska`-metoden anropas, ska den nya resväskan inte läggas till i lastutrymmet.

Din klass borde nu fungera med följande program:

```python
lastutrymme = Lastutrymme(1000)
print(lastutrymme)

bok = Sak("ABC bok", 2)
telefon = Sak("Nokia 3210", 1)
tegelsten = Sak("Tegelsten", 4)

adas_vaska = Resvaska(10)
adas_vaska.tillsatt_sak(bok)
adas_vaska.tillsatt_sak(telefon)

peters_vaska = Resvaska(10)
peters_vaska.tillsatt_sak(tegelsten)

lastutrymme.tillsatt_resvaska(adas_vaska)
print(lastutrymme)

lastutrymme.tillsatt_resvaska(peters_vaska)
print(lastutrymme)
```

<sample-output>

0 resväskor, rum för 1000 kg
1 resväska, rum för 997 kg
2 resväskor, rum för 993 kg

</sample-output>

## Lastutrymmets innehåll

Lägg till metoden `skriv_ut_saker`, till din `Lastutrymme`-klass. Metoden ska skriva ut alla saker i alla resväskor i lastutrymmet.

Din klass borde nu fungera med följande program:

```python
bok = Sak("ABC bok", 2)
telefon = Sak("Nokia 3210", 1)
tegelsten = Sak("Tegelsten", 4)

adas_vaska = Resvaska(10)
adas_vaska.tillsatt_sak(bok)
adas_vaska.tillsatt_sak(telefon)

peters_vaska = Resvaska(10)
peters_vaska.tillsatt_sak(tegelsten)

lastutrymme = Lastutrymme(1000)
lastutrymme.tillsatt_resvaska(adas_vaska)
lastutrymme.tillsatt_resvaska(peters_vaska)

print("Väskorna i lastutrymmet innehåller följande saker:")
lastutrymme.skriv_ut_saker()
```

Utskriften för ovanstående program borde vara följande:


<sample-output>

Väskorna i lastutrymmet innehåller följande saker:
ABC bok (2 kg)
Nokia 3210 (1 kg)
Tegelsten (4 kg)

</sample-output>

</programming-exercise>

Svara avslutningsvis på följande frågeformulär:

<quiz id="34723602-dd55-54df-914d-bdd2037722f8"></quiz>
