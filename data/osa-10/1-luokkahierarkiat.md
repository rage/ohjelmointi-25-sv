---
path: '/osa-10/1-luokkahierarkiat'
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

Låt oss ta en titt på två klassdefinitioner: `Student` och `Larare`. Getter- och sättar-metoder har utelämnats tills vidare för att hålla exemplet kort.

```python

class Opiskelija:

    def __init__(self, nimi: str, opnro: str, sposti: str, opintopisteet: str):
        self.nimi = nimi
        self.opnro = opnro
        self.sposti = sposti
        self.opintopisteet = opintopisteet

class Opettaja:

    def __init__(self, nimi: str, sposti: str, huone: str, opetusvuosia: int):
        self.nimi = nimi
        self.sposti = sposti
        self.huone = huone
        self.opetusvuosia = opetusvuosia

```

Även i ett avskalat exempel som ovan har vi redan en hel del upprepningar: båda klasserna innehåller attributen `namn` och `epost`. Det vore en bra idé att ha en enda attributdefinition, så att det räcker med en enda funktion för att redigera båda attributen.

Tänk dig till exempel att skolans e-postadress ändras. Alla adresser skulle behöva uppdateras. Vi skulle kunna skriva två separata versioner av i stort sett samma funktion:  

```python

def korjaa_email(o: Opiskelija):
    o.sposti = o.sposti.replace(".com", ".edu")

def korjaa_email2(o: Opettaja):
    o.sposti = o.sposti.replace(".com", ".edu")

```

Att skriva i stort sett samma sak två gånger är onödig upprepning, för att inte tala om att det fördubblar möjligheterna till fel. Det skulle vara en klar förbättring om vi kunde använda en enda funktion för att arbeta med instanser av båda klasserna.

Båda klasserna har också attribut som är unika för dem. Att bara kombinera alla attribut i en enda klass skulle innebära att alla instanser av klassen då skulle ha onödiga attribut, bara olika för olika instanser. Det verkar inte heller vara en idealisk situation.

## Arv

Objektorienterade programmeringsspråk innehåller vanligtvis en teknik som kallas arv (eng. inheritance). En klass kan ärva egenskaper från en annan klass. Förutom dessa ärvda egenskaper kan en klass också innehålla egenskaper som är unika för den.

Med detta i åtanke är det rimligt att klasserna `Larare` och `Student` har en gemensam bas eller föräldraklass `Person`:

 ```python

class Henkilo:

    def __init__(self, nimi: str, sposti: str):
        self.nimi = nimi
        self.sposti = sposti

 ```

Den nya klassen innehåller de egenskaper som delas av de andra två klasserna. Nu kan `Student` och `Larare` ärva dessa egenskaper och dessutom lägga till sina egna. :

Syntaxen för arv innebär helt enkelt att basklassens namn läggs till inom parentes på rubrikraden:

 ```python

class Henkilo:

    def __init__(self, nimi: str, sposti: str):
        self.nimi = nimi
        self.sposti = sposti

    def vaihda_spostitunniste(self, uusi_tunniste: str):
        vanha = self.sposti.split("@")[1]
        self.sposti = self.sposti.replace(vanha, uusi_tunniste)

class Opiskelija(Henkilo):

    def __init__(self, nimi: str, opnro: str, sposti: str, opintopisteet: str):
        self.nimi = nimi
        self.opnro = opnro
        self.sposti = sposti
        self.opintopisteet = opintopisteet

class Opettaja(Henkilo):

    def __init__(self, nimi: str, sposti: str, huone: str, opetusvuosia: int):
        self.nimi = nimi
        self.sposti = sposti
        self.huone = huone
        self.opetusvuosia = opetusvuosia

# Testi
if __name__ == "__main__":
    olli = Opiskelija("Olli Opiskelija", "1234", "olli@example.com", 0)
    olli.vaihda_spostitunniste("example.edu")
    print(olli.sposti)

    outi = Opettaja("Outi Ope", "outi@example.fi", "A123", 2)
    outi.vaihda_spostitunniste("example.ex")
    print(outi.sposti)

 ```

