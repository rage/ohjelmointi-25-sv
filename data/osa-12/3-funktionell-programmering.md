---
path: '/osa-12/3-funktionell-programmering'
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
stranglista = ["123","-10", "23", "98", "0", "-110"]

talen = map(lambda x : int(x), stranglista)

print(talen)

for tal in talen:
    print(tal)
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
def versalisera(strang: str):
    borjan = strang[0]
    borjan = borjan.upper()
    return borjan + strang[1:]

testlista = ["första", "andra", "tredje", "fjärde"]

fardiga = map(versalisera, testlista)

fardiga_lista = list(fardiga)
print(fardiga_lista)
```

<sample-output>

['Första', 'Andra', 'Tredje', 'Fjärde']

</sample-output>

Som du kan se i exemplen ovan accepterar `map`-funktionen både en anonym lambda-funktion och en namngiven funktion som definieras med nyckelordet `def`.

Vi skulle kunna uppnå samma resultat med en list comprehension:

```python
def versalisera(strang: str):
    borjan = strang[0]
    borjan = borjan.upper()
    return borjan + strang[1:]

testlista = ["första", "andra", "tredje", "fjärde"]


fardiga_lista = [versalisera(foremal) for foremal in testlista]
print(fardiga_lista)
```

...eller så kan vi gå igenom den ursprungliga listan med en `for`-loop och spara de bearbetade objekten i en ny lista med `append`-metoden. I programmering finns det vanligtvis många olika lösningar på varje problem. Det finns sällan några absolut rätta eller felaktiga svar. Att känna till många olika tillvägagångssätt hjälper dig att välja den mest lämpliga för varje situation, eller den som bäst passar din egen smak.

Det är värt att påpeka att `map`-funktionen inte returnerar en lista, utan ett iteratorobjekt av typen map. En iterator beter sig på många sätt som en lista, men det finns undantag, vilket kan ses i följande exempel:

```python
def versalisera(strang: str):
    borjan = strang[0]
    borjan = borjan.upper()
    return borjan + strang[1:]

testlista = ["första", "andra", "tredje", "fjärde"]

# lagrar map-funktionens returvärde
fardiga = map(versalisera, testlista)

for ord in fardiga:
  print(ord)

print("samma igen:")
for ord in fardiga:
  print(ord)
```

Detta skulle skriva ut följande:

<sample-output>

Första
Andra
Tredje
Fjärde
samma igen:

</sample-output>

Ovan försökte vi skriva ut innehållet i `map`-iteratorn två gånger, men det andra försöket gav ingen utskrift. Anledningen är att `map` är en iterator; när man går igenom den med en `for`-loop "töms" den, ungefär som en generator töms när dess maximala värde har uppnåtts. När objekten i iteratorn har genomgåtts med en `for`-loop finns det inget kvar att gå igenom.

Om du behöver gå igenom innehållet i en `map`-iterator mer än en gång kan du t.ex. konvertera map till en lista:

```python
testlista = ["första", "andra", "tredje", "fjärde"]

# konvertera returvärdet från map-funktionen till en lista
fardiga = list(map(versalisera, testlista))

for ord in fardiga:
  print(ord)

print("samma igen:")
for ord in fardiga:
  print(ord)
```

<sample-output>

Första
Andra
Tredje
Fjärde
samma igen:
Första
Andra
Tredje
Fjärde

</sample-output>

## Map-funktionen och dina egna klasser

Du kan naturligtvis också bearbeta instanser av dina egna klasser med `map`-funktionen. Det krävs inga speciella knep, som du kan se i exemplet nedan:

```python
class Bankkonto:
    def __init__(self, nummer: str, namn: str, saldo: float):
        self.__nummer = nummer
        self.namn = namn
        self.__saldo = saldo

    def tillsatt_pengar(self, mangd: float):
        if mangd > 0:
            self.__saldo += mangd

    def hamta_saldo(self):
        return self.__saldo

