---
path: '/osa-7/4-behandla-data'
title: 'Behandla data'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* kan du använda en modul för att behandla CSV-filer
* kan du använda en modul för att behandla JSON-filer
* kan du komma åt filer från internet och läsa dem.

</text-box>

## Läsa CSV-filer

CSV är ett så enkelt format att vi tills vidare har behandlat dessa filer med självskriven kod. Det finns däremot en färdig modul för CSV-filer i Pythons standardbibliotek: [`csv`](https://docs.python.org/3/library/csv.html). Modulen fungerar så här:

```python
import csv

with open("test.csv") as fil:
    for rad in csv.reader(fil, delimiter=";"):
        print(rad)
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

CSV är bara ett maskinläsbart dataformat. [JSON](https://www.json.org/json-sv.html) är ett annat sådant format och det används ofta när data överförs mellan olika program.

JSON-filer är textfiler som följer en strikt syntax, som eventuellt är lite mindre människovänligt än CSV-formatet. Följande exempel använder filen `kurser.json`, som innehåller information om några kurser:

```x
[
    {
        "namn": "Introkurs i programmering",
        "id": "Ohpe",
        "perioder": [1, 3]
    },
    {
        "namn": "Fortsättningskurs i programmering",
        "id": "Ohja",
        "perioder": [2, 4]
    },
    {
        "namn": "Databasapplikation",
        "id": "Tsoha",
        "perioder": [1, 2, 3, 4]
    }
]
```


Strukturen hos en JSON-fil kanske ser bekant ut. JSON-filen ser ut som en Python-lista som innehåller tre Python-lexikon.

Standardbiblioteket innehåller [`json`-modulen](https://docs.python.org/3/library/json.html) som kan användas för att behandla JSON-filer. Funktionen `loads` tar emot ett argument som innehåller data i JSON-format och konverterar den till Pythons egen datastruktur. När vi använder `kurser.json` i koden nedan…

```python
import json

with open("kurser.json") as fil:
    data = fil.read()
kurser = json.loads(data)
print(kurser)
```

…får vi följande utskrift:

<sample-output>

[{'namn': 'Introkurs i programmering', 'id': 'Ohpe', 'perioder': [1, 3]}, {'namn': 'Fortsättningskurs i programmering', 'id': 'Ohja', 'perioder': [2, 4]}, {'namn': 'Databasapplikation', 'id': 'Tsoha', 'perioder': [1, 2, 3, 4]}]

</sample-output>

Om vi vill skriva ut namnet på varje kurs kan vi använda en for-loop:

```python
for kurs in kurser:
    print(kurs["namn"])
```

<sample-output>

Introkurs i programmering
Fortsättningskurs i programmering
Databasapplikation

</sample-output>

<programming-exercise name='JSON-fil' tmcname='osa07-12_jsontiedostot'>

Vi inspekterar en JSON-fil med innehåll om studerande i följande format:

```json
[
    {
        "namn": "Piritta Pythonist",
        "alder": 27,
        "hobbyer": [
            "att koda",
            "att virka"
        ]
    },
    {
        "namn": "Jessica Javalig",
        "alder": 24,
        "hobbyer": [
            "att koda",
            "bergsklättring",
            "att läsa"
        ]
    }
]
```

Skapa funktionen `skriv_ut_personer(fil: str)` som läser en JSON-fil enligt formatet ovan och skriver ut informationen så här:

<sample-output>

Piritta Pythonist 27 år (att koda, att virka)
Jessica Javalig 24 år (att koda, bergsklättring, att läsa)

</sample-output>

Hobbyerna ska vara i samma ordning som i JSON-filen.

</programming-exercise>

## Hämta en fil från internet

Standardbiblioteket i Python innehåller också moduler som kan användas för att hantera innehåll på internet. En nyttig funktion är [`urllib.request.urlopen`](https://docs.python.org/3/library/urllib.request.html#urllib.request.urlopen). Det lönar sig att bekanta sig med modulen som helhet, men följande exempel borde räcka till för att få en insikt i hur funktionen fungerar. Den kan användas för att hämta data från internet, för vidare behandling i ditt program.

Följande kodstunn skriver ut innehållet från huvudsidan för Helsingfors universitet:

```python
import urllib.request

begaran = urllib.request.urlopen("https://helsinki.fi")
print(begaran.read())
```

Sidor som är skräddarsydda för människoögon ser inte vanligtvis trevliga ut när deras kod skrivs ut. I de kommande exemplen kommer vi däremot att läsa in data i maskinformat från internet. En stor del maskinläsbara data på internet är i JSON-format.

<programming-exercise name='Kursstatistik' tmcname='osa07-13_kurssistatistiikka'>

#### Info om kurser

På adressen <https://studies.cs.helsinki.fi/stats-mock/api/courses> finns det info om några nätkurser i JSON-format.

Skapa funktionen `hamta_alla()` som hämtar och returnerar de aktiva kursernas (fältet `enabled` har värdet `True`) info som en lista med tupler enligt följande exempel:

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

Alla tupler innehåller alltså

* kursens namn (`fullName`)
* kort namn (`name`)
* år (`year`)
* totalt antal övningar (`exercises`).

Obs! Du måste använda funktionen `urllib.request.urlopen`.

Obs! Hårdkoda inte data, testerna kommer att avslöja sådana försök!!

Obs! En del Mac-användare har stött på följande problem:

```sh
File "/Library/Frameworks/Python.framework/Versions/3.8/lib/python3.8/urllib/request.py", line 1353, in do_open
    raise URLError(err)
urllib.error.URLError: <urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: unable to get local issuer certificate (_ssl.c:1124)>
```

Lösningen beror på hur Python är installerat på datorn. I vissa fall fungerar:

```sh
cd "/Applications/Python 3.8/"
sudo "./Install Certificates.command
```

Sökvägen i `cd`-kommandot beror på din Python-version.

[Här](https://stackoverflow.com/q/27835619) hittar du flera möjliga lösningar.

Du kan testa på följande:

```python
import urllib.request
import json
import ssl # lägg till det här

def hamta_alla():
    # och det här i början av funktioner
    context = ssl._create_unverified_context()
    # övrig kod
```

Ett annat sätt att komma runt problemet:

 ```python
import urllib.request
import certifi # lägg till det här
import json

def hamta_alla():
    adress = "https://studies.cs.helsinki.fi/stats-mock/api/courses"
    # lägger till ett andra argument
    begaran = urllib.request.urlopen(adress, cafile=certifi.where())
    # övrig kod
```

#### Info om en kurs

För varje kurs finns uppgiftsstatistik på adressen <https://studies.cs.helsinki.fi/stats-mock/api/courses/****/stats> – ersätt asteriskerna med kursens korta namn (`name`).

T.ex. statistik för kursen `docker2019` finns på <https://studies.cs.helsinki.fi/stats-mock/api/courses/docker2019/stats>.

Skapa funktionen `hamta_kurs(kurs: str)` som hämtar statistik för den valda kursen.

När vi anropar `hamta_kurs("docker2019")` returnerar funktionen ett lexikon med följande innehåll:

<sample-output>

<pre>
{
    'veckor': 4,
    'studerande': 220,
    'timmar': 5966,
    'timmar_genomsnitt': 27,
    'uppgifter': 4988,
    'uppgifter_genomsnitt': 22
}
</pre>

</sample-output>

Värdena bestäms enligt följande:

- `veckor`: antal JSON-element som representerar en kurs
- `studerande`: maxantal studerande under veckorna
- `timmar`: summan av alla veckornas timantal (`hour_total`)
- `timmar_genomsnitt`: föregående dividerat med antal studerande (heltal, avrundas nedåt)
- `uppgifter`: alla veckors uppgiftsantal (`exercise_total`) summerat
- `uppgifter_genomsnitt`: föregående dividerat med antal studerande (heltal, avrundas nedåt)

Obs! Alla `Obs!` ovan gäller också här.

Obs! I [`math`-modulen](https://docs.python.org/3/library/math.html) hittar du en funktion som gör det lätt att avrunda nedåt.

</programming-exercise>

<programming-exercise name='Vem lurade' tmcname='osa07-14_kuka_huijasi'>

I filen `start.csv` finns starttider för tentor i formatet `id;hh:mm`:

```csv
jarmo;09:00
timo;18:42
kalle;13:23
```

I filen `returnering.csv` finns returneringstiden för uppgifter i formatet `id;uppgift;poäng;hh:mm`:

```csv
jarmo;1;8;16:05
timo;2;10;21:22
jarmo;2;10;19:15
o.s.v. ...
```

Din uppgift är att hitta de studerande som använt över tre timmar för att göra sin tenta, dvs. någon av uppgifterna har lämnats in över tre timmar sedan tentan inleddes. Det kan alltså finnas flera inlämningar. Du kan anta att alla klockslag är under samma dygn.

Skapa funktionen `fuskare()` som returnerar en lista över fuskarnas id:n.

</programming-exercise>

<programming-exercise name='Vem lurade, andra versionen' tmcname='osa07-15_kuka_huijasi_2'>

Du har till ditt förfogande de filer som presenterades i den förra uppgiften. Skapa funktionen `officiella_poang()`, som returnerar studerandenas provpoäng i ett lexikon enligt följande regler:

* om samma uppgift har flera inlämningar, tas inlämningen med högsta poäng i beaktande
* om en inlämning gjorts över tre timmar efter att tentan inletts, ska inlämningen inte tas i beaktande.

Uppgifterna är numrerade 1-8 och för varje uppgift kan man få 0-6 poäng.

I lexikonet är nyckeln id:t och värdet totalpoängen.

Tips: Du kan lagra lexikon inuti lexikon, vilket kan vara till nytta då du lagrar poängantal och tider för olika studerande.

</programming-exercise>

## Hitta moduler

Pythons officiella dokumentation innehåller information om alla moduler som är tillgängliga i standardbiblioteket:

* https://docs.python.org/3/library/

Förutom standardbiblioteket är internet fullproppat med andra Python-moduler för olika ändamål. Några vanliga moduler listas på den här sidan:

* https://wiki.python.org/moin/UsefulModules

<programming-exercise name='Spell checker, andra versionen' tmcname='osa07-16_spellchecker_versio2'>

I den här uppgiften förbättrar vi lite vårt språkkontrollverktyg.

Som i den förra versionen ska programmet be användaren ange text på engelska. Programmet utför språkkontroll och markerar felstavade ord. Dessutom ska programmet nu föreslå lösningar på skrivfelen.

Två exempel:

<sample-output>

write text: **We use ptython to make a spell checker**
<pre>
We use *ptython* to make a spell checker
förslag:
ptython: python, pythons, typhon
</pre>

</sample-output>

<sample-output>

write text: **this is acually a good and usefull program**
<pre>
this is *acually* a good and *usefull* program
förslag:
acually: actually, tactually, factually
usefull: usefully, useful, museful
</pre>

</sample-output>

Korrigeringsförslagen söks med hjälp av [modulen `difflib`](https://docs.python.org/3/library/difflib.html) i standardbiblioteket: använd funktionen [`get_close_matches`](https://docs.python.org/3/library/difflib.html#difflib.get_close_matches).

Obs! För att testen ska fungera ska du använda funktionen med dess förinställda val – ge alltså bara två argument: felaktiga ordet och listan med korrekta ord.

</programming-exercise>

<quiz id="84313649-9311-51a5-a46d-71802083cede"></quiz>
