---
path: '/osa-7/5-omat-moduulit'
title: 'Skapa dina egna moduler'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* kan du skapa dina egna moduler
* vet du vad Python-variabeln `__name__` och värdet `__main__` har för betydelse.

</text-box>

Att skapa dina egna Python-moduler är enkelt. Vilken som helst fil som innehåller valid Python-kod kan importeras som en modul. Låt oss säga att vi har filen `ord.py`, med följande innehåll:

```python
def eka_sana(mjono: str):
    osat = mjono.split(" ")
    return osat[0]

def vika_sana(mjono: str):
    osat = mjono.split(" ")
    return osat[-1]

def sanojen_maara(mjono: str):
    osat = mjono.split(" ")
    return len(osat)
```

Funktionerna som definierats i filen kan kommas åt genom att importera filen:

```python
import sanat

mjono = "Vesihiisi sihisi hississä"

print(sanat.eka_sana(mjono))
print(sanat.vika_sana(mjono))
print(sanat.sanojen_maara(mjono))
```

<sample-output>

Vesihiisi
hississä
3

</sample-output>

Obs! Filen som innehåller Python-modulen måste befinna sig i samma mapp där programmet som importerar modulen finns i. Alternativt kan filen med modulen vara i någon av de andra mappar där Python söker moduler ifrån. I övriga fall kommer Pythontolken inte att hitta modulen när `import`-satsen körs.

Vi kan använda våra moduler exakt på samma sätt som moduler i Pythons standardbibliotek:

```python
from sanat import eka_sana, vika_sana

lause = input("Anna lause: ")

print("Eka sana oli: " + eka_sana(lause))
print("Viimeinen sana oli: " + vika_sana(lause))
```

<sample-output>

Anna lause: **Python on metka ohjelmointikieli**
Eka sana oli: Python
Viimeinen sana oli: ohjelmointikieli

</sample-output>

## Använda typledtrådar

När vi använder moduler är typledtrådar speciellt till nytta. Om du använder en kodeditor som stödjer typledtrådar, kommer användandet av moduler att bli mycket enklare.

Till exempel Visual Studio Code visar typledtrådar medan du skriver kod:

<img src="7_vihje.png">

## Kod i modulens huvudfunktion

Om en modul innehåller kod som inte finns inom en funktionsdefinition (dvs. kod i huvudfunktionen), kommer den här koden att köras automatiskt då modulen importeras.

Låt oss se på en situation där `ord.py` innehåller några testutskrifter:

```python
def eka_sana(mjono: str):
    osat = mjono.split(" ")
    return osat[0]

def vika_sana(mjono: str):
    osat = mjono.split(" ")
    return osat[-1]

def sanojen_maara(mjono: str):
    osat = mjono.split(" ")
    return len(osat)

print(eka_sana("Tämä on testi"))
print(vika_sana("Tämä on testeistä toinen"))
print(sanojen_maara("Yks kaks kolme neljä viisi"))
```

Om vi nu importerar modulen med en `import`-sats, kommer all kod utanför de definierade funktionerna att köras:

```python
import sanat

mjono = "Vesihiisi sihisi hississä"

print(sanat.eka_sana(mjono))
print(sanat.vika_sana(mjono))
print(sanat.sanojen_maara(mjono))
```

<sample-output>

Tämä
toinen
5
Vesihiisi
hississä
3

</sample-output>

Som du ser, är det här inte en riktigt bra sak i vår situation, eftersom vår utskrift nu blandas med testutskrifter från modulen.

Till all lycka finns en lösning, och den är bekant sedan tidigare. Vi måste helt enkelt testa om programmet körs självständigt eller om koden har importerats med en `import`-sats. Python har en inbyggd variabel `__name__` som innehåller namnet på programmet som körs. Om programmet körs självständigt är värdet på den nyss nämnda variabeln `__main__`. Om programmet däremot har importerats är värdet på variabeln namnet på modulen som importerats (i vårt fall `ord`).

Nu när vi vet det här kan vi lägga till en if-sats som låter oss köra våra test endast då programmet körs självständigt. Som du ser nedan, är strukturen bekant:

```python
def eka_sana(mjono: str) -> str:
    osat = mjono.split(" ")
    return osat[0]

def vika_sana(mjono: str) -> str:
    osat = mjono.split(" ")
    return osat[-1]

def sanojen_maara(mjono: str) -> int:
    osat = mjono.split(" ")
    return len(osat)

if __name__ == "__main__":
    # Testataan funktioiden toimintaa
    print(eka_sana("Tämä on testi"))
    print(vika_sana("Tämä on testeistä toinen"))
    print(sanojen_lkm("Yks kaks kolme neljä viisi"))
```

Om du kör modulen självständigt, skrivs testutskrifterna ut:

<sample-output>

Tämä
toinen
5

</sample-output>

När modulen importeras i ett program, kommer testutskrifterna inte att göras:

```python
import sanat

mjono = "Vesihiisi sihisi hississä"

print(sanat.eka_sana(mjono))
print(sanat.vika_sana(mjono))
print(sanat.sanojen_maara(mjono))
```

<sample-output>

Vesihiisi
hississä
3

</sample-output>

I uppgifterna under den här kursen har du flera gånger ombetts att ha dina test under ett `if __name__ == "__main__"` -block. Nu vet du varför.

<programming-exercise name='Merkkiapuri' tmcname='osa07-17_merkkiapuri'>

Tee moduuli `merkkiapuri`, joka sisältää seuraavat funktiot:

Funktio `vaihda_koko(merkkijono: str)` saa parametrikseen merkkijonon. Funktio luo ja palauttaa uuden merkkijonon, jossa alkuperäisen merkkijonon pienet kirjaimet on muutettu isoiksi kirjaimiksi ja päinvastoin.

Funktio `puolita(merkkijono: str)` palauttaa tuplessa parametrinaan saamansa merkkijonon ensimmäisen ja toisen puolikkaan. Jos merkkijonossa on pariton määrä kirjaimia, ensimmäinen puolikas on lyhyempi.

Funktio `poista_erikoismerkit(merkkijono: str)` palauttaa merkkijonon, josta on poistettu kaikki muut merkit paitsi aakkoset [a...ö, A...Ö], numerot ja välilyönnit.

Esimerkkejä moduulin toiminnasta:

```python
import merkkiapuri

mjono = "Moi kaikki!"

print(merkkiapuri.vaihda_koko(mjono))

p1, p2 = merkkiapuri.puolita(mjono)

print(p1)
print(p2)

m2 = merkkiapuri.poista_erikoismerkit("Tämä on testi, katsotaan miten käy!!!11!")
print(m2)
```

<sample-output>

mOI KAIKKI!
Moi k
aikki!
Tämä on testi katsotaan miten käy11

</sample-output>

</programming-exercise>

<quiz id="caf731dc-cf22-5dfc-ad4d-a3224b2df020"></quiz>

Vänligen svara på en kort enkät om materialet för den här veckan.

<quiz id="7794fe8b-1641-5a54-94d5-16d900a14d13"></quiz>
