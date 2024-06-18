---
path: '/osa-5/3-lexikon'
title: 'Lexikon'
hidden: false
---


<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* känner du till datatypen lexikon
* kan du använda lexikon med olika typer av nycklar och värden
* vet du hur man går igenom värden i ett lexikon
* har du koll på olika användningsområden för lexikon.

</text-box>

Listor kan vara händiga i flera situationer, men deras svaga punkt är att elementen hämtas med hjälp av index (0, 1, 2 o.s.v.). Om du vill hitta ett element i en lista måste du alltså veta dess index, eller alternativt gå igenom hela listan.

En ytterligare central datastruktur i Python är lexikon, som vi nu ska se på. I lexikon är elementen indexerade enligt nycklar. Varje nyckel har ett värde. Värden som lagrats i ett lexikon kan hämtas och ändras med hjälp av dess nyckel.

## Att använda lexikon

Det följande visar hur datastrukturen hos lexikon fungerar. Här är ett enkelt lexikon som innehåller översättningar från finska till svenska:

```python
lexikon = {}

lexikon["apina"] = "apa"
lexikon["banaani"] = "banan"
lexikon["cembalo"] = "cembalo"

print(len(lexikon))
print(lexikon)
print(lexikon["apina"])
```

<sample-output>

3
{'apina': 'apa', 'banaani': 'banan', 'cembalo': 'cembalo'}
apa

</sample-output>

Notationen `{}` skapar ett tomt lexikon dit vi kan lägga till element. Tre stycken nyckel-värdepar skapas: `"apina"` är knutet till `"apa"`, `"banaani"` till `"banan"` och `"cembalo`" till `"cembalo"`. Till slut skriver vi ut antalet nyckel-värdepar i lexikonet, lexikonets innehåll samt det värde som tillhör nyckeln `"apina"`.

Efter att vi har skapat ett lexikon kan vi också använda det med indata från användaren:

```python
ord = input("Ange ord: ")
if ord in lexikon:
    print("Översättning:", lexikon[ord])
else:
    print("Ordet hittades inte")
```

Märk hur vi använder `in`-operatorn ovan. När vi använder operatorn för variabler med typen lexikon, kollar operatorn om den första operanden finns bland nycklarna i lexikonet. Så här kan det se ut när programmet körs:

<sample-output>

Ange ord: **apina**
Översättning: apa

</sample-output>

<sample-output>

Ange ord: **pöllö**
Ordet hittades inte

</sample-output>

## Vad kan lagras i ett lexikon?

Datatypen kallas lexikon, men det innebär inte att man bara skulle kunna lagra strängar där. I det här exemplet är nycklarna strängar men värdena är heltal:

```python
resultat = {}
resultat["Maja"] = 4
resultat["Lisa"] = 5
resultat["Kalle"] = 2
```

Här är nycklarna heltal medan värdena är listor:

```python
listor = {}
listor[5] = [1, 2, 3]
listor[42] = [5, 4, 5, 4, 5]
listor[100] = [5, 2, 3]
```

## Hur nycklar och värden fungerar

Varje nyckel kan endast förekomma en gång i ett lexikon. Om du lägger till ett nytt värde med en nyckel som redan finns i lexikonet, kommer det ursprungliga värdet kopplat till nyckeln att ersättas med det nya värdet:

```python
lexikon["suuri"] = "väldig"
lexikon["suuri"] = "stor"
print(lexikon["suuri"])
```

<sample-output>

stor

</sample-output>

Alla nycklar i ett lexikon måste vara oföränderliga. Det betyder att en lista inte kan vara en nyckel, eftersom listor kan ändras på. Den här koden ger till exempel ett fel:

```python
lexikon[[1, 2, 3]] = 5
```

<sample-output>

TypeError: unhashable type: 'list'

</sample-output>

<text-box variant="hint" name="Hashtabell">

Märk ordet "unhashable" i felmeddelandet ovan. Det här är en hänvisning till de inte strukturerna i ett lexikon. Python lagrar innehållet i ett lexikon i en hashtabell. Varje nyckel har ett hashvärde som indikerar var nyckeln finns lagrad i minnet. Felmeddelandet ovan indikerar att en lista inte kan förvandlas till ett hashvärde, och kan därmed inte användas som en nyckel i lexikonet.

