---
path: '/osa-12/1-funktioner-som-argument'
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
produkter = [("banan", 5.95), ("äppel", 3.95), ("apelsin", 4.50), ("vattenmelon", 4.95)]

produkter.sort()

for produkt in produkter:
    print(produkt)
```

<sample-output>

('apelsin', 4.5)
('banan', 5.95)
('vattenmelon', 4.95)
('äppel', 3.95)

</sample-output>

Men vad händer om vi vill sortera listan baserat på priset?

## Funktioner som argument

En sorteringsmetod eller -funktion accepterar vanligtvis ett valfritt andra argument som gör att du kan kringgå standardsorteringskriterierna. Detta andra argument är en funktion som definierar hur värdet på varje föremål i listan bestäms. När listan sorteras anropar Python denna funktion när den jämför föremålen med varandra.

Låt oss ta en titt på ett exempel:

```python
def prisordning(foremal: tuple):
    # Returnerar tupelns andra föremål, alltså priset
    return foremal[1]

if __name__ == "__main__":
    produkter = [("banan", 5.95), ("äppel", 3.95), ("apelsin", 4.50), ("vattenmelon", 4.95)]

    # Använd funktionen prisordning för sortering
    produkter.sort(key=prisordning)

    for produkt in produkter:
        print(produkt)
```

<sample-output>

('äppel', 3.95)
('apelsin', 4.5)
('vattenmelon', 4.95)
('banan', 5.95)

</sample-output>

Nu är listan sorterad utifrån artiklarnas priser, men vad händer egentligen i programmet?

Funktionen `prisordning` är faktiskt ganska enkel. Den tar ett objekt som sitt argument och returnerar ett värde för det objektet. Mer specifikt returnerar den det andra objektet i tupeln, som representerar priset. Men sedan har vi den här kodraden, där `sort`-metoden anropas:

`produkter.sort(key=prisordning)`

Här anropas `sort`-metoden med en funktion som argument. Detta är inte en referens till funktionens returvärde, utan en referens till själva funktionen. `Sort`-metoden anropar denna funktion flera gånger och använder varje objekt i listan som argument i tur och ordning.

Om vi inkluderar en extra print-sats i funktionsdefinitionen för `prisordning` kan vi verifiera att funktionen verkligen anropas en gång för varje objekt i listan:

```python
def prisordning(foremal: tuple):
    # Skriver ut föremålet
    print(f"Anropade prisordning({foremal})")

    # Returnerar tupelns andra föremål, alltså priset
    return foremal[1]


produkter = [("banan", 5.95), ("äppel", 3.95), ("apelsin", 4.50), ("vattenmelon", 4.95)]

# Använd funktionen prisordning för sortering
produkter.sort(key=prisordning)

for produkt in produkter:
    print(produkt)
```

<sample-output>

Anropade prisordning(('banan', 5.95))
Anropade prisordning(('äppel', 3.95))
Anropade prisordning(('apelsin', 4.5))
Anropade prisordning(('vattenmelon', 4.95))
('äppel', 3.95)
('apelsin', 4.5)
('vattenmelon', 4.95)
('banan', 5.95)

</sample-output>

Ordningen kan vändas med ett annat nyckelordsargument; `reverse`, som är tillgängligt med både `sort`-metoden och funktionen `sorted`:

```python
produkter.sort(key=prisordning, reverse=True)

t2 = sorted(produkter, key=prisordning, reverse=True)
```

## En funktionsdefinition inom en funktionsdefinition

Vi kan också inkludera en namngiven funktion för den nya prisbaserade sorteringsfunktionen som vi har skapat. Låt oss lägga till en funktion med namnet `sortera_enligt_pris`:

```python
def prisordning(foremal: tuple):
    return foremal[1]

def sortera_enligt_pris(foremalen: list):
    # Använd funktionen prisordning här
    return sorted(foremalen, key=prisordning)

produkter = [("banan", 5.95), ("äppel", 3.95), ("apelsin", 4.50), ("vattenmelon", 4.95)]

for produkt in sortera_enligt_pris(produkter):
    print(produkt)
