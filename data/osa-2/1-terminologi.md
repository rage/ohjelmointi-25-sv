---
path: '/osa-2/1-terminologi'
title: 'Programmeringsterminologi'
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* känner du till de väsentligaste termerna inom programmering
* vet du vad skillnaden mellan en sats och ett uttryck är
* kan du ta reda på datatypen på värdet av ett uttryck
* har du lärt dig hur du genom att debugga hittar fel i din kod.

</text-box>

Under den första modulen fokuserade vi inte så mycket på terminologi. Nu är det dags att ta en titt på några centrala begrepp inom programmering.

## Sats

En sats (statement) är en del av ett program som kör någonting. En sats syftar ofta, men inte alltid, till en enstaka instruktion.

Till exempel `print("Hej")` är en sats som skriver ut en rad text. På samma sätt är `nummer = 2` en sats som lagrar ett värde i en variabel.

En sats kan också vara mera invecklad. Den kan till exempel bestå av flera satser. Följande sats består av tre rader:

```python
if namn == "Anna":
    print("Hejsan!")
    nummer = 2
```

Ovan finns två satser (print-sats och tilldelningssats) inom en if-sats.

## Block

Ett block är en grupp av efter varandra följande satser som är på samma nivå i programmets struktur. Till exempel if-satsens block innehåller de satser som körs då villkoret är sant.

```python
if alder > 17:
    # if-satsens block inleds
    print("Du är myndig!")
    alder = alder + 1
    print("Du är nu ett år äldre...")
    # blocket avslutas

print("Det här är i ett annat block.")
```

I Python markeras block genom att indentera all kod i blocket med samma antal mellanrum.

Obs! Pythons huvudblock ska aldrig indenteras, utan ska alltid vara så långt till vänster som möjligt i filen:

```python
# det här programmet fungerar inte eftersom koden inte är indenterad till det vänstra hörnet
  print("Hej allihopa")
  print("Det här är ett dåligt program")
```

## Uttryck

Ett uttryck (expression) är en kodsnutt som resulterar i en viss datatyp. När programmet körs, får uttrycket ett värde som kan användas i programmet.

Här följder några exempel på uttryck:

| Uttryck          | Värde     | Datatyp       | Datatyp i Python |
|------------------|-----------|---------------|------------------|
| `2 + 4 + 3`      | `9`       | heltal        | `int`            |
| `"abc" + "de"`   | `"abcde"` | sträng        | `str`            |
| `11 / 2`         | `5.5`     | flyttal       | `float`          |
| `2 * 5 > 9`      | `True`    | sanningsvärde | `bool`           |

Eftersom alla uttryck har en datatyp, kan de tilldelas till en variabel:

```python
# variabeln x får värdet på uttrycket 1 + 2
x = 1 + 2
```

Enkla uttryck kan kombineras för att få ett mera komplicerat uttryck till stånd. Så här kan man till exempel utföra räkneoperationer:

```python
# variabeln y får värdet på uttrycket "3 gånger x plus x upphöjt till två"
y = 3 * x + x**2
```

## Funktion

En funktion kör någon slags funktionalitet. Funktioner kan också ta emot en eller flera parametrar, alltså data som funktionen tar emot och behandlar.

En funktion körs då den anropas – det vill säga då funktionen och dess möjliga parametrar nämns i koden. Följande sats anropar `print`-funktionen med parametern `"det här är en parameter"`:

```python
print("det här är en parameter")
```

En annan funktion du redan känner till väl är `input`, som används för att ta emot data från användaren. Parametern i funktionen är det meddelande som ska visas till användaren:

```python
namn = input("Berätta ditt namn: ")
```

I det här fallet returnerar funktionen också ett värde. När funktionen har körts ersätts den del i koden där funktionen anropades med det värde som funktionen returnerar – det är nu ett uttryck med ett värde. `input`-funktionen returnerar en sträng som innehåller den text som användaren gett programmet. Värdet som en funktion returnerar lagras ofta i en variabel för att programmet ska kunna använda det senare.

## Datatyp

Datatyp syftar till de egenskaper ett värde har i ett program. I följande kodexempel är datatyperna sträng (`str`) för variabeln `namn` och heltal (`int`) för variabeln `resultat`:

```python
namn = "Anna"
resultat = 100
```

Med hjälp av funktionen `type` kan man ta reda på datatypen hos ett uttryck. Så här kan du använda funktionen:

```python
print(type("Anna"))
print(type(100))
```

<sample-output>

<class 'str'>
<class 'int'>

</sample-output>

## Syntax

På samma sätt som vanliga språk har regler för hur man skriver har även programmeringsspråk en syntax – det vill säga ett regelverk för hur koden ska skrivas. Den skiljer sig för varje programmeringsspråk.

Pythons syntax bestämmer bland annat att första raden i en if-sats ska sluta med ett kolon och att därefter följande block ska indenteras:

```python
if namn == "Anna":
    print("Hejsan!")
```

Följer man inte dessa regler, kommer ett fel att uppstå:

```python
if namn == "Anna"
    print("Hejsan!")
```

