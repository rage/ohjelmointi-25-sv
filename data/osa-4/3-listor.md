---
path: '/osa-4/3-listor'
title: 'Listor'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

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

print("Summan av de två första:", lista[0] + lista[1])
```

<sample-output>

7
2
5
Summan av de två första: 9

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


<programming-exercise name='Ändra på elementens värden' tmcname='osa04-07a_alkioiden_arvojen_muutokset'>

Skapa ett program som initierar en lista med värdena `[1, 2, 3, 4, 5]`. Programmet ber därefter användaren ange ett index och ett nytt värde som programmet lagrar, och listan skrivs ut på nytt. Programmet avslutas då använder anger -1 som index.

Exempel:

<sample-output>

Ange index: **0**
Ange värde: **10**
[10, 2, 3, 4, 5]
Ange index: **2**
Ange värde: **250**
[10, 2, 250, 4, 5]
Ange index: **4**
Ange värde: **-45**
[10, 2, 250, 4, -45]
Ange index: **-1**

</sample-output>

Obs! Placera inte kod i `if __name__ == "__main__"` -blocket i någon av dessa uppgifter, om du inte ombeds göra det.

</programming-exercise>

## Lägga till element i en lista

Metoden `append` lägger till element i slutet av en lista. Metoden fungerar så här:

```python
siffror = []
siffror.append(5)
siffror.append(10)
siffror.append(3)
print(siffror)
```

<sample-output>

[5, 10, 3]

</sample-output>

Följande exempel använder sig av två listor:

```python
siffror = []
skonummer = []

siffror.append(5)
siffror.append(10)
siffror.append(3)

skonummer.append(37)
skonummer.append(44)
skonummer.append(40)
skonummer.append(28)

print("Siffror:")
print(siffror)

print("Skonummer:")
print(skonummer)
```

Elementet läggs till i slutet av den lista som metoden anropas på:

<sample-output>

Siffror:
[5, 10, 3]
Skonummer:
[37, 44, 40, 28]

</sample-output>

<programming-exercise name='Lägg till element i en lista' tmcname='osa04-07b_alkoiden_lisays_listaan'>

Skapa ett program som ber användaren ge antalet siffror. Därefter ber programmet användaren ange det här antalet siffror, som läggs till i en lista i den givna ordningen.

Listan ska till slut skrivas ut:

<sample-output>

Hur många siffror: **3**
Ge siffra 1: **10**
Ge siffra 2: **250**
Ge siffra 3: **34**
[10, 250, 34]

</sample-output>

Obs! Placera inte kod i `if __name__ == "__main__"` -blocket i någon av dessa uppgifter, om du inte ombeds göra det.

</programming-exercise>

## Lägga till ett element på ett specifikt ställe

Om du vill specificera på vilket ställe i en lista ett värde ska läggas till, kan du använda `insert`-metoden. Metoden lägger till ett element vid ett specifikt index. Alla element vid det här eller senare index flyttar ett index framåt, "mot höger":

<img src="4_2_2.png" alt = "Alkion lisäys listaan">

Till exempel det här programmet…

```python
siffror = [1, 2, 3, 4, 5, 6]
siffror.insert(0, 10)
print(siffror)
siffror.insert(2, 20)
print(siffror)
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

siffra = lista.pop(2)
print(siffra)
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

<programming-exercise name='Lägg till, ta bort' tmcname='osa04-07c_lisays_ja_poisto'>

Skapa ett program som låter användaren lägga till eller avlägsna ett värde. Varje operation görs i slutet av listan. När ett element läggs till är dess värde alltid ett större än det föregående värdet (1 om inga element finns i listan).

Mellan varje operation skrivs listan ut. Här följer ett exempel:

<sample-output>

Listan är nu []
(l)ägg till, (a)vlägsna eller a(v)sluta: **l**
Listan är nu [1]
(l)ägg till, (a)vlägsna eller a(v)sluta: **l**
Listan är nu [1, 2]
(l)ägg till, (a)vlägsna eller a(v)sluta: **l**
Listan är nu [1, 2, 3]
(l)ägg till, (a)vlägsna eller a(v)sluta: **a**
Listan är nu [1, 2]
(l)ägg till, (a)vlägsna eller a(v)sluta: **l**
Listan är nu [1, 2, 3]
(l)ägg till, (a)vlägsna eller a(v)sluta: **v**
Hejdå!

</sample-output>

Du kan anta att man inte försöker avlägsna element då listan är tom.

Obs! Placera inte kod i `if __name__ == "__main__"` -blocket i någon av dessa uppgifter, om du inte ombeds göra det.