Kursen Datastrukturer och algoritmer ger en större insikt i hashtabeller.

</text-box>

Till skillnad från nycklar, kan värden i ett lexikon ändra och därmed kan vilken som helst typ av data lagras som ett värde. Ett och samma värde kan också vara kopplat till flera nycklar i samma lexikon.

<programming-exercise name='Gånger tio' tmcname='osa05-10b_kertaa_kymmenen'>

Skapa funktionen `ganger_tio(start: int, slut: int)` som skapar och returnerar ett lexikon. Lexikonet ska ha nycklarna i intervallet `start-slut`.

Värdet för varje nyckel ska vara nyckeln multiplicerat med tio.

Exempel:

```python
d = ganger_tio(3, 6)
print(d)
```

<sample-output>

{3: 30, 4: 40, 5: 50, 6: 60}

</sample-output>

</programming-exercise>

<programming-exercise name='Fakulteter' tmcname='osa05-11_kertomat'>

Skapa funktionen `fakulteter(n: int)` som returnerar fakulteterna för talen i intervallet `1-n` i ett lexikon så att nyckeln är `n` och värdet `n`:s fakultet.

Som en påminnelse: Talet `n`:s fakultet (`n!`) räknas genom att multiplicera talet med alla föregående positiva heltal. T.ex. `4! = 4 * 3 * 2 * 1 = 24`.

Exempel:

```python
k = fakulteter(5)
print(k[1])
print(k[3])
print(k[5])
```

<sample-output>

1
6
120

</sample-output>

</programming-exercise>

## Gå igenom ett lexikon

Den bekanta `for element in samling` -loopen kan också användas för att gå igenom ett lexikon. När det används direkt hos ett lexikon kommer loopen att en för en gå igenom nycklarna i lexikonet. I följande exempel skrivs varje nyckel och respektive värde:

```python
lexikon = {}

lexikon["apina"] = "apa"
lexikon["banaani"] = "banan"
lexikon["cembalo"] = "cembalo"

for nyckel in lexikon:
    print("nyckel:", nyckel)
    print("värde:", lexikon[nyckel])
```

<sample-output>

nyckel: apina
värde: apa
nyckel: banaani
värde: banan
nyckel: cembalo
värde: cembalo

</sample-output>

Ibland behöver du gå igenom allt innehåll i ett lexikon. Då kan du använda metoden `items` som returnerar alla nycklar och värden, ett par i sänder:

```python

for nyckel, varde in lexikon.items():
    print("nyckel:", nyckel)
    print("värde:", varde)
```

I exemplen ovan märkte du kanske att nycklar behandlas i den ordning som de lagts till i lexikonet. Eftersom nycklarna behandlas enligt deras hashvärden, borde ordningen inte ha någon skillnad i programmen. I flera äldre versioner av Python är det dessutom inte garanterat att ordningen är den samma som nycklarna lagts till.

## Några mer avancerade sätt att använda lexikon

Låt oss kika på en lista med ord:

```python
ordlista = [
  "banan", "mjölk", "ost", "jordnöt", "pasta", "mjöl", "majs",
  "tomat", "korv", "vitlök", "margarin", "jordnöt", "majs",
  "ost", "pasta", "pasta", "vitlök", "ost", "socker"
]
```

Vi skulle vilja analysera den här ordlistan på olika sätt. Vi är till exempel intresserade av hur många gånger de olika orden förekommer i listan.

Ett lexikon fungera väl för att hålla reda på sådan här information. I exemplet nedan går vi igenom orden i listan. Vi använder sedan orden som nycklar i ett lexikon som vi skapat, så att värdet som är kopplat till varje nyckel indikerar hur många gånger det specifika ordet har förekommit:

```python
def antal(lista):
    ordsamling = {}
    for ord in lista:
        # om ordet inte förekommit ska nyckeln skapas och få ett värde
        if ord not in ordsamling:
            ordsamling[ord] = 0
        # öka på antalet gånger ordet förekommit
        ordsamling[ord] += 1
    return ordsamling

# vi anropar funktionen
print(antal(ordlista))
```

Programmet skriver ut det följande:

<sample-output>

{'banan': 1, 'mjölk': 1, 'ost': 3, 'jordnöt': 2, 'pasta': 3, 'mjöl': 1, 'majs': 2, 'tomat': 1, 'korv': 1, 'vitlök': 2, 'margarin': 1, 'socker': 1}

