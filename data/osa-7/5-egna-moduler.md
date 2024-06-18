---
path: '/osa-7/5-egna-moduler'
title: 'Skapa dina egna moduler'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* kan du skapa dina egna moduler
* vet du vad Python-variabeln `__name__` och värdet `__main__` har för betydelse.

</text-box>

Att skapa dina egna Python-moduler är enkelt. Vilken som helst fil som innehåller valid Python-kod kan importeras som en modul. Låt oss säga att vi har filen `ord.py`, med följande innehåll:

```python
def ord_ett(strang: str):
    delar = strang.split(" ")
    return delar[0]

def sista_ordet(strang: str):
    delar = strang.split(" ")
    return delar[-1]

def antal_ord(strang: str):
    delar = strang.split(" ")
    return len(delar)
```

Funktionerna som definierats i filen kan kommas åt genom att importera filen:

```python
import ord

strang = "Polisstationen var full"

print(ord.ord_ett(strang))
print(ord.sista_ordet(strang))
print(ord.antal_ord(strang))
```

<sample-output>

Polisstationen
full
3

</sample-output>

Obs! Filen som innehåller Python-modulen måste befinna sig i samma mapp där programmet som importerar modulen finns i. Alternativt kan filen med modulen vara i någon av de andra mappar där Python söker moduler ifrån. I övriga fall kommer Pythontolken inte att hitta modulen när `import`-satsen körs.

Vi kan använda våra moduler exakt på samma sätt som moduler i Pythons standardbibliotek:

```python
from ord import ord_ett, sista_ordet

mening = input("Ange mening: ")

print("Första ordet var: " + ord_ett(mening))
print("Sista ordet var: " + sista_ordet(mening))
```

<sample-output>

Ange mening: **Han höll på att svimma i den heta bussen**
Första ordet var: Han
Sista ordet var: bussen

</sample-output>

## Använda typledtrådar

När vi använder moduler är typledtrådar speciellt till nytta. Om du använder en kodeditor som stödjer typledtrådar, kommer användandet av moduler att bli mycket enklare.

Till exempel Visual Studio Code visar typledtrådar medan du skriver kod:

<img src="7_vihje.png">

## Kod i modulens huvudfunktion

Om en modul innehåller kod som inte finns inom en funktionsdefinition (dvs. kod i huvudfunktionen), kommer den här koden att köras automatiskt då modulen importeras.

Låt oss se på en situation där `ord.py` innehåller några testutskrifter:

```python
def ord_ett(strang: str):
    delar = strang.split(" ")
    return delar[0]

def sista_ordet(strang: str):
    delar = strang.split(" ")
    return delar[-1]

def antal_ord(strang: str):
    delar = strang.split(" ")
    return len(delar)

print(ord_ett("Det här är ett test"))
print(sista_ordet("Ett annat test"))
print(antal_ord("Postlådan var full med tidningar"))
```

Om vi nu importerar modulen med en `import`-sats, kommer all kod utanför de definierade funktionerna att köras:

```python
import ord

strang = "Polisstationen var full"

print(ord.ord_ett(strang))
print(ord.sista_ordet(strang))
print(ord.antal_ord(strang))
```

<sample-output>

Det
test
5
Polisstationen
full
3

</sample-output>

Som du ser, är det här inte en riktigt bra sak i vår situation, eftersom vår utskrift nu blandas med testutskrifter från modulen.

Till all lycka finns en lösning, och den är bekant sedan tidigare. Vi måste helt enkelt testa om programmet körs självständigt eller om koden har importerats med en `import`-sats. Python har en inbyggd variabel `__name__` som innehåller namnet på programmet som körs. Om programmet körs självständigt är värdet på den nyss nämnda variabeln `__main__`. Om programmet däremot har importerats är värdet på variabeln namnet på modulen som importerats (i vårt fall `ord`).

Nu när vi vet det här kan vi lägga till en if-sats som låter oss köra våra test endast då programmet körs självständigt. Som du ser nedan, är strukturen bekant:

```python
def ord_ett(strang: str) -> str:
    delar = strang.split(" ")
    return delar[0]

def sista_ordet(strang: str) -> str:
    delar = strang.split(" ")
    return delar[-1]

def antal_ord(strang: str) -> int:
    delar = strang.split(" ")
    return len(delar)

if __name__ == "__main__":
    # testar funktionerna
    print(ord_ett("Det här är ett test"))
    print(sista_ordet("Ett annat test"))
    print(sanojen_lkm("Postlådan var full med tidningar"))
```

Om du kör modulen självständigt, skrivs testutskrifterna ut:

<sample-output>

Det
test
5

</sample-output>

När modulen importeras i ett program, kommer testutskrifterna inte att göras:

```python
import ord

strang = "Polisstationen var full"

print(ord.ord_ett(strang))
print(ord.sista_ordet(strang))
print(ord.antal_ord(strang))
```

<sample-output>

Polisstationen
full
3

</sample-output>

I uppgifterna under den här kursen har du flera gånger ombetts att ha dina test under ett `if __name__ == "__main__"` -block. Nu vet du varför.

<programming-exercise name='Teckenverktyg' tmcname='osa07-17_merkkiapuri'>

Skapa modulen `teckenverktyg` som innehåller de följande funktionerna:

* `byt_storlek(strang: str)`: returnerar den givna strängen så att versaler och gemener har konverterats till gemener respektive versaler
* `halvera(strang: str)`: returnerar den givna strängen halverad i en tuple, vid behov är den första halvan kortare
* `specialtecken_bort(stang: str)` returnerar den givna strängen så att andra tecken än a-ö, A-Ö, siffror och mellanslag är avlägsnade.

Exempel:

```python
import teckenverktyg

strang = "Hej alla!"

print(teckenverktyg.byt_storlek(strang))

p1, p2 = teckenverktyg.halvera(strang)

print(p1)
print(p2)

m2 = teckenverktyg.specialtecken_bort("Det här är ett test, men hur går det??00")
print(m2)
```

<sample-output>

hEJ ALLA!
Hej
alla!
Det här är ett test men hur går det00

</sample-output>

</programming-exercise>

<quiz id="caf731dc-cf22-5dfc-ad4d-a3224b2df020"></quiz>

Vänligen svara på en kort enkät om materialet för den här veckan.

<quiz id="7794fe8b-1641-5a54-94d5-16d900a14d13"></quiz>
