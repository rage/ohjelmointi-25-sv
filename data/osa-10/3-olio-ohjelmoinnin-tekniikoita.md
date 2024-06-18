---
path: '/osa-10/3-olio-ohjelmoinnin-tekniikoita'
title: 'Objektorienterade programmeringstekniker'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Tämän osion jälkeen

- Känner du till några av de olika användningsområdena för variabelnamnet `self`
- Vet du hur du överlagrar operatorer i dina egna klasser
- Kommer du att kunna skapa en iterabel klass

</text-box>

En klass kan innehålla en metod som returnerar ett objekt av samma klass. Nedan har vi t.ex. klassen `Produkt`, vars metod `reaprodukt` returnerar ett nytt Produkt-objekt med samma namn som det ursprungliga men med ett pris som är 25 % lägre:

```python
class Produkt:
    def __init__(self, namn: str, pris: float):
        self.__namn = namn
        self.__pris = pris

    def __str__(self):
        return f"{self.__namn} (pris {self.__pris})"

    def reaprodukt(self):
        nedsatt = Produkt(self.__namn, self.__pris * 0.75)
        return nedsatt
```

```python
banan1 = Produkt("Banan", 2.99)
banan2 = banan1.reaprodukt()
print(banan1)
print(banan2)
```

<sample-output>

Banan (pris 2.99)
Banan (pris 2.2425)

</sample-output>

Låt oss gå igenom syftet med variabeln `self`: inom en klassdefinition hänvisar den till själva objektet. Vanligtvis används den för att hänvisa till objektets egna egenskaper, dess attribut och metoder. Variabeln kan också användas för att hänvisa till hela objektet, till exempel om själva objektet måste returneras till klientkoden. I exemplet nedan har vi lagt till metoden `billigare` i klassdefinitionen. Den tar en annan Produkt som sitt argument och returnerar det billigare av de två:

```python
class Produkt:
    def __init__(self, namn: str, pris: float):
        self.__namn = namn
        self.__pris = pris

    def __str__(self):
        return f"{self.__namn} (pris {self.__pris})"

    @property
    def pris(self):
        return self.__pris

    def billigare(self, produkt):
        if self.__pris < produkt.pris:
            return self
        else:
            return produkt
```

```python
banan = Produkt("Banan", 2.99)
apelsin = Produkt("Apelsin", 3.95)
ananas = Produkt("Ananas", 5.25)

print(apelsin.billigare(banan))
print(apelsin.billigare(ananas))
```

<sample-output>

Banan (2.99)
Apelsin (3.95)

</sample-output>

Även om det här fungerar bra är det ett mycket specialiserat fall av att jämföra två objekt. Det skulle vara bättre om vi kunde använda Pythons jämförelseoperatorer direkt på dessa `Produkt`-objekt.

## Överlagring av operatorer

Python innehåller några speciellt namngivna inbyggda metoder för att arbeta med standardoperatorerna för aritmetik och jämförelse. Tekniken kallas operatörsöverlagring (eng. operator overloading). Om du vill kunna använda en viss operator på instanser av självdefinierade klasser kan du skriva en speciell metod som returnerar det korrekta resultatet av operatorn. Vi har redan använt den här tekniken med `__str__` metoden: Python vet att leta efter en metod som heter så här när en strängrepresentation av ett objekt efterfrågas.

Låt oss börja med operatorn > som talar om för oss om den första operanden är större än den andra. Klassdefinitionen `Produkt` nedan innehåller metoden `__gt__`, som är en förkortning av greater than. Denna speciellt namngivna metod ska returnera det korrekta resultatet av jämförelsen. Specifikt ska den returnera `True` om och endast om det aktuella objektet är större än det objekt som skickas som ett argument. De kriterier som används kan bestämmas av programmeraren. Med aktuellt objekt menar vi det objekt som metoden anropas på med punkt `.` notationen

```python
class Produkt:
    def __init__(self, namn: str, pris: float):
        self.__namn = namn
        self.__pris = pris

    def __str__(self):
        return f"{self.__namn} (pris {self.__pris})"

    @property
    def pris(self):
        return self.__pris

    def __gt__(self, annan_produkt):
        return self.pris > annan_produkt.pris
```