Både `Student` och `Larare` ärver klassen `Person`, så båda har de egenskaper som definieras i klassen Person, inklusive metoden `uppdatera_epost_doman`. Samma metod fungerar för instanser av båda de härledda klasserna.

 Låt oss titta på ett annat exempel. Vi har en `Bokhylla` som ärver klassen `BokLada`:

 ```python
class Kirja:
    """ Luokka mallintaa yksinkertaista kirjaa """
    def __init__(self, nimi: str, kirjailija: str):
        self.nimi = nimi
        self.kirjailija = kirjailija


class Kirjalaatikko:
    """ Luokka mallintaa laatikkoa, johon voidaan tallentaa kirjoja """

    def __init__(self):
        self.kirjat = []

    def lisaa_kirja(self, kirja: Kirja):
        self.kirjat.append(kirja)

    def listaa_kirjat(self):
        for kirja in self.kirjat:
            print(f"{kirja.nimi} ({kirja.kirjailija})")

class Kirjahylly(Kirjalaatikko):
    """ Luokka mallintaa yksinkertaista kirjahyllyä """

    def __init__(self):
        super().__init__()

    def lisaa_kirja(self, kirja: Kirja, paikka: int):
        self.kirjat.insert(paikka, kirja)


 ```

 Klassen `Bokhylla` innehåller metoden `tillägg_bok`. En metod med samma namn finns definierad i basklassen `BokLada`. Detta kallas överstyrning (eng. override): om en härledd klass har en metod med samma namn som basklassen, överstyr den härledda versionen originalet i instanser av den härledda klassen.

 Tanken i exemplet ovan är att en ny bok som läggs till i en BokLada alltid hamnar högst upp, men med en Bokhylla kan du själv ange platsen. Metoden `lista_böcker` fungerar likadant för båda klasserna, eftersom det inte finns någon överordnad metod i den härledda klassen.

 Låt oss prova dessa klasser:

 ```python

if __name__ == "__main__":
    # Luodaan pari kirjaa testiksi
    k1 = Kirja("7 veljestä", "Aleksis Kivi")
    k2 = Kirja("Sinuhe", "Mika Waltari")
    k3 = Kirja("Tuntematon sotilas", "Väinö Linna")

    # Luodaan kirjalaatikko ja lisätään kirjat sinne
    laatikko = Kirjalaatikko()
    laatikko.lisaa_kirja(k1)
    laatikko.lisaa_kirja(k2)
    laatikko.lisaa_kirja(k3)

    # Luodaan kirjahylly ja lisätään kirjat sinne (aina hyllyn alkupäähän)
    hylly = Kirjahylly()
    hylly.lisaa_kirja(k1, 0)
    hylly.lisaa_kirja(k2, 0)
    hylly.lisaa_kirja(k3, 0)


    # Tulostetaan
    print("Laatikossa:")
    laatikko.listaa_kirjat()

    print()

    print("Hyllyssä:")
    hylly.listaa_kirjat()

 ```

 <sample-output>

Laatikossa:
7 veljestä (Aleksis Kivi)
Sinuhe (Mika Waltari)
Tuntematon sotilas (Väinö Linna)

Hyllyssä:
Tuntematon sotilas (Väinö Linna)
Sinuhe (Mika Waltari)
7 veljestä (Aleksis Kivi)

 </sample-output>

Klassen Bokhylla har alltså också tillgång till metoden `lista_böcker`. Genom ärvning är metoden medlem i alla klasser som kommer från klassen `BokLada`.

## Arv och räckvidd av egenskaper

 En härledd klass ärver alla egenskaper från sin basklass. Dessa egenskaper är direkt åtkomliga i den härledda klassen, såvida de inte har definierats som privata i basklassen (med två understreck före egenskapens namn).

 Eftersom attributen för en Bokhylla är identiska med en BokLada, fanns det ingen anledning att skriva om konstruktorn för Bokhylla. Vi anropade helt enkelt basklassens konstruktor:

 ```python

 class Kirjahylly(Kirjalaatikko):

    def __init__(self):
        super().__init__()

```

