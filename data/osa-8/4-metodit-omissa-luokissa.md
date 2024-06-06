---
path: '/osa-8/4-metodit-omissa-luokissa'
title: 'Metoder i egna klasser'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen:

- Vet du hur klassmetoder fungerar
- Kan du skriva nya metoder i dina egna klasser
- Kommer du att förstå begreppen inkapsling och klient inom objektorienterad programmering

</text-box>

Klasser som endast innehåller dataattribut skiljer sig inte så mycket från ordlistor. Nedan kan du se två sätt att modellera ett bankkonto, först med en klassdefinition och sedan med hjälp av en ordlista.

```python
# Esimerkki omaa luokkaa käyttäen
class Pankkitili:

    def __init__(self, tilinumero: str, omistaja: str, saldo: float, vuosikorko: float):
        self.tilinumero = tilinumero
        self.omistaja = omistaja
        self.saldo = saldo
        self.vuosikorko = vuosikorko

pekan_tili = Pankkitili("12345-678", "Pekka Python", 1500.0, 0.015)
```

```python
# Esimerkki sanakirjaa käyttäen
pekan_tili = {"tilinumero": "12345-678", "omistaja": "Pekka Python", "saldo": 1500.0, "vuosikorko": 0.0}
```

Med en ordlista är implementeringen mycket kortare och enklare. Med en klass är strukturen däremot mer "hårt bunden", så vi kan förvänta oss att alla `Bankkonto`-objekt är strukturellt lika. Dessutom är en klass också namngiven. Klassen `Bankkonto` refereras till när ett nytt bankkonto skapas, och objektets typ är `Bankkonto`, inte dict.

En annan stor fördel med klasser är att de förutom data även kan innehålla funktionalitet. En av de vägledande principerna för objektorienterad programmering är att ett objekt används för att komma åt både den data som är kopplad till ett objekt och funktionaliteten för att bearbeta denna data.

## Metoder i klasser

En metod är ett underprogram eller en funktion som är knuten till en specifik klass. Vanligtvis påverkar en metod bara ett enda objekt. En metod definieras inom klassdefinitionen och den kan komma åt klassens dataattribut precis som vilken annan variabel som helst.

Låt oss fortsätta med klassen `Bankkonto` som introducerades ovan. Nedan har vi en ny metod som lägger till ränta på kontot:

```python
class Pankkitili:

    def __init__(self, tilinumero: str, omistaja: str, saldo: float, vuosikorko: float):
        self.tilinumero = tilinumero
        self.omistaja = omistaja
        self.saldo = saldo
        self.vuosikorko = vuosikorko

    # Metodi lisää koron tilin saldoon
    def lisaa_korko(self):
        self.saldo += self.saldo * self.vuosikorko


pekan_tili = Pankkitili("12345-678", "Pekka Python", 1500.0, 0.015)
pekan_tili.lisaa_korko()
print(pekan_tili.saldo)
```

<sample-output>

1522.5

</sample-output>

Metoden `tillsätt_ränta` multiplicerar saldot på kontot med den årliga ränteprocenten och lägger sedan till resultatet till det aktuella saldot. Metoden verkar bara på det objekt som den anropas på.

Låt oss se hur detta fungerar när vi har skapat flera instanser av klassen:

```python
# Luokka Pankkitili on määritelty edellisessä esimerkissä

pekan_tili = Pankkitili("12345-678", "Pekka Python", 1500.0, 0.015)
pirjon_tili = Pankkitili("99999-999", "Pirjo Pythonen", 1500.0, 0.05)
paulin_tili = Pankkitili("1111-222", "Pauli Paulinen", 1500.0, 0.001)

# Lisätään korko Pekalle ja Pirjolle, mutta ei Paulille
pekan_tili.lisaa_korko()
pirjon_tili.lisaa_korko()

# Tulostetaan kaikki
print(pekan_tili.saldo)
print(pirjon_tili.saldo)
print(paulin_tili.saldo)
```

<sample-output>

