---
path: '/osa-7/4-datan-kasittely'
title: 'Behandla data'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* kan du använda en modul för att behandla CSV-filer
* kan du använda en modul för att behandla JSON-filer
* kan du komma åt filer från internet och läsa dem.

</text-box>

## Läsa CSV-filer

CSV är ett så enkelt format att vi tills vidare har behandlat dessa filer med självskriven kod. Det finns däremot en färdig modul för CSV-filer i Pythons standardbibliotek: `csv`. Modulen fungerar så här:

```python
import csv

with open("testi.csv") as tiedosto:
    for rivi in csv.reader(tiedosto, delimiter=";"):
        print(rivi)
```

Koden ovan läser alla rader i CSV-filen `test.csv`, skiljer innehåller på varje rad med separatorn `;` och skriver ut varje lista. Om innehållet i filen är det följande…

```x
012121212;5
012345678;2
015151515;4
```

…borde koden skriva ut det här:

<sample-output>

['012121212', '5']
['012345678', '2']
['015151515', '4']

</sample-output>

Eftersom CSV-formatet är så enkelt, kan vi fråga oss vad nyttan med en skild modul är då vi bara kunde använda `split`-funktionen. Det finns några bra orsaker. En orsak är att `csv`-modulen klarar av strängar som innehåller skiljetecknet:

```x
"aaa;bbb";"ccc;ddd"
```

Koden ovan skulle då ge följande resultat:

<sample-output>

['aaa;bbb', 'ccc;ddd']

</sample-output>

Om vi skulle använda `split`-funktionen, skulle själva strängarna också delas i två, vilket skulle förstöra den data som ska behandlas och antagligen orsaka problem i programmet.

## Läsa JSON-filer

CSV är bara ett maskinläsbart dataformat. JSON är ett annat sådant format och det används ofta när data överförs mellan olika program.

JSON-filer är textfiler som följer en strikt syntax, som eventuellt är lite mindre människovänligt än CSV-formatet. Följande exempel använder filen `kurser.json`, som innehåller information om några kurser:

```x
[
    {
        "nimi": "Ohjelmoinnin perusteet",
        "tunnus": "Ohpe",
        "periodit": [1, 3]
    },
    {
        "nimi": "Ohjelmoinnin jatkokurssi",
        "tunnus": "Ohja",
        "periodit": [2, 4]
    },
    {
        "nimi": "Tietokantasovellus",
        "tunnus": "Tsoha",
        "periodit": [1, 2, 3, 4]
    }
]
```


Strukturen hos en JSON-fil kanske ser bekant ut. JSON-filen ser ut som en Python-lista som innehåller tre Python-lexikon.

Standardbiblioteket innehåller `json`-modulen som kan användas för att behandla JSON-filer. Funktionen `loads` tar emot ett argument som innehåller data i JSON-format och konverterar den till Pythons egen datastruktur. När vi använder `kurser.json` i koden nedan…

```python
import json

with open("kurssit.json") as tiedosto:
    data = tiedosto.read()
kurssit = json.loads(data)
print(kurssit)
```

…får vi följande utskrift:

<sample-output>

[{'nimi': 'Ohjelmoinnin perusteet', 'tunnus': 'Ohpe', 'periodit': [1, 3]}, {'nimi': 'Ohjelmoinnin jatkokurssi', 'tunnus': 'Ohja', 'periodit': [2, 4]}, {'nimi': 'Tietokantasovellus', 'tunnus': 'Tsoha', 'periodit': [1, 2, 3, 4]}]

</sample-output>

Om vi vill skriva ut namnet på varje kurs kan vi använda en for-loop:

```python
for kurssi in kurssit:
    print(kurssi["nimi"])
```

<sample-output>

Ohjelmoinnin perusteet
Ohjelmoinnin jatkokurssi
Tietokantasovellus

</sample-output>

<programming-exercise name='JSON-tiedoston käsittely' tmcname='osa07-12_jsontiedostot'>

Tarkastellaan JSON-tiedostoa, jossa on tietoa opiskelijoista seuraavassa muodossa:

```json
[
    {
        "nimi": "Pekka Pythonisti",
        "ika": 27,
        "harrastukset": [
            "koodaus",
            "kutominen"
        ]
    },
    {
        "nimi": "Jaana Javanainen",
        "ika": 24,
        "harrastukset": [
            "koodaus",
            "kalliokiipeily",
            "lukeminen"
        ]
    }
]
```

Toteuta funktio `tulosta_henkilot(tiedosto: str)`, joka lukee esimerkin tavalla muodostetun JSON-tiedoston (jonka sisältönä voi olla mielivaltainen määrä henkilöitä) ja tulostaa ne seuraavassa muodossa:

<sample-output>

Pekka Pythonisti 27 vuotta (koodaus, kutominen)
Jaana Javanainen 24 vuotta (koodaus, kalliokiipeily, lukeminen)

</sample-output>

Harrastukset tulee luetella samassa järjestyksessä kuin ne on annettu JSON-tiedostossa.

</programming-exercise>

## Hämta en fil från internet

