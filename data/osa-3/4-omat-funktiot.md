---
path: '/osa-3/4-omat-funktiot'
title: 'Definiera funktioner'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* kan du skriva och kalla på dina egna funktioner
* förstår du vad ett argument och en parameter hos en funktion är
* kan du definiera parametrar i dina egna funktioner.

</text-box>

Vi har redan använt funktioner som `len`, `print` och `input` i våra program. Dessa är funktioner som är inbyggda i Python och de är därmed alltid tillgängliga. Det är dessutom möjligt att definiera egna funktioner.

## Definiera en funktion

Före en funktion kan användas måste den definieras. Man börjar definieringen av en funktion med nyckelordet `def` (define). Därefter följer namnet på funktionen, följt av parentes och kolon. Efter det här följer funktionens innehåll – indenterat precis som med while- och if-blocken.

Den här kodsnutten definierar till exempel funktionen `meddelande`:

```python
def meddelande():
    print("Det här är min funktion!")
```

Om programmet körs, verkar det som att inget händer. Det beror på att funktionens innehåll endast körs då funktionen anropas.

Man kan anropa en funktion enkelt – genom att nämna dess namn i koden. Så här kan vi utveckla det föregående exemplet:

```python
def meddelande():
    print("Det här är min funktion!")

meddelande()
```

Här är resultatet:

<sample-output>

Det här är min funktion!

</sample-output>

När en funktion har definierats kan den kallas flera gånger.

```python
def meddelande():
    print("Det här är min funktion!")

meddelande()
meddelande()
meddelande()
```

<sample-output>

Det här är min funktion!
Det här är min funktion!
Det här är min funktion!

</sample-output>

<text-box variant='hint' name='Testa dina egna funktioner'>

Obs! Från och med nu kommer de flesta av kursens uppgifter förutsätta att du definierar dina egna funktioner.

När ett program består bara av funktioner verkar ingenting hända då programmet körs. Följande kod skriver inte ut någonting, även om den innehåller en `print`-sats:

```python
def halsa():
    print("Hejps!")
```

Det här beror på att koden i `halsa`-funktionen endast körs då funktionen anropas.

"Huvudprogrammet" nedan ska innehålla alla funktionsanrop för att kunna testa funktionerna. Python tolkar all kod utanför funktionsdefinitioner som en del av huvudfunktionen, som körs automatiskt när själva filen körs. Låt oss anropa funktionen:

```python
def halsa():
    print("Hejps!")

# huvudprogrammet är den del av programmet som inte är inom någon funktion
# vi anropar vår funktion

halsa()
```

Viktigt! De automatiska testerna i den här kursen kräver att övningsfilernas huvudfunktion är tom. Inga kommandon bör lämnas i huvudfunktionen i din lösning. All kod som du använder för att testa funktioner ska istället vara innanför ett speciellt if-block:

```python
def halsa():
    print("Hejps!")

# vi skriver huvudprogrammet inom ett block som det här
if __name__ == "__main__":
    halsa()
```

Kod utanför blocket orsakar ett felmeddelande som detta:

<img src="3_4_1.png">

Det lönar sig också att märka att testen inte kör kod i `if __name__ == "__main__"` -block. Dit ska man inte placera kod som behövs för uppgifterna.

</text-box>

<in-browser-programming-exercise name="Sju bröder" tmcname="osa03-21_seitseman_veljesta">

Skapa funktionen `sju_broder` som skriver ut namnet på sju bröder i alfabetisk ordning:

<sample-output>

Aapo
Eero
Juhani
Lauri
Simeoni
Timo
Tuomas

</sample-output>

</in-browser-programming-exercise>

## Argument hos funktioner

Funktioner tar ofta emot ett eller fler argument som kan påverka på vad funktionen gör. Till exempel de inbyggda `print`- och `input`-funktionerna i Python tar emot texten som ska visas som argument:

```python
print("Hejps!")                      # som parameter strängen "Hejps!"
namn = input("Berätta ditt namn: ")  # som parameter strängen "Berätta ditt namn: "
print(namn)                          # som parameter värdet på variabeln namn
```

