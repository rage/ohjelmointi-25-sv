---
path: '/osa-4/3-listat'
title: 'Listor'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* vet du vad listor är i Python
* vet du hur du kommer åt ett visst element i en lista
* kan du lägga till och avlägsna ett element från en lista
* känner du till inbyggda funktioner och metoder för listor.

</text-box>

Tills nu har vi lagrat data med variabler i våra program, så att varje sak har lagrats i sin egen variabel. Det här har sina begränsningar – det kan bli arbetsdrygt att tilldela variabler för allt då det finns mycket data att behandla.

I Python är en lista en samling av värden som finns lagrade under samma variabelnamn. Listans element skrivs mellan hakparenteser. Listans värden kallas element.

Följande kommando skapar en ny tom lista…

```python
lista = []
```

…medan det här kommandot skapar en lista med fem element:

```python
lista = [7, 2, 2, 5, 2]
```

## Komma åt element i en lista

Elementen i en lista är indexerade på samma sätt som tecken i en sträng. Indexeringen börjar från noll och det sista indexet är listans längd minus ett:

<img src="4_2_1.png" alt="Lista indeksoidaan nollasta alkaen">

Ett specifikt element kan kommas åt på samma sätt som ett specifikt tecken i en sträng, med hakparenteser:

```python
lista = [7, 2, 2, 5, 2]

print(lista[0])
print(lista[1])
print(lista[3])

print("Kahden ekan summa:", lista[0] + lista[1])
```

<sample-output>

7
2
5
Kahden ekan summa: 9

</sample-output>

Hela listans innehåll kan också skrivas ut:

```python
lista = [7, 2, 2, 5, 2]
print(lista)
```

<sample-output>

[7, 2, 2, 5, 2]

</sample-output>

Till skillnad från strängar är listor föränderliga, vilket betyder att deras innehåll kan ändra. Du kan tilldela ett nytt värde till ett element i en lista på samma sätt som du kan tilldela ett nytt värde till en variabel:

```python
lista = [7, 2, 2, 5, 2]
print(lista)
lista[1] = 3
print(lista)
```

<sample-output>

[7, 2, 2, 5, 2]
[7, 3, 2, 5, 2]

</sample-output>

Funktionen `len` berättar antalet element i en lista:

```python
lista = [7, 2, 2, 5, 2]
print(len(lista))
```

<sample-output>

5

</sample-output>


<programming-exercise name='Alkioiden arvojen muutokset' tmcname='osa04-07a_alkioiden_arvojen_muutokset'>

Tee ohjelma, joka alustaa listan jossa on arvot `[1, 2, 3, 4, 5]`. Tämän jälkeen ohjelma kysyy käyttäjältä alkion indeksin ja uuden arvon, vaihtaa kyseisen alkion arvon ja tulostaa listan uudelleen. Ohjelman suoritus päättyy, jos käyttäjä antaa alkion indeksiksi -1.

Esimerkkisuoritus:

<sample-output>

Anna indeksi: **0**
Anna arvo: **10**
[10, 2, 3, 4, 5]
Anna indeksi: **2**
Anna arvo: **250**
[10, 2, 250, 4, 5]
Anna indeksi: **4**
Anna arvo: **-45**
[10, 2, 250, 4, -45]
Anna indeksi: **-1**

</sample-output>

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!

</programming-exercise>

## Lägga till element i en lista

Metoden `append` lägger till element i slutet av en lista. Metoden fungerar så här:

```python
luvut = []
luvut.append(5)
luvut.append(10)
luvut.append(3)
print(luvut)
```

<sample-output>

[5, 10, 3]

</sample-output>

Följande exempel använder sig av två listor:

```python
luvut = []
kengannumerot = []

luvut.append(5)
luvut.append(10)
luvut.append(3)

kengannumerot.append(37)
kengannumerot.append(44)
kengannumerot.append(40)
kengannumerot.append(28)

print("Luvut:")
print(luvut)

print("Kengännumerot:")
print(kengannumerot)
```

Elementet läggs till i slutet av den lista som metoden anropas på:

<sample-output>

Luvut:
[5, 10, 3]
Kengännumerot:
[37, 44, 40, 28]

</sample-output>

<programming-exercise name='Alkioiden lisäys listaan' tmcname='osa04-07b_alkoiden_lisays_listaan'>

Tee ohjelma, joka kysyy käyttäjältä ensin lukujen määrän. Sen jälkeen ohjelma pyytää käyttäjää syöttämään annetun määrän lukuja yksitellen ja lisää ne listaan samassa järjestyksessä.

Lopuksi lista tulostetaan.

Esimerkkisuoritus:

<sample-output>