Standardbiblioteket i Python innehåller också moduler som kan användas för att hantera innehåll på internet. En nyttig funktion är `urllib.request.urlopen`. Det lönar sig att bekanta sig med modulen som helhet, men följande exempel borde räcka till för att få en insikt i hur funktionen fungerar. Den kan användas för att hämta data från internet, för vidare behandling i ditt program.

Följande kodstunn skriver ut innehållet från huvudsidan för Helsingfors universitet:

```python
import urllib.request

pyynto = urllib.request.urlopen("https://helsinki.fi")
print(pyynto.read())
```

Sidor som är skräddarsydda för människoögon ser inte vanligtvis trevliga ut när deras kod skrivs ut. I de kommande exemplen kommer vi däremot att läsa in data i maskinformat från internet. En stor del maskinläsbara data på internet är i JSON-format.

<programming-exercise name='Kurssien tilastot' tmcname='osa07-13_kurssistatistiikka'>

#### tieto kursseista

Osoitteesta <https://studies.cs.helsinki.fi/stats-mock/api/courses> löytyy JSON-muodossa muutaman laitoksen verkkokurssin perustiedot.

Tee funktio `hae_kaikki()` joka hakee ja palauttaa kaikkien menossa olevien kurssien (kentän `enabled` arvona `True`) tiedot listana tupleja. Paluuarvon muoto on seuraava:

<sample-output>

<pre>
[
    ('Full Stack Open 2020', 'ofs2019', 2020, 201),
    ('DevOps with Docker 2019', 'docker2019', 2019, 36),
    ('DevOps with Docker 2020', 'docker2020', 2020, 36),
    ('Beta DevOps with Kubernetes', 'beta-dwk-20', 2020, 28)
]
</pre>

</sample-output>

Jokainen tuple siis sisältää seuraavat arvot:

- kurssin koko nimi (`fullName`)
- nimi (`name`)
- vuosi (`year`)
- harjoitusten (`exercises`) yhteenlaskettu määrä


*Huom*: Tämän tehtävän testien toimivuuden osalta on oleellista, että haet tiedot funktiolla `urllib.request.urlopen`.

*Huom2:* Testeissä käytetään myös ovelaa kikkaa, joka hieman muuttaa internetistä tulevaa dataa ja tämän avulla varmistaa, että et huijaa tehtävässäsi palauttamalla "kovakoodattua" dataa.

*Huom3:* Jotkut Mac-käyttäjät ovat törmänneet tehtävässä seuraavaan ongelmaan:

```sh
File "/Library/Frameworks/Python.framework/Versions/3.8/lib/python3.8/urllib/request.py", line 1353, in do_open
    raise URLError(err)
urllib.error.URLError: <urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: unable to get local issuer certificate (_ssl.c:1124)>
```

Ongelman ratkaisutapa riippuu siitä miten python on asennettu koneellesi. Joissain tapauksissa toimii seuraava:

```sh
cd "/Applications/Python 3.8/"
sudo "./Install Certificates.command
```

Huomaa, että cd-komennon polku riippuu käyttämästäsi Pythonin versiosta. Se voi olla myös "/Applications/Python 3.8/".

