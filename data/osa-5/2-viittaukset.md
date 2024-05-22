---
path: '/osa-5/2-viittaukset'
title: 'Referenser'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* vet du vad som menas med en referens till en variabel
* vet du att det kan finnas flera referenser till ett och samma objekt
* kan du använda listor som parameter i funktioner
* förstår du vad som menas med sidoeffekt hos en funktion.

</text-box>

Hittills har vi tänkt att en variabel är en slags ”låda” som innehåller variabelns värde. Från teknisk synvinkel stämmer detta inte i Python – variabler innehåller inte ett värde, utan en referens till ett objekt, som en siffra, sträng eller en lista.

I praktiken innebär det att man inte lagrar ett värde i en variabel, utan ett ställe varifrån variabelns värde hittas från.

En referens kan beskrivas som en pil från variabeln till dess riktiga värde:

<img src="5_2_1.png">

Referensen berättar alltså var det riktiga värdet finns. Funktionen `id` berättar vart en variabel refererar:

```python
a = [1, 2, 3]
print(id(a))
b = "Tämäkin on viittaus"
print(id(b))
```

<sample-output>

4538357072
4537788912

</sample-output>

Referensen, alltså variabelns id är ett heltal. Man kan tänka att talet är adressen för variabelns värde i datorns minne. Observera att om du kör koden ovan på din dator, kommer resultatet sannolikt vara olikt eftersom variablerna har olika referenser.

Som vi redan såg i förra delens exempel, visar Python Tutors visualiseringsverktyg referenser som ”pilar” till det riktiga innehållet. Verktyget ”lurar” ändå när det kommer till strängar, och visar dem som att strängens innehåll skulle vara lagrat i själva variabeln:

<img src="5_2_1a.png">

Så är det ändå inte i verkligheten – strängar behandlas också internt av Python på samma sätt som listor.

Flera av Pythons inbyggda datatyper – som `str` – är oföränderliga. Det betyder att värdet på objektet aldrig kan ändras. Däremot kan ett värde ersättas med ett nytt värde.

<img src="5_2_2.png">

I Python finns också datatyper som är föränderliga. Till exempel innehållet på en lista kan förändras utan att man behöver skapa en ny lista:

<img src="5_2_3.png">

Något förvånande är att också grundläggande datatyper för lagring av siffor och sanningsvärden, `int`, `float` och `bool`, är oföränderliga. Låt oss använda följande kod som exempel:

```python
luku = 1
luku = 2
luku += 10
```

Det verkar som att koden ändrar på siffran, men från teknisk synvinkel är det inte så. Istället skapar varje kommando en ny siffra.

Utskriften från det här programmet är intressant:

```python
luku = 1
print(id(luku))
luku += 10
print(id(luku))
a = 1
print(id(a))
```

<sample-output>

4535856912
4535856944
4535856912

</sample-output>

I början refererar variabeln `luku` till adressen `4535856912` och när variabelns värde förändras refererar variabeln till adressen `4535856944`. När variabeln `a` definieras och får värdet `1`, kommer variabeln att referera till samma ställe som variabeln `luku` när dess värde var `1`.

Det verkar som att Python har lagrat siffran 1 till adressen `4535856912` och alltid då en variabels värde är `1`, refererar variabeln till det här specifika stället i ”datorns minne”.

Även om de grundläggande datatyperna `int`, `float` och `bool` är referenser behöver man som programmerare inte egentligen fundera på det.

## Flera referenser till en och samma lista

Vi undersöker som ett exempel att kopiera värdet på en variabel med en lista:

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

Om en och samma lista har flera referenser kan den behandlas på samma sätt med vilken som helst av referenserna. Däremot återspeglas en förändring via en referens också till alla andra referenser.

Visualiseringsverktyget klargör igen vad som sker i programmet:

<img src="5_2_4a.png">

## Att kopiera en lista

Om du vill skapa en verklig kopia av en lista kan du skapa en ny lista och lägga till alla element från den ursprungliga listan till den nya listan:

```python
lista = [1, 2, 3, 3, 5]

kopio = []
for alkio in lista:
    kopio.append(alkio)

kopio[0] = 10
kopio.append(6)
print("lista", lista)
print("kopio", kopio)
```

<sample-output>

lista [1, 2, 3, 3, 5]
kopio [10, 2, 3, 3, 5, 6]

</sample-output>

Så ser det ut från visualiseringsverktyget:

<img src="5_2_4b.png">

Variabeln `ny_lista` refererar till en annan lista än `min_lista`.

Ett enklare sätt att kopiera en lista är att använda hakparenteser `[]`, som vi använt tidigare för att extrahera innehåll från strängar och listor. Notationen `[:]` väljer alla element i en samling. Därmed skapar det en kopia av en lista:

```python
lista = [1,2,3,4]
kopio = lista[:]

lista[0] = 10
kopio[1] = 20

print(lista)
print(kopio)
```

<sample-output>

[10, 2, 3, 4]
[1, 20, 3, 4]

</sample-output>

## En lista som parameter i en funktion

När en lista ges som parameter till en funktion, förmedlas referensen till listan. Det här innebär att funktionen kan ändra på listan som getts som parameter.

Till exempel följande funktion lägger till ett nytt element i en lista som getts som funktionens parameter:

```python
def lisaa_alkio(lista: list):
    uusi_alkio = 10
    lista.append(uusi_alkio)

lista = [1,2,3]
print(lista)
lisaa_alkio(lista)
print(lista)
```

<sample-output>
[1, 2, 3]
[1, 2, 3, 10]
</sample-output>

Märk att funktionen `lisaa_alkio` inte returnerar något, utan ändrar på den lista som getts som funktionens parameter. Visualiseringsverktyget presenterar situationen så här:

<img src="5_2_4c.png">

Global frame syftar på huvudprogrammets variabler, och den blå lådan `lisaa_alkio` på funktionens parametrar och variabler. Som visualiseringen visar, refererar funktionen till samma lista som huvudprogrammet, vilket betyder att ändringar som görs i listan inom funktionen också syns i huvudprogrammet.

Ett annat sätt är att skapa en ny lista och returnera den:

```python
def lisaa_alkio(lista: list) -> list:
    uusi_alkio = 10
    kopio = lista[:]
    kopio.append(uusi_alkio)
    return kopio

luvut = [1, 2, 3]
luvut2 = lisaa_alkio(luvut)

print("Alkuperäinen lista:", luvut)
print("Uusi lista:", luvut2)
```

<sample-output>

Alkuperäinen lista: [1, 2, 3]
Uusi lista: [1, 2, 3, 10]

</sample-output>

Om du inte är helt säker på vad som händer i en kodsnutt, kan det löna sig att utnyttja visualiseringsverktyget.

## Ändra på en lista som getts som argument

Det följande är ett försök på att skapa en funktion som ökar på varje element med tio:

```python
def kasvata_kaikkia(lista: list):
    uusilista = []
    for alkio in lista:
        uusilista.append(alkio + 10)
    lista = uusilista

luvut = [1, 2, 3]
print("alussa ",luvut)
kasvata_kaikkia(luvut)
print("funktion jälkeen", luvut)
```

<sample-output>

alussa: [1, 2, 3]
funktion jälkeen: [1, 2, 3]

</sample-output>


Av någon orsak fungerar funktionen inte. Varför så?

Funktionen tar emot en referens till en lista som argument. Det här är lagrat i variabeln `min_lista`. Tilldelningen `min_lista = ny_lista` tilldelar ett nytt värde till den samma variabeln. Variabeln `min_lista` hänvisar nu till den nya listan som skapades i funktionen, vilket betyder att referensen till den ursprungliga listan inte mera är tillgänglig inom funktionen. Tilldelningen har inte dock någon påverkan utanför funktionen.

