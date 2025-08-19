---
path: '/osa-4/4-iteration'
title: 'Iteration'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* vet du vad som menas med iteration
* vet du hur `for`-loopen i Python fungerar
* kan du använda dig av en `for`-loop för att gå igenom listor och strängar.

</text-box>

Du kan använda en while-loop för att gå igenom elementen i en lista på samma sätt som vi använde oss av while-loopar för att gå igenom strängar. Det följande programmet skriver ut elementen i en lista på varsin rad:

```python
lista = [3, 2, 4, 5, 2]

plats = 0
while plats < len(lista):
    print(lista[plats])
    plats += 1
```

<sample-output>

3
2
4
5
2

</sample-output>

Det här fungerar som avsett, men är onödigt komplicerat eftersom vi behöver använda en hjälpvariabel, den som i exemplet ovan kallas `plats`, för att hålla koll på det aktuella elementet. Om vi glömmer att uppdatera hjälpvariabelns värde, riskerar vi att hamna i en oändlig loop. Python erbjuder ett enklare sätt för att gå igenom listor, strängar och andra liknande strukturer. 

## `for`-loopen

När du vill gå igenom en sekvens eller samling av element i Python, kan du använda dig av `for`-loopen. Loopen kan till exempel gå igenom alla element i en lista – från det första till det sista.

När man använder en while-loop, vet programmet inte på förhand hur många gånger loopen kommer att köras, dvs. hur många iterationer ("varv") den kommer att gå igenom. Loopen kommer att fortsätta tills villkoret inte längre är sant eller loopen avslutas på ett annat sätt. I en `for`-loop vet man antalet iterationer på förhand.

Idén är att `for`-loopen går igenom elementen i samlingen ett för ett och kör samma kod för varje element. Programmeraren behöver inte fundera på vilket element som behandlas och när. Syntaxen för `for`-loopen ser ut så här:

```python
for <variabel> in <samling>:
    <block>
```

`for`-loopen tar det första elementet i samlingen, tilldelar det till en variabel, kör kodblocket. Därefter tilldelas variabeln värdet på det följande elementet i samlingen, varpå kodblocket körs igen. Det här upprepas tills samlingens alla element har gåtts igenom. Efter det fortsätter programmet att köras från den kodrad som kommer efter loopen.

<img src="4_3_1.png" alt="Listan iterointi">

Följande program skriver ut alla element i en lista med hjälp av en `for`-loop:

```python
lista = [3, 2, 4, 5, 2]

for element in lista:
    print(element)
```

<sample-output>

3
2
4
5
2

</sample-output>

Jämfört med exemplet i början av den här delen är strukturen mycket enklare att förstå. En `for`-loop gör det enkelt att gå igenom elementen i en samling från början till slut.

Samma princip gäller också för strängar:

```python
namn = input("Ge mig ditt namn: ")

for tecken in namn:
    print(tecken)
```

<sample-output>

Ge mig ditt namn: **Peter**
P
e
t
e
r

</sample-output>

<programming-exercise name='Utskrift med asterisker' tmcname='osa04-11a_utskrift_asterisker'>

Skapa ett program som ber användaren mata in en sträng. Programmet ska sedan skriva ut strängen så att dess tecken kommer under varandra.

Efter varje tecken skriver man också ut en asterisk på en ny rad.

Exempel:

<sample-output>

Ange en sträng: **Python**
P
*
y
*
t
*
h
*
o
*
n
*

</sample-output>

Obs! I de här uppgifterna ska du inte placera kod i `if __name__ == "__main__"` -blocket, om du inte ombeds göra det.

</programming-exercise>

## Funktionen `range`

Man vet ofta hur många gånger man vill upprepa en viss kodsnutt. Det kan till exempel hända att du vill gå igenom talen ett till 100 med en `for`-loop. I stället för att t.ex. manuellt skapa en lista med alla talen i ([1,2,3,4,5,....,100]), kan vi använda funktionen `range` som skapar en följd av heltal.

