---
path: '/osa-12/1-funktio-parametrina'
title: 'Funktioner som argument'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Kan du sortera listor enligt olika kriterier
- Kommer du att veta vad ett lambdauttryck är
- Kan du använda lambda-uttryck med andra Python-funktioner
- Vet du hur en funktion skickas som argument till en annan funktion

</text-box>

Vi är redan bekanta med metoden `sort` och funktionen `sorted`, som används för att sortera listor i deras naturliga ordning. För siffror och strängar fungerar detta vanligtvis bra. För allt som är mer komplicerat än dem så är dock den naturliga ordningen på föremål enligt Python inte alltid det som vi som programmerare avser.

Till exempel sorteras som standard en lista med tupler baserat på det första objektet i varje tupel:

```python
tuotteet = [("banaani", 5.95), ("omena", 3.95), ("appelsiini", 4.50), ("vesimeloni", 4.95)]

tuotteet.sort()

for tuote in tuotteet:
    print(tuote)
```

<sample-output>

('appelsiini', 4.5)
('banaani', 5.95)
('omena', 3.95)
('vesimeloni', 4.95)

</sample-output>

Men vad händer om vi vill sortera listan baserat på priset?

## Funktioner som argument

En sorteringsmetod eller -funktion accepterar vanligtvis ett valfritt andra argument som gör att du kan kringgå standardsorteringskriterierna. Detta andra argument är en funktion som definierar hur värdet på varje föremål i listan bestäms. När listan sorteras anropar Python denna funktion när den jämför föremålen med varandra.

Låt oss ta en titt på ett exempel:

```python
def hintajarjestys(alkio: tuple):
    # Palautetaan tuplen toinen alkio eli hinta
    return alkio[1]

if __name__ == "__main__":
    tuotteet = [("banaani", 5.95), ("omena", 3.95), ("appelsiini", 4.50), ("vesimeloni", 4.95)]

    # Hyödynnetään funktiota hintajarjestys
    tuotteet.sort(key=hintajarjestys)

    for tuote in tuotteet:
        print(tuote)
```

<sample-output>

('omena', 3.95)
('appelsiini', 4.5)
('vesimeloni', 4.95)
('banaani', 5.95)

</sample-output>

Nu är listan sorterad utifrån artiklarnas priser, men vad händer egentligen i programmet?

Funktionen `ordning_enligt_pris` är faktiskt ganska enkel. Den tar ett objekt som sitt argument och returnerar ett värde för det objektet. Mer specifikt returnerar den det andra objektet i tupeln, som representerar priset. Men sedan har vi den här kodraden, där `sort`-metoden anropas:

`produkter.sort(key=ordning_enligt_pris)`

Här anropas `sort`-metoden med en funktion som argument. Detta är inte en referens till funktionens returvärde, utan en referens till själva funktionen. `Sort`-metoden anropar denna funktion flera gånger och använder varje objekt i listan som argument i tur och ordning.

Om vi inkluderar en extra print-sats i funktionsdefinitionen för `ordning_enligt_pris` kan vi verifiera att funktionen verkligen anropas en gång för varje objekt i listan:

```python
def hintajarjestys(alkio: tuple):
    # Tulostetaan alkio
    print(f"Kutsuttiin hintajarjestys({alkio})")

    # Palautetaan tuplen toinen alkio eli hinta
    return alkio[1]


tuotteet = [("banaani", 5.95), ("omena", 3.95), ("appelsiini", 4.50), ("vesimeloni", 4.95)]

# Hyödynnetään funktiota hintajarjestys
tuotteet.sort(key=hintajarjestys)

for tuote in tuotteet:
    print(tuote)
```

<sample-output>

Kutsuttiin hintajarjestys(('banaani', 5.95))
Kutsuttiin hintajarjestys(('omena', 3.95))
Kutsuttiin hintajarjestys(('appelsiini', 4.5))
Kutsuttiin hintajarjestys(('vesimeloni', 4.95))
('omena', 3.95)
('appelsiini', 4.5)
('vesimeloni', 4.95)
('banaani', 5.95)