<img src="5_2_6.png" width="400">

Dessutom innehåller variabeln `ny_lista` nu de nya värdena, men de är inte tillgängliga utanför funktionen. Variabeln försvinner alltså när funktionen körts och programmet fortsätter tillbaka till huvudfunktionen. Variabeln siffror i huvudfunktionen hänvisar alltid till den ursprungliga listan.

Visualiseringsverktyget hjälper igen. När du går igenom stegen utförligt märker du att den ursprungliga listan inte påverkas på något sätt av funktionen:

<img src="5_2_4d.png">

Ett enkelt sätt att korrigera problemet är att kopiera över alla element från den nya listan till den gamla:

```python
def kasvata_kaikkia(lista: list):
    uusilista = []
    for alkio in lista:
        uusilista.append(alkio + 10)

    # kopioidaan vanhaan listaan uuden listan arvot
    for i in range(len(lista)):
        lista[i] = uusilista[i]
```

Eller lite enklare tack vare Python:

```python
>>> lista = [1, 2, 3, 4]
>>> lista[1:3] = [10, 20]
>>> lista
[1, 10, 20, 4]
```

I exemplet ovan ersätts en del av en lista med värden från en annan samling.

Som vi vet, kan vi också göra detta för en hel samling:

```python
>>> lista = [1, 2, 3, 4]
>>> lista[:] = [100, 99, 98, 97]
>>> lista
[100, 99, 98, 97]
```

Allt innehåll i den gamla listan ersätts. Inspirerat av det här har vi nu skapat en fungerande version av funktionen som ökar på elementens värden:

```python
def kasvata_kaikkia(lista: list):
    uusilista = []
    for alkio in lista:
        uusilista.append(alkio + 10)

    lista[:] = uusilista
```

Egentligen finns det ingen orsak att skapa en ny lista inom funktionen. Vi kan helt enkelt tilldela värdena direkt till den ursprungliga listan:

```python
def kasvata_kaikkia(lista: list):
    for i in range(len(lista)):
        lista[i] += 10

```


<programming-exercise name='Alkiot tuplana' tmcname='osa05-06a_alkiot_tuplana'>

Tee funktio `tuplaa_alkiot(luvut: list)`, joka saa parametrikseen lukuja sisältävän listan.

Funktio palauttaa uuden listan, jossa alkuperäisen listan alkiot on kerrottu kahdella. Funkto _ei_ saa muuttaa alkuperäistä listaa.

Esimerkki funktion kutsumisesta:

```python
if __name__ == "__main__":
    luvut = [2, 4, 5, 3, 11, -4]
    tuplaluvut = tuplaa_alkiot(luvut)
    print("alkuperäinen:", luvut)
    print("tuplattu:", tuplaluvut)
```
<sample-output>

alkuperäinen: [2, 4, 5, 3, 11, -4]
tuplattu: [4, 8, 10, 6, 22, -8]

</sample-output>

</programming-exercise>


<programming-exercise name='Poista pienin' tmcname='osa05-06b_poista_pienin'>

Tee funktio `poista_pienin(luvut: list)`, joka saa parametrikseen lukuja sisältävän listan.

Funktio etsii ja poistaa listasta pienimmän alkion. Voit olettaa, että pienin alkio esiintyy listassa vain kerran.

Funktio ei siis palauta mitään, vaan muokkaa parametrinaan saamaansa listaa!

Esimerkki funktion kutsumisesta:

```python
if __name__ == "__main__":
    luvut = [2, 4, 6, 1, 3, 5]
    poista_pienin(luvut)
    print(luvut)
```
<sample-output>

[2, 4, 6, 3, 5]

</sample-output>

</programming-exercise>


<programming-exercise name='Sudoku: ruudukon tulostus ja luvun lisäys' tmcname='osa05-07_sudoku_osa5'>

Tässä tehtävässä toteutetaan vielä kaksi funktiota sudokua varten: `tulosta` ja `lisays`.