Alla egenskaper i basklassen kan nås från den härledda klassen med funktionen `super()`. Argumentet `self` utelämnas från metodanropet, eftersom Python lägger till det automatiskt.

Men vad händer om attributen inte är identiska; kan vi fortfarande använda basklassens konstruktor på något sätt? Låt oss titta på en klass som heter `Avhandling` och som ärver klassen `Bok`. Den härledda klassen kan fortfarande anropa konstruktören från basklassen:

```python

class Kirja:
    """ Luokka mallintaa yksinkertaista kirjaa """

    def __init__(self, nimi: str, kirjailija: str):
        self.nimi = nimi
        self.kirjailija = kirjailija


class Gradu(Kirja):
    """ Luokka mallintaa gradua eli ylemmän korkeakoulututkinnon lopputyötä """

    def __init__(self, nimi: str, kirjailija: str, arvosana: int):
        super().__init__(nimi, kirjailija)
        self.arvosana = arvosana

```

Konstruktorn i `Avhandling`-klassen anropar konstruktorn i basklassen `Bok` med argumenten för `namn` och `forfattare`. Dessutom anger konstruktören i den härledda klassen värdet för attributet `vitsord`. Detta kan naturligtvis inte vara en del av basklassens konstruktor, eftersom basklassen inte har något sådant attribut.

Ovanstående klass kan användas på följande sätt:


```python

# Testataan
if __name__ == "__main__":
    gradu = Gradu("Python ja maailmankaikkeus", "Pekka Python", 3)

    # Tulostetaan kenttien arvot
    print(gradu.nimi)
    print(gradu.kirjailija)
    print(gradu.arvosana)

```

<sample-output>

Python ja maailmankaikkeus
Pekka Python
3

</sample-output>

Även om en härledd klass åsidosätter en metod i sin basklass kan den härledda klassen fortfarande anropa den åsidosatta metoden i basklassen. I följande exempel har vi ett grundläggande `BonusKort` och ett särskilt `PlatinumKort` för särskilt lojala kunder. Metoden `rakna_bonus` är åsidosatt i den härledda klassen, men den åsidosatta metoden anropar basmetoden:

```python

class Tuote:

    def __init__(self, nimi: str, hinta: float):
        self.nimi = nimi
        self.hinta = hinta

class Bonuskortti:

    def __init__(self):
        self.ostetut_tuotteet = []

    def lisaa_tuote(self, tuote: Tuote):
        self.ostetut_tuotteet.append(tuote)

    def laske_bonus(self):
        bonus = 0
        for tuote in self.ostetut_tuotteet:
            bonus += tuote.hinta * 0.05

        return bonus

class Platinakortti(Bonuskortti):

    def __init__(self):
        super().__init__()

    def laske_bonus(self):
        # Kutsutaan yliluokan metodia...
        bonus = super().laske_bonus()

        # ...ja lisätään vielä viisi prosenttia päälle
        bonus = bonus * 1.05
        return bonus


```

Bonusen för ett PlatinumKort beräknas alltså genom att anropa den överstyrda metoden i basklassen och sedan lägga till 5 procent extra till basresultatet. Ett exempel på hur dessa klasser används: 

```python
if __name__ == "__main__":
    kortti = Bonuskortti()
    kortti.lisaa_tuote(Tuote("Banaanit", 6.50))
    kortti.lisaa_tuote(Tuote("Mandariinit", 7.95))
    bonus = kortti.laske_bonus()

    kortti2 = Platinakortti()
    kortti2.lisaa_tuote(Tuote("Banaanit", 6.50))
    kortti2.lisaa_tuote(Tuote("Mandariinit", 7.95))
    bonus2 = kortti2.laske_bonus()

    print(bonus)
    print(bonus2)
```

<sample-output>

0.7225
0.7586250000000001

</sample-output>

<programming-exercise name='Kannettava tietokone' tmcname='osa10-01_kannettava_tietokone'>

Tehtäväpohjassa on määritelty luokka `Tietokone`, jolla on attribuutit `malli` ja `nopeus`.