</sample-output>

Ordningen kan vändas med ett annat nyckelordsargument; `reverse`, som är tillgängligt med både `sort`-metoden och funktionen `sorted`:

```python
tuotteet.sort(key=hintajarjestys, reverse=True)

t2 = sorted(tuotteet, key=hintajarjestys, reverse=True)
```

## En funktionsdefinition inom en funktionsdefinition

Vi kan också inkludera en namngiven funktion för den nya prisbaserade sorteringsfunktionen som vi har skapat. Låt oss lägga till en funktion med namnet `sortera_enligt_pris`:

```python
def hintajarjestys(alkio: tuple):
    return alkio[1]

def jarjesta_hinnan_mukaan(alkiot: list):
    # käytetään täällä funktiota hintajarjestys
    return sorted(alkiot, key=hintajarjestys)

tuotteet = [("banaani", 5.95), ("omena", 3.95), ("appelsiini", 4.50), ("vesimeloni", 4.95)]

for tuote in jarjesta_hinnan_mukaan(tuotteet):
    print(tuote)
```

Om vi vet att hjälpfunktionen `ordning_enligt_pris` inte används någonstans utanför funktionen `sortera_enligt_pris`, kan vi placera den första funktionsdefinitionen inom den senare:

```python
def jarjesta_hinnan_mukaan(alkiot: list):
    # määritellään apufunktio tällä kertaa funktion sisällä
    def hintajarjestys(alkio: tuple):
        return alkio[1]

    return sorted(alkiot, key=hintajarjestys)
```

<programming-exercise name='Järjestys varastosaldon mukaan' tmcname='osa12-01_varastosaldo'>

Tee funktio `jarjesta_varastosaldon_mukaan(alkiot: list)`. Funktio saa parametrina listan tupleja, joissa kolmantena alkiona on tuotteiden varastosaldo. Funktio järjestää parametrinaan saamat tuotteet varastosaldojen  mukaiseen kasvavaan järjestykseen.  Funktio ei muuta parametrina olevaa listaa, vaan palauttaa uuden listan.

Funktio toimii seuraavasti:

```python
tuotteet = [("banaani", 5.95, 12), ("omena", 3.95, 3), ("appelsiini", 4.50, 2), ("vesimeloni", 4.95, 22)]

for tuote in jarjesta_varastosaldon_mukaan(tuotteet):
    print(f"{tuote[0]} {tuote[2]} kpl")
```

<sample-output>
appelsiini 2 kpl
omena 3 kpl
banaani 12 kpl
vesimeloni 22 kpl
</sample-output>

</programming-exercise>

<programming-exercise name='Järjestys tuotantokausien mukaan' tmcname='osa12-02_tuotantokaudet'>

Tee funktio `jarjesta_tuotantokausien_mukaan(alkiot: list)`. Funktio saa parametrina listan sanakirjoja, jotka edustavat yksittäisiä TV-sarjoja, ja järjestää ne tuotantokausien lukumäärän mukaiseen kasvavaan järjestykseen. Funktio ei muuta parametrina olevaa listaa, vaan palauttaa uuden listan.

Funktio toimii seuraavasti:

```python
sarjat = [{ "nimi": "Dexter", "pisteet" : 8.6, "kausia":9 }, { "nimi": "Friends", "pisteet" : 8.9, "kausia":10 },  { "nimi": "Simpsons", "pisteet" : 8.7, "kausia":32 }  ]

for sarja in jarjesta_tuotantokausien_mukaan(sarjat):
    print(f"{sarja['nimi']}  {sarja['kausia']} tuotantokautta")
```

<sample-output>
Dexter 9 tuotantokautta
Friends 10 tuotantokautta
Simpsons 32 tuotantokautta
</sample-output>

</programming-exercise>

<programming-exercise name='Järjestys pisteiden mukaan' tmcname='osa12-03_pisteiden_mukaan'>

