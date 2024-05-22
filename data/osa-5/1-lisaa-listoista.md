---
path: '/osa-5/1-lisaa-listoja'
title: 'Mer om listor'
hidden: false
---


<text-box variant='learningObjectives' name='Oppimistavoitteet'>

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
nimet = ["Maija", "Liisa", "Pekka"]
print(nimet)
nimet.append("Kalle")
print(nimet)

print("Listalla nimiä:", len(nimet))
print("Nimet aakkosjärjestyksessä:")
nimet.sort()
for nimi in nimet:
  print(nimi)
```

<sample-output>

['Maija', 'Liisa', 'Pekka']
['Maija', 'Liisa', 'Pekka', 'Kalle']
Listalla nimiä: 4
Nimet aakkosjärjestyksessä:
Kalle
Liisa
Maija
Pekka

</sample-output>

Flyttal kan också lagras i listor:

```python
mittaukset = [-2.5, 1.1, 7.5, 14.6, 21.0, 19.2]

for mittaus in mittaukset:
    print(mittaus)

keskiarvo = sum(mittaukset) / len(mittaukset)

print("Keskiarvo:", keskiarvo)
```

<sample-output>

-2.5
1.1
7.5
14.6
21.0
19.2
Keskiarvo: 10.15

</sample-output>

<!--vastaava varoitusteksti löytyy osioista 3-4, 4-6 ja 5-1, tsekkaa kaikki jos muokkaat tätä-->
## Muistutus: globaalin muuttujan käytön sudenkuoppa

Kuten olemme nähneet, funktioiden sisällä on mahdollista määritellä muuttujia. Kannattaa myös huomata se, että funktio näkee sen ulkopuolella, eli pääohjelmassa määritellyt muuttujat. Tälläisia muuttujia sanotaan _globaaleiksi_ muuttujiksi.

Globalien muuttujien käyttämistä funktioista käsin ei useimmiten pidetä hyvänä asiana muun muassa siksi, että ne saattavat johtaa ikäviin bugeihin.

Seuraavassa on esimerkki funktiosta, joka käyttää "vahingossa" globaalia muuttujaa:

```python
def tulosta_vaarinpain(nimet: list):
    # käytetään vahingossa parametrin sijaan globaalia muuttujaa nimilista
    i = len(nimilista) - 1
    while i>=0:
        print(nimilista[i])
        i -= 1

# globaali muuttuja
nimilista = ["Antti", "Emilia", "Erkki", "Margaret"]
tulosta_vaarinpain(nimilista)
print()
tulosta_vaarinpain(["Tupu", "Hupu", "Lupu"])
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

Vaikka funktiota kutsutaan oikein, se tulostaa aina globaalissa muuttujassa _nimilista_ olevat nimet.

Kuten olemme nähneet, kaikki funktioita testaava koodi on kirjoitettava erillisen lohkon sisälle, jotta TMC-testit hyväksyisivät koodin. Edellinen esimerkki siis tulisi toteuttaa seuraavasti:

```python
def tulosta_vaarinpain(nimet: list):
    # käytetään vahingossa parametrin sijaan globaalia muuttujaa nimilista
    i = len(nimilista) - 1
    while i>=0:
        print(nimilista[i])
        i -= 1

# kaikki funktiota testaava koodi tämän lohkon sisälle
if __name__ == "__main__":
    # globaali muuttuja
    nimilista = ["Antti", "Emilia", "Erkki", "Margaret"]
    tulosta_vaarinpain(nimilista)
    print()
    tulosta_vaarinpain(["Tupu", "Hupu", "Lupu"])
```

Nyt myös globaalin muuttujan määrittely on siirtynyt `if`-lohkoon.

TMC-testit suoritetaan aina siten, että mitään `if`-lohkon sisällä olevaa koodia ei huomioida. Tämän takia funktio ei voi edes teoriassa toimia, sillä se viittaa muuttujaan `nimilista` mitä ei testejä suoritettaessa ole ollenkaan olemassa.

## Varning: att skriva över en parameter och returnera för tidigt