Kirjoita luokka `KannettavaTietokone`, joka _perii luokan Tietokone_. Luokka saa konstruktorissa luokan Tietokone attribuuttien lisäksi kolmannen kokonaislukutyyppisen attribuutin `paino`.

Kirjoita luokkaan lisäksi metodi `__str__`, jonka avulla voi tulostaa esimerkkisuorituksen mukaisen tulosteen olion tilasta.

Esimerkki:

```python
ipm = KannettavaTietokone("IPM MikroMauri", 1500, 2)
print(ipm)
```

<sample-output>

IPM MikroMauri, 1500 MHz, 2 kg

</sample-output>

</programming-exercise>

<programming-exercise name='Pelimuseo' tmcname='osa10-02_pelimuseo'>

Tehtäväpohjassa on määritelty luokat `Tietokonepeli` ja `Pelivarasto`. Pelivarastoon voidaan säilöä tietokonepelejä.

Tutustu luokkien ohjelmakoodiin ja kirjoita sitten uusi luokka `Pelimuseo`, joka perii luokan `Pelivarasto`.

Pelimuseo-luokassa _uudelleentoteutetaan_ metodi `anna_pelit()` niin, että se palauttaa listassa ainoastaan ne pelit, jotka on tehty ennen vuotta 1990.

Lisäksi luokassa tulee olla konstruktori, josta _kutsutaan yliluokan Pelivarasto konstruktoria_. Konstruktorilla ei ole parametreja.

Esimerkiksi:

```python
museo = Pelimuseo()
museo.lisaa_peli(Tietokonepeli("Pacman", "Namco", 1980))
museo.lisaa_peli(Tietokonepeli("GTA 2", "Rockstar", 1999))
museo.lisaa_peli(Tietokonepeli("Bubble Bobble", "Taito", 1986))
for peli in museo.anna_pelit():
    print(peli.nimi)
```

<sample-output>

Pacman
Bubble Bobble

</sample-output>

</programming-exercise>

<programming-exercise name='Pinta-alat' tmcname='osa10-03_pinta_alat'>