Kuinka monta lukua: **3**
Anna luku 1: **10**
Anna luku 2: **250**
Anna luku 3: **34**
[10, 250, 34]

</sample-output>

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!

</programming-exercise>

## Lägga till ett element på ett specifikt ställe

Om du vill specificera på vilket ställe i en lista ett värde ska läggas till, kan du använda `insert`-metoden. Metoden lägger till ett element vid ett specifikt index. Alla element vid det här eller senare index flyttar ett index framåt, "mot höger":

<img src="4_2_2.png" alt = "Alkion lisäys listaan">

Till exempel det här programmet…

```python
luvut = [1, 2, 3, 4, 5, 6]
luvut.insert(0, 10)
print(luvut)
luvut.insert(2, 20)
print(luvut)
```

…skriver ut följande:

<sample-output>

[10, 1, 2, 3, 4, 5, 6]
[10, 1, 20, 2, 3, 4, 5, 6]

</sample-output>

## Ta bort element från en lista

Det finns två sätt för att ta bort ett element från en lista:

* om man vet indexet för elementet kan man använda `pop`-metoden
* om man vet innehållet i elementet kan man använda `remove`-metoden.

`pop`-metoden tar indexet för elementet som ska avlägsnas som argument. Följande program tar bort elementen vid indexen 2 och 3 i listan. Märk hur indexen för de resterande elementen ändrar när ett element avlägsnas:

```python
lista = [1, 2, 3, 4, 5, 6]

lista.pop(2)
print(lista)
lista.pop(3)
print(lista)
```

<sample-output>

[1, 2, 4, 5, 6]
[1, 2, 4, 6]

</sample-output>

Det är bra att minnas att `pop`-metoden också returnerar det avlägsnade elementet:

```python
lista = [4, 2, 7, 2, 5]

luku = lista.pop(2)
print(luku)
print(lista)
```

<sample-output>

7
[4, 2, 2, 5]

</sample-output>

`remove`-metoden tar värdet för det element som ska avlägsnas som argument. Till exempel följande program…

```python
lista = [1, 2, 3, 4, 5, 6]

lista.remove(2)
print(lista)
lista.remove(5)
print(lista)
```

…skriver ut detta:

<sample-output>

[1, 3, 4, 5, 6]
[1, 3, 4, 6]

</sample-output>

Metoden tar bort det första värdet som motsvarar det givna argumentet från listan – på samma sätt som funktionen find hos strängar returnerar den första delsträngen:

```python
lista = [1, 2, 1, 2]

lista.remove(1)
print(lista)
lista.remove(1)
print(lista)
```

<sample-output>

[2, 1, 2]
[2, 2]

</sample-output>

<programming-exercise name='Lisäys ja poisto' tmcname='osa04-07c_lisays_ja_poisto'>

Tee ohjelma, joka pyytää käyttäjää valitsemaan alkion lisäyksen tai poiston. Sekä lisäys että poisto tehdään listan loppuun. Lisättävän alkion arvo on aina yhtä suurempi kuin listan viimeinen alkio (tai 1, jos listassa ei ole alkioita).

Joka operaation välissä lista tulostetaan. Katso esimerkkiä seuraavasta tulosteesta:

<sample-output>

Lista on nyt []
(l)isää, (p)oista vai e(x)it: **l**
Lista on nyt [1]
(l)isää, (p)oista vai e(x)it: **l**
Lista on nyt [1, 2]
(l)isää, (p)oista vai e(x)it: **l**
Lista on nyt [1, 2, 3]
(l)isää, (p)oista vai e(x)it: **p**
Lista on nyt [1, 2]
(l)isää, (p)oista vai e(x)it: **l**
Lista on nyt [1, 2, 3]
(l)isää, (p)oista vai e(x)it: **x**
Moi!

</sample-output>

Voit olettaa, että listalta ei yritetä poistaa alkioita, jos lista on tyhjä.

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!

</programming-exercise>

Om det givna elementet inte hittas i listan, kommer remove-funktionen att ge ett fel. På samma sätt som med strängar kan vi kolla om ett element finns i en lista med hjälp av `in`-operatorn:

```python
lista = [1, 3, 4]

if 1 in lista:
    print("Listalla on alkio 1")

if 2 in lista:
    print("listalla on alkio 2")
```

<sample-output>

Listalla on alkio 1

</sample-output>

<programming-exercise name='Sama sana kahdesti' tmcname='osa04-08_sama_sana_kahdesti'>

Tee ohjelma, joka kyselee käyttäjältä sanoja. Kun käyttäjä syöttää jonkin sanan kahdesti, ohjelma tulostaa eri sanojen määrän ja lopettaa toimintansa.

<sample-output>

sana: **olipa**
sana: **kerran**
sana: **kauan**
sana: **sitten**
sana: **kerran**
Annoit 4 eri sanaa