```

Om vi vet att hjälpfunktionen `prisordning` inte används någonstans utanför funktionen `sortera_enligt_pris`, kan vi placera den första funktionsdefinitionen inom den senare:

```python
def sortera_enligt_pris(foremalen: list):
    # hjälpfunktion definierad inom funktionen
    def prisordning(foremal: tuple):
        return foremal[1]

    return sorted(foremalen, key=prisordning)
```

<programming-exercise name='Sortering enligt återstående lager' tmcname='osa12-01_aterstaende_lager'>

Skapa en funktion med namnet `sortera_enligt_aterstaende_lager(foremal: list)`. Funktionen tar en lista med tupler som sitt argument. Tuplerna består av namn, pris och återstående lager för en produkt. Funktionen ska returnera en ny lista, där artiklarna är sorterade enligt återstående lager, med det lägsta värdet först. Den ursprungliga listan ska inte ändras.

Funktionen ska fungera på följande sätt:

```python
produkter = [("banan", 5.95, 12), ("äppel", 3.95, 3), ("apelsin", 4.50, 2), ("vattenmelon", 4.95, 22)]

for produkt in sortera_enligt_aterstaende_lager(produkter):
    print(f"{produkt[0]} {produkt[2]} st")
```

<sample-output>
apelsin 2 st
äppel 3 st
banan 12 st
vattenmelon 22 st
</sample-output>

</programming-exercise>

<programming-exercise name='Sortering enligt produktionssäsonger' tmcname='osa12-02_produktionssasong'>

Skapa en funktion med namnet `sortera_enligt_sasonger(foremal: list)` som tar en lista med ordlistor som sitt argument. Varje ordlista innehåller information om ett enda TV-program. Funktionen ska sortera listan efter antalet säsonger som varje program har, i stigande ordning. Funktionen ska inte ändra den ursprungliga listan, utan istället returnera en ny lista.

Funktionen ska fungera på följande sätt:

```python
serier = [{ "namn": "Dexter", "betyg" : 8.6, "säsonger":9 }, { "namn": "Friends", "betyg" : 8.9, "säsonger":10 },  { "namn": "Simpsons", "betyg" : 8.7, "säsonger":32 }  ]

for serie in sortera_enligt_sasonger(serier):
    print(f"{serie['namn']}  {serie['säsonger']} säsonger")
```

<sample-output>
Dexter 9 säsonger
Friends 10 säsonger
Simpsons 32 säsonger
</sample-output>

</programming-exercise>

<programming-exercise name='Sortering enligt poäng' tmcname='osa12-03_enligt_poang'>

Skapa en funktion med namnet `sortera_enligt_betyg(foremal: list)` som tar en lista med ordlistor som sitt argument. Ordlistornas struktur är identisk med den i den föregående övningen. Denna funktion ska sortera ordlistorna i fallande ordning baserat på programmens betyg. Funktionen ska inte ändra den ursprungliga listan, utan returnera en ny lista istället.

```python
serier = [{ "namn": "Dexter", "betyg" : 8.6, "säsonger":9 }, { "namn": "Friends", "betyg" : 8.9, "säsonger":10 },  { "namn": "Simpsons", "betyg" : 8.7, "säsonger":32 }  ]

print("Betygsättning enligt IMDB")
for serie in sortera_enligt_betyg(serier):
    print(f"{serie['namn']}  {serie['betyg']}")
```

<sample-output>
Betygsättning enligt IMDB
Friends 8.9
Simpsons 8.7
Dexter 8.6
</sample-output>

</programming-exercise>

## Sortering av samlingar av egna objekt

Låt oss med samma princip skriva ett program som sorterar en lista med objekt från vår egen klass `Studerande` på två olika sätt:

```python
class Studerande:
    """ Klassen modellerar en enkel studerande """
    def __init__(self, namn: str, id: str, poang: int):
        self.namn = namn
        self.id = id
        self.poang = poang

    def __str__(self):
        return f"{self.namn} ({self.id}), {self.poang} sp."


def enligt_id(foremal: Studerande):
    return foremal.id

def enligt_poang(foremal: Studerande):
    return foremal.poang


