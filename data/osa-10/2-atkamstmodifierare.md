---
path: '/osa-10/2-atkamstmodifierare'
title: 'Åtkomstmodifierare'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Kommer du att förstå åtkomstmodifierarna privat och skyddad
- Vet du hur synligheten för egenskaper bestäms i Python

</text-box>

Om en egenskap definieras som privat i basklassen är den inte direkt åtkomlig i några härledda klasser, liksom kort nämndes i föregående avsnitt. Låt oss ta en titt på ett exempel. I klassen `Anteckningsbok` nedan lagras anteckningarna i en lista, och listattributet är privat:

```python

class Anteckningsbok:
    """ En Anteckningsbok förvarar anteckningar i strängformat """

    def __init__(self):
        # privat attribut
        self.__anteckningar = []

    def tillsatt_anteckning(self, anteckning):
        self.__anteckningar.append(anteckning)

    def hamta_anteckning(self, index):
        return self.__anteckningar[index]

    def alla_anteckningar(self):
        return ",".join(self.__anteckningar)

```

Om klassens integritet är viktig är det vettigt att göra listattributen `anteckningar` privat. Klassen förser trots allt klienten med lämpliga metoder för att lägga till och bläddra i anteckningar. Detta tillvägagångssätt blir problematiskt om vi definierar en ny klass `AnteckningsbokPro`, som ärver `Anteckningsbok`-klassen. Det privata listattributet är inte tillgängligt för klienten, men det är inte heller tillgängligt för de härledda klasserna. Om vi försöker komma åt det, som i metoden `hamta_anteckningar` nedan, får vi ett felmeddelande:

```python
class AnteckningsbokPro(Anteckningsbok):
    """ En bättre Anteckningsbok med sökfunktionalitet """
    def __init__(self):
        # Detta är ok, eftersom konstruktorn är offentlig trots understrykning
        super().__init__()

    # Detta orsakar ett fel
    def hitta_anteckningar(self, sokord):
        hittade = []
        # Attributet __anteckningar är privat, den härledda
        # klassen kan inte komma åt den direkt
        for anteckning in self.__anteckningar:
            if sokord in anteckning:
                hittade.append(anteckning)

        return hittade

```

<sample-output>

AttributeError: 'AnteckningsbokPro' object has no attribute '_AnteckningsbokPro__anteckningar'

</sample-output>



## Skyddade egenskaper

Många objektorienterade programmeringsspråk har en funktion, oftast ett speciellt nyckelord, för att skydda egenskaper. Detta innebär att en egenskap ska vara dold för klassens klienter, men hållas tillgänglig för dess underklasser. Python avskyr i allmänhet nyckelord, så ingen sådan funktion är direkt tillgänglig i Python. Istället finns det en konvention för att markera skyddade egenskaper på ett visst sätt.

Kom ihåg att en egenskap kan döljas genom att prefixera dess namn med två understreck:

```python

def __init__(self):
    self.__anteckningar = []

```

Den överenskomna konventionen för att skydda en egenskap är att prefixera namnet med endast ett understreck. Nu är detta bara en konvention. Ingenting hindrar en programmerare från att bryta mot konventionen, men det anses vara en dålig programmeringspraxis.

```python

def __init__(self):
    self._anteckningar = []

```

Nedan har vi hela Anteckningsbok-exemplet, med skyddade `_anteckningar` istället för privata `__anteckningar`:

```python

class Anteckningsbok:
    """ En Anteckningsbok förvarar anteckningar i strängformat """

    def __init__(self):
        # Skyddade attribut
        self._anteckningar = []

    def tillsatt_anteckning(self, anteckning):
        self._anteckningar.append(anteckning)

    def hamta_anteckning(self, index):
        return self._anteckningar[index]

    def alla_anteckningar(self):
        return ",".join(self._anteckningar)

class AnteckningsbokPro(Anteckningsbok):
    """ En bättre Anteckningsbok med sökfunktionalitet """
    def __init__(self):
        # Detta är ok, eftersom konstruktorn är offentlig trots understrykning
        super().__init__()

    # Nu fungerar metoden, eftersom den skyddadde attributen är
    # ankomstbar till den härledda klassen
    def hitta_anteckningar(self, sokord):
        hittade = []
        for anteckning in self._anteckningar:
            if sokord in anteckning:
                hittade.append(anteckning)

        return hittade

```

Nedan har vi en praktisk tabell för synligheten av attribut med olika åtkomstmodifierare:

Åtkomstmodifierare	| Exempel | Synlig till klienten | Synlig till härledd klass
:--:|:----:|:----:|:----:
Offentlig | `self.namn` | ja | ja
Skyddad | `self._namn` | nej | ja
Privat | `self.__namn` | nej | nej