k1 = Bankkonto("123456", "Robert Rik", 5000)
k2 = Bankkonto("12321", "Peter Pank", 1)
k3 = Bankkonto("223344", "Maja Miljonär ", 1000000)

konton = [k1, k2, k3]

kunder = map(lambda t: t.namn, konton)
for namn in kunder:
  print(namn)

saldon = map(lambda t: t.hamta_saldo(), konton)
for saldo in saldon:
  print(saldo)
```

<sample-output>

Robert Rik
Peter Pank
Maja Miljonär
5000
1
1000000

</sample-output>

Här samlar vi först in namnen på kontoinnehavarna med `map`-funktionen. En anonym lambda-funktion används för att hämta värdet på `namn`-attributet från varje Bankkonto-objekt:

```python
kunder = map(lambda t: t.namn, konton)
```

På samma sätt samlas saldot för varje Bankkonto in. Lambda-funktionen ser lite annorlunda ut, eftersom saldot hämtas med ett metodanrop, inte direkt från attributet:

```python
saldon = map(lambda t: t.hamta_saldo(), konton)
```

<programming-exercise name='Prestationer' tmcname='osa12-11_prestationer'>

I uppgiftsbotten finns klassdefinitionen för `Prestation`, som fungerar enligt följande:

```python
prestation = Prestation("Peter Python", "Introduktion till programmering", 5)
print(prestation.studerandens_namn)
print(prestation.kurs)
print(prestation.vitsord)
print(prestation)
```

<sample-output>

Peter Python
Introduktion till programmering
5
Peter Python, vitsord från kursen Introduktion till programmering 5

</sample-output>

## Namnet på studeranden

Skapa funktionen `presterarnas_namn(prestationer: list)` som tar en lista av Prestation-objekt som argument. Funktionen ska returnera en ny lista med namnen på studeranden som genomför kursen.

```python
p1 = Prestation("Peter Python", "Introduktion till programmering", 3)
p2 = Prestation("Patrik Programmerare", "Introduktion till programmering", 5)
p3 = Prestation("Peter Python", "Fortsättningskurs i programmering", 2)

for namn in presterarnas_namn([p1, p2, p3]):
    print(namn)
```

<sample-output>

Peter Python
Patrik Programmerare
Peter Python

</sample-output>

Implementera funktionen användandes `map`-funktionen!

## Kurser

Skapa funktionen `kursnamn(prestationer: list)` som tar en lista av Prestation-objekt som argument. Funktionen ska returnera en ny lista som innehåller namnet på kurserna i den ursprungliga listan i alfabetisk ordning. Varje kursnamn ska förekomma endast en gång på listan.

```python
p1 = Prestation("Peter Python", "Introduktion till programmering", 3)
p2 = Prestation("Patrik Programmerare", "Introduktion till programmering", 5)
p3 = Prestation("Peter Python", "Fortsättningskurs i programmering", 2)

for namn in kursnamn([p1, p2, p3]):
    print(namn)
```
<sample-output>

Fortsättningskurs i programmering
Introduktion till programmering

</sample-output>

Implementera funktionen användandes `map`-funktionen. Du behöver nånting annat också, för att se till att kursnamnen är unika.

</programming-exercise>

## filter

Den inbyggda Python-funktionen `filter` liknar `map`-funktionen, men som namnet antyder tar den inte alla föremål från källan. Istället filtrerar den dem med en kriteriefunktion, som skickas som ett argument. Om kriteriefunktionen returnerar `True` väljs föremålet.

Låt oss titta på ett exempel med `filter`:

```python
talen = [1, 2, 3, 5, 6, 4, 9, 10, 14, 15]

jamna = filter(lambda tal: tal % 2 == 0, talen)

for tal in jamna:
    print(tal)
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
def ar_det_jamnt(tal: int):
    if tal % 2 == 0:
        return True
    return False

