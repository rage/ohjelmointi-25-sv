---
path: '/osa-5/4-tuple'
title: 'Tuple'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* känner du till datatypen tuple
* kan du skapa tupler av olika typer av värden
* vet du vad skillnaden mellan en lista och tuple är
* kan du nämna några vanliga användningsområden för tupler.

</text-box>

En tuple är en datastruktur som på flera sätt påminner listan. De största skillnaderna mellan dessa två är:

* tupler är inom parenteser `()` medan listor är inom hakparenteser `[]`
* tupler är oföränderliga, medan innehållet i en lista kan ändra.

Den följande kodsnutten skapar en tuple som innehåller koordinaterna för en punkt:

```python
punkt = (10, 20)
```

Elementen lagrade i tupler kan kommas åt med index, på samma sätt som med listor:

```python
punkt = (10, 20)
print("x-koordinat:", punkt[0])
print("y-koordinat:", punkt[1])
```

<sample-output>

x-koordinat: 10
y-koordinat: 20

</sample-output>

Värden som lagrats i en tuple kan inte ändras efter att en tuple har skapats. Det följande kommer inte att fungera:

```python
punkt = (10, 20)
punkt[0] = 15
```

<sample-output>

TypeError: 'tuple' object does not support item assignment

</sample-output>

<programming-exercise name='Skapa tuple' tmcname='osa05-17c_skapa_tuple'>

Skapa funktionen `skapa_tuple(x: int, y: int, z: int)` som skapar och returnerar en tuple enligt dessa regler:

* tuplens första element är det minsta av de givna argumenten
* tuplens andra element är det största av de givna argumenten
* tuplens tredje element är de givna argumentens summa

Exempel:

```python
if __name__ == "__main__":
    print(skapa_tuple(5, 3, -1))
```

<sample-output>

(-1, 5, 7)

</sample-output>


</programming-exercise>

<programming-exercise name='Äldst' tmcname='osa05-18_aldst'>

Skapa funktionen `aldst(personer: list)` som får som argument en lista med tupler som innehåller information om personer. Funktionen ska hitta den äldsta personen och returnera hennes namn.

Varje tuple består av ett namn (element 1) och ett födelseår (element 2).

Exempel:

```python
p1 = ("Algot", 1977)
p2 = ("Eskil", 1985)
p3 = ("Mette", 1953)
p4 = ("Ellie", 1997)
personer = [p1, p2, p3, p4]

print(aldst(personer))
```

<sample-output>

Mette

</sample-output>

</programming-exercise>

<programming-exercise name='Äldre' tmcname='osa05-19_aldre'>

Vi antar att vi fortfarande har tuplerna från den föregående uppgiften till vårt förfogande.

Skapa funktionen `aldre(personer: list, ar: int)`. Funktionen ska returnera en ny lista som innehåller namnen på personerna i den givna listan som fötts före det givna året.

Exempel:

```python
p1 = ("Algot", 1977)
p2 = ("Eskil", 1985)
p3 = ("Mette", 1953)
p4 = ("Ellie", 1997)
personer = [p1, p2, p3, p4]

aldre_personer = aldre(personer, 1979)
print(aldre_personer)
```

<sample-output>

