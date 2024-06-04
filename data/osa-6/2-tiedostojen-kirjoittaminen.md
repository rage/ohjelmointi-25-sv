---
path: '/osa-6/2-tiedostojen-kirjoittaminen'
title: 'Skriva filer'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* kan du skapa filer med Python
* kan du skriva textdata till en fil
* vet du hur man skapar en CSV-fil.

</text-box>

Nu har vi sett hur man kan läsa data från filer, men det är naturligtvis också möjligt att skriva data till filer. I en vanlig situation behandlar programmet någon data och skriver det i en fil, så att det kan senare användas eller behandlas vidare av något annat program.

Vi kan skapa en ny fil varje gång vi vill skriva data, men vi kan också lägga till data i en fil som redan finns. I båda fallen använder vi `open`-funktionen som vi bekantade oss med i den förra delen. För att skriva filer måste vi ge funktionen ett andra argument.

## Skapa en fil

Om du vill skapa en ny fil ska du anropa funktionen `open` med `w` som andra argument. Det här indikerar att filen ska öppnas i skrivläge. Funktionsanropet skulle då kunna se ut så här:

```python
with open("ny_fil.txt", "w") as fil:
    # vi skriver till filen här
```

Obs! Om filen redan finns, kommer allt innehåll att skrivas över. Man ska vara väldigt försiktig när man skapar nya filer.

När filen är öppen, kan du skriva data i den. Du kan använda metoden `write`, som tar strängen som ska skrivas som sitt argument:

```python
with open("ny_fil.txt", "w") as fil:
    fil.write("Hej alla!")
```

När du kör programmet, dyker en ny fil med namnet `ny_fil.txt` upp i mappen. Innehållet borde se ut så här:

<sample-data>

Hej alla!

</sample-data>

Om du vill ha radbyten i filen, måste du lägga till dem för hand. Funktionen `write` fungerar inte som print-funktionen, även om de har likheter. Följande program…

```python
with open("ny_fil.txt", "w") as fil:
    fil.write("Hej alla!")
    fil.write("Andra raden")
    fil.write("Sista raden")
```

…skulle resultera i en fil som denna:

<sample-data>

Hej alla!Andra radenSista raden

</sample-data>

Radbrytningar får man till stånd med att inkludera `\n` i strängarna som ges som argument till `write`-funktionen:

```python
with open("ny_fil.txt", "w") as fil:
    fil.write("Hej alla!\n")
    fil.write("Andra raden\n")
    fil.write("Sista raden\n")
```

Nu borde innehållet i `ny_fil.txt` se ut så här:

<sample-data>

Hej alla!
Andra raden
Sista raden

</sample-data>

<programming-exercise name='Omistuskirjoitus' tmcname='osa06-10_omistuskirjoitus'>

Skapa ett program som ber om ett namn och skapar en liten text som är tillägnad till personen i fråga. Texten ska sparas i en fil. Exempel:

<sample-output>

Tillägnas till: **Stella**
Skrivs till: **till_min_van.txt**

</sample-output>

Innehållet i `till_min_van.txt` är:

<sample-data>

Hej Stella! Vi önskar dig trevliga stunder med Python-kursmaterialet. Mvh. MOOC-teamet

</sample-data>

Obs! I dessa uppgifter ska kod inte placeras i `if __name__ == "__main__"` -blocket, om du inte ombeds göra det.

</programming-exercise>

## Lägga till data i en befintlig fil

Om du vill lägga till data i slutet av en fil istället för att skriva över en hel fil, kan du använda argumentet `a` istället för `w`.

Om filen inte ännu finns, fungerar det här läget på samma sätt som skrivläget.

Följande program öppnar filen `ny_fil.txt` och lägger till några rader text i slutet:

```python
with open("ny_fil.txt", "a") as fil:
    fil.write("Rad fyra\n")
    fil.write("Ännu en till rad\n")
```

När programmet körs, borde innehållet i filen se ut på följande sätt:

<sample-output>

Hej alla!
Andra raden
Sista raden
Rad fyra
Ännu en till rad