talen = [1, 2, 3, 5, 6, 4, 9, 10, 14, 15]

jamna = filter(ar_det_jamnt, talen)

for tal in jamna:
    print(tal)
```

Dessa två program är funktionellt helt identiska. Det är mest en fråga om åsikt vilket du anser vara det bättre tillvägagångssättet.

Låt oss ta en titt på ett annat filtreringsexempel. Det här programmet modellerar fiskar och väljer bara ut dem som väger minst 1000 gram:

```python
class Fisk:
    """ Klassen modellerar en fisk av en specifik art och vikt """
    def __init__(self, art: str, vikt: int):
        self.art = art
        self.vikt = vikt

    def __repr__(self):
        return f"{self.art} ({self.vikt} g.)"

if __name__ == "__main__":
    f1 = Fisk("Gädda", 1870)
    f2 = Fisk("Abborre", 763)
    f3 = Fisk("Gädda", 3410)
    f4 = Fisk("Torsk", 2449)
    f5 = Fisk("Mört", 210)

    fiskar = [f1, f2, f3, f4, f5]

    over_kilot = filter(lambda fisk : fisk.vikt >= 1000, fiskar)

    for fisk in over_kilot:
        print(fisk)
```

<sample-output>

Gädda (1870 g.)
Gädda (3410 g.)
Torsk (2449 g.)

</sample-output>

Vi kunde lika väl använda oss av en list comprehension för att uppnå samma resultat:

```python
over_kilot = [fisk for fisk in fiskar if fisk.vikt >= 1000]
```

## Returvärdet för filter är en iterator

Funktionen `filter` liknar funktionen `map` även i det avseendet att den returnerar en iterator. Det finns situationer där du bör vara särskilt försiktig med `filter` eftersom iteratorer bara kan genomlöpas en gång. Så att försöka skriva ut samlingen av stora fiskar två gånger kommer inte att fungera så enkelt som du kanske tror:

```python
f1 = Fisk("Gädda", 1870)
f2 = Fisk("Abborre", 763)
f3 = Fisk("Gädda", 3410)
f4 = Fisk("Torsk", 2449)
f5 = Fisk("Mört", 210)

fiskar = [f1, f2, f3, f4, f5]

over_kilot = filter(lambda fisk : fisk.vikt >= 1000, fiskar)

for fisk in over_kilot:
    print(fisk)

print("samma igen")

for fisk in over_kilot:
    print(fisk)
```

Detta skulle skriva ut följande:

<sample-output>

Gädda (1870 g.)
Gädda (3410 g.)
Torsk (2449 g.)
samma igen

</sample-output>

Om du behöver gå igenom innehållet i en `filter` iterator mer än en gång kan du konvertera resultatet till en lista:

```python
fiskar = [f1, f2, f3, f4, f5]

# konvertera returvärdet från filter-funktionen till en lista
over_kilot = list(filter(lambda fisk : fisk.vikt >= 1000, fiskar))
```

<programming-exercise name='Begränsade prestationer' tmcname='osa12-12_begransade_prestationer'>

I denna övning fortsätter vi med `Prestation`-klassen.

## Godkända försök

Skapa funktionen `godkanda(prestationer: list)`, som tar en lista av Prestation-objekt som argument. Funktionen ska returnera en ny lista av Prestation-objekt, inkluderandes endast de föremål från den ursprungliga listan vars vitsord är åtminstone 1.

```python
p1 = Prestation("Peter Python", "Introduktion till programmering", 3)
p2 = Prestation("Patrik Programmerare", "Introduktion till programmering", 5)
p3 = Prestation("Peter Python", "Fortsättningskurs i programmering", 0)

for prestation in godkanda([p1, p2, p3]):
    print(prestation)
