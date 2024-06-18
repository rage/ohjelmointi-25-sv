---
path: '/osa-7/1-moduulit'
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

Vi har redan bekantat oss med en hel del olika debuggningsmetoder under den här kursen. [Visualiseringsverktyget](https://pythontutor.com/visualize.html) och `print`-satser för debuggning är redan bekanta för dig. Du har kanske också testat på det inbyggda debuggningsverktyget i Visual Studio Code. Om du har problem med att debuggaren inte hittar dina filer, kan du bekanta dig med några tips från den förra modulen.

Sedan versionen 3.7 av Python finns ett ytterligare sätt att debugga program: kommandot [`breakpoint()`](https://docs.python.org/3/library/functions.html#breakpoint).

Du kan lägga till det här kommandot på valfritt ställe i din kod (kom dock ihåg att följa reglerna som gäller syntax). När programmet körs, kommer programmet att stanna på det ställe där `breakpoint`-kommandot finns. Här är ett exempel där vi debuggar en uppgiftslösning från den förra modulen:

<img src="7_1_1.png">

När programmet stannar upp vid ett `breakpoint`-kommando kommer ett interaktivt terminalfönster att öppnas. Här kan du skriva kod på samma sätt som i en normal Pythonterminal. Du ser hur koden fungerar exakt vid den här punkten i ditt program.

Kommandot `breakpoint` är speciellt nyttigt då du vet att någon kodrad orsakar ett fel, men du är osäker på orsaken till det. Lägg till en breakpoint just före den problematiska kodraden och kör ditt program. Nu kan du testa på olika saker i den interaktiva terminalen och lista ut vad som måste ändras på i ditt program.

Det är också möjligt att fortsätta körandet av programmet där det stannat upp. Kommandot `continue` (kort `c`) i terminalen får programmet att fortsätta tills nästa breakpoint nås. Den här bilden illustrerar en situation där en loop har upprepat några gånger:

<img src="7_1_2.png">

Det finns också några andra kommandon tillgängliga i debuggningsterminalen. Du kan hitta dem [här](https://docs.python.org/3/library/pdb.html#debugger-commands) eller så kan du skriva `help` i debuggningsterminalen:

<img src="7_1_3.png">

Kommandot `exit` avslutar programmet.

När du är klar med debuggandet ska du minnas att ta bort `breakpoint`-kommandona från din kod!

## Använda moduler

Python i sig innehåller redan en del nyttiga funktioner som `len` (returnerar längden på en sträng eller en lista) och `sum` (returnerar summan av element i en datastruktur). Dessa hjälper dock dig som programmerare bara till en viss del. Pythons standardbibliotek är en samling av standardiserade funktioner och objekt som kan utöka Pythons "uttryckskraft". Vi har redan använt en del av funktionerna i Pythons standardbibliotek i de tidigare övningarna – till exempel då vi räknade med kvadratrötter.

Standardbiblioteket består av moduler. De innehåller funktioner och klasser som är grupperade kring olika teman och funktionaliteter. I den här modulen kommer vi att bekanta oss med några nyttiga Python-moduler. Vi lär oss också att skapa egna moduler.

Kommandot `import` gör innehållet i en given modul tillgängligt i ett program. Vi tar en närmare titt på hur vi kan använda modulen `math`. Den innehåller matematiska funktioner som `sqrt` för kvadratrot och `log` för logaritm.

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

Funktionerna är definierade i modulen `math`, så de måste hänvisas till med notationerna `math.sqrt` och `math.log` i koden.

## Välja specifika delar från en modul

Ett annat sätt att använda moduler är att välja specifika delar av modulen med `from`-kommandot. Om vi endast vill använda funktionerna `sqrt` och `log` från modulen `math`, kan vi göra på följande sätt:

```python
from math import sqrt, log

print(sqrt(5))
print(log(5,2))
```

Som du ser ovan, behöver vi inte `math`-prefixet då vi importerar och använder funktioner på det här sättet.

Vid behov kan man använda sig av en asterisk för att importera allt innehåll i en modul:

```python
from math import *

print(sqrt(5))
print(log(5,2))
```

Det här sättet att importera moduler kan vara nyttigt då man testar på något eller arbetar med ett mindre projekt. Det kan däremot orsaka problem, vilket vi kommer att se lite senare.

<programming-exercise name='Hypotenusa' tmcname='osa07-01_hypotenuusa'>

Skapa funktionen `hypotenusa(katet1: float, katet2: float)` som får som argument kateternas längder i en rätvinklig triangel. Funktionen ska returnera hypotenusans längd.

Använd [Pythagoras sats](https://sv.wikipedia.org/wiki/Pythagoras_sats). Kvadratroten kan du räkna med den relevanta funktionen i `math`-modulen.

Exempel:

```python
print(hypotenusa(3,4)) # 5.0
print(hypotenusa(5,12)) # 13.0
print(hypotenusa(1,1)) # 1.4142135623730951
```

</programming-exercise>

## Innehållet i en modul

Pythons dokumentation inkluderar mycket information om alla moduler som är tillgängliga i standardbiblioteket. Dokumentationen berättar om funktioner och metoder som är definierade i en modul, och därtill får man veta hur modulen kan användas. Som ett exempel följer en länk till `math`-modulens dokumentation:

* https://docs.python.org/3/library/math.html

Vi kan också kolla på innehållet i en modul med funktionen `dir`:

```python
import math

print(dir(math))
```

Den här funktionen returnerar en lista av namn definierade av modulen. Det kan vara namn på klasser, fixerade värden eller funktioner:

<sample-output>

['\_\_doc\_\_', '\_\_name\_\_', '\_\_package\_\_', 'acos', 'acosh', 'asin', 'asinh', 'atan', 'atan2', 'atanh', 'ceil', 'copysign', 'cos', 'cosh', 'degrees', 'e', 'erf', 'erfc', 'exp', 'expm1', 'fabs', 'factorial', 'floor', 'fmod', 'frexp', 'fsum', 'gamma', 'hypot', 'isinf', 'isnan', 'ldexp', 'lgamma', 'log', 'log10', 'log1p', 'modf', 'pi', 'pow', 'radians', 'sin', 'sinh', 'sqrt', 'tan', 'tanh', 'trunc']

</sample-output>

<programming-exercise name='Specialtecken' tmcname='osa07-02_erikoismerkit'>

I [modulen `string`](https://docs.python.org/3/library/string.html) finns strängkonstanter som definiar specifika teckengrupper (t.ex. gemener och skiljetecken). Bekanta dig med dessa konstanter och skapa funktionen `dela_upp(strang: str)` som får som argument en sträng som ska returneras uppdelad i tre delar:

1. en sträng med alla gemener och versaler (enligt engelska alfabetet), konstanten `ascii_letters`
1. en sträng med tecknen som definieras i konstanten `punctuation`
1. en sträng med de resterade tecknen (t.ex. mellanslag)

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

<programming-exercise name='Bråk' tmcname='osa07-03_murtoluvuilla_laskeminen'>

Bekanta dig med Pythonmodulen `fractions` och implementera funktionen `delar(antal: int)` som får som argument ett antal delar. Funktionen ska dela upp talet ett i så här många delar och returnera delarna i en lista.

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

<quiz id="26b53ed8-0c22-573e-a0e9-60b89ef34855"></quiz>