Funktio `tulosta` saa parametriksi sudokuruudukkoa esittävän kaksiulotteisen listan ja tulostaa sen alla olevan esimerkkitulostuksen mukaisessa muodossa.

Funktio `lisays(sudoku: list, rivi_nro: int, sarake_nro: int, luku:int)` saa parametriksi sudokuruudukkoa esittävän kaksiulotteisen listan, rivi- ja sarakenumerot sekä luvun väliltä 1–9. Funktio lisää luvun parametrien ilmoittamaan kohtaan sudokuruudukkoa.

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

tulosta(sudoku)
lisays(sudoku, 0, 0, 2)
lisays(sudoku, 1, 2, 7)
lisays(sudoku, 5, 7, 3)
print()
print("Kolme numeroa lisätty:")
print()
tulosta(sudoku)
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

Kolme numeroa lisätty:

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

**Vihje**

Saatat tässä tehtävässä hyötyä siitä, että `print`-komentoa on mahdollista käyttää myös siten, että se ei aiheuta rivinvaihtoa:

```python
print("merkkejä ", end="")
print("ilman välejä", end="")
```

<sample-output>

merkkejä ilman välejä

</sample-output>

Joskus taas tarvitaan pelkkää rivinvaihtoa, ja se onnistuu seuraavasti:

```python
print()
```

</programming-exercise>

<programming-exercise name='Sudoku: luvun lisäys ruudukon kopioon' tmcname='osa05-08_sudoku_osa6'>

Viimeisessä sudokua käsittelevässä tehtävässä toteutetaan hieman erilainen versio funktiosta, jonka avulla sudokuruudukkoon lisätään uusia lukuja.

Funktio `kopioi_ja_lisaa(sudoku: list, rivi_nro: int, sarake_nro: int, luku:int)` saa parametreikseen sudokuruudukkoa esittävän kaksiulotteisen listan, rivinumeron, sarakenumeron sekä luvun väliltä 1–9. Funktio _palauttaa_ parametrina saadusta sudokuruudukosta _kopion_, johon on lisätty parametrina saatu luku parametrina saatuun sijaintiin sijoitettuna. Funktio _ei saa muuttaa_ parametrina annettua sudokuruudukkoa.

Seuraavassa on edellisen tehtävän funktiota `tulosta` hyödyntävä käyttöesimerkki:

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

