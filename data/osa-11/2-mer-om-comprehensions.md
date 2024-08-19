---
path: '/osa-11/2-mer-om-comprehensions'
title: 'Mer om comprehensions'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Kommer du att kunna använda comprehensions med strängar
- Vet du hur du använder comprehensions med dina egna klasser
- Kommer du att kunna skapa ordlistscomprehensions

</text-box>


Listor är kanske det vanligaste målet för comprehensions, men comprehensions fungerar på alla serier av föremål, inklusive strängar. Liksom listexemplen i föregående avsnitt, ifall en list comprehension utförs på en sträng, plockas föremålen (dvs. tecknen) i strängen en efter en, bearbetas enligt det givna uttrycket och lagras i en lista.

```python

namn = "Peter Python"

stora_bokstaver = [tecken.upper() for tecken in namn]
print(stora_bokstaver)

```

<sample-output>

['P', 'E', 'T', 'E', 'R', ' ', 'P', 'Y', 'T', 'H', 'O', 'N']

</sample-output>

Resultatet är en lista, vilket dikteras av parentesnotationen runt comprehension-satsen. Om vi ville ha en sträng istället skulle vi kunna använda strängmetoden `join`  för att tolka listan till en sträng. Kom ihåg att metoden anropas på den sträng som vi vill använda som "lim" mellan tecknen. Låt oss ta en titt på några exempel:

```python

namn = "Peter"
lista = list(namn)
print(lista)

print("".join(lista))
print(" ".join(lista))
print(",".join(lista))
print(" och ".join(lista))

```

<sample-output>

['P', 'e', 't', 'e', 'r']
Peter
P e t e r
P,e,t,e,r
P och e och t och e och r

</sample-output>

List comprehensions och `join`-metoden gör det enkelt att skapa nya strängar baserade på andra strängar. Vi kan t.ex. skapa en sträng som bara innehåller vokalerna från en annan sträng:

```python

teststrang = "Halloj allihopa, det här är ett test"

vokaler = [tecken for tecken in teststrang if tecken in "aeiouyåäö"]
nystrang = "".join(vokaler)

print(nystrang)

```

<sample-output>

aoaioaeääee

</sample-output>

I exemplet ovan står list comprehension och `join`-metoden på separata rader, men de kan kombineras till ett enda uttryck:

```python

teststrang = "Halloj allihopa, det här är ett test"

vokalstrang = "".join([tecken for tecken in teststrang if tecken in "aeiouyåäö"])

print(vokalstrang)

```

Många Python-programmerare står trogna vid dessa oneliners, så det är väl värt besväret att lära sig läsa dem. Vi kan till och med lägga till `split`-metoden i mixen, så att vi kan bearbeta hela meningar effektivt med ett enda uttalande. I exemplet nedan tas det första tecknet från varje ord i en mening bort:

```python

mening = "Sju sjösjuka sjömän på skeppet Shang Hai."

mening_utan_initialer = " ".join([ord[1:] for ord in mening.split()])
print(mening_utan_initialer)

```

<sample-output>

ju jösjuka jömän å keppet hang ai

</sample-output>

Låt oss gå igenom detta steg för steg:

- `ord[1:]` extraherar en delsträng från det andra tecknet (vid index 1) och framåt
- `mening.split()` delar upp meningen i avsnitt vid det angivna tecknet. I det här fallet ges inget argument till metoden, så meningen delas upp vid mellanslagstecken som standard
- `" ".join()` kombinerar föremålen i listan till en ny sträng med ett mellanslag mellan föremålen

En mer traditionell iterativ metod skulle kunna se ut så här:

```python

mening = "Sju sjösjuka sjömän på skeppet Shang Hai."

ordlista = []
orden = mening.split()
for ord in orden:
    ord_utan_initialer = ord[1:]
    ordlista.append(ord_utan_initialer)

mening_utan_initialer = " ".join(ordlista)


print(mening_utan_initialer)

```

<programming-exercise name='Filtrera förbjudna' tmcname='osa11-08_filtrera_forbjudna'>

Skapa funktionen `filtrera_forbjudna(strang: str, forbjuden: str)` som tar två strängar som argument. Funktionen ska returnera en ny version av den första strängen. Den ska inte innehålla tecken från den andra strängen.

Funktionen bör implementeras med hjälp av list comprehension. Funktionen får vara högst tre rader lång, inklusive rubrikraden som börjar med nyckelordet `def`.

Funktionen ska fungera på följande sätt:

```python
mening = "Det! var, en gång: en python!??!?!"
filtrerad = filtrera_forbjudna(mening, "!?:,.")
print(filtrerad)
```

