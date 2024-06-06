---
path: '/osa-10/3-olio-ohjelmoinnin-tekniikoita'
title: 'Objektorienterade programmeringstekniker'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Tämän osion jälkeen

- Känner du till några av de olika användningsområdena för variabelnamnet `self`
- Vet du hur du överbelastar operatorer i dina egna klasser
- Kommer du att kunna skapa en iterabel klass

</text-box>

En klass kan innehålla en metod som returnerar ett objekt av samma klass. Nedan har vi t.ex. klassen `Produkt`, vars metod `produkt_på_rea` returnerar ett nytt Produkt-objekt med samma namn som det ursprungliga men med ett pris som är 25 % lägre:

```python
class Tuote:
    def __init__(self, nimi: str, hinta: float):
        self.__nimi = nimi
        self.__hinta = hinta

    def __str__(self):
        return f"{self.__nimi} (hinta {self.__hinta})"

    def alennustuote(self):
        alennettu = Tuote(self.__nimi, self.__hinta * 0.75)
        return alennettu
```

```python
omena1 = Tuote("Omena", 2.99)
omena2 = omena1.alennustuote()
print(omena1)
print(omena2)
```

<sample-output>

Omena (hinta 2.99)
Omena (hinta 2.2425)

</sample-output>

Låt oss gå igenom syftet med variabeln `self`: inom en klassdefinition hänvisar den till själva objektet. Vanligtvis används den för att hänvisa till objektets egna egenskaper, dess attribut och metoder. Variabeln kan också användas för att hänvisa till hela objektet, till exempel om själva objektet måste returneras till klientkoden. I exemplet nedan har vi lagt till metoden `billigare` i klassdefinitionen. Den tar en annan Produkt som sitt argument och returnerar det billigare av de två:

```python
class Tuote:
    def __init__(self, nimi: str, hinta: float):
        self.__nimi = nimi
        self.__hinta = hinta

    def __str__(self):
        return f"{self.__nimi} (hinta {self.__hinta})"

    @property
    def hinta(self):
        return self.__hinta

    def halvempi(self, tuote):
        if self.__hinta < tuote.hinta:
            return self
        else:
            return tuote
```

```python
omena = Tuote("Omena", 2.99)
appelsiini = Tuote("Appelsiini", 3.95)
banaani = Tuote("Banaani", 5.25)

print(appelsiini.halvempi(omena))
print(appelsiini.halvempi(banaani))
```

<sample-output>

Omena (2.99)
Appelsiini (3.95)

</sample-output>

Även om det här fungerar bra är det ett mycket specialiserat fall av att jämföra två objekt. Det skulle vara bättre om vi kunde använda Pythons jämförelseoperatorer direkt på dessa `Produkt`-objekt.

## Överbelastande av operatorer

Python innehåller några speciellt namngivna inbyggda metoder för att arbeta med standardoperatorerna för aritmetik och jämförelse. Tekniken kallas operatörsöverbelastning. Om du vill kunna använda en viss operator på instanser av självdefinierade klasser kan du skriva en speciell metod som returnerar det korrekta resultatet av operatorn. Vi har redan använt den här tekniken med `__str__` metoden: Python vet att leta efter en metod som heter så här när en strängrepresentation av ett objekt efterfrågas.

Låt oss börja med operatorn > som talar om för oss om den första operanden är större än den andra. Klassdefinitionen `Produkt` nedan innehåller metoden `__gt__`, som är en förkortning av greater than. Denna speciellt namngivna metod ska returnera det korrekta resultatet av jämförelsen. Specifikt ska den returnera `True` om och endast om det aktuella objektet är större än det objekt som skickas som ett argument. De kriterier som används kan bestämmas av programmeraren. Med aktuellt objekt menar vi det objekt som metoden anropas på med punkt `.` notationen

```python
class Tuote:
    def __init__(self, nimi: str, hinta: float):
        self.__nimi = nimi
        self.__hinta = hinta

    def __str__(self):
        return f"{self.__nimi} (hinta {self.__hinta})"

    @property
    def hinta(self):
        return self.__hinta

    def __gt__(self, toinen_tuote):
        return self.hinta > toinen_tuote.hinta
```

