---
path: '/osa-9/2-oliot-attribuuttina'
title: 'Objekt som attribut '
hidden: False
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Vet du hur man använder objekt som attribut i andra objekt
- Kommer du vara bekant med nyckelordet `None`

</text-box>

Vi har redan sett exempel på klasser som har listor som attribut. Eftersom det alltså inte finns något som hindrar oss från att inkludera mutabla objekt som attribut i våra klasser, kan vi lika gärna använda instanser av våra egna klasser som attribut i andra klasser som vi själva har definierat. I följande exempel kommer vi att definiera klasserna `Kurs`, `Studerande` och `SlutfordKurs`. En slutförd kurs använder sig av de två första klasserna. Klassdefinitionerna är mycket korta och enkla för att vi bättre ska kunna koncentrera oss på tekniken att använda instanser av våra egna klasser som attribut.

Vi kommer att anta att varje klass definieras i en separat fil.

Först definierar vi klassen `Kurs` i en fil med namnet `kurs.py`:

```python
class Kurs:
    def __init__(self, namn: str, kod: str, studiepoang: int):
        self.namn = namn
        self.kod = kod
        self.studiepoang = studiepoang
```

Till näst, klassen `Studerande` i en fil med namnet `studerande.py`:

```python
class Studerande:
    def __init__(self, namn: str, studerandenummer: str, studiepoang: int):
        self.namn = namn
        self.studerandenummer = studerandenummer
        self.studiepoang = studiepoang
```

Slutligen är klassen `SlutfordKurs` definierad i en fil med namned `SlutfordKurs.py`. Eftersom den använder de två andra klasserna, måste de importeras innan de kan användas:

```python
from kurs import Kurs
from studerande import Studerande

class SlutfordKurs:
    def __init__(self, studerande: Studerande, kurs: Kurs, vitsord: int):
        self.studerande = studerande
        self.kurs = kurs
        self.vitsord = vitsord
```

Här är ett exempel av en huvudfunktion som lägger till några slutförda kurser i en lista:

```python
from slutfordkurs import SlutfordKurs
from kurs import Kurs
from studerande import Studerande

# Vi skapar en lista av studeranden
studeranden = []
studeranden.append(Studerande("Olle", "1234", 10))
studeranden.append(Studerande("Peter", "3210", 23))
studeranden.append(Studerande("Lena", "9999", 43))
studeranden.append(Studerande("Tina", "3333", 8))

# Kurssen Introduktion till Programmering
itp = Kurs("Introduktion till Programmering", "itp1", 5)

# Vi ger prestationer för varje student, med vitsordet 3 till alla
prestationer = []
for studerande in studeranden:
    prestationer.append(SlutfordKurs(studerande, itp, 3))

# Vi skriver ut studerandenas namn för varje avklarad kurs
for prestation in prestationer:
    print(prestation.studerande.namn)
```

<sample-output>

Olle
Peter
Lena
Tina

</sample-output>

Vad exakt händer med alla prickar på raden `print(kurs.studerande.namn)`?

* `kurs` är en instans av klassen `SlutfordKurs`
* `studerande` refererar till ett attribut i objektet `SlutfordKurs`, som är ett objekt av typen `Studerande`
* attributnamnet i `Studerande`-objektet innehåller namnet på studenten

## När är en import nödvändig?

I exemplen ovan förekommer en `import`-sats ganska många gånger:

```python
from slutfordkurs import SlutfordKurs
from kurs import Kurs
from studerande import Studerande

# kod
```

En importsats är bara nödvändig när man använder kod som är definierad någonstans utanför den aktuella filen (eller Python-tolksessionen). Detta inkluderar situationer där vi vill använda något som är definierat i Pythons standardbibliotek. Modulen `math` innehåller till exempel vissa matematiska operationer:

```python
import math

x = 10
print(f"kvadratroten av {x} är {math.sqrt(x)}")
```

I exemplet ovan antog vi att de tre klasserna definierades i var sin fil och att huvudfunktionen kördes från ytterligare en fil. Det var därför `import`-satserna var nödvändiga.

Om all programkod skrivs i samma fil, vilket de flesta övningarna i den här kursen rekommenderar, behöver du **inte** `import`-satser för att använda de klasser du har definierat.

Ifall du märker dig själv skriva något i stil med

```python
from person import Person

# kod
```

är det sannolikt att du förstått nånting felaktigt. Ifall du behöver en uppfriskare så introducerades `import` deklarationen för första gången i [del 7](/osa-7/1-moduulit/) av kursmaterialet.

<programming-exercise name='Lemmikit' tmcname='osa09-06_lemmikki'>

I uppgiftsbotten finns två klasser, `Person` och `Husdjur`. Varje person har ett djur. Ändra `__str__`-metoden i `Person` klassen, så att metoden returnerar en sträng som berättar personens namn plus husdjurets namn och ras enligt exemplet nedan.

Strängen som returneras av metoden _måste följa det format som anges nedan exakt_.

```python
hulda = Husdjur("Hulda", "blandrasig hund")
ludde = Person("Ludde", hulda)

print(ludde)
```

