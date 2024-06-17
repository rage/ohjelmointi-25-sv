---
path: '/osa-4/6-lisaa-rakenteista'
title: 'Mera strängar och listor'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* kommer du att vara bekant med flera metoder för att extrahera delar av strängar och listor
* förstår du vad oföränderlighet hos strängar innebär
* kan du använda dig av metoderna `count` och `replace`.

</text-box>

Du är redan bekant med syntaxen `[]` för att ta fram en delsträng:

```python
strang = "exempel"
print(strang[3:7])
```

<sample-output>

mpel

</sample-output>

Samma syntax fungerar med listor. Dellistor kan extraheras på samma sätt som delsträngar:

```python
lista = [3,4,2,4,6,1,2,4,2]
print(lista[3:7])
```

<sample-output>

[4, 6, 1, 2]

</sample-output>

## Mera extrahering

Syntaxen `[]` fungerar faktiskt mycket lika som `range`-funktionen, vilket innebär att vi också kan ge den ett steg:

```python
strang = "exempel"
print(strang[0:7:2])
lista = [1,2,3,4,5,6,7,8]
print(lista[6:2:-1])
```

<sample-output>

eepl
[7, 6, 5, 4]

</sample-output>

Om vi lämnar bort något av indexen kommer operatorn att inkludera alla element. Tack vare detta kan vi till exempel skriva ett mycket kort program som vänder om en sträng:

```python
strang = input("Ange en sträng: ")
print(strang[::-1])
```

<sample-output>

Ange en sträng: **exempel**
lepmexe

</sample-output>

<!--vastaava varoitusteksti löytyy osioista 3-4, 4-6 ja 5-1, tsekkaa kaikki jos muokkaat-->
## Varoitus: globaalin muuttujan käyttö funktion sisällä

Funktioiden sisällä on mahdollista määritellä muuttujia, mutta tämän lisäksi funktio näkee sen ulkopuolella pääohjelmassa määritellyt muuttujat. Tälläisia muuttujia sanotaan _globaaleiksi_ muuttujiksi.

Globaalien muuttujien käyttämistä funktioista käsin ei useimmiten pidetä hyvänä asiana muun muassa siksi, että ne saattavat johtaa ikäviin bugeihin.

Seuraavassa on esimerkki funktiosta, joka käyttää "vahingossa" globaalia muuttujaa:

```python
def tulosta_vaarinpain(nimet: list):
    # käytetään vahingossa parametrin sijaan globaalia muuttujaa nimilista
    i = len(nimilista) - 1
    while i >= 0:
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

Kaikki funktioita testaava koodi on kirjoitettava erillisen lohkon sisälle, jotta TMC-testit hyväksyisivät koodin. Edellinen esimerkki siis tulisi toteuttaa seuraavasti:

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

TMC-testit suoritetaan aina siten, että mitään `if`-lohkon sisällä olevaa koodia ei suoriteta. Tämän takia funktio ei voi edes teoriassa toimia, sillä se viittaa muuttujaan `nimilista`, jota ei testejä suoritettaessa ole lainkaan olemassa.

<programming-exercise name='Allt omvänt' tmcname='osa04-21_kaikki_vaarinpain'>

Skapa funktionen `allt_omvant` som får som argument en lista med strängar. Funktionen ska skapa och returnera en ny lista där alla strängar i den ursprungliga listan är omvända. Elementen ska också komma i omvänd ordning i listan.

Exempel:

```python
lista = ["Hej", "alla", "exempel", "ett till"]
lista2 = allt_omvant(lista)
print(lista2)
```

<sample-output>

['llit tte', 'lepmexe', 'alla', 'jeH']

</sample-output>

</programming-exercise>

## Strängar är oföränderliga

Strängar och listor har en hel del likheter, framför allt då det kommer till hur de fungerar med olika operatorer. En nyckelskillnad är att strängar är oföränderliga. Det betyder att de inte kan ändras.

```python
strang = "exempel"
strang[0] = "a"
```

Strängar kan inte ändras på, så det här programmet kommer att ge ett felmeddelande:

<sample-output>

TypeError: 'str' object does not support item assignment

</sample-output>

Ett liknande fel uppstår om du försöker ordna en sträng med `sort`-metoden.

Strängar är oföränderliga, men variablerna som lagrar dem är inte det. En sträng kan ersättas med en annan sträng.

De följande exemplen är alltså till sin grund olika:

```python
lista = [1,2,3]
lista[0] = 10
```

<img src="4_4_1.png">

```python
strang = "Hej"
strang = strang + "!"
```

<img src="4_4_2.png">

Det första exemplet ändrar på innehållet i den lista som man hänvisar till. I det andra exemplet ersätts hänvisningen till den ursprungliga strängen med en hänvisning till en ny sträng. Den ursprungliga strängen finns fortfarande någonstans i datorns minne, men det saknas en referens till strängen så den kan inte längre användas i programmet.

Vi återkommer till det här ämnet senare. Då utforskar vi hänvisningar till listor närmare.

## Mera metoder hos listor och strängar

Metoden `count` räknar antalet gånger ett element eller en delsträng finns i en lista eller sträng:

```python
strang = "Hon håsa på hussatimmen så lärar'n sa sakta: städa upp mjölet på golvet så att klassen int' e som en savann"
print(strang.count("sa"))

