---
path: '/osa-2/3-kombinera-villkor'
title: 'Kombinera villkor'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* vet du hur man använder operatorerna `and`, `or` och `not` i villkorsuttryck
* kan du skriva nästlade if-satser.

</text-box>

## Logiska operatorer

Du kan kombinera flera villkorsuttryck med de logiska operatorerna `and` och `or`. Operatorn `and` innebär att alla ingående villkorsuttryck måste vara sanna samtidigt. Operatorn `or` kräver att minst ett av villkorsuttrycken är sant.

Till exempel villkoret `tal >= 5 and tal <= 8` anger att tal måste samtidigt vara minst fem och högst åtta – alltså mellan fem och åtta.

```python
tal = int(input("Ge ett tal: "))
if tal >= 5 and tal <= 8:
    print("Talet är mellan 5 och 8")
```

Villkoret `tal < 5 or tal > 8` anger att talet måste vara mindre än fem eller större än åtta – alltså inte mellan fem till åtta.

```python
tal = int(input("Ge ett tal: "))
if tal < 5 or tal > 8:
    print("Talet är inte mellan 5 och 8")
```

Den här sanningstabellen beskriver hur operatorerna fungerar i olika situationer:

a     | b     | a and b | a or b |
:----:|:-----:|:-------:|:------:|
False | False | False   | False  |
True  | False | False   | True   |
False | True  | False   | True   |
True  | True  | True    | True   |

Ibland kan det vara bra att veta om ett villkorsuttryck inte är sant. Operatorn `not` inverterar ett värde, dvs. byter det till det motsatta:


a     | not a
:----:|:-----:
True  | False
False | True

Det ovanstående exemplet som anger om talet inte är mellan 5-8 kan också skrivas så här:

```python
nummer = int(input("Ge en siffra: "))
if not (nummer >= 5 and nummer <= 8):
    print("Siffran är inte mellan 5 och 8")
```

Logiska operatorer kallas framför allt inom programmering för Boolean-operatorer.


<text-box variant='hint' name='Kombinerade villkor – förenklat'>

Villkoret `x >= a and x <= b` är ett mycket vanligt sätt att bestämma om talet `x` ligger i intervallet `a` till `b`. Den här strukturen återkommer i flera programmeringsspråk.

Python ger oss också möjlighet att använda oss av ett förenklat uttryckssätt för att kombinera villkorsuttryck: `a <= x <= b` ger samma resultat som den längre versionen med `and`. Den här notationen är kanske bekant från matematikens värld men den används inte så ofta i Python – kanske för att många andra programmeringsspråk saknar liknande syntax.

</text-box>

## Att kombinera och kedja villkorsuttryck

Det här programmet ber användaren att mata in fyra tal. Sedan kollar programmet vilket tal som är störst med hjälp av några villkor:

```python
n1 = int(input("Ge tal 1: "))
n2 = int(input("Ge tal 2: "))
n3 = int(input("Ge tal 3: "))
n4 = int(input("Ge tal 4: "))

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

Ge tal 1: **2**
Ge tal 2: **4**
Ge tal 3: **1**
Ge tal 4: **1**
4 är det största talet.

</sample-output>

I exemplet ovan är `n1 > n2 and n1 > n3 and n1 > n4` sant endast då alla tre "delvillkor" är sanna.

<in-browser-programming-exercise name="Kontroll av ålder" tmcname="osa02-08_alderskoll">

Skapa ett program som ber användern mata in sin ålder och skriva ut ett meddelande beroende på åldern. Om åldern är under fem, eller t.o.m. negativ ska programmet reagera på det. 

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

<in-browser-programming-exercise name="Brorsöner" tmcname="osa02-09_brorsoner">

Skapa ett program som ber användare mata in sitt namn. 

Om namnet är Knatte, Fnatte eller Tjatte, ska programmet anta att användaren är Kalle Ankas brorson.

Om namnet är Teddi eller Freddi, ska programmet anta att användaren är Musse Piggs brorson.

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

<in-browser-programming-exercise name="Vitsord och poäng" tmcname="osa02-10_vitsord_poang">

Följande tabell beskriver hur man kommer fram till vitsordet på en kurs. Skapa ett program som meddelar vitsordet på basis av den här tabellen.

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

Det här programmet ska be användaren att mata in ett tal. Om talet är delbart med 3, skriver man ut Fizz. Om talet är delbart med 5, skriver man ut Buzz. Om talet är delbart med både 3 och 5, skriver man ut FizzBuzz.

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

if-satser kan nästlas innanför andra if-satser. Till exempel kollar följande program först om talet är noll innan det kollar om talet är jämnt eller inte.

```python
tal = int(input("Ge ett tal: "))