Det finns ett par nya källor till buggar som vi borde ta en titt på före vi börjar med övningarna i den här modulen. Låt oss kika på en funktion som berättar om ett heltal hittas i en lista. Båda är definierade som parametrar i funktionen:

```python
def luku_listalla(luvut: list, luku: int):
    for luku in luvut:
        if luku == luku:
            return True
        else:
            return False
```

Den här funktionen verkar alltid returnera värdet `True`. Orsaken till det är att for-loopen skriver över värdet som är lagrat i parametern `nummer`. Därför är villkoret i if-satsen alltid sant.

Att ändra på parameterns namn löser problemet:

```python
def luku_listalla(luvut: list, etsittava_luku: int):
    for luku in luvut:
        if luku == etsittava_luku:
            return True
        else:
            return False
```

Nu verkar villkoret i if-satsen vara i bättre skick. Men det finns ett nytt problem, eftersom funktionen inte ännu heller fungerar som den ska. Om vi testar följande, märker vi en bugg:

```python
on = luku_listalla([1, 2, 3, 4], 3)
print(on)  # tulostuu False
```

Problemet här är att funktionen returnerar ett värde för tidigt, utan att kolla igenom alla siffror i listan. Funktionen kollar faktiskt endast det första värdet i listan och returnerar `True` eller `False` beroende på dess värde. Vi kan inte veta att en siffra inte finns i listan förrän vi har gått igenom hela listan. Kommandot `return False` måste alltså placeras utanför for-loopen:

```python
def luku_listalla(luvut: list, etsittava_luku: int):
    for luku in luvut:
        if luku == etsittava_luku:
            return True

    return False
```

Låt oss ta en titt på en annan funktion som inte fungerar korrekt:

```python
def luvut_erisuuret(luvut: list):
    # apumuuttuja, johon kerätään ne luvut jotka on jo tarkastettu
    luvut = []
    for luku in luvut:
        # joko luku on nähty?
        if luku in luvut:
            return False
        luvut.append(luku)

    return True

on = luvut_erisuuret([1, 2, 2])
print(on)  # tulostuu True
```

Funktionen borde kolla om alla siffor i en lista är olika, men värdet som returneras är alltid `True`.

I det här fallet skriver funktionen igen över värdet som är lagrat i dess parameter. Funktionen försöker använda variabeln `nummer` för att lagra de siffror som redan har kontrollerats, men det här skriver över det ursprungliga argumentet. Att namnge hjälpvariabeln på nytt löser vårt problem:

```python
def luvut_erisuuret(luvut: list):
    # apumuuttuja, johon kerätään ne luvut jotka on jo tarkastettu
    havaitut_luvut = []
    for luku in luvut:
        # joko luku on nähty?
        if luku in havaitut_luvut:
            return False
        havaitut_luvut.append(luku)

    return True

on = luvut_erisuuret([1, 2, 2])
print(on)  # tulostuu False
```

Problem som dessa kan hittas och korrigeras med hjälp av debuggaren eller visualiseringsverktyget. Det lönar sig verkligen att lära sig använda dessa effektivt.

<programming-exercise name='Pisin merkkijono' tmcname='osa05-01a_pisin_merkkijono'>

**HUOM:** tämä ja seuraava tehtävä ovat väärässä järjestyksessä VS Coden sivupalkissa

Tee funktio `pisin(merkkijonot: list)`, joka saa parametrikseen listan merkkijonoja. Funktio etsii ja palauttaa listalta pisimmän merkkijonon. Voit olettaa, että vain yksi jonoista on pisin.

Esimerkkikutsu:

```python

if __name__ == "__main__":
    jonot = ["moi", "moikka", "heip", "hellurei", "terve"]
    print(pisin(jonot))

```

<sample-output>

hellurei

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
["Anu", 10, 26]
```

En databas bestående av flera personer skulle då kunna vara en lista, vars element skulle vara listor som innehåller information om en person:

```python
henkilot = [["Anu", 10, 26], ["Petteri", 7, 22], ["Emilia", 32, 37], ["Antti", 39, 44]]