`range`-funktionen har olika funktionalitet beroende på antalet argument man ger. Det enklaste sättet är att använda ett argument, som då representar antalet element man vill ha i sitt intervall. När man använder ett argument är det första talet alltid 0, vilket innebär att anropet `range(n)` returnerar talföljden `0 ... n - 1`. Vi kan därefter använda det värdet i en `for`-loop: 

```python
for i in range(5):
    print(i)
```

<sample-output>

0
1
2
3
4

</sample-output>

Med två heltalsargument kommer funktionen att returnera ett intervall mellan de två talen. Funktionen `range(a, b)` kommer att ge en följd som startar med `a` och slutar med `b - 1`. Precis som med slicing är intervallet halvöppet – b kommer inte med.

```python
for i in range(3, 7):
    print(i)
```

<sample-output>

3
4
5
6

</sample-output>

Vi kan ännu också ge ett tredje argument som specificerar avståndet mellan talen i intervallet. Anropet `range(a, b, c)` kommer att returnera en följd som börjar med `a` och slutar vid `b - 1`, där värdena ökar med `c` för varje steg.

```python
for i in range(1, 9, 2):
    print(i)
```

<sample-output>

1
3
5
7

</sample-output>

Avståndet eller steget kan också vara negativt. Då kommer intervallet att vara ordnat i fallande ordning. Observera att vi då behöver byta plats på de två första argumenten:

```python
for i in range(6, 2, -1):
    print(i)
```

<sample-output>

6
5
4
3

</sample-output>

<programming-exercise name='Från negativ till positiv' tmcname='osa04-11b_negativ_till_positiv'>

Skapa ett program som ber användaren mata in ett positivt heltal `n`. Programmet ska därefter skriva ut talen i intervallet `-n ... n`, exklusive noll. Varje tal skrivs ut på en skild rad.

Exempel:

<sample-output>

Ange tal: **4**
-4
-3
-2
-1
1
2
3
4

</sample-output>

Obs! I de här uppgifterna ska du inte placera kod i `if __name__ == "__main__"` -blocket, om du inte ombeds göra det.

</programming-exercise>

## Från intervall till lista

Funktionen `range` returnerar ett `range`-objekt som på flera sätt fungerar som en lista, men i verkligheten inte är det. Om du försöker skriva ut värdet som funktionen returnerar kommer du bara att se en beskrivning av `range`-objektet:

```python
tal = range(2, 7)
print(tal)
```

<sample-output>

range(2, 7)

</sample-output>

Funktionen `list` konverterar ett intervall till en lista. Den nya listan kommer att innehålla de värden som finns i intervallet. Vi kommer att bekanta oss närmare med detta i fortsättningskursen som kommer efter den här kursen.

```python
tal = list(range(2, 7))
print(tal)
```

<sample-output>

[2, 3, 4, 5, 6]

</sample-output>

## En påminnelse om de automatiska testerna

Tills nu har de övningar som krävt att du skriver en funktion haft färdiga mallar som sett ut på följande sätt:

```python
# din lösning ska skrivas här

# det lönar sig att testa på funktionen här, på följande sätt
if __name__ == "__main__":
    mening = "jag gillar blåbärspaj så länge den inte innehåller ägg"

    print(ord_ett(mening))
    print(ord_tva(mening))
    print(sista_ordet(mening))
```

Från och med nu kommer det inte längre att finnas påminnelser om att använda `if __name__ == "__main__"` -blocket. De automatiska testerna kommer fortsättningsvis ändå att kräva dem, så du måste själv lägga till blocket i din kod när du testar dina funktioner inom programmets huvudfunktion.

Obs! Vissa övningar, som Palindrom i den här delen, förutsätter att du skriver kod som använder sig av den funktion du skapat. Den här koden bör inte läggas i `if __name__ == "__main__"` -blocket. De automatiska testerna kör ingen kod inom dessa block, så din lösning kommer inte att vara fullständig om du placerar dina funktionsanrop där.