</sample-output>

Om vi då skulle vela ordna orden enligt den första bokstaven i varje ord? Här kunde vi också kunna använda lexikon:

```python
def enligt_forsta_bokstaven(lista):
    grupper = {}
    for ord in lista:
        forsta_bokstaven = ord[0]
        # skapa lista då bokstaven förekommer för den första gången
        if forsta_bokstaven not in grupper:
            grupper[forsta_bokstaven] = []
        # lägg till ordet under den korrekta bokstaven
        grupper[forsta_bokstaven].append(ord)
    return grupper

grupper = enligt_forsta_bokstaven(ordlista)

for nyckel, varde in grupper.items():
    print(f"ord som börjar med {nyckel}: ")
    for ord in varde:
        print(ord)
```

Funktionens struktur liknar mycket den som finns i det tidigare exemplet, men den här gången är värden lagrade i form av listor. Programmet skriver ut det följande:

<sample-output>

ord som börjar med b:
  banan
ord som börjar med m:
  mjölk
  mjöl
  majs
  margarin
  majs
ord som börjar med o:
  ost
  ost
  ost
ord som börjar med j:
  jordnöt
  jordnöt
ord som börjar med p:
  pasta
  pasta
  pasta
ord som börjar med t:
  tomat
ord som börjar med k:
  korv
ord som börjar med v:
  vitlök
  vitlök
ord som börjar med s:
  socker

</sample-output>

<programming-exercise name='Histogram' tmcname='osa05-12_histogrammi'>

Skapa funktionen `histogram` som får som argument en sträng. Funktionen ska skriva ut ett histogram som beskriver förekomsten av olika bokstäver.

Exempelvis för anropet `histogram("abba")` ska utskriften vara:

<sample-output>

<pre>
a **
b **
</pre>

</sample-output>

Eller `histogram("lyxvilla")`:

<sample-output>

<pre>
l *
y *
x *
v *
i *
l **
a *
</pre>

</sample-output>

</programming-exercise>

<programming-exercise name='Telefonkatalog, version 1' tmcname='osa05-13_puhelinluettelo_versio1'>

Skapa en telefonkatalog som fungerar på följande sätt:

<sample-output>

kommando (1 sök, 2 lägg till, 3 avsluta): **2**
namn: **pekka**
nummer: **040-5466745**
ok!
kommando (1 sök, 2 lägg till, 3 avsluta): **2**
namn: **emilia**
nummer: **045-1212344**
ok!
kommando (1 sök, 2 lägg till, 3 avsluta): **1**
namn: **pekka**
040-5466745
kommando (1 sök, 2 lägg till, 3 avsluta): **1**
namn: **maija**
inget nummer
kommando (1 sök, 2 lägg till, 3 avsluta): **2**
namn: **pekka**
nummer: **09-22223333**
ok!
kommando (1 sök, 2 lägg till, 3 avsluta): **1**
namn: **pekka**
09-22223333
kommando (1 sök, 2 lägg till, 3 avsluta): **3**
avslutar...

</sample-output>

Observera att varje namn endast kan vara förknippat till ett nummer. Om ett nytt nummer ges för en person kommer det tidigare numret att ersättas.

Obs! I dessa uppgifter ska du inte placera kod i `if __name__ == "__main__"` -blocket, om du inte ombeds göra det.

</programming-exercise>

<programming-exercise name='Telefonkatalog, version 2' tmcname='osa05-14_puhelinluettelo_versio2'>

Skapa nu en förbättrad version av telefonkatalogen. Samma person ska nu kunna ha flera nummer. I övrigt fungerar programmet som den tidigare versionen.

<sample-output>

kommando (1 sök, 2 lägg till, 3 avsluta): **2**
namn: **pekka**
nummer: **040-5466745**
ok!
kommando (1 sök, 2 lägg till, 3 avsluta): **2**
namn: **emilia**
nummer: **045-1212344**
ok!
kommando (1 sök, 2 lägg till, 3 avsluta): **1**
namn: **pekka**
040-5466745
kommando (1 sök, 2 lägg till, 3 avsluta): **1**
namn: **maija**
inget nummer
kommando (1 sök, 2 lägg till, 3 avsluta): **2**
namn: **pekka**
nummer: **09-22223333**
ok!
kommando (1 sök, 2 lägg till, 3 avsluta): **1**
namn: **pekka**
040-5466745
09-22223333
kommando (1 sök, 2 lägg till, 3 avsluta): **3**
avslutar...