</sample-output>

I praktiken är det inte så vanligt att man lägger till innehåll i en befintlig fil.

Oftare läser man en fil, behandlar man data och till sist skrivs filen över med nya data. Till exempel om man vill ändra på innehållet i mitten av en fil, är det vanligtvis enklast att skriva över hela filen.

<programming-exercise name='Päiväkirja' tmcname='osa06-11_paivakirja'>

Skapa ett program som låter användaren skapa en enkel dagbok. Dagboksinläggen ska lagras i filen `dagbok.txt`. När programmet körs läses inläggen in från filen.

Obs! De lokala testen kan ändra på filens innehåll. Skapa alltså en kopia av filen om du vill behålla dess innehåll.

Programmet ska fungera så här:

<sample-output>

1 – lägg till inlägg, 2 – läs inlägg, 0 – avsluta
Val: **1**
Skriv inlägg: **Idag åt jag gröt**
Sparat

1 – lägg till inlägg, 2 – läs inlägg, 0 – avsluta
Val: **2**
Inlägg:
Idag åt jag gröt
1 – lägg till inlägg, 2 – läs inlägg, 0 – avsluta
Val: **1**
Skriv inlägg: **På kvällen var jag i bastu**
Sparat

1 – lägg till inlägg, 2 – läs inlägg, 0 – avsluta
Val: **2**
Inlägg:
Idag åt jag gröt
På kvällen var jag i bastu
1 – lägg till inlägg, 2 – läs inlägg, 0 – avsluta
Val: **0**
Hejdå!

</sample-output>

Vi startar programmet på nytt:

<sample-output>

1 – lägg till inlägg, 2 – läs inlägg, 0 – avsluta
Val: **2**
Inlägg:
Idag åt jag gröt
På kvällen var jag i bastu
1 – lägg till inlägg, 2 – läs inlägg, 0 – avsluta
Val: **0**
Hejdå!

</sample-output>

Obs! I dessa uppgifter ska kod inte placeras i `if __name__ == "__main__"` -blocket, om du inte ombeds göra det.

</programming-exercise>

## Skriva CSV-filer

CSV-filer kan skrivas rad för rad med `write`-metoden, precis som med vilken som helst annan fil. Det följande exemplet skapar filen `programmerare.csv` som innehåller namnet, programmeringsmiljön, favoritprogrammeringsspråket och antalet år arbetserfarenhet hos en programmerare. Fälten skiljs åt med semikolon.

```python
with open("programmerare.csv", "w") as fil:
    fil.write("Erik;Windows;Pascal;10\n")
    fil.write("Mats;Linux;PHP;2\n")
    fil.write("Anton;Linux;Java;17\n")
    fil.write("Emilia;Mac;Cobol;9\n")
```

När programmet körs får vi följande fil:

<sample-output>

Erik;Windows;Pascal;10
Mats;Linux;PHP;2
Anton;Linux;Java;17
Emilia;Mac;Cobol;9

</sample-output>

Hur är det om data som ska skrivas finns i en lista i datorns minne?

```python
programmerare = []
programmerare.append(["Erik", "Windows", "Pascal", 10])
programmerare.append(["Mats", "Linux", "PHP", 2])
programmerare.append(["Anton", "Linux", "Java", 17])
programmerare.append(["Emilia", "Mac", "Cobol", 9])
```

Vi kan konstruera den sträng som vi vill skriva som en f-sträng, och skriva den klara raden i filen:

```python
with open("programmerare.csv", "w") as fil:
    for person in programmerare:
        rad = f"{person[0]};{person[1]};{person[2]};{person[3]}"
        fil.write(rad+"\n")
```

Om varje lista skulle vara väldigt lång, skulle det vara arbetsdrygt att konstruera strängen för hand och då skulle vi istället kunna använda en for-loop:

```python
with open("programmerare.csv", "w") as fil:
    for person in programmerare:
        rad = ""
        for varde in person:
            rad += f"{varde};"
        rad = rad[:-1]
        fil.write(rad+"\n")
```

## Tömma innehållet i en fil och ta bort en fil