Det har tidigare nämnts att termerna argument och parameter ofta syftar till samma sak. Skillnaden är att argument används för den data som ges till funktionen vid ett anrop, medan dessa inom funktionen tilldelas till variabler som kallas parametrar. Vi ger alltså argument till en funktion då vi anropar den. När vi definierar en funktion talar vi istället om parametrar.

Det här kan kännas som en meningslös skillnad, och dessutom följer inte alla källor den här definitionen. Vi strävar att göra den här skillnaden tydlig under den här kursen. Med korrekt terminologi är det lättare att förstå andra material förutom det som den här kursen erbjuder.

Låt oss definiera några funktioner som tar emot argument. I funktionsdefinitionen följer parametrarna funktionens namn, inom parenteserna:

```python
def halsa(sak):
    print("Hej", sak)
```

När funktionen anropas två gånger…

```python
halsa("Beatrice")
halsa("världen!")
```

…får vi två hälsningar:

<sample-output>

Hej Beatrice
Hej världen!

</sample-output>

Vi tar ännu en titt på funktionsdefinitionen:

```python
def halsa(sak):
    print("Hej", sak)
```

På den första raden har vi definierat att funktionen tar emot ett argument och tilldelar det till en variabel med namnet `sak`. Inom funktionen använder `print`-kommandot det värde som finns lagrat i variabeln `sak`.

När funktionen anropas får parametern sak det värde som getts som argument i funktionsanropet. Till exempel följande funktionsanrop…

```python
namn = "Alice"
halsa(namn)
```

…resulterar i att variabeln `sak` får värdet `"Alice"`.

Namnet på en funktion ges enligt samma principer som variabelnamn. De ska vara beskrivande, i regel innehålla små bokstäver och understreck. Undantag finns igen, men vi ignorerar dem tills vidare.

<in-browser-programming-exercise name="Första tecknet" tmcname="osa03-22_ensimmainen_merkki">

Gör så att funktionen `forsta` i den här uppgiften skriver ut det första tecknet i den sträng som ges som argument.

```python
def forsta(strang):
     # skriv kod här

# vi testar på funktionen
if __name__ == "__main__":
    forsta('python')
    forsta('yxa')
    forsta('tapet')
    forsta('himmel')
    forsta('opera')
    forsta('normal')
```

<sample-output>

p
y
t
h
o
n

</sample-output>

</in-browser-programming-exercise>

<text-box variant='hint' name='Testa funktioner med argument'>

Då du testar på funktioner som tar emot ett eller fler argument, kan det vara till nytta att testa den med olika argument.

Håll koll på möjliga "speciella fall". Hur kommer funktionen att fungera om argumentet till exempel är noll eller negativt? Eller ett flyttal istället för ett heltal? Vad händer om argumentet är en tom sträng?

Om en uppgift inte förutsätter att du anropar en funktion kan du ändå göra det. Använd då ett if-block enligt det som beskrevs tidigare. Testen kommer att ignorera koden inom det här blocket.

</text-box>

## Fler exempel

Vi tar en titt på fler exempelfunktioner som tar emot argument. Här är parametern en siffra:

```python
def kvadrat(x):
    print(f"Kvadraten av {x} är {x * x}")

kvadrat(2)
kvadrat(5)
```

<sample-output>

Kvadraten av 2 är 4
Kvadraten av 5 är 25

</sample-output>

Här har vi en if-sats inom en funktion:

```python
def halsa(namn):
    if namn == "Beatrice":
        print("Hejps,", namn)
    else:
        print("God dag,", namn)

halsa("Beatrice")
halsa("Mårten")
```

<sample-output>

Hejps, Beatrice
God dag, Mårten

</sample-output>

Den här funktionen tar emot två argument:

```python
def summa(x, y):
    resultat = x + y
    print(f"Summan av {x} och {y} är {resultat}")

summa(1, 2)
summa(5, 24)
```

<sample-output>

Summan av 1 och 2 är 3
Summan av 5 och 24 är 29

</sample-output>

Funktionen har också en hjälpvariabel, `resultat`, som används för att lagra summan av argumentens värden.

Märk att namnen på parametrarna i funktionsdefinitionen inte har några kopplingar till andra variabler utanför definitionen. Vi kan anropa ovanstående funktion på följande sätt:

```python
x = 100
y = 30
summa(1, 2)
summa(x + y, 10)
```

Det här skriver ut:

<sample-output>

Summan av 1 och 2 är 3
Summan av 130 och 10 är 140

</sample-output>

I det första funktionsanropet får parametrarna värdena `x = 1` och `y = 2`. I det andra anropet får de värdena `x = 130` och `y = 10`. Det här oavsett att vi i anropet använder variabler med samma namn.

I nästa modul återkommer vi till funktionsdefinitioner.

<!--vastaava varoitusteksti löytyy osioista 3-4, 4-6 ja 5-1, tsekkaa kaikki jos muokkaat tätä-->
## Varning: globala variabler inom funktioner

I exemplen ovan observerade vi att det är möjligt att tilldela nya variabler i funktionsdefinitioner. Funktionen kan också se variabler utanför funktionen, i huvudfunktionen. Dessa variabler kallas globala variabler.

Att använda globala variabler från funktioner är oftast en dålig idé. Det kan orsaka en hel del problem, till exempel orsaka buggar som är svåra att spåra.

Här är ett exempel på en funktion som använder en global variabel "av misstag":

```python
# global variabel
namn = "Beatrice"

def halsa(etunimi):
    # vi skriver av misstag ut den globala variabelns värde istället för parametern
    print("Hej", namn)

halsa("Alice")
halsa("Beatrice")
```

<sample-output>

Hej Beatrice
Hej Beatrice

</sample-output>

Oavsett vilka argument vi anropar funktionen med skrivs värdet "Beatrice" från den globala variabeln ut.

<in-browser-programming-exercise name="Medelvärde" tmcname="osa03-25_keskiarvo">

Skapa funktionen `medeltal` som tar emot tre heltal som argument. Funktionen ska skriva ut medelvärdet av dessa tal.

```python
medeltal(5, 3, 1)
medeltal(10, 1, 1)
```

<sample-output>

3.0
4.0

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Flera utskrifter" tmcname="osa03-24_monta_tulostusta">

Skapa funktionen `skriv_ut_flera_ganger(strang, ganger)`, som får en sträng och ett heltal som argument. Strängen ska skrivas ut så många gånger som heltalet indikerar:

```python
skriv_ut_flera_ganger("hej!!", 5)

print()

merkkijono = "Allt började då grannbondens gamla traktor började ryka..."
kertaa = 3
skriv_ut_flera_ganger(merkkijono, kertaa)
```
<sample-output>

hej!!
hej!!
hej!!
hej!!
hej!!

Allt började då grannbondens gamla traktor började ryka....
Allt började då grannbondens gamla traktor började ryka....
Allt började då grannbondens gamla traktor började ryka....

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Fyrkant" tmcname="osa03-23_risunelio">

Skapa funktionen `fyrkant(langd)`, som får som argument ett heltal som indikerar hur stor fyrkant programmet ska skriva ut:

```python
fyrkant(3)
print()
fyrkant(5)
```

<sample-output>

<pre>
###
###
###

#####
#####
#####
#####
#####
</pre>

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Schackbräde" tmcname="osa03-26_shakkilauta">

Skapa funktionen `schackbrade` som skapar ett schackbräde av siffrorna noll och ett enligt exemplen nedan.

```python
schackbrade(3)
print()
schackbrade(6)
```

<sample-output>

<pre>
101
010
101

101010
010101
101010
010101
101010
010101
</pre>

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Ordkvadrat" tmcname="osa03-27_sananelio">

Skapa funktionen `kvadrat` som skriver ut en "ordkvadrat" enligt exemplen nedan.

```python
kvadrat("ab", 3)
print()
kvadrat("aybabtu", 5)
```

<sample-output>

<pre>
aba
bab
aba

aybab
tuayb
abtua
ybabt
uayba
</pre>

</sample-output>

</in-browser-programming-exercise>

<quiz id="ecfc4b08-6ee4-514c-a830-a2d846364928"></quiz>

Vänligen svara på en kort enkät gällande den här veckans material.

<quiz id="3f7c6a3f-40a6-5e2b-ba4a-5acddee4b9b7"></quiz>
