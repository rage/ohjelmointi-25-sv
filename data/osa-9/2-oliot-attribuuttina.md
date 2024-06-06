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

Vi har redan sett exempel på klasser som har listor som attribut. Eftersom det alltså inte finns något som hindrar oss från att inkludera mutabla objekt som attribut i våra klasser, kan vi lika gärna använda instanser av våra egna klasser som attribut i andra klasser som vi själva har definierat. I följande exempel kommer vi att definiera klasserna `Kurs`, `Student` och `AvslutadKurs`. En avslutad kurs använder sig av de två första klasserna. Klassdefinitionerna är mycket korta och enkla för att vi bättre ska kunna koncentrera oss på tekniken att använda instanser av våra egna klasser som attribut.

Vi kommer att anta att varje klass definieras i en separat fil.

Först definierar vi klassen `Kurs` i en fil med namnet `kurs.py`:

```python
class Kurssi:
    def __init__(self, nimi: str, koodi: str, opintopisteet: int):
        self.nimi = nimi
        self.koodi = koodi
        self.opintopisteet = opintopisteet
```

Till näst, klassen `Student` i en fil med namnet `student.py`:

```python
class Opiskelija:
    def __init__(self, nimi: str, opiskelijanumero: str, opintopisteet: int):
        self.nimi = nimi
        self.opiskelijanumero = opiskelijanumero
        self.opintopisteet = opintopisteet
```

Slutligen är klassen `AvslutadKurs` definierad i en fil med namned `avslutadkurs.py`. Eftersom den använder de två andra klasserna, måste de importeras innan de kan användas:

```python
from kurssi import Kurssi
from opiskelija import Opiskelija

class Opintosuoritus:
    def __init__(self, opiskelija: Opiskelija, kurssi: Kurssi, arvosana: int):
        self.opiskelija = opiskelija
        self.kurssi = kurssi
        self.arvosana = arvosana
```

Här är ett exempel av en huvudfunktion som lägger till några avslutade kurser i en lista:

```python
from opintosuoritus import Opintosuoritus
from kurssi import Kurssi
from opiskelija import Opiskelija

# Luodaan lista opiskelijoista
opiskelijat = []
opiskelijat.append(Opiskelija("Olli", "1234", 10))
opiskelijat.append(Opiskelija("Pekka", "3210", 23))
opiskelijat.append(Opiskelija("Leena", "9999", 43))
opiskelijat.append(Opiskelija("Tiina", "3333", 8))

# Kurssi Ohjelmoinnin perusteet
ohpe = Kurssi("Ohjelmoinnin perusteet", "ohpe1", 5)

# Annetaan suoritukset kaikille opiskelijoille, kaikille arvosanaksi 3
suoritukset = []
for opiskelija in opiskelijat:
    suoritukset.append(Opintosuoritus(opiskelija, ohpe, 3))

# Tulostetaan kaikista suorituksista opiskelijan nimi
for suoritus in suoritukset:
    print(suoritus.opiskelija.nimi)
```

<sample-output>

Olli
Pekka
Leena
Tiina

</sample-output>

Vad exakt händer med alla prickar på raden `print(kurs.student.namn)`?

* `kurs` är en instans av klassen `AvslutadKurs`
* `student` refererar till ett attribut i objektet `AvslutadKurs`, som är ett objekt av typen `Student`
* attributnamnet i `Student`-objektet innehåller namnet på studenten

## När är en import nödvändig?

I exemplen ovan förekommer en `import`-sats ganska många gånger:

```python
from opintosuoritus import Opintosuoritus
from kurssi import Kurssi
from opiskelija import Opiskelija

# koodi
```

En importsats är bara nödvändig när man använder kod som är definierad någonstans utanför den aktuella filen (eller Python-tolksessionen). Detta inkluderar situationer där vi vill använda något som är definierat i Pythons standardbibliotek. Modulen `math` innehåller till exempel vissa matematiska operationer:

```python
import math

x = 10
print(f"luvun {x} {neliöjuuri math.sqrt(x)}")
```

