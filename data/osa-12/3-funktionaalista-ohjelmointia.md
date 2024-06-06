---
path: '/osa-12/3-funktionaalista-ohjelmointia'
title: 'Funktionell programmering'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Vet du vad funktionell programmering innebär
- Kommer du att kunna använda funktionerna `map`, `reduce` och `filter` i dina egna program

</text-box>

Funktionell programmering avser ett programmeringsparadigm som undviker förändringar i programtillståndet så mycket som möjligt. Variabler undviks i allmänhet. Istället är det kedjor av funktionsanrop som utgör ryggraden i programmet.

Lambda-uttryck och olika typer av förståelser är vanliga tekniker i den funktionella programmeringsstilen, eftersom de låter dig bearbeta data utan att lagra dem i variabler, så att programmets tillstånd inte ändras. Ett lambdauttryck är till exempel i alla avseenden en funktion, men vi behöver inte lagra en namngiven referens till den någonstans.

Som nämnts ovan är funktionell programmering ett programmeringsparadigm, eller en programmeringsstil. Det finns många olika programmeringsparadigm, och vi har redan stött på några av dem:

* imperativ programmering, där programmet består av en sekvens av instruktioner som utförs i tur och ordning
* procedurprogrammering, där programmet är uppdelat i procedurer eller underprogram
* objektorienterad programmering, där programmet och dess tillstånd lagras i objekt som definieras i klasser.

Det finns olika uppfattningar om gränsdragningen mellan de olika paradigmen, t.ex. hävdar vissa att imperativ och procedurell programmering betyder samma sak, medan andra placerar imperativ programmering som ett paraplybegrepp som täcker både procedurell och objektorienterad programmering. Terminologin och uppdelningen är inte så viktig, och det är inte heller viktigt att strikt hålla sig till det ena eller andra paradigmet, men det är viktigt att förstå att det finns sådana olika synsätt eftersom de påverkar de val som programmerare gör.

Många programmeringsspråk är utformade med det ena eller det andra programmeringsparadigmet i åtanke, men Python är ett ganska mångsidigt programmeringsspråk och gör det möjligt att följa flera olika programmeringsparadigm, även inom ett enda program. Detta gör att vi kan välja den mest effektiva och tydliga metoden för att lösa varje problem.

Låt oss ta en titt på några funktionella programmeringsverktyg som tillhandahålls av Python.

## map

Funktionen `map` utför någon operation på varje objekt i en iterabel serie. Det här låter ungefär som den effekt en comprehension har, men syntaxen är annorlunda.

Låt oss anta att vi har en lista med strängar som vi vill konvertera till en lista med heltal:

```python
mjonolista = ["123","-10", "23", "98", "0", "-110"]

luvut = map(lambda x : int(x), mjonolista)

print(luvut)

for luku in luvut:
    print(luku)
```

<sample-output>

<map object at 0x0000021A4BFA9A90>
123
-10
23
98
0
-110

</sample-output>

Den allmänna syntaxen för `map`-funktionen är

`map(<funktion>, <serie>)`

där `funktion` är den operation vi vill utföra på varje föremål  i `serie`n.

`map`-funktionen returnerar ett objekt av typen `map`, som är itererbart och kan konverteras till en lista:

```python
def alkukirjain_isoksi(mjono: str):
    alku = mjono[0]
    alku = alku.upper()
    return alku + mjono[1:]

testilista = ["eka", "toka", "kolmas", "neljäs"]

valmiit = map(alkukirjain_isoksi, testilista)

valmiit_lista = list(valmiit)
print(valmiit_lista)
```

<sample-output>

['Eka', 'Toka', 'Kolmas', 'Neljäs']

</sample-output>

Som du kan se i exemplen ovan accepterar `map`-funktionen både en anonym lambda-funktion och en namngiven funktion som definieras med nyckelordet `def`.

Vi skulle kunna uppnå samma resultat med en list comprehension:

```python
def alkukirjain_isoksi(mjono: str):
    alku = mjono[0]
    alku = alku.upper()
    return alku + mjono[1:]

testilista = ["eka", "toka", "kolmas", "neljäs"]


valmiit_lista = [alkukirjain_isoksi(alkio) for alkio in testilista]
print(valmiit_lista)
```

...eller så kan vi gå igenom den ursprungliga listan med en `for`-loop och spara de bearbetade objekten i en ny lista med `append`-metoden. I programmering finns det vanligtvis många olika lösningar på varje problem. Det finns sällan några absolut rätta eller felaktiga svar. Att känna till många olika tillvägagångssätt hjälper dig att välja den mest lämpliga för varje situation, eller den som bäst passar din egen smak.

Det är värt att påpeka att `map`-funktionen inte returnerar en lista, utan ett iteratorobjekt av typen map. En iterator beter sig på många sätt som en lista, men det finns undantag, vilket kan ses i följande exempel:

```python
def alkukirjain_isoksi(mjono: str):
    alku = mjono[0]
    alku = alku.upper()
    return alku + mjono[1:]

testilista = ["eka", "toka", "kolmas", "neljäs"]

# talletetaan map-funktion tulos
valmiit = map(alkukirjain_isoksi, testilista)

for sana in valmiit:
  print(sana)

print("sama uusiksi:")
for sana in valmiit:
  print(sana)
```

Detta skulle skriva ut följande:

<sample-output>

Eka
Toka
Kolmas
Neljäs
sama uusiksi:

</sample-output>

Ovan försökte vi skriva ut innehållet i `map`-iteratorn två gånger, men det andra försöket gav ingen utskrift. Anledningen är att `map` är en iterator; när man går igenom den med en `for`-loop "töms" den, ungefär som en generator töms när dess maximala värde har uppnåtts. När objekten i iteratorn har genomgåtts med en `for`-loop finns det inget kvar att gå igenom.

Om du behöver gå igenom innehållet i en `map`-iterator mer än en gång kan du t.ex. konvertera map till en lista:

```python
testilista = ["eka", "toka", "kolmas", "neljäs"]

# muutetaan map-funktion palauttama iteraattori listaksi
valmiit = list(map(alkukirjain_isoksi, testilista))

for sana in valmiit:
  print(sana)

print("sama uusiksi:")
for sana in valmiit:
  print(sana)
```

<sample-output>

Eka
Toka
Kolmas
Neljäs
sama uusiksi:
Eka
Toka
Kolmas
Neljäs

</sample-output>

## Map-funktionen och dina egna klasser

Du kan naturligtvis också bearbeta instanser av dina egna klasser med `map`-funktionen. Det krävs inga speciella knep, som du kan se i exemplet nedan:

```python
class Pankkitili:
    def __init__(self, numero: str, nimi: str, saldo: float):
        self.__numero = numero
        self.nimi = nimi
        self.__saldo = saldo

    def lisaa_rahaa(self, rahasumma: float):
        if rahasumma > 0:
            self.__saldo += rahasumma

    def hae_saldo(self):
        return self.__saldo

t1 = Pankkitili("123456", "Reijo Rahakas", 5000)
t2 = Pankkitili("12321", "Keijo Köyhä ", 1)
t3 = Pankkitili("223344", "Maija Miljonääri ", 1000000)

tilit = [t1, t2, t3]

asiakkaat = map(lambda t: t.nimi, tilit)
for nimi in asiakkaat:
  print(nimi)

saldot = map(lambda t: t.hae_saldo(), tilit)
for saldo in saldot:
  print(saldo)
```

<sample-output>

Reijo Rahakas
Keijo Köyhä
Maija Miljonääri
5000
1
1000000

</sample-output>

Här samlar vi först in namnen på kontoinnehavarna med `map`-funktionen. En anonym lambda-funktion används för att hämta värdet på `namn`-attributet från varje Bankkonto-objekt:

```python
asiakkaat = map(lambda t: t.nimi, tilit)
```