<sample-output>

Det var en gång en python

</sample-output>

</programming-exercise>

## Egna klasser och comprehensions

Comprehensions kan vara ett användbart verktyg för att bearbeta eller formulera instanser av dina egna klasser, vilket vi kommer att se i följande exempel.

Låt oss först ta en titt på klassen `Land` som är en enkel modell för ett enda land, med attribut för namn och befolkning. I huvudfunktionen nedan skapar vi först några Land-objekt och använder sedan en list comprehension för att bara välja dem vars befolkning är större än fem miljoner.

```python

class Land:
    """ Denna klass modellerar ett enkelt land med befolkning """
    def __init__(self, namn: str, befolkningsmangd: int):
        self.namn = namn
        self.befolkningsmangd = befolkningsmangd

if __name__ == "__main__":
    finland = Land("Finland", 6000000)
    malta = Land("Malta", 500000)
    sverige = Land("Sverige", 10000000)
    island = Land("Island", 350000)

    lander = [finland, malta, sverige, island]

    storre_land = [land.namn for land in lander if land.befolkningsmangd > 5000000]
    for land in storre_land:
        print(land)


```

<sample-output>

Finland
Sverige

</sample-output>

I list comprehension ovan valde vi bara namnattributet från Land-objekten, så innehållet i listan kunde skrivas ut direkt. Vi skulle också kunna skapa en ny lista med länderna och komma åt namnattributet i `for`-loopen. Detta skulle vara användbart om samma lista med länder skulle användas senare i programmet, eller om vi behövde befolkningsattributet i `for`-loopen också:

```python

if __name__ == "__main__":
    finland = Land("Finland", 6000000)
    malta = Land("Malta", 500000)
    sverige = Land("Sverige", 10000000)
    island = Land("Island", 350000)

    lander = [finland, malta, sverige, island]

    storre_land = [land for land in lander if land.befolkningsmangd > 5000000]
    for land in storre_land:
        print(land.namn)
```

I nästa exempel har vi en klass som heter `Fotlopp` som modellerar ett enskilt lopp med attribut för loppets längd och namn. Vi kommer att använda list comprehension för att skapa `Fotlopp`-objekt baserat på en lista med tävlingslängder.

Parametern `namn` har ett standardvärde i konstruktorn för `Fotlopp`-klassen, vilket är varför vi inte behöver skicka namnet som ett argument.

```python

class Fotlopp:
    """ Klassen modellerar ett fotloppsevenemang med längden n meter """
    def __init__(self, stracka:int, namn:str = "inget namn"):
        self.stracka = stracka
        self.namn = namn

    def __repr__(self):
        return f"{self.stracka} m. ({self.namn})"

if __name__ == "__main__":
    langder = [100, 200, 1500, 3000, 42195]
    strackor = [Fotlopp(langd) for langd in langder]

    # Skriv ut alla
    print(strackor)

    # Ta en från listan och ge den ett namn
    maraton = strackor[-1] # sista föremålet i listan
    maraton.namn = "Maraton"

    # Skriv ut alla igen, inkluderandes det nya namnet
    print(strackor)

```

<sample-output>

[100 m. (inget namn), 200 m. (inget namn), 1500 m. (inget namn), 3000 m. (inget namn), 42195 m. (inget namn)]
[100 m. (inget namn), 200 m. (inget namn), 1500 m. (inget namn), 3000 m. (inget namn), 42195 m. (Maraton)]

</sample-output>