1522.5
1575.0
1500.0

</sample-output>

Som du kan se ovan läggs den årliga räntan endast till på de konton som metoden anropas på. Eftersom den årliga räntan är olika för Peters och Paulas konton, blir resultatet olika för dessa två konton. Saldot på Pippas konto ändras inte, eftersom metoden `tillsätt_ränta` inte anropas på objektet `pippas_konto`.

## Inkapsling

Inom objektorienterad programmering dyker ordet klient upp då och då. Det används för att hänvisa till ett kodavsnitt som skapar ett objekt och använder den tjänst som tillges av dess metoder. När data som finns i ett objekt endast används genom de metoder som det tillges, garanteras objektets interna integritet. I praktiken innebär detta att t.ex. en `Bankkonto`-klass erbjuder metoder för att hantera `saldo`-attributet, så att saldot aldrig nås direkt av klienten. Dessa metoder kan sedan verifiera att saldot till exempel inte tillåts gå under noll.

Ett exempel på hur detta skulle fungera:

```python
class Pankkitili:

    def __init__(self, tilinumero: str, omistaja: str, saldo: float, vuosikorko: float):
        self.tilinumero = tilinumero
        self.omistaja = omistaja
        self.saldo = saldo
        self.vuosikorko = vuosikorko

    # Metodi lisää koron tilin saldoon
    def lisaa_korko(self):
        self.saldo += self.saldo * self.vuosikorko

    # Metodilla "nostetaan" tililtä rahaa
    # Metodi palauttaa true, jos nosto onnistuu, muuten False
    def nosto(self, nostosumma: float):
        if nostosumma <= self.saldo:
            self.saldo -= nostosumma
            return True

        return False

pekan_tili = Pankkitili("12345-678", "Pekka Python", 1500.0, 0.015)

if pekan_tili.nosto(1000):
    print("Nosto onnistui, tilin saldo on nyt", pekan_tili.saldo)
else:
    print("Nosto ei onnistunut, rahaa ei ole tarpeeksi.")

# Yritetään uudestaan
if pekan_tili.nosto(1000):
    print("Nosto onnistui, tilin saldo on nyt", pekan_tili.saldo)
else:
    print("Nosto ei onnistunut, rahaa ei ole tarpeeksi.")
```

<sample-output>

Nosto onnistui, tilin saldo on nyt 500.0
Nosto ei onnistunut, rahaa ei ole tarpeeksi.

</sample-output>

Att bibehålla objektets interna integritet och erbjuda lämpliga metoder för att säkerställa detta kallas inkapsling. Tanken är att objektets inre arbete är dolt för klienten, men objektet erbjuder metoder som kan användas för att komma åt den data som lagras i objektet.

Att lägga till en metod innebär inte att attributet automatiskt döljs. Även om klassdefinitionen `Bankkonto` innehåller metoden `uttag` för att ta ut pengar, kan klientkoden fortfarande komma åt och ändra attributet `saldo` direkt:

```python
pekan_tili = Pankkitili("12345-678", "Pekka Python", 1500.0, 0.015)

# Yritetään nostaa 2000
if pekan_tili.nosto(2000):
    print("Nosto onnistui, tilin saldo on nyt", pekan_tili.saldo)
else:
    print("Nosto ei onnistunut, rahaa ei ole tarpeeksi.")

    # Nostetaan "väkisin" 2000
    pekan_tili.saldo -= 2000

print("Saldo nyt:", pekan_tili.saldo)
```

Det är möjligt att dölja dataattributen från klientkoden, vilket kan bidra till att lösa detta problem. Vi återkommer till detta ämne i nästa del.

<programming-exercise name='Vähenevä laskuri' tmcname='osa08-10_vaheneva_laskuri'>

Tässä tehtävässä on useampi osa. Jokainen osa vastaa yhtä tehtäväpistettä.

Tehtäväpohjan mukana tulee osittain valmiiksi toteutettu luokka `VahenevaLaskuri`:

```python
class VahenevaLaskuri:
    def __init__(self, arvo_alussa: int):
        self.arvo = arvo_alussa

    def tulosta_arvo(self):
        print("arvo:", self.arvo)

    def vahenna(self):
        pass

    # ja tänne muut metodit
```

Luokkaa käytetään seuraavasti

```python
laskuri = VahenevaLaskuri(10)
laskuri.tulosta_arvo()
laskuri.vahenna()
laskuri.tulosta_arvo()
laskuri.vahenna()
laskuri.tulosta_arvo()
```

<sample-output>

arvo: 10
arvo: 9
arvo: 8

</sample-output>


### Laskurin vähentäminen

Täydennä luokan runkoon metodin `vahenna` toteutus sellaiseksi, että se vähentää kutsuttavan olion oliomuuttujan arvoa yhdellä. Kun olet toteuttanut metodin `vahenna`, äskeisen pääohjelman tulee toimia esimerkkitulosteen mukaan.

### Laskurin arvo ei saa olla negatiivinen

Täydennä metodin `vahenna` toteutus sellaiseksi, ettei laskurin arvo mene koskaan negatiiviseksi: jos laskurin arvo on jo 0, sitä ei enää vähennetä.

```python
laskuri = VahenevaLaskuri(2)
laskuri.tulosta_arvo()
laskuri.vahenna()
laskuri.tulosta_arvo()
laskuri.vahenna()
laskuri.tulosta_arvo()
laskuri.vahenna()
laskuri.tulosta_arvo()
```

<sample-output>

arvo: 2
arvo: 1
arvo: 0
arvo: 0

</sample-output>

### Laskurin arvon nollaus

Tee laskurille metodi `nollaa`, joka nollaa laskurin arvon:

```python
laskuri = VahenevaLaskuri(100)
laskuri.tulosta_arvo()
laskuri.nollaa()
laskuri.tulosta_arvo()
```

<sample-output>

arvo: 100
arvo: 0

</sample-output>

### Alkuperäisen arvon palautus

Tee laskurille metodi `palauta_alkuperainen_arvo()` joka palauttaa laskurille sen alkuperäisen arvon:

```python
laskuri = VahenevaLaskuri(55)
laskuri.vahenna()
laskuri.vahenna()
laskuri.vahenna()
laskuri.vahenna()
laskuri.tulosta_arvo()
laskuri.palauta_alkuperainen_arvo()
laskuri.tulosta_arvo()
```

<sample-output>

arvo: 51
arvo: 55

</sample-output>

</programming-exercise>

Som avslutning på detta avsnitt tittar vi på en klass som modellerar en spelares personliga bästa. Klassdefinitionen innehåller separata valideringsmetoder som kontrollerar att de argument som skickas är giltiga. Metoderna anropas redan i konstruktorn. Detta säkerställer att det skapade objektet är sunt internt.

```python
from datetime import date

class Ennatystulos:

    def __init__(self, pelaaja: str, paiva: int, kuukausi: int, vuosi: int, pisteet: int):
        # Oletusarvot
        self.pelaaja = ""
        self.paivamaara = date(1900, 1, 1)
        self.pisteet = 0

        if self.nimi_ok(pelaaja):
            self.pelaaja = pelaaja

        if self.pvm_ok(paiva, kuukausi, vuosi):
            self.paivamaara = date(vuosi, kuukausi, paiva)

        if self.pisteet_ok(pisteet):
            self.pisteet = pisteet

    # Apumetodit, joilla tarkistetaan ovatko syötteet ok
    def nimi_ok(self, nimi: str):
        return len(nimi) >= 2 # Nimessä vähintään kaksi merkkiä

    def pvm_ok(self, paiva, kuukausi, vuosi):
        try:
            date(vuosi, kuukausi, paiva)
            return True
        except:
            # Poikkeus, jos yritetään muodostaa epäkelpo päivämäärä
            return False

    def pisteet_ok(self, pisteet):
        return pisteet >= 0

if __name__ == "__main__":
    tulos1 = Ennatystulos("Pekka", 1, 11, 2020, 235)
    print(tulos1.pisteet)
    print(tulos1.pelaaja)
    print(tulos1.paivamaara)

    # Epäkelpo arvo päivämäärälle
    tulos2 = Ennatystulos("Piia", 4, 13, 2019, 4555)
    print(tulos2.pisteet)
    print(tulos2.pelaaja)
    print(tulos2.paivamaara) # Tulostaa oletusarvon 1900-01-01
```