<programming-exercise name='Asterisker' tmcname='osa04-12_asterisker'>

Skapa funktionen `lista_som_asterisker` som tar en lista med heltal som argument. Funktionen ska skriva ut rader med asterisker så att talen i listan indikerar antalet asterisker på en rad.

T.ex. med anropet `lista_som_asterisker([3, 7, 1, 1, 2])` ska resultatet vara:

<sample-output>

<pre>
***
*******
*
*
**
</pre>

</sample-output>

<!-- **OBS!** En del av testerna kan för tillfället vålla problem i Windows-miljö. Om du får följande felmeddelande: 

<img src="4_3_2.png" alt="Listan iterointi">

kan du utföra testerna genom att skicka dem till servern manuellt med _Submit solutions_ som du kommer åt via TMC-menyn som öppnas via symbolen till höger om testknappen. 

Du kan åtgärda felet genom att gå till pluginens inställningsmeny och byta uppgifternas plats under "TMC Data" till en annan plats med en kortare sökväg. Se bilden nedan och knappen _change path_. Det kan ta en stund att sköta överföringen så vänta tills operationen har avslutats. 

<img src="4_3_3.png" alt="Listan iterointi">

Vi försöker hitta en bättre lösning inom de närmaste dagarna. -->

</programming-exercise>

<programming-exercise name='Anagram' tmcname='osa04-13_anagram'>

Skapa funktionen `anagram` som får två strängar som argument. Funktionen ska returnera `True` om strängarna är anagram – dvs. om de innehåller exakt samma bokstäver.

Exempel:

```python
print(anagram("stol", "lost")) # True
print(anagram("burk", "bruk")) # True
print(anagram("anagram", "magarna")) # True
print(anagram("lykta", "lycka")) # False
print(anagram("python", "java")) # False
```

Tips: Funktionen `sorted` fungerar även för strängar.

</programming-exercise>

<programming-exercise name='Palindrom' tmcname='osa04-14_palindrom'>

Skapa funktionen `palindrom` som får en sträng som argument. Funktionen ska returnera `True` om strängen är ett palindrom – dvs. den är den samma oberoende om man börjar läsa från vänster eller höger.

Skapa ett huvudprogram som ber användaren ange ord tills ett palindrom matas in:

<sample-output>

Ange ett palindrom: **python**
det var inte ett palindrom
Ange ett palindrom: **java**
det var inte ett palindrom
Ange ett palindrom: **snöhöna**
det var inte ett palindrom
Ange ett palindrom: **snöhöns**
snöhöns är ett palindrom!

</sample-output>

Obs! Huvudprogrammet ska inte vara i `if __name__ == "__main__"` -blocket.

</programming-exercise>

<programming-exercise name='Summan av de positiva' tmcname='osa04-15_positivas_summa'>

Skapa funktionen `positiv_summa` som tar emot en lista med heltal som argument.

Funktionen ska returnera summan av de positiva talen i listan.

```python
lista = [1, -2, 3, -4, 5]
svar = positiv_summa(lista)
print("svar", svar)
```

<sample-output>

svar 9

</sample-output>

</programming-exercise>

I dessa uppgifter kommer vi att använda listor som argument och returvärden. Det här såg vi på i den förra delen.

<programming-exercise name='Jämna' tmcname='osa04-16_jamna'>

Skapa funktionen `jamna` som får en lista med heltal som argument .

Funktionen ska returnera en ny lista som innehåller de jämna talen som förekommer i den ursprungliga listan.

```python
lista = [1, 2, 3, 4, 5]
ny_lista = jamna(lista)
print("ursprunglig", lista)
print("ny", ny_lista)
```

<sample-output>

ursprunglig [1, 2, 3, 4, 5]
ny [2, 4]

</sample-output>

</programming-exercise>

<programming-exercise name='Summalista' tmcname='osa04-17_summalista'>