for henkilo in henkilot:
  nimi = henkilo[0]
  ika = henkilo[1]
  kenka = henkilo[2]
  print(f"{nimi}: ikä {ika} vuotta, kengännumero {kenka}")
```

<sample-output>

Anu: ikä 10 vuotta, kengännumero 26
Petteri: ikä  7 vuotta, kengännumero 22
Emilia: ikä 32 vuotta, kengännumero 37
Antti: ikä 39 vuotta, kengännumero 44

</sample-output>

For-loopen går igenom elementen i den yttre listan en för en. Varje lista som innehåller info om en person tilldelas en för en till variabeln `person`.

Listor är inte alltid det bästa sättet att presentera data som information om en person. Vi kommer snart att se på lexikon (dictionary) i Python. Den är bättre anpassad för situationer som den ovan nämnda.

## Matriser

En tvådimensionell tabell – matris – är ett annat användningsområde för listor inom listor.

Till exempel följande matris…

<img src="5_1_0.png">

…kan presenteras som en tvådimensionell lista i Python på följande sätt:

```python
matriisi = [[1, 2, 3], [3, 2, 1], [4, 5, 6]]
```

Eftersom en matris är en lista som innehåller listor kan enskilda element inom matrisen kommas åt med hjälp av varandra påföljande hakparenteser. Det första indexet hänvisar till raden, medan den andra hänvisar till kolumnen. Indexeringen startar från noll så `min_matris[0][1]` hänvisar till det andra elementet på den första raden.

```python
matriisi = [[1, 2, 3], [3, 2, 1], [4, 5, 6]]

print(matriisi[0][1])
matriisi[1][0] = 10
print(matriisi)
```

<sample-output>

2
[[1, 2, 3], [10, 2, 1], [4, 5, 6]]

</sample-output>

Som med vilken som helst lista, kan raderna i matrisen gås igenom med en for-loop. Den följande koden skriver ut varje rad i matrisen på en skild rad:

```python
matriisi = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

for rivi in matriisi:
    print(rivi)
```

<sample-output>

[1, 2, 3]
[4, 5, 6]
[7, 8, 9]

</sample-output>

På samma sätt kan kapslade loopar användas för att komma åt enskilda element inom matrisen. Följande kodsnutten skriver ut varje element i matrisen på en skild rad med hjälp av två for-loopar:

```python
matriisi = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

for rivi in matriisi:
    print("uusi rivi")
    for alkio in rivi:
        print(alkio)
```

<sample-output>

uusi rivi
1
2
3
uusi rivi
4
5
6
uusi rivi
7
8
9

</sample-output>

## Visualisering av kod som innehåller listor inom listor

Program som består av listor inom listor kan vara svåra att greppa om i början. Visualiseringsverktyget av Python Tutor är ett bra sätt att bekanta sig med hur de fungerar. Det följande är en visualisering av exemplet ovan:

<img src="5_1_0a.png">

Bilden ovan avslöjar att en 3 x 3 -matris tekniskt sett består av fyra listor. Den första listan representerar hela matrisen. De tre resterande listorna är element i den första listan, och de representerar rader i matrisen.

Eftersom multidimensionella listor kan gås igenom med kapslade loopar skulle man kunna tänka sig att listorna är inuti varandra, men som bilden visar är detta inte sant. Istället hänvisar den ”stora listan” som representerar matrisen till skilda listor som alla representerar en rad i matrisen. Det här är en referens – något vi kommer att se mera på i följande del.

I bilden ovan har programmet hunnit till den andra raden i matrisen och det är den listan som variabeln `rad` hänvisar till för tillfället. Variabeln `element` innehåller det element där programmet är vid för tillfället. Värdet i den variabeln är det mellersta värdet i listan, dvs. 5.

## Komma åt element i en matris

Att komma åt en viss rad i en matris är enkelt. Det är bara att välja den raden. Följande funktion räknar summan av elementen på en viss rad:

```python
def rivin_alkioiden_summa(matriisi, rivi_nro: int):
    # tarkasteluun valitaan yksi rivi
    rivi = matriisi[rivi_nro]
    summa = 0
    for alkio in rivi:
        summa += alkio

    return summa