if __name__ == "__main__":
    s1 = Studerande("Anton", "a123", 220)
    s2 = Studerande("Maja", "m321", 210)
    s3 = Studerande("Anna", "a999", 131)

    studeranden = [s1, s2, s3]

    print("Enligt id:")
    for studerande in sorted(studeranden, key=enligt_id):
        print(studerande)

    print()

    print("Enligt poäng:")
    for studerande in sorted(studeranden, key=enligt_poang):
        print(studerande)
```

<sample-output>

Enligt id:
Anton (a123), 220 sp.
Anna (a999), 131 sp.
Maja (m321), 210 sp.

Enligt poäng:
Anna (a999), 131 sp.
Maja (m321), 210 sp.
Anton (a123), 220 sp.

</sample-output>

Som du kan se ovan fungerar sortering efter olika kriterier precis som det är tänkt. Om funktionerna `enligt_id` och `enligt_studiepoang` inte behövs någon annanstans finns det sätt att göra implementeringen enklare. Vi återkommer till detta ämne efter dessa övningar.

<programming-exercise name='Klättringsrutt' tmcname='osa12-04_klattringsrutt'>

Uppgiftsbottnet innehåller en klassdefinition för `Klattringsrutt`, som fungerar enligt följande:

```python
rutt1 = Klattringsrutt("Kantti", 38, "6A+")
rutt2 = Klattringsrutt("Smooth operator", 11, "7A")
rutt3 = Klattringsrutt("Syncro", 14, "8C+")


print(rutt1)
print(rutt2)
print(rutt3.namn, rutt3.langd, rutt3.grade)
```

<sample-output>

Kantti, längd 38 meter, grade 6A+
Smooth operator, längd 11 meter, grade 7A
Syncro 14 8C+

</sample-output>

## Sortera enligt längd

Skapa funktionen `enligt_langd(rutter: list)`, som returnerar en ny lista av rutter sorterade enligt längd från längsta till kortaste.

Funktionen ska fungera enligt följande:

```python
r1 = Klattringsrutt("Kantti", 38, "6A+")
r2 = Klattringsrutt("Smooth operator", 11, "7A")
r3 = Klattringsrutt("Syncro", 14, "8C+")
r4 = Klattringsrutt("Små steg", 12, "6A+")

rutter = [r1, r2, r3, r4]

for rutt in enligt_langd(rutter):
    print(rutt)
```

<sample-output>

Kantti, längd 38 meter, grade 6A+
Syncro, längd 14 meter, grade 8C+
Små steg, längd 12 meter, grade 6A+
Smooth operator, längd 11 meter, grade 7A

</sample-output>

## Sortera enligt svårighetsgrad

Skapa funktionen `enligt_svarighet(rutter: list)`, som returnerar en ny lista av rutter sorterade enligt svårighet från svåraste till lättaste. För rutter med samma svårighet är den längre svårare. Skalan för svårighet är _4, 4+, 5, 5+, 6A, 6A+, ..._ som i praktiken fungerar enligt alfabetiska ordningen för strängar.

Funktionen ska fungera enligt följande:

```python
r1 = Klattringsrutt("Kantti", 38, "6A+")
r2 = Klattringsrutt("Smooth operator", 11, "7A")
r3 = Klattringsrutt("Syncro", 14, "8C+")
r4 = Klattringsrutt("Små steg", 12, "6A+")

rutter = [r1, r2, r3, r4]
for rutt in enligt_svarighet(rutter):
    print(rutt)
```

<sample-output>

Syncro, längd 14 meter, grade 8C+
Smooth operator, längd 11 meter, grade 7A
Kantti, längd 38 meter, grade 6A+
Små steg, längd 12 meter, grade 6A+

</sample-output>

**Tips:** Ifall ordningen är baserad på en lista eller tupel, sorterar Python föremål per standard baserat på första föremålet, sedan baserat på det andra och så vidare:

```python
lista = [("a", 4),("a", 2),("b", 30), ("b", 0) ]
print(sorted(lista))
```

<sample-output>

[('a', 2), ('a', 4), ('b', 0), ('b', 30)]

</sample-output>

</programming-exercise>

<programming-exercise name='Klättringsområde' tmcname='osa12-05_klattringsomrade/'>

I uppgiftsbotten finns förutom klassen `Klattringsrutt` dessutom klassen `Klattringsomrade`.

```python
o1 = Klattringsomrade("Olhava")
o1.tillsatt_rutt(Klattringsrutt("Kantti", 38, "6A+"))
o1.tillsatt_rutt(Klattringsrutt("Stora snittet", 36, "6B"))
o1.tillsatt_rutt(Klattringsrutt("Svensk rutt", 42, "5+"))

