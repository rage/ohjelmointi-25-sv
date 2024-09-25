---
path: '/osa-4/2-mer-om-funktioner'
title: 'Mer om funktioner'
hidden: false
---


<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* vet du mera om argument och parametrar i samband med funktioner
* kan du returnera värden från funktioner och använda dessa värden i ditt program
* kan du ge typledtrådar för parametrar och värden som returneras.

</text-box>

Vi börjar med en snabbrepetition av funktioner i Python. Funktioner definieras med nyckelordet `def`:

```python
def meddelande():
    print("Det här kommer från en funktion")
```

För att använda funktionen behöver vi anropa eller kalla på den i programmet:


```python
meddelande()
```

I det här fallet skulle programmet skriva ut följande:

<sample-output>

Det här kommer från en funktion

</sample-output>

## Parametrar och argument hos en funktion

En funktion kan ta emot en eller flera _argument_. När funktionen anropas tilldelas argumenten till variabler som är definierade i funktionsdefinitionen. Dessa variabler kallas _parametrar_ och de listas inom de parenteser som kommer efter funktionens namn.

I den följande koden har funktionen `halsa` en definierad parameter (namn), medan funktionen `summa` har två (a och b):

```python
def halsa(namn):
    print("Hej,", namn)

def summa(a, b):
    print("Summan av parametrarna är", a + b)
```

```python
halsa("Emilia")
summa(2, 3)
```

<sample-output>

Hej, Emilia
Summan av parametrarna är 5

</sample-output>

<text-box variant='hint' name='Formell och aktuell, parameter och argument'>

Terminologin kring data som ges till en funktion kan kännas förvirrande. För att göra situationen ännu konstigare, använder en del källor uttryck som formella och aktuella parametrar eller formella och aktuella argument. Pythons dokumentation nämner endast termerna argument och parameter. Därför använder vi också dessa termer.

Vad händer egentligen när funktionsanropet `halsa("Emilia")` körs?

I funktionsdefinitionen `halsa(namn)` beter sig parametern namn som en normal variabel. Vi kan använda den inom funktionen på samma sätt som vi har använt variabler i huvudfunktionen i flera program hittills.

I funktionsanropet `halsa("Emilia")` är argumentet `"Emilia"` som vilken som helst annan sträng vi stött på tidigare. Vi kan till exempel tilldela den till en variabel.

När funktionsanropet körs kommer alltså värdet på argumentet – `"Emilia"` – att tilldelas till variabeln `namn`. Under den här körningen av funktionen kommer `namn = "Emilia"`. När funktionen anropas med ett annat argument kommer värdet på namn att vara ett annat.

Terminologin kan kännas överflödig, men datavetenskapen strävar efter att vara en så exakt vetenskap som möjligt. Att använda noga definierad terminologi hjälper.

</text-box>

## Felmeddelanden som uppstår i testerna

De flesta uppgifter under den här kursen inkluderar automatiska tester. Om programmet inte fungerar på det sätt som förutsätts av uppgiften, kommer testet att visa ett felmeddelande. Det här meddelandet kan vara till nytta – eller inte. Det är värt att läsa meddelandet noga.

I vissa fall berättar felmeddelandet inte särskilt mycket. I nästa övning kan du stöta på det här felmeddelandet:

<img src="4_2_0a.png">

Meddelandet berättar att man borde kunna köra funktionen `streck` med de specificerade argumenten:

```python
streck(5, "")
```

Det verkliga problemet får vi reda på när vi kör det funktionsanrop som står i felmeddelandet. Du kan göra det genom att kopiera funktionsanropet till ditt program och klicka på triangeln:

<img src="4_2_0b.png">

Den del av felmeddelandet som uppstår när programmet körs (markerade i bilden ovan) berättar att rad fyra i koden orsakar felet `IndexError`. I den förra modulen fanns ett liknande exempel, där vi försökte använda ett index som inte var en del av en sträng. Den här gången orsakas problemet av att vi försöker hämta den första bokstaven hos en tom sträng – dvs. en sträng med längden noll.