lista = [1,2,3,1,4,5,1,6]
print(lista.count(1))
```

<sample-output>

5
3

</sample-output>

Metoden räknar inte överlappande förekomster. Till exempel i strängen `aaaa` räknar metoden upp till två förekomster av delsträngen `aa`, även om det finns tre stycken om överlappande förekomster skulle tillåtas.

Metoden `replace` skapar en ny sträng där en specifik delsträng har ersatts med en annan sträng:

```python
strang = "Hej alla"
uusi = strang.replace("Hej", "God eftermiddag")
print(uusi)
```

<sample-output>

God eftermiddag alla

</sample-output>

Metoden påverkar alla delsträngar som hittas:

```python
lause = "de åtta potatissemlorna förvandlades till en stor potatisplåt i ugnen – läraren, ja hon suckade i sitt hörn av klassen"
print(lause.replace("en", "EN"))
```

<sample-output>

de åtta potatissemlorna förvandlades till EN stor potatisplåt i ugnEN – lärarEN, ja hon suckade i sitt hörn av klassEN

</sample-output>

När `replace`-metoden används, är ett vanligt misstag att man glömmer att strängar är oföränderliga:

```python
strang = "Jag gillar Python"

# vi ersätter en delsträng, men resultatet lagras ingenstans
strang.replace("Python", "Java")
print(strang)
```

<sample-output>

Jag gillar Python

</sample-output>

Om den gamla strängen inte längre behövs kan man tilldela den nya strängen till samma variabel:

```python
strang = "Jag gillar Python"

# vi ersätter en delsträng och lagrar resultatet
strang = strang.replace("Python", "Java")
print(strang)
```

<sample-output>

Jag gillar Java

</sample-output>

<programming-exercise name='Vanligaste bokstaven' tmcname='osa04-22_eniten_kirjaimia'>

Skapa funktionen `vanligaste_bokstaven` som får som argument en sträng. Funktionen ska returnera den bokstav som förekommer mest i strängen. Om det finns flera kandidater ska man returnera den bokstav som förekommer först.

Exempel:

```python
strang = "abba"
print(vanligaste_bokstaven(strang))

strang2 = "jästsurdegmedsaltosocker"
print(vanligaste_bokstaven(strang2))
```

<sample-output>

a
s

</sample-output>

</programming-exercise>


<programming-exercise name='Utan vokaler' tmcname='osa04-23_vokaalit_pois'>

Skapa funktionen `utan_vokaler` som får som argument en sträng. Funktionen ska returnera en ny sträng där vokalerna i den ursprungliga strängen fattas.

Du kan anta att strängen består av gemener i intervallet `a-ö`.

Exempel:

```python
strang = "det här är ett exempel"
print(ilman_vokaaleja(strang))
```

<sample-output>

dt hr r tt xmpl

</sample-output>

</programming-exercise>


<programming-exercise name='Versaler bort' tmcname='osa04-24_poista_isot'>

Pythons strängmetod `isupper()` returnerar `True` om strängen består av enbart versaler.

Exempel:

```python
print("XYZ".isupper())

