---
path: '/osa-7/1-moduler'
title: 'Moduler'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* vet du vad en Python-modul är
* vet du hur man inkluderar en modul i ett program med `import`-satsen
* vet du hur man hittar mera information om innehållet i en modul.

</text-box>

## Lite mera om debuggande

Vi har redan bekantat oss med flera olika debuggningsmetoder under kursen. Till exempel borde [visualiseringsverktyget](https://pythontutor.com/visualize.html) och användningen av `print`-satser för debuggning vara bekanta. Du har kanske också testat det inbyggda debuggningsverktyget i Visual Studio Code. Om du har problem med att debuggaren inte hittar dina filer, kan du bekanta dig med några tips från förra veckan.

Från och med version 3.7 erbjuder Python också ett ytterligare sätt för att debugga program, nämligen instruktionen [`breakpoint()`](https://docs.python.org/3/library/functions.html#breakpoint).

Du kan lägga till den här instruktionen på valfritt ställe i din kod (kom dock ihåg att följa syntaxreglerna). När programmet körs, kommer programmet att stanna på det ställe där `breakpoint`-instruktionen finns. Här är ett exempel där vi debuggar en uppgiftslösning från förra veckan:

<img src="7_1_1.png">

När programmet stannar vid en `breakpoint`-instruktion kommer ett interaktivt terminalfönster att öppnas. Här kan du skriva kod på samma sätt som i en normal Pythonterminal. Du ser hur koden fungerar exakt vid den här punkten i ditt program.

Instruktionen `breakpoint` är speciellt nyttig då du vet att någon kodrad orsakar ett fel, men du är osäker på varför. Lägg till en breakpoint just före den problematiska kodraden och kör ditt program. Då kan du göra ändringar och köra koden i den interaktiva terminalen för att lista ut vad som behöver ändras i programmet. 

Det är också möjligt att fortsätta att köra programmet efter att det stannat. Med `continue` (kort `c`) i terminalen får vi programmet att fortsätta fram till följande eventuella breakpoint. Den här bilden illustrerar en situation där en loop har upprepat några gånger:

<img src="7_1_2.png">

Vi kan också använda andra nyckelord i debuggningsterminalen. Du kan hitta dem [här](https://docs.python.org/3/library/pdb.html#debugger-commands) eller så kan du skriva `help` i terminalen:

<img src="7_1_3.png">

För att avsluta använder vi `exit`.

Kom ihåg att ta bort alla `breakpoint` ur koden då du har debuggat klart!

## Använda moduler

Python i sig innehåller redan en del nyttiga funktioner som `len` (returnerar längden på en sträng eller en lista) och `sum` (returnerar summan av element i en datastruktur). Dessa hjälper dig som programmerare till viss del. Pythons standardbibliotek är en samling standardiserade funktioner och objekt som utökar vår programmeringsverktygslåda. Vi har redan använt en del av funktionerna i Pythons standardbibliotek i de tidigare övningarna – till exempel då vi räknade med kvadratrötter.

Standardbiblioteket består av moduler. De innehåller funktioner och klasser som är grupperade kring olika teman och funktionaliteter. I den här modulen kommer vi att bekanta oss med några nyttiga Python-moduler. Vi lär oss också att skapa egna moduler.

Instruktionen `import` gör allt innehåll i en given modul tillgängligt i ett program. Vi tar en närmare titt på hur vi kan använda modulen `math`. Den innehåller matematiska funktioner som `sqrt` för kvadratrot och `log` för logaritm.

```python
import math

# kvadratroten av fem
print(math.sqrt(5))
# logaritmen av åtta (bas två)
print(math.log(8, 2))
```

<sample-output>

2.23606797749979
3.0

</sample-output>

Funktionerna är definierade i modulen `math`, och vi behöver ange detta då vi vill använda dem. Det gör vi med punktnotation (modulnamn.funktionsnamn), dvs. `math.sqrt` och `math.log`.

## Välja specifika delar från en modul

Ett annat sätt att använda moduler är att välja ut specifika delar med `from`-instruktionen. Om vi endast vill använda funktionerna `sqrt` och `log` från modulen `math`, behöver vi inte importera hela modulen. I stället kan vi göra så här: 

```python
from math import sqrt, log

print(sqrt(5))
print(log(5,2))
```

Då vi importerar och använder delar ur en modul med from...import, behöver vi inte ange vilken modul funktionerna finns i. 

Vid behov kan man använda sig av en asterisk för att importera allt innehåll i en modul så att vi inte behöver ange modulens namn:

```python
from math import *

print(sqrt(5))
print(log(5,2))
```

Att importera modulers innehåll direkt med hjälp av from...import  kan vara nyttigt då man prövar olika funktioner eller arbetar med mindre projekt. Det kan däremot också ställa till med problem, vilket vi kommer att se lite senare.

<programming-exercise name='Hypotenusa' tmcname='osa07-01_hypotenusa'>

Skapa funktionen `hypotenusa(katet1: float, katet2: float)` som tar kateternas längder i en rätvinklig triangel som argument. Funktionen ska returnera hypotenusans längd.

Använd [Pythagoras sats](https://sv.wikipedia.org/wiki/Pythagoras_sats). Kvadratroten kan du beräkna med motsvarande funktion i `math`-modulen.

Exempel:

```python
print(hypotenusa(3,4)) # 5.0
print(hypotenusa(5,12)) # 13.0
print(hypotenusa(1,1)) # 1.4142135623730951
```

</programming-exercise>

## Innehållet i en modul

Pythons dokumentation inkluderar mycket information om alla moduler som är tillgängliga i standardbiblioteket. Dokumentationen berättar om funktioner och metoder som är definierade i en modul, och därtill får man veta hur modulen kan användas. Som ett exempel hittar du här en länk till `math`-modulens dokumentation:

* https://docs.python.org/3/library/math.html

Vi kan också kolla på innehållet i en modul med funktionen `dir`:

```python
import math

print(dir(math))
```

Den här funktionen returnerar en lista på namn som finns definierade i modulen. Det kan vara namn på klasser, konstanta värden eller funktioner:

<sample-output>

['\_\_doc\_\_', '\_\_name\_\_', '\_\_package\_\_', 'acos', 'acosh', 'asin', 'asinh', 'atan', 'atan2', 'atanh', 'ceil', 'copysign', 'cos', 'cosh', 'degrees', 'e', 'erf', 'erfc', 'exp', 'expm1', 'fabs', 'factorial', 'floor', 'fmod', 'frexp', 'fsum', 'gamma', 'hypot', 'isinf', 'isnan', 'ldexp', 'lgamma', 'log', 'log10', 'log1p', 'modf', 'pi', 'pow', 'radians', 'sin', 'sinh', 'sqrt', 'tan', 'tanh', 'trunc']

</sample-output>

<programming-exercise name='Specialtecken' tmcname='osa07-02_specialtecken'>

I [modulen `string`](https://docs.python.org/3/library/string.html) finns strängkonstanter som definierar specifika teckengrupper (t.ex. gemener och skiljetecken). Bekanta dig med dessa konstanter och skapa funktionen `dela_upp(strang: str)` som tar som argument en sträng som ska returneras uppdelad i tre delar:

1. en sträng med alla gemener och versaler (enligt engelska alfabetet), konstanten `ascii_letters`
1. en sträng med de tecken som definieras i konstanten `punctuation`
1. en sträng med resterande tecken (t.ex. mellanslag och skandinaviska tecken)

Tecknen ska förekomma i samma ordning som i den ursprungliga strängen.

Exempel:

```python
delar = dela_upp("Det här är ett test, fungerar det?? åå")
print(delar[0])
print(delar[1])
print(delar[2])
```

<sample-output>

Dethrretttestfungerardet
,??
 ä ä     åå

</sample-output>

</programming-exercise>

<programming-exercise name='Bråk' tmcname='osa07-03_brak'>

Bekanta dig med Pythonmodulen `fractions` och implementera funktionen `delar(antal: int)` som får ett antal som argument. Funktionen ska dela upp talet ett i så många delar som argumentet antal anger, och sedan returnera delarna i en lista.

Exempel:

```python
for p in delar(3):
    print(p)

print()

print(delar(5))
```

<sample-output>

1/3
1/3
1/3

[Fraction(1, 5), Fraction(1, 5), Fraction(1, 5), Fraction(1, 5), Fraction(1, 5)]

</sample-output>

</programming-exercise>

<quiz id="ddcf5f21-b32f-5bc5-9137-d75f7f83bb73"></quiz>