[ 'Algot', Mette' ]

</sample-output>

</programming-exercise>

## Vad behöver man tupler för?

Tupler är nyttiga i situationer där det finns en samling av värden som är på något sätt sammankopplade. Till exempel då man behandlar x- och y-koordinaterna hos en punkt, är tuplen ett naturligt val eftersom koordinater alltid består av två värden:

```python
punkt = (10, 20)
```

Det är tekniskt möjligt att använda en lista för att lagra dessa:

```python
punkt = [10, 20]
```

En lista är en samling av element i en viss ordning. Listans storlek kan också ändra. Eftersom vi lagrar koordinaterna för en punkt, vill vi lagra x- och y-koordinaterna specifikt – inte en godtycklig lista med dessa värden.

Eftersom tupler är oföränderliga – till skillnad från listor – kan de användas som nycklar i lexikon. Det följande kodexemplet skapar ett lexikon där koordinater används som nycklar:

```python
punkter = {}
punkter[(3, 5)] = "apa"
punkter[(5, 0)] = "banan"
punkter[(1, 2)] = "cembalo"
print(punkter[(3, 5)])
```

<sample-output>
apa
</sample-output>

Det är inte möjligt att skapa ett liknande lexikon med hjälp av listor:

```python
punkter = {}
punkter[[3, 5]] = "apa"
punkter[[5, 0]] = "banan"
punkter[[1, 2]] = "cembalo"
print(punkter[[3, 5]])
```

<sample-output>

TypeError: unhashable type: 'list'

</sample-output>

## Tupler utan parenteser

Parenteser är inte obligatoriska då man skapar tupler. Följande variabeltilldelningar ger likadana resultat:

```python
siffror = (1, 2, 3)
```

```python
siffror = 1, 2, 3
```

Det innebär att vi enkelt kan returnera flera värden med hjälp av tupler. Ta en titt på följande exempel:

```python
def minmax(lista):
  return min(lista), max(lista)

lista = [33, 5, 21, 7, 88, 312, 5]

minst, storst = minmax(lista)
print(f"Minsta talet är {minst} och största är {storst}")
```

<sample-output>

Minsta talet är 5 och största är 312

</sample-output>

Funktionen returnerar två värden i en tuple. Returvärdet kan tilldelas till två variabler samtidigt:

```python
minst, storst = minmax(lista)
```

Att använda parenteser kan göra notationen tydligare. Till vänster av tilldelningssatsen har vi också en tuple som består av två variabelnamn. Värdena som finns i tuplen som funktionen returnerar tilldelas till dessa två variabler.

```python
(minst, storst) = minmax(lista)
```

Du kanske minns metoden `items` från den förra delen. Vi använde den för att komma åt nycklarna och värdena som lagrats i ett lexikon:

```python
lexikon = {}

lexikon["apina"] = "apa"
lexikon["banaani"] = "banan"
lexikon["cembalo"] = "cembalo"

for nyckel, varde in lexikon.items():
    print("nyckel:", nyckel)
    print("värde:", varde)
```

Tupler finns i bakgrunden här också. Metoden `lexikon.items()` returnerar varje nyckel-värdepar som en tuple, där det första elementet innehåller nyckeln och det andra värdet.

Ett annat användningsområde för tupler är att byta värden sinsemellan två variabler:

```python
tal1, tal2 = tal2, tal1
```

Tilldelningssatsen ovan svänger på värdena lagrade i variablerna `tal1` och `tal2`. Resultatet är detsamma som vi skulle uppnå med hjälp av en hjälpvariabel:

```python
hjalp = tal1
tal1 = tal2
tal2 = hjalp
```

<programming-exercise name='Studeranderegister' tmcname='osa05-20_studeranderegister'>

I denna uppgift skapar vi ett enkelt register över studerande. Före du börjar programmera lönar det sig att fundera hurdan datastruktur som behövs för att organisera den data som ska lagras.

#### Lägga till studerande

Börja med att skapa funktionen `skapa_studerande` samt en första version av funktionen `skriv_ut`, som används för att skriva ut information om en studerande.

Så här används funktionerna:

```python
studerande = {}
skapa_studerande(studerande, "Robert")
skapa_studerande(studerande, "Lilou")
skriv_ut(studerande, "Robert")
skriv_ut(studerande, "Lilou")
skriv_ut(studerande, "Siri")
```

I det här skedet skriver programmet ut:

<sample-output>

<pre>
Robert:
 inga prestationer
Lilou:
 inga prestationer
hittade ingen med namnet Siri
</pre>

</sample-output>

#### Lägga till prestationer

Skapa funktionen `ny_prestation`, som lägger till en prestation för en studerande. Prestationen är en tuple som består av kursens namn och ett vitsord:

```python
studerande = {}
skapa_studerande(studerande, "Robert")
ny_prestation(studerande, "Robert", ("introkurs i Python", 3))
ny_prestation(studerande, "Robert", ("datastrukturer", 2))
skriv_ut(studerande, "Robert")
```

Utskriften ändras då det finns prestationer:

<sample-output>

<pre>
Robert:
 prestationer från 2 kurser:
  introkurs i Python 3
  datastrukturer 2
 medeltal 2.5
</pre>

</sample-output>

#### Höja på vitsord

När man lägger till en prestation ska kurser med vitsordet noll ignorera och tidigare vitsord ska inte sänkas:

```python
studerande = {}
skapa_studerande(studerande, "Robert")
ny_prestation(studerande, "Robert", ("introkurs i Python", 3))
ny_prestation(studerande, "Robert", ("datastrukturer", 2))
ny_prestation(studerande, "Robert", ("datastrukturer II", 0))
ny_prestation(studerande, "Robert", ("introkurs i Python", 2))
skriv_ut(studerande, "Robert")
```

<sample-output>

<pre>
Robert:
 prestationer från 2 kurser:
  introkurs i Python 3
  datastrukturer 2
 medeltal 2.5
</pre>

</sample-output>

#### Översikt

Skapa funktionen `oversikt` som skriver ut en översikt för samtliga studerandes prestationer:

```python
studerande = {}
skapa_studerande(studerande, "Robert")
skapa_studerande(studerande, "Lilou")
ny_prestation(studerande, "Robert", ("datastrukturer II", 1))
ny_prestation(studerande, "Robert", ("introkurs i Python", 1))
ny_prestation(studerande, "Robert", ("datastrukturer", 1))
ny_prestation(studerande, "Lilou", ("introkurs i Python", 5))
ny_prestation(studerande, "Lilou", ("spaden", 4))
kooste(studerande)
```

Utskriften ser ut så här:

<sample-output>

<pre>
antal studerande 2
flest prestationer 3 Robert
bästa medeltal 4.5 Lilou
</pre>

</sample-output>

</programming-exercise>

<programming-exercise name="Bokstavsruta" tmcname="osa05-21_bokstavsruta">

Den här delen når nu sitt kulmen med en relativt svår uppgift som kräver problemlösningsförmåga. Uppgiften kan lösas på flera sätt. Även om vi nyss har behandlat tupler så lönar det sig dock antagligen inte att använda dem i den här uppgiften.

Skapa ett program som skriver ut en bokstavsruta enligt följande exempel. Du kan anta att det finns högst 26 våningar.

<sample-output>

Våningar: **3**
<pre>
CCCCC
CBBBC
CBABC
CBBBC
CCCCC
</pre>

</sample-output>

<sample-output>

Våningar: **4**
<pre>
DDDDDDD
DCCCCCD
DCBBBCD
DCBABCD
DCBBBCD
DCCCCCD
DDDDDDD
</pre>

</sample-output>

Obs! Placera inte kod i `if __name__ == "__main__"` -blocket i dessa uppgifter, om du inte skilt ombeds göra det.

</programming-exercise>

<quiz id="8342aecc-48cd-5e26-a8ad-6272ba1df02a"></quiz>

Vänligen svara på en kort enkät gällande materialet för den här veckan.

<quiz id="7c3732cd-b37b-5524-9747-0fcf49c917bb"></quiz>