m = [[4, 2, 3, 2], [9, 1, 12, 11], [7, 8, 9, 5], [2, 9, 15, 1]]

summa = rivin_alkioiden_summa(m, 1)
print(summa) # tulostuu 33 (saadaan laskemalla 9 + 1 + 12 + 11)
```

Att arbeta med kolumner i en matris är lite mera komplicerat eftersom matrisen är lagrad som rader:

```python
def sarakkeen_alkioiden_summa(matriisi, sarake_nro: int):
    # summaan lisätään kaikkien rivien halutussa kohdassa oleva alkio
    summa = 0
    for rivi in matriisi:
        summa += rivi[sarake_nro]

    return summa

m = [[4, 2, 3, 2], [9, 1, 12, 11], [7, 8, 9, 5], [2, 9, 15, 1]]

summa = sarakkeen_alkioiden_summa(m, 2)
print(summa) # tulostuu 39 (saadaan laskemalla 3 + 12 + 9 + 15)
```

Kolumnen som söks här består av elementen vid index 2 på varje rad.

Visualiseringsverktyget rekommenderas varmt för att bättre förstå hur de här funktionerna fungerar.

Att ändra på ett värde hos ett specifikt element inom en matris är enkelt. Välj en rad i matrisen och sedan en kolumn inom raden:

```python
def vaihda_arvoon(matriisi, rivi_nro: int, sarake_nro: int, arvo: int):
    # haetaan oikea rivi
    rivi = matriisi[rivi_nro]
    # ja sen sisältä oikea kohta
    rivi[sarake_nro] = arvo

m = [[4, 2, 3, 2], [9, 1, 12, 11], [7, 8, 9, 5], [2, 9, 15, 1]]

print(m)
vaihda_arvoon(m, 2, 3, 1000)
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


<programming-exercise name='Alkioiden määrä' tmcname='osa05-01_alkoiden_maara'>

**HUOM:** tämä ja edellinen tehtävä ovat väärässä järjestyksessä VS Coden sivupalkissa

Tee funktio `laske_alkiot(matriisi: list, alkio: int)`, joka saa parametrikseen kaksiulotteisen kokonaislukutaulukon. Funktio laskee, kuinka monta annetun alkion mukaista arvoa taulukosta löytyy.

Esimerkiksi

```python
m = [[1, 2, 1], [0, 3, 4], [1, 0, 0]]
print(laske_alkiot(m, 1))
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
def tulosta(sudoku):
    for rivi in sudoku:
        for ruutu in rivi:
            if ruutu > 0:
                print(f" {ruutu}", end="")
            else:
                print(" _", end="")
        print()

tulosta(sudoku)
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

Go-pelissä lisätään vuorotellen mustia ja valkoisia kiviä pelilaudalle. Pelin voittaa se pelaaja, joka saa omilla kivillään rajattua enemmän aluetta pelilaudalta.

Kirjoita funktio `kumpi_voitti(pelilauta: list)`, joka saa parametrikseen kaksiulotteisen taulukon, joka kuvaa pelilautaa. Taulukko koostuu kokonaisluvuista seuraavasti:

* 0: tyhjä ruutu
* 1: pelaajan 1 nappula
* 2: pelaajan 2 nappula

Esimerkissä pelilaudan koko voi olla mikä tahansa.

Funktio palauttaa arvon 1, jos pelaaja 1 on voittanut pelin, ja arvon 2, jos pelaaja 2 on voittanut pelin. Jos molemmilla pelaajilla on yhtä paljon nappuloita laudalla, funktio palauttaa arvon 0.

</programming-exercise>

<programming-exercise name='Sudoku: rivit oikein' tmcname='osa05-03_sudoku_osa1'>

Tee funktio `rivi_oikein(sudoku: list, rivi_nro: int)`, joka saa parametriksi sudokuruudukkoa esittävän kaksiulotteisen taulukon ja rivin numeron kertovan kokonaisluvun (rivit on numeroitu nollasta alkaen). Metodi palauttaa tiedon, onko rivi oikein täytetty eli onko siinä kukin luvuista 1–9 korkeintaan kerran.

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

print(rivi_oikein(sudoku, 0))
print(rivi_oikein(sudoku, 1))
```