</programming-exercise>

## Att ta bort nycklar och värden från ett lexikon

Det är naturligtvis möjligt att ta bort nyckel-värdepar från ett lexikon. Det finns två sätt att göra det här. Det första sättet är att använda kommandot `del`:

```python
personal = {"Antti": "lektor", "Emilia": "professor", "Arto": "lektor"}
del personal["Arto"]
print(personal)
```

<sample-output>

{'Antti': 'lektor', 'Emilia': 'professor'}

</sample-output>

Om du försöker använda `del`-kommandot för att ta bort en nyckel som inte finns i listan, kommer ett fel att uppstå:

```python
personal = {"Antti": "lektor", "Emilia": "professor", "Arto": "lektor"}
del personal["Jukka"]
```

<sample-output>

<pre>
>>> del personal["Jukka"]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'Jukka'
</pre>

</sample-output>

Därmed lönar det sig att kolla om en nyckel existerar före du försöker avlägsna den från listan:

```python
personal = {"Antti": "lektor", "Emilia": "professor", "Arto": "lektor"}
if "Jukka" in personal:
  del personal["Jukka"]
  print("Avlägsnades")
else:
  print("Hittade inte personen som skulle avlägsnas")
```

Ett annat sätt att ta bort element från listan är att använda metoden `pop`:

```python
personal = {"Antti": "lektor", "Emilia": "professor", "Arto": "lektor"}
borttagen = personal.pop("Arto")
print(personal)
print("Avlägsnade", borttagen)
```

<sample-output>

{'Antti': 'lektor', 'Emilia': 'professor'}
Avlägsnade lektor

</sample-output>

Metoden `pop` returnerar också värdet på elementet som togs bort.

Metoden `pop` kommer också i vanliga fall att ge ett fel om nyckeln som man försöker ta bort saknas i lexikonet. Det här kan man dock undvika genom att som ett andra argument ge till funktionen ett return-värde som funktionen kan returnera då en nyckel saknas. Värdet `None` kan till exempel användas här:

```python
personal = {"Antti": "lektor", "Emilia": "professor", "Arto": "lektor"}
borttagen = personal.pop("Jukka", None)
if borttagen == None:
  print("Hittade inte personen som skulle avlägsnas")
else:
  print("Avlägsnade", borttagen)
```

<sample-output>

Hittade inte personen som skulle avlägsnas

</sample-output>

Obs! Om du vill tömma ett lexikon och försöker göra det med en for-loop…

```python
personal = {"Antti": "lektor", "Emilia": "professor", "Arto": "lektor"}
for nyckel in personal:
  del personal[nyckel]
```

…kommer du att få ett felmeddelande:

<sample-output>

RuntimeError: dictionary changed size during iteration

</sample-output>

När man går igenom en samling med en for-loop, kan man inte ändra på samlingens innehåll så länge for-loopen är igång.

Lyckligtvis har lexikon en inbyggd metod som kan användas istället:

```python
personal.clear()
```

<programming-exercise name='Att vända ett lexikon' tmcname='osa05-15_sanakirjan_kaanto'>

Skapa funktionen `vand(lexikon: dict)` som får som argument ett lexikon. Funktionen ska vända på nycklarna och värdena enligt exemplet nedan.

```python
s = {1: "första", 2: "andra", 3: "tredje", 4: "fjärde"}
vand(s)
print(s)
```

<sample-output>

{"första": 1, "andra": 2, "tredje": 3, "fjärde": 4}

</sample-output>

Observera att det här också gäller för lexikon som getts som argument.