<sample-output>

235
Pekka
2020-11-01
4555
Piia
1900-01-01

</sample-output>

I exemplet ovan anropades även hjälpmetoderna via parameternamnet `self` när de användes i konstruktorn. Det är också möjligt att inkludera /statiska/ metoddefinitioner i klassdefinitioner. Dessa är metoder som kan anropas utan att det någonsin skapas en instans av klassen. Vi återkommer till detta i nästa del.

Parameternamnet `self` används endast när man hänvisar till /objektets egenskaper som en instans av klassen/. Det gäller både dataattributen och de metoder som är knutna till ett objekt. För att göra terminologin mer förvirrande kallas dataattributen och metoderna tillsammans ibland helt enkelt för objektets attribut, vilket är anledningen till att vi i detta material ofta har angett dataattribut när vi menar de variabler som definieras inom klassen. Det är här terminologin hos vissa Python-programmerare skiljer sig något från den terminologi som mer allmänt används inom objektorienterad programmering, där attribut vanligtvis bara hänvisar till dataattributen hos ett objekt.

Det är också möjligt att skapa lokala variabler inom metoddefinitioner utan att hänvisa till `self`. Detta bör du göra om det inte finns något behov av att komma åt variablerna utanför metoden. Lokala variabler inom metoder har inga speciella nyckelord; de används precis som alla vanliga variabler som du har stött på hittills. .

Så här skulle det till exempel fungera: 

```python
class Bonuskortti:
    def __init__(self, nimi: str, saldo: float):
        self.nimi = nimi
        self.saldo = saldo

    def lisaa_bonus(self):
        # Nyt muuttuja bonus on paikallinen muuttuja,
        # eikä olion attribuutti - siihen siis ei voi
        # viitata olion kautta
        bonus = self.saldo * 0.25
        self.saldo += bonus

    def lisaa_superbonus(self):
        # Myös muuttuja superbonus on paikallinen muuttuja
        # Yleensä apumuuttujina käytetään paikallisia
        # muuttujia, koska niihin ei ole tarvetta
        # viitatata muissa metodeissa tai olion kautta
        superbonus = self.saldo * 0.5
        self.saldo += superbonus

    def __str__(self):
        return f"Bonuskortti(nimi={self.nimi}, saldo={self.saldo})"
```

<programming-exercise name="Etu- ja sukunimi" tmcname='osa08-10b_etu_ja_sukunimi'>

Kirjoita luokka `Henkilo`, jolla on _ainoastaan yksi attribuutti_ `nimi`, joka asetetaan konstruktorissa.

Lisäksi luokalle tule kirjoitaa kaksi metodia:

Metodi `anna_etunimi` palauttaa henkilön etunimen ja metodi `anna_sukunimi` vastaavasti henkilön sukunimen.

Voit olettaa metodeissa, että konstruktroissa annetussa nimessä on etu- ja sukunimi välilyönnillä erotettuna eikä muita nimiä.

Esimerkki luokan käytöstä:

```python
if __name__ == "__main__":
    pekka = Henkilo("Pekka Python")
    print(pekka.anna_etunimi())
    print(pekka.anna_sukunimi())

    pauli = Henkilo("Pauli Pythonen")
    print(pauli.anna_etunimi())
    print(pauli.anna_sukunimi())
```

<sample-output>

Pekka
Python
Pauli
Pythonen

</sample-output>


</programming-exercise>

<programming-exercise name='Lukutilasto' tmcname='osa08-11_lukutilasto'>