<programming-exercise name='Streck' tmcname='osa04-02_streck'>

Skapa funktionen `streck` som tar två argument (bredd, strang). Funktionen ska sedan skapa ett streck genom att skriva ut det första tecknet i den angivna strängen så många gånger som angetts i den första parametern. Om den andra parametern är tom, används asterisker.

Exempel:

```python
streck(7, "%")
streck(10, "LOL")
streck(3, "")
```

<sample-output>

<pre>
%%%%%%%
LLLLLLLLLL
***
</pre>

</sample-output>

</programming-exercise>

## Funktionsanrop inom funktionsanrop

Du kan anropa en funktion från en annan funktion. Vi har faktiskt gjort det redan flera gånger – vi har anropat `print`-funktionen inom våra egna funktioner i den förra modulen. Våra egna funktioner fungerar på samma sätt. I det följande exemplet anropar funktionen `halsa_flera_ganger` funktionen `halsa` så många gånger som specificerats i argumentet ganger:

```python
def halsa(namn):
    print("Hej,", namn)

def halsa_flera_ganger(namn, ganger):
    while ganger > 0:
        halsa(namn)
        ganger -= 1

halsa_flera_ganger("Emilia", 3)
```

<sample-output>

Hej, Emilia
Hej, Emilia
Hej, Emilia

</sample-output>


<programming-exercise name='Fyrkant (igen)' tmcname='osa04-02a_fyrkant'>

Skapa funktionen `fyrkant` som skriver ut en tio tecken bred fyrkant med den höjd som getts som argument.

Funktionen ska anropa `streck` från den föregående uppgiften. Kopiera alltså funktionen från den föregående uppgiften till den här uppgiften och skriv den nya funktionen under. Redigera inte funktionen `streck`!

Exempel:

```python
fyrkant(5)
print()
fyrkant(2)
```

<sample-output>

<pre>
##########
##########
##########
##########
##########

##########
##########
</pre>

</sample-output>

</programming-exercise>

<programming-exercise name='Kvadrat' tmcname='osa04-02b_kvadrat'>

Skapa funktionen `kvadrat` som skriver ut en kvadrat med den storlek som angetts som argument.

Funktionen ska anropa `streck` från den föregående uppgiften. Kopiera alltså funktionen från den föregående uppgiften till den här uppgiften och skriv den nya funktionen nedanför. Redigera inte funktionen `streck`!

Exempel:

```python
kvadrat(5)
print()
kvadrat(3)
```

<sample-output>

<pre>
#####
#####
#####
#####
#####

###
###
###
</pre>

</sample-output>

</programming-exercise>

<programming-exercise name='Speciell kvadrat' tmcname='osa04-02c_speciell_kvadrat'>

Skapa funktionen `speciell_kvadrat` som tar emot två argument – storleken samt det tecken som används för att rita kvadraten.

Funktionen ska anropa `streck` från den föregående uppgiften. Kopiera alltså funktionen från den föregående uppgiften till den här uppgiften och skriv den nya funktionen nedanför. Redigera inte funktionen `streck`!

Exempel:

```python
speciell_kvadrat(5, "*")
print()
speciell_kvadrat(3, "o")
```

<sample-output>

<pre>
*****
*****
*****
*****
*****

ooo
ooo
ooo
</pre>

</sample-output>

</programming-exercise>

<programming-exercise name='Triangel' tmcname='osa04-02d_triangel'>

Skapa funktionen `triangel` som skriver ut en triangel med den höjd/bredd som angetts med argumenten.

Funktionen ska anropa `streck` från den föregående uppgiften. Kopiera alltså funktionen från den föregående uppgiften till den här uppgiften och skriv den nya funktionen nedanför. Redigera inte funktionen `streck`!

Exempel:

```python
triangel(6)
print()
triangel(3)
```

<sample-output>

<pre>
#
##
###
####
#####
######

#
##
###
</pre>

</sample-output>

</programming-exercise>

<programming-exercise name='Figur' tmcname='osa04-03_figur'>

