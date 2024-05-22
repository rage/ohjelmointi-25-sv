---
path: '/osa-2/1-ohjelmoinnin-termeja'
title: 'Programmeringsterminologi'
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* känner du till de väsentligaste termerna inom programmering
* vet du vad skillnaden mellan en sats och ett uttryck är
* kan du ta reda på datatypen på värdet av ett uttryck
* har du lärt dig hur du genom att debugga hittar fel i din kod.

</text-box>

Under den första modulen fokuserade vi inte så mycket på terminologi. Nu är det dags att ta en titt på några centrala begrepp inom programmering.

## Sats

En sats (statement) är en del av ett program som kör någonting. En sats syftar ofta, men inte alltid, till ett enstaka kommando.

Till exempel `print("Hej")` är en sats som skriver ut en rad text. På samma sätt är `nummer = 2` en sats som lagrar ett värde i en variabel.

En sats kan också vara mera invecklad. Den kan till exempel bestå av flera satser. Följande sats består av tre rader:

```python
if nimi == "Anna":
    print("Moi!")
    luku = 2
```

Ovan finns två satser (print-sats och tilldelningssats) inom en if-sats.

## Block

Ett block är en grupp av efter varandra följande satser som är på samma nivå i programmets struktur. Till exempel if-satsens block innehåller de satser som körs då villkoret är sant.

```python
if ika > 17:
    # ehtolauseessa oleva lohko alkaa
    print("Olet täysi-ikäinen!")
    ika = ika + 1
    print("nyt vuoden vanhempi...")
    # lohko loppuu

print("tämä on eri lohkossa")
```

I Python markeras block genom att indentera all kod i blocket med samma antal mellanrum.

Obs! Pythons huvudblock ska aldrig indenteras, utan ska alltid vara så långt till vänster som möjligt i filen:

```python
# tämä ohjelma ei toimi sillä koodia ei ole sisennetty vasempaan reunaan
  print("hei maailma")
  print("huono ohjelma...")
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
# muuttuja x saa arvoksi lausekkeen 1 + 2 arvon
x = 1 + 2
```

Enkla uttryck kan kombineras för att få ett mera komplicerat uttryck till stånd. Så här kan man till exempel utföra räkneoperationer:

```python
# muuttuja y saa arvoksi lausekkeen '3 kertaa x plus x toiseen' arvon
y = 3 * x + x**2
```

## Funktion

En funktion kör någon slags funktionalitet. Funktioner kan också ta emot en eller flera parametrar, alltså data som funktionen tar emot och behandlar.

En funktion körs då den anropas – det vill säga då funktionen och dess möjliga parametrar nämns i koden. Följande sats anropar `print`-funktionen med parametern `"det här är en parameter"`:

```python
print("tämä on parametri")
```

En annan funktion du redan känner till väl är `input`, som används för att ta emot data från användaren. Parametern i funktionen är det meddelande som ska visas till användaren:

```python
nimi = input("Kerro nimesi: ")
```

I det här fallet returnerar funktionen också ett värde. När funktionen har körts ersätts den del i koden där funktionen anropades med det värde som funktionen returnerar – det är nu ett uttryck med ett värde. `input`-funktionen returnerar en sträng som innehåller den text som användaren gett programmet. Värdet som en funktion returnerar lagras ofta i en variabel för att programmet ska kunna använda det senare.

## Datatyp

Datatyp syftar till de egenskaper ett värde har i ett program. I följande kodexempel är datatyperna sträng (`str`) för variabeln `namn` och heltal (`int`) för variabeln `resultat`:

```python
nimi = "Anna"
tulos = 100
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
if nimi == "Anna":
    print("Moi!")
```

Följer man inte dessa regler, kommer ett fel att uppstå:

```python
if nimi == "Anna"
    print("Moi!")
```

<sample-output>

<pre>
  File "testi.py", line 1
    if nimi == "Anna"
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
tulos = x / y

print(f"{x} jaettuna {y} on {tulos}")
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

Ett enkelt – men desto nyttigare – sätt att debugga sitt program är att lägga till `print`-satser i sin kod. Att verifiera vad som sker i koden med hjälp av print-kommandon ger en bekräftelse att programmet gör det som du vill.

Det här är ett exempel på ett försök att lösa en av föregående modulens uppgifter:

```python
tuntipalkka = float(input("Tuntipalkka: "))
tunnit = int(input("Työtunnit: "))
paiva = input("Viikonpäivä: ")

palkka = tuntipalkka * tunnit
if paiva == "sunnnuntai":
    palkka * 2

print(f"Palkka {palkka} euroa")
```

Det här programmet fungerar inte helt korrekt. När testen körs får vi följande resultat:

<sample-output>

<pre>
FAIL: PalkkaTest: test_sunnuntai_1

Syötteellä 23.0, 12, sunnuntai oikeaa palkkaa 552.0 ei löydy tulosteestasi Palkka 276.0 euroa
</pre>

</sample-output>

När vi debuggar den här kursens uppgifter är det första steget ofta att testa hur programmet fungerar när man ger det den data som orsakade ett fel i testet. Nu kan vi se att programmet faktiskt ger ett inkorrekt resultat:

<sample-output>

Palkka 276.0 euroa

</sample-output>

Att debugga innebär vanligtvis att vi kör programmet flera gånger. Det kan vara händigt att tillfälligt hårdkoda det problematiska värdet istället för att alltid fråga efter värdet från användaren. Så här kunde det se ut i vårt exempel:

```python
# tuntipalkka = float(input("Tuntipalkka: "))
# tunnit = int(input("Työtunnit: "))
# paiva = input("Viikonpäivä: ")
tuntipalkka = 23.0
tunnit = 12
paiva = "sunnuntai"

palkka = tuntipalkka * tunnit
if paiva == "sunnnuntai":
    palkka * 2

print(f"Palkka {palkka} euroa")
```

Nästa steg kan vara att lägga till `print`-satser för att debugga. Problemet i den här koden uppstår i den delen där söndagar behandlas. Låt oss lägga till ett par print-satser: en före lönen ska fördubblas och en efter det:

```python
# ...

palkka = tuntipalkka * tunnit
if paiva == "sunnnuntai":
    print("palkka alussa:", palkka)
    palkka * 2
    print("palkka kasvatuksen jälkeen:", palkka)

print(f"Palkka {palkka} euroa")
```

När vi kör koden märker vi att programmet inte alls skriver ut något på basis av de `print`-satser vi lagt till i koden. Det verkar som att innehållet i `if`-blocket aldrig körs. Det finns visst ett problem med if-satsen. Låt oss skriva ut Boolean-uttryckets värde:

```python
# ...

palkka = tuntipalkka * tunnit
print("ehto:", paiva=="sunnnuntai")
if paiva == "sunnnuntai":
    print("palkka alussa:", palkka)
    palkka * 2
    print("palkka kasvatuksen jälkeen:", palkka)

print(f"Palkka {palkka} euroa")
```

Värdet är `False`, alltså kommer `if`-blockets kod aldrig att köras:

<sample-output>

ehto:  False
Palkka 276.0 euroa

</sample-output>

Problemet ligger alltså i if-satsens villkor. Som i flera andra situationer inom programmering har bokstavsstorleken också skillnad när man jämför värden. Observera att "Söndag" i Boolean-uttrycket är skrivet med en stor bokstav medan det i indatat inte är det. Vi korrigerar det – både i if-satsen och `print`-kommandot:

```python
# ...

palkka = tuntipalkka * tunnit
print("ehto:", paiva=="sunnuntai")
if paiva == "sunnuntai":
    print("palkka alussa:", palkka)
    palkka * 2
    print("palkka kasvatuksen jälkeen:", palkka)

print(f"Palkka {palkka} euroa")
```

Nu får vi följande utskrift när programmet körs:

<sample-output>

ehto: True
palkka alussa: 276.0
palkka kasvatuksen jälkeen: 276.0
Palkka 276.0 euroa

</sample-output>

Det verkar som att värdet lagrat i `dagslon` är korrekt i början: `timlon = 20.0` och `timmar = 12`, 20,0 * 6 = 120,0. Kommandot som ska multiplicera det här med två fungerar dock inte. Det måste alltså vara ett problem med det kommandot:

```python
palkka * 2
```

Kommandot multiplicerar nog värdet, men resultatet lagras ingenstans. Vi ändrar på det:

```python
palkka *= 2
```

När vi nu kör programmet, märker vi att resultatet är korrekt:

<sample-output>

ehto:  True
palkka alussa: 276.0
palkka kasvatuksen jälkeen: 552.0
Palkka 552.0 euroa

</sample-output>

När programmet fungerar som det ska, är det viktigt att ta bort `print`-satser och annan kod som använts för att debugga.