<sample-output>

True
False

</sample-output>

</programming-exercise>

<programming-exercise name='Sudoku: sarakkeet oikein' tmcname='osa05-04_sudoku_osa2'>

Tee funktio `sarake_oikein(sudoku: list, sarake_nro: int)`, joka saa parametriksi sudokuruudukkoa esittävän kaksiulotteisen taulukon ja sarakkeen (eli pystyrivin) numeron kertovan kokonaisluvun. Metodi palauttaa tiedon, onko sarake oikein täytetty eli onko siinä kukin luvuista 1–9 korkeintaan kerran.

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

print(sarake_oikein(sudoku, 0))
print(sarake_oikein(sudoku, 1))
```

<sample-output>

False
True

</sample-output>

</programming-exercise>

<programming-exercise name='Sudoku: neliöt oikein' tmcname='osa05-05_sudoku_osa3'>

Tee funktio `nelio_oikein(sudoku: list, rivi_nro: int, sarake_nro: int)`, joka saa parametriksi sudokuruudukkoa esittävän kaksiulotteisen taulukon sekä yhden ruudun paikan kertovat rivi- ja sarakenumerot.

Funktio kertoo onko parametrina saadusta rivi/sarakenumerosta alkava 3x3-kokoinen neliö oikein täytetty eli onko siinä kukin luvuista 1–9 korkeintaan kerran.

Huomaa, että tässä tehtävässä toteutettava funktio on hieman yleiskäyttöisempi kuin sudokussa oikeasti tarvitaan. Todellisuudessahan oikeassa sudokussa tarkastellaan ainoastaan kohdista (0, 0), (0, 3), (0, 6), (3, 0), (3, 3), (3, 6), (6, 0), (6, 3) ja (6, 6) alkavia neliöitä.

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

print(nelio_oikein(sudoku, 0, 0))
print(nelio_oikein(sudoku, 1, 2))
```

<sample-output>

False
True

</sample-output>

Ensimmäisen funktiokutsun tarkastelema kohdasta 0, 0 alkava neliö on

<pre>
9 0 0
2 0 0
0 2 0
</pre>

Toisen funktiokutsun tarkastelema kohdasta riviltä 1 ja sarakkeesta 2 alkava neliö on

<pre>
0 2 5
0 3 0
4 0 0
</pre>

Tämä neliö on siis sellainen, jota oikeassa sudokussa ei tarkasteltaisi.

</programming-exercise>

<programming-exercise name='Sudoku: ruudukko oikein' tmcname='osa05-06_sudoku_osa4'>

Tee funktio `sudoku_oikein(sudoku: list)`, joka saa parametriksi sudokuruudukkoa esittävän kaksiulotteisen taulukon. Funktio kertoo käyttäen edellisen kolmen tehtävän funktioita (kopioi ne tämän tehtävän koodin joukkoon), onko parametrina saatu ruudukko täytetty oikein, eli sen jokainen rivi, jokainen sarake sekä kaikki erilliset 3x3-neliöt sisältävät korkeintaan kertaalleen jokaisen luvuista 1–9.

Huom: ylempänä olevaan sudokuruudukkoa esittävään kuvaan on merkitty ne 3x3-neliöt, joita sudokua ratkaistessa tulee tarkastella.
Nämä ovat siis kohdista (0, 0), (0, 3), (0, 6), (3, 0), (3, 3), (3, 6), (6, 0), (6, 3) ja (6, 6) alkavat yhdeksän neliöä.

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

print(sudoku_oikein(sudoku1))

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

print(sudoku_oikein(sudoku2))
```

<sample-output>

False
True

</sample-output>

</programming-exercise>

<quiz id="646c91c8-cc9a-57c0-b502-ef939f5f4d45"></quiz>