Ibland behöver vi tömma innehållet i en fil. Då kan vi helt enkelt öppna filen i skrivläge och därefter stänga filen:

```python
with open("fil_som_ska_tommas.txt", "w") as fil:
    pass
```

Observera att `with`-blocket nu bara innehåller kommandot `pass`, som inte gör något. Python tillåter inte tomma block, så därför använder vi det här kommandot här.

Det är också möjligt att undvika `with`-blocket och istället använda följande kommando:

```python
open('fil_som_ska_tommas.txt', 'w').close()
```

<text-box variant='hint' name='Ta bort filer'>

Du kan också helt och hållet avlägsna en fil. Vi måste be operativsystemet om hjälp för att uppnå detta:

```python
# det här behöver vi för att kunna använda remove-funktionen
import os

os.remove("onodig_fil.csv")
```

Obs! Det här fungerar inte i testmiljön som används för de automatiska testen. Om du ombeds tömma innehållet i en fil, ska du använda någon av metoderna som beskrevs ovan.

</text-box>


<programming-exercise name='Aineiston suodatus' tmcname='osa06-12_aineiston_suodatus'>

I filen `kalkyler.csv` finns lösningar på uppgifter enligt följande exempel:

```csv
Anton;2+5;7
Pärla;3-2;1
Erik;9+3;11
Anton;8-3;4
Pärla;5+5;10
o.s.v. ...
```

Formatet för varje rad är alltså `studerande;uppgift;resultat`. Uppgifterna är alltså additions- eller subtraktionsräkningar med två operander.

Skapa funktionen `ordna_uppgifter()` som

* läser innehållet i `kalkyler.csv`
* skriver filen `korrekta.csv` med de uppgifter som är korrekt lösta
* skriver filen `inkorrekta.csv` med de övriga uppgifterna.

Filen `korrekta.csv` skulle se ut så här med det föregående exemplet:

```sh
Anton;2+5;7
Pärla;3-2;1
Pärla;5+5;10
```

De två resterande raderna skulle vara i `inkorrekta.csv`.

Raderna ska förekomma i samma ordning som i den ursprungliga filen. Ändra inte på den filen.

Märk att funktionen ska fungera oavsett hur många gånger den anropas:

```python
suodata_laskut()
```

och...

```python
suodata_laskut()
suodata_laskut()
suodata_laskut()
suodata_laskut()
```

...ska ge likadant slutresultat.

</programming-exercise>

<programming-exercise name='Henkilöt talteen' tmcname='osa06-13_henkilot_talteen'>

Skapa funktionen `spara_person(person: tuple)` som får som argument en tuple som representerar en person. Tuplen innehåller följande information:

1. Namn (sträng)
1. Ålder (heltal)
1. Längd (flyttal)

Spara informationen i filen `personer.csv`, efter befintliga data. Formatet ska vara `namn;ålder;längd`. En person är alltså lika med en rad. Om tuplen är `("Sara Simonsson", 37, 175.5)` skulle programmet skriva följande rad i slutet av filen:

```
Sara Simonsson;37;175.5
```

</programming-exercise>

## Behandla data i CSV-format

Låt oss skapa ett program som utvärderar elevernas framgång under en kurs. Programmet läser en CSV-fil som innehåller de veckovisa poängen som den studerande fått under kursens lopp. Programmet räknar ihop poängen och utvärderar därefter vilket vitsord de räcker till. Till slut skapar programmet en CSV-fil som innehåller poängsumman och vitsordet för varje elev.

CSV-filen som vi har tillgång till när vi börjar ser ut så här:

<sample-data>

Pärla;4;2;3;5;4;0;0
Paula;7;2;8;3;5;4;5
Pirjo;3;4;3;5;3;4;4
Emilia;6;6;5;5;0;4;8

</sample-data>

Programmets logik är uppdelad i tre funktioner: läsande av filen och behandlande av innehållet, vitsordsberäkning och skrivande av en ny fil.

