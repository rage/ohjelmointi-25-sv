---
path: '/osa-1/2-info-fran-anvandaren'
title: 'Information från användaren'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* vet du hur man skriver ett program som kan läsa in information av användaren
* vet du hur man använder variabler för att lagra indata och skriva ut motsvarande värden
* kan du kombinera strängar.

</text-box>

Indata (input) syftar till information som programmet läser in från omvärlden. Det kan handla om allt från indata från tangentbordet eller musklick till sensorer. I Python används `input` för att läsa in en rad text som användaren matar in. `input` kan också användas för att skriva ut ett meddelande till användaren för att be om någon specifik information.

Det här programmet läser in användarens namn med hjälp av `input`. Därefter skriver programmet ut namnet med `print`:

```python
namn = input("Ange ditt namn: ")
print("Hej på dig, " + namn)
```

När programmet körs, kan det se ut så här (indata från användaren markerat med rött):

<sample-output>

Ange ditt namn: **Pauline Python**
Hej på dig, Pauline Python

</sample-output>

Vad programmet skriver ut beror här på den information som användaren ger. Utskriften kommer alltså att variera beroende på vad användaren matar in:

<sample-output>

Ange ditt namn: **Kira Kodare**
Hej på dig, Kira Kodare

</sample-output>

Ordet `namn` i programmet ovan är en variabel. Inom programmering är en variabel ett ställe för att lagra ett värde – till exempel en sträng eller ett nummer. Värdet kan användas senare och det kan också ändras.

<text-box variant="hint" name="Att namnge variabler">

I princip kan variabler namnges relativt fritt, men Python har några begränsningar som måste tas i beaktande.

Det är vanligt att namnge variabler på engelska, men du kan stöta på variabler som namngetts på andra språk – till exempel på programmerarens eget modersmål. Variabelns namn påverkar inte dess värde, så det har inte en direkt påverkan på programmets funktion. Däremot kan variabler namngivna på engelska förtydliga kodens funktion för läsaren – förutsatt att variablerna har logiska namn. Det viktigaste är att använda variabelnamn som gör koden lättläst och förståelig både för dig som programmerar och för andra som till exempel behöver granska koden.

</text-box>

<in-browser-programming-exercise name="Namn, två gånger" tmcname="osa01-06_namn_tva_ganger">

Gör ett program som frågar efter användarens förnamn. Programmet ska sedan skriva ut namnet två gånger på varandra följande rader.

Så här ska programmet fungera:

<sample-output>

Ange ditt namn: **Pauline**
Pauline
Pauline

</sample-output>

</in-browser-programming-exercise>

## Hänvisa till en variabel

En viss variabel kan hänvisas till flera gånger i ett program:

```python
namn = input("Ange ditt namn: ")

print("Hej, " + namn + "!")
print(namn + " är ett ganska fint namn.")
```

Om användaren ger namnet `Paulus Python`, skriver programmet ut följande rader:

<sample-output>

Ange ditt namn: **Paulus Python**
Hej, Paulus Python!
Paulus Python är ett ganska fint namn.

</sample-output>

Låt oss undersöka närmare hur `print` används ovan. Mellan parenteserna i instruktionen finns det både text inom citattecken och namn på variabler, som hänvisar till indata från användaren. De har kombinerats med `+`-operatorn, som kombinerar två strängar till en sträng.


Strängar och variabler kan kombineras ganska fritt:

```python
namn = input("Ange ditt namn: ")

print("Hej " + namn + "! Ditt namn var alltså " + namn + "?")
```

Om användaren ger namnet `Ellen Exempel`, skrivs följande ut:

<sample-output>

Ange ditt namn: **Ellen Exempel**
Hej Ellen Exempel! Ditt namn var alltså Ellen Exempel?

</sample-output>

<in-browser-programming-exercise name="Namn med utropstecken" tmcname="osa01-07_namn_utropstecken">

Skriv ett program som frågar efter användarens förnamn. Programmet ska skriva ut det angivna namnet två gånger på samma rad, så att det finns ett utropstecken mellan namnen och i början och slutet av raden.

