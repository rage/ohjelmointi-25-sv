---
path: '/osa-5/2-referenser'
title: 'Referenser'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* vet du vad som menas med en referens till en variabel
* vet du att det kan finnas flera referenser till ett och samma objekt
* kan du använda listor som parameter i funktioner
* förstår du vad som menas med en funktions sidoeffekter.

</text-box>

Hittills har vi tänkt att en variabel är en slags "låda" som innehåller variabelns värde. Från teknisk synvinkel stämmer detta inte i Python – variabler innehåller inte ett värde, utan en referens till ett objekt, såsom en siffra, sträng eller en lista.

I praktiken innebär det att man inte lagrar ett värde i en variabel, utan däremot en minnesposition där man kan hitta variabelns värde.

En referens kan beskrivas som en pil från variabeln till dess riktiga värde:

<img src="5_2_1.png">

Referensen berättar alltså var det riktiga värdet finns. Funktionen `id` berättar vad en variabel refererar till:

```python
a = [1, 2, 3]
print(id(a))
b = "Det här är också en referens"
print(id(b))
```

<sample-output>

4538357072
4537788912

</sample-output>

Referensen, alltså variabelns id är ett heltal. Man kan tänka att talet är adressen för variabelns värde i datorns minne. Observera att om du kör koden ovan på din dator, kommer resultatet sannolikt vara ett annat eftersom variablerna knappast har lagrats på exakt samma adress i din dators minne. 

Som vi redan såg i förra delens exempel, visar Python Tutors visualiseringsverktyg referenser som "pilar" till det egentliga innehållet. Verktyget "lurar" ändå när det kommer till strängar, och visar dem som att strängens innehåll skulle vara lagrat i själva variabeln:

<img src="5_2_1a.png">

Så är det inte i verkligheten – strängar behandlas också internt av Python på samma sätt som listor.

Flera av Pythons inbyggda datatyper – som `str` – är oföränderliga. Det betyder att värdet på objektet aldrig kan ändras. Däremot kan ett värde ersättas med ett nytt värde.

<img src="5_2_2.png">

I Python finns också datatyper som är föränderliga. Till exempel kan innehållet i en lista förändras utan att man behöver skapa en ny lista:

<img src="5_2_3.png">

Något förvånande är att också grundläggande datatyper för lagring av tal och sanningsvärden, `int`, `float` och `bool`, är oföränderliga. Låt oss använda följande kod som exempel:

```python
tal = 1
tal = 2
tal += 10
```

Det verkar som att koden ändrar på talet, men från teknisk synvinkel är det inte så. Istället skapar varje instruktion ett nytt tal.

Utskriften från det här programmet är intressant:

```python
tal = 1
print(id(tal))
tal += 10
print(id(tal))
a = 1
print(id(a))
```

<sample-output>

4535856912
4535856944
4535856912

</sample-output>

I början refererar variabeln `tal` till adressen `4535856912` och när variabelns värde förändras refererar variabeln till adressen `4535856944`. När variabeln `a` definieras och får värdet `1`, kommer variabeln att referera till samma ställe som variabeln `tal` när dess värde var `1`.

Det verkar som att Python har lagrat siffran 1 i adressen `4535856912` och alltid då en variabels värde är `1`, refererar variabeln till det här specifika stället i "datorns minne".

Även om de grundläggande datatyperna `int`, `float` och `bool` är referenser behöver man som programmerare egentligen inte fundera på det.

## Flera referenser till en och samma lista

Vi undersöker vad som händer om vi försöker kopiera en lista:

```python
a = [1, 2, 3]
b = a
b[0] = 10
```

Deklarationen `b = a` kopierar variabeln `a`:s värde till variabeln `b`. Det är ändå viktigt att observera att variabelns värde inte är en lista utan en referens till listan.

Deklarationen `b = a` kopierar alltså referensen, varpå det efter kopieringen finns två referenser till samma lista.

<img src="5_2_4.png">

Listan kan behandlas med båda referenserna:

```python
lista = [1, 2, 3, 4]
lista2 = lista

lista[0] = 10
lista2[1] = 20

print(lista)
print(lista2)
```

<sample-output>

[10, 20, 3, 4]
[10, 20, 3, 4]

</sample-output>

Om flera variabler refererar till samma lista, kan vi använda vilken som helst av variablerna för att komma åt listan. Det innebär dock också att ändringar som görs via en referens också kommer att påverka alla andra referenser. 

Visualiseringsverktyget klargör igen vad som sker i programmet:

<img src="5_2_4a.png">

## Att kopiera en lista

Om du vill skapa en verklig kopia av en lista kan du skapa en ny lista och lägga till alla element från den ursprungliga listan i den nya listan:

```python
lista = [1, 2, 3, 3, 5]

kopia = []
for element in lista:
    kopia.append(element)

kopia[0] = 10
kopia.append(6)
print("lista", lista)
print("kopia", kopia)
```

<sample-output>

lista [1, 2, 3, 3, 5]
kopia [10, 2, 3, 3, 5, 6]

</sample-output>

Så här ser det ut i visualiseringsverktyget:

<img src="5_2_4b.png">

Variabeln `ny_lista` refererar till en annan lista än `min_lista`.

Ett enklare sätt att kopiera en lista är att använda hakparenteser `[]`, som vi använt tidigare för att extrahera innehåll från strängar och listor. Notationen `[:]` väljer alla element i en samling. Därmed skapar det en kopia av en lista:

```python
lista = [1,2,3,4]
kopia = lista[:]

lista[0] = 10
kopia[1] = 20

print(lista)
print(kopia)
```

<sample-output>

[10, 2, 3, 4]
[1, 20, 3, 4]

</sample-output>

## En lista som parameter i en funktion

När vi ger en lista som argument till en funktion, får funktionen tillgång till referensen till listan. Det här innebär att funktionen kan ändra på listan. 

Till exempel lägger följande funktion till ett nytt element i den lista som getts som argument:

```python
def lagg_till_element(lista: list):
    nytt_element = 10
    lista.append(nytt_element)

lista = [1,2,3]
print(lista)
lagg_till_element(lista)
print(lista)
```

<sample-output>
[1, 2, 3]
[1, 2, 3, 10]
</sample-output>

Märk att funktionen `lagg_till_element` inte returnerar något, utan ändringen sker direkt i den lista som getts som argument. Visualiseringsverktyget presenterar situationen så här:

<img src="5_2_4c.png">

Global frame syftar till huvudprogrammets variabler, och den blå lådan `lagg_till_element` på funktionens parametrar och variabler. Som visualiseringen visar, refererar funktionen till samma lista som huvudprogrammet, vilket betyder att ändringar som görs i listan inom funktionen också syns i huvudprogrammet.

Om man vill undvika detta kan man inne i funktionen först skapa en ny kopia av argumentlistan, göra ändringar i den och slutligen returnera den:

```python
def lagg_till_element(lista: list) -> list:
    nytt_element = 10
    kopia = lista[:]
    kopia.append(nytt_element)
    return kopia

siffror = [1, 2, 3]
siffror2 = lagg_till_element(siffror)

print("Ursprunglig lista:", siffror)
print("Ny lista:", siffror2)
```

<sample-output>

Ursprunglig lista: [1, 2, 3]
Ny lista: [1, 2, 3, 10]

</sample-output>

Om du inte är helt säker på vad som händer i en kodsnutt, kan det löna sig att utnyttja visualiseringsverktyget.

## Ändra på en lista som getts som argument

Vi försöker skapa en funktion som ökar på varje element i en lista med tio:

```python
def oka_pa_alla(lista: list):
    ny_lista = []
    for element in lista:
        ny_lista.append(element + 10)
    lista = ny_lista

tal = [1, 2, 3]
print("start:",tal)
oka_pa_alla(tal)
print("efter funktionen:", tal)
```

<sample-output>

start: [1, 2, 3]
efter funktionen: [1, 2, 3]

</sample-output>


Av någon orsak fungerar funktionen inte. Varför det?

Funktionen tar en referens till en lista som argument. Det här är lagrat i variabeln `min_lista`. Tilldelningen `min_lista = ny_lista` tilldelar ett nytt värde till den samma variabeln. Variabeln `min_lista` hänvisar nu till den nya listan som skapades i funktionen, vilket betyder att referensen till den ursprungliga listan inte längre är tillgänglig inom funktionen. Tilldelningen har dock inte någon påverkan utanför funktionen.

<img src="5_2_6.png" width="400">

Dessutom innehåller variabeln `ny_lista` nu de nya värdena, men de är inte tillgängliga utanför funktionen. Variabeln försvinner alltså när funktionen körts och programmet fortsätter tillbaka till huvudfunktionen. Variabeln `tal` i huvudfunktionen hänvisar alltid till den ursprungliga listan.

Visualiseringsverktyget hjälper igen. När du går igenom stegen utförligt märker du att den ursprungliga listan inte påverkas av funktionen på något sätt alls:

<img src="5_2_4d.png">

Ett enkelt sätt att korrigera problemet är att kopiera över alla element från den nya listan till den gamla:

```python
def oka_pa_alla(lista: list):
    ny_lista = []
    for element in lista:
        ny_lista.append(element + 10)

    # vi kopierar de nya värdena till den gamla listan
    for i in range(len(lista)):
        lista[i] = ny_lista[i]
```