Filens inläsning sker enligt det vi lärt oss i den förra delen. Data lagras i ett lexikon där nyckeln är elevens namn och värdet är en lista på poängen som eleven i fråga har fått, i heltalsform:

```python
def las_veckopoang(filnamn):
    veckopoang = {}
    with open(filnamn) as fil:
        for rad in fil:
            delar = rad.split(";")
            lista = []
            for poang in delar[1:]:
                lista.append(int(poang))
            veckopoang[delar[0]] = lista

    return veckopoang
```

Den andra funktionen beräknar vilket vitsord ett visst antal poäng räcker till. Funktionen används av den tredje funktionen, som skriver resultaten i en fil:

```python
def vitsord(poang):
    if poang < 20:
        return 0
    elif poang < 25:
        return 1
    elif poang < 30:
        return 2
    elif poang < 35:
        return 3
    elif poang < 40:
        return 4
    else:
        return 5

def spara_resultat(filnamn, veckopoang):
    with open(filnamn, "w") as fil:
        for namn, lista in veckopoang.items():
            summa = sum(lista)
            fil.write(f"{namn};{summa};{vitsord(summa)}\n")
```

Strukturen tillåter oss skapa en mycket enkel huvudfunktion. Observera att filnamnen ges som argument i huvudfunktionen:

```python
veckopoang = las_veckopoang("veckopoang.csv")
spara_resultat("resultat.csv", veckopoang)
```

När huvudfunktionen körs, skapas filen `resultat.csv` med följande innehåll:

<sample-data>

Pärla;18;0
Paula;34;3
Pirjo;26;2
Emilia;41;5

</sample-data>

Notera att alla funktioner ovan är relativt enkla till sin funktionalitet – de har en uppgift var. Det här är ett vanligt och rekommenderat sätt att skapa större helheter när man programmerar. När en funktion har en uppgift är det enklare att säkerställa att den fungerar på önskat sätt. Det här gör det också enklare att senare ändra på programmet och lägga till ny funktionalitet.

Om vi till exempel vill ha en funktion för att skriva ut vitsordet för enskild studerande, kan vi skapa en ny funktion som använder sig av en befintlig funktion i koden:

```python
def hamta_vitsord(person, veckopoang):
    for namn, lista in veckopoang.items():
        if namn == person:
            return vitsord(sum(lista))


veckopoang = las_veckopoang("veckopoang.csv")
print(hamta_vitsord("Paula", veckopoang))

```

<sample-data>

3

</sample-data>

Om vi märker att någon funktionalitet i programmet kräver åtgärdande, kommer ändringar inte att orsaka följder överallt i koden. Om vi till exempel vill ändra på vitsordsgränserna, behöver vi bara ändra på funktionen som räknar ut vitsordet – alla andra funktioner som använder den här funktionen skulle fortfarande fungera, med de nya gränserna. Om koden för den här funktionaliteten skulle vara splittrad, finns det en risk att vi glömmer att uppdatera koden på något ställe. Det här skulle antagligen orsaka problem.

<programming-exercise name='Kurssin tulokset, osa 4' tmcname='osa06-14_kurssin_tulokset_osa4'>

Vi utvecklar ännu lite programmet som genererar kursresultat.

För tillfället läses studerandenas namn, uppgifts- och provpoäng från respektive filer. Vi ändrar på programmet så att också kursens namn och studiepoäng läses in från en fil. Formatet är det följande:

<sample-data>

<pre>

namn: Introkurs i programmering
sp: 5
</pre>

</sample-data>

Programmet ska skapa två filer. Filen `resultat.txt` ska följa det här formatet:

<sample-data>

<pre>
Introkurs i programmering, 5 studiepoäng
========================================
namn                          uppg_ant  uppg_poang  provpoang  tot_poang  vitsord
pekka peloton                 21        5           9          14         0
jaana javanainen              27        6           11         17         1
liisa virtanen                35        8           14         22         3
</pre>

</sample-data>

Den här delen liknar alltså utskriften från den förra versionen av programmet.

Dessutom ska filen `resultat.csv` skapas. Dess format ska följa detta exempel:

<sample-data>