Tehtäväpohjan mukana tulee luokka `Suorakulmio` joka nimensä mukaisesti mallintaa [suorakulmiota](https://fi.wikipedia.org/wiki/Suorakulmio). Luokkaa käytetään seuraavasti:

```python
suorakulmio = Suorakulmio(2, 3)
print(suorakulmio)
print("pinta-ala:", suorakulmio.pinta_ala())
```

<sample-output>

suorakulmio 2x3
pinta-ala: 6

</sample-output>

## Neliö

Toteuta luokka `Nelio` joka perii luokan `Suorakulmio`. Suorakulmiosta poiketen [neliön](https://fi.wikipedia.org/wiki/Neli%C3%B6_(geometria)) kaikki sivut ovat saman pituisia, eli neliö on eräänlainen yksinkertaisempi erikoistapaus suorakulmiosta. Luokka ei saa määritellä uusia attribuutteja!

Luokkaa käytetään seuraavasti:

```python
nelio = Nelio(4)
print(nelio)
print("pinta-ala:", nelio.pinta_ala())
```

<sample-output>

neliö 4x4
pinta-ala: 16

</sample-output>

</programming-exercise>

<programming-exercise name='Sanapeli' tmcname='osa10-04_sanapeli'>

Tehtäväpohja sisältää valmiin luokan `Sanapeli`, joka tarjoaa perustoiminnallisuuden erilaisten sanapelien pelaamiseen:

```python
import random

class Sanapeli():
    def __init__(self, kierrokset: int):
        self.voitot1 = 0
        self.voitot2 = 0
        self.kierrokset = kierrokset

    def kierroksen_voittaja(self, pelaaja1_sana: str, pelaaja2_sana: str):
        # arvotaan voittaja
        return random.randint(1, 2)

    def pelaa(self):
        print("Sanapeli:")
        for i in range(1, self.kierrokset+1):
            print(f"kierros {i}")
            vastaus1 = input("pelaaja1: ")
            vastaus2 = input("pelaaja2: ")

            if self.kierroksen_voittaja(vastaus1, vastaus2) == 1:
                self.voitot1 += 1
                print("pelaaja 1 voitti")
            elif self.kierroksen_voittaja(vastaus1, vastaus2) == 2:
                self.voitot2 += 1
                print("pelaaja 2 voitti")
            else:
                pass # tasapeli

        print("peli päättyi, voitot:")
        print(f"pelaaja 1: {self.voitot1}")
        print(f"pelaaja 2: {self.voitot2}")
```

Peliä käytetään seuraavasti:

```python
p = Sanapeli(3)
p.pelaa()
```

Esimerkkitulostus

<sample-output>

Sanapeli:
kierros 1
pelaaja1: **pitkäsana**
pelaaja2: **??**
pelaaja 2 voitti
kierros 2
pelaaja1: **olen paras**
pelaaja2: **mitä?**
pelaaja 1 voitti
kierros 3
pelaaja1: **kuka voittaa**
pelaaja2: **minä**
pelaaja 1 voitti
peli päättyi voitot:
pelaaja 1: 2
pelaaja 2: 1

</sample-output>

Tässä pelin "perusversiossa" voittaja ratkaistaan arpomalla, pelaajien antamilla syötteillä ei ole tulokseen vaikutusta.

## Pisin sana voittaa

Tee nyt luokka `PisinSana` eli pelin versio, missä kunkin kierroksen voittaja on sen kierroksen aikana pidemmän sanan syöttänyt käyttäjä.

Uusi versio toteuteaan _perimällä_ luokka `Sanapeli` ja ylikirjoittamalla sen metodi `kierroksen_voittaja` sopivalla tavalla. Uuden luokan runko on siis seuraavanlainen

```python
class PisinSana(Sanapeli):
    def __init__(self, kierrokset: int):
        super().__init__(kierrokset)

    def kierroksen_voittaja(self, pelaaja1_sana: str, pelaaja2_sana: str):
        # tänne voittajan ratkaiseva koodi
```

Esimerkki toiminnasta:

```python
p = PisinSana(3)
p.pelaa()
```

<sample-output>

Sanapeli:
kierros 1
pelaaja1: **lyhyt**
pelaaja2: **pitkäsana**
pelaaja 2 voitti
kierros 2
pelaaja1: **sana**
pelaaja2: **vat?**
kierros 3
pelaaja1: **olen paras**
pelaaja2: **minäpäs**
pelaaja 1 voitti
peli päättyi, voitot:
pelaaja 1: 1
pelaaja 2: 1

</sample-output>

## Eniten vokaaleja voittaa

Tee nyt luokka `EnitenVokaaleja` eli pelin versio, missä kunkin kierroksen voittaja on se pelaaja, jonka sanassa oli enemmän vokaaleja.

## Kivi, paperi, sakset

Tee nyt luokka `KiviPaperiSakset` joka mallintaa nimensä mukaisesti [kivi, paperi ja sakset](https://fi.wikipedia.org/wiki/Kivi,_paperi_ja_sakset) -peliä.

Pelin säännöt ovat seuraavat:

- kivi voittaa sakset (kivellä voi rikkoa sakset eikä saksilla voi leikata kiveä)
- paperi voittaa kiven (kiven voi peittää paperilla)
- sakset voittaa paperin (saksilla voi leikata paperia)

Jos pelaajan syöte on epäkelpo, eli se ei ole mikään sanoista _kivi, paperi, sakset_ pelaaja häviää kierroksen, ellei molempien syöte ole epäkelpo.

Esimerkki toiminnasta:

```python
p = KiviPaperiSakset(4)
p.pelaa()
```

<sample-output>

Sanapeli:
kierros 1
pelaaja1: **kivi**
pelaaja2: **kivi**
kierros 2
pelaaja1: **kivi**
pelaaja2: **paperi**
pelaaja 2 voitti
kierros 3
pelaaja1: **sakset**
pelaaja2: **paperi**
pelaaja 1 voitti
kierros 4
pelaaja1: **paperi**
pelaaja2: **dynamiitti**
pelaaja 1 voitti
peli päättyi, voitot:
pelaaja 1: 2
pelaaja 2: 1

</sample-output>

</programming-exercise>
