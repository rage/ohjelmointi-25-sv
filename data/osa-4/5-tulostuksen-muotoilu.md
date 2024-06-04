---
path: '/osa-4/5-tulostuksen-muotoilu'
title: 'Formatera utskrift'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* kan du använda argument för att påverka formatet på `print`-kommandots resultat
* kan du använda dig av f-strängar för att formatera utskrift.

</text-box>

Vi har redan lärt oss tre metoder för att ge argument till `print`-kommandot.

Det första är `+`-operatorn för strängar. Den tillåter enkel kombination av strängar:

```python
namn = "Elin"
alder = 22
print("Hej " + namn + " med din ålder på " + str(alder) + " år" )
```

Den här metoden fungerar inte då något av segmenten inte är strängar. I exemplet ovan har variabeln `alder` konverterats till en sträng med funktionen `str`, i och med att variabeln är ett heltal.

Den andra metoden är att ge alla delar av strängen som skilda argument, skiljandes dem med komma:

```python
print("Hej", namn, "med din ålder på", alder, "år" )
```

Den här koden ger likadant resultat som den föregående versionen. `print`-kommandot lägger vanligtvis ett mellanslag mellan varje argument. Det positiva är att olika segment kan ha olika datatyper, så man behöver inte konvertera någonting till en sträng.

Om du vill avlägsna mellanslagen som läggs till automatiskt, kan du ge ett argument med namnet `sep`:

```python
print("Hej", namn, "med din ålder på", alder, "år", sep="")
```

Det här skriver ut:

<sample-output>

HejElinmed din ålder på22år

</sample-output>


Argumentet `sep=""` är ett namngivet argument. Det specificerar att alla argument ska avgränsas med en tom sträng. Du kan använda vilken som helst sträng som avgränsare. Till exempel om du vill ha varje argument på en skild rad kan du använda avgränsaren `"\n"` som är en radbrytning.

```python
print("Hej", namn, "med din ålder på", alder, "år", sep="\n")
```

<sample-output>

Hej
Elin
med din ålder på
22
år

</sample-output>

Vanligtvis avslutas `print`-kommandot med en radbrytning, men du kan också ändra på det här. Det namngivna argumentet `end` bestämmer vad som ska finnas i slutet av en rad. Om end är en tom sträng, kommer ingen radbrytning att skrivas ut i slutet av utskriften:

```python
print("Hej ", end="")
print("allihopa!")
```

<sample-output>

Hej allihopa!

</sample-output>

## F-strängar

Det tredje sättet att förbereda strängar för utskrift är f-strängar. Det föregående exemplet med namnet och åldern skulle se så här ut med f-strängar:

```python
namn = "Elin"
alder = 22
print(f"Hej {namn} med din ålder på {alder} år")
```

Hittills har vi bara använt oss av enkla f-strängar, men de är väldigt flexibla när det kommer till formatering av innehållet i strängen. Ett vanligt användningsområde är att specificera antalet decimaler hos ett flyttal. Normalt är antalet ganska stort:

```python
siffra = 1/3
print(f"Siffran är {siffra}")
```

<sample-output>

Siffran är 0.333333333333333

</sample-output>

Vi kan ändra på detta med hjälp av att inom klammerparenteser ge variabelnamnet och formateringsinstruktioner:

```python
siffra = 1/3
print(f"Siffran är {siffra:.2f}")
```

```python
Siffran är 0.33
```

Instruktionen `.2f` berättar att vi vill visa två decimaler. Bokstaven f betyder att vi vill visa variabeln som ett flyttal.

Här är ett annat exempel där vi ger ett visst mellanrum som är reserverat för en specifik variabel i utskriften. I båda fallen inkluderas variabeln namn i den resulterande strängen, med 15 tecken reserverat utrymme. Först är namnen vänsterjusterade, sedan högerjusterade:

```python
namn =  ["Antonia", "Emilia", "Johan", "Maja"]
for person in namn:
  print(f"{person:15} mittplats {person:>15}")
```

```
Antonia         mittplats         Antonia
Emilia          mittplats          Emilia
Johan           mittplats           Johan
Maja            mittplats            Maja
```

Man kan också använda f-strängar utanför print-kommandon. De kan tilldelas till variabler och kombineras med andra strängar:

```python
namn = "Leffe"
alder = 59
stad = "Villmanstrand"
halsning = f"Hej {namn}, du är {alder} år"
print(halsning + f", du bor i {stad}")
```

<sample-output>

Hej Leffe, du är 59 år, du bor i Villmanstrand

</sample-output>

Du kan tänka att f-strängen är en slags funktion som skapar en normal sträng baserat på "argumenten" mellan klammerparenteserna.

<programming-exercise name='Lukulistasta merkkijonolistaksi' tmcname='osa04-20_lukulistasta_merkkijonolistaksi'>

Skapa funktionen `formatera` som får som argument en lista med flyttal. Funktionen ska returnera en ny lista som innehåller strängar med flyttalen avrundade till närmaste två decimaler. Ordningen av siffrorna ska vara den samma.

Tips: Använd f-strängar för att formatera flyttalen.

Exempel:

```python
lista = [1.234, 0.3333, 0.11111, 3.446]
lista2 = formatera(lista)
print(lista2)
```

<sample-output>

['1.23', '0.33', '0.11', '3.45']

</sample-output>

</programming-exercise>

<quiz id="92e6d079-80c1-5914-8cf7-abd181a418dd"></quiz>
