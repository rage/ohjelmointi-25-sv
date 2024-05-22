---
path: '/osa-1/2-tietoa-kayttajalta'
title: 'Information från användaren'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* vet du hur man skriver ett program som använder sig av information som användaren ger
* vet du hur man använder variabler för att lagra indata och skriva ut den
* kan du kombinera strängar.

</text-box>

Indata (input) syftar till information som en användare ger till ett program. I Python används kommandot `input` för att läsa in en rad text skriven av användaren. Kommandot kan också användas för att skriva ut ett meddelande till användaren för att be om någon specifik information.

Det här programmet läser in användarens namn med hjälp av `input`-kommandot. Därefter skriver programmet ut namnet med `print`-kommandot:

```python
nimi = input("Anna nimesi: ")
print("Moi vaan, " + nimi)
```

När programmet körs, kan det se ut så här (indata från användaren markerat med rött):

<sample-output>

Anna nimesi: **Pekka Python**
Moi vaan, Pekka Python

</sample-output>

Det programmet skriver ut beror delvis på den information som användaren ger. Därmed kan det också till exempel se ut så här när programmet körs:

<sample-output>

Anna nimesi: **Outi Ohjelmoija**
Moi vaan, Outi Ohjelmoija

</sample-output>

Ordet `namn` i programmet är en variabel. Inom programmering är en variabel ett ställe för att lagra ett värde – till exempel en sträng eller ett nummer. Värdet kan användas senare och det kan också ändras på.

<text-box variant="hint" name="Att namnge variabler">

I princip kan variabler namnges relativt fritt, men Python har några begränsningar som måste tas i beaktande.

Det är ett allmänt tillvägagångssätt att namnge variabler på engelska, men du kan stöta på variabler som namngetts på andra språk – till exempel på programmerarens eget modersmål. Variabelns namn påverkar inte dess värde, så det har inte en direkt påverkan på programmets funktion. Däremot kan variabler namngivna på engelska förtydliga kodens funktion för en läsare – förutsatt att variablerna har logiska namn.

</text-box>

<in-browser-programming-exercise name="Nimi kahdesti" tmcname="osa01-06_nimi_kahdesti">

Kirjoita ohjelma, joka kysyy käyttäjän nimeä ja tämän jälkeen tulostaa nimen kahteen kertaan peräkkäisille riveille.

Ohjelman tulee toimia seuraavasti:

<sample-output>

Anna nimesi: **Pekka**
Pekka
Pekka

</sample-output>

</in-browser-programming-exercise>

## Hänvisa till en variabel

En viss variabel kan hänvisas till flera gånger i ett program:

```python
nimi = input("Anna nimesi: ")

print("Moi, " + nimi + "!")
print(nimi + " on aika kiva nimi.")
```

Om användaren ger namnet `Paulus Python`, skriver programmet ut följande rader:

<sample-output>

Anna nimesi: **Pauli Python**
Moi, Pauli Python!
Pauli Python on aika kiva nimi.

</sample-output>

Låt oss undersöka närmare hur `print`-kommandot används ovan. Mellan parenteserna i kommandot finns det både text inom citattecken och namn på variabler, som hänvisar till indata från användaren. De har kombinerats med `+`-operatorn, som kombinerar två strängar till en sträng.


Strängar och variabler kan kombineras ganska fritt:

```python
nimi = input("Anna nimesi: ")

print("Moi " + nimi + "! Varmistan vielä: nimesi on siis " + nimi + "?")
```

Om användaren ger namnet `Ellen Exempel`, skrivs följande ut:

<sample-output>

Anna nimesi: **Erkki Esimerkki**
Moi Erkki Esimerkki! Varmistan vielä: nimesi on siis Erkki Esimerkki?

</sample-output>

<in-browser-programming-exercise name="Nimet huutomerkillä" tmcname="osa01-07_nimi_ja_huutomerkit">

Kirjoita ohjelma, joka kysyy käyttäjän nimeä ja tämän jälkeen tulostaa nimen kaksi kertaa samalle riville siten, että rivin alussa lopussa sekä nimien välissä on huutomerkki.

Ohjelman tulee toimia seuraavasti:

<sample-output>

Anna nimesi: **Pekka**
!Pekka!Pekka!

</sample-output>