I implementationen ovan returnerar metoden `__gt__` `True` om priset på den aktuella produkten är högre än priset på den produkt som skickas som argument. I annat fall returnerar metoden `False`.

Nu finns jämförelseoperatorn `>` tillgänglig för användning med objekt av typen Produkt:

```python
appelsiini = Tuote("Appelsiini", 4.90)
omena = Tuote("Omena", 3.95)

if appelsiini > omena:
    print("Appelsiini on suurempi")
else:
    print("Omena on suurempi")
```

<sample-output>

Appelsiini on suurempi

</sample-output>

Som nämnts ovan är det upp till programmeraren att bestämma vilka kriterier som ska gälla för att avgöra vad som är störst och vad som är minst. Vi kan t.ex. bestämma att ordningen inte ska baseras på pris, utan i stället ska vara alfabetisk enligt namn. Detta skulle innebära att `banan` nu skulle vara "större än" `apelsin`, eftersom "banan" kommer senare alfabetiskt.

```python
class Tuote:
    def __init__(self, nimi: str, hinta: float):
        self.__nimi = nimi
        self.__hinta = hinta

    def __str__(self):
        return f"{self.__nimi} (hinta {self.__hinta})"

    @property
    def hinta(self):
        return self.__hinta

    @property
    def nimi(self):
        return self.__nimi

    def __gt__(self, toinen_tuote):
        return self.nimi > toinen_tuote.nimi
```

```python
appelsiini = Tuote("Appelsiini", 4.90)
omena = Tuote("Omena", 3.95)

if appelsiini > omena:
    print("Appelsiini on suurempi")
else:
    print("Omena on suurempi")
```

<sample-output>

Omena on suurempi

</sample-output>

## Fler operatorer

Här har vi en tabell som innehåller de vanliga jämförelseoperatorerna, tillsammans med de metoder som måste implementeras om vi vill göra dem tillgängliga för användning på våra objekt:

Operaattori | Merkitys perinteisesti | Metodin nimi
:--:|:--:|:--:
`<` | Pienempi kuin | `__lt__(self, toinen)`
`>` | Suurempi kuin | `__gt__(self, toinen)`
`==` | Yhtä suuri kuin | `__eq__(self, toinen)`
`!=` | Eri suuri kuin | `__ne__(self, toinen)`
`<=` | Pienempi tai yhtäsuuri kuin | `__le__(self, toinen)`
`>=` | Suurempi tai yhtäsuuri kuin | `__ge__(self, toinen)`

Du kan också implementera några andra operatorer, inklusive följande aritmetiska operatorer:

Operaattori | Merkitys perinteisesti | Metodin nimi
:--:|:--:|:--:
`+` | Yhdistäminen | `__add__(self, toinen)`
`-` | Vähentäminen | `__sub__(self, toinen)`
`*` | Monistaminen | `__mul__(self, toinen)`
`/` | Jakaminen | `__truediv__(self, toinen)`
`//` | Kokonaisjakaminen | `__floordiv__(self, toinen)`

Fler operatorer och metodnamn finns lätt att hitta på nätet. Kom också ihåg `dir`-instruktionen för att lista de metoder som är tillgängliga för användning på ett visst objekt.

Det är mycket sällan nödvändigt att implementera alla aritmetiska operatorer och jämförelseoperatorer i dina egna klasser. Division är t.ex. en operation som sällan är meningsfull utanför numeriska objekt. Vad skulle resultatet av att dividera ett Student-objekt med tre, eller med ett annat Student-objekt bli? Trots detta är vissa av dessa operatorer ofta mycket användbara även i egna klasser. Valet av metoder att implementera beror på vad som är vettigt, med tanke på egenskaperna hos dina objekt.

Låt oss ta en titt på en klass som modellerar en enda anteckning. Om vi implementerar metoden `__add__` i vår klassdefinition blir additionsoperatorn + tillgänglig för våra Anteckning-objekt:

```python
from datetime import datetime

class Muistiinpano:
    def __init__(self, pvm: datetime, merkinta: str):
        self.pvm = pvm
        self.merkinta = merkinta

    def __str__(self):
        return f"{self.pvm}: {self.merkinta}"

    def __add__(self, toinen):
        # Uuden muistiinpanon ajaksi nykyinen aika
        uusi_muistiinpano = Muistiinpano(datetime.now(), "")
        uusi_muistiinpano.merkinta = self.merkinta + " ja " + toinen.merkinta
        return uusi_muistiinpano
```