kopio = kopioi_ja_lisaa(sudoku, 0, 0, 2)
print("Alkuperäinen:")
tulosta(sudoku)
print()
print("Kopio:")
tulosta(kopio)
```

<sample-output>

<pre>
Alkuperäinen:
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _
_ _ _  _ _ _  _ _ _

Kopio:
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

**Vihje** tässä tehtävässä pitää olla tarkkana mitä kaikkea tulee kopioida, ja mihin lisäys lopulta kohdistuu. Kuten yleensäkin, [visualisaattori](http://www.pythontutor.com/visualize.html#mode=edit) auttaa myös nyt. Sudokuruudukon koon takia näkymä tosin on hieman normaalia sekavampi.

</programming-exercise>

<programming-exercise name='Ristinolla' tmcname='osa05-09_ristinolla'>

Ristinollaa pelataan 3 x 3 -kokoisella ruudukolla, johon pelaajat merkitsevät vuorotellen ristin tai nollan. Pelin voittaa se pelaaja, joka saa ensimmäisenä kolme merkkiä pystyyn, vaakaan tai kulmittain. Peli päättyy tasapeliin, jos kumpikaan pelaaja ei saa kolmen sarjaa.

Kirjoita funktio `pelaa_siirto(lauta: list, x: int, y: int, nappula: str)`, jossa sijoitetaan annettu pelinappula annettuihin koordinaatteihin pelilaudalla. Koordinaattien arvot ovat väliltä 0..2.

**Huomaa** että tässä tehtävässä parametrit ovat eri päin kuin sudokussa, ensin annetaan saraketta kuvaava `x` ja sen jälkeen riviä kuvaava `y`.

Pelilauta koostuu merkkijonoista seuraavasti:

* `""`: tyhjä ruutu
* `"X"`: pelaajan 1 merkki
* `"O"`: pelaajan 2 merkki

Funktio palauttaa arvon `True`, jos nappula saatiin sijoitettua laudalle (eli jos paikka oli tyhjä), ja arvon `False`, jos paikka oli varattu TAI jos koordinaatin arvo oli liian pieni tai suuri (eli ei väliltä 0..2).

Esimerkiksi:

```python
lauta = [["", "", ""], ["", "", ""], ["", "", ""]]
print(pelaa_siirto(lauta, 2, 0, "X"))
print(lauta)
```

<sample-output>

True
[['', '', 'X'], ['', '', ''], ['', '', '']]

</sample-output>

</programming-exercise>

<programming-exercise name='Matriisin kääntö' tmcname='osa05-10_matriisin_kaanto'>

Kirjoita funktio `transponoi(matriisi: list)`, joka saa parametrikseen kaksiulotteisen kokonaislukuja sisältävän taulukon eli matriisin. Funktio _transponoi_ matriisin eli muuntaa rivit sarakkeiksi ja päinvastoin.

Voit olettaa, että matriisissa on yhtä monta riviä kuin sarakettakin (eli matriisi on _neliömatriisi_).

Esimerkiksi matriisista

```python
1 2 3
4 5 6
7 8 9
```

tulisi transponoinnin jälkeen tällainen:

```python
1 4 7
2 5 8
3 6 9
```

Funktio ei palauta mitään, vaan muokkaa parametrinaan saamaansa matriisia.

</programming-exercise>

## Sidoeffekter hos funktioner

Om en funktion tar emot en referens till en lista som argument, kan funktionen ändra på listan. Om programmeraren inte har tagit i beaktande att listan kan ändras på direkt, kan ändringar i listan förorsaka problem på andra håll i programmet.

Låt oss ta en titt på en funktion som borde hitta det näst minsta värdet i en lista:

```python
def toiseksi_pienin(lista: list) -> int:
    # järjestetyn listan toiseksi pienin alkio on kohdassa 1
    lista.sort()
    return lista[1]

luvut = [1, 4, 2, 5, 3, 6, 4, 7]
print(toiseksi_pienin(luvut))
print(luvut)
```

<sample-output>
2
[1, 2, 3, 4, 4, 5, 6, 7]
</sample-output>

Funktionen hittar det näst minsta värdet, men dessutom ordnar funktionen listan. Om ordningen av elementen har betydelse på andra håll i programmet kommer det här funktionsanropet eventuellt att orsaka fel. Oplanerade modifikationer som görs hos objekt som ges som referens till en funktion kallas sidoeffekt.

Vi kan förhindra den här sidoeffekten genom att göra en liten ändring i funktionen:

```python
def toiseksi_pienin(lista: list) -> int:
    kopio = sorted(lista)
    return kopio[1]

luvut = [1, 4, 2, 5, 3, 6, 4, 7]
print(toiseksi_pienin(luvut))
print(luvut)
```

<sample-output>

2
[1, 4, 2, 5, 3, 6, 4, 7]

</sample-output>

Funktionen `sorted` returnerar en ny ordnad kopia av listan, så vi behöver inte mera ”sabotera” den ursprungliga listan när vi söker efter det näst minsta värdet.

Det är en bra vana att undvika sidoeffekter i funktioner. Sidoeffekter kan göra det svårare att säkerställa att programmet fungerar som det ska i alla situationer.

Funktioner som saknar sidoeffekter kallas rena funktioner. Då man arbetar med funktionell programmering är rena funktioner speciellt viktiga. Vi dyker djupare i det här under fortsättningskursen i programmering.

<quiz id="c978cb03-cb95-52a3-b122-2cc9ddf8a552"></quiz>