Skapa funktionen `figur` som tar emot fyra argument. Funktionen skapar en figur som består av en triangel och en fyrkant enligt de givna argumenten. Se exemplen.

Funktionen ska anropa `streck` från den föregående uppgiften. Kopiera alltså funktionen från den föregående uppgiften till den här uppgiften och skriv den nya funktionen nedanför. Redigera inte funktionen `streck`!

Exempel:

```python
figur(5, "X", 3, "*")
print()
figur(2, "o", 4, "+")
print()
figur(3, ".", 0, ",")
```

<sample-output>

<pre>
X
XX
XXX
XXXX
XXXXX
*****
*****
*****

o
oo
++
++
++
++

.
..
...
</pre>

</sample-output>

Tips: Försök inte lösa allt på en gång. Fokusera på en sak åt gången – börja till exempel med att få triangeln utritad på korrekt sätt och fortsätt sedan med fyrkanten. Det här gäller vilket som helst problem inom programmering. Ta små steg och kolla att allt fungerar innan du fortsätter.

</programming-exercise>

<programming-exercise name='Julgran' tmcname='osa04-04_julgran'>

Skapa funktionen `julgran` som tar emot ett argument. Funktionen ska skriva ut texten "julgran!" samt en julgran med den angivna höjden.

Exempelvis `julgran(3)`:

<sample-output>

<pre>
julgran!
  *
 ***
*****
  *
</pre>

</sample-output>

Eller till exempel `julgran(5)`:

<sample-output>

<pre>
julgran!
    *
   ***
  *****
 *******
*********
    *
</pre>

</sample-output>

Observera att antalet mellanslag till vänster om granen ska vara exakt korrekt. Även om granens form är korrekt, accepteras granen inte om den nedersta "grenen" inte börjar direkt i början på raden.

</programming-exercise>

## Funktioners returvärde

Funktioner kan också returnera värden. Till exempel returnerar Pythons inbyggda funktion `input` den sträng som användaren har matat in. Värdet som returneras av en funktion kan lagras i en variabel:

```python
ord = input("Ange ett ord: ")
```

När du vill få ett heltalsvärde av användaren måste det värde som hen matar in via `input` konverteras till ett heltal. För det använder vi `int`-funktionen som också returnerar ett värde:

```python
siffra = int(input("Ange ett heltal: "))
```

Funktionen `int` tar den sträng som returneras av `input`-funktionen som argument och returnerar – om möjligt – värdet i heltalsform.

## `return`-satsen

Funktioner som du själv definierar kan också returnera värden. För det här ändamålet behöver du använda `return`-satsen. Till exempel returnerar funktionen `summa` nedan summan av dess parametrar:

```python
def summa(a, b):
    return a + b

svar = summa(2, 3)

print("Summa:", svar)
```

<sample-output>

Summa: 5

</sample-output>

Här är ett annat exempel på ett returnerat värde. Funktionen ber om användarens namn och returnerar den sträng som användaren matar in:

```python
def fraga_namn():
    namn = input("Vad är ditt namn? ")
    return namn

namn = fraga_namn()
print("Hej,", namn)
```

<sample-output>

Vad är ditt namn? **Anna**
Hej, Anna

</sample-output>

Observera att `return`-satsen avbryter funktionen, och gör så att programmet fortsätter köras i huvudfunktionen. Det här är ett sätt att göra en jämförelsefunktion:

```python
def minst(a,b):
    if a < b:
        return a
    return b

print(minst(3, 7))
print(minst(5, 2))
```

Idén är att om `a` är mindre än `b` så kommer funktionen att returnera `a` och avslutas direkt. Annars fortsätter man till nästa rad som returnerar värdet `b`. Det går alltså inte att köra två `return`-satser i samma funktion under samma funktionsanrop, eftersom den första `return`-satsen första kommer att avbryta funktionen.

<sample-output>

3
2

</sample-output>

Du kan använda dig av `return`-satsen även om funktionen inte returnerar något värde. Då är dess uppgift helt enkelt att avsluta funktionskörningen:

