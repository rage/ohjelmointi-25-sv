---
path: '/osa-2/3-ehtojen-yhdistäminen'
title: 'Kombinera villkor'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* vet du hur man använder operatorerna `and`, `or` och `not` i villkor
* kan du skriva kapslade if-satser.

</text-box>

## Logiska operatorer

Du kan kombinera villkor med de logiska operatorerna `and` och `or`. Operatorn `and` innebär att alla villkor måste vara sanna samtidigt. Operatorn `or` kräver att minst ett av villkoren ska vara sant.

Till exempel villkoret `nummer >= 5 and nummer <= 8` bestämmer att nummer måste samtidigt vara minst fem och högst åtta – alltså mellan fem och åtta.

```python
nummer = int(input("Ge en siffra: "))
if nummer >= 5 and nummer <= 8:
    print("Siffran är mellan 5 och 8")
```

Villkoret `nummer < 5 or nummer > 8` bestämmer att nummer måste vara mindre än fem eller större än åtta – alltså inte mellan fem till åtta.

```python
nummer = int(input("Ge en siffra: "))
if nummer < 5 or nummer > 8:
    print("Siffran är inte mellan 5 och 8")
```

Den här sanningstabellen beskriver hur operatorerna fungerar i olika situationer:

a     | b     | a and b | a or b |
:----:|:-----:|:-------:|:------:|
False | False | False   | False  |
True  | False | False   | True   |
False | True  | False   | True   |
True  | True  | True    | True   |

Ibland kan det vara händigt att veta om något värde inte är sant. Operatorn `not` byter värdet på ett villkor till det motsatta:


a     | not a
:----:|:-----:
True  | False
False | True

Det ovanstående exemplet med talen 5–8 borträknade kan också skrivas så här:

```python
nummer = int(input("Ge en siffra: "))
if not (nummer >= 5 and nummer <= 8):
    print("Siffran är inte mellan 5 och 8")
```

Framför allt inom programmering kallas logiska operatorer Boolean-operatorer.


<text-box variant='hint' name='Kombinerade villkor – förenklat'>

Villkoret `x >= a and x <= b` är ett mycket vanligt sätt att bestämma om talet `x` är i intervallet `a` till `b`. Den här strukturen fungerar i flera programmeringsspråk.

Python ger också oss möjligheten att använda oss av ett förenklat uttryckssätt för att kombinera villkor: `a <= x <= b` ger samma resultat som den längre versionen med `and`. Den här notationen är kanske bekant från matematikens värld men den används inte så ofta i Python – kanske för att många andra programmeringsspråk saknar liknande syntax.

</text-box>

## Kombinera och kedja villkor

Det här programmet ber användaren att ge fyra siffror. Sedan kollar programmet vilken siffra som är störst med hjälp av några villkor:

```python
n1 = int(input("Ge siffra 1: "))
n2 = int(input("Ge siffra 2: "))
n3 = int(input("Ge siffra 3: "))
n4 = int(input("Ge siffra 4: "))

if n1 > n2 and n1 > n3 and n1 > n4:
    storst = n1
elif n2 > n3 and n2 > n4:
    storst = n2
elif n3 > n4:
    storst = n3
else:
    storst = n4

print(f" {storst} är det största talet.")
```

<sample-output>

Ge siffra 1: **2**
Ge siffra 2: **4**
Ge siffra 3: **1**
Ge siffra 4: **1**
4 är det största talet.

</sample-output>

I exemplet ovan är `n1 > n2 and n1 > n3 and n1 > n4` sant endast då alla tre "delvillkor" är sanna.

<in-browser-programming-exercise name="Kontroll av ålder" tmcname="osa02-08_ian_tarkistus">

Skapa ett program som frågar om användarens ålder. Om åldern är under fem, ska programmet kommentera det här.

Se exemplen nedan:

<sample-output>

Vad är din ålder? **13**
Okej, du är alltså 13 år

</sample-output>

<sample-output>

Vad är din ålder? **2**
Jag tror inte att du kan skriva...

</sample-output>

<sample-output>

Vad är din ålder? **-4**
Du måste ha skrivit fel.

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Brorsöner" tmcname="osa02-09_veljenpojat">

Skapa ett program som frågar efter användarens namn. Om namnet är Knatte, Fnatte eller Tjatte, antar programmet att användaren är Kalle Ankas brorson.

Om namnet är Teddi eller Freddi, antar programmet att användaren är Musse Piggs brorson.

Exempel:

<sample-output>

Ange ditt namn: **Teddi**
Du är antagligen Musse Piggs brorson.

</sample-output>

<sample-output>

Ange ditt namn: **Fnatte**
Du är antagligen Kalle Ankas brorson.

</sample-output>

<sample-output>

Ange ditt namn: **Kid**
Jag vet inte vems brorson du är.

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Vitsord och poäng" tmcname="osa02-10_arvosana_ja_pisteet">

Följande tabell beskriver hur vitsordet på en kurs räknas. Skapa ett program som meddelar vitsordet på basis av den här tabellen.

Poäng  | Vitsord
:-----:|:------:
< 0    | omöjligt!
0-49   | underkänt
50-59  | 1
60-69  | 2
70-79  | 3
80-89  | 4
90-100 | 5
\> 100 | omöjligt!

Exempel på programmets funktion:

<sample-output>

Ge poäng [0-100]: **37**
Vitsord: underkänt

