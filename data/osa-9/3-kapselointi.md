---
path: '/osa-9/3-kapselointi'
title: 'Inkapsling'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Vet du vad inkapsling innebär
- Kommer du att kunna skapa privata attribut
- Vet du hur du skapar gettar och sättare för dina attribut

</text-box>

I objektorienterad programmering avser termen klient ett program som använder en klass eller instanser av en klass. En klass erbjuder klienten tjänster genom vilka klienten kan komma åt de objekt som skapats baserat på klassen. Målen här är att

1) användningen av en klass och/eller objekt är så enkel som möjligt ur klientens synvinkel
2) integriteten för varje objekt bevaras hela tiden

Ett objekts integritet innebär att objektets tillstånd alltid förblir acceptabelt. I praktiken innebär detta att värdena på objektets attribut alltid är acceptabla. Ett objekt som representerar ett datum ska till exempel aldrig ha 13 som värde för månaden, ett objekt som representerar en student ska aldrig ha ett negativt tal som värde för uppnådda studiepoäng och så vidare.

Låt oss ta en titt på en klass som heter Student:

```python
class Opiskelija:
    def __init__(self, nimi: str, opiskelijanumero: str):
        self.nimi = nimi
        self.opiskelijanumero = opiskelijanumero
        self.opintopisteet = 0

    def lisaa_suoritus(self, opintopisteet):
        if opintopisteet > 0:
            self.opintopisteet += opintopisteet
```

`Student`objektet erbjuder sina klienter metoden `tillägg_poäng`, som gör det möjligt för klienten att lägga till ett angivet antal studiepoäng till studentens totala antal. Metoden säkerställer att värdet som skickas som argument är över noll. Följande kod lägger till studiepoäng vid tre tillfällen:

```python
oskari = Opiskelija("Oskari Opiskelija", "12345")
oskari.lisaa_suoritus(5)
oskari.lisaa_suoritus(5)
oskari.lisaa_suoritus(10)
print("Opintopisteet:", oskari.opintopisteet)
```

<sample-output>

Opintopisteet: 20

</sample-output>


Trots metoddefinitionen är det fortfarande möjligt att komma åt attributet `studie_poäng` direkt. Detta kunde resultera i ett felaktigt tillstånd där objektets integritet går förlorad:

```python
oskari = Opiskelija("Oskari Opiskelija", "12345")
oskari.opintopisteet = -100
print("Opintopisteet:", oskari.opintopisteet)
```

<sample-output>

Opintopisteet: -100

</sample-output>

## Inkapsling

Ett vanligt inslag i objektorienterade programmeringsspråk är att klasserna kan dölja sina attribut för eventuella kunder. Dolda attribut kallas vanligtvis privata. I Python uppnås denna sekretess genom att lägga till två understreck `__` i början av attributnamnet:

```python
class Pankkikortti:
    # Attribuutti numero on piilotettu, nimi on näkyvissä
    def __init__(self, numero: str, nimi: str):
        self.__numero = numero
        self.nimi = nimi
```

Ett privat attribut är inte direkt synligt för klienten. Försök att referera till det orsakar ett fel. I exemplet ovan är attributet namn lätt att komma åt och ändra:

```python
kortti = Pankkikortti("123456","Reijo Rahakas")
print(kortti.nimi)
kortti.nimi = "Reijo Rutiköyhä"
print(kortti.nimi)
```

<sample-output>

Reijo Rahakas
Reijo Rutiköyhä

</sample-output>

Ifall man provar få en utskrift av kortnumret så orsakar det däremot ett fel:

```python
kortti = Pankkikortti("123456","Reijo Rahakas")
print(kortti.__numero)
```

<sample-output>

AttributeError: 'Pankkikortti' object has no attribute '__numero'

</sample-output>

Att dölja attribut från klienter kallas inkapsling. Som namnet antyder är attributet "slutet inne i en kapsel". Klienten erbjuds sedan ett lämpligt gränssnitt (engelska: interface) för att komma åt och bearbeta den data som finns lagrad i objektet.

Låt oss lägga till ett annat inkapslat attribut: saldot på kreditkortet. Den här gången lägger vi också till offentligt synliga metoder som gör det möjligt för klienten att komma åt och ändra saldot:

```python
class Pankkikortti:
    def __init__(self, numero: str, nimi: str, saldo: float):
        self.__numero = numero
        self.nimi = nimi
        self.__saldo = saldo

    def lisaa_rahaa(self, maara: float):
        if maara > 0:
            self.__saldo += maara

    def kayta_rahaa(self, maara: float):
        if maara > 0 and maara <= self.__saldo:
            self.__saldo -= maara

    def hae_saldo(self):
        return self.__saldo
```

```python
kortti = Pankkikortti("123456", "Reijo Rahakas", 5000)
print(kortti.hae_saldo())
kortti.lisaa_rahaa(100)
print(kortti.hae_saldo())
kortti.kayta_rahaa(500)
print(kortti.hae_saldo())
# Tämä ei onnistu, koska saldo ei riitä
kortti.kayta_rahaa(10000)
print(kortti.hae_saldo())
```

<sample-output>

5000
5100
4600
4600

</sample-output>

Saldot kan inte ändras direkt eftersom attributet är privat, men vi har inkluderat metoderna `tillsatt_pengar` och `ta_ut_pengar` för att ändra värdet. Metoden `returnera_saldo` returnerar det värde som lagrats i saldo. Metoderna innehåller några rudimentära kontroller för att bibehålla objektets integritet: till exempel kan kortet inte överdras.

<programming-exercise name='Auto' tmcname='osa09-09_auto'>

Toteuta luokka `Auto`, jossa on _kapseloituina attribuutteina_ tieto bensatankin sisällöstä (0-60 litraa) sekä ajetuista kilometreista. Auto kuluttaa litran bensaa kilometrillä.

Luokalla on seuraavat metodit:

- `tankkaa()`, joka täyttää bensatankin
- `aja(km:int)`, joka ajaa parametrina olevan kilometrimäärän tai niin pitkälle kuin bensaa riittää
- `__str__`, joka näyttää esimerkin mukaisen kuvauksen autosta

Esimerkki luokan käyttämisestä:

```python
auto = Auto()
print(auto)
auto.tankkaa()
print(auto)
auto.aja(20)
print(auto)
auto.aja(50)
print(auto)
auto.aja(10)
print(auto)
auto.tankkaa()
auto.tankkaa()
print(auto)
```

<sample-output>

Auto: ajettu 0 km, bensaa 0 litraa
Auto: ajettu 0 km, bensaa 60 litraa
Auto: ajettu 20 km, bensaa 40 litraa
Auto: ajettu 60 km, bensaa 0 litraa
Auto: ajettu 60 km, bensaa 0 litraa
Auto: ajettu 60 km, bensaa 60 litraa

</sample-output>

**Huomaa**, että bensan ja ajettujen kilometrien määrä on kapseloitava, niihin ei tule pystyä vaikuttamaan muuten kuin auton metodeja kutsumalla.

</programming-exercise>

## En kort notis om privata attribut, Python och objektorienterad programmering

Det finns sätt att kringgå understryknings `__`-notationen för att dölja attribut, som du kan stöta på om du söker efter material online. Inget Python-attribut är verkligen privat, och det är avsiktligt från skaparna av Pythons. Å andra sidan förväntas en Python-programmerare i allmänhet respektera de riktlinjer för synlighet som anges i klasser, och det krävs en särskild ansträngning för att komma runt dessa. I andra objektorienterade programmeringsspråk, till exempel Java, är privata variabler ofta verkligen dolda, och det är bäst om du tänker på privata Python-variabler som sådana också.

## Getter och sättare

I objektorienterad programmering kallas metoder som är avsedda för att komma åt och ändra attribut vanligtvis för getter och sättare (eng: setters). Inte alla Python-programmerare använder termerna "getter" och "sättare", men konceptet med egenskaper som beskrivs nedan är mycket liknande, vilket är varför vi kommer att använda den allmänt accepterade objektorienterade programmeringsterminologin här.

Ovan skapade vi några offentliga metoder för att komma åt privata attribut, men det finns ett enklare, "pythoniskt" sätt att komma åt attribut. Låt oss ta en titt på en enkel klass som heter `Plånbok` med ett enda privat attribut `pengar`:

```python
class Lompakko:
    def __init__(self):
        self.__rahaa = 0
```

Vi kan tillägga getter och sättar metoder för att komma åt det privata attributet genom att använda `@property` dekoratorn:

```python
class Lompakko:
    def __init__(self):
        self.__rahaa = 0

    # Havainnointimetodi
    @property
    def rahaa(self):
        return self.__rahaa

    # Asetusmetodi
    @rahaa.setter
    def rahaa(self, rahaa):
        if rahaa >= 0:
            self.__rahaa = rahaa
```

Först definierar vi en getter-metod som returnerar den summa pengar som för närvarande finns i plånboken. Sedan definierar vi en sättar-metod som sätter ett nytt värde för money-attributet och samtidigt ser till att det nya värdet inte är negativt.

De nya metoderna kan användas på följande sätt:

```python
lompsa = Lompakko()
print(lompsa.rahaa)

lompsa.rahaa = 50
print(lompsa.rahaa)

lompsa.rahaa = -30
print(lompsa.rahaa)
```

<sample-output>

0
50
50

</sample-output>

För klienten är det ingen skillnad att använda dessa nya metoder jämfört med att direkt komma åt ett attribut. Parenteser är inte nödvändiga, utan det är helt acceptabelt att ange `plånbok.pengar = 50`, som om vi helt enkelt tilldelar ett värde till en variabel. Syftet var faktiskt att dölja (dvs. kapsla in) den interna implementeringen av attributet och samtidigt erbjuda ett enkelt sätt att komma åt och ändra den data som lagras i objektet.

I det föregående exemplet finns dock ett litet problem: klienten meddelas inte om att det inte går att ange ett negativt värde för attributet pengar. När ett värde som anges är uppenbart felaktigt är det vanligtvis en bra idé att skapa ett undantag och på så sätt informera klienten. I det här fallet bör undantaget förmodligen vara av typen `ValueError` för att visa att det angivna värdet var oacceptabelt.

Här har vi en förbättrad version av klassen, tillsammans med lite kod för att testa den:

```python
class Lompakko:
    def __init__(self):
        self.__rahaa = 0

    # Havainnointimetodi
    @property
    def rahaa(self):
        return self.__rahaa

    # Asetusmetodi
    @rahaa.setter
    def rahaa(self, rahaa):
        if rahaa >= 0:
            self.__rahaa = rahaa
        else:
            raise ValueError("Rahasumma ei saa olla negatiivinen")
```

```python
lompsa.rahaa = -30
print(lompsa.rahaa)
```

<sample-output>

ValueError: Rahasumma ei saa olla negatiivinen

</sample-output>

OBS: getter-metoden, dvs `@property-dekoratorn`, måste introduceras före sättar-metoden i koden, annars blir det fel när klassen exekveras. Detta beror på att `@property-dekoratorn` definierar namnet på det "attribut" som erbjuds till klienten. Sättar-metoden, som läggs till med `.setter`, lägger helt enkelt till en ny funktionalitet till den.

<programming-exercise name='Äänite' tmcname='osa09-10_aanite'>

Kirjoita luokka `Aanite`, joka mallintaa yksittäistä äänitettä. Luokalla on yksi piilotettu attribuutti, kokonaislukutyyppinen `__pituus`.

Kirjoita luokalle

* konstruktori, joka saa parametrikseen pituuden
* havainnointimetodi `pituus`, joka palauttaa pituuden
* asetusmetodi, joka asettaa pituuden arvon

Luokkaa siis käytetään seuraavasti:

```python
the_wall = Aanite(43)
print(the_wall.pituus)
the_wall.pituus = 44
print(the_wall.pituus)
```

<sample-output>

43
44

</sample-output>

Jos pituudeksi yritetään asettaa nollaa pienempää arvoa joko konstruktorissa tai asetusmetodissa, tulee tuottaa virhe `ValueError`.

