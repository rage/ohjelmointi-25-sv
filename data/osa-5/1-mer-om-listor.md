---
path: '/osa-5/1-mer-om-listor'
title: 'Mer om listor'
hidden: false
---


<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* kan du skapa listor med element av olika typer
* vet du hur man kan använda listor för att organisera data
* kan du lagra en matris som en tvådimensionell lista.

</text-box>

<!--vastaava teksti löytyy osioista 3-1, 5-1 ja 6-1, tsekkaa kaikki jos muokkaat tätä-->
<text-box variant='hint' name='Kurssin tehtävien tekemisestä'>

Ohjelmointitaidon kehittyminen edellyttää vahvaa rutiinia ja myös omaa soveltavaa oivaltamista. Tämän takia kurssilla on paljon tehtäviä. Osa tehtävistä on kohtuullisen suoraviivaisesti materiaalia hyödyntäviä ja osa taas aivan tarkoituksella haastavampia soveltavia tehtäviä.

Ei kannata huolestua, vaikka osa kurssin tehtävistä tuntuisikin ensiyrittämällä liian vaikealta. Kaikkia tehtäviä ei ole pakko tehdä, kuten [arvosteluperusteet](/arvostelu-ja-kokeet) toteavat, _kurssin läpipääsyyn vaaditaan vähintään 25 % jokaisen osan ohjelmointitehtävien pisteistä._

**Kurssin osien tehtävät eivät etene vaikeusjärjestyksessä.** Jokaisessa aliosassa esitellään yleensä muutama uusi konsepti, joita harjoitellaan sekä helpommilla että soveltavimmilla tehtävillä. **Jos törmäät liian haastavan tuntuiseen tehtävään, hyppää seuraavaan**. Voit palata vaikeimpiin tehtäviin osan lopuksi, jos aikaa vielä jää.

Lohdutuksen sanana todettakoon, että tällä viikolla mahdottomalta vaikuttava tehtävä näyttää melko varmasti neljän viikon päästä melko helpolta.

</text-box>

## Listor med olika typer av data

I den förra modulen fokuserade vi främst på listor med element av heltalstyp, men listor kan innehålla vilka typer av data som helst. En lista bestående av strängar kunde exempelvis kunna se ut så här:

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
## Muistutus: globaalin muuttujan käytön sudenkuoppa

Kuten olemme nähneet, funktioiden sisällä on mahdollista määritellä muuttujia. Kannattaa myös huomata se, että funktio näkee sen ulkopuolella, eli pääohjelmassa määritellyt muuttujat. Tälläisia muuttujia sanotaan _globaaleiksi_ muuttujiksi.

Globalien muuttujien käyttämistä funktioista käsin ei useimmiten pidetä hyvänä asiana muun muassa siksi, että ne saattavat johtaa ikäviin bugeihin.

Seuraavassa on esimerkki funktiosta, joka käyttää "vahingossa" globaalia muuttujaa:

```python
def tulosta_vaarinpain(namn: list):
    # käytetään vahingossa parametrin sijaan globaalia muuttujaa nimilista
    i = len(nimilista) - 1
    while i>=0:
        print(nimilista[i])
        i -= 1

# globaali muuttuja
nimilista = ["August", "Emilia", "Erkki", "Margaret"]
tulosta_vaarinpain(nimilista)
print()
tulosta_vaarinpain(["Tupu", "Hupu", "Lupu"])
```

<sample-output>

Margaret
Erkki
Emilia
August

Margaret
Erkki
Emilia
August

</sample-output>

Vaikka funktiota kutsutaan oikein, se tulostaa aina globaalissa muuttujassa _nimilista_ olevat namn.

Kuten olemme nähneet, kaikki funktioita testaava koodi on kirjoitettava erillisen lohkon sisälle, jotta TMC-testit hyväksyisivät koodin. Edellinen esimerkki siis tulisi toteuttaa seuraavasti:

```python
def tulosta_vaarinpain(namn: list):
    # käytetään vahingossa parametrin sijaan globaalia muuttujaa nimilista
    i = len(nimilista) - 1
    while i>=0:
        print(nimilista[i])
        i -= 1

# kaikki funktiota testaava koodi tämän lohkon sisälle
if __name__ == "__main__":
    # globaali muuttuja
    nimilista = ["August", "Emilia", "Erkki", "Margaret"]
    tulosta_vaarinpain(nimilista)
    print()
    tulosta_vaarinpain(["Tupu", "Hupu", "Lupu"])
```

Nyt myös globaalin muuttujan määrittely on siirtynyt `if`-lohkoon.

TMC-testit suoritetaan aina siten, että mitään `if`-lohkon sisällä olevaa koodia ei huomioida. Tämän takia funktio ei voi edes teoriassa toimia, sillä se viittaa muuttujaan `nimilista` mitä ei testejä suoritettaessa ole ollenkaan olemassa.

## Varning: att skriva över en parameter och returnera för tidigt

Det finns ett par nya källor till buggar som vi borde ta en titt på före vi börjar med övningarna i den här modulen. Låt oss kika på en funktion som berättar om ett heltal hittas i en lista. Båda är definierade som parametrar i funktionen:

```python
def siffra_i_listan(siffror: list, siffra: int):
    for siffra in siffror:
        if siffra == siffra:
            return True
        else:
            return False
```

Den här funktionen verkar alltid returnera värdet `True`. Orsaken till det är att for-loopen skriver över värdet som är lagrat i parametern `siffra`. Därför är villkoret i if-satsen alltid sant.

Att ändra på parameterns namn löser problemet:

```python
def siffra_i_listan(siffror: list, siffra_som_soks: int):
    for siffra in siffror:
        if siffra == siffra_som_soks:
            return True
        else:
            return False
```

Nu verkar villkoret i if-satsen vara i bättre skick. Men det finns ett nytt problem, eftersom funktionen inte ännu heller fungerar som den ska. Om vi testar följande, märker vi en bugg:

```python
resultat = siffra_i_listan([1, 2, 3, 4], 3)
print(resultat) # False
```

Problemet här är att funktionen returnerar ett värde för tidigt, utan att kolla igenom alla siffror i listan. Funktionen kollar faktiskt endast det första värdet i listan och returnerar `True` eller `False` beroende på dess värde. Vi kan inte veta att en siffra inte finns i listan förrän vi har gått igenom hela listan. Kommandot `return False` måste alltså placeras utanför for-loopen:

```python
def siffra_i_listan(siffror: list, siffra_som_soks: int):
    for siffra in siffror:
        if siffra == siffra_som_soks:
            return True

    return False
```

Låt oss ta en titt på en annan funktion som inte fungerar korrekt:

```python
def siffrorna_olika(siffror: list):
    # hjälpvariabel där vi lagrar de värden som kollats
    siffror = []
    for siffra in siffror:
        # har siffran redan förekommit?
        if siffra in siffror:
            return False
        siffror.append(siffra)

    return True

resultat = siffrorna_olika([1, 2, 2])
print(resultat) # True
```

Funktionen borde kolla om alla siffor i en lista är olika, men värdet som returneras är alltid `True`.

I det här fallet skriver funktionen igen över värdet som är lagrat i dess parameter. Funktionen försöker använda variabeln `siffra` för att lagra de siffror som redan har kontrollerats, men det här skriver över det ursprungliga argumentet. Att namnge hjälpvariabeln på nytt löser vårt problem:

```python
def siffrorna_olika(siffror: list):
    # hjälpvariabel där de siffror som kollats lagras
    sedda_siffror = []
    for siffra in siffror:
        # har siffran redan förekommit?
        if siffra in sedda_siffror:
            return False
        sedda_siffror.append(siffra)

    return True

resultat = siffrorna_olika([1, 2, 2])
print(resultat) # False
```