Eller lite enklare tack vare Python:

```python
>>> lista = [1, 2, 3, 4]
>>> lista[1:3] = [10, 20]
>>> lista
[1, 10, 20, 4]
```

I exemplet ovan ersätts en del av listan med värden från en annan lista.

Vi kan naturligtvis också göra detta för en hel lista:

```python
>>> lista = [1, 2, 3, 4]
>>> lista[:] = [100, 99, 98, 97]
>>> lista
[100, 99, 98, 97]
```

Allt innehåll i den gamla listan ersätts. Inspirerat av det här har vi nu skapat en fungerande version av funktionen som ökar på elementens värden:

```python
def oka_pa_alla(lista: list):
    ny_lista = []
    for element in lista:
        ny_lista.append(element + 10)

    lista[:] = ny_lista
```

Egentligen finns det ingen orsak till att skapa en ny lista inom funktionen. Vi kan helt enkelt tilldela värdena direkt till den ursprungliga listan:

```python
def oka_pa_alla(lista: list):
    for i in range(len(lista)):
        lista[i] += 10
```


<programming-exercise name='Elementen fördubblade' tmcname='osa05-06a_elementen_x2'>

Skapa funktionen `elementen_fordubblade(tal: list)` som får som argument en lista med tal.

Funktionen ska returnera en ny lista där alla tal är multiplicerade med två. Funktionen får inte ändra på den ursprungliga listan.

Exempel:

```python
if __name__ == "__main__":
    tal = [2, 4, 5, 3, 11, -4]
    fordubblade = elementen_fordubblade(tal)
    print("ursprunglig:", tal)
    print("fördubblade:", fordubblade)
```

<sample-output>

ursprunglig: [2, 4, 5, 3, 11, -4]
fördubblade: [4, 8, 10, 6, 22, -8]

</sample-output>

</programming-exercise>


<programming-exercise name='Bort med minsta' tmcname='osa05-06b_minsta_bort'>

Skapa funktionen `avlagsna_minsta(tal: list)` som tar en lista med tal som argument.

Funktionen ska ta bort det minsta talet ur listan. Du kan anta att det minsta talet endast förekommer en gång.

Funktionen ska inte returnera något, den ska endast ändra på listan som getts som argument!

Exempel:

```python
if __name__ == "__main__":
    tal = [2, 4, 6, 1, 3, 5]
    avlagsna_minsta(tal)
    print(tal)
```

<sample-output>

[2, 4, 6, 3, 5]

</sample-output>

</programming-exercise>


<programming-exercise name='Sudoku: Utskrift och att lägga till ett tal' tmcname='osa05-07_sudoku_utskrift_ny_siffra'>

I den här uppgiften skapar vi ännu två funktioner för ett sudoku: `skriv_ut` och `lagg_till`.

Funktionen `skriv_ut` får som argument en matris och skriver den ut enligt exemplet nedan.

Funktionen `lagg_till(sudoku: list, radnummer: int, kolumnnummer: int, siffra: int)` tar emot som argument en matris, två siffror som indikerar positionen och ett tal (1-9) som ska lagras.

```python
sudoku  = [
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0]
]

skriv_ut(sudoku)
lagg_till(sudoku, 0, 0, 2)
lagg_till(sudoku, 1, 2, 7)
lagg_till(sudoku, 5, 7, 3)
print()
print("Tre siffror tillagda:")
print()
skriv_ut(sudoku)
```

<sample-output>

<pre>
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

Tre siffror tillagda:

2 _ _  _ _ _  _ _ _
_ _ 7  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ 3 _

_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

</pre>

</sample-output>

Tips: Du kan dra nytta av att `print`-funktionen kan användas så att radbyten inte görs:

```python
print("tecken ", end="")
print("utan mellanrum", end="")
```

<sample-output>

tecken utan mellanrum

</sample-output>

En radbrytning kan åstadkommas så här:

```python
print()
```

</programming-exercise>

<programming-exercise name='Sudoku: Lägga till en siffra i en kopia av sudokut' tmcname='osa05-08_sudoku_ny_siffra_kopia'>

I den här uppgiften skapar vi en lite annorlunda version av funktionen som lägger till nya tal i ett sudoku.

Funktionen `kopiera_och_lagg_till(sudoku: list, radnummer: int, kolumnnummer: int, siffra: int)` får som argument 

* en matris,
* två siffror som anger en position i sodukot, samt
* en siffra (1-9) som ska lagras.

Funktionen ska returnera en kopia av matrisen som gavs som argument, med den angivna siffran lagrad på korrekt ställe. Funktionen får inte ändra på matrisen som getts som argument.

