---
path: "/osa-1/5-villkorssatser"
title: "If-satser"
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* kan du använda dig av en enkel villkorssats (if-sats) när du programmerar
* vet du vad ett Boolean-värde är
* kan du uttrycka villkor med hjälp av jämförelseoperatorer.

</text-box>

Hittills har vi skapat program där koden körts rad för rad från början till slut. Istället för att köra varje kodrad när programmet är igång är det ofta nyttigt att ha delar i programmet som endast körs i vissa situationer.

Till exempel verifierar följande program att användaren är tillräckligt gammal:

```python
alder = int(input("Vad är din ålder? "))

if alder > 17:
    print("Du är myndig!")
    print("Här får du alltså GTA 6.")

print("Nästa kund!")
```

När användaren är över 17 år, borde det se ut så här när programmet körs:

<sample-output>

Vad är din ålder? **18**
Du är myndig!
Här får du alltså GTA 6.
Nästa kund!

</sample-output>

Däremot, om användaren är 17 eller yngre, ser utskriften ut så här:

<sample-output>

Vad är din ålder? **16**
Nästa kund!

</sample-output>

Dessa exempel visar hur ett värde som getts till programmet påverkar vilka delar av koden som körs. Programmet innehåller en villkorssats, som vanligen kallas if-sats, som gör det möjligt att ange vilken kod som ska köras i vilka situationer. 

<img src="1_6.png">

I en if-sats följs nyckelordet `if` av ett villkorsuttryck som till exempel kan vara en jämförelse av två värden. Koden som följer körs endast då villkoret uppfylls.

Notera kolontecknet. Om det saknas…

```python
alder = 10

# kolonet saknas i slutet av raden
if alder > 17
    print("Du är myndig.")
```

…kommer ett felmeddelande att skrivas ut när programmet körs:

<sample-output>
<pre>
File "program.py", line 3
  if alder > 17
              ^
SyntaxError: invalid syntax
</pre>
</sample-output>

## Jämförelseoperatorer

Det är vanligt att man vill jämföra två värden sinsemellan. Här följer en tabell över de vanligaste jämförelseoperatorerna i Python:

| Operator | Betydelse                | Exempel  |
|:--------:|--------------------------|----------|
| `==`     | Är lika med              | `a == b` |
| `!=`     | Är inte lika             | `a != b` |
| `>`      | Större än                | `a > b`  |
| `>=`     | Större än eller lika med | `a >= b` |
| `<`      | Mindre än                | `a < b`  |
| `<=`     | Mindre än eller lika med | `a <= b` |

Vi tar nu en titt på ett program som ger olika utskrifter baserat på det värde som användaren anger. Här har vi tre if-satser som kan uppfyllas då värdet är negativt, positivt eller lika med noll:

```python
tal = int(input("Ge ett tal: "))

if tal < 0:
    print("Talet är negativt.")

if tal > 0:
    print("Talet är positivt.")

if tal == 0:
    print("Talet är noll.")
```

Så här kan det se ut när vi kör programmet med olika indata:

<sample-output>

Ge ett tal: **15**
Talet är positivt.

</sample-output>

<sample-output>

Ge ett tal: **-18**
Talet är negativt.

</sample-output>

<sample-output>

Ge ett tal: **0**
Talet är noll.

</sample-output>

## Indentering

Python känner igen att en kodsnutt hör till en if-sats på basis av indentering, dvs. instruktioner som dragits in på raden. Alla instruktioner som kommer efter if-raden som indenteras på samma sätt hör till if-satsen. Indenteringen (indragningen, tomrummet) ska vara lika stort för varje rad.

Exempelvis:

````python
losenord = input("Ange lösenord: ")

if losenord == "katt":
    print("Du visste lösenordet!")
    print("Du måste alltså vara den riktiga användaren...")
    print("...eller så är du en hacker.")

print("Programmet avslutades. Tack och hej!")
````

Du kan använda tab-tangenten för att lägga till mellanrum där det behövs. Om du använder mellanslag är det viktigt att komma ihåg att använda lika många för varje rad. OBS! Använd antingen tab eller mellanslag, blanda inte inom samma if-sats.

<img src="1_6_keyboard.png">

Flera texteditorer indenterar automatiskt den följande raden när Enter-tangenten trycks efter ett kolon. Du får bort indenteringen genom att använda Backspace-tangenten i början av en rad.

<img src="1_6_keyboard2.png">
<small><center>
Tangentbordsbilden hämtad från:
 <a href="https://pixabay.com/users/Clker-Free-Vector-Images-3736/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=311803">Clker-Free-Vector-Images</a> from <a href="https://pixabay.com/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=311803">Pixabay</a>