Tee funktio `jarjesta_pisteiden_mukaan(alkiot: list)`. Funktio saa parametrina listan sanakirjoja, jotka edustavat yksittäisiä TV-sarjoja, ja järjestää ne _pisteiden mukaiseen laskevaan järjestykseen_.  Funktio ei muuta parametrina olevaa listaa, vaan palauttaa uuden listan.

```python
sarjat = [{ "nimi": "Dexter", "pisteet" : 8.6, "kausia":9 }, { "nimi": "Friends", "pisteet" : 8.9, "kausia":10 },  { "nimi": "Simpsons", "pisteet" : 8.7, "kausia":32 }  ]

print("IMDB:n mukainen pistemäärä")
for sarja in jarjesta_pisteiden_mukaan(sarjat):
    print(f"{sarja['nimi']}  {sarja['pisteet']}")
```

<sample-output>
IMDB:n mukainen pistemäärä
Friends 8.9
Simpsons 8.7
Dexter 8.6
</sample-output>

</programming-exercise>

## Sortering av samlingar av egna objekt

Låt oss med samma princip skriva ett program som sorterar en lista med objekt från vår egen klass `Student` på två olika sätt:

```python
class Opiskelija:
    """ Luokka mallintaa yhtä opiskelijaa """
    def __init__(self, nimi: str, tunnus: str, pisteet: int):
        self.nimi = nimi
        self.tunnus = tunnus
        self.pisteet = pisteet

    def __str__(self):
        return f"{self.nimi} ({self.tunnus}), {self.pisteet} op."


def tunnuksen_mukaan(alkio: Opiskelija):
    return alkio.tunnus

def pisteiden_mukaan(alkio: Opiskelija):
    return alkio.pisteet


if __name__ == "__main__":
    o1 = Opiskelija("Aapeli", "a123", 220)
    o2 = Opiskelija("Maija", "m321", 210)
    o3 = Opiskelija("Anna", "a999", 131)

    opiskelijat = [o1, o2, o3]

    print("Tunnuksen mukaan:")
    for opiskelija in sorted(opiskelijat, key=tunnuksen_mukaan):
        print(opiskelija)

    print()

    print("Pisteiden mukaan:")
    for opiskelija in sorted(opiskelijat, key=pisteiden_mukaan):
        print(opiskelija)
```

<sample-output>

Aapeli (a123), 220 op.
Anna (a999), 131 op.
Maija (m321), 210 op.

Pisteiden mukaan:
Anna (a999), 131 op.
Maija (m321), 210 op.
Aapeli (a123), 220 op.

</sample-output>

Som du kan se ovan fungerar sortering efter olika kriterier precis som det är tänkt. Om funktionerna `enligt_id` och `enligt_studiepoäng` inte behövs någon annanstans finns det sätt att göra implementeringen enklare. Vi återkommer till detta ämne efter dessa övningar.

<programming-exercise name='Kiipeilyreitti' tmcname='osa12-04_kiipeilyreitti'>

Tehtäväpohjan mukana tulee valmis luokka `Kiipeilyreitti`, jota käytetään seuraavasti:

```python
reitti1 = Kiipeilyreitti("Kantti", 38, "6A+")
reitti2 = Kiipeilyreitti("Smooth operator", 11, "7A")
reitti3 = Kiipeilyreitti("Syncro", 14, "8C+")


print(reitti1)
print(reitti2)
print(reitti3.nimi, reitti3.pituus, reitti3.grade)
```

<sample-output>

Kantti, pituus 38 metriä, grade 6A+
Smooth operator, pituus 11 metriä, grade 7A
Syncro 14 8C+

</sample-output>

## Pituuden mukainen järjestys

Tee funktio `pituuden_mukaan(reitit: list)` joka palauttaa kiipeilyreitit pituuden mukaan käänteisessä järjestyksessä.

Funktio toimii seuraavasti:

```python
r1 = Kiipeilyreitti("Kantti", 38, "6A+")
r2 = Kiipeilyreitti("Smooth operator", 11, "7A")
r3 = Kiipeilyreitti("Syncro", 14, "8C+")
r4 = Kiipeilyreitti("Pieniä askelia", 12, "6A+")

reitit = [r1, r2, r3, r4]

for reitti in pituuden_mukaan(reitit):
    print(reitti)
```