I implementationen ovan returnerar metoden `__gt__` `True` om priset på den aktuella produkten är högre än priset på den produkt som skickas som argument. I annat fall returnerar metoden `False`.

Nu finns jämförelseoperatorn `>` tillgänglig för användning med objekt av typen Produkt:

```python
apelsin = Produkt("Apelsin", 4.90)
banan = Produkt("Banan", 3.95)

if apelsin > banan:
    print("Apelsin är större")
else:
    print("Banan är större")
```

<sample-output>

Apelsin är större

</sample-output>

Som nämnts ovan är det upp till programmeraren att bestämma vilka kriterier som ska gälla för att avgöra vad som är störst och vad som är minst. Vi kan t.ex. bestämma att ordningen inte ska baseras på pris, utan i stället ska vara alfabetisk enligt namn. Detta skulle innebära att `banan` nu skulle vara "större än" `apelsin`, eftersom "banan" kommer senare alfabetiskt.

```python
class Produkt:
    def __init__(self, namn: str, pris: float):
        self.__namn = namn
        self.__pris = pris

    def __str__(self):
        return f"{self.__namn} (pris {self.__pris})"

    @property
    def pris(self):
        return self.__pris

    @property
    def namn(self):
        return self.__namn

    def __gt__(self, annan_produkt):
        return self.namn > annan_produkt.namn
```

```python
apelsin = Produkt("Apelsin", 4.90)
banan = Produkt("Banan", 3.95)

if apelsin > banan:
    print("Apelsin är större")
else:
    print("Banan är större")
```

<sample-output>

Banan är större

</sample-output>

## Fler operatorer

Här har vi en tabell som innehåller de vanliga jämförelseoperatorerna, tillsammans med de metoder som måste implementeras om vi vill göra dem tillgängliga för användning på våra objekt:

Operator | Traditionell mening | Metodens namn
:--:|:--:|:--:
`<` | Mindre än | `__lt__(self, annan)`
`>` | Större än | `__gt__(self, annan)`
`==` | Lika med | `__eq__(self, annan)`
`!=` | Inte lika med | `__ne__(self, annan)`
`<=` | Mindre eller lika med | `__le__(self, annan)`
`>=` | Större eller lika med | `__ge__(self, annan)`

Du kan också implementera några andra operatorer, inklusive följande aritmetiska operatorer:

Operator | Traditionell mening | Metodens namn
:--:|:--:|:--:
`+` | Addition | `__add__(self, annan)`
`-` | Subtraktion | `__sub__(self, annan)`
`*` | Multiplikation | `__mul__(self, annan)`
`/` | Division (bråktal) | `__truediv__(self, annan)`
`//` | Division (heltal) | `__floordiv__(self, annan)`

Fler operatorer och metodnamn finns lätt att hitta på nätet. Kom också ihåg `dir`-instruktionen för att lista de metoder som är tillgängliga för användning på ett visst objekt.

Det är mycket sällan nödvändigt att implementera alla aritmetiska operatorer och jämförelseoperatorer i dina egna klasser. Division är t.ex. en operation som sällan är meningsfull utanför numeriska objekt. Vad skulle resultatet av att dividera ett Student-objekt med tre, eller med ett annat Student-objekt bli? Trots detta är vissa av dessa operatorer ofta mycket användbara även i egna klasser. Valet av metoder att implementera beror på vad som är vettigt, med tanke på egenskaperna hos dina objekt.

Låt oss ta en titt på en klass som modellerar en enda anteckning. Om vi implementerar metoden `__add__` i vår klassdefinition blir additionsoperatorn + tillgänglig för våra Anteckning-objekt:

```python
from datetime import datetime

class Anteckning:
    def __init__(self, dtm: datetime, inlagg: str):
        self.dtm = dtm
        self.inlagg = inlagg

    def __str__(self):
        return f"{self.dtm}: {self.inlagg}"

    def __add__(self, annan):
        # Datumet för den nya anteckningen är aktuell tid
        nytt_inlagg = Anteckning(datetime.now(), "")
        nytt_inlagg.inlagg = self.inlagg + "och " + annan.inlagg
        return nytt_inlagg
```