Låt oss nu ta reda på vad som gör en serie objekt "begripliga" (“comprehendible”). I föregående del lärde vi oss hur vi kan göra våra egna klasser itererbara. Det är exakt samma funktion som också möjliggör list comprehension. Om din egen klass är itererbar kan den användas som grund för en list comprehension. Följande klassdefinitioner är kopierade direkt från [modul 10](https://rage.github.io/ohjelmointi-24-sv/osa-10/3-objektorienterade-programmeringstekniker):

```python

class Bok:
    def __init__(self, namn: str, forfattare: str, sidor: int):
        self.namn = namn
        self.forfattare = forfattare
        self.sidor = sidor

class Bokhylla:
    def __init__(self):
        self._bocker = []

    def tillsatt_bok(self, bok: Bok):
        self._bocker.append(bok)

    # Iteratorns initialiseringsmetod
    # Här bör iterationsvariabeln(variablerna) initialiseras
    def __iter__(self):
        self.n = 0
        # Metoden returnerar en referens till själva objektet
        # eftersom iteratorn är implementerad inom samma klassdefinition
        return self

    # Denna metod returnerar nästa föremål inom objektet
    # Om alla föremål har genomgåtts åstadkomms StopIteration
    def __next__(self):
        if self.n < len(self._bocker):
            # Ta det aktuella föremålet från listan i objektet
            bok = self._bocker[self.n]
            # Öka räknaren med ett
            self.n += 1
            # ...och returnera föremålet
            return bok
        else:
            # Inga fler böcker
            raise StopIteration

# Testar
if __name__ == "__main__":
    b1 = Bok("Livet av en Python", "Peter Python", 123)
    b2 = Bok("Den gamle och Java", "Ernest Hemingjava", 204)
    b3 = Bok("C-värdheter på nätet", "Karl Kodare", 997)

    hylla = Bokhylla()
    hylla.tillsatt_bok(b1)
    hylla.tillsatt_bok(b2)
    hylla.tillsatt_bok(b3)

    # Skapa en lista innehållandes namnet på alla böcker
    bockernas_namn = [bok.namn for bok in hylla]
    print(bockernas_namn)

```

<programming-exercise name='Affärslistans produkter' tmcname='osa11-09_affarslistans_produkter'>

I modul 10 skapade du en [itererbar affärslista](https://rage.github.io/ohjelmointi-24-sv/osa-10/3-objektorienterade-programmeringstekniker). Objekt av en itererbar klass kan användas med list comprehensions. Uppgiftsmallen innehåller en avskalad version av `Affarslista` med knappt tillräckligt funktion för denna övning.

Skapa en funktion med namnet `affarslistans_produkter(affarslista, antal: int)` som tar som argument ett affarslista-objekt och ett heltalsvärde. Funktionen returnerar en lista av produktnamn. Listan borde inkludera endast produkter som har åtminstone ett lika stort antal som parametern `antal`.

Funktionen bör implementeras med hjälp av list comprehension. Funktionen får vara högst två rader lång, inklusive rubrikraden som börjar med nyckelordet `def`. Klassdefinitionen för `Affarslista` bör _inte_ modifieras.


Funktionen ska fungera enligt följande:

```python
lista = Affarslista()
lista.tillsatt("bananer", 10)
lista.tillsatt("äppel", 5)
lista.tillsatt("alkoholfri öl", 24)
lista.tillsatt("ananas", 1)

print("Affärslistan har minst 8 av följande:")
for produkt in affarslistans_produkter(lista, 8):
    print(produkt)
```

<sample-output>

Affärslistan har minst 8 av följande:
bananer
alkoholfri öl

</sample-output>

</programming-exercise>

<programming-exercise name='Billigare prisskillnad' tmcname='osa11-10_billigare_prisskillnad'>

Denna övning innehåller en aning modifierad version av klassen [Bostad](https://rage.github.io/ohjelmointi-24-sv/osa-9/1-objekt-och-referenser) från modul 9.

Skapa en funktion med namnet `billigare(bostader: list, jamforelse: Bostad)` som tar en lista med bostäder och ett enda Bostad-objekt som sina argument. Funktionen ska returnera en lista som endast innehåller de bostäder i den ursprungliga listan som är billigare än jämförelsebostaden, tillsammans med prisskillnaden. Föremålen i den returnerade listan bör vara tupler, där det första föremålet är själva bostaden och den andra är prisskillnaden.

Funktionen bör implementeras med hjälp av list comprehension. Funktionen får vara högst två rader lång, inklusive rubrikraden som börjar med nyckelordet `def`.

Koden för Bostad-klassen ingår i övningsmallen och ska inte ändras.

Ett exempel på funktionen i användning:

```python
a1 = Bostad(1, 16, 5500, "Eira etta")
a2 = Bostad(2, 38, 4200, "Berghäll tvåa")
a3 = Bostad(3, 78, 2500, "Jakobacka trea")
a4 = Bostad(6, 215, 500, "Suomussalmi egnahemshus")
a5 = Bostad(4, 105, 1700, "Kerava 4r och kök")
a6 = Bostad(25, 1200, 2500, "Haikon kartano")

bostader = [a1, a2, a3, a4, a5, a6]

print(f"billigare alternativ än {a3.beskrivning}:")
for foremal in billigare(bostader, a3):
    print(f"{foremal[0].beskrivning:30} prisskillnad {foremal[1]} euro")
```

<sample-output>

billigare alternativ än Jakobacka trea:
Eira etta                     prisskillnad 107000 euro
Berghäll tvåa                  prisskillnad 35400 euro
Suomussalmi egnahemshus        prisskillnad 87500 euro
Kerava 4r och kök           prisskillnad 16500 euro

</sample-output>

</programming-exercise>

## Comprehensions och ordlistor

Det finns inget i sig "list-aktigt" med comprehensions. Resultatet är en lista eftersom comprehension-satsen är inkapslad i hakparenteser, som indikerar en Python-lista. Förståelser fungerar lika bra med Python-ordlistor om du använder rundparenteser istället. Kom dock ihåg att ordlistor kräver nyckel-värde-par. Båda måste anges när en ordlista skapas, även när det gäller comprehensions.

Grunden för en comprehension kan vara vilken itererbar serie som helst, vare sig det är en lista, en sträng, en tupel, en ordlista, någon av dina egna itererbara klasser och så vidare.

I följande exempel använder vi en sträng som bas för en ordlista. Ordlistan innehåller alla unika tecken i strängen, tillsammans med antalet gånger de förekommer:

```python

mening = "Hej alla"

tecken_antal = {bokstav : mening.count(bokstav) for bokstav in mening}
print(tecken_antal)

```

<sample-output>

{'H': 1, 'e': 1, 'j': 1, ' ': 1, 'a': 2, 'l': 2}

</sample-output>

Principen för comprehension-satsen är exakt densamma som för listor, men i stället för ett enda värde består uttrycket nu av en nyckel och ett värde. Den allmänna syntaxen ser ut så här:

`{<nyckeluttryck> : <värdeuttryck> för <föremål> i <serie>}`

Som avslutning på det här avsnittet tittar vi på faktorialtal igen. Den här gången lagrar vi resultaten i en ordlista. Själva talet är nyckeln, medan värdet är resultatet av faktorn från vår funktion:

```python

def fakultet(n: int):
    """ Funktionen beräknar fakulteten n! för positiva heltal """
    k = 1
    while n >= 2:
        k *= n
        n -= 1
    return k

if __name__ == "__main__":
    lista = [-2, 3, 2, 1, 4, -10, 5, 1, 6]
    fakultett = {tal : fakultet(tal) for tal in lista if tal > 0}
    print(fakulteter)

```

<sample-output>

{3: 6, 2: 2, 1: 1, 4: 24, 5: 120, 6: 720}

</sample-output>

<programming-exercise name='Strängarnas längder' tmcname='osa11-11_strangarnas_langder'>

Skapa en funktion med namnet `langder(strangar: list)` som tar en lista med strängar som sitt argument. Funktionen ska returnera en ordlista med strängarna i listan som nycklar och deras längder som värden.

Funktionen bör implementeras med en ordlistscomprehension. Funktionen får vara högst två rader lång, inklusive rubrikraden som inleds med nyckelordet `def`.

Funktionen ska fungera på följande sätt:

```python
ordlista = ["det", "var" , "en", "gång", "python"]

sanojen_langder = langder(ordlista)
print(sanojen_langder)
```

<sample-output>

{'det': 3, 'var': 3, 'en': 2, 'gång': 4, 'python': 6}

</sample-output>


</programming-exercise>

<programming-exercise name='Vanligaste orden' tmcname='osa11-12_vanligaste_orden'>

Skapa en funktion med namnet `vanligaste_orden(filnamn: str, nedre_grans: int)` som tar ett filnamn och ett heltalsvärde som en nedre gräns som sina argument. Funktionen ska returnera en ordlista som innehåller antalet förekomster av de ord som förekommer minst det antal gånger som anges i parametern `nedre_grans`.

Anta t.ex. att funktionen används för att bearbeta en fil med namnet comprehensions.txt med följande innehåll:

```txt
List comprehension is an elegant way to define and create lists based on existing lists.
List comprehension is generally more compact and faster than normal functions and loops for creating list.
However, we should avoid writing very long list comprehensions in one line to ensure that code is user-friendly.
Remember, every list comprehension can be rewritten in for loop, but every for loop can’t be rewritten in the form of list comprehension.
```

När funktionen anropas med argumenten `vanligaste_orden("comprehensions.txt", 3)` ska den returnera

<sample-output>

{'comprehension': 4, 'is': 3, 'and': 3, 'for': 3, 'list': 4, 'in': 3}

</sample-output>

Observera att bokstävernas versaler påverkar resultatet och att alla böjda former är unika ord i den här övningen. Det vill säga att orden `List`, `lists` och `list` är separata ord här, och endast `list` har tillräckligt många förekomster för att komma med i den returnerade listan. Alla skiljetecken ska tas bort innan du räknar upp förekomsterna.

Det är upp till dig att bestämma hur detta ska implementeras. Det enklaste sättet skulle troligen vara att använda list- och ordlistsscomprehension.

</programming-exercise>