<sample-output>

Kantti, pituus 38 metriä, grade 6A+
Syncro, pituus 14 metriä, grade 8C+
Pieniä askelia, pituus 12 metriä, grade 6A+
Smooth operator, pituus 11 metriä, grade 7A

</sample-output>

## Vaikeuden mukainen järjestys

Tee funktio `vaikeuden_mukaan(reitit: list)` joka palauttaa kiipeilyreitit vaikeuden (eli graden) mukaan laskevassa järjestyksessä. Jos reittien vaikeus on sama, ratkaisee pituus vaikeuden. Pidempi on vaikeampi. Kiipeilyreittien vaikeusasteikko on _4, 4+, 5, 5+, 6A, 6A+, ..._ eli käytännössä se seuraa aakkosjärjestystä.

Funktio toimii seuraavasti:

```python
r1 = Kiipeilyreitti("Kantti", 38, "6A+")
r2 = Kiipeilyreitti("Smooth operator", 11, "7A")
r3 = Kiipeilyreitti("Syncro", 14, "8C+")
r4 = Kiipeilyreitti("Pieniä askelia", 12, "6A+")

reitit = [r1, r2, r3, r4]
for reitti in vaikeuden_mukaan(reitit):
    print(reitti)
```

<sample-output>

Syncro, pituus 14 metriä, grade 8C+
Smooth operator, pituus 11 metriä, grade 7A
Kantti, pituus 38 metriä, grade 6A+
Pieniä askelia, pituus 12 metriä, grade 6A+

</sample-output>

*Vihje* jos järjestysperusteena on lista tai tuple, järjestetään ensisijaiseti ensimmäisen alkion mukaan, toissijaisesti toisen:

```python
lista = [("a", 4),("a", 2),("b", 30), ("b", 0) ]
print(sorted(lista))
```

<sample-output>

[('a', 2), ('a', 4), ('b', 0), ('b', 30)]

</sample-output>

</programming-exercise>

<programming-exercise name='Kiipeilykalliot' tmcname='osa12-05_kiipeilykalliot/'>

Tehtäväpohjasta löytyy luokan `Kiipeilyreitti` lisäksi luokka `Kiipeilykallio`.

```python
k1 = Kiipeilykallio("Olhava")
k1.lisaa_reitti(Kiipeilyreitti("Kantti", 38, "6A+"))
k1.lisaa_reitti(Kiipeilyreitti("Suuri leikkaus", 36, "6B"))
k1.lisaa_reitti(Kiipeilyreitti("Ruotsalaisten reitti", 42, "5+"))

k2 = Kiipeilykallio("Nummi")
k2.lisaa_reitti(Kiipeilyreitti("Syncro", 14, "8C+"))

k3 = Kiipeilykallio("Nalkkilan släbi")
k3.lisaa_reitti(Kiipeilyreitti("Pieniä askelia", 12, "6A+"))
k3.lisaa_reitti(Kiipeilyreitti("Smooth operator", 11, "7A"))
k3.lisaa_reitti(Kiipeilyreitti("Possu ei pidä", 12 , "6B+"))
k3.lisaa_reitti(Kiipeilyreitti("Hedelmätarha", 8, "6A"))

print(k1)
print(k3.nimi, k3.reitteja())
print(k3.vaikein_reitti())
```

<sample-output>

Olhava, 3 reittiä, vaikein 6B
Nalkkilan slabi 4
Smooth operator, pituus 9 metriä, grade 7A

</sample-output>

## Reittien määrän mukaan

Tee funktio `reittien_maaran_mukaan`, joka järjestää kiipeilykalliot reittien määrän mukaiseen kasvavaan suuruusjärjestykseen.

```python
# k1, k2 ja k3 määritelty kuten edellä
kalliot = [k1, k2, k3]
for kallio in reittien_maaran_mukaan(kalliot):
    print(kallio)

```

<sample-output>