</center></small>

<in-browser-programming-exercise name="Orwell" tmcname="osa01-21_orwell">

Skapa ett program som frågar användaren om ett heltal och skriver ut texten "Orwell" om siffran är 1984. Annars skrivs inget ut.

<sample-output>

Ge ett tal: **2020**

</sample-output>

<sample-output>

Ge ett tal: **1984**
Orwell

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Absolutbelopp" tmcname="osa01-22_absolutbelopp">

Skapa ett program som ber använder om ett heltal. Om talet är mindre än noll, skriver programmet ut talet multiplicerat med  -1. I övriga fall skriver programmet ut det tal som användaren angett. Nedan finns några exempel på hur programmet ska fungera.

<sample-output>

Ge ett tal: **-7**
Talets absolutbelopp är 7

</sample-output>

<sample-output>

Ge ett tal: **1**
Talets absolutbelopp är 1

</sample-output>

<sample-output>

Ge ett tal: **-99**
Talets absolutbelopp är 99

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Soppa. Eller inte." tmcname="osa01-23_soppa">

Skapa ett program som först frågar efter användarens förnamn. Om namnet inte är "Jerry", fortsätter programmet med att fråga antalet sopportioner och berättar sedan priset för "hela soppan". En portion kostar 5,90.

Två exempel:

<sample-output>

Vad heter du: **Kramer**
Hur många sopportioner: **2**
Slutsumma 11.8
Nästa!

</sample-output>

<sample-output>

Vad heter du: **Jerry**
Nästa!

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Storleksklass" tmcname="osa01-24_storleksklass">

Skapa ett program som frågar efter ett heltal av användaren. Programmet ska sedan berätta i vilken storleksklass talet är, enligt följande exempel:

<sample-output>

Ge ett tal: **950**
Siffran är mindre än 1000
Tackar!

</sample-output>

<sample-output>

Ge ett tal: **59**
Siffran är mindre än 1000
Siffran är mindre än 100
Tackar!

</sample-output>

<sample-output>

Ge ett tal: **2**
Siffran är mindre än 1000
Siffran är mindre än 100
Siffran är mindre än 10
Tackar!

</sample-output>

<sample-output>

Ge ett tal: **1123**
Tackar!

</sample-output>


</in-browser-programming-exercise>


## Boolean-värden och -uttryck

Alla villkor i en if-sats resulterar i ett sanningsvärde, det vill säga sant eller falskt. Till exempel är villkoret `a < 5` sant då `a` är mindre än fem och falskt då `a` är fem eller större.

Denna typ av värden kallas alltså Boolean-värden (efter matematikern George Boole). I Python representerar datatypen `bool` ett sanningsvärde. Variabler av typen `bool` kan endast ha ett av följande värden: `True` (sant) och `False` (falskt).

En kodsnutt som resulterar i något av de ovan nämnda värdena kallas Boolean-uttryck. Ett villkor i en if-sats är alltid ett Boolean-uttryck och kan i flera situationer användas som synonym för villkorsuttryck.

Resultatet av ett Boolean-uttryck kan lagras i en variabel på samma sätt som vilken som helst annan numerisk räkneoperation:

```python
a = 3
villkor = a < 5
print(villkor)
if villkor:
    print("a är mindre än 5")
```

<sample-output>

True
a är mindre än 5

</sample-output>

Pythons nyckelord `True` och `False` kan också användas direkt som sådana. I det följande exemplet körs `print`-instruktionen alltid, eftersom värdet på villkoret är `True`:

```python
villkor = True
if villkor:
    print("Vi når alltid hit")
```

<sample-output>

Vi når alltid hit

</sample-output>

Man kan tycka att det i ovanstående exempel inte verkar vara en så nyttig funktion, men senare under kursen kommer vi att se på situationer där vi kan ha mer nytta av Boolean-variabler.

<in-browser-programming-exercise name="Räknare" tmcname="osa01-25_raknare">

Skapa ett program som först ber användaren ange två tal och därefter en resultat av en aritmetisk operation. Om användaren matar in summa, produkt eller differens, ska programmet utföra den nämnda räkneoperationen. I övriga fall skriver inte programmet ut något.

Exempel:

<sample-output>

Tal 1: **10**
Tal 2: **17**
Kommando: **summa**

10 + 17 = 27

</sample-output>

<sample-output>

Tal 1: **4**
Tal 2: **6**
Kommando: **produkt**

4 * 6 = 24

</sample-output>

<sample-output>

Tal 1: **4**
Tal 2: **6**
Kommando: **differens**

4 - 6 = -2

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Temperaturer" tmcname="osa01-26_temperaturer">