bara_stora = "Abc".isupper()
print(bara_stora)
```

<sample-output>

True
False

</sample-output>

Skapa funktionen `versaler_bort` som tar emot som argument en lista med strängar. Funktionen ska returnera en ny lista med de strängar som inte består av enbart versaler.

Exempel:

```python
lista = ["ABC", "def", "STOR", "ANNANSTOR", "liten", "annan liten", "Delvis stoR"]
filtrerad_lista = versaler_bort(lista)
print(filtrerad_lista)
```

<sample-output>

['def', 'liten', 'annan liten', 'Delvis stoR']

</sample-output>

</programming-exercise>

<programming-exercise name='Grannar i en lista' tmcname='osa04-25_naapureita_listassa'>

Vi definierar att två element i en lista är grannar då skillnaden mellan deras värden är ett. Dvs. t.ex. elementen `1` och `2` samt `56` och `55`.

Skapa funktionen `langsta_grannstrackan` som letar efter den längsta dellistan bestående av bredvidliggande grannar. Listans längd ska returneras.

T.ex. i listan `[1, 2, 5, 4, 3, 4]` skulle dellistan vara `[5, 4, 3, 4]` och längden som returneras därmed `4`.

Exempel:

```python
lista = [1, 2, 5, 7, 6, 5, 6, 3, 4, 1, 0]
print(langsta_grannstrackan(lista))
```

<sample-output>

4

</sample-output>

</programming-exercise>

## Skapa ett större programmeringsprojekt

Den här fjärde modulen avslutas med ett lite större programmeringsprojekt där du får utnyttja det du lärt dig hittills.

Den viktigaste regeln när man börjar med ett programmeringsprojekt är att man inte ska försöka lösa alla problem samtidigt. Programmet ska bestå av mindre delar, till exempel hjälpfunktioner. Du ska testa att varje del fungerar före du fortsätter framåt. Om du försöker göra för mycket samtidigt kommer du högst antagligen hamna i en situation som präglas av kaos och mera kaos.

Du kommer att behöva ett sätt att testa dina funktioner utanför huvudfunktionen. Du kan uppnå det här genom att definiera en skild huvudfunktion som du anropar utanför alla andra funktioner i programmet. Det är enkelt att tillfälligt kommentera bort ett funktionsanrop när man testar programmet. De första stegen i utförandet av programmeringsprojektet skulle kunna se ut så här:

```python
def main():
    poang = []
    # programmets kod hit

main()
```

Nu kan hjälpfunktionerna köras utan att huvudfunktionen körs:

```python
# hjälpfunktion som räknar vitsord baserat på givet poängantal
def vitsord(poang):
    # koo

def main():
    poang = []
    # programmets kod hit

# kommenterar huvudprogrammet bort
#main()

# testar hjälpfunktionen
poang = 35
resultat = vitsord(poang)
print(resultat)
```

## Skicka data från en funktion till en annan

När ett program innehåller flera funktioner uppstår en fråga: hur skickar jag data från en funktion till en annan?

I följande exempel frågar man efter några heltal från användaren. Programmet skriver sedan ut dessa värden och utför en "analys" på dem. Programmet är uppdelat i tre skilda funktioner:

```python
def las_fran_anvandare(antal: int):
    print(f"Ange {antal} tal:")
    siffror = []

    for i in range(antal):
        siffra = int(input("Ange tal: "))
        siffror.append(siffra)

    return siffror

def skriv_ut(siffror: list):
    print("Talen är: ")
    for siffra in siffror:
        print(siffra)

def analysera(siffror: list):
    medeltal = sum(siffror) / len(siffror)
    return f"Siffror tillsammans {len(siffror)}, medeltal {medeltal}, minsta {min(siffror)} och största {max(siffror)}"

# "huvudprogram" som använder funktionerna
indata = las_fran_anvandare(5)
skriv_ut(indata)
analysens_resultat = analysera(indata)
print(analysens_resultat)
```

När programmet körs, skulle det kunna se ut så här:

<sample-output>

Ange 5 tal:
Ange tal: **10**
Ange tal: **34**
Ange tal: **-32**
Ange tal: **99**
Ange tal: **-53**
Talen är:
10
34
-32
99
-53
Siffror tillsammans 5, medeltal 11.6, minsta -53 och största 99

</sample-output>

Idén är att huvudfunktionen "lagrar" all data som behandlas av programmet. I det här fallet är det enda som vi behöver de värden som användaren gett, i variabeln `siffror`.

Om det här behövs i en funktion ges det som ett argument. Det här sker med funktionerna `skriv_ut_resultat` och `analysera`. Om funktionen resulterar i data som behövs på annat håll i programmet, returnerar funktionen det. Det här sparas i en variabel i huvudfunktionen. Det här sker med funktionerna `indata_fran_anvandare` och `analysera`.

Du kunde använda den globala variabeln siffror från huvudfunktionen direkt i hjälpfunktionerna. Vi har redan gått igenom varför det är en dålig idé, men här följer ännu en annan förklaring. Om funktionerna kan ändra på den globala variabeln kan oförutsedda saker börja hända i programmet, framför allt då antalet funktioner ökar.

Att skicka data ut och in från funktioner gör man alltså helst med hjälp av argument och return-värden.

Du kunde också göra huvudfunktionen till sin egen funktion. Då skulle variabeln siffor inte längre vara en global variabel, utan en lokal variabel i `main`-funktionen:

```python
# funktion som representerar huvudfunktionen
def main():
    indata = las_fran_anvandare(5)
    skriv_ut(indata)
    analysens_resultat = analysera(indata)

    print(analysens_resultat)