[Täällä](https://stackoverflow.com/questions/27835619/urllib-and-ssl-certificate-verify-failed-error) on ehdotettu useita erilaisia ratkaisuja ongelmaan.

Eräs kikka jota voit kokeilla, on seuraava:

```python
import urllib.request
import json
import ssl # lisää tämä kirjasto importeihin

def hae_kaikki():
    # ja tämä rivi funktioiden alkuun
    context = ssl._create_unverified_context()
    # muu koodi
```

Toinen tapa kiertää ongelma on seuraava:

 ```python
import urllib.request
import certifi # lisää tämä kirjasto importeihin
import json

def hae_kaikki():
    osoite = "https://studies.cs.helsinki.fi/stats-mock/api/courses"
    # lisätään kutsuun toinen parametri
    pyynto = urllib.request.urlopen(osoite, cafile=certifi.where())
    # muu koodi
```

#### yhden kurssin tiedot

Kunkin kurssin JSON-muotoinen tehtävästatistiikka löytyy omasta osoitteesta, joka saadaan vaihtamalla kurssin kenttä `name` seuraavassa tähtien paikalle <https://studies.cs.helsinki.fi/stats-mock/api/courses/****/stats>

Esimerkiksi kurssin `docker2019` tiedot ovat osoitteessa <https://studies.cs.helsinki.fi/stats-mock/api/courses/docker2019/stats>

Tee ohjelmaasi funktio `hae_kurssi(kurssi: str)`, joka palauttaa kurssin tarkemman tehtävästatistiikan.

Kun kutsutaan `hae_kurssi("docker2019")`, funktio palauttaa sanakirjan, jonka sisältö on seuraava:

<sample-output>

<pre>
{
    'viikkoja': 4,
    'opiskelijoita': 220,
    'tunteja': 5966,
    'tunteja_keskimaarin': 27,
    'tehtavia': 4988,
    'tehtavia_keskimaarin': 22
}
</pre>

</sample-output>

Sanakirjaan tallennetut arvot määrittyvät seuraavasti:

- `viikkoja`: kurssia vastaavan JSON-olioiden määrä
- `opiskelijoita` viikkojen opiskelijamäärien maksimi
- `tunteja`: kakkien viikkojen tuntimäärien (`hour_total`) summa
- `tunteja_keskimaarin`: edellinen jaettuna opiskelijamäärällä (kokonaislukuna pyöristettynä alaspäin)
- `tehtavia`: kakkien viikkojen tehtävämäärien (`exercise_total`) summa
- `tehtavia_keskimaarin`: edellinen jaettuna opiskelijamäärällä (kokonaislukuna pyöristettynä alaspäin)

*Huom*: Samat huomiot pätevät tähän osaan kuin edelliseen!

*Huom2*: löydät [math](https://docs.python.org/3/library/math.html) -moduulista funktion, jonka avulla kokonaisluvun alaspäin pyöristäminen on helppoa

</programming-exercise>

<programming-exercise name='Kuka huijasi' tmcname='osa07-14_kuka_huijasi'>

Tiedostossa `tentin_aloitus.csv` on tenttien aloitusaikoja muodossa `tunnus;hh:mm`. Esimerkiksi:

```csv
jarmo;09:00
timo;18:42
kalle;13:23
```

Lisäksi tiedostossa `palautus.csv` on tehtävien palautusaikoja muodossa `tunnus;tehtävä;pisteet;hh:mm`. Esimerkiksi:

```csv
jarmo;1;8;16:05
timo;2;10;21:22
jarmo;2;10;19:15
jne...
```

Tehtäväsi on etsiä ne opiskelijat, jotka ovat käyttäneet tenttiin yli 3 tuntia aikaa, eli opiskelijat, joiden _jonkin_ tehtävän palautus on tehty yli 3 tuntia tentin aloitusajasta. Palautuksia voi siis olla useampi. Voit olettaa, että kaikki ajat ovat saman vuorokauden puolella.

Kirjoita funktio `huijarit()`, joka palauttaa listan huijanneiden opiskelijoiden käyttäjätunnuksista.

</programming-exercise>

<programming-exercise name='Kuka huijasi, versio 2' tmcname='osa07-15_kuka_huijasi_2'>

Käytössäsi on edellisessä tehtävässä määritellyt datatiedostot. Kirjoita funktio `viralliset_pisteet()`, joka palauttaa sanakirjassa (dict) opiskelijoiden koepisteet seuraavien sääntöjen mukaan:

* Jos samaan tehtävänumeroon on tehty useita palautuksia, korkeimman pistemäärän palautus otetaan huomioon
* Jos tehtäväpalautus on tehty yli 3 tuntia tentin aloittamisen jälkeen, palautusta ei huomioida ollenkaan

Tehtävät on numeroitu 1–8 ja jokaisesta tehtävästä voi saada 0–6 pistettä.

Palautetussa sanakirjassa tunnus on avain ja tehtävien yhteispistemäärä arvo.

Vinkki: sisäkkäiset sanakirjat (dict) ovat mainio työkalua tallennettaessa eri opiskelijoiden pisteitä ja aikoja.

</programming-exercise>

## Hitta moduler

Pythons officiella dokumentation innehåller information om alla moduler som är tillgängliga i standardbiblioteket:

* https://docs.python.org/3/library/

Förutom standardbiblioteket är internet fullproppat med andra Python-moduler för olika ändamål. Några vanliga moduler listas på den här sidan:

* https://wiki.python.org/moin/UsefulModules

<programming-exercise name='Spellchecker, versio 2' tmcname='osa07-16_spellchecker_versio2'>

Teemme tässä tehtävässä hieman parannellun version edellisen osan tehtävästä Spellchecker.

Edellisen osan version tapaan ohjelma pyytää käyttäjää kirjoittamaan rivin englanninkielistä tekstiä. Ohjelma suorittaa tekstille oikeinkirjoitustarkistuksen ja tulostaa saman tekstin siten, että kaikki väärin kirjoitetut sanat on ympäröity tähdillä. _Tämän lisäksi ohjelma antaa listan korjausehdotuksia väärin kirjotettuihin sanoihin._

Seuraavassa kaksi käyttöesimerkkiä:

<sample-output>

write text: **We use ptython to make a spell checker**
<pre>
We use *ptython* to make a spell checker
korjausehdotukset:
ptython: python, pythons, typhon
</pre>

</sample-output>

<sample-output>

write text: **this is acually a good and usefull program**
<pre>
this is *acually* a good and *usefull* program
korjausehdotukset:
acually: actually, tactually, factually
usefull: usefully, useful, museful
</pre>

</sample-output>

Korjausehdotukset etsitään standardikirjaston moduulin [difflib](https://docs.python.org/3/library/difflib.html) tarjoaman funktion [get\_close\_matches](https://docs.python.org/3/library/difflib.html#difflib.get_close_matches) avulla.

*Huom*: jotta testit toimisivat, käytä funktiota "oletusasetuksilla", eli antamalla sille kaksi parametria: virheellinen sana ja lista oikeista sanoista.

</programming-exercise>

<quiz id="84313649-9311-51a5-a46d-71802083cede"></quiz>