```python
inlagg1 = Anteckning(datetime(2016, 12, 17), "Kom ihåg att köpa presenter")
inlagg2 = Anteckning(datetime(2016, 12, 23), "Kom ihåg att hämta en gran")

# Nu kan dessa anteckningar bli sammanlagda med + operatorn - detta kallar metoden __add__ i Anteckning-klassen
bada = inlagg1 + inlagg2
print(bada)
```

<sample-output>

2020-09-09 14:13:02.163170: Kom ihåg att köpa presenter och Kom ihåg att hämta en gran

</sample-output>

## En strängrepresentation av ett objekt

Du har redan implementerat en hel del `__str__`-metoder i dina klasser. Som du vet returnerar metoden en strängrepresentation av objektet. En annan ganska liknande metod är `__repr__` som returnerar en teknisk representation av objektet. Metoden `__repr__` är ofta implementerad så att den returnerar den programkod som kan exekveras för att returnera ett objekt med identiskt innehåll som det aktuella objektet.

Funktionen `repr` returnerar denna tekniska strängrepresentation av objektet. Den tekniska representationen används även när metoden `__str__` inte har definierats för objektet. Exemplet nedan kommer att göra detta tydligare:

```python
class Person:
    def __init__(self, namn: str, alder: int):
        self.namn = namn
        self.alder = alder

    def __repr__(self):
        return f"Person({repr(self.namn)}, {self.alder})"
```

```python3
person1 = Person("Anna", 25)
person2 = Person("Peter", 99)
print(person1)
print(person2)
```

<sample-output>

Person('Anna', 25)
Person('Peter', 99)

</sample-output>

Lägg märke till hur metoden `__repr__` själv använder `repr`-funktionen för att hämta den tekniska representationen av strängen. Detta är nödvändigt för att inkludera tecknen `'` i resultatet.

Följande klass har definitioner för både `__repr__` och `__str__`:

```python
class Person:
    def __init__(self, namn: str, alder: int):
        self.namn = namn
        self.alder = alder

    def __repr__(self):
        return f"Person({repr(self.namn)}, {self.alder})"

    def __str__(self):
        return f"{self.namn} ({self.alder} år)"
```

```python3
person = Person("Anna", 25)
print(person)
print(repr(person))
```

<sample-output>

Anna (25 år)
Person('Anna', 25)

</sample-output>

Det är värt att nämna att med datastrukturer, såsom listor, använder Python alltid `__repr__`-metoden för strängrepresentationen av innehållet. Detta kan ibland se lite förvirrande ut:

```python3
personer = []
personer.append(Person("Anna", 25))
personer.append(Person("Peter", 99))
personer.append(Person("Maja", 55))
print(personer)
```

<sample-output>

[Person('Anna', 25), Person('Peter', 99), Person('Maja', 55)]

</sample-output>

<programming-exercise name='Raha' tmcname='osa10-07_raha'>

Övningsmallen innehåller en mall för en klass som heter `Pengar`. Den här övningen ber dig att implementera några ytterligare metoder och att åtgärda några små problem i mallen

## Del 1: Fixa strängrepresentationen

Metoden `__str__` i klassdefinitionen fungerar inte riktigt som den ska. Med följande två `Pengar`-objekt skrivs det senare ut på fel sätt:

```python
e1 = Pengar(4, 10)
e2 = Pengar(2, 5)  # två euro och 5 cent

print(e1)
print(e2)
```

<sample-output>

4.10
2.5

</sample-output>

Fixa metoden så att den skriver ut:

<sample-output>

4.10 eur
2.05 eur

</sample-output>

## Del 2: Lika stora mängder

Definiera en ny metod med namnet `__eq__(self, annan)` som gör att du kan använda jämförelseoperatorn == på `Pengar`-objekt. Du kan testa din implementation med följande kod:

```python
e1 = Pengar(4, 10)
e2 = Pengar(2, 5)
e3 = Pengar(4, 10)

print(e1)
print(e2)
print(e3)
print(e1 == e2)
print(e1 == e3)
```

<sample-output>

4.10 eur
2.05 eur
4.10 eur
False
True

</sample-output>

## Del 3: Andra jämförelseoperatörer

Implementera även metoder för jämförelseoperatörerna `<`, `>` och `!=`.

```python
e1 = Pengar(4, 10)
e2 = Pengar(2, 5)

print(e1 != e2)
print(e1 < e2)
print(e1 > e2)
```

<sample-output>

True
False
True