<sample-output>

Ludde, vars kompis är Hulda, en blandrasig hund

</sample-output>

**OBS:** alla klassdefinitioner finns i samma textfil. Du ska inte behöva `import`era något.

</programming-exercise>

## En lista med objekt som attribut till ett objekt

I exemplen ovan använde vi enstaka instanser av andra klasser som attribut: en Person har ett enda Husdjur som attribut, och en SlutfordKurs har en Studerande och en Kurs som attribut.

I objektorienterad programmering är det ofta så att vi vill ha en samling objekt som attribut. Till exempel följer relationen mellan ett idrottslag och dess spelare detta mönster:

```python
class Spelare:
    def __init__(self, namn: str, mal: int):
        self.namn = namn
        self.mal = mal

    def __str__(self):
        return f"{self.namn} (mål {self.mal})"

class Lag:
    def __init__(self, namn: str):
        self.namn = namn
        self.spelare = []

    def tillsatt_spelare(self, spelare: Spelare):
        self.spelare.append(spelare)

    def sammanfattning(self):
        mal = []
        for spelare in self.spelare:
            mal.append(spelare.mal)
        print("Lag:", self.namn)
        print("Spelare:", len(self.spelare))
        print("Spelarnas målmängd:", mal)
```

Ett exempel på hur vår klass fungerar:

```python
gumboll = Lag("Gumtäkts boll")
gumboll.tillsatt_spelare(Spelare("Erik", 10))
gumboll.tillsatt_spelare(Spelare("Emilia", 22))
gumboll.tillsatt_spelare(Spelare("Anton", 1))
gumboll.sammanfattning()
```

<sample-output>

Lag: Gumtäkts boll
Spelare: 3
Spelarnas målmängd: [10, 22, 1]

</sample-output>

<programming-exercise name='Lahjapakkaus' tmcname='osa09-07_lahjapakkaus'>

I den här övningen får du öva på att slå in presenter. Du kommer att skriva två klasser: `Present` och `Lada`. En present har ett namn och en vikt, och en låda innehåller presenter.

## Del 1: Presentklassen

Definiera klassen `Present` som kan användas för att representera olika typer av presenter. Klassdefinitionen bör innehålla attribut för presentens namn och vikt (i kg). Instanser av klassen ska fungera på följande sätt:

```python
bok = Present("ABC bok", 2)

print("Presenens namn:", bok.namn)
print("Presenens vikt:", bok.vikt)
print("Present:", bok)
```

Utskriften borde vara

<sample-output>

Presenens namn: ABC bok
Presenens vikt: 2
Present: ABC bok (2 kg)

</sample-output>

## Del 2: Lådklassen

Definiera klassen `Lada`. Du ska kunna lägga presenter i lådan och lådan ska hålla reda på den sammanlagda vikten av presenterna i den. Klassdefinitionen bör innehålla dessa metoder:

- `tillsatt_present(self, present: Present)`, som tillsätter present givet som argument till lådan. Metoden returnerar inget värde.
- `totalvikt(self)`, som returnerar den totala vikten av presenterna i lådan.

Följande är ett exempel av koden i användning:

```python
bok = Present("ABC bok", 2)

lada = Lada()
lada.tillsatt_present(bok)
print(lada.totalvikt())

cd_skiva = Present("Pink Floyd: Dark side of the moon", 1)
lada.tillsatt_present(cd_skiva)
print(lada.totalvikt())
```

<sample-output>

2
3

</sample-output>

</programming-exercise>

## None: en referens till ingenting

I Python-programmering refererar alla initialiserade variabler till ett objekt. Det finns dock oundvikligen situationer där vi måste referera till något som inte existerar, utan att orsaka fel. Nyckelordet `None` representerar just ett sådant "tomt" objekt.

Låt oss fortsätta från exemplet med lag och spelare ovan och anta att vi vill lägga till en metod för att söka efter spelare i laget med hjälp av spelarens namn. Om ingen sådan spelare hittas kan det vara vettigt att returnera `None`:

```python
class Spelare:
    def __init__(self, namn: str, mal: int):
        self.namn = namn
        self.mal = mal

    def __str__(self):
        return f"{self.namn} (mål {self.mal})"

class Lag:
    def __init__(self, namn: str):
        self.namn = namn
        self.spelare = []

    def tillsatt_spelare(self, spelare: Spelare):
        self.spelare.append(spelare)

    def sok(self, namn: str):
        for spelare in self.spelare:
            if spelare.namn == namn:
                return spelare
        return None
```

Låt oss testa vår funktion:

```python
gumboll = Lag("Gumtäkts boll")
gumboll.tillsatt_spelare(Spelare("Erik", 10))
gumboll.tillsatt_spelare(Spelare("Emilia", 22))
gumboll.tillsatt_spelare(Spelare("Anton", 1))

spelare1 = gumboll.sok("Anton")
print(spelare1)
spelare2 = gumboll.sok("Johan")
print(spelare2)
```

<sample-output>

Anton (mål 1)
None

</sample-output>

