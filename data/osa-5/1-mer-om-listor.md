---
path: '/osa-5/1-mer-om-listor'
title: 'Mer om listor'
hidden: false
---


<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* kan du skapa listor med element av olika typer
* vet du hur man kan använda listor för att organisera data
* kan du skapa en matris som en tvådimensionell lista.

</text-box>

<!--vastaava teksti löytyy osioista 3-1, 5-1 ja 6-1, tsekkaa kaikki jos muokkaat tätä-->
<text-box variant='hint' name='Om uppgifterna i den här kursen'>

Att bli en skicklig programmerare kräver mycket övning. Man måste utveckla en problemlösningsförmåga och ha en förmåga att intuition komma fram till korrekta lösningar. Därför finns det massor av övningar av olika typer i den här kursen. Vissa övningar är enklare och baserar sig mera eller mindre direkt på materialet medan andra uppgifter är svårare och kräver tillämpande av kunskaper som man lärt sig under kursen.

En del uppgifter kan kännas svåra, men det är inte något att oroa sig över. Ingen av uppgifterna är obligatorisk och du behöver bara 25 % av poängen från varje modul för att klara den här kursen. Du kan läsa mera på kursens bedömningssida.

Uppgifterna är inte i svårighetsordning. Varje del introducerar vanligtvis några nya saker inom programmering och i samband finns relaterade uppgifter – både enklare och svårare. Om du stöter på en uppgift som känns oöverkomlig ska du fortsätta till nästa uppgift. Du kan alltid senare återkomma till tidigare uppgifter.

En uppgift som känns för svår just nu kommer sannolikt att vara ganska enkel om en månad.

</text-box>

## Listor med olika typer av data

I den förra modulen fokuserade vi främst på listor med element av heltalstyp, men listor kan innehålla vilka typer av data som helst. En lista bestående av strängar kunde exempelvis se ut så här:

```python
namn = ["Maja", "Lotta", "Pontus"]
print(namn)
namn.append("Konrad")
print(namn)

print("Antal namn:", len(namn))
print("Namnen i alfabetisk ordning:")
namn.sort()
for person in namn:
  print(person)
```

<sample-output>

['Maja', 'Lotta', 'Pontus']
['Maja', 'Lotta', 'Pontus', 'Konrad']
Antal namn: 4
Namnen i alfabetisk ordning:
Konrad
Lotta
Maja
Pontus

</sample-output>

Flyttal kan också lagras i listor:

```python
matningar = [-2.5, 1.1, 7.5, 14.6, 21.0, 19.2]

for matning in matningar:
    print(matning)

medeltal = sum(matningar) / len(matningar)

print("Medelvärde:", medeltal)
```

<sample-output>

-2.5
1.1
7.5
14.6
21.0
19.2
Medelvärde: 10.15

</sample-output>

<!--vastaava varoitusteksti löytyy osioista 3-4, 4-6 ja 5-1, tsekkaa kaikki jos muokkaat tätä-->
## Varning: globala variabler inom funktioner

Vi har sett att det går att tilldela nya variabler inne i funktionsdefinitioner. Funktionen kan också komma åt variabler som finns utanför funktionen, i huvudfunktionen. Dessa variabler kallas globala variabler.

Att använda globala variabler inifrån funktioner är oftast en dålig idé. Det kan orsaka en hel del problem, till exempel buggar som är svåra att spåra.

Här är ett exempel på en funktion som använder en global variabel "av misstag":

```python
def svangd_utskrift(namn: list):
    # använder av misstag den globala variabeln namnlista
    i = len(namnlista) - 1
    while i >= 0:
        print(namnlista[i])
        i -= 1

# global variabel
namnlista = ["Antti", "Emilia", "Erkki", "Margaret"]
svangd_utskrift(namnlista)
print()
svangd_utskrift(["Louise", "Ophelia", "Lotta"])
```

<sample-output>

Margaret
Erkki
Emilia
Antti

Margaret
Erkki
Emilia
Antti

</sample-output>

Även om funktionen anropas korrekt skrivs alltid namnen i den globala variabeln `namnlista` ut.

All kod som testar funktioner ska skrivas inom ett separat block så att TMC-testen accepterar koden. Föregående exempel ska alltså skrivas så här:

