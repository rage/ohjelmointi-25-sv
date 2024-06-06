---
path: '/osa-8/1-oliot-ja-metodit'
title: 'Objekt och metoder'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

- Kommer du veta vad ett objekt är i programmering
- Kommer du förstå vad som menas med oberoende hos individuella objekt
- Kommer du kunna skapa och komma åt objekt

</text-box>

Detta är första delen av den Avancerade Kursen inom Programmering. Materialet är designat för att bli använt med Visual Studio Code editeraren, liksom den föregående kursen Introduktion till Programming. Ifall du inte använt Visual Studio Code tidigare, så hittar du installeringsinstruktionerna [här](https://www.mooc.fi/fi/installation/vscode) och en introduktion till programmeringsomgivningen från förra kursen [här](https://programming-24.mooc.fi/part-4/1-vscode).

I introduktion till Programmering kursen så lade vi märke till att det ofta är logiskt att gruppera relaterad data tillsammans i våra program. Ifall vi till exemepl skulle förvara information om en bok skulle det vara logiskt att använda oss av en tuple eller en ordlista för att organisera datan till en enskild datastruktur.

Lösningen kunde se ut så här när man använder en tuple:

```python
nimi = "Nuoruuteni näppäilyt"
kirjailija = "Pekka Python"
vuosi = 1992

# Yhdistetään yhdeksi tupleksi
kirja = (nimi, kirjailija, vuosi)

# Tulostetaan kirjan nimi
print(kirja[0])
```

I ett fall som detta är fördelen med att använda en ordlista att vi kan använda strängar istället för indexar som nycklar. Alltså, kan vi ge deskriptiva namn till sakerna som förvaras datastrukturen:

```python
nimi = "Nuoruuteni näppäilyt"
kirjailija = "Pekka Python"
vuosi = 1992

# Yhdistetään yhdeksi sanakirjaksi
kirja = {"nimi": nimi, "kirjailija": kirjailija, "vuosi": vuosi}

# Tulostetaan kirjan nimi
print(kirja["nimi"])
```

I båda fallen så skapar vi ett nytt _objekt_. Inom programmering har termen specifikt betydelsen av en oberoende helhet, i detta fall innehållande några bitar av data som på något vis är relaterade. Att vara oberoende betyder att ändringar till ett objekt inte påverkar andra objekt.

Ifall vi skulle skapa två strukturellt identiska representationer av böcker, användandes ordlistor och identiska nycklar, skulle ändringar som görs till en av dem inte påverka den andra:

```python
kirja1 = {"nimi": "Vanhus ja Python", "kirjailija": "Ernest Pythonen", "vuosi": 1952}
kirja2 = {"nimi": "Seitsemän Pythonia", "kirjailija": "Aleksis Python", "vuosi": 1894}

print(kirja1["nimi"])
print(kirja2["nimi"])

kirja1["nimi"] = "Jäähyväiset aaseille"

print(kirja1["nimi"])
print(kirja2["nimi"])
```

<sample-output>

Vanhus ja Python
Seitsemän Pythonia
Jäähyväiset aaseille
Seitsemän Pythonia

</sample-output>

<img src="8_1_1.png">

<text-box variant="info" name="Python objekt">


Du kanske kommer ihåg från introduktion till programmering kursen att vilket som helst värde i Python internt är behandlat som ett objekt. Detta betyder att värdet lagrat i en variabel är en _referens till ett objekt_. Själva datan är lagrad inuti ett objekt i datorns minne. Ifall du ger ett värde till en ny variable med kommandot `a = 3`, är värdet som lagras i variabeln _inte_ 3, utan en _referens till ett objekt som innehåller värdet 3_.

De flesta andra programmeringsspråk (i varje fall de som stöder objekt-orienterad programmering) inkluderar vissa särskilt definierade _primitiva datatyper_. Dessa inkluderar ofta åtminstone [integer] nummer, flyttals nummer och boleska sanningsvärden. Primitiver är processerade direkt, vilket betyder att de är lagrade direkt i variabler, inte som referenser. Python har inga sådana primitiver, men att jobba med de grundläggade datatyperna i Python är i praktiken väldigt liknande. Objekt av dessa grundläggande datatyper (såsom nummer, boleska värden och strängar) är _oföränderliga_, vilket betyder att de inte kan ändras i minnet. Ifall värdet som lagras i en variabel med en grundläggande datatyp måste ändras så byts hela referensen ut, men själva objektet kvarstår i minnet.


</text-box>

## Objekt och metoder

Datan som lagras i ett objekt kan kommas åt genom olika _metoder_. En metod är en funktion som opererar på ett specifikt objekt som den är kopplad till. Sättet att åtskilja mellan metoder och andra funktioner ligger i hur de är kallade: först skriver man namnet på objektet som avses, sedan en punkt och till sist metodens namn, åtföljt av argument ifall sådana finns. Till exempel returnerar metoden `values` alla värden som är lagrade i ett objekt av typen ordlista eller `dict`:

```python
# muodostetaan sanakirjatyyppinen kirjaolio
kirja = {"nimi": "Vanhus ja Python", "kirjailija": "Ernest Pythonen", "vuosi": 1952}

# Tulostetaan kaikki arvot
# Metodikutsu values() kirjoitetaan muuttujan perään
# pisteellä erotettuna
for arvo in kirja.values():
    print(arvo)
```

<sample-output>

Vanhus ja Python
Ernest Pythonen
1952

</sample-output>

På samma sätt opererar en strängmetod på det strängobjekt som den kallas på. Några exempel av strängmetoder är `count` och `find`:

```python
nimi = "Keijo Keksitty"

# Tulostetaan K-kirjaimien määrä
print(nimi.count("K"))

# K-kirjaimien määrä toisessa jonossa
print("Karkkilan Kolisevat Karjut".count("K"))

# Osajonon Keksitty indeksi
print(nimi.find("Keksitty"))

# Tästä merkkijonosta osajonoa ei löydy
print("Ihan eri jono".find("Keksitty"))
```

<sample-output>

2
3
6
-1

</sample-output>

Strängmetoder returnerar värden, men ändrar inte innehållet av en sträng. Liksom nämnt ovan är strängar i Python oföränderliga. Detta gäller däremot inte alla metoder; Pythonlistor är föränderliga, alltså kan listmetoder ändra innehållet av listan som de kallas på: 

```python
lista = [1,2,3]

# Lisätään pari alkiota
lista.append(5)
lista.append(1)

print(lista)

# Poistetaan alkio alusta
lista.pop(0)

print(lista)
```

<sample-output>

[1, 2, 3, 5, 1]
[2, 3, 5, 1]

</sample-output>

<programming-exercise name='Pienin keskiarvo' tmcname='osa08-01_pienin_keskiarvo'>

Tee funktio `pienin_keskiarvo(henkilo1: dict, henkilo2: dict, henkilo3: dict)`, joka saa parametrikseen kolme sanakirjaoliota.

Jokaisessa sanakirjaoliossa on alkiot, joihin viittaavat nämä avaimet:

* `"nimi"`: kilpailijan nimi
* `"tulos1"`: kilpailijan ensimmäinen tulos (kokonaisluku väliltä 1...10)
* `"tulos2"`: kilpailijan toinen tulos (kuten yllä)
* `"tulos3"`: kilpailijan kolmas tulos (kuten yllä)

Funktio laskee kaikkien kilpailijoiden tulosten keskiarvot ja palauttaa sen kilpailijan, jonka keskiarvo on pienin. Funktion palautusarvona on sanakirjaolio.

Voit olettaa, että vain yhdellä henkilöllä on pienin keskiarvo.

Esimerkki funktion kutsumisesta:

```python
henkilo1 = {"nimi": "Keijo", "tulos1": 2, "tulos2": 3, "tulos3": 3}
henkilo2 = {"nimi": "Reijo", "tulos1": 5, "tulos2": 1, "tulos3": 8}
henkilo3 = {"nimi": "Veijo", "tulos1": 3, "tulos2": 1, "tulos3": 1}

print(pienin_keskiarvo(henkilo1, henkilo2, henkilo3))
```

<sample-output>

{'nimi': 'Veijo', 'tulos1': 3, 'tulos2': 1, 'tulos3': 1}

</sample-output>

</programming-exercise>

<programming-exercise name='Rivien summat' tmcname='osa08-02_rivien_summmat '>

Listan alkioiden arvot ovat viittauksia olioihin. Tämä pätee myös silloin, kun mallinnetaan matriisia: jokainen päälistan alkion arvo on viittaus toiseen listaan (jonka alkiot taas ovat viittauksia arvoihin).

Tee funktio `rivien_summat(matriisi: list)`, joka saa parametrikseen kokonaislukuja sisältävän matriisin.

Funktio lisää jokaiselle matriisin riville uuden alkion, jonka arvo on rivin alkioiden summa. Funktio ei palauta mitään, vaan muokkaa parametrinaan saamaansa matriisia.

Esimerkki funktion kutsumisesta:

```python
matriisi = [[1, 2], [3, 4]]
rivien_summat(matriisi)
print(matriisi)
```

<sample-output>

[[1, 2, 3], [3, 4, 7]]

</sample-output>

</programming-exercise>