Nummi, 1 reittiä, vaikein 8C+
Olhava, 3 reittiä, vaikein 6B
Nalkkilan slabi, 4 reittiä, vaikein 7A

</sample-output>

## Vaikeimman reitin mukaan

Tee funktio `vaikeimman_reitin_mukaan`, joka järjestää kiipeilykalliot kalliolta löytyvän vaikeimman reitin mukaiseen _laskevaan_ suuruusjärjestykseen.

```python
# k1, k2 ja k3 määritelty kuten edellä
kalliot = [k1, k2, k3]
for kallio in vaikeimman_reitin_mukaan(kalliot):
    print(kallio)

```

<sample-output>

Nummi, 1 reittiä, vaikein 8C+
Nalkkilan slabi, 4 reittiä, vaikein 7A
Olhava, 3 reittiä, vaikein 6B

</sample-output>

</programming-exercise>

## Lambda-uttryck

Vi har mest arbetat med funktioner ur modularitetssynpunkt. Det är sant att funktioner spelar en viktig roll när det gäller att hantera komplexiteten i dina program och undvika upprepning av kod. Funktioner skrivs vanligtvis så att de kan användas många gånger.

Men ibland behöver man något som liknar en funktion som man bara använder en gång. Med lambda-uttryck kan du skapa små, anonyma funktioner som skapas (och kasseras) när de behövs i koden. Den allmänna syntaxen är som följer:

`lambda <parametrar> : <uttryck>`

Att sortera en lista med tupler efter det andra objektet i varje tupel skulle se ut så här implementerat med ett lambda-uttryck:

```python
tuotteet = [("banaani", 5.95), ("omena", 3.95), ("appelsiini", 4.50), ("vesimeloni", 4.95)]

# Funktio luodaan "lennosta" lambda-lausekkeella:
tuotteet.sort(key=lambda alkio: alkio[1])

for tuote in tuotteet:
    print(tuote)
```

<sample-output>

('omena', 3.95)
('appelsiini', 4.5)
('vesimeloni', 4.95)
('banaani', 5.95)

</sample-output>

Uttrycket

`lambda föremål: föremål[1]`

Är ekvivalent med funktionsdefinitionen

```python

def hinta(alkio):
    return alkio[1]
```

förutom det faktum att en lambdafunktion inte har något namn. Det är därför lambda-funktioner kallas anonyma funktioner.

I alla andra avseenden skiljer sig inte en lambda-funktion från någon annan funktion, och de kan användas i alla samma sammanhang som en motsvarande namngiven funktion. Följande program sorterar till exempel en lista med strängar i alfabetisk ordning enligt det sista tecknet i varje sträng:

```python
mjonot = ["Mikko", "Makke", "Maija", "Markku", "Mikki"]

for jono in sorted(mjonot, key=lambda jono: jono[-1]):
    print(jono)
```

<sample-output>

Maija
Makke
Mikki
Mikko
Markku

</sample-output>

Vi kan också kombinera list comprehensions, `join`-metoden och lambda-uttryck. Vi kan till exempel sortera strängar baserat på enbart vokalerna i dem och ignorera alla andra tecken:

```python
mjonot = ["Mikko", "Makke", "Maija", "Markku", "Mikki"]

for jono in sorted(mjonot, key=lambda jono: "".join([m for m in jono if m in "aeiouyäö"])):
    print(jono)
```

<sample-output>

Makke
Maija
Markku
Mikki
Mikko

</sample-output>

Anonyma funktioner kan också användas med andra inbyggda Python-funktioner, inte bara de som används för sortering. Till exempel tar funktionerna `min` och `max` också ett nyckelordsargument som heter `key`. Det används som kriterium för att jämföra objekten när det lägsta eller högsta värdet väljs.

I följande exempel handlar det om ljudinspelningar. Först väljer vi den äldsta inspelningen och sedan den längsta:

```python

class Levy:
    """Luokka mallintaa yhtä äänilevyä"""
    def __init__(self, nimi: str, esittaja: str, vuosi: int, kesto: int):
        self.nimi = nimi
        self.esittaja = esittaja
        self.vuosi = vuosi
        self.kesto = kesto


    def __str__(self):
        return f"{self.nimi} ({self.esittaja}), {self.vuosi}. {self.kesto} min."

if __name__ == "__main__":
    l1 = Levy("Nevermind", "Nirvana", 1991, 43)
    l2 = Levy("Let It Be", "Beatles", 1969, 35)
    l3 = Levy("Joshua Tree", "U2", 1986, 50)

    levyt = [l1, l2, l3]


    print("Vanhin levy:")
    print(min(levyt, key=lambda levy: levy.vuosi))

    print("Pisin levy: ")
    print(max(levyt, key=lambda levy: levy.kesto))
```

<sample-output>

Vanhin levy:
Let It Be (Beatles), 1969. 35 min.
Pisin levy:
U2 (Joshua Tree), 1986. 50 min.

</sample-output>

<programming-exercise name='Palloilijat' tmcname='osa12-06_palloilijat'>

Tehtäväpohjasta löytyy luokka `Palloilija`, jolla on seuraavat julkiset piirteet:

* nimi
* pelinumero
* tehtyjen maalien määrä `maalit`
* annettujen syöttöjen määrä `syotot`
* peliminuuttien määrä `minuutit`

Kirjoita seuraavien tehtävänantojen mukaiset funktiot. Huomaa, että jokaisessa funktiossa palautetaan erityyppiset tiedot.

## Eniten maaleja

Kirjoita funktio `eniten_maaleja`, joka saa parametrikseen listan palloilijoita.

Funktio palauttaa merkkijonona sen pelaajan nimen, joka on tehnyt eniten maaleja.

## Eniten pisteitä

Kirjoita funktio `eniten_pisteita`, joka saa parametrikseen listan palloilijoita.

Funktio palauttaa tuplena sen pelaajan nimen ja pelinumeron, joka on tehnyt yhteensä eniten pisteitä. Pisteisiin lasketaan siis sekä maalit että syötöt.

## Vähiten peliminuutteja

Kirjoita funktio `vahiten_minuutteja`, joka saa parametrikseen listan palloilijoita.

Funktio palauttaa sen `Palloilija`-olion, jolla on vähiten peliminuutteja kaikista pelaajista.

## Testiohjelma

Voit testata koodisi toimintaa seuraavalla ohjelmalla:

```python
if __name__ == "__main__":
    pelaaja1 = Palloilija("Kelju Kojootti", 13, 5, 12, 46)
    pelaaja2 = Palloilija("Maantiekiitäjä", 7, 2, 26, 55)
    pelaaja3 = Palloilija("Uka Naakka", 9, 1, 32, 26)
    pelaaja4 = Palloilija("Pelle Peloton", 12, 1, 11, 41)
    pelaaja5 = Palloilija("Hessu Hopo", 4, 3, 9, 12)

    joukkue = [pelaaja1, pelaaja2, pelaaja3, pelaaja4, pelaaja5]
    print(eniten_maaleja(joukkue))
    print(eniten_pisteita(joukkue))
    print(vahiten_minuutteja(joukkue))
```

Tulostuksen tulisi olla:

<sample-output>

Kelju Kojootti
('Uka Naakka', 9)
Palloilija(nimi=Hessu Hopo, pelinumero=4, maalit=3, syotot=9, minuutit=12)

</sample-output>

</programming-exercise>

## Funktioner som argument inom egna funktioner

Vi konstaterade ovan att det är möjligt att skicka en referens till en funktion som argument till en annan funktion. Som avslutning på detta avsnitt skriver vi en egen funktion som tar en funktion som argument.

```python
# tyyppivihje callable viittaa funktioon
def suorita_operaatio(operaatio: callable):
    # Kutsutaan välitettyä funktiota
    return operaatio(10, 5)

def summa(a: int, b: int):
    return a + b

def tulo(a: int, b: int):
    return a * b


if __name__ == "__main__":
    print(suorita_operaatio(summa))
    print(suorita_operaatio(tulo))
    print(suorita_operaatio(lambda x,y: x - y))

```