o2 = Klattringsomrade("Nummi")
o2.tillsatt_rutt(Klattringsrutt("Syncro", 14, "8C+"))

o3 = Klattringsomrade("Nalkkilan släbi")
o3.tillsatt_rutt(Klattringsrutt("Små steg", 12, "6A+"))
o3.tillsatt_rutt(Klattringsrutt("Smooth operator", 11, "7A"))
o3.tillsatt_rutt(Klattringsrutt("Grisen gillar inte", 12 , "6B+"))
o3.tillsatt_rutt(Klattringsrutt("Fruktträdgård", 8, "6A"))

print(o1)
print(o3.namn, o3.rutter())
print(o3.svaraste_rutt())
```

<sample-output>

Olhava, 3 rutter, svåraste 6B
Nalkkilan släbi 4
Smooth operator, längd 9 meter, grade 7A

</sample-output>

## Sortera enligt antalet rutter

Skapa funktionen `enligt_antal_rutter`, som sorterar klättringsområdena enligt antalet rutter de har i ökande ordning.

```python
# o1, o2 och o3 definierade enligt ovan
omraden = [o1, o2, o3]
for omrade in enligt_antal_rutter(omraden):
    print(omrade)

```

<sample-output>

Nummi, 1 rutter, svåraste 8C+
Olhava, 3 rutter, svåraste 6B
Nalkkilan slabi, 4 rutter, svåraste 7A

</sample-output>

## Sortera enligt svåraste rutt

Skapa funktionen `enligt_svaraste_rutt`, som sorterar klättringsområdena enligt högsta svårighetsgraden de har i _minskande_ ordning.

```python
# o1, o2 och o3 definierade enligt ovan
omraden = [o1, o2, o3]
for omrade in enligt_svaraste_rutt(omraden):
    print(omrade)

```

<sample-output>

Nummi, 1 rutter, svåraste 8C+
Nalkkilan slabi, 4 rutter, svåraste 7A
Olhava, 3 rutter, svåraste 6B

</sample-output>

</programming-exercise>

## Lambda-uttryck

Vi har mest arbetat med funktioner ur modularitetssynpunkt. Det är sant att funktioner spelar en viktig roll när det gäller att hantera komplexiteten i dina program och undvika upprepning av kod. Funktioner skrivs vanligtvis så att de kan användas många gånger.

Men ibland behöver man något som liknar en funktion som man bara använder en gång. Med lambda-uttryck kan du skapa små, anonyma funktioner som skapas (och kasseras) när de behövs i koden. Den allmänna syntaxen är som följer:

`lambda <parametrar> : <uttryck>`

Att sortera en lista med tupler efter det andra objektet i varje tupel skulle se ut så här implementerat med ett lambda-uttryck:

```python
produkter = [("banan", 5.95), ("äppel", 3.95), ("apelsin", 4.50), ("vattenmelon", 4.95)]

# Funktionen skapas "i farten" med ett lambda-uttryck:
produkter.sort(key=lambda foremal: foremal[1])

for produkt in produkter:
    print(produkt)
```

<sample-output>

('äppel', 3.95)
('apelsin', 4.5)
('vattenmelon', 4.95)
('banan', 5.95)

</sample-output>

Uttrycket

`lambda föremål: föremål[1]`

Är ekvivalent med funktionsdefinitionen

```python

def pris(foremal):
    return foremal[1]
```

förutom det faktum att en lambdafunktion inte har något namn. Det är därför lambda-funktioner kallas anonyma funktioner.

I alla andra avseenden skiljer sig inte en lambda-funktion från någon annan funktion, och de kan användas i alla samma sammanhang som en motsvarande namngiven funktion. Följande program sorterar till exempel en lista med strängar i alfabetisk ordning enligt det sista tecknet i varje sträng:

```python
strangar = ["Mikael", "Makke", "Maja", "Markus", "Minna"]

for strang in sorted(strangar, key=lambda strang: strang[-1]):
    print(strang)
