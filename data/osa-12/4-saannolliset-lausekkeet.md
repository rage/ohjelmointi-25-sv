---
path: '/osa-12/4-saannolliset-lausekkeet'
title: 'Reguljära uttryck'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Vet du vad reguljära uttryck är
- Kommer du att kunna använda reguljära uttryck i dina egna program

</text-box>

Vi har redan konstaterat att Python är en utmärkt miljö för att bearbeta text. Ett ytterligare kraftfullt verktyg för textbehandling är reguljära uttryck (eng. regular expressions), ofta förkortat som regex eller regexp. De är ett sätt att välja ut och söka efter strängar som följer ett visst mönster. I det här avsnittet får du en introduktion till grunderna i reguljära uttryck, men du hittar mycket mer information på nätet, bland annat i Pythons egna [handledning](https://docs.python.org/3/howto/regex.html).

## Vad är reguljära uttryck?

Reguljära uttryck är inte bara en Python-funktion. De representerar på sätt och vis ett programmeringsspråk inom ett programmeringsspråk. De är i viss utsträckning kompatibla med många olika programmeringsspråk. Reguljära uttryck har sin egen specifika syntax. Tanken är att definiera en samling strängar som följer vissa regler.

Låt oss börja med ett enkelt exempel innan vi dyker djupare in i syntaxen:

```python
import re

sanat = ["Python", "Ponneton", "Ponttooni", "Pullero", "Pallon"]

for sana in sanat:
    # merkkijonon tulee alkaa "P" ja päättyä "on"
    if re.search("^P.*on$", sana):
        print(sana, "löytyy!")
```

<sample-output>

Python löytyy!
Ponneton löytyy!
Pallon löytyy!

</sample-output>

Vi behöver importera modulen `re` för att kunna använda reguljära uttryck i Python. Modulen `re` innehåller många funktioner för att arbeta med reguljära uttryck. I exemplet ovan tar `search`-funktionen två strängargument: mönstersträngen och den målsträng där mönstret ska sökas.

I det här andra exemplet letar man efter alla siffror i en sträng. Funktionen `findall` returnerar en lista över alla instanser som matchar mönstret:

```python
import re

lause = "Eka, 2 !#kolmas 44 viisi 678xyz962"

luvut = re.findall("\d+", lause)

for luku in luvut:
    print(luku)
```

<sample-output>

2
44
678
962

</sample-output>

## Syntaxen för reguljära uttryck

Låt oss bekanta oss med den grundläggande syntaxen för reguljära uttryck. De flesta av följande exempel använder sig av detta testprogram:

```python
import re

lauseke = input("Anna lauseke: ")

while True:
    mjono = input("Anna merkkijono: ")
    if mjono == "":
        break
    if re.search(lauseke, mjono):
        print("Osuma!")
    else:
        print("Ei osumaa.")
```

### Alternativa delsträngar

Lodstrecket  (eng. vertical bar) `|`, gör att du kan matcha alternativa delsträngar. Dess betydelse är alltså eller. Uttrycket `911|112` matchar t.ex. strängar som innehåller antingen delsträngen `911` eller delsträngen `112`.

Ett exempel med testprogrammet:

<sample-output>

Anna lauseke: **aa|ee|ii**
Anna testijono: **saapas**
Osuma!
Anna testijono: **teema**
Osuma!
Anna testijono: **iilimato**
Osuma!
Anna testijono: **ooppera**
Ei osumaa.
Anna testijono: **uuttera**
Ei osumaa.

</sample-output>


### Grupper av tecken

Hakparenteser används för att beteckna grupper av accepterade tecken. Uttrycket `[aeio]` skulle t.ex. matcha alla strängar som innehåller något av tecknen a, e, i eller o.

Ett bindestreck är också tillåtet för att matcha intervall av tecken. Uttrycket `[0-68a-d]` skulle till exempel matcha alla strängar som innehåller en siffra mellan 0 och 6, eller en åtta, eller ett tecken mellan a och d. I den här notationen är alla intervall inkluderande.

Om du kombinerar två uppsättningar parenteser kan du matcha två tecken i följd. Till exempel skulle uttrycket `[1-3][0-9]` matcha alla tvåsiffriga tal mellan 10 och 39, inklusive.

Ett exempel med testprogrammet:

<sample-output>

Anna lauseke: **[C-FRSÖ]**
Anna testijono: **C**
Osuma!
Anna testijono: **E**
Osuma!
Anna testijono: **G**
Ei osumaa.
Anna testijono: **R**
Osuma!
Anna testijono: **Ö**
Osuma!
Anna testijono: **T**
Ei osumaa.

</sample-output>

### Upprepade matchningar

Varje del av ett uttryck kan upprepas med följande operatorer:

* `*` upprepas hur många gånger som helst, inklusive noll
* `+` upprepas hur många gånger som helst, men minst en gång
* `{m}` upprepas exakt `m` gånger

Dessa operatorer fungerar på den del av uttrycket som kommer omedelbart före operatorn. Uttrycket `ba+b` skulle t.ex. matcha delsträngarna `bab`, `baab` och `baaaaaaaaaaab`, bland andra. Uttrycket `A[BCDE]*Z` skulle matcha delsträngarna `AZ`, `ADZ` eller `ABCDEBCDEBCDEZ`, bland andra.

Ett exempel med testprogrammet:

<sample-output>

Anna lauseke: **1[234]\*5**
Anna testijono: **15**
Osuma!
Anna testijono: **125**
Osuma!
Anna testijono: **145**
Osuma!
Anna testijono: **12342345**
Osuma!
Anna testijono: **126**
Ei osumaa.
Anna testijono: **165**
Ei osumaa.

</sample-output>


### Andra specialtecken

En punkt är ett jokertecken som kan matcha vilket enskilt tecken som helst. Uttrycket `c...o` skulle till exempel matcha alla delsträngar med fem tecken som börjar med ett `c` och slutar med ett `o`, till exempel `c-3po` eller `cello`.

Tecknet `^` anger att matchningen måste ske i början av strängen och `$` anger att matchningen måste ske i slutet av strängen. Dessa tecken kan också användas för att utesluta andra tecken än de angivna från matchningen:

<sample-output>

Anna lauseke: **\^[123]\*$**
Anna testijono: **4**
Ei osumaa.
Anna testijono: **1221**
Osuma!
Anna testijono: **333333333**
Osuma!

</sample-output>

Ibland behöver du matcha för specialtecken som är reserverade för syntaxen för reguljära uttryck. Omvänt snedstreck (eng. backslash) `\` kan användas för att undkomma specialtecken. Uttrycket `1+` matchar alltså ett eller flera tal `1`, men uttrycket `1\+` matchar strängen `1+`.

<sample-output>

Anna lauseke: **^\\\***
Anna testijono: **moi\***
Ei osumaa.
Anna testijono: **m\*o\*i**
Ei osumaa.
Anna testijono: **\*moi**
Osuma!

</sample-output>

Runda parenteser kan användas för att gruppera ihop olika delar av uttrycket. Till exempel skulle uttrycket `(ab)+c` matcha delsträngarna `abc`, `ababc` och `abababababababc`, men inte strängarna `ac` eller `bc`, eftersom hela delsträngen `ab` måste förekomma minst en gång.

<sample-output>

Anna lauseke: **^(jabba).\*(hut)$**
Anna testijono: **jabba the hut**
Osuma!
Anna testijono: **jabba a hut**
Osuma!
Anna testijono: **jarmo the hut**
Ei osumaa.
Anna testijono: **jabba the smut**
Ei osumaa.

</sample-output>

<programming-exercise name='Säännölliset lausekkeet' tmcname='osa12-14_saannolliset_lausekkeet'>

Harjoitellaan hieman säännöllisten lausekkeiden käyttöä.

## Viikonpäivät

Tee säännöllisen lausekkeen avulla funktio `on_viikonpaiva(merkkijono: str)` joka palauttaa `True`, jos sen parametrina saama merkkijono sisältää viikonpäivän lyhenteen (ma, ti, ke, to, pe, la tai su).

Esimerkki funktion kutsumisesta:

```python
print(on_viikonpaiva("ma"))
print(on_viikonpaiva("pe"))
print(on_viikonpaiva("tu"))
```

<sample-output>

True
True
False

</sample-output>

## Vokaalitarkistus

Tee funktio `kaikki_vokaaleja(merkkijono: str)`, joka tarkistaa säännöllisen lausekkeen avulla, ovatko parametrina annetun merkkijonon kaikki merkit vokaaleja.

Esimerkki funktion kutsumisesta:

```python
print(kaikki_vokaaleja("eioueioieoieouyyyy"))
print(kaikki_vokaaleja("autoooo"))
```

<sample-output>

True
False

</sample-output>

## Kellonaika

Tee funktio `kellonaika(merkkijono: str)`, joka tarkistaa säännöllisen lausekkeen avulla, onko parametrina oleva merkkijono muotoa `tt:mm:ss` oleva kellonaika (tunnit, minuutit ja sekunnit kaksinumeroisina).

Esimerkki funktion kutsumisesta:

```python
print(kellonaika("12:43:01"))
print(kellonaika("AB:01:CD"))
print(kellonaika("17:59:59"))
print(kellonaika("33:66:77"))
```

<sample-output>

True
False
True
False

</sample-output>

</programming-exercise>

## Den stora finalen

Som avslutning på denna del av materialet ska vi arbeta lite mer med objekt och klasser genom att bygga ett lite mer omfattande program. Denna övning innefattar inte nödvändigtvis reguljära uttryck, men avsnitten om [Funktioner som argument ](/osa-12/1-funktio-parametrina) och [list comprehension](/osa-11/1-koosteet) kommer sannolikt att vara användbara.

Du kan också ha nytta av de exempel som finns i [del 10](/osa-10/4-lisaa-esimerkkeja).

<programming-exercise name='Tilastot ojennukseen' tmcname='osa12-15_tilastot_ojennukseen'>

Tässä tehtävässä tehdään sovellus, jonka avulla on mahdollista tarkastella NHL-jääkiekkoliigan tilastoja muutamassa hieman erilaisessa muodossa.

Tehtäväpohjan mukana tulee kaksi json-muodossa olevaa tiedostoa `osa.json` ja `kaikki.json`, näistä ensimmäinen on tarkoitettu lähinnä testailun avuksi. Jälkimmäinen sisältää kaikkien kaudella 2019-20 pelanneiden pelaajien statistiikat.

Yksittäisen pelaajan tiedot ovat muodossa

```json
{
    "name": "Patrik Laine",
    "nationality": "FIN",
    "assists": 35,
    "goals": 28,
    "penalties": 22,
    "team": "WPG",
    "games": 68
},
```

ja molemmat tiedostoista sisältävät yksittäisten pelaajien tiedot taulukossa.

Jos et muista, miten json-muotoinen tiedosto saadaan luettua Python-ohjelmaan, voit kerrata tämän [osan 7 materiaalista](/osa-7/4-datan-kasittely#json-tiedoston-lukeminen).

Tee nyt ohjelma, joka kysyy aluksi tiedoston nimeä ja tarjoaa sitten seuraavat toiminnot:

- yksittäisen pelaajan tietojen haku nimen perusteella
- listaus joukkueiden nimien lyhenteistä (aakkosjärjestyksessä)
- listaus maiden nimien lyhenteistä (aakkosjärjestyksessä)

Näistä toiminnoista saa yhden pisteen. Ohjelman tulee toimia seuraavasti:

<sample-output>

tiedosto: **osa.json**
luettiin 14 pelaajan tiedot

komennot:
0 lopeta
1 hae pelaaja
2 joukkueet
3 maat
4 joukkueen pelaajat
5 maan pelaajat
6 eniten pisteitä
7 eniten maaleja

komento: **1**
nimi: **Travis Zajac**
<pre>
Travis Zajac         NJD   9 + 16 =  25
</pre>

komento: **2**
BUF
CGY
DAL
NJD
NYI
OTT
PIT
WPG
WSH

komento: **3**
CAN
CHE
CZE
SWE
USA

komento: **0**

</sample-output>

Huomaa, että pelaajien tulostusasun pitää olla täsmälleen seuraavanlainen:

<sample-output>

<pre>
Leon Draisaitl       EDM  43 + 67 = 110
Connor McDavid       EDM  34 + 63 =  97
Travis Zajac         NJD   9 + 16 =  25
Mike Green           EDM   3 +  8 =  11
Markus Granlund      EDM   3 +  1 =   4
123456789012345678901234567890123456789
</pre>

</sample-output>

Alimman rivin numerot on lisätty helpottamaan oikean merkkimäärän laskemista. Joukkueen nimen lyhenne siis tulostetaan alkaen rivin 22. merkistä. Plus on rivin 30. merkki ja = rivin 35. merkki. Kaikki luvut tulee tasata oikeaan reunaan omaa tulostusaluettaan. Tyhjät kohdat ovat välilyöntejä.

Tulostuksen muotoilu kannattaa hoitaa f-merkkijonoina samaan tapaan kuin [tässä](/osa-6/1-tiedostojen-lukeminen#programming-exercise-kurssin-tulokset-osa-3) osan 6 tehtävässä.

Seuraavat toiminnot tuovat toisen pisteen:

- joukkueen pelaajien listaaminen pisteiden (joka saadaan laskemalla _goals_ + _assits_) mukaisessa järjestyksessä
- tietyn maan pelaajien listaaminen pisteiden mukaisessa järjestyksessä

Toiminnallisuus on seuraava:

<sample-output>

tiedosto: **osa.json**
luettiin 14 pelaajan tiedot

komennot:
0 lopeta
1 hae pelaaja
2 joukkueet
3 maat
4 joukkueen pelaajat
5 maan pelaajat
6 eniten pisteitä
7 eniten maaleja

komento: **4**
joukkue: **OTT**
<pre>
Drake Batherson      OTT   3 +  7 =  10
Jonathan Davidsson   OTT   0 +  1 =   1
</pre>

komento: **5**
maa: **CAN**
<pre>
Jared McCann         PIT  14 + 21 =  35
Travis Zajac         NJD   9 + 16 =  25
Taylor Fedun         DAL   2 +  7 =   9
Mark Jankowski       CGY   5 +  2 =   7
Logan Shaw           WPG   3 +  2 =   5
</pre>

komento: **0**

</sample-output>

Kolmannen pisteen saa seuraavilla toiminnoilla:

- n eniten pistettä saanutta pelaajaa
  - jos kahden pelaajan pistemäärä on sama, ratkaisee maalimäärä
- n eniten maaleja (_goals_) tehnyttä pelaajaa
  - jos kahden pelaajan maalimäärä on sama, järjestyksen ratkaisee se kummalla on vähemmän otteluja (_games_)

Toiminnallisuus on seuraava:

<sample-output>

tiedosto: **osa.json**
luettiin 14 pelaajan tiedot

komennot:
0 lopeta
1 hae pelaaja
2 joukkueet
3 maat
4 joukkueen pelaajat
5 maan pelaajat
6 eniten pisteitä
7 eniten maaleja

komento: **6**
kuinka monta: **2**
<pre>
Jakub Vrana          WSH  25 + 27 =  52
Jared McCann         PIT  14 + 21 =  35
</pre>

komento: **6**
kuinka monta: **5**

<pre>
Jakub Vrana          WSH  25 + 27 =  52
Jared McCann         PIT  14 + 21 =  35
John Klingberg       DAL   6 + 26 =  32
Travis Zajac         NJD   9 + 16 =  25
Conor Sheary         BUF  10 + 13 =  23
</pre>

komento: **7**
kuinka monta: **6**

<pre>
Jakub Vrana          WSH  25 + 27 =  52
Jared McCann         PIT  14 + 21 =  35
Conor Sheary         BUF  10 + 13 =  23
Travis Zajac         NJD   9 + 16 =  25
John Klingberg       DAL   6 + 26 =  32
Mark Jankowski       CGY   5 +  2 =   7
</pre>

komento: **0**

</sample-output>

</programming-exercise>

Vastaa lopuksi osion loppukyselyyn:

<quiz id="2249a8d3-9455-5228-bd15-d5328d147b19"></quiz>
