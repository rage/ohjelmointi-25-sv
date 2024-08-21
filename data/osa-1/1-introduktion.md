---
path: '/osa-1/1-introduktion'
title: 'Introduktion'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* har du skrivit och kört ditt första Python-program
* vet du hur man använder print-instruktionen
* kan du utföra räkneoperationer genom att programmera.

</text-box>

Datorprogram består av instruktioner eller kommandon. Varje kommando instruerar datorn att göra en viss sak. Datorn utför varje instruktion ett för ett. Instruktionerna kan till exempel användas för att utföra räkneoperationer, jämföra saker i datorns minne, göra ändringar i hur programmet fungerar, förmedla meddelanden eller fråga något av programmets användare.

Låt oss börja programmera genom att bekanta oss med `print`-instruktionen som skriver ut (print) text. I praktiken betyder det att programmet visar någon text på skärmen.

Det följande programmet skriver ut texten "Hej!":

```python
print("Hej!")
```

När programmet körs, blir resultatet det följande:

<sample-output>

Hej!

</sample-output>

Programmet fungerar inte om koden inte skrivs exakt som den är ovan. Om man till exempel kör programmet utan citattecken, på följande sätt…

```python
print(Hej!)
```

…så kommer texten "Hej!" inte att skrivas ut. Istället får vi ett felmeddelande:

<sample-output>

<pre>
File "<stdin>", line 1
  print(Hej!)
                   ^
SyntaxError: invalid syntax
</pre>

</sample-output>

Sammanfattningsvis: För att skriva ut text, måste den vara inom citattecken för att Python ska kunna tolka den korrekt.

<in-browser-programming-exercise name="Leende" tmcname="osa01-01_leende" height="300px">

Gör ett program som skriver ut ett leende: :-)

</in-browser-programming-exercise>

## Ett program med flera instruktioner

Flera instruktioner som skrivs efter varandra körs i ordning från det första till det sista. Till exempel följande program…

```python
print("Välkommen till vår programmeringskurs!")
print("För att börja ska vi testa på print-instruktionen.")
print("Det här programmet skriver ut tre rader text.")
```

…skriver ut dessa textrader på skärmen:

<sample-output>

Välkommen till vår programmeringskurs!
För att börja ska vi testa på print-instruktionen.
Det här programmet skriver ut tre rader text.

</sample-output>

<in-browser-programming-exercise name="Fixa programmet: Sju bröder" tmcname="osa01-03_sju_broder">

Det här programmet borde skriva ut namnet på sju bröder i alfabetisk ordning. Det finns ändå några fel i programmet. Korrigera dem, så att namnen skrivs ut i korrekt ordning.

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


<in-browser-programming-exercise name="Gubben Noak" tmcname="osa01-02_gubben_noak">

Gör ett program som skriver ut följande textrader (exakt som de står nedan):

<sample-output>

Gubben Noak, gubben Noak var en hedersman
När han gick ur arken plantera han på marken
Gubben Noak, gubben Noak var en hedersman.

</sample-output>

</in-browser-programming-exercise>


## Räkneoperationer

Du kan också utföra räkneoperationer i `print`-instruktionen. När instruktionen körs, kommer resultatet av operationen att skrivas ut på skärmen. Till exempel detta program…

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

Observera att citattecknen fattas från instruktionerna med räkneoperationer. Citattecknen används för att markera strängar. Inom programmering är strängar en serie bestående av tecken. Strängar kan innehålla bokstäver, siffror och alla andra typer av tecken – till exempel skiljetecken. Strängar är inte nödvändigtvis bara ord utan kan vara flera meningar långa. Strängar skrivs vanligtvis ut exakt så som de är skrivna. Därmed ger dessa två instruktioner mycket olika resultat:

```python
print(2 + 2 * 10)
print("2 + 2 * 10")
```

Programmet skriver ut:

<sample-output>

22
2 + 2 * 10

</sample-output>

I instruktionen på den andra raden utför Python inte några räkneoperationer utan skriver ut operationen som sådan, en sträng. Strängar skrivs alltså ut som sådana oavsett deras innehåll.

## Kommentarer

Om en rad börjar med tecknet `#`, tolkas raden som en kommentar. Det innebär att en rad som börjar med `#` inte påverkar programmets funktion på något sätt – Python ignorerar helt enkelt hela raden.

Kommentarer kan användas för att beskriva hur ett program fungerar – både för programmeraren och för andra personer som läser koden. I det här programmet finns en kommentar som beskriver räkneoperationen som utförs:

```python
print("Antal timmar i ett år:")
# ett år består av 365 dagar och varje dag av 24 timmar
print(365*24)
```

När programmet körs, kommer kommentaren inte att synas för användaren:

<sample-output>

Antal timmar i ett år:
8760

</sample-output>

Korta kommentarer kan också skrivas i slutet på en rad, på följande sätt:

```python
print("Antal timmar i ett år:")
print(365*24) # 365 dagar, 24 timmar per dag
```

<in-browser-programming-exercise name="Minuter i ett år" tmcname="osa01-04_minuter_per_ar">

Gör ett program som skriver ut antalet minuter i ett år. Låt Python utföra räkneoperationen som i exemplet ovan.

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Kod som skriver ut kod" tmcname="osa01-05_skriv_ut_kod">

Istället för dubbla citattecken (`"`) kan man i Python också använda enkla citattecken ( `'`).

Det här kan vara nyttigt till exempel i situationer där man vill skriva ut citattecken:

```python
print('"Kom tillbaka direkt!", vrålade polisen.')
```

<sample-output>

"Kom tillbaka direkt!", vrålade polisen.

</sample-output>

Skapa ett program som skriver ut det följande:

<sample-output>

print("Hej!")

</sample-output>

</in-browser-programming-exercise>

Kertauskysely tämän osan asioihin liittyen:

<quiz id="4b736942-71b8-5171-8427-508b57d1776b"></quiz>