# start av programmet
main()
```

<programming-exercise name='Vitsordsstatistik' tmcname='osa04-26_arvosanatilasto'>

I den här uppgiften skapar vi ett program vars uppgift är att skriva ut vitsordsstatistik för en kurs.

Till programmet ger man rader med information om en studerandes provpoäng samt antalet gjorda uppgifter under kursen. Programmet skriver ut statistik på basis av dessa uppgifter.

Provpoängen är heltal mellan noll och 20. Antalet gjorda uppgifter under kursen är ett heltal mellan noll och 100.

Programmet ber om indata från användaren, tills hon matar in en tom rad. Du kan anta att alla rader är korrekt inmatade – de innehåller alltså antingen två heltal eller är tomma.

Så här anger man provpoängen och antalet gjorda uppgifter under kursen:

<sample-output>

Provpoäng samt antalet gjorda uppgifter under kursen: **15 87**
Provpoäng samt antalet gjorda uppgifter under kursen: **10 55**
Provpoäng samt antalet gjorda uppgifter under kursen: **11 40**
Provpoäng samt antalet gjorda uppgifter under kursen: **4 17**
Provpoäng samt antalet gjorda uppgifter under kursen:
Statistik:

</sample-output>

När användaren matat in en tom rad ska programmet skriva ut statistik.

Statistiken består av de följande:

Uppgiftspoäng: Ett poäng för 10 % gjorda uppgifter. Detta går ända upp till 100 % (100 uppgifter) --> 10 poäng. Uppgiftspoängen är ett heltal.

Kursvitsord: Räknas på basis av prov- och uppgiftspoängens summa, se följande tabell.

Provpoäng + uppgiftspoäng | Vitsord
:------------------------:|:-------:
0–14                      | 0 (underkänt)
15–17                     | 1
18–20                     | 2
21–23                     | 3
24–27                     | 4
28–30                     | 5

Om provpoängen är under 10, kommer vitsordet dock alltid att vara 0, underkänt.

Följande statistik skrivs ut med indatan från exemplet ovan:

<sample-output>

<pre>
Statistik:
Poängmedeltal: 14.5
Godkända (%): 75.0
Vitsordsfördelning:
  5:
  4:
  3: *
  2:
  1: **
  0: *
</pre>

</sample-output>

Decimaltal ska skrivas ut med en decimal.

Obs! I dessa uppgifter ska du inte placera kod i `if __name__ == "__main__"` -blocket, om du inte ombeds göra det. Om programmets funktionalitet t.ex. finns i funktionen `main`, ska funktionen anropas utanför det nämnda if-blocket.

Tips: Indatan ges som rader som består av två siffror i följande format.

<sample-output>

Provpoäng samt antalet gjorda uppgifter under kursen: **15 87**

</sample-output>

Raden som matas in ska först delas i två, varefter delarna ska konverteras till heltal med `int`-funktionen. Du kan dela en rad på samma sätt som i den här uppgiften. Du kan också använda strängmetoden `split`. Du kan söka efter `python string split` på nätet för mera information.

<!-- **Huomaa** että tällä hetkellä Windowsissa on ongelmia joidenkin tehtävien testien suorittamisessa. Jos törmäät seuraavaan virheilmoitukseen

<img src="4_3_2.png" alt="Listan iterointi">

voit suorittaa testit lähettämällä ne palvelimelle valitsemalla testien suoritusnapin oikealla puolella olevasta symbolista avautuvasta TMC-valikosta _Submit solutions_.

Ongelman saa korjattua menemällä laajennuksen asennusvalikkoon ja muuttamalla "TMC Data" -kohdassa tehtävien sijainnin johonkin toiseen sijaintiin, jonka tiedostopolku on lyhempi, allaolevassa kuvassa nappi _change path_. Siirrossa saattaa kestää hetken, joten odotathan operaation päättymistä.

<img src="4_3_3.png" alt="Listan iterointi">

Ongelmaan pyritään saamaan parempi ratkaisu lähipäivinä. -->

</programming-exercise>

<quiz id="00a23e8f-ecc1-59b7-bd22-a78c4c3e2d4b"></quiz>

Vänligen svara på en kort enkät om den här veckans material.

<quiz id="a0b1296c-99b2-5bed-accc-2872ad2f59b6"></quiz>