Det här var ett ganska enkelt exempel och i fall som det här kan man eventuellt hitta buggar genom att läsa igenom koden med omtanke. Att använda `print`-satser för att debugga är ändå ofta ett snabbt sätt att få en ledtråd för var problemet kan ligga. `print`-satser kan också användas för att fastställa vilka delar av koden som fungerar korrekt. Då kan man fokusera på andra ställen där buggar med större sannolikhet gömmer sig.

`print`-satser är bara ett sätt att debugga program. Vi återkommer till det här ämnet senare under kursen. Nu ska du bli van vid att debugga, med hjälp av `print`-kommandon, för att hitta problematiska delar i din kod. Proffs klarar sig inte utan `print`-satser i debuggningssyfte – det är alltså en viktig resurs redan som nybörjare.

<in-browser-programming-exercise name="Korjaa virheet" tmcname="osa02-01_korjaa_virheet" height="400px">

Seuraavassa ohjelmassa on useita _syntaksivirheitä_. Korjaa ohjelma siten, että syntaksi on kunnossa ja se toimii alla olevien esimerkkien mukaisesti.

```python
  luku = input("Anna luku: ")
  if luku>100
    print("Luku oli suurempi kuin sata")
    luku - 100
    print("Nyt luvun arvo on pienentynyt sadalla)
     print("Arvo on nyt"+ luku)
 print(luku + " taitaa olla onnenlukuni!")
 print("Hyvää päivänjatkoa!)
```

<sample-output>

Anna luku: **13**
13 taitaa olla onnenlukuni!
Hyvää päivänjatkoa!

</sample-output>

<sample-output>

Anna luku: **101**
Luku oli suurempi kuin sata
Nyt luvun arvo on pienentynyt sadalla
Arvo on nyt 1
1 taitaa olla onnenlukuni!
Hyvää päivänjatkoa!

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Merkkien määrä" tmcname="osa02-02_merkkien_maara">

Funktiolla `len` voidaan laskea (muun muassa) merkkijonon pituus. Funktio palauttaa merkkijonossa olevien merkkien määrän.

Esimerkkejä funktion toiminnasta:

```python
sana = "abcd"
print(len(sana))

print(len("moikka"))

sana2 = "heipparallaa"
pituus = len(sana2)
print(pituus)

tyhja_merkkijono = ""
pituus = len(tyhja_merkkijono)
print(pituus)
```

<sample-output>

4
6
12
0

</sample-output>

Tee ohjelma, joka lukee käyttäjältä sanan ja tulostaa sanan merkkien määrän, mikäli niitä on enemmän kuin yksi.

Esimerkkisuorituksia:

<sample-output>

Anna sana: hei
Sanassa hei on 3 kirjainta
Kiitos!

</sample-output>

<sample-output>

Anna sana: banaani
Sanassa banaani on 7 kirjainta
Kiitos!

</sample-output>

<sample-output>

Anna sana: b
Kiitos!

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Tyyppimuunnos" tmcname="osa02-03_tyyppimuunnos">

Pythonissa voidaan usein muuntaa jokin arvo tyypistä toiseen. Esimerkiksi liukuluku voidaan muuntaa kokonaisluvuksi funktion `int` avulla:

```python

lampo = float(input("Anna lämpötila: "))

print("Lämpötila on", lampo)

print("...eli pyöreästi", int(lampo))

```

<sample-output>

Anna lämpötila: **5.15**
Lämpötila on 5.15
...eli pyöreästi 5

</sample-output>

Huomaa, että funktio ei pyöristä arvoa matematiikasta tutulla tavalla, vaan pyöristää luvun alaspäin (kyse on siis ns. _lattiafunktiosta_):

<sample-output>

Anna lämpötila: **8.99**
Lämpötila on 8.99
...eli pyöreästi 8

</sample-output>

Tee int-funktiota hyödyntäen ohjelma, joka kysyy käyttäjältä desimaaliluvun ja tulostaa erikseen luvun kokonaisosan ja desimaaliosan.

Huom! Voit olettaa, että annettu desimaaliluku on suurempi kuin nolla.

Esimerkiksi

<sample-output>

Anna luku: **1.34**
Kokonaisosa: 1
Desimaaliosa: 0.34

</sample-output>

</in-browser-programming-exercise>

<quiz id="83116ef2-ab65-5403-8721-d6c0ba32f7d4"></quiz>