</sample-output>

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!

</programming-exercise>

## Ordna listor

Elementen i en lista kan ordnas från minsta till största med metoden `sort`.

```python
lista = [2,5,1,2,4]
lista.sort()
print(lista)
```

<sample-output>

[1, 2, 2, 4, 5]

</sample-output>

Notera att den här metoden modifierar själva listan. Alltid vill vi inte ändra på den ursprungliga listan, och då kan vi istället använda funktionen `sorted`. Den returnerar en ordnad lista:

```python
lista = [2,5,1,2,4]
print(sorted(lista))
```

<sample-output>

[1, 2, 2, 4, 5]

</sample-output>

Kom ihåg skillnaden mellan dessa: `sort` ändrar på ordningen i den ursprungliga listan medan `sorted` skapar en ny, ordnad kopia av listan. Med `sorted` kan vi behålla den ursprungliga ordningen hos listan:

```python
alkuperainen = [2, 5, 1, 2, 4]
jarjestetty = sorted(alkuperainen)
print(alkuperainen)
print(jarjestetty)
```

<sample-output>

[2, 5, 1, 2, 4]
[1, 2, 2, 4, 5]

</sample-output>

<programming-exercise name='Lista kahdesti' tmcname='osa04-08b_lista_kahdesti'>

Tee ohjelma, joka kysyy käyttäjältä lukuja ja lisää niitä listaan. Lista tulostetaan jokaisen luvun lisäyksen jälkeen kahdella eri tavalla:
- alkiot lisäysjärjestyksessä ja
- järjestettynä pienimmästä suurimpaan alkioon

Ohjelman suoritus päättyy, kun käyttäjä syöttää luvun 0.

Esimerkkisuoritus:

<sample-output>

Anna luku: **3**
Lista: [3]
Järjestettynä: [3]
Anna luku: **1**
Lista: [3, 1]
Järjestettynä: [1, 3]
Anna luku: **9**
Lista: [3, 1, 9]
Järjestettynä: [1, 3, 9]
Anna luku: **5**
Lista: [3, 1, 9, 5]
Järjestettynä: [1, 3, 5, 9]
Anna luku: **0**
Moi!

</sample-output>

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!

</programming-exercise>

## Maximi- och minimivärde samt summa

Funktionerna `max` och `min` returnerar det största respektive minsta värdet i en lista. Funktionen `sum` returnerar summan av listans värden.

```python
lista = [5, 2, 3, 1, 4]

suurin = max(lista)
pienin = min(lista)
summa = sum(lista)

print("Pienin:", pienin)
print("Suurin:", suurin)
print("Summa:", summa)
```

<sample-output>

Pienin: 1
Suurin: 5
Summa: 15

</sample-output>

## Metoder och funktioner

Det finns två sätt att behandla listor i Python, och det här kan ibland orsaka huvudbry. För det mesta kommer du att använda metoder hos listor – till exempel `append` och `sort`. De används med punktoperatorn hos listvariabeln:

```python
lista = []

# metodikutsuja
lista.append(3)
lista.append(1)
lista.append(7)
lista.append(2)

# metodikutsu
lista.sort()
```

En del funktioner kan ta emot listor som argument. De nyss presenterade funktionerna `max`, `min`, `len` och `sorted` är goda exempel:

```python
lista = [3, 2, 7, 1]

# funktiokutsuissa lista on parametrina
suurin = max(lista)
pienin = min(lista)
pituus = len(lista)

print("Pienin:", pienin)
print("Suurin:", suurin)
print("Listan pituus:", pituus)

# funktiokutsu: lista on parametrina, järjestetty lista paluuarvona
jarjestyksessa = sorted(lista)
print(jarjestyksessa)
```

<sample-output>

Pienin: 1
Suurin: 7
Listan pituus: 4
[1, 2, 3, 7]

</sample-output>

## Lista som argument eller return-värde

Som de inbyggda funktionerna ovan kan också våra egna funktioner ta listor som argument och returnera listor. Den följande funktionen tar reda på det mellersta – median – värdet i en ordnad lista:

```python
def mediaani(lista: list):
    jarjestetty = sorted(lista)
    keskikohta = len(jarjestetty) // 2
    return jarjestetty[keskikohta]
```

Funktionen skapar en ordnad version av listan som gavs som argument och returnerar elementet i mitten. Märk heltalsdivisionsoperatorn `//` som används. Indexet i en lista måste vara ett heltal.

Funktionen fungerar på följande sätt:

```python
kengannumerot = [45, 44, 36, 39, 40]
print("Kengännumeroiden mediaani on", mediaani(kengannumerot))

iat = [1, 56, 34, 22, 5, 77, 5]
print("Ikien mediaani on", mediaani(iat))
```