```python
def halsa(namn):
    if namn == "":
        print("???")
        return
    print("Hej,", namn)

halsa("Emilia")
halsa("")
halsa("Mårten")
```

Om argumentet som sparas i variabeln `namn` är en tom sträng, kommer texten `???` att skrivas ut och funktionen avslutas:

<sample-output>

Hej, Emilia
???
Hej, Mårten

</sample-output>

## Att använda returvärden från funktioner

Vi känner redan till att värden som returneras från funktioner kan lagras i variabler:

```python
def summa(a, b):
    return a + b

resultat = summa(4, 6)
print("Summan är", resultat)
```

<sample-output>

Summan är 10

</sample-output>

Returvärdet hos en funktion kan jämföras med vilket som helst annat värde. Det är inte nödvändigt att lagra värdet i en variabel för att ge det som argument till `print`-instruktionen:

```python
print("Summan är", summa(4, 6))
```

Returvärdet hos en funktion kan vara ett argument för en funktion:

```python
def summa(a, b):
    return a+b

def differens(a, b):
    return a-b

resultat = differens(summa(5, 2), summa(2, 3))
print("Svaret är", resultat)
```

<sample-output>

Svaret är 2

</sample-output>

I det här fallet körs de inre funktionsanropen `summa(5, 2)` och `summa(2, 3)` först. Värdena som returneras (7 och 5) används som argument för det yttre funktionsanropet.

Det yttre funktionsanropet `differens(7, 5)` returnerar värdet 2, som lagras i variabeln `resultat` och skrivs ut.

För att sammanfatta: värden som returneras av funktioner fungerar som alla andra värden i Python. De kan skrivas ut, lagras i variabler och användas i uttryck och som argument i funktionsanrop.

## Skillnaden mellan `return` och `print`

Ibland är skillnaden mellan att använda `return` och `print` inte helt uppenbar. Vi undersöker två olika sätt att skapa en funktion som berättar vilket av två värden är större:

```python
def max1(a, b):
    if a > b:
        return a
    else:
        return b

def max2(a, b):
    if a > b:
        print(a)
    else:
        print(b)

svar = max1(3, 5)
print(svar)

max2(7, 2)
```

<sample-output>

5
7

</sample-output>

Båda versionerna verkar fungera i och med att det större värdet skrivs ut korrekt. Det finns ändå en central skillnad mellan de två funktionerna. Den första, `max1`, skriver inte ut något. Den använder sig istället av `return`-satsen. Om vi kör den följande kodraden…

```python
max1(3, 5)
```

…verkar ingenting hända. Funktionens returvärde måste användas på något sätt i den kod som anropar funktionen. Det kan till exempel lagras i en variabel och skrivas ut:

```python
svar = max1(3, 5)
print(svar)
```

 Om man inte behöver värdet för något annat ändamål i koden, kan man också skriva ut det direkt: 

```python
print(max1(3, 5))
```

Den andra versionen, `max2`, använder sig av `print`-instruktionen inom funktionen. Om vi vill se resultatet på skärmen, kan vi helt enkelt anropa funktionen…

```python
max2(7, 5)
```

…varpå det större värdet kommer att skrivas ut. Det dåliga med den här funktionen är att värdet som funktionen räknar ut inte lagras någonstans och därmed inte kan användas av själva programmet. Därför är funktioner som returnerar ett värde ofta ett bättre alternativ.

<programming-exercise name='Störst av talen' tmcname='osa04-05_storst'>

Skapa funktionen `storst` som tar tre tal som argument och returnerar det största av dem.

Exempel:

```python
print(storst(3, 4, 1)) # 4
print(storst(99, -4, 7)) # 99
print(storst(0, 0, 0)) # 0
```

</programming-exercise>

<programming-exercise name='Lika tecken' tmcname='osa04-06_lika'>

Skapa funktionen `lika` som tar en sträng och två heltal som argument. De två heltalen representerar index. Funktionen ska returnera `True` eller `False` beroende på om tecknen vid dessa index i strängen är lika eller inte. Om något av indexen inte finns i strängen ska funktionen returnera `False`.