```

<sample-output>

Maja
Minna
Makke
Mikael
Markus

</sample-output>

Vi kan också kombinera list comprehensions, `join`-metoden och lambda-uttryck. Vi kan till exempel sortera strängar baserat på enbart vokalerna i dem och ignorera alla andra tecken:

```python
strangar = ["Mikael", "Makke", "Maja", "Markus", "Minna"]

for strang in sorted(strangar, key=lambda strang: "".join([m for m in strang if m in "aeiouyäö"])):
    print(strang)
```

<sample-output>

Maja
Makke
Markus
Minna
Mikael

</sample-output>

Anonyma funktioner kan också användas med andra inbyggda Python-funktioner, inte bara de som används för sortering. Till exempel tar funktionerna `min` och `max` också ett nyckelordsargument som heter `key`. Det används som kriterium för att jämföra objekten när det lägsta eller högsta värdet väljs.

I följande exempel handlar det om ljudinspelningar. Först väljer vi den äldsta inspelningen och sedan den längsta:

```python

class Skiva:
    """ Klassen modellerar en enkel skiva """
    def __init__(self, namn: str, artist: str, ar: int, langd: int):
        self.namn = namn
        self.artist = artist
        self.ar = ar
        self.langd = langd


    def __str__(self):
        return f"{self.namn} ({self.artist}), {self.ar}. {self.langd} min."

if __name__ == "__main__":
    l1 = Skiva("Nevermind", "Nirvana", 1991, 43)
    l2 = Skiva("Let It Be", "Beatles", 1969, 35)
    l3 = Skiva("Joshua Tree", "U2", 1986, 50)

    skivor = [l1, l2, l3]


    print("Äldsta skiva:")
    print(min(skivor, key=lambda skiva: skiva.ar))

    print("Längsta skiva: ")
    print(max(skivor, key=lambda skiva: skiva.langd))
```

<sample-output>

Äldsta skiva:
Let It Be (Beatles), 1969. 35 min.
Längsta skiva:
U2 (Joshua Tree), 1986. 50 min.

</sample-output>

<programming-exercise name='Bollspelare' tmcname='osa12-06_bollspelare'>

Uppgiftsbotten innehåller en definition för en klass med namnet `Bollspelare`, som har följande offentliga attribut:

* namn
* spelnummer
* mängden gjorda mål `mal`
* mängden målpassningar `malpassningar`
* minuter spelade `minuter`

Implementera följande funktioner. OBS: varje funktion har olika typer av returvärden.

## Flest mål

Skapa funktionen `flest_mal`, som får bollspelare som argument.

Funktionen ska returnera namnet av spelaren som gjort flest mål, i strängformat.

## Flest poäng

Skapa funktionen `flest_poang`, som får en bollspelare som argument.

Funktionen ska returnera en tupel som innehåller namnet och skjortnumret av spelaren som fått flest poäng. Den totala mängden av poäng är antalet mål och antalet målpassningar ihopslaget.

## Minst minuter

Skapa funktionen `minst_minuter`, som får en bollspelare som argument.

Funktionen ska returnera `Bollspelare`-objektet som har den minsta mängden minuter spelade.

## Testprogram

Du kan testa dina funktioner med följande program:

```python
if __name__ == "__main__":
    spelare1 = Bollspelare("Kalle Ankka", 13, 5, 12, 46)
    spelare2 = Bollspelare("Långben", 7, 2, 26, 55)
    spelare3 = Bollspelare("Musse Pigg", 9, 1, 32, 26)
    spelare4 = Bollspelare("Peter Pan", 12, 1, 11, 41)
    spelare5 = Bollspelare("Nalle Puh", 4, 3, 9, 12)

    lag = [spelare1, spelare2, spelare3, spelare4, spelare5]
    print(flest_mal(lag))
    print(flest_poang(lag))
    print(minst_minuter(lag))
```

Detta ska skriva ut:

<sample-output>

Kalle Ankka
('Musse Pigg', 9)
Bollspelare(namn=Nalle Puh, spelnummer=4, mål=3, målpassningar=9, minuter=12)

</sample-output>

</programming-exercise>

## Funktioner som argument inom egna funktioner

Vi konstaterade ovan att det är möjligt att skicka en referens till en funktion som argument till en annan funktion. Som avslutning på detta avsnitt skriver vi en egen funktion som tar en funktion som argument.

```python
# typledtråden callable refererar till en funktion
def utfor_operation(operation: callable):
    # Anropa funktionen som passerades som argument
    return operation(10, 5)