På samma sätt samlas saldot för varje Bankkonto in. Lambda-funktionen ser lite annorlunda ut, eftersom saldot hämtas med ett metodanrop, inte direkt från attributet:

```python
saldot = map(lambda t: t.hae_saldo(), tilit)
```

<programming-exercise name='Suoritukset' tmcname='osa12-11_suoritukset'>

Tehtäväpohjassa on mukana kurssisuoritusta kuvaava luokka `Suoritus`, joka toimii seuraavasti:

```python
suoritus = Suoritus("Pekka Python", "Ohjelmoinnin perusteet", 5)
print(suoritus.opiskelijan_nimi)
print(suoritus.kurssi)
print(suoritus.arvosana)
print(suoritus)
```

<sample-output>

Pekka Python
Ohjelmoinnin perusteet
5
Pekka Python, arvosana kurssilta Ohjelmoinnin perusteet 5

</sample-output>

## Suorittajat

Tee funktio `suorittajien_nimet(suoritukset: list)` joka saa parametriksi listan suoritus-olioita. Funktio palauttaa listan, jolta löytyy suorittajien nimet.

```python
s1 = Suoritus("Pekka Python", "Ohjelmoinnin perusteet", 3)
s2 = Suoritus("Olivia Ohjelmoija", "Ohjelmoinnin perusteet", 5)
s3 = Suoritus("Pekka Python", "Ohjelmoinnin jatkokurssi", 2)

for nimi in suorittajien_nimet([s1, s2, s3]):
    print(nimi)
```

<sample-output>

Pekka Python
Olivia Ohjelmoija
Pekka Python

</sample-output>

Toteuta funktio käyttäen `map`-funktiota!

## Kurssit

Tee funktio `kurssien_nimet(suoritukset: list)` joka saa parametriksi listan suoritus-olioita. Funktio palauttaa listan, jolla on suorituksessa olevien kurssien nimet aakkosjärjestyksessä. Kukin kurssi esiintyy listalla vain kerran.

```python
s1 = Suoritus("Pekka Python", "Ohjelmoinnin perusteet", 3)
s2 = Suoritus("Olivia Ohjelmoija", "Ohjelmoinnin perusteet", 5)
s3 = Suoritus("Pekka Python", "Ohjelmoinnin jatkokurssi", 2)

for nimi in kurssien_nimet([s1, s2, s3]):
    print(nimi)
```
<sample-output>

Ohjelmoinnin jatkokurssi
Ohjelmoinnin perusteet

</sample-output>

Hyödynnä funktion toteutuksessa `map`-funktiota. Se ei tosin yksistään riitä, joten tarvitset muutakin...

</programming-exercise>

## filter

Den inbyggda Python-funktionen `filter` liknar `map`-funktionen, men som namnet antyder tar den inte alla föremål från källan. Istället filtrerar den dem med en kriteriefunktion, som skickas som ett argument. Om kriteriefunktionen returnerar `True` väljs föremålet.

Låt oss titta på ett exempel med `filter`:

```python
luvut = [1, 2, 3, 5, 6, 4, 9, 10, 14, 15]

parilliset = filter(lambda luku: luku % 2 == 0, luvut)

for luku in parilliset:
    print(luku)
```

<sample-output>

2
6
4
10
14

</sample-output>

Det kunde göra ovanstående exemplet en aning tydligare ifall vi använde en namngiven funktion istället:

```python
def onko_parillinen(luku: int):
    if luku % 2 == 0:
        return True
    return False

luvut = [1, 2, 3, 5, 6, 4, 9, 10, 14, 15]

parilliset = filter(onko_parillinen, luvut)

for luku in parilliset:
    print(luku)
```

Dessa två program är funktionellt helt identiska. Det är mest en fråga om åsikt vilket du anser vara det bättre tillvägagångssättet.

Låt oss ta en titt på ett annat filtreringsexempel. Det här programmet modellerar fiskar och väljer bara ut dem som väger minst 1000 gram:

```python
class Kala:
    """ Luokka mallintaa tietynpainoista kalaa """
    def __init__(self, laji: str, paino: int):
        self.laji = laji
        self.paino = paino

    def __repr__(self):
        return f"{self.laji} ({self.paino} g.)"

if __name__ == "__main__":
    k1 = Kala("Hauki", 1870)
    k2 = Kala("Ahven", 763)
    k3 = Kala("Hauki", 3410)
    k4 = Kala("Turska", 2449)
    k5 = Kala("Särki", 210)

    kalat = [k1, k2, k3, k4, k5]

    ylikiloiset = filter(lambda kala : kala.paino >= 1000, kalat)

    for kala in ylikiloiset:
        print(kala)
```

<sample-output>

Hauki (1870 g.)
Hauki (3410 g.)
Turska (2449 g.)

</sample-output>

Vi kunde lika väl använda oss av en list comprehension för att uppnå samma resultat:

```python
ylikiloiset = [kala for kala in kalat if kala.paino >= 1000]
```

## Returvärdet för filter är en iterator

Funktionen `filter` liknar funktionen `map` även i det avseendet att den returnerar en iterator. Det finns situationer där du bör vara särskilt försiktig med `filter` eftersom iteratorer bara kan genomlöpas en gång. Så att försöka skriva ut samlingen av stora fiskar två gånger kommer inte att fungera så enkelt som du kanske tror:

```python
k1 = Kala("Hauki", 1870)
k2 = Kala("Ahven", 763)
k3 = Kala("Hauki", 3410)
k4 = Kala("Turska", 2449)
k5 = Kala("Särki", 210)

kalat = [k1, k2, k3, k4, k5]

ylikiloiset = filter(lambda kala : kala.paino >= 1000, kalat)

for kala in ylikiloiset:
    print(kala)

print("sama uudelleen")

for kala in ylikiloiset:
    print(kala)
```

Detta skulle skriva ut följande:

<sample-output>

Hauki (1870 g.)
Hauki (3410 g.)
Turska (2449 g.)
sama uudelleen

</sample-output>

Om du behöver gå igenom innehållet i en `filter` iterator mer än en gång kan du konvertera resultatet till en lista:

```python
kalat = [k1, k2, k3, k4, k5]

# muutetaan tulos listaksi kutsumalla list-konstruktorioa
ylikiloiset = list(filter(lambda kala : kala.paino >= 1000, kalat))
```

<programming-exercise name='Rajatut suoritukset' tmcname='osa12-12_rajatut_suoritukset'>

Tässä tehtävässä jatketaan luokan `Suoritus` käyttämistä

## Hyväksytyt suoritukset

Tee funktio `hyvaksytyt(suoritukset: list)` joka saa parametriksi listan suoritus-olioita. Funktio palauttaa listan, jolta löytyy suorituksista ne, joiden arvosana on vähintään 1.

```python
s1 = Suoritus("Pekka Python", "Ohjelmoinnin perusteet", 3)
s2 = Suoritus("Olivia Ohjelmoija", "Ohjelmoinnin perusteet", 5)
s3 = Suoritus("Pekka Python", "Ohjelmoinnin jatkokurssi", 0)

for suoritus in hyvaksytyt([s1, s2, s3]):
    print(suoritus)
```

<sample-output>

Pekka Python, arvosana kurssilta Ohjelmoinnin perusteet 3
Olivia Ohjelmoija arvosana kurssilta Ohjelmoinnin perusteet 5

</sample-output>

Toteuta funktio käyttäen `filter`-funktiota!

## Arvosanan suoritukset

Tee funktio `suoritus_arvosanalla(suoritukset: list, arvosana: int)` joka saa parametriksi listan suoritus-olioita sekä kokonaisluvun. Funktio palauttaa listan, jolta löytyy suorituksista ne, joiden arvosana on sama kuin toisen parametrin arvo.