Här utnyttjar vi funktionen `skriv_ut` från den föregående uppgiften:

```python
sudoku  = [
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0]
]

kopia = kopiera_och_lagg_till(sudoku, 0, 0, 2)
print("Ursprunglig:")
skriv_ut(sudoku)
print()
print("Kopia:")
skriv_ut(kopia)
```

<sample-output>

<pre>
Ursprunglig:
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

Kopia:
2 _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

</pre>

</sample-output>

Tips: I den här uppgiften måste man vara noga med vad allt som behöver kopieras och vart man slutligen lagrar värdet som getts till funktionen. [Visualiseringsverktyget](https://pythontutor.com/visualize.html) kan hjälpa. På grund av sudokuts storlek kan vyn dock vara aningen otydlig. 

</programming-exercise>

<programming-exercise name='Tre i rad' tmcname='osa05-09_tre_i_rad'>

Tre i rad spelas med ett 3 x 3 -rutnät, där spelarna turvis markerar ett kryss eller en ring. Den spelare som först får tre markeringar i rad, vågrätt, lodrätt eller diagonalt, vinner. Om ingendera av spelarna får det, är spelet oavgjort.

Skapa funktionen `tur(brade: list, x: int, y: int, markering: str)` där den givna markeringen görs på stället som indikeras av koordinaterna (0-2).

Observera att `x` indikerar kolumn och `y` rad.

Spelbrädan består av följande strängar:

* `""`: tom ruta
* `"X"`: markering, spelare 1
* `"O"`: markering, spelare 2

Funktionen returnerar `True` om markeringen lyckades (stället var tomt på brädan), och `False` om stället var reserverat eller koordinaterna inte låg i intervallet 0-2.

Exempel:

```python
brade = [["", "", ""], ["", "", ""], ["", "", ""]]
print(tur(brade, 2, 0, "X"))
print(brade)
```

<sample-output>

True
[['', '', 'X'], ['', '', ''], ['', '', '']]

</sample-output>

</programming-exercise>

<programming-exercise name='Transponera' tmcname='osa05-10_transponera'>

Skapa funktionen `transponera(matris: lista)` som får som argument en matris. Funktionen ska transponera matrisen, alltså byta plats på rader och kolumner.

Du kan anta att matrisen har lika många rader och kolumner.

Den här matrisen...

```python
1 2 3
4 5 6
7 8 9
```

...skulle se ut så här efter transponeringen:

```python
1 4 7
2 5 8
3 6 9
```

Funktionen ska inte returnera något. Den ska ändra på matrisen som den fått som argument.

</programming-exercise>

## Funktioners sidoeffekter 

Som vi sett ovan, kan en funktion som tar emot en referens till en lista som argument ändra på listan. Om programmeraren inte har tagit i beaktande att listan kan komma att ändras inne i funktionen, kan detta förorsaka problem på andra håll i programmet.

Låt oss ta en titt på en funktion som borde hitta det nästminsta värdet i en lista:

```python
def nast_minst(lista: list) -> int:
    # i en sorterad lista finns det nästminsta elementet på index 1
    lista.sort()
    return lista[1]

tal = [1, 4, 2, 5, 3, 6, 4, 7]
print(nast_minst(tal))
print(tal)
```

<sample-output>
2
[1, 2, 3, 4, 4, 5, 6, 7]
</sample-output>

Funktionen hittar det nästminsta värdet, men sorterar dessutom listan. Om elementens ordning har betydelse på andra håll i programmet kommer det här funktionsanropet eventuellt att orsaka fel. Oplanerade modifikationer som görs hos objekt som ges som referens till en funktion kallas sidoeffekter.

Vi kan förhindra den här sidoeffekten genom att göra en liten ändring i funktionen:

```python
def nast_minst(lista: list) -> int:
    kopia = sorted(lista)
    return kopia[1]

tal = [1, 4, 2, 5, 3, 6, 4, 7]
print(nast_minst(tal))
print(tal)
```

<sample-output>

2
[1, 4, 2, 5, 3, 6, 4, 7]

</sample-output>

Funktionen `sorted` returnerar en ny sorterad kopia av listan, så vi behöver inte mera "sabotera" den ursprungliga listan när vi söker efter det näst minsta värdet.

Det är en god vana att försöka undvika sidoeffekter i funktioner. Sidoeffekter kan göra det svårare att säkerställa att programmet fungerar som det ska i alla situationer.

Funktioner som saknar sidoeffekter kallas rena funktioner. Då man arbetar med funktionell programmering är rena funktioner speciellt viktiga. Vi kommer se närmare på det under fortsättningskursen i programmering.

<quiz id="63f11402-1cff-570f-b6cb-4db6eaa766fc"></quiz>