<sample-output>

Kengännumeroiden mediaani on 40
Ikien mediaani on 22

</sample-output>

En funktion kan också returnera en lista. Den följande funktionen ber användaren ge heltal, som sedan returneras som en lista:

```python
def lue_luvut():
    luvut = []
    while True:
        syote = input("Anna luku (tyhjä lopettaa): ")
        if len(syote) == 0:
            break
        luvut.append(int(syote))
    return luvut
```

Funktionen använder sig av hjälpvariabeln `siffror`, som är en lista. Alla siffror som användaren skriver läggs till i listan. När loopen avslutas returnerar funktionen listan med satsen `return siffror`.

När funktionen anropas så här…

```python
luvut = lue_luvut()

print("Suurin luku on", max(luvut))
print("Lukujen mediaani on", mediaani(luvut))
```

…kan utskriften se ut på följande sätt:

<sample-output>

Anna luku (tyhjä lopettaa): **5**
Anna luku (tyhjä lopettaa): **-22**
Anna luku (tyhjä lopettaa): **4**
Anna luku (tyhjä lopettaa): **35**
Anna luku (tyhjä lopettaa): **1**
Anna luku (tyhjä lopettaa):
Suurin luku on 35
Lukujen mediaani on 4

</sample-output>

Det här lilla exemplet demonstrerar ett av de viktigaste användningsområdena för funktioner: de hjälper dig att dela din kod i mindre helheter som enkelt kan förstås.

Samma funktionalitet kan förstås fås till stånd utan några som helst egna funktioner:

```python
luvut = []
while True:
    syote = input("Anna luku (tyhjä lopettaa): ")
    if len(syote) == 0:
        break
    luvut.append(int(syote))

jarjestetty = sorted(luvut)
keskikohta = len(jarjestetty) // 2
mediaani = jarjestetty[keskikohta]

print("Suurin luku on", max(luvut))
print("Lukujen mediaani on", mediaani)
```

I den här versionen är det svårare att uppfatta logiken bakom programmet, eftersom det inte mera är enkelt att se vilka kommandon som hör till vilken funktionalitet. Koden uppnår samma mål – ta emot data, räkna medianvärde o.s.v. – men strukturen är mycket mindre tydlig.

Att dela din kod i flera funktioner kommer att förbättra läsbarheten av koden och hjälper att uppfatta logiska helheter. Det här är till nytta när du ska verifiera att programmet fungerar som det ska, eftersom varje funktion kan testas separat.

En annan viktig orsak till att använda funktioner är återanvändbarhet av koden. Om du behöver samma funktionalitet på flera ställen i ditt program är det en bra idé att skapa en funktion och namnge den väl:

```python
print("Kengännumerot:")
kengat = lue_luvut()

print("Painot:")
painot = lue_luvut()

print("Pituudet:")
pituudet = lue_luvut()
```

<programming-exercise name='Listan pituus' tmcname='osa04-09_listan_pituus'>

Tee funktio `pituus`, joka palauttaa parametrinaan saamansa listan pituuden.

```python
lista = [1, 2, 3, 4, 5]
vastaus = pituus(lista)
print("vastaus", vastaus)

# huomaa, että voit kutsua funktiota myös antamalla listan suoraan funktion parametriksi
vastaus = pituus([1, 1, 1, 1])
print("vastaus", vastaus)
```

<sample-output>

vastaus 5
vastaus 4

</sample-output>

</programming-exercise>

<programming-exercise name='Keskiarvo' tmcname='osa04-10_keskiarvo'>

Tee funktio `keskiarvo`, joka palauttaa parametrinaan saamansa kokonaislukuja sisältävän listan alkioiden keskiarvon.

```python
lista = [1, 2, 3, 4, 5]
vastaus = keskiarvo(lista)
print("vastaus", vastaus)
```

<sample-output>

vastaus 3.0

</sample-output>

</programming-exercise>

<programming-exercise name='Vaihteluväli' tmcname='osa04-11_vaihteluvali'>

Tee funktio `vaihteluvali`, joka palauttaa parametrinaan saamansa kokonaislukuja sisältävän listan vaihteluvälin (eli suurimman ja pienimmän alkion erotuksen).

```python
lista = [1, 2, 3, 4, 5]
vastaus = vaihteluvali(lista)
print("vastaus", vastaus)
```

<sample-output>

vastaus 4

</sample-output>


</programming-exercise>

## Lisää listan käsittelystä

Det finns flera sätt till att använda listor i Python. Om du vill läsa mera är Pythons dokumentation ett bra ställe att börja med.

<quiz id="3974e1bb-cd83-52b3-85d2-a16223773ce7"></quiz>