```python
def svangd_utskrift(namn: list):
    # använder av misstag den globala variabeln namnlista
    i = len(namnlista) - 1
    while i >= 0:
        print(namnlista[i])
        i -= 1

# kod som testar funktionen placeras här
if __name__ == "__main__":
    # global variabel
    namnlista = ["Antti", "Emilia", "Erkki", "Margaret"]
    svangd_utskrift(namnlista)
    print()
    svangd_utskrift(["Louise", "Ophelia", "Lotta"])
```

Nu definieras också den globala variabeln i if-blocket.

TMC-testerna körs alltid så att det som finns i detta if-block inte körs. Därför fungerar funktionen inte ens i teorin eftersom variabeln `namnlista` inte finns då testerna körs.

## Varning: att skriva över en parameter och returnera för tidigt

Ju mer vi lär oss, desto fler potentiella orsaker till buggar får vi. Låt oss titta på en funktion som meddelar om ett heltal hittas i en lista. Både listan och talet är definierade som parametrar i funktionen:

```python
def tal_i_listan(tal: list, t: int):
    for t in tal:
        if t == t:
            return True
        else:
            return False
```

Den här funktionen verkar alltid returnera värdet `True`. Orsaken till det är att for-loopen skriver över värdet som är lagrat i parametern `t` (det som gavs in som argument skrivs i for-loopen över av det första värdet i listan tal). Därför är villkoret i if-satsen alltid sant.

Att ändra på parameterns namn löser problemet:

```python
def tal_i_listan(tal: list, tal_som_soks: int):
    for t in tal:
        if t == tal_som_soks:
            return True
        else:
            return False
```

Nu är villkoret i if-satsen i sin ordning. I stället har vi nu ett nytt problem, eftersom funktionen inte ännu heller fungerar som den ska. Om vi testar följande, märker vi en bugg:

```python
resultat = tal_i_listan([1, 2, 3, 4], 3)
print(resultat) # False
```

Problemet här är att funktionen returnerar resultatet för tidigt, utan att gå igenom alla tal i listan. Funktionen kollar faktiskt endast det första värdet i listan och returnerar `True` eller `False` beroende på dess värde. Vi kan inte veta att ett tal inte finns i listan förrän vi har gått igenom hela listan. Instruktionen `return False` måste alltså placeras utanför for-loopen:

```python
def tal_i_listan(tal: list, tal_som_soks: int):
    for t in tal:
        if t == tal_som_soks:
            return True

    return False
```

Låt oss ta en titt på en annan funktion som inte fungerar korrekt:

```python
def tal_olika(tal: list):
    # hjälpvariabel där vi lagrar de värden som kollats
    tal = []
    for t in tal:
        # har talet redan förekommit?
        if t in tal:
            return False
        tal.append(t)

    return True

resultat = tal_olika([1, 2, 2])
print(resultat) # True
```

Funktionen borde kolla om alla tal i en lista är olika, men kommer alltid att returnera `True`. Varför det?

I det här fallet skriver funktionen igen över värdet som är lagrat i dess parameter. Funktionen försöker använda variabeln `tal` för att lagra de siffror som redan har kontrollerats, men det här skriver över det ursprungliga argumentet. Att namnge hjälpvariabeln på nytt löser vårt problem:

```python
def tal_olika(tal: list):
    # hjälpvariabel där de tal som kollats lagras
    sedda_tal = []
    for t in tal:
        # har talet redan förekommit?
        if t in sedda_tal:
            return False
        sedda_tal.append(t)

    return True

resultat = tal_olika([1, 2, 2])
print(resultat) # False
```

