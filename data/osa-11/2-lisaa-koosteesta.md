---
path: '/osa-11/2-lisaa-koosteesta'
title: 'Fler comprehensions'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Kommer du att kunna använda comprehensions med strängar
- Vet du hur du använder comprehensions med dina egna klasser
- Kommer du att kunna skapa ordlistscomprehensions

</text-box>


Listor är kanske det vanligaste målet för comprehensions, men comprehensions fungerar på alla serier av föremål, inklusive strängar. Liksom listexemplen i föregående avsnitt, ifall en list comprehension utförs på en sträng, plockas föremålen (dvs. tecknen) i strängen en efter en, bearbetas enligt det givna uttrycket och lagras i en lista.

```python

nimi = "Pekka Python"

isot_kirjaimet = [merkki.upper() for merkki in nimi]
print(isot_kirjaimet)

```

<sample-output>

['P', 'E', 'K', 'K', 'A', ' ', 'P', 'Y', 'T', 'H', 'O', 'N']

</sample-output>

Resultatet är en lista, vilket dikteras av parentesnotationen runt comprehension-satsen. Om vi ville ha en sträng istället skulle vi kunna använda strängmetoden `join`  för att tolka listan till en sträng. Kom ihåg att metoden anropas på den sträng som vi vill använda som "lim" mellan tecknen. Låt oss ta en titt på några exempel:

```python

nimi = "Pekka"
lista = list(nimi)
print(lista)

print("".join(lista))
print(" ".join(lista))
print(",".join(lista))
print(" ja ".join(lista))

```

<sample-output>

['P', 'e', 'k', 'k', 'a']
Pekka
P e k k a
P,e,k,k,a
P ja e ja k ja k ja a

</sample-output>

List comprehensions och `join`-metoden gör det enkelt att skapa nya strängar baserade på andra strängar. Vi kan t.ex. skapa en sträng som bara innehåller vokalerna från en annan sträng:

```python

testijono = "Heippa vaan kaikki, tämä on testi"

vokaalit = [merkki for merkki in testijono if merkki in "aeiouyåäö"]
uusijono = "".join(vokaalit)

print(uusijono)

```

<sample-output>

eiaaaaiiääoei

</sample-output>

I exemplet ovan står list comprehension och `join`-metoden på separata rader, men de kan kombineras till ett enda uttryck:

```python

testijono = "Heippa vaan kaikki, tämä on testi"

vokaalijono = "".join([merkki for merkki in testijono if merkki in "aeiouyåäö"])

print(vokaalijono)

```

Många Python-programmerare står trogna vid dessa oneliners, så det är väl värt besväret att lära sig läsa dem. Vi kan till och med lägga till `split`-metoden i mixen, så att vi kan bearbeta hela meningar effektivt med ett enda uttalande. I exemplet nedan tas det första tecknet från varje ord i en mening bort:

```python

lause = "Vesihiisi se kuulkaa vaan sihisi hississä"

lause_ilman_alkuja = " ".join([sana[1:] for sana in lause.split()])
print(lause_ilman_alkuja)

```

<sample-output>

esihiisi e uulkaa aan ihisi ississä

</sample-output>

Låt oss gå igenom detta steg för steg:

- `ord[1:]` extraherar en delsträng från det andra tecknet (vid index 1) och framåt
- `mening.split()` delar upp meningen i avsnitt vid det angivna tecknet. I det här fallet ges inget argument till metoden, så meningen delas upp vid mellanslagstecken som standard
- `" ".join()` kombinerar föremålen i listan till en ny sträng med ett mellanslag mellan föremålen

En mer traditionell iterativ metod skulle kunna se ut så här:

```python

lause = "Vesihiisi se kuulkaa vaan sihisi hississä"

sanalista = []
sanat = lause.split()
for sana in sanat:
    sana_ilman_alkua = sana[1:]
    sanalista.append(sana_ilman_alkua)

lause_ilman_alkuja = " ".join(sanalista)


print(lause_ilman_alkuja)

```

<programming-exercise name='Suodata kielletyt' tmcname='osa11-08_suodata_kielletyt'>

Tee funktio `suodata_kielletyt(merkkijono: str, kielletyt: str)` joka palauttaa sen parametrina olevasta merkkijonosta version, joka ei sisällä yhtään merkkiä sen toisena parametrina olevasta "kiellettyjen merkkien" merkkijonosta.

Funktion tulee käyttää listakoostetta. Funktio saa sisältää `def`-rivi mukaanlukien maksimissaan 3 riviä.