```python
s1 = Suoritus("Pekka Python", "Ohjelmoinnin perusteet", 3)
s2 = Suoritus("Olivia Ohjelmoija", "Ohjelmoinnin perusteet", 5)
s3 = Suoritus("Pekka Python", "Tietoliikenteen perusteet", 3)
s4 = Suoritus("Olivia Ohjelmoija", "Johdatus yliopistomatematiikkaan", 3)

for suoritus in suoritus_arvosanalla([s1, s2, s3, s4], 3):
    print(suoritus)
```

<sample-output>

Pekka Python, arvosana kurssilta Ohjelmoinnin perusteet 3
Pekka Python, arvosana kurssilta Tietoliikenteen perusteet 3
Olivia Ohjelmoija, arvosana kurssilta Johdatus yliopistomatematiikkaan 3

</sample-output>

Toteuta funktio käyttäen `filter`-funktiota!

## Kurssin suorittajat

Tee funktio `kurssin_suorittajat(suoritukset: list, kurssi: str)` joka saa parametriksi listan suoritus-olioita sekä kurssin nimen. Funktio palauttaa _aakkosjärjestyksessä_ niiden opiskelijoiden nimet, jotka ovat suorittaneet parametrina olevan kurssin arvosanalla joka on suurempi kuin nolla.

```python
s1 = Suoritus("Pekka Python", "Ohjelmoinnin perusteet", 3)
s2 = Suoritus("Olivia Ohjelmoija", "Tietoliikenteen perusteet", 5)
s3 = Suoritus("Pekka Python", "Tietoliikenteen perusteet", 0)
s4 = Suoritus("Niilo Nörtti", "Tietoliikenteen perusteet", 3)

for suoritus in kurssin_suorittajat([s1, s2, s3, s4], "Tietoliikenteen perusteet"):
    print(suoritus)
```

<sample-output>

Niilo Nörtti
Olivia Ohjelmoija

</sample-output>

Toteuta funktio käyttäen funktioita `filter` ja `map`.

</programming-exercise>

## reduce

En tredje hörnstensfunktion i denna introduktion till funktionella programmeringsprinciper är `reduce`, från modulen `functools`. Som namnet antyder är dess syfte att reducera objekten i en serie till ett enda värde.

`reduce`-funktionen börjar med en operation och ett startvärde. Den utför den givna operationen på varje objekt i serien i tur och ordning, så att värdet ändras i varje steg. När alla objekt har bearbetats returneras det resulterande värdet.

Vi har gjort summering av listor med heltal på olika sätt tidigare, men här har vi ett exempel med hjälp av funktionen `reduce`. Notera `import`-satsen; i Python version 3 och senare är den nödvändig för att komma åt `reduce`-funktionen. I äldre Python-versioner behövdes inte `import`-satsen, så du kan stöta på exempel utan den på nätet.

```python
from functools import reduce

lista = [2, 3, 1, 5]

lukujen_summa = reduce(lambda summa, alkio: summa + alkio, lista, 0)

print(lukujen_summa)
```

<sample-output>

11

</sample-output>

Låt oss ta en närmare titt på vad som händer här. `reduce`-funktionen tar emot tre argument: en funktion, en serie av föremål och ett startvärde. I det här fallet är serien en lista med heltal, och eftersom vi beräknar en summa är ett lämpligt startvärde noll.

Det första argumentet är en funktion, som representerar den operation vi vill utföra på varje objekt. Här är funktionen en anonym lambda-funktion:

```python
lambda summa, alkio: summa + alkio
```

Denna funktion tar två argument: det aktuella reducerade värdet och det föremål vars tur det är att bearbetas. Dessa används för att beräkna ett nytt värde för det reducerade värdet. I detta fall är det nya värdet summan av det gamla värdet och det aktuella objektet.

Det kan vara lättare att förstå vad funktionen `reduce` faktiskt gör om vi använder en vanlig namngiven funktion i stället för en lambda-funktion. På så sätt kan vi också inkludera användbara utskrifter:

```python
from functools import reduce

lista = [2, 3, 1, 5]

# reducen apufunktio joka huolehtii yhden alkion arvon lisäämisestä summaan
def summaaja(summa, alkio):
  print(f"summa nyt {summa}, vuorossa alkio {alkio}")
  # uusi summa on vanha summa + alkion arvo
  return summa + alkio

lukujen_summa = reduce(summaaja, lista, 0)

print(lukujen_summa)
```

Detta program skriver ut:

<sample-output>

summa nyt 0, vuorossa alkio 2
summa nyt 2, vuorossa alkio 3
summa nyt 5, vuorossa alkio 1
summa nyt 6, vuorossa alkio 5
11

</sample-output>

Först tar funktionen hand om objektet med värdet 2. Till att börja med är den reducerade summan 0, vilket är det ursprungliga värdet som skickas till `reduce`-funktionen. Funktionen beräknar och returnerar summan av dessa två: `0 + 2 = 2`.

Detta är det värde som lagras i `reducerad_summa` när `reduce`-funktionen bearbetar nästa objekt i listan, med värdet 3. Funktionen beräknar och returnerar summan av dessa två: `2 + 3 = 5`. Detta resultat används sedan när nästa objekt bearbetas, och så vidare, och så vidare.

Nu är det enkelt att summera, eftersom det till och med finns en inbyggd `sum`-funktion för detta ändamål. Men hur är det med multiplikation? Det krävs bara små förändringar för att skapa en reducerad produkt:

```python
from functools import reduce

lista = [2, 2, 4, 3, 5, 2]

tulo = reduce(lambda tulo, alkio: tulo * alkio, lista, 1)

print(tulo)
```

<sample-output>

480

</sample-output>

Eftersom vi har att göra med multiplikation är startvärdet inte noll. Istället använder vi 1. Vad skulle hända om vi använde 0 som startvärde?

Ovan har vi till stor del behandlat heltal, men `map`, `filter` och `reduce` kan alla hantera en samling objekt av alla typer.

Låt oss som ett exempel generera en totalsumma av saldona för alla konton i en bank med hjälp av `reduce`:

```python
class Pankkitili:
    def __init__(self, numero: str, nimi: str, saldo: float):
        self.__numero = numero
        self.nimi = nimi
        self.__saldo = saldo

    def lisaa_rahaa(self, rahasumma: float):
        if rahasumma > 0:
            self.__saldo += rahasumma

    def hae_saldo(self):
        return self.__saldo

t1 = Pankkitili("123456", "Reijo Rahakas", 5000)
t2 = Pankkitili("12321", "Keijo Köyhä ", 1)
t3 = Pankkitili("223344", "Maija Miljonääri ", 1000000)

tilit = [t1, t2, t3]

from functools import reduce

def saldojen_summaaja(yht_saldo, tili):
  return yht_saldo + tili.hae_saldo()

saldot_yhteensa = reduce(saldojen_summaaja, tilit, 0)

print("pankissa rahaa yhteensä")
print(saldot_yhteensa)
```

Detta program skulle skriva ut:

<sample-output>

pankissa rahaa yhteensä
1005001

</sample-output>

Funktionen `saldo_summa_hjalpare` tar saldot på varje bankkonto, med den metod som är avsedd för ändamålet i klassdefinitionen `Bankkonto`:

```python
def saldojen_summaaja(yht_saldo, tili):
  return yht_saldo + tili.hae_saldo()
```

<text-box variant='hint' name='Alkuarvoton reduce'>

Funktion `reduce` kolmas parametri eli alkuarvo ei itse asiassa ole kaikissa tilanteissa pakollinen. Esimerkiksi summan laskeminen onnistuisi _ilman_ alkuarvoa:

```python
lista = [2, 3, 1, 5]

lukujen_summa = reduce(lambda summa, alkio: summa + alkio, lista)

print(lukujen_summa)
```

Jos alkuarvoa ei anneta, toimii listan ensimmäinen luku alkuarvona ja "redusointi" aloitetaan vasta listan toisesta alkiosta.

OBS: Om föremålen i serien är av en annan typ än det avsedda reducerade resultatet, är det tredje argumentet obligatoriskt. Exemplet med bankkontona skulle inte fungera utan det ursprungliga värdet. Det vill säga att prova detta

