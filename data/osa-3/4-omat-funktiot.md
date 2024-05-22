---
path: '/osa-3/4-omat-funktiot'
title: 'Definiera funktioner'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

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
def viesti():
    print("Tämä on oma funktio!")
```

Om programmet körs, verkar det som att inget händer. Det beror på att funktionens innehåll endast körs då funktionen anropas.

Man kan anropa en funktion enkelt – genom att nämna dess namn i koden. Så här kan vi utveckla det föregående exemplet:

```python
def viesti():
    print("Tämä on oma funktio!")

viesti()
```

Här är resultatet:

<sample-output>

Tämä on oma funktio!

</sample-output>

När en funktion har definierats kan den kallas flera gånger.

```python
def viesti():
    print("Tämä on oma funktio!")

viesti()
viesti()
viesti()
```

<sample-output>

Tämä on oma funktio!
Tämä on oma funktio!
Tämä on oma funktio!

</sample-output>

<text-box variant='hint' name='Testa dina egna funktioner'>

Obs! Från och med nu kommer de flesta av kursens uppgifter förutsätta att du definierar dina egna funktioner.

När ett program består bara av funktioner verkar ingenting hända då programmet körs. Följande kod skriver inte ut någonting, även om den innehåller en `print`-sats:

```python
def moikkaa():
    print("Moi!")
```

Det här beror på att koden i `halsa`-funktionen endast körs då funktionen anropas.

”Huvudprogrammet” nedan ska innehålla alla funktionsanrop för att kunna testa funktionerna. Python tolkar all kod utanför funktionsdefinitioner som en del av huvudfunktionen, som körs automatiskt när själva filen körs. Låt oss anropa funktionen:

```python
def moikkaa():
    print("Moi!")

# Pääohjelma on se ohjelman osa, joka ei ole minkään funktion sisällä
# Kutsutaan omaa funktiota

moikkaa()
```

Viktigt! De automatiska testerna i den här kursen kräver att övningsfilernas huvudfunktion är tom. Inga kommandon bör lämnas i huvudfunktionen i din lösning. All kod som du använder för att testa funktioner ska istället vara innanför ett speciellt if-block:

```python
def moikkaa():
    print("Moi!")

# Kirjoita pääohjelma aina seuraavanlaisen lohkon sisälle
if __name__ == "__main__":
    moikkaa()
```

Lohkon ulkopuolelle jätetty testikoodi aiheuttaa seuraavan virheilmoituksen:

<img src="3_4_1.png">

Kannattaa myös huomata, että testit eivät suorita `if __name__ == "__main__"` -lohkon sisälle kirjoitettua koodia eikä sinne tule sijoittaa tehtävien edellyttämää koodia.

</text-box>

<in-browser-programming-exercise name="Seitsemän veljestä" tmcname="osa03-21_seitseman_veljesta">

Tee funktio `seitseman_veljesta` jonka kutsuminen tulostaa seitsemän veljeksen nimet aakkosjärjestyksessä:

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
print("Hei!")                     # parametrina merkkijono "Hei!"
nimi = input("Kerro nimesi: ")    # parametrina merkkijono "Kerro nimesi: "
print(nimi)                       # parametrina muuttujan nimi arvo
```

Det har tidigare nämnts att termerna argument och parameter ofta syftar till samma sak. Skillnaden är att argument används för den data som ges till funktionen vid ett anrop, medan dessa inom funktionen tilldelas till variabler som kallas parametrar. Vi ger alltså argument till en funktion då vi anropar den. När vi definierar en funktion talar vi istället om parametrar.

Det här kan kännas som en meningslös skillnad, och dessutom följer inte alla källor den här definitionen. Vi strävar att göra den här skillnaden tydlig under den här kursen. Med korrekt terminologi är det lättare att förstå andra material förutom det som den här kursen erbjuder.

Låt oss definiera några funktioner som tar emot argument. I funktionsdefinitionen följer parametrarna funktionens namn, inom parenteserna:

```python
def tervehdi(kohde):
    print("Hei", kohde)
```

När funktionen anropas två gånger…

```python
tervehdi("Emilia")
tervehdi("maailma!")
```

…får vi två hälsningar:

<sample-output>

Hei Emilia
Hei maailma!

</sample-output>

Vi tar ännu en titt på funktionsdefinitionen:

```python
def tervehdi(kohde):
    print("Hei", kohde)
```

På den första raden har vi definierat att funktionen tar emot ett argument och tilldelar det till en variabel med namnet `sak`. Inom funktionen använder `print`-kommandot det värde som finns lagrat i variabeln `sak`.

När funktionen anropas får parametern sak det värde som getts som argument i funktionsanropet. Till exempel följande funktionsanrop…

```python
nimi = "Antti"
tervehdi(nimi)
```

…resulterar i att variabeln `sak` får värdet `”Alice”`.

Namnet på en funktion ges enligt samma principer som variabelnamn. De ska vara beskrivande, i regel innehålla små bokstäver och understreck. Undantag finns igen, men vi ignorerar dem tills vidare.

<in-browser-programming-exercise name="Ensimmäinen merkki" tmcname="osa03-22_ensimmainen_merkki">

Täydennä koodipohjassa oleva funktio `ensimmainen` siten, että se tulostaa parametrinaan saamansa merkkijonon ensimmäisen merkin.