```python
merkinta1 = Muistiinpano(datetime(2016, 12, 17), "Muista ostaa lahjoja")
merkinta2 = Muistiinpano(datetime(2016, 12, 23), "Muista hakea kuusi")

# Nyt voidaan yhdistää plussalla - tämä kutsuu metodia __add__ luokassa Muistiipano
molemmat = merkinta1 + merkinta2
print(molemmat)
```

<sample-output>

2020-09-09 14:13:02.163170: Muista ostaa lahjoja ja Muista hakea kuusi

</sample-output>

## En strängrepresentation av ett objekt

Du har redan implementerat en hel del `__str__`-metoder i dina klasser. Som du vet returnerar metoden en strängrepresentation av objektet. En annan ganska liknande metod är `__repr__` som returnerar en teknisk representation av objektet. Metoden `__repr__` är ofta implementerad så att den returnerar den programkod som kan exekveras för att returnera ett objekt med identiskt innehåll som det aktuella objektet.

Funktionen `repr` returnerar denna tekniska strängrepresentation av objektet. Den tekniska representationen används även när metoden `__str__` inte har definierats för objektet. Exemplet nedan kommer att göra detta tydligare:

```python
class Henkilo:
    def __init__(self, nimi: str, ika: int):
        self.nimi = nimi
        self.ika = ika

    def __repr__(self):
        return f"Henkilo({repr(self.nimi)}, {self.ika})"
```

```python3
henkilo1 = Henkilo("Anna", 25)
henkilo2 = Henkilo("Pekka", 99)
print(henkilo1)
print(henkilo2)
```

<sample-output>

Henkilo('Anna', 25)
Henkilo('Pekka', 99)

</sample-output>

Lägg märke till hur metoden `__repr__` själv använder `repr`-funktionen för att hämta den tekniska representationen av strängen. Detta är nödvändigt för att inkludera tecknen `'` i resultatet.

Följande klass har definitioner för både `__repr__` och `__str__`:

```python
class Henkilo:
    def __init__(self, nimi: str, ika: int):
        self.nimi = nimi
        self.ika = ika

    def __repr__(self):
        return f"Henkilo({repr(self.nimi)}, {self.ika})"

    def __str__(self):
        return f"{self.nimi} ({self.ika} vuotta)"
```

```python3
henkilo = Henkilo("Anna", 25)
print(henkilo)
print(repr(henkilo))
```

<sample-output>

Anna (25 vuotta)
Henkilo('Anna', 25)

</sample-output>

Det är värt att nämna att med datastrukturer, såsom listor, använder Python alltid `__repr__`-metoden för strängrepresentationen av innehållet. Detta kan ibland se lite förvirrande ut:

```python3
henkilot = []
henkilot.append(Henkilo("Anna", 25))
henkilot.append(Henkilo("Pekka", 99))
henkilot.append(Henkilo("Maija", 55))
print(henkilot)
```

<sample-output>

[Henkilo('Anna', 25), Henkilo('Pekka', 99), Henkilo('Maija', 55)]

</sample-output>

<programming-exercise name='Raha' tmcname='osa10-07_raha'>

Tehtäväpohjasta löytyy luokan `Raha` runko. Tässä tehtävässä laajennetaan runkoa muutamilla operaattoreilla, ja korjataan pari rungossa olevaa pientä ongelmaa

## Korjaa merkkijonoesitys

Rahan merkkijonoesityksen muodostava metodi ei ole nyt ihan kunnossa. Seuraavassa esimerkissä muodostetaan kaksi raha-olioa, joista jälkimmäinen ei tulostu oikein:

```python
e1 = Raha(4, 10)
e2 = Raha(2, 5)  # kaksi euroa ja viisi senttiä

print(e1)
print(e2)
```

<sample-output>

4.10
2.5

</sample-output>

Korjaa luokan metodi `__str__(self)` siten, että tulostus on seuraava:

<sample-output>

4.10 eur
2.05 eur

</sample-output>

## Yhtäsuuruus

Määrittele raha-oliolle metodi  `__eq__(self, toinen)`, jonka avulla rahan yhtäsuuruusvertailu saadaan toimimaan:

```python
e1 = Raha(4, 10)
e2 = Raha(2, 5)
e3 = Raha(4, 10)

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

## Muut vertailut

Toteuta rahalle myös seuraavat vertailuoperaattorit `<`, `>`, `!=`.

```python
e1 = Raha(4, 10)
e2 = Raha(2, 5)

print(e1 != e2)
print(e1 < e2)
print(e1 > e2)
```

<sample-output>

True
False
True

</sample-output>

## Plus ja miinus

Toteuta rahalle yhteen- ja vähennyslaskuoperaatiot. Molempien operaatioiden tulee palauttaa uusi rahaolio, ja ne eivät saa muuttaa olioa itseään tai parametrina olevaa olioa!

Huomaa, että rahan arvo ei voi olla negatiivinen. Negatiiviseen tulokseen päätyvän vähennyslaskuyrityksen tulee aiheuttaa ValueError-tyyppinen poikkeus.

```python
e1 = Raha(4, 5)
e2 = Raha(2, 95)

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
  File "tiedosto.py", line 416, in <module>
    e5 = e2-e1
  File "tiedosto.py", line 404, in __sub__
    raise ValueError(f"negatiivinen tulos ei sallittu")
ValueError: negatiivinen tulos ei sallittu

</sample-output>

## Arvoa ei voi muuttaa

Luokassa on tällä hetkellä vielä pieni ongelma, koska käyttäjä voi "huijaamalla" muuttaa rahan arvoa:

```python
print(e1)
e1.eurot = 1000
print(e1)
```

<sample-output>

4.05 eur
1000.05 eur

</sample-output>

