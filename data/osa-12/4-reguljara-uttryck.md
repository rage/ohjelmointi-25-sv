---
path: '/osa-12/4-reguljara-uttryck'
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

orden = ["Python", "Population", "Pantomi", "Perfekt", "Prestation"]

for ord in orden:
    # Ifall strängen börjar med "P" och slutar med "on"
    if re.search("^P.*on$", ord):
        print(ord, "hittad!")
```

<sample-output>

Python hittad!
Population hittad!
Prestation hittad!

</sample-output>

Vi behöver importera modulen `re` för att kunna använda reguljära uttryck i Python. Modulen `re` innehåller många funktioner för att arbeta med reguljära uttryck. I exemplet ovan tar `search`-funktionen två strängargument: mönstersträngen och den målsträng där mönstret ska sökas.

I det här andra exemplet letar man efter alla siffror i en sträng. Funktionen `findall` returnerar en lista över alla instanser som matchar mönstret:

```python
import re

mening = "Först, 2 !#tredje 44 fem 678xyz962"

numren = re.findall("\d+", mening)

for nummer in numren:
    print(nummer)
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

uttryck = input("Ange uttryck: ")

while True:
    strang = input("Ange sträng: ")
    if strang == "":
        break
    if re.search(uttryck, strang):
        print("Hittad!")
    else:
        print("Hittades inte.")