Problem som dessa kan hittas och korrigeras med hjälp av debuggaren eller [visualiseringsverktyget](https://pythontutor.com/visualize.html). Det lönar sig verkligen att lära sig använda dessa effektivt.

<programming-exercise name='Längsta strängen' tmcname='osa05-01a_langsta_strangen'>

**HUOM:** tämä ja seuraava tehtävä ovat väärässä järjestyksessä VS Coden sivupalkissa

Skapa funktionen `langst(strangar: list)` som får som argument en lista med strängar. Funktionen ska hitta och returnera den längsta strängen. Du kan anta att det bara finns en längsta sträng.

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

Ett element i en lista kan vara en lista:

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

I hurdana fall skulle det här kunna vara nyttigt?

Kom ihåg att listor kan innehålla element av olika typer. Du kan till exempel lagra information om en person i en lista. Det första elementet kan till exempel vara personens namn, det andra dess ålder och det tredje dess höjd:

```python
["Nelly", 10, 26]
```

En databas bestående av flera personer skulle då kunna vara en lista, vars element skulle vara listor som innehåller information om en person:

```python
personer = [["Nelly", 10, 26], ["PO", 7, 22], ["Emilia", 32, 37], ["August", 39, 44]]

for person in personer:
  namn = person[0]
  alder = person[1]
  sko = person[2]
  print(f"{namn}: {alder} år, skostorlek {sko}")
```

<sample-output>

Nelly: 10 år, skostorlek 26
PO: 7 år, skostorlek 22
Emilia: 32 år, skostorlek 37
August: 39 år, skostorlek 44

</sample-output>

For-loopen går igenom elementen i den yttre listan en för en. Varje lista som innehåller info om en person tilldelas en för en till variabeln `person`.

Listor är inte alltid det bästa sättet att presentera data som information om en person. Vi kommer snart att se på lexikon (dictionary) i Python. Den är bättre anpassad för situationer som den ovan nämnda.

## Matriser

En tvådimensionell tabell – matris – är ett annat användningsområde för listor inom listor.

Till exempel följande matris…

<img src="5_1_0.png">

…kan presenteras som en tvådimensionell lista i Python på följande sätt:

```python
matris = [[1, 2, 3], [3, 2, 1], [4, 5, 6]]
```

Eftersom en matris är en lista som innehåller listor kan enskilda element inom matrisen kommas åt med hjälp av varandra påföljande hakparenteser. Det första indexet hänvisar till raden, medan den andra hänvisar till kolumnen. Indexeringen startar från noll så `matris[0][1]` hänvisar till det andra elementet på den första raden.

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

På samma sätt kan kapslade loopar användas för att komma åt enskilda element inom matrisen. Följande kodsnutten skriver ut varje element i matrisen på en skild rad med hjälp av två for-loopar:

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

Program som består av listor inom listor kan vara svåra att greppa om i början. [Visualiseringsverktyget](https://pythontutor.com/visualize.html) av Python Tutor är ett bra sätt att bekanta sig med hur de fungerar. Det följande är en visualisering av exemplet ovan:

<img src="5_1_0a.png">

Bilden ovan avslöjar att en 3 x 3 -matris tekniskt sett består av fyra listor. Den första listan representerar hela matrisen. De tre resterande listorna är element i den första listan, och de representerar rader i matrisen.

Eftersom multidimensionella listor kan gås igenom med kapslade loopar skulle man kunna tänka sig att listorna är inuti varandra, men som bilden visar är detta inte sant. Istället hänvisar den "stora listan" som representerar matrisen till skilda listor som alla representerar en rad i matrisen. Det här är en referens – något vi kommer att se mera på i följande del.

I bilden ovan har programmet hunnit till den andra raden i matrisen och det är den listan som variabeln `rad` hänvisar till för tillfället. Variabeln `element` innehåller det element där programmet är vid för tillfället. Värdet i den variabeln är det mellersta värdet i listan, dvs. 5.

## Komma åt element i en matris

Att komma åt en viss rad i en matris är enkelt. Det är bara att välja den raden. Följande funktion räknar summan av elementen på en viss rad:

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

Att arbeta med kolumner i en matris är lite mera komplicerat eftersom matrisen är lagrad som rader:

```python
def summan_av_kolumnens_element(matris, kolumnnummer: int):
    # till summan adderas för varje rad elementet på det önskade stället
    summa = 0
    for rad in matris:
        summa += rad[kolumnnummer]

    return summa

m = [[4, 2, 3, 2], [9, 1, 12, 11], [7, 8, 9, 5], [2, 9, 15, 1]]

summa = summan_av_kolumnens_element(m, 2)
print(summa) # 39 (dvs. 3 + 12 + 9 + 15)
```

Kolumnen som söks här består av elementen vid index 2 på varje rad.

[Visualiseringsverktyget](https://pythontutor.com/visualize.html) rekommenderas varmt för att bättre förstå hur de här funktionerna fungerar.

Att ändra på ett värde hos ett specifikt element inom en matris är enkelt. Välj en rad i matrisen och sedan en kolumn inom raden:

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

Observera att vi ovan använde indexen för raden och kolumnen för att komma åt det element vi ville ändra på. Om vi vill ändra på innehållet i en matris måste vi komma åt elementen md hjälp av deras index. Vi kan inte bara använda oss av en `for element in lista` -loop för att gå igenom matrisen då vi vill ändra på innehållet i en matris.

Istället behöver vi hålla reda på indexen hos elementen: till exempel med en while-loop eller en for-loop med `range`-funktionen. Följande kod ökar på värdet hos varje element i en matris med ett:


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

**HUOM:** tämä ja edellinen tehtävä ovat väärässä järjestyksessä VS Coden sivupalkissa

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

En matris kan fungera väl som datastruktur i flera olika spel. Till exempel rutorna i ett sudokuspel…

<img src="5_1_1.png">

…kan representeras i en matris på följande sätt:

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

```x

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

Flera andra spel kan också representeras på liknande sätt: till exempel schack, minröj, sänka skepp och Mastermind. I sudoku fungerar siffor väl för att representera spelets läge, medan för andra spel kan andra metoder vara bättre.

<programming-exercise name='Go' tmcname='osa05-02_go'>

I spelet Go plaerar man turvis svarta och vita stenar på spelbrädet. Den spelare som har flera stenar på brädet vinner spelet.

Skapa funktionen `vem_vann(brade: list)` som får som argument en matris som representerar spelbrädet. Matrisen består av heltalsvärden:

* 0: tom ruta
* 1: sten, spelare 1
* 2: sten, spelare 2

Spelbrädet kan vara av vilken storlek som helst.

Funktionen ska returnera `1` om spelare ett har vunnit, `2` om spelare två har vunnit och `0` om båda spelarna har lika många stenar på brädet.

</programming-exercise>

<programming-exercise name='Sudoku: Rader korrekt' tmcname='osa05-03_sudoku_rader'>

Skapa funktionen `rad_korrekt(sudoku: list, radnummer: int)` som får som argument en matris samt ett heltal. Radnumreringen börjar med noll. Funktionen ska returnera ett värde som beskriver om raden är korrekt ifylld, dvs. talen 1-9 förekommer högst en gång.

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

Skapa funktionen `kolumn_korrekt(sudoku: list, kolumnnummer: int)` som får som argument en matris samt ett heltal. Funktionen ska returnera ett värde som beskriver om kolumnen är korrekt ifylld, dvs. talen 1-9 förekommer högst en gång.


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

Funktionen ska berätta om 3 x 3 -kvadraten vid positionen (radnummer, kolumnnummer) är korrekt ifylld, dvs. talen 1-9 förekommer högst en gång.

Det är värt att notera att i man vanligtvis i sudoku enbart ser på kvadraterna vid positionerna (0, 0), (0, 3), (0, 6), (3, 0), (3, 3), (3, 6), (6, 0), (6, 3) och (6, 6). Den här funktionen kommer dock inte att beakta det här.

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

I ett riktigt sudokuspel skulle den här kvadraten inte alltså kollas.

</programming-exercise>

<programming-exercise name='Sudoku: Korrekt?' tmcname='osa05-06_sudoku_korrekt'>

Skapa funktionen `sudoku_korrekt(sudoku: list)` som får som argument en matris. Den här funktionen ska använda sig av de tre föregående uppgifternas funktioner (kopiera dem) för att säkerställa att varje rad, kolumn och 3 x 3 -kvadrat innehåller högst en av siffrorna 1-9.

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

<quiz id="646c91c8-cc9a-57c0-b502-ef939f5f4d45"></quiz>
