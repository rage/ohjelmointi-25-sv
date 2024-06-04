---
path: '/osa-4/4-silmukat-ja-iterointi'
title: 'Iteration'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

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

Det här fungerar helt bra, men det är ett komplicerat sätt att gå igenom en lista eftersom att det krävs en hjälpvariabel, `index`, för att minnas vid vilket element man är vid. Till all lycka erbjuder Python ett enklare sätt att gå igenom listor, strängar och liknande strukturer.

## `for`-loopen

När du vill gå igenom en färdig samling av element i Python, kan du använda dig av en `for`-loop. Loopen kan till exempel gå igenom alla element i en lista – från det första till det sista.

När man använder en while-loop, vet programmet inte på förhand hur många iterationer ("varv") loopen kommer att gå igenom. Loopen kommer att fortsätta tills villkoret inte längre är sant eller loopen avslutas på ett annat sätt. I en `for`-loop vet man antalet iterationer på förhand.

Idén är att `for`-loopen går igenom elementen i samlingen ett för ett och utför samma sak för varje element. Programmeraren behöver inte fundera på vilket element som behandlas och när det görs. Syntaxen för `for`-loopen är den följande:

```python
for <variabel> in <samling>:
    <block>
```

`for`-loopen tar ett element i samlingen, tilldelar det till en variabel, kör kodblocket och fortsätter till nästa element. När alla element har behandlats kommer programmet att fortsätta köras från och med kodraden som följer loopen.

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
namn = input("Ange ditt namn: ")

for tecken in namn:
    print(tecken)
```

<sample-output>

Ange ditt namn: **Peter**
P
e
t
e
r

</sample-output>

<programming-exercise name='Tulostus tähdillä' tmcname='osa04-11a_tulostus_tahdilla'>

Skapa ett program som ber användaren ange en sträng. Programmet ska sedan skriva ut strängen så att dess tecken kommer under varandra.

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

Man vet ofta hur många gånger man vill upprepa en viss kodsnutt. Det kan till exempel hända att du vill gå igenom siffrorna ett till hundra. Funktionen `range` kan användas i samband med en `for`-loop för att uppnå detta.

Det finns några olika sätt att använda `range`-funktionen. Det enklaste sättet är att använda ett argument, som då hänvisar till slutpunkten. Själva slutpunkten inkluderas inte, likt extrahering av delsträngar (slice). Det betyder alltså att anropet `range(n)` ger oss en loop som går igenom siffrorna `0` till `n - 1`:

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

Med två argument kommer funktionen att returnera ett intervall mellan två siffror. Funktionen `range(a, b)` kommer att ge ett intervall som startar med `a` och slutar med `b - 1`.

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

Till sist: vi kan ge ett tredje argument som specificerar avståndet mellan värdena. Anropet `range(a, b, c)` kommer att ge ett intervall som börjar med `a` och slutar vid `b - 1`, och ökar med `c` för varje steg.

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

Avståndet eller steget kan också vara negativt. Då kommer intervallet att vara ordnat i fallande ordning. Observera att de två första argumenten har bytt plats här:

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

<programming-exercise name='Negatiivisesta positiiviseen' tmcname='osa04-11b_negatiivisesta_positiiviseen'>

Skapa ett program som ber användaren ge ett positivt heltal `n`. Programmet ska därefter skriva ut siffrorna i intervallet `-n ... n`, exklusive noll. Varje siffra skrivs ut på en skild rad.

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
siffror = range(2, 7)
print(siffror)
```

<sample-output>

range(2, 7)

</sample-output>

Funktionen `list` konverterar ett intervall till en lista. Listan kommer att innehålla de värden som finns i intervallet. I fortsättningskursen i Python som följer den här kursen kommer vi att gå djupare in på det här.

```python
siffror = list(range(2, 7))
print(siffror)
```

<sample-output>

[2, 3, 4, 5, 6]

</sample-output>

## En påminnelse om de automatiska testen

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

Från och med nu kommer det inte längre att finnas påminnelser om att använda `if __name__ == "__main__"` -blocket. De automatiska testen kommer fortsättningsvis ändå att kräva att de används, så du måste själv lägga till blocket i din kod när du testar dina funktioner inom programmets huvudfunktion.

Obs! Vissa övningar, som Palindrom i den här delen, förutsätter att du skriver kod som använder sig av den funktionen du gjort. Den här koden bör inte läggas i `if __name__ == "__main__"` -blocket. De automatiska testen kör ingen kod inom dessa block, så din lösning kommer inte att vara fullständig om du placerar dina funktionsanrop där.

<programming-exercise name='Tähdet' tmcname='osa04-12_tahdet'>

Skapa funktionen `lista_som_asterisker` som får som argument en lista med heltal. Funktionen ska skriva ut rader med asterisker så att siffrorna i listan indikerar antalet asterisker på en rad.

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

