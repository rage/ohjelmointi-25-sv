---
path: '/osa-8/1-objekt-och-metoder'
title: 'Objekt och metoder'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Kommer du veta vad ett objekt är i programmering
- Kommer du förstå vad som menas med oberoende hos individuella objekt
- Kommer du kunna skapa och komma åt objekt

</text-box>

Detta är första delen av fortsättningskursen i programmering. Materialet är designat för att användas med programmeringsmiljön Visual Studio Code, precis som i den föregående kursen (Grundkurs i porgrammering). Ifall du inte använt Visual Studio Code tidigare, hittar du installeringsinstruktionerna [här](https://www.mooc.fi/fi/installation/vscode) och en introduktion till programmeringsomgivningen från förra kursen [här](https://rage.github.io/ohjelmointi-24-sv/osa-4/1-vscode).

I grundkursen i programmering lade vi märke till att det ofta är logiskt att gruppera relaterade data tillsammans i våra program. Ifall vi till exemepl skulle förvara information om en bok skulle det vara logiskt att använda oss av en tupel eller en ordlista för att organisera datan till en enskild datastruktur.

Lösningen kunde se ut så här när man använder en tupel:

```python
namn = "Kodningsboken"
författare = "Peter Python"
ar = 1992

# Vi sammanställer dessa i en ordlista
bok = (namn, författare, ar)

# Vi skriver ut bokens namn
print(bok[0])
```

I ett fall som detta är fördelen med att använda en ordlista att vi kan använda strängar istället för indexar som nycklar. Vi kan alltså ge beskrivande namn till de saker som lagras i datastrukturen:

```python
namn = "Kodningsboken"
forfattare = "Peter Python"
ar = 1992

# Slår ihop till en ordlista
bok = {"namn": namn, "författare": forfattare, "år": ar}

# Vi skriver ut bokens namn
print(bok["namn"])
```

I båda fallen så skapar vi ett nytt _objekt_. Inom programmering har termen en specifik betydelse: ett objekt är en oberoende helhet, som i detta fall innehåller data som på något vis är relaterade. Att vara oberoende betyder att ändringar i ett objekt inte påverkar andra objekt.

Ifall vi skulle skapa två strukturellt identiska representationer av böcker med hjälp av ordlistor och identiska nycklar, skulle ändringar som görs i den ena inte påverka den andra:

```python
bok1 = {"namn": "Den gamle och Python", "författare": "Ernest Pythonson", "år": 1952}
bok2 = {"namn": "Sju Python", "författare": "Aleksis Python", "år": 1894}

print(bok1["namn"])
print(bok2["namn"])

bok1["namn"] = "Ett nytt namn"

print(bok1["namn"])
print(bok2["namn"])
```

<sample-output>

Den gamle och Python
Sju Python
Ett nytt namn
Sju Python

</sample-output>

<img src="8_1_1.png">

<text-box variant="info" name="Python objekt">


Du kanske kommer ihåg från grundkursen i programmering att vilket som helst värde i Python internt behandlas som ett objekt. Det betyder att värdet som lagrats i en variabel är en _referens till ett objekt_. Själva data är lagrad inuti ett objekt i datorns minne. Ifall du ger ett värde till en ny variabel med tilldelningen `a = 3`, är värdet som lagras i variabeln _inte_ 3, utan en _referens till ett objekt som innehåller värdet 3_.

De flesta andra programmeringsspråk (i varje fall de som stöder objektorienterad programmering) inkluderar vissa särskilt definierade _primitiva datatyper_. Dessa inkluderar ofta åtminstone [integer] heltal, flyttal och booleska sanningsvärden. Primitiver processeras direkt, vilket betyder att de är lagrade direkt i variabler, inte som referenser. Python har inga sådana primitiver, men att jobba med de grundläggade datatyperna i Python fungerar i praktiken på liknande sätt. Objekt av dessa grundläggande datatyper (såsom tal, booleska värden och strängar) är _oföränderliga_, vilket betyder att de inte kan ändras i minnet. Om värdet som lagras i en variabel med en grundläggande datatyp ändras, dvs. variabeln tilldelas ett nytt värde, så byts hela referensen ut. Det ursprungliga objektet finns dock kvar i minnet. 


</text-box>

## Objekt och metoder

Man kan komma åt data som lagras i ett objekt genom olika _metoder_. En metod är en funktion som opererar på ett specifikt objekt som den är kopplad till. Vi kan skilja på metoder och "vanliga" funktioner genom att se på hur de anropas, eftersom metoder används med punktnotation: först skriver man namnet på det objekt som avses, sedan en punkt och till sist metodens namn, åtföljt av argument ifall sådana finns. Till exempel returnerar metoden `values` alla värden som är lagrade i ett objekt av typen ordlista eller `dict`:

```python
# detta skapar ett objekt av typen ordlista med namnet bok
bok = {"namn": "Den gamle och Python", "författare": "Ernest Pythonson", "år": 1952}

# Vi skriver ut alla värden
# Metodanropet values() skrivs efter namnet på variabeln
# Kom ihåg punktnotation!
for varde in bok.values():
    print(varde)
```

<sample-output>

Den gamle och Python
Ernest Pythonson
1952

</sample-output>

På samma sätt opererar en strängmetod på det strängobjekt som den kallas på. Några exempel på strängmetoder är `count` och `find`:

```python
namn = "Påhittige Per"

# Skriv ut mängden P som förekommer
print(namn.count("P"))

# Mängden P som hittas i en annan sträng
print("Påhittade Praktiska Prepositioner".count("P"))

# Indexen av delsträngen Per
print(namn.find("Per"))

# Denna sträng har ingen matchande delsträng
print("Helt annan sträng".find("Per"))
```

<sample-output>

2
3
10
-1

</sample-output>

Strängmetoder returnerar värden, men ändrar inte innehållet i en sträng eftersom strängar i Python är oföränderliga. Detta gäller däremot inte alla objekt och metoder. Listor i Python är föränderliga, alltså kan listmetoder ändra innehållet i den lista som den kallas på utan att skapa en ny referens eller ett nytt objekt.

```python
lista = [1,2,3]

# Vi lägger till några element
lista.append(5)
lista.append(1)

print(lista)

# Vi tar bort ett element från början
lista.pop(0)

print(lista)
```

<sample-output>

[1, 2, 3, 5, 1]
[2, 3, 5, 1]

</sample-output>

<programming-exercise name='Minsta medeltalet' tmcname='osa08-01_minsta_medeltalet'>

Skapa funktionen `minsta_medeltalet(person1: dict, person2: dict, person3: dict)`, som får tre ordlistor som argument.

Varje ordlistsobjekt innehåller värden som refererar till följande nycklar:

* `"namn"`: deltagarens namn
* `"resultat1"`: deltagarens första resultat (heltal mellan 1...10)
* `"resultat2"`: deltagarens andra resultat (liksom ovan)
* `"resultat3"`: deltagarens tredje resultat (liksom ovan)

Funktionen ska beräkna genomsnittet av de tre resultaten för varje deltagare och sedan returnera den deltagare vars genomsnittliga resultat är minst. Returvärdet bör vara hela det ordlistsobjekt som innehåller information om deltagaren.

Du kan anta att endast en deltagare har det minsta medeltalet.

Ett exempel på funktionen:

```python
person1 = {"namn": "Ella", "resultat1": 2, "resultat2": 3, "resultat3": 3}
person2 = {"namn": "Bella", "resultat1": 5, "resultat2": 1, "resultat3": 8}
person3 = {"namn": "Stella", "resultat1": 3, "resultat2": 1, "resultat3": 1}

print(minsta_medeltalet(person1, person2, person3))
```

<sample-output>

{'namn': 'Stella', 'resultat1': 3, 'resultat2': 1, 'resultat3': 1}

</sample-output>

</programming-exercise>

<programming-exercise name='Radernas summor' tmcname='osa08-02_radernas_summor '>

I Python är varje värde som lagras i en variabel en referens till ett objekt, så varje värde som lagras i en lista är också en referens till ett objekt. Detta gäller även vid modellering av en matrisdatastruktur: varje värde i listan på högsta nivån är en referens till en annan lista, som i sin tur innehåller referenser till de objekt som representerar elementen i matrisen.

Skapa funktionen `radernas_summor(matris: list)`, som tar en heltalsmatris som argument.

Funktionen ska lägga till ett nytt element på varje rad i matrisen. Detta element innehåller summan av de andra elementen på den raden. Funktionen har inget returvärde. Den bör modifiera matrisen i parametern.

Ett exempel på funktionen i användning:

```python
matris = [[1, 2], [3, 4]]
radernas_summor(matris)
print(matris)
```

<sample-output>

[[1, 2, 3], [3, 4, 7]]

</sample-output>

</programming-exercise>