I exemplet ovan antog vi att de tre klasserna definierades i var sin fil och att huvudfunktionen kördes från ytterligare en fil. Det var därför `import`-satserna var nödvändiga.

Om all programkod skrivs i samma fil, vilket de flesta övningarna i den här kursen rekommenderar, behöver du **inte** `import`-satser för att använda de klasser du har definierat.

Ifall du märker dig själv skriva något i stil med

```python
from henkilo import Henkilo

# koodi
```

är det sannolikt att du förstått nånting felaktigt. Ifall du behöver en uppfriskare så introducerades `import`deklarationen för första gången i [del 7](/osa-7/1-moduulit/) av kursmaterialet.

<programming-exercise name='Lemmikit' tmcname='osa09-06_lemmikki'>

Tehtäväpohjassa tulee kaksi luokkaa, `Henkilo` ja `Lemmikki`. Jokaisella henkilöllä on yksi lemmikki. Täydennä luokan `Henkilo` metodia `__str__` siten, että metodi palauttaa merkkijonon, joka kertoo henkilön nimen lisäksi lemmikin nimen ja rodun alta löytyvät esimerkkitulosteen mukaisesti.

Huomaa, että metodin palauttaman merkkijonon pitää olla _täsmälleen samanlainen kuin esimerkkitulosteessa esitetty_!

```python
hulda = Lemmikki("Hulda", "sekarotuinen koira")
leevi = Henkilo("Leevi", hulda)

print(leevi)
```

<sample-output>

Leevi, kaverina Hulda, joka on sekarotuinen koira

</sample-output>

**Huom:** koska kaikki koodi tulee samaan tiedostoon, et tarvitse tehtävässä `import`:ia ollenkaan!

</programming-exercise>

## En lista med objekt som attribut till ett objekt

I exemplen ovan använde vi enstaka instanser av andra klasser som attribut: en Person har ett enda Husdjur som attribut, och en AvslutadKurs har en Student och en Kurs som attribut.

I objektorienterad programmering är det ofta så att vi vill ha en samling objekt som attribut. Till exempel följer relationen mellan ett idrottslag och dess spelare detta mönster:

```python
class Pelaaja:
    def __init__(self, nimi: str, maalit: int):
        self.nimi = nimi
        self.maalit = maalit

    def __str__(self):
        return f"{self.nimi} (maaleja {self.maalit})"

class Joukkue:
    def __init__(self, nimi: str):
        self.nimi = nimi
        self.pelaajat = []

    def lisaa_pelaaja(self, pelaaja: Pelaaja):
        self.pelaajat.append(pelaaja)

    def yhteenveto(self):
        maalit = []
        for pelaaja in self.pelaajat:
            maalit.append(pelaaja.maalit)
        print("Joukkue", self.nimi)
        print("Pelaajia", len(self.pelaajat))
        print("Pelaajien maalimäärät", maalit)
```

Ett exempel på hur vår klass fungerar:

```python
kupa = Joukkue("Kumpulan pallo")
kupa.lisaa_pelaaja(Pelaaja("Erkki", 10))
kupa.lisaa_pelaaja(Pelaaja("Emilia", 22))
kupa.lisaa_pelaaja(Pelaaja("Antti", 1))
kupa.yhteenveto()
```

<sample-output>

Joukkue Kumpulan pallo
Pelaajia 3
Pelaajien maalimäärät [10, 22, 1]

</sample-output>

<programming-exercise name='Lahjapakkaus' tmcname='osa09-07_lahjapakkaus'>

Tässä tehtävässä harjoitellaan lahjojen pakkaamista. Tehdään luokat `Lahja` ja `Pakkaus`. Lahjalla on nimi ja paino, ja pakkaus sisältää lahjoja.

## Lahja-luokka

Tee luokka `Lahja`, josta muodostetut oliot kuvaavat erilaisia lahjoja. Tallennettavat tiedot ovat tavaran nimi ja paino (kg). Luokan olioiden tulee toimia seuraavasti:

```python
kirja = Lahja("Aapiskukko", 2)

print("Lahjan nimi:", kirja.nimi)
print("Lahjan paino:" ,kirja.paino)
print("Lahja:", kirja)
```

Ohjelman tulostuksen tulisi olla seuraava:

<sample-output>

Lahjan nimi: Aapiskukko
Lahjan paino: 2
Lahja: Aapiskukko (2 kg)

</sample-output>

## Pakkaus-luokka

Tee luokka `Pakkaus`, johon voi lisätä lahjoja ja joka pitää kirjaa pakkauksessa olevien lahjojen yhteispainosta. Luokassa tulee olla seuraavat metodit

- `lisaa_lahja(self, lahja: Lahja)`, joka lisää parametrina annettavan lahjan pakkaukseen. Metodi ei palauta mitään arvoa.
- `yhteispaino(self)`, joka palauttaa pakkauksessa olevien lahjojen yhteispainon.

Seuraavassa on luokan käyttöesimerkki:

```python
kirja = Lahja("Aapiskukko", 2)

pakkaus = Pakkaus()
pakkaus.lisaa_lahja(kirja)
print(pakkaus.yhteispaino())

cd_levy = Lahja("Pink Floyd: Dark side of the moon", 1)
pakkaus.lisaa_lahja(cd_levy)
print(pakkaus.yhteispaino())
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
class Pelaaja:
    def __init__(self, nimi: str, maalit: int):
        self.nimi = nimi
        self.maalit = maalit

    def __str__(self):
        return f"{self.nimi} (maaleja {self.maalit})"

class Joukkue:
    def __init__(self, nimi: str):
        self.nimi = nimi
        self.pelaajat = []

    def lisaa_pelaaja(self, pelaaja: Pelaaja):
        self.pelaajat.append(pelaaja)

    def etsi(self, nimi: str):
        for pelaaja in self.pelaajat:
            if pelaaja.nimi == nimi:
                return pelaaja
        return None
```

Låt oss testa vår funktion:

```python
kupa = Joukkue("Kumpulan pallo")
kupa.lisaa_pelaaja(Pelaaja("Erkki", 10))
kupa.lisaa_pelaaja(Pelaaja("Emilia", 22))
kupa.lisaa_pelaaja(Pelaaja("Antti", 1))

pelaaja1 = kupa.etsi("Antti")
print(pelaaja1)
pelaaja2 = kupa.etsi("Jukkis")
print(pelaaja2)
```

<sample-output>

Antti (maaleja 1)
None

</sample-output>

Var dock försiktig med `None`. Det kan ibland orsaka mer problem än det löser. Det är ett vanligt programmeringsfel att försöka komma åt en metod eller ett attribut via en referens som utvärderas till `None`:

```python
kupa = Joukkue("Kumpulan pallo")
kupa.lisaa_pelaaja(Pelaaja("Erkki", 10))

pelaaja = kupa.etsi("Jukkis")
print(f"Jukkiksen maalimäärä {pelaaja.maalit}")
```

Exekverande av ovanstående skulle orsaka ett fel:

<sample-output>

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'NoneType' object has no attribute 'maalit'

</sample-output>

Det är en god idé att kontrollera om det finns `None` innan du försöker komma åt några attribut eller metoder för returvärden: 

```python
kupa = Joukkue("Kumpulan pallo")
kupa.lisaa_pelaaja(Pelaaja("Erkki", 10))

pelaaja = kupa.etsi("Jukkis")
if pelaaja is not None:
    print(f"Jukkiksen maalimäärä {p.maalit}")
else:
    print(f"Jukkis ei pelaa Kumpulan pallossa :(")
```

<sample-output>