if tal > 0:
    if tal % 2 == 0:
        print("Talet är jämnt")
    else:
        print("Talet är ojämnt")
else:
    print("Talet är negativt")
```

Så här kan programmet fungera:

<sample-output>

Ge ett tal: **3**
Talet är ojämnt

Ge ett tal: **18**
Talet är jämnt

Ge ett tal: **-4**
Talet är negativt

</sample-output>

När man nästlar if-satser är det viktigt att indenteringen blir rätt. Indenteringen bestämmer vilka grenar som hör ihop. Till exempel tolkas en if-gren och en else-gren med samma indenteringsnivå som grenar av en och samma if-sats.

Ofta kan man åstadkomma samma sak med logiska operatorer och nästlade if-satser. Det följande exemplet fungerar helt på samma sätt som exemplet ovan: 

```python
tal = int(input("Ge ett tal: "))

if tal > 0 and tal % 2 == 0:
    print("Talet är jämnt")
elif tal > 0 and tal % 2 != 0:
    print("Talet är ojämnt")
else:
    print("Talet är negativt")
```

Man kan inte på rak arm säga vilkendera lösning som är bättre. Situationen bestämmer ofta hur det lönar sig att bygga upp if-satsen på ett logiskt sätt. I det här exemplet tycker många att versionen med nästling är mer intuitiv.

<in-browser-programming-exercise name="Skottår" tmcname="osa02-12_skottar">

Ett år är ett skottår om det är delbart med fyra. Om årtalet däremot är delbart med 100 är det ett skottår enbart då det är delbart med 400.

Skapa ett program som ber användaren mata in ett årtal. Programmet ska sedan meddela om året är ett skottår eller inte.

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

<in-browser-programming-exercise name="I mitten av alfabetet" tmcname="osa02-13_mellerst_i_alfabetet">

Skapa ett program som ber användaren mata in tre bokstäver. Programmet ska sedan skriva ut den mellersta bokstaven om man ser till den alfabetiska ordningen.

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


<in-browser-programming-exercise name="Gåvoskatt" tmcname="osa02-14_gavoskatt" height="500px">

[Enligt skattemyndigheten](https://www.vero.fi/sv/privatpersoner/egendom/gava/) är en gåva egendom som överlåts till en annan person utan ersättning. Om en person får gåvor från samma person till ett värde på 5 000 euro eller mera, ska gåvoskatt betalas.

När gåvan kommer från en nära släkting, räknas gåvoskatten [enligt följande tabell](https://www.vero.fi/sv/privatpersoner/egendom/gava/g%C3%A5voskatter%C3%A4knaren/):

Gåvans värde        | Skatt vid nedre gränsen | Skatteprocent för överstigande andel
:------------------:|:-----------------------:|:-----------------------------------:
5 000 - 25 000      | 100	                  | 8
25 000 - 55 000	    | 1 700                   | 10
55 000 - 200 000    | 4 700	                  | 12
200 000 - 1 000 000	| 22 100                  | 15
1 000 000 -	        | 142 100                 | 17

Till exempel för en gåva på 6 000 euro ska man betala 180 euro skatt (100 + (6000 - 5000) * 0,08). För en gåva på 75 000 euro betalar man 7 100 euro i beskattningen (4700 + (75000 - 55000) * 0,12).

Skapa ett program som beräknar den gåvoskatt man måste betala på en gåva från en nära släkting. Nedan följer några exempel.

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

<quiz id="3e75ce86-d29f-5589-a058-47e1fa91d317"></quiz>