<sample-output>

15
50
5

</sample-output>

Det värde som returneras av funktionen `utfor_operation` beror på vilken funktion som skickades som argument. Vilken funktion som helst som tar emot två argument skulle duga, oavsett om den är anonym eller namngiven.

Att skicka referenser till funktioner som argument till andra funktioner är kanske inte något som du kommer att göra dagligen under din programmeringskarriär, men det kan vara en användbar teknik. Följande program väljer ut några rader från en fil och skriver dem till en annan fil. Hur raderna väljs ut bestäms av en funktion som returnerar True endast om raderna ska kopieras:

```python
def kopioi_rivit(lahde_nimi: str, kohde_nimi: str, kriteeri= lambda x: True):
    with open(lahde_nimi) as lahde, open(kohde_nimi, "w") as kohde:
        for rivi in lahde:
            # Poistetaan ensin tyhjät merkit alusta ja lopusta
            rivi = rivi.strip()

            if kriteeri(rivi):
                kohde.write(rivi + "\n")

# Esimerkkejä
if __name__ == "__main__":
    # Jos kolmatta parametria ei ole määritelty, kopioidaan kaikki
    kopioi_rivit("eka.txt", "toka.txt")

    # Kopioidaan kaikki ei-tyhjät rivit
    kopioi_rivit("eka.txt", "toka.txt", lambda rivi: len(rivi) > 0)

    # Kopioidaan kaikki rivit, joilla on sana "Python"
    kopioi_rivit("eka.txt", "toka.txt", lambda rivi: "Python" in rivi)

    # Kopioidaan kaikki rivit, jotka eivät pääty pisteeseen
    kopioi_rivit("eka.txt", "toka.txt", lambda rivi: rivi[-1] != ".")
```

Funktionsdefinitionen innehåller ett standardvärde för nyckelordsparametern `kriterie`: `lambda x: True`. Denna anonyma funktion returnerar alltid `True` oavsett indata. Standardbeteendet är alltså att kopiera alla rader. Som vanligt gäller att om ett värde anges för en parameter med ett standardvärde, ersätter det nya värdet standardvärdet. 

<programming-exercise name='Tuotteiden haku' tmcname='osa12-07_tuotteiden_haku'>

Tässä tehtävässä käsitellään tupleina esitettäviä tuotteita, jotka on esimerkeissä alustettu muuttujaan `tuotteet` seuraavasti:

```python
tuotteet = [("banaani", 5.95, 12), ("omena", 3.95, 3), ("appelsiini", 4.50, 2), ("vesimeloni", 4.95, 22), ("Kaali", 0.99, 1)]
```

Jokaisessa tuplessa ensimmäinen alkio siis edustaa nimeä, seuraava hintaa ja kolmas määrää.

Toteuta funktio `hae(tuotteet: list, kriteeri: callable)`, missä toisena parametrina on funktio, joka saa parametriksi yhden tuotetta edustavan tuplen ja palauttaa totuusarvon. Funktio palauttaa listassa parametrina annetuista tuotteista ne, jotka toteuttavat kriteerin.

Sopiva kriteeri voisi olla esimerkiksi seuraavanlainen

```python
def hinta_alle_4_euroa(tuote):
    return tuote[1] < 4
```

Funktio siis palauttaa _True_ jos tuotteen hinta on alle 4 euroa.

Funktio `haku` toimii seuraavasti:

```python
for tuote in hae(tuotteet, hinta_alle_4_euroa):
    print(tuote)
```

<sample-output>

('omena', 3.95, 3)
('kaali', 0.99, 1)

</sample-output>

Kriteerifunktion voi myös määritellä lambda-funktiona. Seuraava käyttää funktiota `haku` etsimään tuotteet, joita on vähintään 11 kappaletta:

```python
for tuote in hae(tuotteet, lambda t: t[2]>10):
    print(tuote)
```

<sample-output>

('banaani', 5.95, 12)
('vesimeloni', 4.95, 22)

</sample-output>

</programming-exercise>