Jos et muista miten poikkeus tuotetaan, kertaa
[osan 6](/osa-6/3-virheet#poikkeusten-tuottaminen) materiaalista.

</programming-exercise>

Följande exempel har en klass med två privata attribut, tillsammans med getter och sättare för båda. Prova programmet med olika värden som skickas som argument:

```python
class Pelaaja:
    def __init__(self, nimi: str, pelinumero: int):
        self.__nimi = nimi
        self.__pelinumero = pelinumero

    @property
    def nimi(self):
        return self.__nimi

    @nimi.setter
    def nimi(self, nimi: str):
        if nimi != "":
            self.__nimi = nimi
        else:
            raise ValueError("Nimi ei voi olla tyhjä")

    @property
    def pelinumero(self):
        return self.__pelinumero

    @pelinumero.setter
    def pelinumero(self, pelinumero: int):
        if pelinumero > 0:
            self.__pelinumero = pelinumero
        else:
            raise ValueError("Pelinumeron täytyy olla positiviinen kokonaisluku")
```

```python
pelaaja = Pelaaja("Pekka Palloilija", 10)
print(pelaaja.nimi)
print(pelaaja.pelinumero)

pelaaja.nimi = "Paula Palloilija"
pelaaja.pelinumero = 11
print(pelaaja.nimi)
print(pelaaja.pelinumero)
```

<sample-output>

Pekka Palloilija
10
Paula Palloilija
11

</sample-output>

Som avslutning på detta avsnitt ska vi titta på en klass som modellerar en enkel dagbok. Alla attribut är privata, men de hanteras genom olika gränssnitt: dagbokens ägare har getter- och sättar-metoder, men dagboksposterna behandlas med "traditionella" metoder. I det här fallet är det vettigt att neka klienten all tillgång till dagbokens interna datastruktur. Endast de offentliga metoderna är direkt synliga för klienten.

Inkapsling säkerställer också att den interna implementeringen av klassen kan ändras när som helst, förutsatt att det offentliga gränssnittet förblir intakt. Klienten behöver inte veta eller bry sig om huruvida den interna datastrukturen är baserad på listor, ordlistor eller något helt annat. 

```python
class Paivakirja:
    def __init__(self, omistaja: str):
        self.__omistaja = omistaja
        self.__merkinnat = []

    @property
    def omistaja(self):
        return self.__omistaja

    @omistaja.setter
    def omistaja(self, omistaja):
        if omistaja != "":
            self.__omistaja = omistaja
        else:
            raise ValueError("Omistaja ei voi olla tyhjä")

    def lisaa_merkinta(self, merkinta: str):
        self.__merkinnat.append(merkinta)

    def tulosta(self):
        print("Yhteensä", len(self.__merkinnat), "merkintää")
        for merkinta in self.__merkinnat:
            print("- " + merkinta)
```

```python
paivakirja = Paivakirja("Pekka")
paivakirja.lisaa_merkinta("Tänään söin puuroa")
paivakirja.lisaa_merkinta("Tänään opettelin olio-ohjelmointia")
paivakirja.lisaa_merkinta("Tänään menin ajoissa nukkumaan")
paivakirja.tulosta()
```

<sample-output>

Yhteensä 3 merkintää
- Tänään söin puuroa
- Tänään opettelin olio-ohjelmointia
- Tänään menin ajoissa nukkumaan

</sample-output>

<programming-exercise name='Säähavaintoasema' tmcname='osa09-11_havaintoasema'>

Kirjoita luokka `Havaintoasema`, johon voidaan tallentaa säähavaintoja. Luokalla on seuraavat julkiset piirteet:

* konstruktori, joka saa parametriksen aseman nimen
* metodi `lisaa_havainto(havainto: str)`, joka lisää havainnon listan peräään
* metodi `viimeisin_havainto()`, joka palauttaa viimeksi lisätyn havainnon. Jos havaintoja ei ole tehty, metodi palauttaa _tyhjän merkkijonon_.
* metodi `havaintojen_maara()`, joka palauttaa havaintojen yhteismäärän
* metodi `__str__`, joka palauttaa aseman nimen ja havaintojen yhteismäärän alla olevan esimerkin mukaisessa muodossa.

Luokan kaikkien attribuuttien pitää olla asiakkaalta piilossa. Saat itse päättää luokan sisäisen toteutuksen.

Esimerkki luokan käytöstä:

```python
asema = Havaintoasema("Kumpula")
asema.lisaa_havainto("Sadetta 10mm")
asema.lisaa_havainto("Aurinkoista")
print(asema.viimeisin_havainto())

asema.lisaa_havainto("Ukkosta")
print(asema.viimeisin_havainto())

print(asema.havaintojen_maara())
print(asema)
```

<sample-output>

Aurinkoista
Ukkosta
3
Kumpula, 3 havaintoa

</sample-output>

</programming-exercise>