</programming-exercise>

Om det givna elementet inte hittas i listan, kommer remove-funktionen att ge ett fel. På samma sätt som med strängar kan vi kolla om ett element finns i en lista med hjälp av `in`-operatorn:

```python
lista = [1, 3, 4]

if 1 in lista:
    print("Listan innehåller värdet 1")

if 2 in lista:
    print("Listan innehåller värdet 2")
```

<sample-output>

Listan innehåller värdet 1

</sample-output>

<programming-exercise name='Samma ord två gånger' tmcname='osa04-08_sama_sana_kahdesti'>

Skapa ett program som ber användaren mata in ord. När användaren anger ett ord som hon gett tidigare, avslutas programmet och antalet ord skrivs ut.

<sample-output>

ord: **det**
ord: **var**
ord: **en**
ord: **gång**
ord: **en**
Du gav 4 olika ord

</sample-output>

Obs! Placera inte kod i `if __name__ == "__main__"` -blocket i någon av dessa uppgifter, om du inte ombeds göra det.

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
ursprunglig = [2, 5, 1, 2, 4]
ordnad = sorted(ursprunglig)
print(ursprunglig)
print(ordnad)
```

<sample-output>

[2, 5, 1, 2, 4]
[1, 2, 2, 4, 5]

</sample-output>

<programming-exercise name='En lista, två varianter' tmcname='osa04-08b_lista_kahdesti'>

Skapa ett program som ber användaren ange siffror, som läggs till i en lista. Efter varje tillägg skrivs listan ut på två sätt:

* elementen i den ordning de lagts till
* elementen i storleksordning från det minsta till det största

Programmet avslutas då användaren anger siffran 0.

Exempel:

<sample-output>

Ange siffra: **3**
Lista: [3]
Ordnat: [3]
Ange siffra: **1**
Lista: [3, 1]
Ordnat: [1, 3]
Ange siffra: **9**
Lista: [3, 1, 9]
Ordnat: [1, 3, 9]
Ange siffra: **5**
Lista: [3, 1, 9, 5]
Ordnat: [1, 3, 5, 9]
Ange siffra: **0**
Hejdå!

</sample-output>

Obs! Placera inte kod i `if __name__ == "__main__"` -blocket i någon av dessa uppgifter, om du inte ombeds göra det.

</programming-exercise>

## Maximi- och minimivärde samt summa

Funktionerna `max` och `min` returnerar det största respektive minsta värdet i en lista. Funktionen `sum` returnerar summan av listans värden.

```python
lista = [5, 2, 3, 1, 4]

storst = max(lista)
minst = min(lista)
summa = sum(lista)

print("Minst:", minst)
print("Störst:", storst)
print("Summa:", summa)
```

<sample-output>

Minst: 1
Störst: 5
Summa: 15

</sample-output>

## Metoder och funktioner

Det finns två sätt att behandla listor i Python, och det här kan ibland orsaka huvudbry. För det mesta kommer du att använda metoder hos listor – till exempel `append` och `sort`. De används med punktoperatorn hos listvariabeln:

```python
lista = []

# metodanrop
lista.append(3)
lista.append(1)
lista.append(7)
lista.append(2)

# metodanrop
lista.sort()
```

En del funktioner kan ta emot listor som argument. De nyss presenterade funktionerna `max`, `min`, `len` och `sorted` är goda exempel:

```python
lista = [3, 2, 7, 1]

# funktionsanrop, lista som argument
storst = max(lista)
minst = min(lista)
pituus = len(lista)

print("Minst:", minst)
print("Störst:", storst)
print("Listan pituus:", pituus)

# funktionsanrop, lista som argument, ordnad lista returneras
jarjestyksessa = sorted(lista)
print(jarjestyksessa)
```

<sample-output>

Minst: 1
Störst: 7
Listan pituus: 4
[1, 2, 3, 7]

</sample-output>

## Lista som argument eller return-värde

Som de inbyggda funktionerna ovan kan också våra egna funktioner ta listor som argument och returnera listor. Den följande funktionen tar reda på det mellersta – median – värdet i en ordnad lista:

```python
def median(lista: list):
    ordnad = sorted(lista)
    mellersta = len(ordnad) // 2
    return ordnad[mellersta]
```

Funktionen skapar en ordnad version av listan som gavs som argument och returnerar elementet i mitten. Märk heltalsdivisionsoperatorn `//` som används. Indexet i en lista måste vara ett heltal.

Funktionen fungerar på följande sätt:

```python
skonummer = [45, 44, 36, 39, 40]
print("Skonumrens median är", median(skonummer))

iat = [1, 56, 34, 22, 5, 77, 5]
print("Medianåldern är", median(iat))
```

<sample-output>

Skonumrens median är 40
Medianåldern är 22

</sample-output>

En funktion kan också returnera en lista. Den följande funktionen ber användaren ge heltal, som sedan returneras som en lista:

```python
def las_in_siffror():
    siffror = []
    while True:
        indata = input("Ge siffra (tomt avslutar programmet): ")
        if len(indata) == 0:
            break
        siffror.append(int(indata))
    return siffror
```

Funktionen använder sig av hjälpvariabeln `siffror`, som är en lista. Alla siffror som användaren skriver läggs till i listan. När loopen avslutas returnerar funktionen listan med satsen `return siffror`.

När funktionen anropas så här…

```python
siffror = las_in_siffror()

print("Största siffran är", max(siffror))
print("Medianvärdet är", median(siffror))
```

…kan utskriften se ut på följande sätt:

<sample-output>

Ge siffra (tomt avslutar programmet): **5**
Ge siffra (tomt avslutar programmet): **-22**
Ge siffra (tomt avslutar programmet): **4**
Ge siffra (tomt avslutar programmet): **35**
Ge siffra (tomt avslutar programmet): **1**
Ge siffra (tomt avslutar programmet):
Största siffran är 35
Medianvärdet är 4

</sample-output>

Det här lilla exemplet demonstrerar ett av de viktigaste användningsområdena för funktioner: de hjälper dig att dela din kod i mindre helheter som enkelt kan förstås.

Samma funktionalitet kan förstås fås till stånd utan några som helst egna funktioner:

```python
siffror = []
while True:
    indata = input("Ge siffra (tomt avslutar programmet): ")
    if len(indata) == 0:
        break
    siffror.append(int(indata))

ordnad = sorted(siffror)
mellersta = len(ordnad) // 2
median = ordnad[mellersta]

print("Största siffran är", max(siffror))
print("Medianvärdet är", median)
```

I den här versionen är det svårare att uppfatta logiken bakom programmet, eftersom det inte mera är enkelt att se vilka kommandon som hör till vilken funktionalitet. Koden uppnår samma mål – ta emot data, räkna medianvärde o.s.v. – men strukturen är mycket mindre tydlig.

Att dela din kod i flera funktioner kommer att förbättra läsbarheten av koden och hjälper att uppfatta logiska helheter. Det här är till nytta när du ska verifiera att programmet fungerar som det ska, eftersom varje funktion kan testas separat.

En annan viktig orsak till att använda funktioner är återanvändbarhet av koden. Om du behöver samma funktionalitet på flera ställen i ditt program är det en bra idé att skapa en funktion och namnge den väl:

```python
print("Skonummer:")
skor = las_in_siffror()

print("Painot:")
vikter = las_in_siffror()

print("Pituudet:")
langder = las_in_siffror()
```

<programming-exercise name='Listans längd' tmcname='osa04-09_listan_pituus'>

Skapa funktionen `langd` som returnerar längden på den lista som getts som argument.

```python
lista = [1, 2, 3, 4, 5]
svar = langd(lista)
print("svar", svar)

# observera att du också kan anropa funktionen genom att direkt ge en lista som argument till funktionen
svar = langd([1, 1, 1, 1])
print("svar", svar)
```

<sample-output>

svar 5
svar 4

</sample-output>

</programming-exercise>

<programming-exercise name='Medeltal' tmcname='osa04-10_keskiarvo'>

Skapa funktionen `medeltal` som returnerar medelvärdet av värdena i en lista bestående av heltal som getts som argument till funktionen.

```python
lista = [1, 2, 3, 4, 5]
svar = medeltal(lista)
print("svar", svar)
```

<sample-output>

svar 3.0

</sample-output>

</programming-exercise>

<programming-exercise name='Variationsbredd' tmcname='osa04-11_vaihteluvali'>

Skapa funktionen `variationsbredd` som returnerar diffrensen av det största och minsta värdet i en lista med heltal som getts som argument till funktionen.

```python
lista = [1, 2, 3, 4, 5]
svar = variationsbredd(lista)
print("svar", svar)
```

<sample-output>

svar 4

</sample-output>


</programming-exercise>

## Mer om att behandla listor

Det finns flera sätt till att använda listor i Python. Om du vill läsa mera är [Pythons dokumentation](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists) ett bra ställe att börja med.

<quiz id="3974e1bb-cd83-52b3-85d2-a16223773ce7"></quiz>