</sample-output>

<sample-output>

Ge poäng [0-100]: **76**
Vitsord: 3

</sample-output>

<sample-output>

Ge poäng [0-100]: **-3**
Vitsord: omöjligt!

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="FizzBuzz" tmcname="osa02-11_fizzbuzz">

Det här programmet ska be användaren att ge en siffra. Om siffran är delbar med tre, skriver man ut Fizz. Om talet är delbart med fem, skriver man ut Buzz. Om talet är delbart med de båda talen, skriver man ut FizzBuzz.

Exempel:

<sample-output>

Tal: **9**
Fizz

</sample-output>

<sample-output>

Tal: **7**

</sample-output>

<sample-output>

Tal: **20**
Buzz

</sample-output>

<sample-output>

Tal: **45**
FizzBuzz

</sample-output>

</in-browser-programming-exercise>

## Kapslade if-satser

If-satser kan kapslas inom andra if-satser. Till exempel följande program kollar först om en siffra är noll före det kollar om talet är jämnt eller inte.

```python
nummer = int(input("Ge en siffra: "))

if nummer > 0:
    if nummer % 2 == 0:
        print("Talet är jämnt")
    else:
        print("Talet är ojämnt")
else:
    print("Talet är negativt")
```

Så här kan programmet fungera:

<sample-output>

Ge en siffra: **3**
Talet är ojämnt

Ge en siffra: **18**
Talet är jämnt

Ge en siffra: **-4**
Talet är negativt

</sample-output>

När man kapslar if-satser är det kritiskt att indenteringen blir rätt. Indenteringen bestämmer vilka grenar som är länkade ihop. Till exempel en if-gren och en else-gren med samma inledande mellanrum tolkas som grenar av en och samma if-sats.

Ofta kan likadana resultat åstadkommas både med logiska operatorer och kapslade if-satser. Det följande exemplet fungerar helt på samma sätt som det tidigare exemplet:

```python
nummer = int(input("Ge en siffra: "))

if nummer > 0 and nummer % 2 == 0:
    print("Talet är jämnt")
elif nummer > 0 and nummer % 2 != 0:
    print("Talet är ojämnt")
else:
    print("Talet är negativt")
```

Man kan inte på rak arm säga vilkendera lösning är bättre. Situationen bestämmer ofta hur det lönar sig att bygga upp if-satsen på ett logiskt sätt. I det här exemplet tycker flera personer att versionen med kapsling är mera intuitiv.

<in-browser-programming-exercise name="Skottår" tmcname="osa02-12_karkausvuosi">

Ett år är ett skottår om det är delbart med fyra. Om ett år är delbart med 100 är det ett skottår bara då det är delbart med 400.

Skapa ett program som frågar användaren om ett årtal. Programmet meddelar om året är ett skottår eller inte.

<sample-output>

Ange år: **2011**
Året är inte ett skottår.

</sample-output>

<sample-output>

Ange år: **2020**
Året är ett skottår.

</sample-output>

<sample-output>

Ange år: **1800**
Året är inte ett skottår.

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="I mitten av alfabetet" tmcname="osa02-13_aakkosjarjestyksessa_keskimmainen">

Skapa ett program som frågar användaren efter tre bokstäver. Programmet skriver ut bokstaven som är mellerst i alfabetisk ordning.

Du kan anta att alla bokstäver är antingen gemener eller versaler (små/STORA).

Exempel:

<sample-output>

Ge bokstav 1: x
Ge bokstav 2: c
Ge bokstav 3: p
Den mellersta bokstaven är p

</sample-output>

<sample-output>

Ge bokstav 1: C
Ge bokstav 2: B
Ge bokstav 3: A
Den mellersta bokstaven är B

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Gåvoskatt" tmcname="osa02-14_lahjaverolaskuri" height="500px">

Enligt skattemyndigheten är en gåva sådan egendom som överlåts till en annan person utan ersättning. Om en person får gåvor från samma person till ett värde på 5 000 euro eller mera, ska gåvoskatt betalas.

När gåvan kommer från en nära släkting, räknas gåvoskatten enligt följande tabell:

Gåvans värde        | Skatt vid nedre gränsen | Skatteprocent för överstigande andel
:------------------:|:-----------------------:|:-----------------------------------:
5 000 - 25 000      | 100	                  | 8
25 000 - 55 000	    | 1 700                   | 10
55 000 - 200 000    | 4 700	                  | 12
200 000 - 1 000 000	| 22 100                  | 15
1 000 000 -	        | 142 100                 | 17

Till exempel för en gåva på 6 000 euro ska man betala 180 euro skatt (100 + (6000 - 5000) * 0,08). För en gåva på 75 000 euro betalar man 7 100 euro i beskattningen (4700 + (75000 - 55000) * 0,12).

Skapa ett program som räknar gåvoskatten för en gåva från en nära släkting. Nedan följer några exempel.

<sample-output>

Gåvans värde? **3500**
Ingen gåvoskatt!

</sample-output>

<sample-output>

Gåvans värde? **5000**
Gåvoskatt: 100.0 euro

</sample-output>

<sample-output>

Gåvans värde? **27500**
Gåvoskatt: 1950.0 euro

</sample-output>

</in-browser-programming-exercise>

<quiz id="97b08ca9-2b58-51d5-a457-2727652ed83e"></quiz>