</in-browser-programming-exercise>

## Samla mera data

Ett program kan be användaren att ge data flera gånger. Observera att `input`-kommandot lagrar varje givet värde i en skild variabel.

```python
nimi = input("Anna nimesi: ")
sposti = input("Anna sähköpostiosoitteesi: ")
lempinimi = input("Anna lempinimesi: ")

print("Varmistetaan vielä, että tiedot menivät oikein")
print("Nimesi: " + nimi)
print("Sähköpostiosoitteesi: " + sposti)
print("Lempinimesi: " + lempinimi)
```

Programmet kunde till exempel fungera så här när det körs:

<sample-output>

Anna nimesi: **Keijo Keksitty**
Anna sähköpostiosoitteesi: **keijo99@example.com**
Anna lempinimesi: **Keke**
Varmistetaan vielä, että tiedot menivät oikein
Nimesi: Keijo Keksitty
Sähköpostiosoitteesi: keijo99@example.com
Lempinimesi: Keke

</sample-output>

Om en och samma variabel används för att lagra indata flera gånger kommer det nyaste värdet alltid att ersätta det föregående värdet. Till exempel:

```python
osoite = input("Mikä on osoitteesi? ")
print("Asut siis osoitteessa " + osoite)

osoite = input("Anna uusi osoite: ")
print("Osoite on nyt " + osoite)
```

Så här kan det se ut när programmet körs:

<sample-output>

Mikä on osoitteesi? **Pythonpolku 1 A 10**
Asut siis osoitteessa Pythonpolku 1 A 10
Anna uusi osoite: **Uusikatu 999**
Osoite on nyt Uusikatu 999

</sample-output>

Det här betyder att om samma variabel används för att lagra indata två gånger i rad så kommer det första värdet inte längre att vara tillgängligt efter att det har ersatts:

```python
osoite = input("Mikä on osoitteesi? ")
osoite = input("Anna uusi osoite: ")

print("Osoite on nyt " + osoite)
```

Så här kan det se ut när programmet körs:

<sample-output>

Mikä on osoitteesi? **Pythonpolku 10**
Anna uusi osoite: **Ohjelmoijanraitti 230**
Osoite on nyt Ohjelmoijanraitti 230

</sample-output>

<in-browser-programming-exercise name="Nimi ja osoite" tmcname="osa01-08_nimi_ja_osoite">

Kirjoita ohjelma, joka kysyy käyttäjän nimeä ja osoitetta. Ohjelma tulostaa syötetyt tiedot.

Ohjelman tulee toimia seuraavasti:

<sample-output>

Etunimi: **Sanna**
Sukunimi: **Seppänen**
Katuosoite: **Mannerheimintie 10**
Postinumero ja kaupunki: **00100 Helsinki**
Sanna Seppänen
Mannerheimintie 10
00100 Helsinki

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name=" Korjaa ohjelma: Lausahdukset" tmcname="osa01-09_korjaa_ohjelma_lausahdukset">

Tehtäväpohjassa on annettu ohjelma, jonka pitäisi kysyä käyttäjältä kolme lausahdusta ja tulostaa ne esimerkin mukaisesti:

<sample-output>

Anna 1. osa: **entten**
Anna 2. osa: **tentten**
Anna 3. osa: **teelikamentten**
entten-tentten-teelikamentten!

</sample-output>

Ohjelmassa on kuitenkin virhe tai virheitä, joiden takia se ei toimi oikein. Korjaa ohjelma.

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Tarina" tmcname="osa01-10_tarina">

Tee ohjelma, joka tulostaa oheisen tarinan, johon on upotettu käyttäjän antama nimi ja vuosi.

<sample-output>

Anna nimi: **Maija**
Anna vuosi: **1572**

Maija on urhea ritari, syntynyt vuonna 1572. Eräänä aamuna Maija heräsi kovaan meluun: lohikäärme lähestyi kylää. Vain Maija voisi pelastaa kylän asukkaat.

</sample-output>

Tarinan tulee muuttua sen mukaan, mitkä tiedot käyttäjä antaa.


</in-browser-programming-exercise>

Kertauskysely tämän osan asioihin liittyen:

<quiz id="dd4441a3-c2a3-5553-97d6-30482b1f1126"></quiz>