Tässä tehtävässä toteutetaan olio-ohjelmointia hyödyntäen samantapainen käyttäjän syöttämiä lukuja käsittelevä ohjelma kuin Ohjelmoinnin perusteiden [osan 2 lopussa](/osa-2/4-yksinkertainen-silmukka#programming-exercise-lukujen-kasittelya).

### Lukujen määrä

Tee luokka `Lukutilasto`, joka tuntee seuraavat toiminnot:

- metodi `lisaa_luku` lisää uuden luvun tilastoon
- metodi `lukujen_maara` kertoo lisättyjen lukujen määrän

Luokan ei tarvitse tallentaa mihinkään lisättyjä lukuja vaan riittää, että se muistaa niiden määrän. Metodin `lisaa_luku` ei tässä vaiheessa tarvitse edes ottaa huomioon, mikä luku lisätään tilastoon, koska ainoa tallennettava asia on lukujen määrä.

Luokan runko on seuraava:

```python
class  Lukutilasto:
    def __init__(self):
        self.lukuja = 0

    def lisaa_luku(self, luku:int):
        pass

    def lukujen_maara(self):
        pass
```

```python
tilasto = Lukutilasto()
tilasto.lisaa_luku(3)
tilasto.lisaa_luku(5)
tilasto.lisaa_luku(1)
tilasto.lisaa_luku(2)
print("Lukujen määrä:", tilasto.lukujen_maara())
```

<sample-output>

Lukujen määrä: 4

</sample-output>

### Summa ja keskiarvo

Laajenna luokkaa seuraavilla toiminnoilla:

- metodi `summa` kertoo lisättyjen lukujen summan (tyhjän lukutilaston summa on 0)
- metodi `keskiarvo` kertoo lisättyjen lukujen keskiarvon (tyhjän lukutilaston keskiarvo on 0)

```python
tilasto = Lukutilasto()
tilasto.lisaa_luku(3)
tilasto.lisaa_luku(5)
tilasto.lisaa_luku(1)
tilasto.lisaa_luku(2)
print("Lukujen määrä:", tilasto.lukujen_maara())
print("Summa:", tilasto.summa())
print("Keskiarvo:", tilasto.keskiarvo())
```

<sample-output>

Määrä: 4
Summa: 11
Keskiarvo: 2.75

</sample-output>

### Summa käyttäjältä

Tee ohjelma, joka kysyy lukuja käyttäjältä, kunnes käyttäjä antaa luvun -1. Sitten ohjelma ilmoittaa lukujen summan.

Ohjelmassa tulee käyttää `Lukutilasto`-oliota summan laskemiseen.

HUOM: Älä muuta tässä osassa luokkaa `Lukutilasto`, vaan toteuta sitä hyödyntäen summan laskemiseen käytetty ohjelma.

HUOM2: Älä kirjoita pääohjelmaa `if __name__ == "__main__"`-lohkon sisään, jotta testit toimivat!

<sample-output>

Anna lukuja:
**4**
**2**
**5**
**2**
**-1**
Summa: 13
Keskiarvo: 3.25

</sample-output>

### Monta summaa

Muuta edellistä ohjelmaa niin, että ohjelma laskee myös parillisten ja parittomien lukujen summaa.

HUOM: Älä edelleenkään muuta luokkaa `Lukutilasto`, vaan määrittele ohjelmassa kolme `Lukutilasto`-oliota. Laske ensimmäisen avulla kaikkien lukujen summa ja keskiarvo, toisen avulla parillisten lukujen summa ja kolmannen avulla parittomien lukujen summa.

HUOM2: Älä kirjoita pääohjelmaa `if __name__ == "__main__"`-lohkon sisään, jotta testit toimivat!

Ohjelman tulee toimia seuraavasti:

<sample-output>

Anna lukuja:
**4**
**2**
**5**
**2**
**-1**
Summa: 13
Keskiarvo: 3.25
Parillisten summa: 8
Parittomien summa: 5

</sample-output>



</programming-exercise>