```

<sample-output>

Peter Python, vitsord från kursen Introduktion till programmering 3
Patrik Programmerare vitsord från kursen Introduktion till programmering 5

</sample-output>

Implementera funktionen användandes `filter`-funktionen!

## Prestationer med vitsord

Skapa funktionen `prestationer_med_vitsord(prestationer: list, vitsord: int)`, som tar en lista av Prestation-objekt och ett heltal som argument. Funktionen ska returnera en ny lista som innehåller endast de Prestation-objekt från den ursprungliga listan vars vitsord matchar det andra argumentet.

```python
p1 = Prestation("Peter Python", "Introduktion till programmering", 3)
p2 = Prestation("Patrik Programmerare", "Introduktion till programmering", 5)
p3 = Prestation("Peter Python", "Introduktion till datakommunikation", 3)
p4 = Prestation("Patrik Programmerare", "Introduktion till universitetsmatematik", 3)

for prestation in prestationer_med_vitsord([p1, p2, p3, p4], 3):
    print(prestation)
```

<sample-output>

Peter Python, vitsord från kursen Introduktion till programmering 3
Peter Python, vitsord från kursen Introduktion till datakommunikation 3
Patrik Programmerare, vitsord från kursen Introduktion till universitetsmatematik 3

</sample-output>

Implementera funktionen användandes `filter`-funktionen!

## Studeranden som klarat kursen

Skapa funktionen `kursens_deltagare(prestationer: list, kurs: str)`, som tar en lista av Prestation-objekt och ett kursnamn som argument. Funktionen ska returnera en _alfabetiskt sorterad_ lista av namn på de studeranden som klarat av kursen, d.v.s. deras vitsord för den givna kursen är högre än 0.

```python
p1 = Prestation("Peter Python", "Introduktion till programmering", 3)
p2 = Prestation("Patrik Programmerare", "Introduktion till datakommunikation", 5)
p3 = Prestation("Peter Python", "Introduktion till datakommunikation", 0)
p4 = Prestation("Niko Nörd", "Introduktion till datakommunikation", 3)

for prestation in kursens_deltagare([p1, p2, p3, p4], "Introduktion till datakommunikation"):
    print(prestation)
```

<sample-output>

Niko Nörd
Patrik Programmerare

</sample-output>

Implementera funktionen användandes `filter`- och map-funktionerna!

</programming-exercise>

## reduce

En tredje hörnstensfunktion i denna introduktion till funktionella programmeringsprinciper är `reduce`, från modulen `functools`. Som namnet antyder är dess syfte att reducera objekten i en serie till ett enda värde.

`reduce`-funktionen börjar med en operation och ett startvärde. Den utför den givna operationen på varje objekt i serien i tur och ordning, så att värdet ändras i varje steg. När alla objekt har bearbetats returneras det resulterande värdet.

Vi har gjort summering av listor med heltal på olika sätt tidigare, men här har vi ett exempel med hjälp av funktionen `reduce`. Notera `import`-satsen; i Python version 3 och senare är den nödvändig för att komma åt `reduce`-funktionen. I äldre Python-versioner behövdes inte `import`-satsen, så du kan stöta på exempel utan den på nätet.

```python
from functools import reduce

lista = [2, 3, 1, 5]

talens_summa = reduce(lambda summa, foremal: summa + foremal, lista, 0)

print(talens_summa)
```

<sample-output>

11

</sample-output>

Låt oss ta en närmare titt på vad som händer här. `reduce`-funktionen tar emot tre argument: en funktion, en serie av föremål och ett startvärde. I det här fallet är serien en lista med heltal, och eftersom vi beräknar en summa är ett lämpligt startvärde noll.

Det första argumentet är en funktion, som representerar den operation vi vill utföra på varje objekt. Här är funktionen en anonym lambda-funktion:

```python
lambda summa, foremal: summa + foremal
```

Denna funktion tar två argument: det aktuella reducerade värdet och det föremål vars tur det är att bearbetas. Dessa används för att beräkna ett nytt värde för det reducerade värdet. I detta fall är det nya värdet summan av det gamla värdet och det aktuella objektet.

Det kan vara lättare att förstå vad funktionen `reduce` faktiskt gör om vi använder en vanlig namngiven funktion i stället för en lambda-funktion. På så sätt kan vi också inkludera användbara utskrifter:

```python
from functools import reduce

