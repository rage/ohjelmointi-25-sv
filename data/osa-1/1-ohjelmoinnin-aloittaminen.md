---
path: '/osa-1/1-ohjelmoinnin-aloittaminen'
title: 'Introduktion'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* har du skrivit och kört ditt första Python-program
* vet du hur man använder print-kommandot
* kan du utföra räkneoperationer genom att programmera.

</text-box>

Datorprogram består av kommandon. Varje kommando instruerar datorn att göra en viss sak. Datorn utför varje kommando ett för ett. Kommandona kan till exempel användas för att utföra räkneoperationer, jämföra saker i datorns minne, göra ändringar i hur programmet fungerar, förmedla meddelanden eller fråga något av programmets användare.

Låt oss börja programmera genom att bekanta oss med `print`-kommandot som skriver ut (print) text. I praktiken betyder det att programmet visar någon text på skärmen.

Det följande programmet skriver ut texten "Hej!":

```python
print("Moi kaikki!")
```

När programmet körs, blir resultatet det följande:

<sample-output>

Moi kaikki!

</sample-output>

Programmet fungerar inte om koden inte skrivs exakt som den är ovan. Om man till exempel kör programmet utan citattecken, på följande sätt…

```python
print(Moi kaikki!)
```

…så kommer texten "Hej!" inte att skrivas ut. Istället får vi ett felmeddelande:

<sample-output>

<pre>
File "<stdin>", line 1
  print(Moi kaikki!)
                   ^
SyntaxError: invalid syntax
</pre>

</sample-output>

Sammanfattningsvis: För att skriva ut text, måste den vara inom citattecken för att Python ska kunna tolka den korrekt.

<in-browser-programming-exercise name="Hymiö" tmcname="osa01-01_hymio" height="300px">

Kirjoita ohjelma, joka tulostaa ruudulle hymiön: :-)

</in-browser-programming-exercise>

## Ett program med flera kommandon

Flera kommandon som skrivs efter varandra körs i ordning från det första till det sista. Till exempel följande program…

```python
print("Tervetuloa opettelemaan ohjelmointia!")
print("Aluksi harjoitellaan print-komennon käyttöä.")
print("Tämä ohjelma tulostaa ruudulle kolme riviä tekstiä.")
```
…skriver ut dessa textrader på skärmen:

<sample-output>

Tervetuloa opettelemaan ohjelmointia!
Aluksi harjoitellaan print-komennon käyttöä.
Tämä ohjelma tulostaa ruudulle kolme riviä tekstiä.

</sample-output>

<in-browser-programming-exercise name="Korjaa ohjelma: seitsemän veljestä" tmcname="osa01-03_korjaa_ohjelma_7_veljesta">

Ohjelman tarkoitus on tulostaa seitsemän veljestä aakkosjärjestyksessä. Ohjelmassa on kuitenkin yksi tai useampi virhe, jonka takia se ei toimi oikein.
Korjaa ohjelma niin, että veljekset tulostuvat oikeassa järjestyksessä.

```python
print("Simeoni")
print("Juhani")
print("Eero")
print("Lauri")
print("Aapo")
print("Tuomas")
print("Timo")
```

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Ukko Nooa" tmcname="osa01-02_ukko_nooa">

Kirjoita ohjelma, joka tulostaa ruudulle seuraavat rivit (tarkalleen annetussa muodossa välimerkkeineen):

<sample-output>

Ukko Nooa, Ukko Nooa oli kunnon mies.
Kun hän meni saunaan, laittoi laukun naulaan.
Ukko Nooa, Ukko Nooa oli kunnon mies.

</sample-output>

</in-browser-programming-exercise>


## Räkneoperationer

Du kan också utföra räkneoperationer i `print`-kommandot. När kommandot körs, kommer resultatet av operationen att skrivas ut på skärmen. Till exempel detta program…

```python
print(2 + 5)
print(3 * 3)
print(2 + 2 * 10)
```
…skriver ut följande textrader:

<sample-output>

7
9
22

</sample-output>

Observera att citattecknen fattas från kommandona med räkneoperationer. Citattecknen används för att markera strängar. Inom programmering är strängar en serie bestående av tecken. Strängar kan innehålla bokstäver, siffror och alla andra typer av tecken – till exempel skiljetecken. Strängar är inte nödvändigtvis bara ord utan kan vara flera meningar långa. Strängar skrivs vanligtvis ut exakt så som de är skrivna. Därmed ger dessa två kommandon mycket olika resultat:

```python
print(2 + 2 * 10)
print("2 + 2 * 10")
```

Programmet skriver ut:

<sample-output>

22
2 + 2 * 10

</sample-output>

I kommandot på den andra raden utför Python inte några räkneoperationer utan skriver ut operationen som sådan, en sträng. Strängar skrivs alltså ut som sådana oavsett deras innehåll.

## Kommentarer

Om en rad börjar med tecknet `#`, tolkas raden som en kommentar. Det innebär att en rad som börjar med `#` inte påverkar programmets funktion på något sätt – Python ignorerar helt enkelt hela raden.

Kommentarer kan användas för att beskriva hur ett program fungerar – både för programmeraren och för andra personer som läser koden. I det här programmet finns en kommentar som beskriver räkneoperationen som utförs:

```python
print("Tuntien määrä vuodessa:")
# vuodessa on 365 päivää ja jokaisessa 24 tuntia
print(365*24)
```

När programmet körs, kommer kommentaren inte att synas för användaren:

<sample-output>

Tuntien määrä vuodessa:
8760

</sample-output>

Korta kommentarer kan också skrivas i slutet på en rad, på följande sätt:

```python
print("Tuntien määrä vuodessa:")
print(365*24) # 365 päivää, 24 tuntia päivässä
```

<in-browser-programming-exercise name="Minuutit vuodessa" tmcname="osa01-04_minuuttien_maara_vuodessa">

Tee ohjelma, joka tulostaa minuuttien määrän vuodessa. Käytä edellisen esimerkin tapaan Pythonia tekemään laskutoimitus!

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Ohjelma tulostaa koodia" tmcname="osa01-05_ohjelma_tulostaa_koodia">

Pythonissa voidaan käyttää kaksinkertaisten lainausmerkkien `"` lisäksi myös yksinkertaista lainausmerkkiä `'`.

Tämä on kätevää, kun haluat tulostaa lainausmerkkejä:

```python

print('"Heti takaisin!", poliisi huusi.')

```

<sample-output>

"Heti takaisin!", poliisi huusi.

</sample-output>

Tee ohjelma, jonka tulostus on seuraava:

<sample-output>

print("Moi kaikki!")

</sample-output>



</in-browser-programming-exercise>




Kertauskysely tämän osan asioihin liittyen:

<quiz id="90b76562-cc2b-5dd4-996b-895d7b5bc69e"></quiz>