```python
saldot_yhteensa = reduce(saldojen_summaaja, tilit)
```

Skulle producera ett fel:

```python
TypeError: unsupported operand type(s) for +: 'Pankkitili' and 'int'
```

I ovanstående fall, när `reduce` försöker utföra funktionen `saldo_summa_hjalpare` för första gången, är de argument som används de två första föremålen i listan, som båda är av typen Bankkonto. Specifikt är det värde som tilldelats parametern `saldo_summa` det första föremålet i listan. Funktionen `saldo_summa_hjalpare` försöker lägga till ett heltalsvärde till den, men att lägga till ett heltal direkt till ett Bankkonto-objekt är inte en åtgärd som stöds. 

</text-box>

<programming-exercise name='Opintopisteet' tmcname='osa12-13_opintopisteet'>

Tarkastellaan tässä tehtävässä hieman erilaista versiota luokasta `Suoritus`. Tällä kertaa se kuvastaa ainoastaan yksittäisen opiskelijan kurssisuorituksia. Luokka toimii seuraavasti:


```python
suoritus = Suoritus("Tietorakenteet ja algoritmit", 3, 10)
print(suoritus)
print(suoritus.kurssi)
print(suoritus.opintopisteet)
print(suoritus.arvosana)
```

<sample-output>

Tietorakenteet ja algoritmit (10 op) arvosana 3
Tietorakenteet ja algoritmit
10
3

</sample-output>

## Opintopistemäärä

Toteuta funktio `kaikkien_opintopisteiden_summa`, joka saa parametriksi listan suorituksia ja laskee suoritusten yhteenlasketun opintopistemäärän. Funktio toimii seuraavasti

```python
s1 = Suoritus("Ohjelmoinnin perusteet", 5, 5)
s2 = Suoritus("Ohjelmoinnin jatkokutssi", 4, 5)
s3 = Suoritus("Tietorakenteet ja algoritmit", 3, 10)
summa = kaikkien_opintopisteiden_summa([s1, s2, s3])
print(summa)
```

<sample-output>

20

</sample-output>

Toteuta funktio käyttäen `reduce`-funktiota!

## Hyväksyttyjen opintopistemäärä

Toteuta funktio `hyvaksyttyjen_opintopisteiden_summa`, joka saa parametriksi listan suorituksia ja laskee arvosanan 1 tai parempien omaavien suoritusten yhteenlasketun opintopistemäärän. Funktio toimii seuraavasti

```python
s1 = Suoritus("Ohjelmoinnin perusteet", 5, 5)
s2 = Suoritus("Ohjelmoinnin jatkokutssi", 0, 4)
s3 = Suoritus("Tietorakenteet ja algoritmit", 3, 10)
summa = hyvaksyttyjen_opintopisteiden_summa([s1, s2, s3])
print(summa)
```

<sample-output>

15

</sample-output>

Toteuta funktio käyttäen `reduce`- ja `filter`-funktiota!

## Hyväksyttyjen suoritusten keskiarvo

Toteuta funktio `keskiarvo`, joka saa parametriksi listan suorituksia ja laskee arvosanan 1 tai parempien omaavien suoritusten arvosanojen keskiarvon. Funktio toimii seuraavasti

```python
s1 = Suoritus("Ohjelmoinnin perusteet", 5, 5)
s2 = Suoritus("Ohjelmoinnin jatkokutssi", 0, 4)
s3 = Suoritus("Tietorakenteet ja algoritmit", 3, 10)
summa = keskiarvo([s1, s2, s3])
print(summa)
```

<sample-output>

4.0

</sample-output>

Hyödynnä funktion toteutuksessa `reduce`- ja `filter`-funktiota!

[Tämä](/osa-12/3-funktionaalista-ohjelmointia#filter-palauttaa-iteraattorin) lienee syytä pitää mielessä tätä tehtävää tehdessä-

</programming-exercise>