Skapa ett program som ber användaren ange en temperatur i Fahrenheit. Programmet ska skriva ut den här temperaturen i Celcius. Om temperaturen mätt i Celcius är under noll ska programmet också skriva ut texten "Kallt!".

Du kan söka på nätet efter den korrekta formeln för att konvertera temperaturer i Farenheit till Celcius.

Exempel:

<sample-output>

Ange temperatur (i Fahrenheit): **101**
101 grader Fahrenheit är 38.333333333333336 grader Celcius

Ange temperatur (i Fahrenheit): **21**
21 grader Fahrenheit är -6.111111111111111 grader Celcius
Kallt!

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Lön" tmcname="osa01-27_lon">

Skapa ett program som frågar efter timlön, antal arbetstimmar samt veckodag. Programmet skriver ut lönen som räknas med formeln timlön * arbetstimmar. På söndagar får man dubbel timlön, dvs. den vanliga timlönen * 2. 

<sample-output>

Timlön: **8.5**
Arbetstimmar: **3**
Veckodag: **måndag**
Lön 25.5 euro

</sample-output>

<sample-output>

Timlön: **12.5**
Arbetstimmar: **10**
Veckodag: **söndag**
Lön 250.0 euro

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Fixa programmet: Ränta" tmcname="osa01-28_ranta">

Det här programmet räknar antalet bonuspoäng som ska adderas till ett bonuskort i slutet av året, enligt följande formel:

* bonuspoäng < 100: ränta 10 % extra poäng
* övriga fall: ränta 15 % extra poäng

Så här fungerar programmet:

<sample-output>

Hur många poäng? **55**
Du fick 10 % i bonus
Du har nu 60.5 poäng

</sample-output>

Programmet beter sig dock underligt med en del indata:

<sample-output>

Hur många poäng? **95**
Du fick 10 % i bonus
Du fick 15 % i bonus
Du har nu 120.175 poäng

</sample-output>

Korrigera programmet så att man endast får 10 % eller 15 % bonus – inte både och.

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Morgondagens klädsel" tmcname="osa01-29_kladsel">

Gör ett program som frågar användaren om morgondagens väderprognos. Programmet rekommenderar därefter klädsel enligt vädret.

Rekommendationen beror på om temperaturen är över fem, tio eller 20 grader samt om det regnar.

Så här ska programmet fungera:

<sample-output>

Berätta väderprognosen för imorgon:
Temperatur: **21**
Regnar det (ja/nej): **nej**
Ta på dig byxor och t-skjorta

</sample-output>

<sample-output>

Berätta väderprognosen för imorgon:
Temperatur: **11**
Regnar det (ja/nej): **nej**
Ta på dig byxor och t-skjorta
Ta på dig också en långärmad tröja

</sample-output>

<sample-output>

Berätta väderprognosen för imorgon:
Temperatur: **7**
Regnar det (ja/nej): **nej**
Ta på dig byxor och t-skjorta
Ta på dig också en långärmad tröja
Klä på dig en jacka

</sample-output>

<sample-output>

Berätta väderprognosen för imorgon:
Temperatur: **3**
Regnar det (ja/nej): **ja**
Ta på dig byxor och t-skjorta
Ta på dig också en långärmad tröja
Klä på dig en jacka
En varm jacka rekommenderas
Vantar rekommenderas också
Kom ihåg paraplyet!

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Andra gradens ekvation" tmcname="osa01-30_andra_gradens_ekvation">

Modulen `math` i Python har funktionen `sqrt` som kan användas för att räkna kvadratroten för ett tal. Så här fungerar funktionen:

```python
from math import sqrt

print(sqrt(9))
```

Programmet skriver ut:

<sample-output>

3.0

</sample-output>

Gör ett program som beräknar resultatet för andra gradens ekvation ax² + bx + c. Användaren ska mata in värdena på a, b och c, varefter programmet beräknar lösningen enligt följande formel:

x = (-b ± sqrt(b² - 4ac)) / (2a)

Du kan anta att ekvationen har två rötter, varvid formeln ovan fungerar.

Exempel:

<sample-output>

Ge a: **1**
Ge b: **2**
Ge c: **-8**

Rötterna är 2.0 och -4.0

</sample-output>

</in-browser-programming-exercise>

Repetitionsfrågor till denna del:

<quiz id="cb6eff3b-2fb8-506d-9019-e97de6834d7e"></quiz>

Vänligen svara på en kort enkät om materialet i den här veckans modul. Du får ett poäng när du fyllt i enkäten.

<quiz id="5f238c10-5e09-5a35-94f5-d9a0b56d9e79"></quiz>