```python
def ensimmainen(merkkijono):
     # kirjoita koodia tähän

# kokeillaan funktiota:
if __name__ == "__main__":
    ensimmainen('python')
    ensimmainen('yhtälö')
    ensimmainen('tieto')
    ensimmainen('huominen')
    ensimmainen('omena')
    ensimmainen('nukkumaanmenoaika')
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

Håll koll på möjliga ”speciella fall”. Hur kommer funktionen att fungera om argumentet till exempel är noll eller negativt? Eller ett flyttal istället för ett heltal? Vad händer om argumentet är en tom sträng?

Om en uppgift inte förutsätter att du anropar en funktion kan du ändå göra det. Använd då ett if-block enligt det som beskrevs tidigare. Testen kommer att ignorera koden inom det här blocket.

</text-box>

## Fler exempel

Vi tar en titt på fler exempelfunktioner som tar emot argument. Här är parametern en siffra:

```python
def nelio(x):
    print(f"Luvun {x} neliö on {x * x}")

nelio(2)
nelio(5)
```

<sample-output>

Luvun 2 neliö on 4
Luvun 5 neliö on 25

</sample-output>

Här har vi en if-sats inom en funktion:

```python
def tervehdi(nimi):
    if nimi == "Emilia":
        print("Heippa,", nimi)
    else:
        print("Moikka,", nimi)

tervehdi("Emilia")
tervehdi("Matti")
```

<sample-output>

Heippa, Emilia
Moikka, Matti

</sample-output>

Den här funktionen tar emot två argument:

```python
def summa(x, y):
    tulos = x + y
    print(f"Parametrien {x} ja {y} summa on {tulos} ")

summa(1, 2)
summa(5, 24)
```

<sample-output>

Parametrien 1 ja 2 summa on 3
Parametrien 5 ja 24 summa on 29

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

Parametrien 1 ja 2 summa on 3
Parametrien 130 ja 10 summa on 140

</sample-output>

I det första funktionsanropet får parametrarna värdena `x = 1` och `y = 2`. I det andra anropet får de värdena `x = 130` och `y = 10`. Det här oavsett att vi i anropet använder variabler med samma namn.

I nästa modul återkommer vi till funktionsdefinitioner.

<!--vastaava varoitusteksti löytyy osioista 3-4, 4-6 ja 5-1, tsekkaa kaikki jos muokkaat tätä-->
## Varning: globala variabler inom funktioner

I exemplen ovan observerade vi att det är möjligt att tilldela nya variabler i funktionsdefinitioner. Funktionen kan också se variabler utanför funktionen, i huvudfunktionen. Dessa variabler kallas globala variabler.

Att använda globala variabler från funktioner är oftast en dålig idé. Det kan orsaka en hel del problem, till exempel orsaka buggar som är svåra att spåra.

Här är ett exempel på en funktion som använder en global variabel ”av misstag”:

```python
# globaali muuttuja
nimi = "Emilia"

def tervehdi(etunimi):
    # tulostetaan vahingossa parametrin sijaan globaalin muuttujan arvo
    print("Hei", nimi)

tervehdi("Antti")
tervehdi("Emilia")
```

<sample-output>

Hei Emilia
Hei Emilia

</sample-output>

Oavsett vilka argument vi anropar funktionen med skrivs värdet ”Beatrice” från den globala variabeln ut.

<in-browser-programming-exercise name="Keskiarvo" tmcname="osa03-25_keskiarvo">

Tee funktio `keskiarvo`, joka saa parametrina kolme kokonaislukua. Funktio tulostaa parametriensa keskiarvon.

```python
keskiarvo(5, 3, 1)
keskiarvo(10, 1, 1)
```

<sample-output>

3.0
4.0

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Monta tulostusta" tmcname="osa03-24_monta_tulostusta">

Tee funktio `tulosta_monesti(merkkijono, kertaa)`, joka saa parametriksi merkkijonon sekä kokonaisluvun, joka kertoo, montako kertaa funktion tulee tulostaa parametrina saamansa merkkijono:

```python
tulosta_monesti("hei", 5)

print()

merkkijono = "Alussa olivat suo, kuokka ja Python"
kertaa = 3
tulosta_monesti(merkkijono, kertaa)
```
<sample-output>

hei
hei
hei
hei
hei

Alussa olivat suo, kuokka ja Python.
Alussa olivat suo, kuokka ja Python.
Alussa olivat suo, kuokka ja Python.

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Risuneliö" tmcname="osa03-23_risunelio">

Tee funktio `risunelio(pituus)` joka saa parametriksi kokonaisluvun, joka kertoo kuinka suuri risuneliö funktion pitää tulostaa:

```python
risunelio(3)
print()
risunelio(5)
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

<in-browser-programming-exercise name="Shakkilauta" tmcname="osa03-26_shakkilauta">

Tee funktio `shakkilauta`, joka tulostaa shakkilaudan numeroista 0 ja 1 alla olevien esimerkkien mukaisesti.

```python
shakkilauta(3)
print()
shakkilauta(6)
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


<in-browser-programming-exercise name="Sananeliö" tmcname="osa03-27_sananelio">

Tee funktio `nelio`, joka tulostaa sananeliön alla olevien esimerkkien mukaisesti.

```python
nelio("ab", 3)
print()
nelio("aybabtu", 5)
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