</sample-output>

## Del 4: Addition och subtraktion

Vänligen implementera additions- och subtraktionsoperatorerna `+` och `-` för Pengar-objekt. Båda ska returnera ett nytt objekt av typen Pengar. Varken objektet i sig eller det objekt som skickas som argument ska ändras som ett resultat.

Obs: Värdet på ett Pengar-objekt kan inte vara negativt. Om ett försök att subtrahera skulle resultera i ett negativt resultat ska metoden ge upphov till ett `ValueError`-undantag.

```python
e1 = Pengar(4, 5)
e2 = Pengar(2, 95)

e3 = e1 + e2
e4 = e1 - e2

print(e3)
print(e4)

e5 = e2-e1
```

<sample-output>

7.00 eur
1.10 eur
Traceback (most recent call last):
  File "fil.py", line 416, in <module>
    e5 = e2-e1
  File "fil.py", line 404, in __sub__
    raise ValueError(f"negativt resultat inte tillåtet")
ValueError: negativt resultat inte tillåtet

</sample-output>

## Del 5: Värdet kan inte bli direkt åtkommet

Klassen har fortfarande ett litet integritetsproblem. Användaren kan ”fuska” genom att komma åt attributen direkt och ändra det värde som lagras i `Pengar`-objektet:

```python
print(e1)
e1.euron = 1000
print(e1)
```

<sample-output>

4.05 eur
1000.05 eur

</sample-output>

