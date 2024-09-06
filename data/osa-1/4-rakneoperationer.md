---
path: "/osa-1/4-rakneoperationer"
title: "Räkneoperationer"
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* kan du använda dig av variabler i olika slags räkneoperationer
* kan du hantera tal i indata från användare
* kan du konvertera värden till olika grundläggande datatyper.

</text-box>

I de tidigare delarna har du sett exempel med enkla räkneoperationer. Följande tabell listar de mest allmänna operatorerna som kan användas för att utföra beräkningar i Python:

| Operator | Betydelse                       | Exempel    | Resultat |
|:--------:|---------------------------------|------------|----------|
| `+`      | Addition                        | `2 + 4`    |`6`       |
| `-`      | Subtraktion                     | `10 - 2.5` |`7.5`     |
| `*`      | Multiplikation                  | `-2 * 123` |`-246`    |
| `/`      | Division (resultat som flyttal) | `9 / 2`    |`4.5`     |
| `//`     | Division (resultat som heltal)  | `9 // 2`   |`4`       |
| `%`      | Rest                            | `9 % 2`    |`1`       |
| `**`     | Potens                          | `2 ** 3`   |`8`       |

Ordningen för operationerna är bekant från matematiken: potensuttryck beräknas först, sedan multiplikation och division, till sist addition och subtraktion. Ordningen kan ändras genom att använda parenteser.

Till exempel resulterar denna kodsnutt…

```python
print(2 + 3 * 3)
print((2 + 3) * 3)
```

… i följande utskrift:

<sample-output>

11
15

</sample-output>

## Operand, operator och datatyper

En räkneoperation består oftast av operander och operatorer:

<img src="1_5.png">

Datatypen hos en operand bestämmer i regel datatypen hos resultatet: om två heltal adderas är resultatet också ett heltal. Om ett flyttal subtraheras från ett annat flyttal är resultatet ett flyttal. Vidare kan man notera att om en av operanderna är ett flyttal, kommer resultatet att vara ett flyttal oavsett de andra operanderna.

Division med operatorn `/` är ett undantag. Dess resultat är ett flyttal även om operanderna är heltal. Till exempel kommer operationen `1 / 5` att ge flyttalet `0.2`. Observera att Python använder punkt som decimaltecken, inte decimalkomma som vanligtvis används på svenska.

Exempel:

```python
langd = 172.5
vikt = 68.55

# viktindex beräknas genom att dividera vikten med kvadratroten av längden
# längden anges i meter
bmi = vikt / (langd / 100) ** 2

print(f"Viktindexet är {bmi}")
```

Programmets utskrift ser ut så här:

<sample-output>

Viktindexet är 23.037177063642087

</sample-output>

Märk att Python också har operatorn `//` för division med heltal som resultat. Om operanderna är heltal, kommer resultatet också att vara ett heltal. Resultatet avrundas neråt till närmaste heltal. Exempelvis skriver detta program…

```python
x = 3
y = 2

print(f"/-operatorn {x/y}")
print(f"//-operatorn {x//y}")
```

… ut följande:

<sample-output>

/-operatorn 1.5
//-operatorn 1

</sample-output>

## Tal som indata

Vi har redan använt oss av `input`-funktionen för att läsa in strängar som användaren matat in. Samma funktion kan också användas för att läsa in tal, men då måste strängen som funktionen returnerar först konverteras till någon av de datatyper som representerar ett tal i programkoden. I den förra delen konverterade vi heltal till strängar med `str`-funktionen. Nu gäller samma princip, men vi ska använda en annan funktion eftersom vi gör konverteringen åt motsatt håll.

En sträng kan konverteras till ett heltal med funktionen `int`. Programmet nedan ber användaren mata in sitt födelseår och sparar det i variabeln `indata_strang`. Programmet skapar därefter variabeln `ar` som innehåller året konverterat till heltal. Efter det går det att räkna `2021 - ar`, med hjälp av det värde användaren angett.

```python
indata = input("Vilket är ditt födelseår? ")
ar = int(indata)
print(f"Din ålder i slutet av 2020: {2020 - ar}" )
```

<sample-output>

Vilket är ditt födelseår? **1995**
Din ålder i slutet av 2020: 25

</sample-output>

Vanligen behöver man inte skapa två separata variabler (som ovan) för att läsa en siffra från användaren. Istället kan användarens text läsas in och konverteras till heltal samtidigt:

```python
ar = int(input("Vilket är ditt födelseår? "))
print(f"Din ålder i slutet av 2020: {2020 - ar}" )
```

En sträng kan också konverteras till flyttal. Det sker med funktionen `float`. Det här programmet frågar användaren om hennes eller hans längd och vikt, och använder svaren för att räkna ut viktindexet:

```python
langd = float(input("Ange längd: "))
vikt = float(input("Ange vikt: "))

langd = langd / 100
bmi = vikt / langd ** 2

print(f"Viktindexet är {bmi}")
```

Här är ett exempel på en utskrift från programmet:

<sample-output>

Ange längd: **163**
Ange vikt: **74.45**
Viktindexet är 28.02137829801649

</sample-output>

<in-browser-programming-exercise name="Siffra gånger fem" tmcname="osa01-13_x_ganger_fem">

Skapa ett program som frågar efter ett tal av användaren. Programmet ska skriva ut talet multiplicerat med fem.

Så här ska programmet fungera:

<sample-output>

Ge ett tal: **3**
När 3 multipliceras med 5, får vi 15

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Namn och ålder" tmcname="osa01-14_namn_alder">

Skapa ett program som frågar efter användarens namn samt födelseår. Programmet ska därefter skriva ut ett meddelande enligt följande exempel:

<sample-output>

Ange namn: **Sandro Syntetisk**
Ange födelseår: **1990**
Hej Sandro Syntetisk, du är 30 år i slutet av 2020

</sample-output>

</in-browser-programming-exercise>

## Att använda variabler

Låt oss kika på ett program som beräknar summan av tre tal som användaren anger:

```python
tal1 = int(input("Tal ett: "))
tal2 = int(input("Tal två: "))
tal3 = int(input("Tal tre: "))

summa = tal1 + tal2 + tal3
print(f"Summan av talen: {summa}")
```

Här har vi ett exempel på när vi kör programmet:

<sample-output>

Tal ett: **5**
Tal två: **21**
Tal tre: **7**
Summan av talen: 33

</sample-output>

Programmet använder fyra variabler, men i det här fallet skulle det faktiskt räcka med två variabler:

```python
summa = 0

tal = int(input("Tal ett: "))
summa = summa + tal

tal = int(input("Tal två: "))
summa = summa + tal

tal = int(input("Tal tre: "))
summa = summa + tal

print(f"Summan av talen: {summa}")
```

Nu läses alla tal som användaren ges in med hjälp av en och samma variabel, `tal`. Värdet på variabeln `summa` ökas med värdet på variabeln tal varje gång användaren skriver in ett nytt tal.

Vi tar en lite närmare titt på instruktionen:

```python
summa = summa + tal
```

Här adderas värdena i variablerna `summa` och `tal` – för att lagras i variabeln summa. Till exempel om värdet på `summa` är `3` och värdet på `tal` är `2`, kommer värdet på summa att vara `5` efter att instruktionen körts.

Att öka på värdet hos en variabel är en vanlig operation. Därför finns det en liten genväg. Den här notationen fungerar i praktiken som instruktionen ovan:

```python
summa += tal
```

Det här tillåter oss skriva programmet lite mer koncist:

```python
summa = 0

tal = int(input("Tal ett: "))
summa += tal

tal = int(input("Tal två: "))
summa += tal

tal = int(input("Tal tre: "))
summa += tal

print(f"Summan av talen: {summa}")
```

Egentligen behöver vi inte alls variabeln `tal`. Vi kan också behandla talen som användaren matar in på följande sätt:

```python
summa = 0

summa += int(input("Tal ett: "))
summa += int(input("Tal två: "))
summa += int(input("Tal tre: "))

print(f"Summan av talen: {summa}")
```

I praktiken beror antalet variabler som behövs på situationen. Om man behöver minnas enskilda värden som användaren anger, är det inte möjligt att "återanvända" samma variabel för att läsa in olika värden. Här är ett exempel på en sådan situation:

```python
tal1 = int(input("Tal ett: "))
tal2 = int(input("Tal två: "))

print(f"{tal1} + {tal2} = {tal1+tal2}")
```

<sample-output>

Tal ett: **2**
Tal två: **3**
2 + 3 = 5

</sample-output>