lista = [2, 3, 1, 5]

# en hjälparfunktion för reduce, som lägger till ett värde till den för tillfället reducerade summan
def summare(summa, foremal):
  print(f"summa nu {summa}, nästa föremål {foremal}")
  # den nya summan är gamla summan + nästa föremål
  return summa + foremal

talens_summa = reduce(summare, lista, 0)

print(talens_summa)
```

Detta program skriver ut:

<sample-output>

summa nu 0, nästa föremål 2
summa nu 2, nästa föremål 3
summa nu 5, nästa föremål 1
summa nu 6, nästa föremål 5
11

</sample-output>

Först tar funktionen hand om objektet med värdet 2. Till att börja med är den reducerade summan 0, vilket är det ursprungliga värdet som skickas till `reduce`-funktionen. Funktionen beräknar och returnerar summan av dessa två: `0 + 2 = 2`.

Detta är det värde som lagras i `reducerad_summa` när `reduce`-funktionen bearbetar nästa objekt i listan, med värdet 3. Funktionen beräknar och returnerar summan av dessa två: `2 + 3 = 5`. Detta resultat används sedan när nästa objekt bearbetas, och så vidare, och så vidare.

Nu är det enkelt att summera, eftersom det till och med finns en inbyggd `sum`-funktion för detta ändamål. Men hur är det med multiplikation? Det krävs bara små förändringar för att skapa en reducerad produkt:

```python
from functools import reduce

lista = [2, 2, 4, 3, 5, 2]

produkt = reduce(lambda produkt, foremal: produkt * foremal, lista, 1)

print(produkt)
```

<sample-output>

480

</sample-output>

Eftersom vi har att göra med multiplikation är startvärdet inte noll. Istället använder vi 1. Vad skulle hända om vi använde 0 som startvärde?

Ovan har vi till stor del behandlat heltal, men `map`, `filter` och `reduce` kan alla hantera en samling objekt av alla typer.

Låt oss som ett exempel generera en totalsumma av saldona för alla konton i en bank med hjälp av `reduce`:

```python
class Bankkonto:
    def __init__(self, nummer: str, namn: str, saldo: float):
        self.__nummer = nummer
        self.namn = namn
        self.__saldo = saldo

    def tillsatt_pengar(self, mangd: float):
        if mangd > 0:
            self.__saldo += mangd

    def hamta_saldo(self):
        return self.__saldo

k1 = Bankkonto("123456", "Robert Rik", 5000)
k2 = Bankkonto("12321", "Peter Pank", 1)
k3 = Bankkonto("223344", "Maja Miljonär", 1000000)

konton = [k1, k2, k3]

from functools import reduce

def saldo_summa_hjalpare(tot_saldo, konto):
  return tot_saldo + konto.hamta_saldo()

saldon_totalt = reduce(saldo_summa_hjalpare, konton, 0)

print("Bankens totala saldo:")
print(saldon_totalt)
```

Detta program skulle skriva ut:

<sample-output>

Bankens totala saldo:
1005001

</sample-output>

Funktionen `saldo_summa_hjalpare` tar saldot på varje bankkonto, med den metod som är avsedd för ändamålet i klassdefinitionen `Bankkonto`:

```python
def saldo_summa_hjalpare(tot_saldo, konto):
  return tot_saldo + konto.hamta_saldo()
```

<text-box variant='hint' name='Alkuarvoton reduce'>

Du måste inte alltid ange ett tredje argument till `reduce`-funktionen. Till exempel skulle summering fungera lika väl _utan_ ursprungsvärdet:

```python
lista = [2, 3, 1, 5]

talens_summa = reduce(lambda summa, foremal: summa + foremal, lista)