Muuta luokan toteutus [kapseloiduksi](/osa-9/3-kapselointi#kapselointi) siten, että yllä oleva huijaus ei onnistu. Luokalla ei siis saa olla kapseloimattomia attribuutteja eikä asetus- tai havainnointimetodeita euroille tai senteille!

</programming-exercise>

<programming-exercise name='Päiväys' tmcname='osa10-08_paivays'>

Tässä tehtävässä toteutetaan luokka `Paivays`, jonka avulla on mahdollista käsitellä päivämääriä. Oletetaan tässä tehtävässä yksinkertaisuuden vuoksi, että _jokaisessa kuussa on 30 päivää_.

Huom! Edellisestä johtuen tehtävässä ei poikkeuksellisesti kannata käyttää Pythonin `datetime`-moduulia, vaan toteutetaan luokka itse.

## Vertailut

Toteuta luokan runko ja sille vertailuoperaattorit <, >, == ja !=. Käyttöesimerkki:

```python
p1 = Paivays(4, 10, 2020)
p2 = Paivays(28, 12, 1985)
p3 = Paivays(28, 12, 1985)

print(p1)
print(p2)
print(p1 == p2)
print(p1 != p2)
print(p1 == p3)
print(p1 < p2)
print(p1 > p2)
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

## Kasvatus

Toteuta päiväykselle operaattori +. Operaattori luo uuden päivämäärän joka on lisättävän lukeman päiviä verran suurempi kuin alkuperäinen päivämäärä. Alkuperäinen päivä ei saa muuttua.

```python
p1 = Paivays(4, 10, 2020)
p2 = Paivays(28, 12, 1985)

p3 = p1 + 3
p4 = p2 + 400

print(p1)
print(p2)
print(p3)
print(p4)
```

<sample-output>

4.10.2020
28.12.1985
7.10.2020
8.2.1987

</sample-output>

## Erotus

Toteuta päiväykselle operaattori -, joka palauttaa päivämäärien eron päivissä laskettuna. Huomaa, että koska oletamme jokaisessa kuukaudessa olevan 30 päivää, tässä tehtävässä vuosien päivien lukumäärä on 12*30 eli 360.

Operaattori toimii seuraavasti

```python
p1 = Paivays(4, 10, 2020)
p2 = Paivays(2, 11, 2020)
p3 = Paivays(28, 12, 1985)

print(p2-p1)
print(p1-p2)
print(p1-p3)
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

def laske_positiiviset(lista: list):
    n = 0
    for alkio in lista:
        if alkio > 0:
            n += 1
    return n

```

Funktionen går igenom objekten i listan ett efter ett och håller reda på hur många av objekten som var positiva.

Det är också möjligt att göra sina egna klasser itererbara. Detta är användbart när klassens huvudsyfte handlar om att lagra en samling objekt. Klassen Bokhylla från ett tidigare exempel skulle vara en bra kandidat, eftersom det skulle vara vettigt att använda en `for`-loop för att gå igenom böckerna på hyllan. Detsamma gäller för, exempelvis, ett studentregister. Att kunna iterera genom samlingen av studenter kan vara användbart.

För att göra en klass itererbar måste du implementera iteratormetoderna `__iter__` och `__next__`. Vi återkommer till detaljerna i dessa metoder efter följande exempel:

```python

class Kirja:
    def __init__(self, nimi: str, kirjailija: str, sivuja: int):
        self.nimi = nimi
        self.kirjailija = kirjailija
        self.sivuja = sivuja

class Kirjahylly:
    def __init__(self):
        self._kirjat = []

    def lisaa_kirja(self, kirja: Kirja):
        self._kirjat.append(kirja)

    # Iteraattorin alustusmetodi
    # Tässä tulee alustaa iteroinnissa käytettävä(t) muuttuja(t)
    def __iter__(self):
        self.n = 0
        # Metodi palauttaa viittauksen olioon itseensä, koska
        # iteraattori on toteutettu samassa luokassa
        return self

    # Metodi palauttaa seuraavan alkion
    # Jos ei ole enempää alkioita, heitetään tapahtuma
    # StopIteration
    def __next__(self):
        if self.n < len(self._kirjat):
            # Poimitaan listasta nykyinen
            kirja = self._kirjat[self.n]
            # Kasvatetaan laskuria yhdellä
            self.n += 1
            # ...ja palautetaan
            return kirja
        else:
            # Ei enempää kirjoja
            raise StopIteration

```

Metoden `__iter__` initialiserar iterationsvariabeln eller variablerna. I det här fallet räcker det med att ha en enkel räknare som innehåller index för det aktuella objektet i listan. Vi behöver också metoden `__next__`, som returnerar nästa objekt i iteratorn. I exemplet ovan returnerar metoden objektet med index n från listan i Bokhylla-objektet, och iteratorvariabeln inkrementeras också.

När alla objekt har genomgåtts utlöser metoden `__next__` undantaget `StopIteration`. Processen skiljer sig inte från andra undantag, men det här undantaget hanteras automatiskt av Python och dess syfte är att signalera till koden som anropar iteratorn (t.ex. en `for`-loop) att iterationen nu är över.

Vår bokhylla är nu redo för iteration, till exempel med en `for`-loop: 

```python

if __name__ == "__main__":
    k1 = Kirja("Elämäni Pythoniassa", "Pekka Python", 123)
    k2 = Kirja("Vanhus ja Java", "Ernest Hemingjava", 204)
    k3 = Kirja("C-itsemän veljestä", "Keijo Koodari", 997)

    hylly = Kirjahylly()
    hylly.lisaa_kirja(k1)
    hylly.lisaa_kirja(k2)
    hylly.lisaa_kirja(k3)

    # Tulostetaan kaikkien kirjojen nimet
    for kirja in hylly:
        print(kirja.nimi)

```

<sample-output>

Elämäni Pythoniassa
Vanhus ja Java
C-itsemän veljestä

</sample-output>


<programming-exercise name='Iteroitava kauppalista' tmcname='osa10-09_iteroitava_kauppalista'>

Tehtäväpohjassa on [osan 8 tehtävästä ](/osa-8/2-luokat-ja-oliot#programming-exercise-kauppalista) tuttu luokka `Kauppalista`. Tee luokasta iteroitava, siten että sitä voi käyttää seuraavasti:

```python
lista = Kauppalista()
lista.lisaa("banaanit", 10)
lista.lisaa("omenat", 5)
lista.lisaa("ananas", 1)

for tuote in lista:
    print(f"{tuote[0]}: {tuote[1]} kpl")
```

<sample-output>

banaanit: 10 kpl
omenat: 5 kpl
ananas: 1 kpl

</sample-output>

Iteraattorin metodin `__next__` tulee palauttaa tupleja, joiden ensimmäinen alkio on tuotteen nimi ja toisen listalla olevan tuotteen lukumäärä.

</programming-exercise>