<pre>
12345678;pekka peloton;0
12345687;jaana javanainen;1
12345699;liisa virtanen;3
</pre>

</sample-data>

Exempelkörning:

<sample-output>

Studerande (CSV): **studerande1.csv**
Uppgifter (CSV): **uppgifter1.csv**
Provpoäng (CSV): **provpoang1.csv**
Kursinfo (textfil): **kurs1.txt**
Resultaten lagrade i filerna resultat.txt och resultat.csv

</sample-output>

Programmet frågar bara alltså om filnamnen och skriver resultaten i resultatfilerna.

Obs! I dessa uppgifter ska kod inte placeras i `if __name__ == "__main__"` -blocket, om du inte ombeds göra det.

</programming-exercise>



<programming-exercise name='Sanahaku' tmcname='osa06-15_sanahaku'>

I den här uppgiften behandlar vi filen `ord.txt` som innehåller ord på engelska.

Skapa funktionen `sok_ord(term: str)` som returnerar en lista över matchande ord i filen.

I söktermen kan man, förutom gemener, använda dessa specialtecken:

* punkt betyder att vilket som helst tecken accepteras (`ca.` matchar t.ex. cat och car och `.a.e` care och late)
* asterisk betyder att ordet kan börja eller avslutas på valfritt vis (`ca*` matchar t.ex. california och cat, `*ane` matchar insane och aeroplane) – du kan anta att asterisken endast finns i början eller slutet av ett ord och att söktermen innehåller högst en asterisk
* om söktermen inte innehåller specialtecken ska termen matcha exakt med det sökta ordet.

Vi bestämmer också att en sökterm inte kan innehålla båda typer av specialtecken.

Orden är skrivna med gemener. Du kan också anta att argumentet inte innehåller versaler.

Om inga resultat hittas ska funktionen returnera en tom lista.

Tips: Pythons strängmetoder `startswith()` och `endswith()` kan vara händiga. Sök på nätet för mera information.

Exempel:

```python

print(sok_ord("*vokes"))

```

<sample-output>

['convokes', 'equivokes', 'evokes', 'invokes', 'provokes', 'reinvokes', 'revokes']

</sample-output>

</programming-exercise>

<programming-exercise name='Muistava sanakirja' tmcname='osa06-16_muistava_sanakirja'>

Skapa ett program som fungerar som en ordbok, dit man kan lägga till nya ord eller där man kan söka efter befintliga ord.

Programmet ska fungera så här:

<sample-output>

1 – lägg till ord, 2 – sök ord, 3 – avsluta
Val: **1**
Ange ord på svenska: **bil**
Ange ord på engelska: **car**
Ordpar tillagt
1 – lägg till ord, 2 – sök ord, 3 – avsluta
Val: **1**
Ange ord på svenska: **sopa**
Ange ord på engelska: **garbage**
Ordpar tillagt
1 – lägg till ord, 2 – sök ord, 3 – avsluta
Val: **1**
Ange ord på svenska: **väska**
Ange ord på engelska: **bag**
Ordpar tillagt
1 – lägg till ord, 2 – sök ord, 3 – avsluta
Val: **2**
Ange ord: **bag**
sopa - garbage
väska - bag
1 – lägg till ord, 2 – sök ord, 3 – avsluta
Val: **2**
Ange ord: **car**
bil - car
1 – lägg till ord, 2 – sök ord, 3 – avsluta
Val: **2**
Ange ord: **väska**
väska - bag
1 – lägg till ord, 2 – sök ord, 3 – avsluta
Val: **3**
Hejdå!

</sample-output>

Orden ska lagras i filen `ordbok.txt`. Programmet ska läsa in den här filen när det startar. Nya ordpar läggs till genast.

Du kan själv bestämma i vilket format data lagras.

Observera att körande av de lokala testen kan tömma ordboksfilen.

Obs! I dessa uppgifter ska kod inte placeras i `if __name__ == "__main__"` -blocket, om du inte ombeds göra det.

</programming-exercise>

<quiz id="58b92c76-559a-588f-8662-6c430d212bc2"></quiz>
