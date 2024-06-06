---
path: '/osa-10/2-nakyvyysmaareet'
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

class Muistikirja:
    """ Muistikirjaan voidaan tallentaa muistiinpanoja merkkijonoina """

    def __init__(self):
        # yksityinen attribuutti
        self.__muistiinpanot = []

    def lisaa_muistiinpano(self, muistiinpano):
        self.__muistiinpanot.append(muistiinpano)

    def palauta_muistiinpano(self, indeksi):
        return self.__muistiinpanot[indeksi]

    def kaikki_muistiinpanot(self):
        return ",".join(self.__muistiinpanot)

```

Om klassens integritet är viktig är det vettigt att göra listattributen `anteckningar` privat. Klassen förser trots allt klienten med lämpliga metoder för att lägga till och bläddra i anteckningar. Detta tillvägagångssätt blir problematiskt om vi definierar en ny klass `AnteckningsbokPro`, som ärver `Anteckningsbok`-klassen. Det privata listattributet är inte tillgängligt för klienten, men det är inte heller tillgängligt för de härledda klasserna. Om vi försöker komma åt det, som i metoden `hitta_anteckningar` nedan, får vi ett felmeddelande:

```python
class MuistikirjaPro(Muistikirja):
    """ Parempi muistikirja haku- ja järjestystoiminnoilla """
    def __init__(self):
        # Tämä on ok, koska luokan Muistikirja konstruktori
        # on julkinen
        super().__init__()

    # Tämä antaa virheen
    def etsi_muistiinpanot(self, hakusana):
        loydetty = []
        # Attribuutti __muistiinpanot on yksityinen, eikä näy
        # aliluokalle
        for muistiinpano in self.__muistiinpanot:
            if hakusana in muistiinpano:
                loydetty.append(muistiinpano)

        return loydetty

```

<sample-output>

AttributeError: 'MuistikirjaPro' object has no attribute '_MuistikirjaPro__muistiinpanot'

</sample-output>



## Skyddade egenskaper

Många objektorienterade programmeringsspråk har en funktion, oftast ett speciellt nyckelord, för att skydda egenskaper. Detta innebär att en egenskap ska vara dold för klassens klienter, men hållas tillgänglig för dess underklasser. Python avskyr i allmänhet nyckelord, så ingen sådan funktion är direkt tillgänglig i Python. Istället finns det en konvention för att markera skyddade egenskaper på ett visst sätt.

Kom ihåg att en egenskap kan döljas genom att prefixera dess namn med två understreck:

```python

def __init__(self):
    self.__muistiinpanot = []

```

Den överenskomna konventionen för att skydda en egenskap är att prefixera namnet med endast ett understreck. Nu är detta bara en konvention. Ingenting hindrar en programmerare från att bryta mot konventionen, men det anses vara en dålig programmeringspraxis.

```python

def __init__(self):
    self._muistiinpanot = []

```

Nedan har vi hela Anteckningsbok-exemplet, med skyddade `_anteckningar` istället för privata `__anteckningar`:

```python

class Muistikirja:
    """ Muistikirjaan voidaan tallentaa muistiinpanoja merkkijonoina """

    def __init__(self):
        # suojattu attribuutti
        self._muistiinpanot = []

    def lisaa_muistiinpano(self, muistiinpano):
        self._muistiinpanot.append(muistiinpano)

    def palauta_muistiinpano(self, indeksi):
        return self._muistiinpanot[indeksi]

    def kaikki_muistiinpanot(self):
        return ",".join(self._muistiinpanot)

class MuistikirjaPro(Muistikirja):
    """ Parempi muistikirja haku- ja järjestystoiminnoilla """
    def __init__(self):
        # Tämä on ok, koska luokan Muistikirja konstruktori
        # on julkinen
        super().__init__()

    # Nyt metodi toimii, koska suojattu attribuutti näkyy
    # aliluokalle
    def etsi_muistiinpanot(self, hakusana):
        loydetty = []
        for muistiinpano in self._muistiinpanot:
            if hakusana in muistiinpano:
                loydetty.append(muistiinpano)

        return loydetty

```

Nedan har vi en praktisk tabell för synligheten av attribut med olika åtkomstmodifierare:

Näkyvyysmääre	| Esimerkki | Näkyy asiakkaalle | Näkyy aliluokalle
:--:|:----:|:----:|:----:
Julkinen | `self.nimi` | kyllä | kyllä
Suojattu | `self._nimi` | ei | kyllä
Yksityinen | `self.__nimi` | ei | ei

Åtkomstmodifierare fungerar på samma sätt med alla egenskaper. I klassen `Person` nedan har vi till exempel den skyddade metoden `kapitalisera_initialer` Den kan användas från den härledda klassen `Fotbollsspelare`: 

```python

