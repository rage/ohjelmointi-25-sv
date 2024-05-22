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
nimi = "Erkki"
ika = 39
print("Hei " + nimi + " ikäsi on " + str(ika) + " vuotta" )
```

Den här metoden fungerar inte då något av segmenten inte är strängar. I exemplet ovan har variabeln `alder` konverterats till en sträng med funktionen `str`, i och med att variabeln är ett heltal.

Den andra metoden är att ge alla delar av strängen som skilda argument, skiljandes dem med komma:

```python
print("Hei", nimi, "ikäsi on", ika, "vuotta" )
```

Den här koden ger likadant resultat som den föregående versionen. `print`-kommandot lägger vanligtvis ett mellanslag mellan varje argument. Det positiva är att olika segment kan ha olika datatyper, så man behöver inte konvertera någonting till en sträng.

Om du vill avlägsna mellanslagen som läggs till automatiskt, kan du ge ett argument med namnet `sep`:

```python
print("Hei", nimi, "ikäsi on", ika, "vuotta", sep="")
```

Det här skriver ut:

<sample-output>

HeiErkkiikäsi on39vuotta

</sample-output>


Argumentet `sep=””` är ett namngivet argument. Det specificerar att alla argument ska avgränsas med en tom sträng. Du kan använda vilken som helst sträng som avgränsare. Till exempel om du vill ha varje argument på en skild rad kan du använda avgränsaren `”\n”` som är en radbrytning.

```python
print("Hei", nimi, "ikäsi on", ika, "vuotta", sep="\n")
```

<sample-output>

Hei
Erkki
ikäsi on
39
vuotta

</sample-output>

Vanligtvis avslutas `print`-kommandot med en radbrytning, men du kan också ändra på det här. Det namngivna argumentet `end` bestämmer vad som ska finnas i slutet av en rad. Om end är en tom sträng, kommer ingen radbrytning att skrivas ut i slutet av utskriften:

```python
print("Moi ", end="")
print("kaikki!")
```

<sample-output>

Moi kaikki!

</sample-output>

## F-strängar

Det tredje sättet att förbereda strängar för utskrift är f-strängar. Det föregående exemplet med namnet och åldern skulle se så här ut med f-strängar:

```python
nimi = "Erkki"
ika = 39
print(f"Hei {nimi} ikäsi on {ika} vuotta")
```

Hittills har vi bara använt oss av enkla f-strängar, men de är väldigt flexibla när det kommer till formatering av innehållet i strängen. Ett vanligt användningsområde är att specificera antalet decimaler hos ett flyttal. Normalt är antalet ganska stort:

```python
luku = 1/3
print(f"Luku on {luku}")
```

<sample-output>

Luku on 0.333333333333333

</sample-output>

Vi kan ändra på detta med hjälp av att inom klammerparenteser ge variabelnamnet och formateringsinstruktioner:

```python
luku = 1/3
print(f"Luku on {luku:.2f}")
```

```python
Luku on 0.33
```

Instruktionen `.2f` berättar att vi vill visa två decimaler. Bokstaven f betyder att vi vill visa variabeln som ett flyttal.

Här är ett annat exempel där vi ger ett visst mellanrum som är reserverat för en specifik variabel i utskriften. I båda fallen inkluderas variabeln namn i den resulterande strängen, med 15 tecken reserverat utrymme. Först är namnen vänsterjusterade, sedan högerjusterade:

```python
nimet =  [ "Antti", "Emilia", "Juha-Pekka", "Maya" ]
for nimi in nimet:
  print(f"{nimi:15} keskellä {nimi:>15}")
```

```python
Antti           keskellä           Antti
Emilia          keskellä          Emilia
Juha-Pekka      keskellä      Juha-Pekka
Maya            keskellä            Maya
```

Man kan också använda f-strängar utanför print-kommandon. De kan tilldelas till variabler och kombineras med andra strängar:

```python
nimi = "Pekka"
ika = 59
kaupunki = "Lappeenranta"
tervehdys = f"Hei {nimi}, olet {ika}-vuotias"
print(tervehdys + f", asuinpaikkasi on {kaupunki}")
```

<sample-output>

Hei Pekka, olet 59-vuotias, asuinpaikkasi on Lappeenranta

</sample-output>

Du kan tänka att f-strängen är en slags funktion som skapar en normal sträng baserat på ”argumenten” mellan klammerparenteserna.

<programming-exercise name='Lukulistasta merkkijonolistaksi' tmcname='osa04-20_lukulistasta_merkkijonolistaksi'>

Kirjoita funktio `muotoile`, joka saa parametrikseen liukulukuja sisältävän listan. Funktio muodostaa listan perusteella uuden merkkijonoja sisältävän listan, jossa jokainen liukulukulistan alkio esitetään pyöristettynä kahden desimaalin tarkkuuteen. Listan alkioiden järjestyksen tulee säilyä.

_Vinkki: Käytä liukulukujen muotoiluun merkkijonoiksi f-merkkijonoa._

Esimerkki funktion käytöstä:

```python
lista = [1.234, 0.3333, 0.11111, 3.446]
lista2 = muotoile(lista)
print(lista2)
```

<sample-output>

['1.23', '0.33', '0.11', '3.45']

</sample-output>

</programming-exercise>

<quiz id="92e6d079-80c1-5914-8cf7-abd181a418dd"></quiz>