Jukkis ei pelaa Kumpulan pallossa :(

</sample-output>

<programming-exercise name='Huoneen lyhin' tmcname='osa09-08_huoneen_lyhin'>

Tehtäväpohjassa on valmiina luokka `Henkilo`. Henkilöllä on nimi ja pituus. Toteutetaan tässä tehtävässä luokka `Huone`, jonne voi lisätä henkilöitä ja josta voi hakea ja poistaa lyhimmän henkilön.

## Huone

Luo luokka `Huone`, jonka sisällä on lista henkilöitä ja jolla on seuraavat metodit:

- `lisaa(henkilo: Henkilo)` lisää huoneeseen parametrina annetun henkilön.
- `on_tyhja()` - palauttaa arvon `True` tai `False`, joka kertoo, onko huone tyhjä.
- `tulosta_tiedot()` tulostaa huoneessa olevat henkilöt

Seuraavassa käyttöesimerkki:

```python
huone = Huone()
print("Huone tyhjä?", huone.on_tyhja())
huone.lisaa(Henkilo("Lea", 183))
huone.lisaa(Henkilo("Kenya", 182))
huone.lisaa(Henkilo("Auli", 186))
huone.lisaa(Henkilo("Nina", 172))
huone.lisaa(Henkilo("Terhi", 185))
print("Huone tyhjä?", huone.on_tyhja())
huone.tulosta_tiedot()
```

<sample-output>

Huone tyhjä? True
Huone tyhjä? False
Huoneessa 5 henkilöä, yhteispituus 908 cm
Lea (183 cm)
Kenya (182 cm)
Auli (186 cm)
Nina (172 cm)
Terhi (185 cm)

</sample-output>

## Lyhin henkilö

Lisää luokalle `Huone` metodi `lyhin()`, joka palauttaa huoneeseen lisätyistä henkilöistä lyhimmän. Mikäli huone on tyhjä, metodi palauttaa `None`-viitteen. Metodin ei tule poistaa henkilöä huoneesta.

```python
huone = Huone()

print("Huone tyhjä?", huone.on_tyhja())
print("Lyhin:", huone.lyhin())

huone.lisaa(Henkilo("Lea", 183))
huone.lisaa(Henkilo("Kenya", 182))
huone.lisaa(Henkilo("Nina", 172))
huone.lisaa(Henkilo("Auli", 186))

print()

print("Huone tyhjä?", huone.on_tyhja())
print("Lyhin:", huone.lyhin())

print()

huone.tulosta_tiedot()
```

<sample-output>

Huone tyhjä? True
Lyhin: None

Huone tyhjä? False
Lyhin: Nina

Huoneessa 4 henkilöä, yhteispituus 723 cm
Lea (183 cm)
Kenya (182 cm)
Nina (172 cm)
Auli (186 cm)

</sample-output>

## Huoneesta ottaminen

Lisää luokalle `Huone` metodi `poista_lyhin()`, joka poistaa ja palauttaa huoneesta lyhimmän henkilön. Mikäli huone on tyhjä, metodi palauttaa `None`-viitteen.

```python
huone = Huone()

huone.lisaa(Henkilo("Lea", 183))
huone.lisaa(Henkilo("Kenya", 182))
huone.lisaa(Henkilo("Nina", 172))
huone.lisaa(Henkilo("Auli", 186))
huone.tulosta_tiedot()

print()

poistettu = huone.poista_lyhin()
print(f"Otettiin huoneesta {poistettu.nimi}")

print()

huone.tulosta_tiedot()
```

<sample-output>

Huoneessa 4 henkilöä, yhteispituus 723 cm
Lea (183 cm)
Kenya (182 cm)
Nina (172 cm)
Auli (186 cm)

Otettiin huoneesta Nina

Huoneessa 3 henkilöä, yhteispituus 551 cm
Lea (183 cm)
Kenya (182 cm)
Auli (186 cm)

</sample-output>

**Vihje**: [osassa 4](/osa-4/3-listat#alkioiden-lisaaminen-ja-poistaminen) kerrottiin, miten alkion poistaminen listalta onnistuu.

**Vihje2**: muista, että metodissa on mahdollista kutsua saman olion toista metodia. Eli seuraava koodi toimii:

```python
class Huone:
    # ...
    def lyhin(self):
        # koodi

    def poista_lyhin(self):
        lyhin_henkilo = self.lyhin()
        # ...
```

</programming-exercise>