Åtkomstmodifierare fungerar på samma sätt med alla egenskaper. I klassen `Person` nedan har vi till exempel den skyddade metoden `versalisera_initialer` Den kan användas från den härledda klassen `Fotbollsspelare`:

```python

class Person:
    def __init__(self, namn: str):
        self._namn = self._versalisera_initialer(namn)

    def _versalisera_initialer(self, namn):
        namn_versaliserat = []
        for n in namn.split(" "):
            namn_versaliserat.append(n.capitalize())

        return " ".join(namn_versaliserat)

    def __repr__(self):
        return self.__namn

class Fotbollsspelare(Person):

    def __init__(self, namn: str, smeknamn: str, position: str):
        super().__init__(namn)
        # metoden är ankomstbar eftersom den är skyddad i basklassen
        self.__smeknamn = self._versalisera_initialer(smeknamn)
        self.__position = position

    def __repr__(self):
        r =  f"Fotbollsspelare - namn:{self._namn}, smeknamn: {self.__smeknamn}"
        r += f", position: {self.__position}"
        return r

# Testar klasserna
if __name__ == "__main__":
    fs = Fotbollsspelare("peter pythonson", "putte", "anfallare")
    print(fs)

```

<sample-output>

Fotbollsspelare - namn:Peter Pythonson, smeknamn: Putte, position: anfallare

</sample-output>


<programming-exercise name='Supergrupp' tmcname='osa10-05_supergrupp'>

I uppgiftsbotten finns färdigt klassdefinitionen för en `Superhjalte`.

Skapa klassen `Supergrupp`, som representerar en grupp av superhjältar. Klassen ska innehålla följande:

* **Skyddade** attributen namn (sträng), lokation (sträng) och medlemmar (lista)
* En konstruktor, som får namn och lokation av gruppen som argument, i den ordningen
* Getter-metoden för namn- och lokation-attributen
* Metoden `tillsatt_medlem(hjalte: Superhjalte)`, som lägger till en ny medlem till gruppen
* Metoden `skriv_ut_grupp`, som skriver ut information om gruppen och dess medlemmer, enligt formatet nedan

Exempel av klassen:

```python
superperson = Superhjalte("SuperPerson", "Supersnabbhet, superstyrka")
osynlig = Superhjalte("Osynliga Olle", "Osynlighet")
revengers = Supergrupp("Revengers", "Åland")

revengers.tillsatt_medlem(superperson)
revengers.tillsatt_medlem(osynlig)
revengers.skriv_ut_grupp()
```

<sample-output>

Revengers, Åland
Medlemmar:
SuperPerson, specialförmågor: Supersnabbhet, superstyrka
Osynliga Olle, specialförmågor: Osynlighet

</sample-output>

[Detta](https://rage.github.io/ohjelmointi-24-sv/osa-9/3-inkapsling) kapitel kan vara användbart.

</programming-exercise>

<programming-exercise name='Hemlig trolldryck' tmcname='osa10-06_hemlig_trolldryck'>

Övningsmallen innehåller klassdefinitionen för en `Trolldryck` som gör att du kan spara ett recept på en trolldryck. Klassdefinitionen innehåller en konstruktor tillsammans med metoderna

* `tillsatt_ingrediens(ingrediens: str, mangd: float)` och
* `skriv_ut_recept()`

Definiera en klass med namnet `HemligTrolldryck` som ärver `Trolldryck`-klassen och som gör att du också kan skydda receptet med ett lösenord.

Den nya klassen ska ha en konstruktor som dessutom tar en lösenordssträng som argument.

Klassen ska dessutom innehålla följande metoder:

* `tillsatt_ingrediens(ingrediens: str, mangd: float, losenord: str)` och
* `skriv_ut_recept(losenord: str)`

Om lösenordsargumentet som ges till någon av dessa metoder är felaktigt ska metoderna ge upphov till ett `ValueError`-undantag.

Om lösenordet är korrekt ska varje metod anropa den relevanta metoden i den överordnade klassen. Kopiera och klistra inte in något från `Trolldryck`-klassen.

Exempel på hur detta ska fungera:

```python
krympning = HemligTrolldryck("Krympning maximus", "hocuspocus")
krympning.tillsatt_ingrediens("Granrot", 1.5, "hocuspocus")
krympning.tillsatt_ingrediens("Magisk sand", 3.0, "hocuspocus")
krympning.tillsatt_ingrediens("Grodyngel", 4.0, "hocuspocus")
krympning.skriv_ut_recept("hocuspocus")

krympning.skriv_ut_recept("pocushocus") # FEL LÖSENORD
```

<sample-output>

Krympning maximus:
Granrot 1.5 gram
Magisk sand 3.0 gram
Grodyngel 4.0 gram
Traceback (most recent call last):
  File "hemlig_trolldryck.py", line 98, in <module>
    raise ValueError("Fel lösenord!")
ValueError: Fel lösenord!

</sample-output>

</programming-exercise>