class Henkilo:
    def __init__(self, nimi: str):
        self._nimi = self._isot_alkukirjaimet(nimi)

    def _isot_alkukirjaimet(self, nimi):
        nimi_isoilla = []
        for n in nimi.split(" "):
            nimi_isoilla.append(n.capitalize())

        return " ".join(nimi_isoilla)

    def __repr__(self):
        return self.__nimi

class Jalkapalloilija(Henkilo):

    def __init__(self, nimi: str, lempinimi: str, pelipaikka: str):
        super().__init__(nimi)
        # metodia voi kutsua, koska se on suojattu yliluokassa
        self.__lempinimi = self._isot_alkukirjaimet(lempinimi)
        self.__pelipaikka = pelipaikka

    def __repr__(self):
        r =  f"Jalkapalloilija - nimi:{self._nimi}, lempinimi: {self.__lempinimi}"
        r += f", pelipaikka: {self.__pelipaikka}"
        return r

# Testataan
if __name__ == "__main__":
    jp = Jalkapalloilija("petri pythonen", "pyttis", "hyökkääjä")
    print(jp)

```

<sample-output>

Jalkapalloilija - nimi:Petri Pythonen, lempinimi: Pyttis, pelipaikka: hyökkääjä

</sample-output>


<programming-exercise name='Superryhmä' tmcname='osa10-05_superryhma'>

Tehtäväpohjassa on valmiina luokka `SuperSankari`.

Kirjoita luokka `SuperRyhma`, joka mallintaa supersankareista koostuvaa ryhmää. Luokalla pitää olla seuraava piirteet:

* **Suojatut** attribuutit nimi (merkkijono), kotipaikka (merkkijono) ja jasenet (lista)
* Konstruktori, joka saa parametrikseen tässä järjestyksessä nimen ja kotipaikan
* Havainnointimetodit nimelle ja kotipaikalle
* Metodi `lisaa_jasen(sankari: SuperSankari)`, joka lisää uuden jäsenen ryhmään
* Metodi `tulosta_ryhma`, joka tulostaa ryhmän ja sen jäsenten tiedot alla olevan esimerkin mukaisesti

Esimerkki luokan käytöstä:

```python
supermiekkonen = SuperSankari("Supermiekkonen", "Supernopeus, supervoimakkuus")
nakymaton = SuperSankari("Näkymätön Makkonen", "Näkymättömyys")
ryhma_z = SuperRyhma("Ryhmä Z", "Kälviä")

ryhma_z.lisaa_jasen(supermiekkonen)
ryhma_z.lisaa_jasen(nakymaton)
ryhma_z.tulosta_ryhma()
```

<sample-output>

Ryhmä Z, Kälviä
Jäsenet:
Supermiekkonen, superkyvyt: Supernopeus, supervoimakkuus
Näkymätön Makkonen, superkyvyt: Näkymättömyys

</sample-output>

[Tämän](/osa-9/3-kapselointi#asetus--ja-havainnointimetodit) luvun kertaaminen voi olla hyödyksi.

</programming-exercise>

<programming-exercise name='Salainen taikajuoma' tmcname='osa10-06_salainen_taikajuoma'>

Tehtäväpohjassa on luokka `Taikajuoma`, johon käyttäjä voi tallentaa reseptin. Luokasta löytyy konstruktorin lisäksi metodit

* `lisaa_aines(ainesosa: str, maara: float)` ja
* `tulosta_resepti()`

Kirjoita `Taikajuoma`-luokan perivä luokka `SalainenTaikajuoma`, jolla resepti voidaan suojata salasanalla.

Uusi luokka saa konstruktorissa taikajuoman nimen lisäksi salasanan.

Lisäksi luokalla on metodit

* `lisaa_aines(ainesosa: str, maara: float, salasana: str)` ja
* `tulosta_resepti(salasana: str)`

Jos metodeja kutsutaan väärällä salasanalla, ne antavat `ValueError`-poikkeuksen.

Uudet metodit kutsuvat perityn luokan metodeja, jos salasana on oikein! Älä siis leikkaa ja liimaa toteutuksia luokasta Taikajuoma.

Esimerkki luokan käytöstä:

```python
kutistus = SalainenTaikajuoma("Kutistus maksimus", "hokkuspokkus")
kutistus.lisaa_aines("Kärpässieni", 1.5, "hokkuspokkus")
kutistus.lisaa_aines("Taikahiekka", 3.0, "hokkuspokkus")
kutistus.lisaa_aines("Sammakonkutu", 4.0, "hokkuspokkus")
kutistus.tulosta_resepti("hokkuspokkus")

kutistus.tulosta_resepti("pokkushokkus") # VÄÄRÄ SALASANA!
```

<sample-output>

Kutistus maksimus:
Kärpässieni 1.5 grammaa
Taikahiekka 3.0 grammaa
Sammakonkutu 4.0 grammaa
Traceback (most recent call last):
  File "salaiset_taikajuomat.py", line 98, in <module>
    raise ValueError("Väärä salasana!")
ValueError: Väärä salasana!

</sample-output>

</programming-exercise>