[Inkapsla](/osa-9/3-kapselointi#kapselointi) implementeringen av de attribut som definieras i klassen så att fusket ovan inte är möjligt. Klassen ska inte ha några offentliga attribut och inga getter- eller sätter-metoder för euro eller cent.

</programming-exercise>

<programming-exercise name='Päiväys' tmcname='osa10-08_paivays'>

I den här övningen ska du implementera klassen `SimpelDatum` som gör att du kan hantera datum. För enkelhetens skull antar vi här att _varje månad har 30 dagar_.

På grund av denna förenkling bör du inte använda `datetime`-modulen från Pythons standardbibliotek. Du kommer att implementera liknande funktionalitet själv istället.

## Del 1: Jämförelse

Implementera mallen för klassen, såväl som metoder för jämförelseoperatörerna `<`, `>`, `==` och `!=`. Exempel på användning:

```python
d1 = SimpelDatum(4, 10, 2020)
d2 = SimpelDatum(28, 12, 1985)
d3 = SimpelDatum(28, 12, 1985)

print(d1)
print(d2)
print(d1 == d2)
print(d1 != d2)
print(d1 == d3)
print(d1 < d2)
print(d1 > d2)
```

<sample-output>

4.10.2020
28.12.1985
False
True
False
False
True

</sample-output>

## Del 2: Ökning

Vänligen implementera additionsoperatorn `+` som gör att du kan lägga till ett givet antal dagar till ett `SimpelDatum`-objekt. Operatorn ska returnera ett nytt `SimpelDatum`-objekt. Det ursprungliga objektet ska inte ändras.

```python
d1 = SimpelDatum(4, 10, 2020)
d2 = SimpelDatum(28, 12, 1985)

d3 = d1 + 3
d4 = d2 + 400

print(d1)
print(d2)
print(d3)
print(d4)
```

<sample-output>

4.10.2020
28.12.1985
7.10.2020
8.2.1987

</sample-output>

## Del 3: Skillnad

Vänligen implementera subtraktionsoperatorn `-` som gör att du kan ta reda på skillnaden i dagar mellan två SimpelDatum-objekt. Eftersom vi antar att varje månad har 30 dagar, är ett år inom ramen för denna övning 12*30 = 360 dagar långt.

Operatorn fungerar enligt följande:

```python
d1 = SimpelDatum(4, 10, 2020)
d2 = SimpelDatum(2, 11, 2020)
d3 = SimpelDatum(28, 12, 1985)

print(d2-d1)
print(d1-d2)
print(d1-d3)
```

<sample-output>

28
28
12516

</sample-output>

</programming-exercise>

## Iteratorer

Vi vet att `for`-satsen kan användas för att iterera genom många olika datastrukturer, filer och samlingar av objekt. Ett typiskt användningsfall skulle kunna vara följande funktion:

```python

def rakna_positiva(lista: list):
    n = 0
    for foremal in lista:
        if foremal > 0:
            n += 1
    return n

```

Funktionen går igenom objekten i listan ett efter ett och håller reda på hur många av objekten som var positiva.

Det är också möjligt att göra sina egna klasser itererbara. Detta är användbart när klassens huvudsyfte handlar om att lagra en samling objekt. Klassen Bokhylla från ett tidigare exempel skulle vara en bra kandidat, eftersom det skulle vara vettigt att använda en `for`-loop för att gå igenom böckerna på hyllan. Detsamma gäller för, exempelvis, ett studentregister. Att kunna iterera genom samlingen av studenter kan vara användbart.

För att göra en klass itererbar måste du implementera iteratormetoderna `__iter__` och `__next__`. Vi återkommer till detaljerna i dessa metoder efter följande exempel:

```python

class Bok:
    def __init__(self, namn: str, forfattare: str, sidor: int):
        self.namn = namn
        self.forfattare = forfattare
        self.sidor = sidor

class Bokhylla:
    def __init__(self):
        self._bocker = []

    def tillsatt_bok(self, bok: Bok):
        self._bocker.append(bok)

    # Initialiseringsmetoden för iteratorn
    # Här bör iterationsvariabeln(eller variablerna) initialiseras
    def __iter__(self):
        self.n = 0
        # Metoden returnerar en referens till själva objektet eftersom 
        # iteratorn är implementerad inom samma klassdefinition
        return self

    # Metoden returnerar nästa föremål inom objektet
    # Ifall inga föremål är kvar, åstadkomms StopIteration-händelsen
    def __next__(self):
        if self.n < len(self._bocker):
            # Väljer det aktuella föremålet från listan inom objektet
            bok = self._bocker[self.n]
            # Öka räknaren med ett
            self.n += 1
            # ... och returnera det aktuella föremålet
            return bok
        else:
            # Inga fler böcker
            raise StopIteration

```

Metoden `__iter__` initialiserar iterationsvariabeln eller variablerna. I det här fallet räcker det med att ha en enkel räknare som innehåller index för det aktuella objektet i listan. Vi behöver också metoden `__next__`, som returnerar nästa objekt i iteratorn. I exemplet ovan returnerar metoden objektet med index n från listan i Bokhylla-objektet, och iteratorvariabeln inkrementeras också.

När alla objekt har genomgåtts utlöser metoden `__next__` undantaget `StopIteration`. Processen skiljer sig inte från andra undantag, men det här undantaget hanteras automatiskt av Python och dess syfte är att signalera till koden som anropar iteratorn (t.ex. en `for`-loop) att iterationen nu är över.

Vår bokhylla är nu redo för iteration, till exempel med en `for`-loop: 

```python

if __name__ == "__main__":
    b1 = Bok("Livet av en Python", "Peter Python", 123)
    b2 = Bok("Den gamle och Java", "Ernest Hemingjava", 204)
    b3 = Bok("C-värdheter på nätet", "Karl Kodare", 997)

    hylla = Bokhylla()
    hylla.tillsatt_bok(b1)
    hylla.tillsatt_bok(b2)
    hylla.tillsatt_bok(b3)

    # Skriver ut namnet på alla böcker
    for bok in hylla:
        print(bok.namn)

```

<sample-output>

Livet av en Python
Den gamle och Java
C-värdheter på nätet

</sample-output>


<programming-exercise name='Iteroitava kauppalista' tmcname='osa10-09_iteroitava_kauppalista'>

I uppgiftsbotten finns klassen `Affarslista` från [övningen i del 8](/osa-8/2-luokat-ja-oliot#programming-exercise-kauppalista). Ändra klassen så att den är itererbar och därmed kan användas på följande sätt:

```python
lista = Affarslista()
lista.tillsatt("apelsiner", 10)
lista.tillsatt("bananer", 5)
lista.tillsatt("ananas", 1)

for produkt in lista:
    print(f"{produkt[0]}: {produkt[1]} kpl")
```

<sample-output>

apelsiner: 10 kpl
bananer: 5 kpl
ananas: 1 kpl

</sample-output>

Iteratormetoden `__next__` ska returnera tuplar, där det första föremålet är namnet på produkten och det andra är antalet.

</programming-exercise>