<!-- **Huomaa** että tällä hetkellä Windowsissa on ongelmia joidenkin tehtävien testien suorittamisessa. Jos törmäät seuraavaan virheilmoitukseen

<img src="4_3_2.png" alt="Listan iterointi">

voit suorittaa testit lähettämällä ne palvelimelle valitsemalla testien suoritusnapin oikealla puolella olevasta symbolista avautuvasta TMC-valikosta _Submit solutions_.

Ongelman saa korjattua menemällä laajennuksen asennusvalikkoon ja muuttamalla "TMC Data" -kohdassa tehtävien sijainnin johonkin toiseen sijaintiin, jonka tiedostopolku on lyhempi, allaolevassa kuvassa nappi _change path_. Siirrossa saattaa kestää hetken, joten odotathan operaation päättymistä.

<img src="4_3_3.png" alt="Listan iterointi">

Ongelmaan pyritään saamaan parempi ratkaisu lähipäivinä. -->

</programming-exercise>

<programming-exercise name='Anagrammi' tmcname='osa04-13_anagrammi'>

Skapa funktionen `anagram` som får två strängar som argument. Funktionen ska returnera `True` om strängarna är anagram – dvs. de bildas av exakt samma bokstäver.

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

<programming-exercise name='Palindromit' tmcname='osa04-14_palindromit'>

Skapa funktionen `palindrom` som får en sträng som argument. Funktionen ska returnera `True` om strängen är ett palindrom – dvs. den är den samma oberoende om man börjar läsa från vänster eller höger.

Skapa ett huvudprogram som ber användaren ange ord tills ett palindrom ges:

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

<programming-exercise name='Positiivisten summa' tmcname='osa04-15_positiivisten_summa'>

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

I dessa uppgifter kommer vi att använda listor som argument och return-värden. Det här såg vi på i den förra delen.

<programming-exercise name='Parilliset' tmcname='osa04-16_parilliset'>

Skapa funktionen `jamna` som får som argument en lista med heltal.

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

Skapa funktionen `summa` som får två listor som argument. Båda listorna har samma antal element, som består av heltal.

Funktionen ska returnera en ny lista vars element består av summorna av elementen i de urpsrungliga listorna.

Exempel:

```python
a = [1, 2, 3]
b = [7, 8, 9]
print(summa(a, b)) # [8, 10, 12]
```

</programming-exercise>

<programming-exercise name='Uniikit' tmcname='osa04-18_uniikit'>

Skapa funktionen `unika` som får som argument en lista med heltal.

Funktionen ska returnera en lista som innehåller den ursprungliga listans siffror i storleksordning. Varje siffra ska förekomma bara en gång.

```python
lista = [3, 2, 2, 1, 3, 3, 1]
print(unika(lista)) # [1, 2, 3]
```

</programming-exercise>

## Hitta det bästa eller sämsta värdet i en lista

En vanlig programmeringsuppgift är att hitta det bästa eller sämsta värdet i en lista enligt något visst kriterium. En enkel lösning är att använda en hjälpvariabel för att komma ihåg vilket av elementen tills vidare är det mest "optimala". Det här mest "optimala" jämförs med varje element och när loopen är klar kommer hjälpvariabeln att innehålla det värdet man söker efter.

Här är ett utkast som inte ännu fungerar:

```python
bast = start # det passliga startvärdet beror på situationen
for element in lista:
    if element bättre än bast:
        bast = element

# vi vet nu det bästa värdet
```

Detaljerna kring den slutliga koden beror på typen av elementen i listan och kriteriet för väljandet av det bästa (eller sämsta) elementet. Ibland kan du behöva fler än en hjälpvariabel.

Låt oss öva på den här metoden.

<programming-exercise name='Listan pisimmän pituus' tmcname='osa04-18a_listan_pimman_pituus'>

Skapa funktionen `langsta_langden` som får som argument en lista med strängar. Funktionen ska returnera längden på den längsta strängen i listan.

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

<programming-exercise name='Listan lyhin' tmcname='osa04-18b_listan_lyhin'>

Skapa funktionen `kortast` som får som argument en lista med strängar. Funktionen ska returnera listans kortaste sträng. Om det finns flera strängar med samma längd kan man returnera vilken som helst av dessa. Man kan anta at det inte finns tomma strängar (längd noll) i listan.


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

<programming-exercise name='Listan pisimmät' tmcname='osa04-19_listan_pisimmat'>

Skapa funktionen `langsta` som får som argument en lista med strängar. Funktionen ska returnera en lista som innehåller den längsta strängen i listan. Om de finns flera strängar med samma längd skrivs de alla ut i listan, i den ordning som de förekommer i den ursprungliga listan.

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

<quiz id="ddf4bfa0-6a65-5efa-ba7d-e3e0cd3217fc"></quiz>