def summa(a: int, b: int):
    return a + b

def produkt(a: int, b: int):
    return a * b


if __name__ == "__main__":
    print(utfor_operation(summa))
    print(utfor_operation(produkt))
    print(utfor_operation(lambda x,y: x - y))

```

<sample-output>

15
50
5

</sample-output>

Det värde som returneras av funktionen `utfor_operation` beror på vilken funktion som skickades som argument. Vilken funktion som helst som tar emot två argument skulle duga, oavsett om den är anonym eller namngiven.

Att skicka referenser till funktioner som argument till andra funktioner är kanske inte något som du kommer att göra dagligen under din programmeringskarriär, men det kan vara en användbar teknik. Följande program väljer ut några rader från en fil och skriver dem till en annan fil. Hur raderna väljs ut bestäms av en funktion som returnerar True endast om raderna ska kopieras:

```python
def kopiera_rader(kalla_namn: str, mal_namn: str, kriterie= lambda x: True):
    with open(kalla_namn) as kalla, open(mal_namn, "w") as mal:
        for rad in kalla:
            # Ta bort all tomrum från början och slutet av raden
            rad = rad.strip()

            if kriterie(rad):
                mal.write(rad + "\n")

# Exempel
if __name__ == "__main__":
    # Ifall tredje parametern inte är angiven, kopiera alla rader
    kopiera_rader("första.txt", "andra.txt")

    # Kopiera alla icke-tomma rader
    kopiera_rader("första.txt", "andra.txt", lambda rad: len(rad) > 0)

    # Kopierar alla rader som innehåller ordet "Python"
    kopiera_rader("första.txt", "andra.txt", lambda rad: "Python" in rad)

    # Kopierar alla rader som inte slutar med en punkt
    kopiera_rader("första.txt", "andra.txt", lambda rad: rad[-1] != ".")
```

Funktionsdefinitionen innehåller ett standardvärde för nyckelordsparametern `kriterie`: `lambda x: True`. Denna anonyma funktion returnerar alltid `True` oavsett indata. Standardbeteendet är alltså att kopiera alla rader. Som vanligt gäller att om ett värde anges för en parameter med ett standardvärde, ersätter det nya värdet standardvärdet.

<programming-exercise name='Söking av produkter' tmcname='osa12-07_sokning_av_produkter'>

Den här övningen hanterar produkter som förvaras som tupler. Exemplen antar en variabel med namnet `produkter` som förses med följande värde:

```python
produkter = [("banan", 5.95, 12), ("äppel", 3.95, 3), ("apelsin", 4.50, 2), ("vattenmelon", 4.95, 22), ("kål", 0.99, 1)]
```

Varje tupel innehåller tre föremål: namn, pris och antal.

Skapa funktionen `sok(produkter: list, kriterie: callable)`. Det andra argumentet till funktionen är en funktion i sig, och den ska kunna bearbeta en tupel enligt definitionen ovan och returnera ett booleskt värde. Sökfunktionen ska returnera en ny lista som innehåller de tupler från originalet som uppfyller kriteriet.

Ett passande kriterie kunde exempelvis vara följande:

```python
def pris_under_4(produkt):
    return produkt[1] < 4
```

Funktionen returnerar alltså _True_ ifall produktens pris, tupelns andra föremål, är mindre än 4.

Funktionen `sok` fungerar enligt följande:

```python
for produkt in sok(produkter, pris_under_4):
    print(produkt)
```

<sample-output>

('äppel', 3.95, 3)
('kål', 0.99, 1)

</sample-output>

Kriteriefunktionen kan också vara en lambda-funktion. Om vi bara ville söka efter de produkter vars belopp är minst 11, skulle vi kunna skapa följande:

```python
for produkt in sok(produkter, lambda t: t[2]>10):
    print(produkt)
```

<sample-output>

('banan', 5.95, 12)
('vattenmelon', 4.95, 22)

</sample-output>

</programming-exercise>