Problem som dessa kan hittas och korrigeras med hjälp av debuggaren eller [visualiseringsverktyget](https://pythontutor.com/visualize.html). Det lönar sig verkligen att lära sig använda dessa effektivt.

<programming-exercise name='Längsta strängen' tmcname='osa05-01a_langsta_strangen'>

**OBS:** Denna och följande uppgift kommer i fel ordning i sidobalken i VS Code. 

Skapa funktionen `langst(strangar: list)` som får en lista med strängar som argument. Funktionen ska hitta och returnera den längsta strängen. Du kan anta att det bara finns en längsta sträng.

Exempel:

```python
if __name__ == "__main__":
    lista = ["hej", "hejsan", "morjens", "tjolahoppsan", "tjenare"]
    print(langst(lista))
```

<sample-output>

tjolahoppsan

</sample-output>

</programming-exercise>

## Listor inom listor

Elementen i en lista kan i sin tur vara listor:

```python
lista = [[5, 2, 3], [4, 1], [2, 2, 5, 1]]
print(lista)
print(lista[1])
print(lista[1][0])
```

<sample-output>

[[5, 2, 3], [4, 1], [2, 2, 5, 1]]
[4, 1]
4

</sample-output>

När skulle det här kunna vara nyttigt?

Kom ihåg att listor kan innehålla element av olika typer. Du kan till exempel lagra information om en person i en lista. Det första elementet kan då exempelvis vara personens namn, det andra hens ålder och det tredje hens skostorlek:

```python
["Nelly", 10, 32]
```

Vi kunde då skapa en databas med information om flera personer i form av en lista, vars element i sin tur också vore listor som innehåller information om en enskild person:

```python
personer = [["Nelly", 10, 32], ["PO", 7, 26], ["Emilia", 32, 37], ["August", 39, 44]]

for person in personer:
  namn = person[0]
  alder = person[1]
  sko = person[2]
  print(f"{namn}: {alder} år, skostorlek {sko}")
```

<sample-output>

Nelly: 10 år, skostorlek 32
PO: 7 år, skostorlek 26
Emilia: 32 år, skostorlek 37
August: 39 år, skostorlek 44

</sample-output>

For-loopen går igenom elementen i den yttre listan ett i taget. Variabeln `person` tildelas då ett element ur listan, som i sin tur utgör en lista med information om en person.

Listor är inte alltid det bästa sättet att presentera data som exempelvis information om en person. Vi kommer snart att se på ordlistor/lexikon (dictionary) i Python. Den är bättre anpassad för situationer som den ovannämnda.

## Matriser

En tvådimensionell tabell – matris – är ett annat användningsområde för listor inom listor.

Till exempel kan följande matris…

<img src="5_1_0.png">

… presenteras som en tvådimensionell lista i Python på följande sätt:

```python
matris = [[1, 2, 3], [3, 2, 1], [4, 5, 6]]
```

Eftersom en matris är en lista som innehåller listor kan vi komma åt enskilda element inom matrisen med två index. Det första indexet hänvisar till raden, medan den andra hänvisar till kolumnen. Indexeringen startar från noll så `matris[0][1]` hänvisar till det andra elementet på den första raden.

```python
matris = [[1, 2, 3], [3, 2, 1], [4, 5, 6]]

print(matris[0][1])
matris[1][0] = 10
print(matris)
```

<sample-output>

2
[[1, 2, 3], [10, 2, 1], [4, 5, 6]]

</sample-output>

Som med vilken som helst lista, kan raderna i matrisen gås igenom med en for-loop. Den följande koden skriver ut varje rad i matrisen på en skild rad:

```python
matris = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

for rad in matris:
    print(rad)
```

<sample-output>

[1, 2, 3]
[4, 5, 6]
[7, 8, 9]

</sample-output>

På samma sätt kan vi använda nästlade loopar för att komma åt enskilda element inom matrisen. Följande kod skriver ut varje element i matrisen på en skild rad med hjälp av två for-loopar:

```python
matris = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

for rad in matris:
    print("ny rad")
    for element in rad:
        print(element)
```

<sample-output>

ny rad
1
2
3
ny rad
4
5
6
ny rad
7
8
9

</sample-output>

## Visualisering av kod som innehåller listor inom listor

Program som består av listor inom listor kan till först vara svåra att greppa. [Visualiseringsverktyget](https://pythontutor.com/visualize.html) av Python Tutor är ett bra sätt att bekanta sig med hur de fungerar. Det följande är en visualisering av exemplet ovan:

<img src="5_1_0a.png">

Bilden ovan avslöjar att en 3 x 3 -matris tekniskt sett består av fyra listor. Den första listan representerar hela matrisen. De tre resterande listorna är element i den första listan, och de representerar rader i matrisen.

Eftersom flerdimensionella listor kan gås igenom med nästlade loopar skulle man kunna tänka sig att listorna finns inuti varandra, men som bilden visar är detta inte fallet. Istället hänvisar den "stora listan" som representerar matrisen till skilda listor som alla representerar en rad i matrisen. Det här är en referens – något vi kommer att se mera på i nästa del.

I bilden ovan har programmet hunnit till den andra raden i matrisen och det är den listan som variabeln `rad` hänvisar till för tillfället. Variabeln `element` innehåller det element som programmet hanterar för tillfället, dvs. listans mellersta värde 5.

## Komma åt element i en matris

Att komma åt en viss rad i en matris är enkelt. Det är bara att välja den raden. Följande funktion beräknar summan av elementen på en viss rad:

```python
def summan_av_radens_element(matris, radnummer: int):
    # vi inspekterar bara en rad
    rad = matris[radnummer]
    summa = 0
    for element in rad:
        summa += element

    return summa

m = [[4, 2, 3, 2], [9, 1, 12, 11], [7, 8, 9, 5], [2, 9, 15, 1]]

summa = summan_av_radens_element(m, 1)
print(summa) # 33 (dvs. 9 + 1 + 12 + 11)
```

Att arbeta med kolumner i en matris är aningen mer komplicerat eftersom matrisen är lagrad som rader:

```python
def summan_av_kolumnens_element(matris, kolumnnummer: int):
    # till summan adderas för varje rad elementet på den önskade positionen
    summa = 0
    for rad in matris:
        summa += rad[kolumnnummer]

    return summa

m = [[4, 2, 3, 2], [9, 1, 12, 11], [7, 8, 9, 5], [2, 9, 15, 1]]

summa = summan_av_kolumnens_element(m, 2)
print(summa) # 39 (dvs. 3 + 12 + 9 + 15)
```

Den kolumn som vi vill komma åt består av elementen på index 2 för varje rad.

[Visualiseringsverktyget](https://pythontutor.com/visualize.html) rekommenderas varmt för att bättre förstå hur det här fungerar.

Att ändra på ett värde hos ett specifikt element inom en matris är enkelt – du väljer helt enkelt den rad och kolumn där elementet finns lagrat.

```python
def byt_varde(matris, radnummer: int, kolumnnummer: int, varde: int):
    # välj korrekt rad
    rad = matris[radnummer]
    # och korrekt ställe i raden
    rad[kolumnnummer] = varde

m = [[4, 2, 3, 2], [9, 1, 12, 11], [7, 8, 9, 5], [2, 9, 15, 1]]

print(m)
byt_varde(m, 2, 3, 1000)
print(m)
```

<sample-output>

[[4, 2, 3, 2], [9, 1, 12, 11], [7, 8, 9, 5], [2, 9, 15, 1]]
[[4, 2, 3, 2], [9, 1, 12, 11], [7, 8, 9, 1000], [2, 9, 15, 1]]

</sample-output>

Observera att vi ovan använde indexen för raden och kolumnen för att komma åt det element vi ville ändra på. Om vi vill ändra på innehållet i en matris måste vi komma åt elementen md hjälp av deras index. Vi kan inte bara använda oss av en `for element in lista` -loop för att gå igenom matrisen då vi vill ändra på innehållet.

Istället behöver vi hålla reda på indexen hos elementen: till exempel med en while-loop eller en for-loop och `range`-funktionen. Följande kod ökar värdet på varje element i en matris med ett:


```python
m = [[1,2,3], [4,5,6], [7,8,9]]

for i in range(len(m)):
    for j in range(len(m[i])):
        m[i][j] += 1

print(m)
```

<sample-output>

[[2, 3, 4], [5, 6, 7], [8, 9, 10]]

</sample-output>

Den yttre loopen går igenom indexen från noll till matrisens längd, alltså antalet rader i matrisen. Den inre loopen går igenom indexen från noll till radernas längd.


<programming-exercise name='Antalet element' tmcname='osa05-01_antalet_element'>

**OBS:** Denna och följande uppgift kommer i fel ordning i sidobalken i VS Code. 

Skapa funktionen `rakna_element(matris: list, element: int)` som tar emot en matris samt ett heltal som argument. Funktionen ska returnera antalet gånger det valda elementet hittas i matrisen.

Exempel:

```python
m = [[1, 2, 1], [0, 3, 4], [1, 0, 0]]
print(rakna_element(m, 1))
```

<sample-output>

3

</sample-output>

</programming-exercise>

## En tvådimensionell tabell som datastruktur i ett spel

En matris kan fungera som datastruktur i olika typer av spel. Till exempel kan rutorna i ett sudokuspel…

<img src="5_1_1.png">

… representeras med en matris på följande sätt:

```python
sudoku = [
  [9, 0, 0, 0, 8, 0, 3, 0, 0],
  [0, 0, 0, 2, 5, 0, 7, 0, 0],
  [0, 2, 0, 3, 0, 0, 0, 0, 4],
  [0, 9, 4, 0, 0, 0, 0, 0, 0],
  [0, 0, 0, 7, 3, 0, 5, 6, 0],
  [7, 0, 5, 0, 6, 0, 4, 0, 0],
  [0, 0, 7, 8, 0, 3, 9, 0, 0],
  [0, 0, 1, 0, 0, 0, 0, 0, 3],
  [3, 0, 0, 0, 0, 0, 0, 0, 2]
]
```

Nu representerar noll en tom ruta, eftersom noll inte är ett värde som kan användas i sudoku.

Här är en enkel funktion som skriver ut sudokurutor:

```python
def skriv_ut(sudoku):
    for rad in sudoku:
        for ruta in rad:
            if ruta > 0:
                print(f" {ruta}", end="")
            else:
                print(" _", end="")
        print()

skriv_ut(sudoku)
```

Utskriften borde se ut så här:

```
 9 _ _ _ 8 _ 3 _ _
 _ _ _ 2 5 _ 7 _ _
 _ 2 _ 3 _ _ _ _ 4
 _ 9 4 _ _ _ _ _ _
 _ _ _ 7 3 _ 5 6 _
 7 _ 5 _ 6 _ 4 _ _
 _ _ 7 8 _ 3 9 _ _
 _ _ 1 _ _ _ _ _ 3
 3 _ _ _ _ _ _ _ 2
```

Flera andra spel kan också representeras på liknande sätt: till exempel schack, minröjning, sänka skepp och Mastermind. I sudoku fungerar tal väl för att representera spelets läge, medan för andra spel kan andra metoder vara bättre.

<programming-exercise name='Go' tmcname='osa05-02_go'>

I spelet Go plaerar man turvis svarta och vita stenar på spelbrädan. Den spelare som har flera stenar på brädan vinner spelet.

Skapa funktionen `vem_vann(brade: list)` som tar en matris som representerar spelbrädan som argument. Matrisen består av heltalsvärden:

* 0: tom ruta
* 1: sten, spelare 1
* 2: sten, spelare 2

Spelbrädan kan vara av vilken storlek som helst.

Funktionen ska returnera `1` om spelare ett har vunnit, `2` om spelare två har vunnit och `0` om båda spelarna har lika många stenar på brädan.

</programming-exercise>

<programming-exercise name='Sudoku: Rader korrekt' tmcname='osa05-03_sudoku_rader'>

Skapa funktionen `rad_korrekt(sudoku: list, radnummer: int)` som får som argument en matris samt ett heltal. Radnumreringen börjar med noll. Funktionen ska returnera ett värde som beskriver om raden har fyllts i korrekt, dvs. vart och ett av talen 1-9 förekommer högst en gång.

```python
sudoku = [
  [9, 0, 0, 0, 8, 0, 3, 0, 0],
  [2, 0, 0, 2, 5, 0, 7, 0, 0],
  [0, 2, 0, 3, 0, 0, 0, 0, 4],
  [2, 9, 4, 0, 0, 0, 0, 0, 0],
  [0, 0, 0, 7, 3, 0, 5, 6, 0],
  [7, 0, 5, 0, 6, 0, 4, 0, 0],
  [0, 0, 7, 8, 0, 3, 9, 0, 0],
  [0, 0, 1, 0, 0, 0, 0, 0, 3],
  [3, 0, 0, 0, 0, 0, 0, 0, 2]
]

print(rad_korrekt(sudoku, 0))
print(rad_korrekt(sudoku, 1))
```

<sample-output>

True
False

</sample-output>

</programming-exercise>

<programming-exercise name='Sudoku: Kolumner korrekt' tmcname='osa05-04_sudoku_kolumner'>

Skapa funktionen `kolumn_korrekt(sudoku: list, kolumnnummer: int)` som får en matris och ett heltal som argument. Funktionen ska returnera ett värde som beskriver om kolumnen har fyllts i korrekt, dvs. innehåller vart och ett av talen 1-9 högst en gång.


```python
sudoku = [
  [9, 0, 0, 0, 8, 0, 3, 0, 0],
  [2, 0, 0, 2, 5, 0, 7, 0, 0],
  [0, 2, 0, 3, 0, 0, 0, 0, 4],
  [2, 9, 4, 0, 0, 0, 0, 0, 0],
  [0, 0, 0, 7, 3, 0, 5, 6, 0],
  [7, 0, 5, 0, 6, 0, 4, 0, 0],
  [0, 0, 7, 8, 0, 3, 9, 0, 0],
  [0, 0, 1, 0, 0, 0, 0, 0, 3],
  [3, 0, 0, 0, 0, 0, 0, 0, 2]
]

print(kolumn_korrekt(sudoku, 0))
print(kolumn_korrekt(sudoku, 1))
```

<sample-output>

False
True

</sample-output>

</programming-exercise>

<programming-exercise name='Sudoku: Kvadrater korrekt' tmcname='osa05-05_sudoku_kvadrater'>

Skapa funktionen `kvadrat_korrekt(sudoku: list, radnummer: int, kolumnnummer: int)` som får som argument en matris samt två heltal.

Funktionen ska berätta om 3 x 3 -kvadraten vid positionen (radnummer, kolumnnummer) har fyllts i korrekt, dvs. så att vart och ett av talen 1-9 förekommer högst en gång.

Det är värt att notera att man i sudoku vanligtvis enbart ser på kvadraterna vid positionerna (0, 0), (0, 3), (0, 6), (3, 0), (3, 3), (3, 6), (6, 0), (6, 3) och (6, 6). Din funktion behöver dock inte beakta det.

```python
sudoku = [
  [9, 0, 0, 0, 8, 0, 3, 0, 0],
  [2, 0, 0, 2, 5, 0, 7, 0, 0],
  [0, 2, 0, 3, 0, 0, 0, 0, 4],
  [2, 9, 4, 0, 0, 0, 0, 0, 0],
  [0, 0, 0, 7, 3, 0, 5, 6, 0],
  [7, 0, 5, 0, 6, 0, 4, 0, 0],
  [0, 0, 7, 8, 0, 3, 9, 0, 0],
  [0, 0, 1, 0, 0, 0, 0, 0, 3],
  [3, 0, 0, 0, 0, 0, 0, 0, 2]
]

print(kvadrat_korrekt(sudoku, 0, 0))
print(kvadrat_korrekt(sudoku, 1, 2))
```

<sample-output>

False
True

</sample-output>

Kvadraten vid (0, 0) i det första funktionsanropet:

<pre>
9 0 0
2 0 0
0 2 0
</pre>

Kvadraten vid (1, 2) i det andra funktionsanropet:

<pre>
0 2 5
0 3 0
4 0 0
</pre>

I ett riktigt sudokuspel skulle den här kvadraten alltså inte kollas.

</programming-exercise>

<programming-exercise name='Sudoku: Korrekt?' tmcname='osa05-06_sudoku_korrekt'>

Skapa funktionen `sudoku_korrekt(sudoku: list)` som får en matris som argument. Funktionen ska använda sig av de tre föregående uppgifternas funktioner (kopiera dem) för att säkerställa att varje rad, kolumn och 3 x 3 -kvadrat innehåller högst en av siffrorna 1-9.

De 3 x 3 -kvadrater som ska kontrolleras nämndes ovan. De är alltså vid positionerna (0, 0), (0, 3), (0, 6), (3, 0), (3, 3), (3, 6), (6, 0), (6, 3) och (6, 6).

```python
sudoku1 = [
  [9, 0, 0, 0, 8, 0, 3, 0, 0],
  [2, 0, 0, 2, 5, 0, 7, 0, 0],
  [0, 2, 0, 3, 0, 0, 0, 0, 4],
  [2, 9, 4, 0, 0, 0, 0, 0, 0],
  [0, 0, 0, 7, 3, 0, 5, 6, 0],
  [7, 0, 5, 0, 6, 0, 4, 0, 0],
  [0, 0, 7, 8, 0, 3, 9, 0, 0],
  [0, 0, 1, 0, 0, 0, 0, 0, 3],
  [3, 0, 0, 0, 0, 0, 0, 0, 2]
]

print(sudoku_korrekt(sudoku1))

sudoku2 = [
  [2, 6, 7, 8, 3, 9, 5, 0, 4],
  [9, 0, 3, 5, 1, 0, 6, 0, 0],
  [0, 5, 1, 6, 0, 0, 8, 3, 9],
  [5, 1, 9, 0, 4, 6, 3, 2, 8],
  [8, 0, 2, 1, 0, 5, 7, 0, 6],
  [6, 7, 4, 3, 2, 0, 0, 0, 5],
  [0, 0, 0, 4, 5, 7, 2, 6, 3],
  [3, 2, 0, 0, 8, 0, 0, 5, 7],
  [7, 4, 5, 0, 0, 3, 9, 0, 1]
]

print(sudoku_korrekt(sudoku2))
```

<sample-output>

False
True

</sample-output>

</programming-exercise>

<quiz id="96f54c81-d835-59db-b626-4acc073d823c"></quiz>