Några exempel:

```python
# e och e är lika
print(lika("kodexpert", 3, 6)) # True

# k och x är olika
print(lika("kodexpert", 0, 4)) # False

# det andra indexet finns inte i strängen
print(lika("kodexpert", 0, 20)) # False
```

</programming-exercise>

<programming-exercise name='Första, andra och sista' tmcname='osa04-07_forsta_andra_sista'>

Skapa tre funktioner: `ord_ett`, `ord_tva` och `sista_ordet`. Alla tre funktioner ska ta en mening (alltså en sträng) som argument. 

Funktionerna ska returnera meningens första, andra respektive sista ord.

Du kan anta att strängen alltid innehåller minst två ord och exakt ett mellanslag mellan orden. Det finns inga mellanslag i början eller slutet av strängen.

```python
mening = "jag gillar blåbärspaj så länge den inte innehåller ägg"

print(ord_ett(mening)) # jag
print(ord_tva(mening)) # gillar
print(sista_ordet(mening)) # ägg
```

<sample-output>

jag
gillar
ägg

</sample-output>

```python
mening = "la-la gunilla"

print(ord_tva(mening)) # gunilla
print(sista_ordet(mening)) # gunilla
```

</programming-exercise>

## Argumentets typ

Här är en kort repetition av de datatyper vi bekantat oss med hittills:

Tyyppi        | I Python | Exempel
:-------------|:--------:|-----------
Heltal        | `int`    | `23`
Flyttal       | `float`  | `-0.45`
Sträng        | `str`    | `"Petra Python"`
Sanningsvärde (Boolean) | `bool`   | `True`

När du anropar en funktion, kommer den endast att fungera korrekt då argumenten du ger åt den är av korrekt typ. Ta en titt på det här exemplet:

```python
def skriv_ut_flera_ganger(meddelande, ganger):
    while ganger > 0:
        print(meddelande)
        ganger -= 1
```

Funktionen fungerar korrekt om vi anropar den på följande sätt:

```python
skriv_ut_flera_ganger("Hejsan", 5)
```

<sample-output>

Hejsan
Hejsan
Hejsan
Hejsan
Hejsan

</sample-output>

Om vi däremot ger funktionen ett argument av fel typ så kommer den inte att fungera:

```python
skriv_ut_flera_ganger("Hejsan", "Emilia")
```

<sample-output>

TypeError: '>' not supported between instances of 'str' and 'int'

</sample-output>

Problemet här är att den andra parametern `ganger` jämförs med ett heltal (0) i `while`-loopens villkorsuttryck (på den andra raden i funktionsdefinitionen). Det givna argumentet `"Emilia"` är dock en sträng och inte ett heltal. Strängar och heltal kan inte jämföras så här enkelt – därav felmeddelandet.

För att undvika den här typen av problem kan du inkludera typledtrådar (type hints) när du definierar funktioner. Typledtråden berättar vilken typ av argument funktionen förväntar sig:

```python
def skriv_ut_flera_ganger(meddelande : str, ganger : int):
    while ganger > 0:
        print(meddelande)
        ganger -= 1
```

Det här berättar för alla som använder funktionen att det första argumentet som skickas till funktionen ska vara en sträng och det andra ett heltal. 

Också returvärdets typ kan specificeras när funktionen definieras:

```python
def fraga_namn() -> str:
    namn = input("Vad är ditt namn? ")
    return namn
 ```

Det här berättar för användaren att funktionen kommer att returnera en sträng.

Obs! Typledtrådar är bokstavligen ledtrådar. Det är inte en garanti och kan inte säkerställa att felaktiga datatyper inte ges till eller returneras av en funktion. Om det här sker kommer funktionen ändå att köras, med resultatet att den inte nödvändigtvis fungerar korrekt.

<quiz id="5702d07b-676c-5ec2-ac2e-3d0f3b1b7d4e"></quiz>