Använd [visualiseringsverktyget](https://pythontutor.com/visualize.html) om du stöter på problem.

</programming-exercise>

<programming-exercise name='Siffror som ord' tmcname='osa05-16_luvut_sanoina'>

Skapa funktionen `siffersamling()` som returnerar ett nytt lexikon. Lexikonet ska innehålla nycklarna noll till 99. Värdena ska innehålla nyckeln i skriven form. Se exemplet nedan:

```python
siffror = siffersamling()
print(siffror[2])
print(siffror[11])
print(siffror[45])
print(siffror[99])
print(siffror[0])
```

<sample-output>

två
elva
fyrtiofem
nittionio
noll

</sample-output>

Obs! Bilda inte varje ord skilt för sig utan fundera hur du kan använda loopar och lexikon till nytta i din lösning.

</programming-exercise>

## Använda lexikon för strukturerade data

Lexikon fungerar bra för att strukturera data. Följande kodsnutt skapar ett lexikon som innehåller information om en person:

```python
person = {"namn": "Peppa Python", "längd": 154, "vikt": 61, "ålder:" 44}
```

Här har vi alltså en person som heter Peppa Python. Hennes längd är 154, vikt 61 och ålder 44. Samma information kunde också lagras i skilda variabler:


```python
namn = "Peppa Python"
längd = 154
vikt = 61
alder = 44
```

Fördelen med lexikon är att det är en samling. Det samlar relaterade data under en variabel och det är enkelt att komma åt den information man är ute efter. Samma funktionalitet erbjuds också av listor:

```python
person = ["Peppa Python", 153, 61, 44]
```

Men med listor måste programmeraren minnas vilket index används för vilken information. Det finns inget som indikerar att `person[2]` innehåller vikten och `person[3]` åldern hos en person. När man använder lexikon, undviker man det här problemet eftersom all information finns lagrad under namngivna nycklar.

Om vi antar att det finns flera personer som definierats i samma format, kan vi komma åt deras information på följande sätt:

```python
person1 = {"namn": "Peppa Python", "längd": 154, "vikt": 61, "ålder": 44}
person2 = {"namn": "Philip Python", "längd": 174, "vikt": 103, "ålder": 31}
person3 = {"namn": "Pedro Python", "längd": 191, "vikt": 71, "ålder": 14}

personer = [person1, person2, person3]

for person in personer:
    print(person["namn"])

total_langd = 0
for person in personer:
    total_langd += person["längd"]

print("Medellängden är", total_langd / len(personer))
```

<sample-output>

Peppa Python
Philip Python
Pedro Python
Medellängden är 173.0

</sample-output>

<programming-exercise name='Filmregister' tmcname='osa05-17_elokuvarekisteri'>

Skapa funktionen `ny_film(register: list, namn: str, regissor: str, ar: int, langd: int)`. Funktionen ska lägga till en ny film i ett register.

Registret är en lista och varje element är ett lexikon med dessa nycklar:

* namn
* regissör
* år
* längd

Värdena ges som argument till funktionen.

Exempel:

```python
register = []
ny_film(register, "Drunknad i Python", "Philip Python", 2017, 116)
ny_film(register, "Python vs. Java – vol. 32", "Renny Pytholin", 2001, 94)
print(register)
```

<sample-output>

[{"namn": "Drunknad i Python", "regissör": "Philip Python", "år": 2017, "längd": 116}, {"namn": "Python vs. Java – vol. 32", "regissör": "Renny Pytholin", "år": 2001, "längd": 94}]

</sample-output>

</programming-exercise>

<programming-exercise name='Hitta film' tmcname='osa05-17b_etsi_elokuvat'>

Skapa funktionen `hitta_filmer(register: list, term: str)`. Funktionen ska skapa en ny lista som innehåller de filmer i vars namn söktermen hittas. Gemener och versaler ska inte påverka – med termen `Lil` hittar man t.ex. både filmerna `Lilja 4-ever` och `Den lilla Pythonkodaren`.

Exempel:

```python
register = [{"namn": "Drunknad i Python", "regissör": "Philip Python", "år": 2017, "längd": 116},
{"namn": "Python vs. Java – vol. 32", "regissör": "Renny Python", "år": 2001, "längd": 94},
{"namn": "Skymning i kodarlandet", "regissör": "M. Night Python", "år": 2011, "längd": 101}]

lista = hitta_filmer(register, "python")
print(lista)
```

<sample-output>

[{"namn": "Drunknad i Python", "regissör": "Philip Python", "år": 2017, "längd": 116}, {"namn": "Python vs. Java – vol. 32", "regissör": "Renny Python", "år": 2001, "längd": 94}]

</sample-output>

</programming-exercise>

<quiz id="87776053-a318-5e02-a931-2c68cdac8e99"></quiz>