Esimerkki funktion käytöstä

```python
lause = "Suo! kuokka, ja python: hieno yhdistelmä!??!?!"
suodatettu = suodata_kielletyt(lause, "!?:,.")
print(suodatettu)
```

<sample-output>

Suo kuokka ja python hieno yhdistelmä

</sample-output>

</programming-exercise>

## Egna klasser och comprehensions

Comprehensions kan vara ett användbart verktyg för att bearbeta eller formulera instanser av dina egna klasser, vilket vi kommer att se i följande exempel.

Låt oss först ta en titt på klassen `Land` som är en enkel modell för ett enda land, med attribut för namn och befolkning. I huvudfunktionen nedan skapar vi först några Land-objekt och använder sedan en list comprehension för att bara välja dem vars befolkning är större än fem miljoner.

```python

class Maa:
    """ Luokka mallintaa yhtä maata asukaslukuineen """
    def __init__(self, nimi: str, asukasluku: int):
        self.nimi = nimi
        self.asukasluku = asukasluku

if __name__ == "__main__":
    suomi = Maa("Suomi", 6000000)
    malta = Maa("Malta", 500000)
    ruotsi = Maa("Ruotsi", 10000000)
    islanti = Maa("Islanti", 350000)

    maat = [suomi, malta, ruotsi, islanti]

    isommat_maat = [maa.nimi for maa in maat if maa.asukasluku > 5000000]
    for maa in isommat_maat:
        print(maa)


```

<sample-output>

Suomi
Ruotsi

</sample-output>

I list comprehension ovan valde vi bara namnattributet från Land-objekten, så innehållet i listan kunde skrivas ut direkt. Vi skulle också kunna skapa en ny lista med länderna och komma åt namnattributet i `for`-loopen. Detta skulle vara användbart om samma lista med länder skulle användas senare i programmet, eller om vi behövde befolkningsattributet i `for`-loopen också:

```python

if __name__ == "__main__":
    suomi = Maa("Suomi", 6000000)
    malta = Maa("Malta", 500000)
    ruotsi = Maa("Ruotsi", 10000000)
    islanti = Maa("Islanti", 350000)

    maat = [suomi, malta, ruotsi, islanti]

    isommat_maat = [maa for maa in maat if maa.asukasluku > 5000000]
    for maa in isommat_maat:
        print(maa.nimi)
```

I nästa exempel har vi en klass som heter `Springning` som modellerar ett enskilt lopp med attribut för loppets längd och namn. Vi kommer att använda list comprehension för att skapa `Springning`-objekt baserat på en lista med tävlingslängder.

Parametern `namn` har ett standardvärde i konstruktorn för `Springning`-klassen, vilket är varför vi inte behöver skicka namnet som ett argument.

```python

class Juoksumatka:
    """ Luokka mallintaa yhtä n metrin pituista juoksumatkaa """
    def __init__(self, matka:int, nimi:str = "ei nimeä"):
        self.matka = matka
        self.nimi = nimi

    def __repr__(self):
        return f"{self.matka} m. ({self.nimi})"

if __name__ == "__main__":
    pituudet = [100, 200, 1500, 3000, 42195]
    matkat = [Juoksumatka(pituus) for pituus in pituudet]

    # tulostetaan kaikki
    print(matkat)

    # Poimitaan yksi listasta ja nimetään se
    maraton = matkat[-1] # viimeisenä listassa
    maraton.nimi = "Maraton"

    # Tulostetaan vielä uudella nimellä
    print(matkat)

```

<sample-output>

[100 m. (ei nimeä), 200 m. (ei nimeä), 1500 m. (ei nimeä), 3000 m. (ei nimeä), 42195 m. (ei nimeä)]
[100 m. (ei nimeä), 200 m. (ei nimeä), 1500 m. (ei nimeä), 3000 m. (ei nimeä), 42195 m. (Maraton)]

</sample-output>