Skapa funktionen `summa` som får två heltalslistor som argument. Båda listorna innehåller lika många heltal.

Funktionen ska returnera en ny lista vars element består av summorna av elementen i de två ursprungliga listorna.

Exempel:

```python
a = [1, 2, 3]
b = [7, 8, 9]
print(summa(a, b)) # [8, 10, 12]
```

</programming-exercise>

<programming-exercise name='Unika' tmcname='osa04-18_unika'>

Skapa funktionen `unika` som får en lista med heltal som argument.

Funktionen ska returnera en lista som innehåller talen i den ursprungliga listan i storleksordning. Varje tal ska förekomma bara en gång.

```python
lista = [3, 2, 2, 1, 3, 3, 1]
print(unika(lista)) # [1, 2, 3]
```

</programming-exercise>

## Hitta det bästa eller sämsta värdet i en lista

En vanlig programmeringsuppgift är att hitta det bästa eller sämsta värdet i en lista enligt något visst kriterium. En enkel lösning är att använda en hjälpvariabel för att komma ihåg vilket av elementen som tillsvidare är det mest "optimala". Det mest "optimala" elementet jämförs i varje runda med följande element, varvid det "optimala" antingen hålls oförändrat eller uppdateras till det senaste elementet. När loopen avslutas kommer hjälpvariabeln att innehålla det värde man söker efter.

Här är ett utkast som inte ännu fungerar:

```python
bast = start # startvärdet beror på situationen
for element in lista:
    if element bättre än bast:
        bast = element

# vi vet nu det bästa värdet
```

Detaljerna kring den slutliga koden beror på typen av element i listan och vad kriteriet är för att välja ut det bästa (eller sämsta) elementet. Ibland kan du behöva fler än en hjälpvariabel.

Låt oss öva på den här metoden.

<programming-exercise name='Längden av den längsta' tmcname='osa04-18a_langsta_langden'>

Skapa funktionen `langsta_langden` som får en lista med strängar som argument. Funktionen ska returnera längden på den längsta strängen i listan.

```python
lista = ["första", "andra", "tredje", "sjuttionde"]

resultat = langsta_langden(lista)
print(resultat)
```

```python
lista = ["peter", "emilia", "venla", "eva", "antonia", "julia"]

resultat = langsta_langden(lista)
print(resultat)
```

<sample-output>

10
7

</sample-output>

</programming-exercise>

<programming-exercise name='Listans kortaste' tmcname='osa04-18b_listans_kortaste'>

Skapa funktionen `kortast` som tar en lista med strängar som argument. Funktionen ska returnera den kortaste strängen i listan. Om det finns flera strängar med samma längd kan man returnera vilken som helst av dessa. Du kan anta att det inte finns några tomma strängar (längd noll) i listan.


```python
lista = ["första", "andra", "tredje", "sjuttionde"]

resultat = kortast(lista)
print(resultat)
```

```python
lista = ["peter", "emilia", "venla", "eva", "antonia", "julia"]

resultat = kortast(lista)
print(resultat)
```

<sample-output>

andra
eva

</sample-output>

</programming-exercise>

<programming-exercise name='Listans längsta' tmcname='osa04-19_listans_langsta'>

Skapa funktionen `langsta` som tar en lista med strängar som argument. Funktionen ska returnera en lista som innehåller den längsta strängen i listan. Om det finns flera strängar med samma längd läggs de alla till i listan, i den ordning som de förekommer i den ursprungliga listan.

```python
lista = ["första", "andra", "tredje", "sjuttionde"]

resultat = langsta(lista)
print(resultat) # ['sjuttionde']
```

```python
lista = ["peter", "emilia", "venla", "eva", "antonia", "julia", "saharah"]

resultat = langsta(lista)
print(resultat) # ['antonia', 'saharah']
```

</programming-exercise>

<quiz id="0a813ad1-0b8d-5375-976b-b544f78248e8"></quiz>