Så här ska programmet fungera:

<sample-output>

Ange ditt namn: **Sandrine**
!Sandrine!Sandrine!

</sample-output>

</in-browser-programming-exercise>

## Samla mera data

Ett program kan be användaren att mata in data flera gånger. Observera att vi då behöver flera variabler för att lagra de olika värdena som användaren matar in via `input`.

```python
namn = input("Ange ditt namn: ")
epost = input("Ange din e-postadress: ")
smeknamn = input("Ange ditt smeknamn: ")

print("Vi kollar ännu att alla uppgifter är korrekta")
print("Ditt namn: " + namn)
print("Din e-postadress: " + epost)
print("Ditt smeknamn: " + smeknamn)
```

Programmet kunde till exempel fungera så här när det körs:

<sample-output>

Ange ditt namn: **Per-Pierre Påhittad**
Ange din e-postadress: **perpierre01@example.com**
Ange ditt smeknamn: **PP**
Vi kollar ännu att alla uppgifter är korrekta
Ditt namn: Per-Pierre Påhittad
Din e-postadress: perpierre01@example.com
Ditt smeknamn: PP

</sample-output>

Om en och samma variabel används för att lagra indata flera gånger kommer det nyaste värdet alltid att ersätta det föregående värdet. Till exempel:

```python
gata = input("Vilken är din gatuadress? ")
print("Du bor alltså på " + gata)

gata = input("Ange en ny gatuadress: ")
print("Gatuadressen är nu " + gata)
```

Så här kan det se ut när programmet körs:

<sample-output>

Vilken är din gatuadress? **Pythonparken 7**
Du bor alltså på Pythonparken 7
Ange en ny gatuadress: **Gredelingatan 17 B 231**
Gatuadressen är nu Gredelingatan 17 B 231

</sample-output>

Det här betyder att om samma variabel används för att lagra indata två gånger i rad så kommer det första värdet inte längre att vara tillgängligt efter att det har ersatts:

```python
gata = input("Vilken är din gatuadress? ")
gata = input("Ange en ny gatuadress: ")

print("Gatuadressen är nu " + gata)
```

Så här kan det se ut när programmet körs:

<sample-output>

Vilken är din gatuadress? **Slitagestigen 2**
Ange en ny gatuadress: **Värjan 1**
Gatuadressen är nu Värjan 1

</sample-output>

<in-browser-programming-exercise name="Namn och adress" tmcname="osa01-08_namn_adress">

Skapa ett program som frågar efter användarens namn och adress. Skriv sedan ut dem.

Så här ska programmet fungera:

<sample-output>

Förnamn: **Cecilia**
Efternamn: **Citronlik**
Gatuadress: **Bulevarden 12**
Postnummer och adressort: **00120 HELSINGFORS**
Cecilia Citronlik
Bulevarden 12
00120 HELSINGFORS

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Fixa programmet: Uttryck" tmcname="osa01-09_uttryck">

I den här uppgiften finns ett program som borde fråga användaren efter tre ord och skriva dem ut på följande sätt.

<sample-output>

Ge ord 1: **ärtan**
Ge ord 2: **pärtan**
Ge ord 3: **puff**
ärtan-pärtan-puff!

</sample-output>

Det finns några problem i koden som du nu borde lösa, så att programmet fungerar korrekt.

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Berättelse" tmcname="osa01-10_berattelse">

Skapa ett program som skriver ut den följande berättelsen. Namnet och årtalet användaren anger ska användas i texten.

<sample-output>

Ange namn: **Amelie**
Ange år: **1993**

Amelie är kommunens bästa läkare. När Amelie, född 1993, vaknar till ett telefonsamtal klockan 4 på morgonen, blir det brådis. Amelie behövs till akuten för att rädda livet hos en cyklist som krockat med en bil.

</sample-output>

Berättelsen ska ändras beroende på de värden användaren anger.

</in-browser-programming-exercise>

Du hittar ett repetitionsquiz för denna del här: 

<quiz id="c22a95c7-7ce7-59be-beff-7a67423fbf49"></quiz>