print(talens_summa)
```

Ifall ett ursprungligt värde lämnas bort tar `reduce` det första föremålet i listan som sitt ursprungsvärde och börjar reducera från det andra föremålet framåt.

OBS: Om föremålen i serien är av en annan typ än det avsedda reducerade resultatet, är det tredje argumentet obligatoriskt. Exemplet med bankkontona skulle inte fungera utan det ursprungliga värdet. Det vill säga att prova detta

```python
saldon_totalt = reduce(saldo_summa_hjalpare, konton)
```

Skulle producera ett fel:

```python
TypeError: unsupported operand type(s) for +: 'Bankkonto' and 'int'
```

I ovanstående fall, när `reduce` försöker utföra funktionen `saldo_summa_hjalpare` för första gången, är de argument som används de två första föremålen i listan, som båda är av typen Bankkonto. Specifikt är det värde som tilldelats parametern `saldo_summa` det första föremålet i listan. Funktionen `saldo_summa_hjalpare` försöker lägga till ett heltalsvärde till den, men att lägga till ett heltal direkt till ett Bankkonto-objekt är inte en åtgärd som stöds.

</text-box>

<programming-exercise name='Studiepoäng' tmcname='osa12-13_studiepoang'>

I denna övning jobbar vi med en aning modifierad version av `Prestation`-klassen. Namnet på studeranden är utelämnat, men antalet studiepoäng är inkluderat. Klassen fungerar enligt följande:

```python
prestation = Prestation("Datastrukturer och algoritmer", 3, 10)
print(prestation)
print(prestation.kurs)
print(prestation.studiepoang)
print(prestation.vitsord)
```

<sample-output>

Datastrukturer och algoritmer (10 sp) vitsord 3
Datastrukturer och algoritmer
10
3

</sample-output>

## Totala antalet studiepoäng

Skapa funktionen `studiepoangens_summa`, som tar en lista av prestationer som argument. Funktionen adderar ihop det totala antalet studiepoäng som fås av kurserna. Den ska fungera enligt följande:

```python
p1 = Prestation("Introduktion till programmering", 5, 5)
p2 = Prestation("Fortsättningskurs i programmering", 4, 5)
p3 = Prestation("Datastrukturer och algoritmer", 3, 10)
summa = studiepoangens_summa([p1, p2, p3])
print(summa)
```

<sample-output>

20

</sample-output>

Implementera funktionen användandes `reduce`-funktionen!

## Summan av avklarade studiepoäng

Skapa funktionen `godkanda_studiepoangens_summa`, som tar en lista av prestationer som argument. Funktionen adderar ihop studiepoängen för prestationerna med vitsordet 1 eller högre. Den ska fungera enligt följande:

```python
p1 = Prestation("Introduktion till programmering", 5, 5)
p2 = Prestation("Fortsättningskurs i programmering", 0, 4)
p3 = Prestation("Datastrukturer och algoritmer", 3, 10)
summa = godkanda_studiepoangens_summa([p1, p2, p3])
print(summa)
```

<sample-output>

15

</sample-output>

Implementera funktionen användandes `reduce`- och `filter`-funktionerna!

## Avklarade kursers medelvitsord

Skapa funktionen `medeltal`, som tar en lista av suorits som argument. Funktionen räknar ut medelvitsordet för prestationerna med vitsord 1 eller högre. Den ska fungera enligt följande:

```python
p1 = Prestation("Introduktion till programmering", 5, 5)
p2 = Prestation("Fortsättningskurs i programmering", 0, 4)
p3 = Prestation("Datastrukturer och algoritmer", 3, 10)
summa = medeltal([p1, p2, p3])
print(summa)
```

<sample-output>

4.0

</sample-output>

Implementera funktionen användandes `reduce`- och `filter`-funktionerna!

När du jobbar på den här övningen kan det vara värt att komma ihåg att returvärdet av filter är en iterator.

</programming-exercise>