```

### Alternativa delsträngar

Lodstrecket (eng. vertical bar) `|`, gör att du kan matcha alternativa delsträngar. Dess betydelse är alltså eller. Uttrycket `911|112` matchar t.ex. strängar som innehåller antingen delsträngen `911` eller delsträngen `112`.

Ett exempel med testprogrammet:

<sample-output>

Ange uttryck: **aa|ee|ii**
Ange sträng: **kassaaparat**
Hittad!
Ange sträng: **beteende**
Hittad!
Ange sträng: **friidrott**
Hittad!
Ange sträng: **kooperation**
Hittades inte.
Ange sträng: **bastuugn**
Hittades inte.

</sample-output>


### Grupper av tecken

Hakparenteser används för att beteckna grupper av accepterade tecken. Uttrycket `[aeio]` skulle t.ex. matcha alla strängar som innehåller något av tecknen a, e, i eller o.

Ett bindestreck är också tillåtet för att matcha intervall av tecken. Uttrycket `[0-68a-d]` skulle till exempel matcha alla strängar som innehåller en siffra mellan 0 och 6, eller en åtta, eller ett tecken mellan a och d. I den här notationen är alla intervall inkluderande.

Om du kombinerar två uppsättningar parenteser kan du matcha två tecken i följd. Till exempel skulle uttrycket `[1-3][0-9]` matcha alla tvåsiffriga tal mellan 10 och 39, inklusive.

Ett exempel med testprogrammet:

<sample-output>

Ange uttryck: **[C-FRSÖ]**
Ange sträng: **C**
Hittad!
Ange sträng: **E**
Hittad!
Ange sträng: **G**
Hittades inte.
Ange sträng: **R**
Hittad!
Ange sträng: **Ö**
Hittad!
Ange sträng: **T**
Hittades inte.

</sample-output>

### Upprepade matchningar

Varje del av ett uttryck kan upprepas med följande operatorer:

* `*` upprepas hur många gånger som helst, inklusive noll
* `+` upprepas hur många gånger som helst, men minst en gång
* `{m}` upprepas exakt `m` gånger

Dessa operatorer fungerar på den del av uttrycket som kommer omedelbart före operatorn. Uttrycket `ba+b` skulle t.ex. matcha delsträngarna `bab`, `baab` och `baaaaaaaaaaab`, bland andra. Uttrycket `A[BCDE]*Z` skulle matcha delsträngarna `AZ`, `ADZ` eller `ABCDEBCDEBCDEZ`, bland andra.

Ett exempel med testprogrammet:

<sample-output>

Ange uttryck: **1[234]\*5**
Ange sträng: **15**
Hittad!
Ange sträng: **125**
Hittad!
Ange sträng: **145**
Hittad!
Ange sträng: **12342345**
Hittad!
Ange sträng: **126**
Hittades inte.
Ange sträng: **165**
Hittades inte.

</sample-output>


### Andra specialtecken

En punkt är ett jokertecken som kan matcha vilket enskilt tecken som helst. Uttrycket `c...o` skulle till exempel matcha alla delsträngar med fem tecken som börjar med ett `c` och slutar med ett `o`, till exempel `c-3po` eller `cello`.

Tecknet `^` anger att matchningen måste ske i början av strängen och `$` anger att matchningen måste ske i slutet av strängen. Dessa tecken kan också användas för att utesluta andra tecken än de angivna från matchningen:

<sample-output>

Ange uttryck: **\^[123]\*$**
Ange sträng: **4**
Hittades inte.
Ange sträng: **1221**
Hittad!
Ange sträng: **333333333**
Hittad!

</sample-output>

Ibland behöver du matcha för specialtecken som är reserverade för syntaxen för reguljära uttryck. Omvänt snedstreck (eng. backslash) `\` kan användas för att undkomma specialtecken. Uttrycket `1+` matchar alltså ett eller flera tal `1`, men uttrycket `1\+` matchar strängen `1+`.

<sample-output>

Ange uttryck: **^\\\***
Ange sträng: **hej\***
Hittades inte.
Ange sträng: **h\*e\*j**
Hittades inte.
Ange sträng: **\*hej**
Hittad!

</sample-output>

Runda parenteser kan användas för att gruppera ihop olika delar av uttrycket. Till exempel skulle uttrycket `(ab)+c` matcha delsträngarna `abc`, `ababc` och `abababababababc`, men inte strängarna `ac` eller `bc`, eftersom hela delsträngen `ab` måste förekomma minst en gång.

<sample-output>

Ange uttryck: **^(jabba).\*(hut)$**
Ange sträng: **jabba the hut**
Hittad!
Ange sträng: **jabba a hut**
Hittad!
Ange sträng: **jarmo the hut**
Hittades inte.
Ange sträng: **jabba the smut**
Hittades inte.

</sample-output>

<programming-exercise name='Reguljära uttryck' tmcname='osa12-14_reguljara_uttryck'>

Här följer några övningar för att bekanta dig med syntaxen för reguljära uttryck.

## Veckodagar

Använd ett reguljärt uttryck för att skapa en funktion med namnet `ar_veckodag(strang: str)`. Funktionen ska returnera `True` om strängen som skickas som argument innehåller en förkortning av en veckodag (mån, tis, ons, tors, fre, lör, sön).

Exempel på hur funktionen ska fungera

```python
print(ar_veckodag("mån"))
print(ar_veckodag("fre"))
print(ar_veckodag("turs"))
```

<sample-output>

True
True
False

</sample-output>

## Vokalcheck

Skapa en funktion med namnet `alla_vokaler(strang: str)` som använder ett reguljärt uttryck för att kontrollera om alla tecken i den givna strängen är vokaler.

Exempel på hur funktionen ska fungera:

```python
print(alla_vokaler("eioueioieoieouyyyy"))
print(alla_vokaler("biiiiil"))
```

<sample-output>

True
False

</sample-output>

## Klockans tid

Skapa funktionen `klocktid(strang: str)`, som använder ett reguljärt uttryck för att granska ifall en sträng av formatet `tt:mm:ss` är en giltig tid i ett 24-timmars format, med två siffror var för timmar, minuter och sekunder.

Exempel på hur funktionen ska fungera:

```python
print(klocktid("12:43:01"))
print(klocktid("AB:01:CD"))
print(klocktid("17:59:59"))
print(klocktid("33:66:77"))
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

Du kan också ha nytta av de exempel som finns i [modul 10](/osa-10/4-lisaa-esimerkkeja).

<programming-exercise name='Statistik i ordning' tmcname='osa12-15_statistik_i_ordning'>

I den här övningen kommer du att bygga en applikation för att undersöka hockeyligastatistik från NHL på ett par olika sätt.

Övningsmallen innehåller två JSON-filer: del.json och alla.json. Den första av dessa är mest avsedd för testning. Den senare innehåller en hel del data, eftersom all NHL-spelarstatistik för säsongen 2019-20 ingår i filen.

Inlägget för en enskild spelare är i följande format:

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

Båda filerna innehållar en lista av inlägg enligt ovanstående format.