<sample-output>

<pre>
  File "testi.py", line 1
    if namn == "Anna"
                    ^
SyntaxError: invalid syntax
</pre>


</sample-output>

## Att debugga

När syntaxen i ett program är korrekt men programmet inte ändå fungerar på önskat sätt, finns det en bugg i programmet.

Buggar dyker upp i olika slags situationer. Vissa kan orsaka felmeddelanden medan programmet körs. Ta det här programmet som exempel:

```python
x = 10
y = 0
resultat = x / y

print(f"{x} dividerat med {y} är {resultat}")
```

Nu får vi felet:

<sample-output>

<pre>
ZeroDivisionError: integer division or modulo by zero on line 3
</pre>

</sample-output>

Det här felet har med matematik att göra – det går inte att dividera med noll, och det här stoppar programmet medan det körs.

Fel som uppstår medan programmet körs är relativt lätta att korrigera. Felmeddelandet berättar på vilken rad i koden det uppstod problem. Det är förstås möjligt att felet ligger på något annat ställe i koden än just den här specifika raden.

Ibland märker man en bugg eftersom det resultat som koden ger är fel. Att observera och hitta en sådan här bugg kan vara svårt. I programmeringsuppgifterna under den här kursen finns det olika tester som ska hjälpa med att hitta sådana här fel. Före en bugg kan korrigeras måste man ta reda på var felet uppstår.

Programmerare använder ofta termen debugga – att söka efter orsaker till fel som uppstår i koden. Det här är ett ytterst viktigt verktyg i en programmerares verktygslåda. I yrkeslivet använder programmerare ofta mera tid till att debugga än för att skriva ny kod.

Ett enkelt – men desto nyttigare – sätt att debugga sitt program är att lägga till `print`-satser i sin kod. Att verifiera vad som sker i koden med hjälp av print-instruktioner ger en bekräftelse att programmet gör det som du vill.

Det här är ett exempel på ett försök att lösa en av föregående modulens uppgifter:

```python
timlon = float(input("Timlön: "))
timmar = int(input("Arbetstimmar: "))
dag = input("Veckodag: ")

lon = timlon * timmar
if dag == "söndagg":
    lon * 2

print(f"Lön {lon} euro")
```

Det här programmet fungerar inte helt korrekt. När testen körs får vi följande resultat:

<sample-output>

<pre>
FAIL: PalkkaTest: test_sunnuntai_1

Syötteellä 23.0, 12, söndag oikeaa palkkaa 552.0 ei löydy tulosteestasi Lön 276.0 euro
</pre>

</sample-output>

När vi debuggar den här kursens uppgifter är det första steget ofta att testa hur programmet fungerar när man ger det den data som orsakade ett fel i testet. Nu kan vi se att programmet faktiskt ger ett inkorrekt resultat:

<sample-output>

Lön 276.0 euro

</sample-output>

Att debugga innebär vanligtvis att vi kör programmet flera gånger. Det kan vara händigt att tillfälligt hårdkoda det problematiska värdet istället för att alltid fråga efter värdet från användaren. Så här kunde det se ut i vårt exempel:

```python
# timlon = float(input("Timlön: "))
# timmar = int(input("Arbetstimmar: "))
# dag = input("Veckodag: ")
timlon = 23.0
timmar = 12
dag = "söndag"

lon = timlon * timmar
if dag == "söndagg":
    lon * 2

print(f"Lön {lon} euro")
```

Nästa steg kan vara att lägga till `print`-satser för att debugga. Problemet i den här koden uppstår i den delen där söndagar behandlas. Låt oss lägga till ett par print-satser: en före lönen ska fördubblas och en efter det:

```python
# ...

lon = timlon * timmar
if dag == "söndagg":
    print("lön i början:", lon)
    lon * 2
    print("lön efter fördubbling:", lon)

print(f"Lön {lon} euro")
```

När vi kör koden märker vi att programmet inte alls skriver ut något på basis av de `print`-satser vi lagt till i koden. Det verkar som att innehållet i `if`-blocket aldrig körs. Det finns visst ett problem med if-satsen. Låt oss skriva ut Boolean-uttryckets värde:

```python
# ...

lon = timlon * timmar
print("villkor:", dag=="söndagg")
if dag == "söndagg":
    print("lön i början:", lon)
    lon * 2
    print("lön efter fördubbling:", lon)

print(f"Lön {lon} euro")
```

Värdet är `False`, alltså kommer `if`-blockets kod aldrig att köras:

<sample-output>

villkor: False
Lön 276.0 euro

</sample-output>

Problemet ligger alltså i if-satsens villkor. Som i flera andra situationer inom programmering har bokstavsstorleken också skillnad när man jämför värden. Observera att "söndagg" i Boolean-uttrycket är skrivet med två g medan det i indatat inte är det. Vi korrigerar felet – både i if-satsen och `print`-instruktionen:

```python
# ...

lon = timlon * timmar
print("villkor:", dag=="söndag")
if dag == "söndag":
    print("lön i början:", lon)
    lon * 2
    print("lön efter fördubbling:", lon)

print(f"Lön {lon} euro")
```