Å andra sidan har programmet inte en namngiven variabel där summan av de två angivna värdena skulle lagras.

Att "återanvända" en variabel lönar sig bara då när det finns ett behov att lagra värden av samma typ och orsak – till exempel då man adderar tal.

I följande exempel används variabeln `data` för att lagra användarens namn och därefter hens ålder. Det finns ingen logik i att göra så!

```python
data = input("Vad är ditt namn? ")
print("Hej " + data + "!")

data = int(input("Vad är din ålder? "))
# programmet fortsätter...
```

En bättre idé vore att använda skilda variabler med namn som tydligt beskriver deras funktion:

```python
namn = input("Vad är ditt namn? ")
print("Hej " +  namn + "!")

alder = int(input("Vad är din ålder? "))
# programmet fortsätter...
```

<in-browser-programming-exercise name="Dygn i sekunder" tmcname="osa01-15_dygn_i_sekunder">

Skapa ett program som frågar användaren om ett antal dagar. Programmet ska därefter räkna ut hur många sekunder dessa dagar motsvarar.

Programmet ska fungera så här:

<sample-output>

Hur många dygns längd ska räknas i sekunder? **1**
86400

</sample-output>

Ett annat exempel:

<sample-output>

Hur många dygns längd ska räknas i sekunder? **7**
604800

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Fixa programmet: Produkten av talen" tmcname="osa01-20_produkten_av_talen">

Det här programmet borde fråga efter tre tal från användaren och räkna talens produkt. Det finns dessvärre fel i programmet. Korrigera dem, så att programmet fungerar på önskat sätt.

Här är ett exempel på hur programmet borde fungera:

<sample-output>

Ange tal 1: **2**
Ange tal 2: **3**
Ange tal 3: **5**
Produkten av talen är 30

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Talens summa och produkt" tmcname="osa01-16_summa_produkt">

Skapa ett program som ber användaren mata in två tal. Programmet ska räkna summan och produkten av dessa tal.

Så här ska programmet fungera:

<sample-output>

Tal 1: **3**
Tal 2: **7**
Talens summa 10
Produkten av talen 21

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Summa och medeltal" tmcname="osa01-17_summa_medeltal">

Skapa ett program som ber användaren att ange fyra tal. Programmet ska räkna summan och medeltalet av dessa tal.

Så här ska programmet fungera:

<sample-output>

Tal 1: **2**
Tal 2: **1**
Tal 3: **6**
Tal 4: **7**
Summan av talen är 16 och medeltalet är 4.0

</sample-output>

</in-browser-programming-exercise>



<in-browser-programming-exercise name="Matkostnader" tmcname="osa01-19_matkostnader">

Skapa ett program som uppskattar användarens genomsnittliga matkostnader.

Programmet frågar användaren om hur många gånger i veckan hen besöker Unicafe och vad hen betalar för sin lunch där. Dessutom frågar programmet om övriga matkostnader på veckonivå.

Baserat på den här informationen beräknar programmet de genomsnittliga matkostnaderna på dags- och veckobasis.

Så här ska programmet fungera:

<sample-output>

Hur många gånger i veckan äter du på Unicafe? **4**
Vad kostar Unicafe-lunchen? **2.5**
Hur mycket spenderar då på övriga matinköp under veckan? **28.5**

Genomsnittliga matkostnader:
Under en dag 5.5 euro
Under en vecka 38.5 euro

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Gruppindelning" tmcname="osa01-18_gruppindelning">

Gör ett program som frågar efter antalet studerande på en kurs samt storleken på en grupp. Programmet ska beräkna hur många grupper som behöver bildas. En av grupperna kan vid behov ha färre medlemmar än den önskade gruppstorleken.

<sample-output>

Hur många studerande? **8**
Vad är gruppstorleken? **4**
Antalet grupper: 2

</sample-output>

<sample-output>

Hur många studerande? **11**
Vad är gruppstorleken? **3**
Antalet grupper: 4

</sample-output>

Tips: Använd dig av operatorn för heltalsdivision `//`

Tips 2: Om du inte hittar på en lösning kan du bekanta dig med villkorssatser (if-satser), som presenteras i nästa del. De förenklar uppgiften avsevärt.

</in-browser-programming-exercise>

Repetitionsfrågor till denna del: 

<quiz id="7722d5cd-4b10-5b39-80cc-834d09f01ff2"></quiz>