Låt oss nu ta reda på vad som gör en serie objekt "begripliga" (“comprehendible”). I föregående del lärde vi oss hur vi kan göra våra egna klasser itererbara. Det är exakt samma funktion som också möjliggör list comprehension. Om din egen klass är itererbar kan den användas som grund för en list comprehension. Följande klassdefinitioner är kopierade direkt från [del 10](https://programming-24.mooc.fi/part-10/3-oo-programming-techniques#iterators):

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

# Testataan
if __name__ == "__main__":
    k1 = Kirja("Elämäni Pythoniassa", "Pekka Python", 123)
    k2 = Kirja("Vanhus ja Java", "Ernest Hemingjava", 204)
    k3 = Kirja("C-itsemän veljestä", "Keijo Koodari", 997)

    hylly = Kirjahylly()
    hylly.lisaa_kirja(k1)
    hylly.lisaa_kirja(k2)
    hylly.lisaa_kirja(k3)

    # Luodaan lista, jossa kaikkien kirjojen nimet
    kirjojen_nimet = [kirja.nimi for kirja in hylly]
    print(kirjojen_nimet)

```

<programming-exercise name='Kauppalistan tuotteet' tmcname='osa11-09_kauppalistan_tuotteet'>

Osan 10 tehtävässä teimme [Kauppalista-luokasta iteroitavan](/osa-10/3-olio-ohjelmoinnin-tekniikoita#programming-exercise-iteroitava-kauppalista). Iteroitavan luokan oliota voidaan käyttää listakoosteiden yhteydessä. Tehtäväpohjassa on mukana luokasta typistetty versio, jonka toiminnallisuus riittää tähän tehtävään.

Tee nyt funktio `kauppalistan_tuotteet(kauppalista, maara: int)` joka saa parametriksi kauppalista-olion. Funktio palauttaa kauppalistan ostoksista niiden tuotteiden nimet, joita on listalla vähintään parametrin `maara` verran.

Funktio tulee toteuttaa listakoosteen avulla, ja sen pituus saa olla `def`-määrittelyriveineen yhteensä korkeintaan kaksi riviä. Luokan Kauppalista koodia ei saa muuttaa!

Funktio toimii seuraavasti

```python
lista = Kauppalista()
lista.lisaa("banaanit", 10)
lista.lisaa("omenat", 5)
lista.lisaa("alkoholiton olut", 24)
lista.lisaa("ananas", 1)

print("kauppalistalla vähintään 8 seuraavia tuotteita:")
for tuote in kauppalistan_tuotteet(lista, 8):
    print(tuote)
```

<sample-output>

kauppalistalla vähintään 8 seuraavia tuotteita:
banaanit
alkoholiton olut

</sample-output>

</programming-exercise>

<programming-exercise name='Halvempien hintaero' tmcname='osa11-10_halvempien_hintaero'>

Osan 9 tehtävässä teimme luokan [Asunto](/osa-9/1-oliot-ja-viittaukset#programming-exercise-asuntovertailu). Tässä tehtävässä on käytössä hieman laajennettu versio luokasta.

Tee funktio `halvemmat(asunnot: list, verrattava: Asunto)`, joka saa parametriksi listan asuntoja sekä yksittäisen vertailtavan asunnon. Funktio palauttaa listan, jolla on asunnoista ne, jotka ovat hinnaltaan halvempia kuin vertailtava asunto, sekä näiden hintaeron. Palautettavan listan alkiot ovat tupleja, joiden ensimmäinen jäsen on asunto ja toisena sen hintaero vertailtavaan.

Funktio tulee toteuttaa listakoosteen avulla. Funktion maksimipituus `def`-määrittelyrivi mukaanluettuna on 2 riviä.

Luokan `Asunto` koodia ei saa muuttaa!

Funktio toimii seuraavasti

```python
a1 = Asunto(1, 16, 5500, "Eira yksiö")
a2 = Asunto(2, 38, 4200, "Kallio kaksio")
a3 = Asunto(3, 78, 2500, "Jakomäki kolmio")
a4 = Asunto(6, 215, 500, "Suomussalmi omakotitalo")
a5 = Asunto(4, 105, 1700, "Kerava 4h ja keittiö")
a6 = Asunto(25, 1200, 2500, "Haikon kartano")

asunnot = [a1, a2, a3, a4, a5, a6]

print(f"asuntoa {a3.kuvaus} halvemmat vaihtoehdot:")
for alkio in halvemmat(asunnot, a3):
    print(f"{alkio[0].kuvaus:30} hintaero {alkio[1]} euroa")
```

<sample-output>

asuntoa Jakomäki kolmio halvemmat vaihtoehdot:
Eira yksiö                     hintaero 107000 euroa
Kallio kaksio                  hintaero 35400 euroa
Suomussalmi omakotitalo        hintaero 87500 euroa
Kerava 4h ja keittiö           hintaero 16500 euroa

</sample-output>

</programming-exercise>

## Comprehensions och ordlistor

Det finns inget i sig "list-aktigt" med comprehensions. Resultatet är en lista eftersom comprehension-satsen är inkapslad i hakparenteser, som indikerar en Python-lista. Förståelser fungerar lika bra med Python-ordlistor om du använder rundparenteser istället. Kom dock ihåg att ordlistor kräver nyckel-värde-par. Båda måste anges när en ordlista skapas, även när det gäller comprehensions.

Grunden för en comprehension kan vara vilken itererbar serie som helst, vare sig det är en lista, en sträng, en tupel, en ordlista, någon av dina egna itererbara klasser och så vidare.

I följande exempel använder vi en sträng som bas för en ordlista. Ordlistan innehåller alla unika tecken i strängen, tillsammans med antalet gånger de förekommer:

```python

lause = "Hei kaikki"

merkkimäärät = {kirjain : lause.count(kirjain) for kirjain in lause}
print(merkkimäärät)

```

<sample-output>

{'H': 1, 'e': 1, 'i': 3, ' ': 1, 'k': 3, 'a': 1}

</sample-output>

Principen för comprehension-satsen är exakt densamma som för listor, men i stället för ett enda värde består uttrycket nu av en nyckel och ett värde. Den allmänna syntaxen ser ut så här:

`{<nyckeluttryck> : <värdeuttryck> för <föremål> i <serie>}`

Som avslutning på det här avsnittet tittar vi på faktorialtal igen. Den här gången lagrar vi resultaten i en ordlista. Själva talet är nyckeln, medan värdet är resultatet av faktorn från vår funktion: 

```python

def kertoma(n: int):
    """ Funktio laskee positiivisen luvun n kertoman n! """
    k = 1
    while n >= 2:
        k *= n
        n -= 1
    return k

if __name__ == "__main__":
    lista = [-2, 3, 2, 1, 4, -10, 5, 1, 6]
    kertomat = {luku : kertoma(luku) for luku in lista if luku > 0}
    print(kertomat)

```

<sample-output>

{3: 6, 2: 2, 1: 1, 4: 24, 5: 120, 6: 720}

</sample-output>

<programming-exercise name='Merkkijonojen pituudet' tmcname='osa11-11_merkkijonojen_pituudet'>

Tee funktio `pituudet(merkkijonot: list)`, joka saa parametriksi listan merkkijonoja. Funktio palauttaa _sanakirjan_, jossa avaimina on listan merkkijonot ja arvoina merkkijonojen pituudet.

Funktio tulee toteuttaa sanakirjakoosteen avulla. Funktion maksimipituus def-määrittelyrivi mukaanlukien on kaksi riviä.

Funktio toimii seuraavasti

```python
sanalista = ["suo", "kuokka" , "python", "ja", "koodari"]

sanojen_pituudet = pituudet(sanalista)
print(sanojen_pituudet)
```

<sample-output>

{'suo': 3, 'kuokka': 6, 'python': 6, 'ja': 2, 'koodari': 7}

</sample-output>


</programming-exercise>

<programming-exercise name='Yleisimmät sanat' tmcname='osa11-12_yleisimmat_sanat'>

Tee funktio `yleisimmat_sanat(tiedoston_nimi: str, raja: int)`, joka saa parametrikseen tiedoston nimen. Funktio palauttaa sanakirjan, joka sisältää tiedostossa olevien sanojen esiintymislukumäärän niiden sanojen osalta, joilla on vähintään toisen parametrin `raja` verran esiintymiä.

Esim. jos funktiolla tarkasteltaisiin tiedostoa _comprehensions.txt_ jonka sisältö on seuraava

```txt
List comprehension is an elegant way to define and create lists based on existing lists.
List comprehension is generally more compact and faster than normal functions and loops for creating list.
However, we should avoid writing very long list comprehensions in one line to ensure that code is user-friendly.
Remember, every list comprehension can be rewritten in for loop, but every for loop can’t be rewritten in the form of list comprehension.
```

Kutsuttaessa `yleisimmat_sanat("comprehensions.txt", 3)` funktion palauttama sanakirja näyttäisi seuraavalta:

<sample-output>

{'comprehension': 4, 'is': 3, 'and': 3, 'for': 3, 'list': 4, 'in': 3}

</sample-output>

Huomaa, että kirjainkoko vaikuttaa ja vain kokonaiset sanat lasketaan - sanat 'List' ja 'lists' eivät siis saa kasvattaa sanan 'list' lukumäärää. Lisäksi kaikki sanoissa olevat välimerkit tulee poistaa.

Funktion toteutustapa on vapaa, helpoimmalla pääset hyödyntämällä lista- ja sanakirjakoosteita.

</programming-exercise>