Nu får vi följande utskrift när programmet körs:

<sample-output>

villkor: True
lön i början: 276.0
lön efter fördubbling: 276.0
Lön 276.0 euro

</sample-output>

Det verkar som att värdet lagrat i `lon` är korrekt i början: `timlon = 20.0` och `timmar = 12`, 20,0 * 6 = 120,0. Instruktionen som ska multiplicera det här med två fungerar dock inte. Det måste alltså vara ett problem med den instruktionen:

```python
lon * 2
```

Instruktionen multiplicerar nog värdet, men resultatet lagras ingenstans. Vi ändrar på det:

```python
lon *= 2
```

När vi nu kör programmet, märker vi att resultatet är korrekt:

<sample-output>

villkor:  True
lön i början: 276.0
lön efter fördubbling: 552.0
Lön 552.0 euro

</sample-output>

När programmet fungerar som det ska, är det viktigt att ta bort `print`-satser och annan kod som använts för att debugga.

Det här var ett ganska enkelt exempel och i fall som det här kan man eventuellt hitta buggar genom att läsa igenom koden med omtanke. Att använda `print`-satser för att debugga är ändå ofta ett snabbt sätt att få en ledtråd för var problemet kan ligga. `print`-satser kan också användas för att fastställa vilka delar av koden som fungerar korrekt. Då kan man fokusera på andra ställen där buggar med större sannolikhet gömmer sig.

`print`-satser är bara ett sätt att debugga program. Vi återkommer till det här ämnet senare under kursen. Nu ska du bli van vid att debugga, med hjälp av `print`-instruktioner, för att hitta problematiska delar i din kod. Proffs klarar sig inte utan `print`-satser i debuggningssyfte – det är alltså en viktig resurs redan som nybörjare.

<in-browser-programming-exercise name="Fixa felen" tmcname="osa02-01_fixa_felen" height="400px">

I följande program finns flera syntaxfel. Korrigera dem så att programmet fungerar enligt nedan presenterade exempel.

```python
  nummer = input("Ge en siffra: ")
  if nummer>100
    print("Siffran är större än 100")
    nummer - 100
    print("Nu har siffran blivit 100 mindre)
     print("Värdet är nu"+ nummer)
 print(nummer + " är visst mitt lyckotal!")
 print("Ha en trevlig fortsättning på dagen!)
```

<sample-output>

Ge en siffra: **13**
13 är visst mitt lyckotal!
Ha en trevlig fortsättning på dagen!

</sample-output>

<sample-output>

Ge en siffra: **101**
Siffran är större än 100
Nu har siffran blivit 100 mindre
Värdet är nu 1
1 är visst mitt lyckotal!
Ha en trevlig fortsättning på dagen!

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Antalet tecken" tmcname="osa02-02_antalet_tecken">

Med funktionen `len` kan man bland annat räkna längden på en sträng. Funktionen returnerar antalet tecken i strängen.

Exempel:

```python
ord = "abcd"
print(len(ord))

print(len("hejsan"))

ord2 = "tjingeling"
langd = len(ord2)
print(langd)

tom_strang = ""
langd = len(tom_strang)
print(langd)
```

<sample-output>

4
6
10
0

</sample-output>

Skapa ett program som ber användaren mata in ett ord. Programmet ska därefter skriva ut antalet tecken, om antalet överstiger ett.

Exempel:

<sample-output>

Ge ett ord: hej
I ordet hej finns det 3 bokstäver
Tack!

</sample-output>

<sample-output>

Ge ett ord: basilika
I ordet basilika finns det 8 bokstäver
Tack!

</sample-output>

<sample-output>

Ge ett ord: b
Tack!

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Konvertera värden" tmcname="osa02-03_konvertera_varden">

I Python kan man ofta konvertera ett värde från en datatyp till en annan. Ett flyttal kan till exempel konverteras till ett heltal med funktionen `int`:

```python
temperatur = float(input("Ange temperatur: "))

print("Temperaturen är", temperatur)

print("Alltså ungefär", int(temperatur))
```

<sample-output>

Ange temperatur: **5.15**
Temperaturen är 5.15
Alltså ungefär 5

</sample-output>

Observera att funktionen inte avrundar värdet på det sättet vi kunde anta från matematiken. Siffran avrundas alltid nedåt (golvfunktion):

<sample-output>

Ange temperatur: **8.99**
Temperaturen är 8.99
Alltså ungefär 8

</sample-output>

Använd `int`-funktionen för att skapa ett program som frågar om ett decimaltal från användaren. Programmet ska därefter skriva ut heltals- och decimaldelen av talet på skilda rader.

Du kan anta att det givna decimaltalet är större än noll.

Exempel:

<sample-output>

Ge en siffra: **1.34**
Heltalsdel: 1
Decimaldel: 0.34

</sample-output>

</in-browser-programming-exercise>

<quiz id="02c9e0da-7357-5476-a478-ec1b0cad2b1f"></quiz>