Ifall du behöver en uppfriskare när det gäller hantering av JOSN-filer, kan du ta en titt på [modul 7 i kursmaterialet](/osa-7/4-datan-kasittely#json-tiedoston-lukeminen).

## Sök och lista

Skapa en interaktiv applikation som först frågar efter namnet på filen och sedan erbjuder följande funktioner:

- sök enligt namn för en enskild spelares statistik
- lista alla förkortningar för lagnamn i alfabetisk ordning
- lista alla förkortningar för länder i alfabetisk ordning

Dessa funktioner ger dig totalt ett övningspoäng. Din applikation ska nu fungera enligt följande:

<sample-output>

fil: **del.json**
läste 14 spelares data

instruktioner:
0 avsluta
1 sök spelare
2 lag
3 länder
4 lagets spelare
5 landets spelare
6 flest poäng
7 flest mål

instruktion: **1**
namn: **Travis Zajac**
<pre>
Travis Zajac         NJD   9 + 16 =  25
</pre>

instruktion: **2**
BUF
CGY
DAL
NJD
NYI
OTT
PIT
WPG
WSH

instruktion: **3**
CAN
CHE
CZE
SWE
USA

instruktion: **0**

</sample-output>

Obs: Utskriftens format för en spelare måste vara exakt enligt följande:

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

Den sista raden i exemplet ovan är till för att hjälpa dig att beräkna bredden på de olika fälten i utskriften; du ska inte skriva ut nummerraden själv i din slutliga inlämning.

Förkortningen för teamet skrivs ut från det 22:a tecknet och framåt. `+`-tecknet är det 30:e tecknet och `=`-tecknet är det 35:e tecknet. Alla fält ska vara justifierade till högerkanten. Alla blanksteg är mellanslagstecken.

F-strängar är förmodligen det enklaste sättet att uppnå den önskade utskriften. Processen är liknande som [denna övning](/osa-6/1-tiedostojen-lukeminen#programming-exercise-kurssin-tulokset-osa-3) från modul 6.

## Lista spelare enligt poäng

Följande funktionalitet ger dig ditt andra övningspoäng:

- lista spelare i ett specifikt lag enligt ordningen flest poäng, från högst till lägst. Poäng är mängden _mål_ + _assistanser_
- lista spelare från ett specifikt land enligt ordningen flest poäng, från högst till lägst

Din applikation ska nu fungera enligt följande:

<sample-output>

fil: **del.json**
läste 14 spelares data

instruktioner:
0 avsluta
1 sök spelare
2 lag
3 länder
4 lagets spelare
5 landets spelare
6 flest poäng
7 flest mål

instruktion: **4**
lag: **OTT**
<pre>
Drake Batherson      OTT   3 +  7 =  10
Jonathan Davidsson   OTT   0 +  1 =   1
</pre>

instruktion: **5**
land: **CAN**
<pre>
Jared McCann         PIT  14 + 21 =  35
Travis Zajac         NJD   9 + 16 =  25
Taylor Fedun         DAL   2 +  7 =   9
Mark Jankowski       CGY   5 +  2 =   7
Logan Shaw           WPG   3 +  2 =   5
</pre>

instruktion: **0**

</sample-output>

## Mest framgångsrika spelare

Det tredje övningspoänget får du från följande två funktionaliteter:

- lista av `n` mängd spelare som fått flest poäng
  - ifall två spelare har samma mängd poäng, ska den som har flera mål komma först
- lista av `n` mängd spelare som har gjort flest mål
  - ifall två spelare har samma mängd mål, ska den som spelat färre spel komma först

Applikationen ska nu fungera enligt följande:

<sample-output>

fil: **del.json**
läste 14 spelares data

instruktioner:
0 avsluta
1 sök spelare
2 lag
3 länder
4 lagets spelare
5 landets spelare
6 flest poäng
7 flest mål

instruktion: **6**
hur många: **2**
<pre>
Jakub Vrana          WSH  25 + 27 =  52
Jared McCann         PIT  14 + 21 =  35
</pre>

instruktion: **6**
hur många: **5**

<pre>
Jakub Vrana          WSH  25 + 27 =  52
Jared McCann         PIT  14 + 21 =  35
John Klingberg       DAL   6 + 26 =  32
Travis Zajac         NJD   9 + 16 =  25
Conor Sheary         BUF  10 + 13 =  23
</pre>

instruktion: **7**
hur många: **6**

<pre>
Jakub Vrana          WSH  25 + 27 =  52
Jared McCann         PIT  14 + 21 =  35
Conor Sheary         BUF  10 + 13 =  23
Travis Zajac         NJD   9 + 16 =  25
John Klingberg       DAL   6 + 26 =  32
Mark Jankowski       CGY   5 +  2 =   7
</pre>

instruktion: **0**

</sample-output>

</programming-exercise>

Svara till sist på en snabb enkät:

<quiz id="2249a8d3-9455-5228-bd15-d5328d147b19"></quiz>