Var dock försiktig med `None`. Det kan ibland orsaka mer problem än det löser. Det är ett vanligt programmeringsfel att försöka komma åt en metod eller ett attribut via en referens som utvärderas till `None`:

```python
gumboll = Lag("Gumtäkts boll")
gumboll.tillsatt_spelare(Spelare("Erik", 10))

spelare = gumboll.sok("Johan")
print(f"Johans målmängd {spelare.mal}")
```

Exekverande av ovanstående skulle orsaka ett fel:

<sample-output>

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'NoneType' object has no attribute 'mal'

</sample-output>

Det är en god idé att kontrollera om det finns `None` innan du försöker komma åt några attribut eller metoder för returvärden: 

```python
gumboll = Lag("Gumtäkts boll")
gumboll.tillsatt_spelare(Spelare("Erik", 10))

spelare = gumboll.sok("Johan")
if spelare is not None:
    print(f"Johans målmängd {p.mal}")
else:
    print(f"Johan spelar inte i Gumtäkts boll :(")
```

<sample-output>

Johan spelar inte i Gumtäkts boll :(

</sample-output>

<programming-exercise name='Huoneen lyhin' tmcname='osa09-08_huoneen_lyhin'>

Övningsmallen innehåller klassen `Person`. En person har ett namn och en höjd. I denna övning kommer du att implementera klassen `Rum`. Du kan lägga till valfritt antal personer i ett rum, och du kan också söka efter och ta bort den kortaste personen i rummet.

## Del 1: Rum

Skapa klassen `Rum`, som har en lista på personer som attribut och har följande metoder:

- `tillsatt(person: Person)` lägger till personen som anges som argument till rummet.
- `ar_tomt()` - Teturnerar värdet `True` eller `False`, beroende på om rummet är tomt.
- `skriv_ut_personer()` skriver ut innehållet av listan på personerna i rummet

Följande är ett exempel:

```python
rum = Rum()
print("Rummet tomt?", rum.ar_tomt())
rum.tillsatt(Person("Lena", 183))
rum.tillsatt(Person("Kenya", 182))
rum.tillsatt(Person("Alex", 186))
rum.tillsatt(Person("Nina", 172))
rum.tillsatt(Person("Tom", 185))
print("Rummet tomt?", rum.ar_tomt())
rum.skriv_ut_personer()
```

<sample-output>

Rummet tomt? True
Rummet tomt? False
I rummet finns 5 personer, totallängd 908 cm
Lena (183 cm)
Kenya (182 cm)
Alex (186 cm)
Nina (172 cm)
Tom (185 cm)

</sample-output>

## Del 2: kortaste personen

Definiera metoden kortast() inom klassdefinitionen `Rum`. Metoden ska returnera den kortaste personen i det rum som den anropas i. Om rummet är tomt ska metoden returnera `None`. Metoden ska _inte_ ta bort personen från rummet.

```python
rum = Rum()

print("Rummet tomt?", rum.ar_tomt())
print("Kortast:", rum.kortast())

rum.tillsatt(Person("Lena", 183))
rum.tillsatt(Person("Kenya", 182))
rum.tillsatt(Person("Nina", 172))
rum.tillsatt(Person("Alex", 186))

print()

print("Rummet tomt?", rum.ar_tomt())
print("Kortast:", rum.kortast())

print()

rum.skriv_ut_personer()
```

<sample-output>

Rummet tomt? True
Kortast: None

Rummet tomt? False
Kortast: Nina

I rummet finns 4 personer, totallängd 723 cm
Lena (183 cm)
Kenya (182 cm)
Nina (172 cm)
Alex (186 cm)

</sample-output>

## Del 3: Ta bort en person från rummet

Definiera metoden `ta_bort_kortaste`() inom klassdefinitionen för `Rum`. Metoden ska ta bort det kortaste `Person`-objektet från rummet och returnera referensen till objektet. Om rummet är tomt ska metoden returnera `None`.

```python
rum = Rum()

rum.tillsatt(Person("Lena", 183))
rum.tillsatt(Person("Kenya", 182))
rum.tillsatt(Person("Nina", 172))
rum.tillsatt(Person("Alex", 186))
rum.skriv_ut_personer()

print()

borttagen = rum.ta_bort_kortast()
print(f"Borttagen från rummet: {borttagen.namn}")

print()

rum.skriv_ut_personer()
```

<sample-output>

I rummet finns 4 personer, totallängd 723 cm
Lena (183 cm)
Kenya (182 cm)
Nina (172 cm)
Alex (186 cm)

Borttagen från rummet: Nina

I rummet finns 3 personer, totallängd 551 cm
Lena (183 cm)
Kenya (182 cm)
Alex (186 cm)

</sample-output>

**Tips**: [i del 4](/osa-4/3-listat#alkioiden-lisaaminen-ja-poistaminen) hittar du instruktioner för att ta bort föremål från en lista

**Tips2**: det är alltid möjligt att kalla en annan metod från samma klass inuti en metod. Följande borde fungera helt bra:

```python
class Rum:
    # ...
    def kortast(self):
        # kod

    def ta_bort_kortast(self):
        kortast_person = self.kortast()
        # ...
```

</programming-exercise>
