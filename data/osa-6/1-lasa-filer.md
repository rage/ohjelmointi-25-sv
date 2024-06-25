---
path: '/osa-6/1-lasa-filer'
title: 'Läsa filer'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* kan du läsa en fil med Python
* vet du vad en textfil och en CSV-fil är
* kan du behandla innehållet i en CSV-fil i dina program.

</text-box>

<!--vastaava teksti löytyy osioista 3-1, 5-1 ja 6-1, tsekkaa kaikki jos muokkaat tätä-->
<text-box variant='hint' name='Om uppgifterna i den här kursen'>

Att bli en skicklig programmerare kräver mycket övning. Man måste utveckla en problemlösningsförmåga och ha en förmåga att intuition komma fram till korrekta lösningar. Därför finns det massor av övningar av olika typer i den här kursen. Vissa övningar är enklare och baserar sig mera eller mindre direkt på materialet medan andra uppgifter är svårare och kräver tillämpande av kunskaper som man lärt sig under kursen.

En del uppgifter kan kännas svåra, men det är inte något att oroa sig över. Ingen av uppgifterna är obligatorisk och du behöver bara 25 % av poängen från varje modul för att klara den här kursen. Du kan läsa mera på kursens bedömningssida.

Uppgifterna är inte i svårighetsordning. Varje del introducerar vanligtvis några nya saker inom programmering och i samband finns relaterade uppgifter – både enklare och svårare. Om du stöter på en uppgift som känns oöverkomlig ska du fortsätta till nästa uppgift. Du kan alltid senare återkomma till tidigare uppgifter.

En uppgift som känns för svår just nu kommer sannolikt att vara ganska enkel om en månad.

</text-box>

När man programmerar kan det uppstå ett behov att behandla data som finns lagrad i filer. Datorprogram kan läsa data från filer och skriva data till filer. Också stora mängder data i filer kan enkelt behandlas automatiskt.

Under den här kursen kommer vi endast att arbeta med textfiler. De här filerna består av rader med text. Till exempel kodeditorn Visual Studio Code är kompatibel med textfiler. Obs! Även om ordbehandlingsprogram som Microsoft Word ofta används med filer som innehåller text, är Word-dokument inte textfiler. Dokumenten innehåller också annan information om till exempel textformat, vilket gör det mer komplicerat att behandla filerna i ett program.

## Att läsa data från en fil

Vi börjar att arbeta med filen `exempel.txt` som innehållet det följande:

<sample-data>

Hej alla!
Vår exempelfil består av tre rader.
Det här är den sista raden.

</sample-data>

Ett enkelt sätt att använda filer i Python är med `with`-satsen. Den inledande raden öppnar filen och blocket där vi kan komma åt filen följer. Efter blocket stängs filen automatiskt och då kan den inte mera behandlas.

Den här koden öppnar alltså filen, läser dess innehåll och skriver det ut, och till slut stängs filen:

```python
with open("exempel.txt") as fil:
    innehall = fil.read()
    print(innehall)
```

<sample-output>

Hej alla!
Vår exempelfil består av tre rader.
Det här är den sista raden.

</sample-output>

Variabeln `fil` är en file handle ("filhandtag"). Via variabeln kan vi komma åt filen så länge den är öppen. Här använde vi metoden `read` som returnerar filens innehåll som en hel sträng. I det här fallet skulle strängen se ut så här:

```
"Hej alla!\nVår exempelfil består av tre rader.\nDet här är den sista raden."
```

## Gå igenom innehållet i en fil

Metoden `read` fungerar väl för att skriva ut hela innehållet i en fil, men ofta vill vi gå igenom innehållet rad för rad.

Man kan tänka att textfiler är som listor med strängar, där varje sträng finns på sin egen rad i filen. Vi kan gå igenom listan med en for-loop.

Följande exempel läser in vår exempelfil med hjälp av en for-loop, tar bort radbrytningarna, räknar antalet rader och skriver ut varje rad med sitt radnummer. Programmet håller också koll på radernas längder:

```python
with open("exempel.txt") as fil:
    raknare = 0
    totallangd = 0

    for rad in fil:
        rad = rad.replace("\n", "")
        raknare += 1
        print("Rad", raknare, rad)
        langd = len(rad)
        totallangd += langd

print("Radernas totallängd:", totallangd)
```

<sample-output>

Rad 1 Hej alla!
Rad 2 Vår exempelfil består av tre rader.
Rad 3 Det här är den sista raden.
Radernas totallängd: 63

</sample-output>

Det finns en radbrytning `\n` i slutet av varje rad i filen, men `print`-funktionen lägger också automatiskt till en rad i slutet av utskriften. Det finns inga extra radbyten i utskriften ovan eftersom radbrytningarna avlägsnats med hjälp av `replace`-metoden. Metoden ersätter alla radbrytningstecken med en tom sträng. I och med detta räknas radernas längder också korrekt.

<programming-exercise name='Största siffran' tmcname='osa06-01_storsta_siffran'>

I filen `siffror.txt` finns siffror listade på olika rader enligt exemplet nedan:

```sh
2
45
108
3
-10
1100
o.s.v. ...
```

Skapa funktionen `storst` som ska läsa filen och returnera den största siffran som hittas.

Observera att filnamnet alltid är `siffror.txt` och att funktionen inte har några parametrar.

Obs! Om Visual Studio Code inte hitta din fil även om namnet är korrekt skrivet ska du följa instruktionerna nedan.

</programming-exercise>

## Om Visual Studio Code inte hittar min fil?

När du kör din kod är det möjligt att Visual Studio Code meddelar att filen – även efter att du kollat att filen finns och att namnet är korrekt skrivet. Att ändra på följande inställning kan lösa problemet:

* öppna inställningarna från menyraden: File -> Preferences -> Settings
* sök efter den inställning som ska ändras med sökordet "executeinfile"
* välj fliken Workspace
* bocka i valet under Python -> Terminal -> Execute in file dir.

Inställningsfönstret borde ungefär se ut så här:

<img src="6_1_1.png">

Om det här inte fungerar kan du kopiera filen i src-mappen…

<img src="6_1_2.png">

…direkt till roten av uppgiftsmappen:

<img src="6_1_3.png">

## Att debugga kod som behandlar filer

När man använder Visual Studio Codes debuggare med program som behandlar filer, kan man stöta på följande felmeddelande:

<img src="6_1_4.png">

Orsaken är att debuggaren alltid söker efter filer i roten av uppgiftsmappen. Inställningen Execute in file dir som nämndes ovan har ingen påverkan här. Den enklaste lösningen är att kopiera filen till rotmappen.

Du behöver kanske också starta om Visual Studio Code efter att du har kopierat alla filer som behövs.

## Läsa CSV-filer

En CSV-fil (kommaseparerade värden) är en textfil som innehåller data som separerats med ett visst tecken. Det här tecknet är vanligtvis komma (`,`) eller semikolon (`;`), men vilket som helst tecken är i princip möjligt.

CSV-filer är ett vanligt sätt att lagra olika typer av data. Flera databaser och kalkylprogram – exempelvis Excel – kan importera och exportera data i CSV-format. Det här möjliggör enkel dataöverföring mellan olika system.

Vi har redan bekantat oss med hur man kan gå igenom rader i en fil med en for-loop, men hur kan vi separera fält på en och samma rad? Python har en strängmetod `split`, som kan användas för detta. Metoden tar separatortecknet eller -tecknen som ett strängargument och returnerar innehållet i den ursprungliga strängen som en lista av strängar – separerade vid separatortecknen.

Här finns ett exempel för att tydliggöra det här:

```python
text = "apa,banan,cembalo"
ordlista = text.split(",")
for ord in ordlista:
    print(ord)
```

<sample-output>

apa
banan
cembalo

</sample-output>

Låt oss säga att vi har filen `vitsord.csv`, som innehåller namn på elever samt vitsord de fått av olika kurser. Varje rad har data som tillhör en studerande och data separeras med semikolon.

<sample-data>

Peter;5;4;5;3;4;5;5;4;2;4
Pauline;3;4;2;4;4;2;3;1;3;3
Pia;4;5;5;4;5;5;4;5;4;4

</sample-data>

Följande program går igenom filen rad för rad, delar upp raderna i delar och skriver ut namnen på eleverna samt deras vitsord:

```python
with open("vitsord.csv") as fil:
    for rad in fil:
        rad = rad.replace("\n", "")
        delar = rad.split(";")
        namn = delar[0]
        vitsord = delar[1:]
        print("Namn:", namn)
        print("Vitsord:", vitsord)
```

<sample-output>

Namn: Peter
Vitsord: ['5', '4', '5', '3', '4', '5', '5', '4', '2', '4']
Namn: Pauline
Vitsord: ['3', '4', '2', '4', '4', '2', '3', '1', '3', '3']
Namn: Pia
Vitsord: ['4', '5', '5', '4', '5', '5', '4', '5', '4', '4']

</sample-output>

<programming-exercise name='Fruktaffär' tmcname='osa06-02_fruktaffar'>

I filen `frukter.csv` finns frukter med deras pris enligt exemplet nedan:

```sh
banan;6.50
äpple;4.95
apelsin;8.0
o.s.v. ...
```

Skapa funktionen `las_frukter` som ska läsa filen och skapa ett lexikon där nyckeln är fruktens namn och värdet fruktens pris. Priset ska vara av typen `float`.

Observera att filnamnet alltid är `frukter.csv` och funktionen har inga parametrar.

Funktionen ska till slut returnera lexikonet.

Obs! Om Visual Studio Code inte hittar filen även om namnet är korrekt skrivet, ska du följa instruktionerna här.

</programming-exercise>

<programming-exercise name='Matris' tmcname='osa06-03_matris'>

I filen `matris.txt` finns en matris enligt exemplet nedan:

```sh
1,0,2,8,2,1,3,2,5,2,2,2
9,2,4,5,2,4,2,4,1,10,4,2
o.s.v. ...
```

Skapa funktionerna `summa` och `maximum` som returnerar summan av elementen i matrisen respektive det största elementet.

Skapa också funktionen `radsummor` som returnerar som en lista summorna av matrisens rader. Till exempel för matrisen...

```sh
1,2,3
2,3,4
```

...returnerar funktionen `[6, 9]`.

Tips: Du kan också implementera andra funktioner i programmet. Fundera vilka gemensamma funktioner de ovan nämnda funktionerna kan behöva.

Observera att filen alltid heter `matris.txt` och funktionerna inte har parametrar. Ytterligare funktioner du eventuellt skapar kan ha parametrar.

Obs! Om Visual Studio Code inte hittar filen även om namnet är korrekt skrivet, ska du följa instruktionerna här.

</programming-exercise>

## Läsa samma fil flera gånger

Ibland kan man behöva läsa innehållet i en fil flera gånger i samma program. Vi tittar på ett program som behandlar data om några personer i en CSV-fil:

<sample-data>
Peter;40;Helsingfors
Emilia;34;Esbo
Erik;42;Åbo
Antonia;100;Helsingfors
Lisa;58;Suonenjoki
</sample-data>

```python
with open("personer.csv") as fil:
    # skriver ut namn
    for rad in fil:
        delar = rad.split(";")
        print("Namn:", delar[0])

    # söker efter den äldsta personen
    hogsta_aldern = -1
    for rad in fil:
        delar = rad.split(";")
        namn = delar[0]
        alder = int(delar[1])
        if alder > hogsta_aldern:
            hogsta_aldern = alder
            aldst = namn
    print("Den äldsta är", aldst)
```

När vi kör programmet får vi det här felmeddelandet:

```python
Traceback (most recent call last):
    print("Den äldsta är"; aldst)
UnboundLocalError: local variable 'aldst' referenced before assignment
```

Orsaken till at det här sker är att den andra for-loopen aldrig körs. Detta eftersom filen endast kan behandlas en gång. När den sista raden har lästs stannar file handlen i slutet av filen och data i filen kan inte längre kommas åt.

Om vi vill komma åt innehållet i filen i den andra for-loopen, måste vi öppna filen på nytt:

```python
with open("personer.csv") as fil:
    # skriver ut namn
    for rad in fil:
        delar = rad.split(";")
        print("Namn:", delar[0])

with open("personer.csv") as fil:
    # söker efter den äldsta personen
    hogsta_aldern = -1
    for rad in fil:
        delar = rad.split(";")
        namn = delar[0]
        alder = int(delar[1])
        if alder > hogsta_aldern:
            hogsta_aldern = alder
            aldst = namn
    print("Den äldsta är", aldst)
```

Även om den ovanstående koden fungerar, innehåller den onödig upprepning. Det lönar sig vanligtvis att läsa filen bara en gång, och spara dess innehåll i ett passligt format för fortsatt behandling:

```python
personer = []
# vi läser in personerna till listan
with open("personer.csv") as fil:
    for rad in fil:
        delar = rad.split(";")
        personer.append((delar[0], int(delar[1]), delar[2]))

# skriver ut namn
for person in personer:
    print("Namn:", person[0])

# söker efter den äldsta personen
hogsta_aldern = -1
for person in personer:
    namn = person[0]
    alder = person[1]
    if alder > hogsta_aldern:
        hogsta_aldern = alder
        aldst = namn
print("Den äldsta är", aldst)
```

## Mera om att behandla CSV-filer

Vi fortsätter behandla filen `vitsord.csv`, som innehåller det följande:

<sample-data>

Peter;5;4;5;3;4;5;5;4;2;4
Pauline;3;4;2;4;4;2;3;1;3;3
Pia;4;5;5;4;5;5;4;5;4;4

</sample-data>

Följande program skapar lexikonet `vitsord` baserat på innehållet i filen. Nycklarna är elevernas namn och värdet som är kopplat till nycklarna innehåller elevens vitsord. Programmet konverterar vitsorden till heltal så att de kan behandlas enklare.

```python
vitsord = {}
with open("vitsord.csv") as fil:
    for rad in fil:
        rad = rad.replace("\n", "")
        delar = rad.split(";")
        namn = delar[0]
        vitsord[namn] = []
        for givet_vitsord in delar[1:]:
            vitsord[namn].append(int(givet_vitsord))

print(vitsord)
```

<sample-output>

{'Peter': [5, 4, 5, 3, 4, 5, 5, 4, 2, 4], 'Pauline': [3, 4, 2, 4, 4, 2, 3, 1, 3, 3], 'Pia': [4, 5, 5, 4, 5, 5, 4, 5, 4, 4]}

</sample-output>

Nu kan vi skriva ut statistik om varje studerande, baserat på värdena i lexikonet:

```python
for namn, lista in vitsord.items():
    basta = max(lista)
    medeltal = sum(lista) / len(lista)
    print(f"{namn}: bästa vitsordet {basta}, medeltal {medeltal:.2f}")
```

<sample-output>

Peter: bästa vitsordet 5, medeltal 4.10
Pauline: bästa vitsordet 4, medeltal 2.90
Pia: bästa vitsordet 5, medeltal 4.50

</sample-output>

Ta en titt på programmet i exemplet ovan. Det kan verka något komplicerat på en första titt, men tekniken kan användas med flera olika typer av data.

## Ta bort överflödiga rader, mellanslag och radbrytningar

Låt oss säga att vi har en CSV-fil med namn, exporterat från Excel:

```sh
förnamn; efternamn
Peter; Python
Jaana; Java
Heikki; Haskell
```

Excel är ökänt för att lägga till extra mellanrum lite här och där. Här har vi ett extra mellanrum mellan elementen, efter varje semikolon.

Vi skulle vilja skriva ut efternamnet på varje person som finns i listan. Den första raden i filen innehåller information om den data som följer och kan skippas:

```python
efternamn = []
with open("personer.csv") as fil:
    for rad in fil:
        delar = rad.split(";")
        # skippar raden med rubriker
        if delar[0] == "förnamn":
            continue
        efternamn.append(delar[1])

print(efternamn)
```

När koden körs får vi den här utskriften:

<sample-output>

[' Python\n', ' Java\n', ' Haskell']

</sample-output>

De två första elementen har ett radbrytningstecken i slutet och alla tre element har ett mellanslag i början. Vi har redan använt `replace`-metoden för att ta bort onödigt mellanrum, men ett bättre sätt är `strip`-metoden hos strängar. Den här metoden tar bort mellanrum från början och slutet av en sträng. Metoden tar bort mellanrum, radbrytningar, samt tabb- och andra tecken som normalt inte skulle skrivas ut.

Vi kan testa på metoden i Python-terminalen:

```python
>>> " prov ".strip()
'prov'
>>> "\n\ntest\n".strip()
'test'
>>>
```

Att ta bort de onödiga tecknen kräver bara en liten ändring i programmet:

```python
efternamn = []
with open("personer.csv") as fil:
    for rad in fil:
        delar = rad.split(';')
        if delar[0] == "förnamn":
            continue # skippar raden med rubriker
        efternamn.append(delar[1].strip())
print(efternamn)
```

Nu har får vi den önskade utskriften:

<sample-output>

['Python', 'Java', 'Haskell']

</sample-output>

Strängmetoderna `lstrip` och `rstrip` fungerar lika som metoden `strip`, men gör det då bara för antingen vänstra (l) eller högra (r) kanten av strängen:

```python
>>> " teststräng  ".rstrip()
' teststräng'
>>> " teststräng  ".lstrip()
'teststräng  '
```

## Kombinera data från olika filer

Det är mycket vanligt att data som behandlas av ett program finns utspritt i flera filer. Vi tar en titt på ett exempel där personalens information i ett företag finns i filen `personal.csv`:

```csv
personnr;namn;adress;adressort
080488-123X;Peter Mikkola;Filpusvägen 7;00700 HELSINGFORS
290274-044S;Lisa Marttinen;Mannerheimvägen 100 A 10;00100 HELSINGFORS
010479-007Z;Arto Vihavainen;Tiilitehtaankatu 10;04260 KERAVA
010499-345K;Leevi Hellas;Tapiolavägen 9;02100 ESBO
```

Löneuppgifterna finns i en skild fil, `lon.csv`:

```csv
personnr;lön;bonus
080488-123X;3300;0
290274-044S;4150;200
010479-007Z;1300;1200
```

Alla rader i båda filerna innehåller en personlig id-kod (pic) som identifierar vems data vi arbetar med. När vi använder det här id:t som gemensam faktor, är det lätt att koppla en arbetstagares namn med hennes lön. Vi kan till exempel skriva ut en lista över de månatliga inkomsterna:

<sample-output>

<pre>
inkomster:
Peter Mikkola    3300 euro
Lisa Marttinen   4350 euro
Arto Vihavainen  2500 euro
</pre>

</sample-output>

Programmet använder två lexikon som hjälpdatastrukturer: `namn` och `loner`. Båda använder pic som nyckel:

```python
namn = {}

with open("personal.csv") as fil:
    for rad in fil:
        delar = rad.split(';')
        if delar[0] == "personnr":
            continue
        namn[delar[0]] = delar[1]

loner = {}

with open("lon.csv") as fil:
    for rad in fil:
        delar = rad.split(';')
        if delar[0] == "personnr":
            continue
        loner[delar[0]] = int(delar[1]) +int(delar[2])

print("inkomster:")

for personnr, person in namn.items():
    if personnr in loner:
        lon = loner[personnr]
        print(f"{person:16} {lon} euro")
    else:
        print(f"{person:16} 0 euro")
```

Först skapar programmet lexikonen `namn` och `loner`. De har dessa innehåll:

```sh
{
    '080488-123X': 'Peter Mikkola',
    '290274-044S': 'Lisa Marttinen',
    '010479-007Z': 'Arto Vihavainen',
    '010499-345K': 'Leevi Hellas'
}

{
    '080488-123X': 3300,
    '290274-044S': 4350,
    '010479-007Z': 2500
}
```

For-loopen i slutet av programmet kombinerar namnen på arbetstagarna med deras löner.

Programmet kan också ta i beaktande situationer där pic saknas för en arbetstagare.

Kom ihåg att ordningen som elementen är lagrade i lexikon inte har någon skillnad, eftersom nycklarna behandlas med hjälp av hashvärden.

<programming-exercise name='Kursresultat, del 1' tmcname='osa06-04_resultat_1'>

Programmet behandlar två CSV-filen. I den ena finns information om studerande:

```csv
studerandenr;förnamn;efternamn
12345678;pekka;peloton
12345687;jaana;javanainen
12345699;liisa;virtanen
```

Och i den andra antalet gjorda uppgifter på veckonivå:

```csv
studerandenr;v1;v2;v3;v4;v5;v6;v7
12345678;4;1;1;4;5;2;4
12345687;3;5;3;1;5;4;6
12345699;10;2;2;7;10;2;2
```

I de båda CSV-filerna innehåller den första rade rubriker.

Skapa ett program som frågar efter filnamnen och skriver därefter ut antalet gjorda uppgifter för varje studerande. Exempel:

<sample-output>

Studerande (CSV): **studerande1.csv**
Uppgifter (CSV): **uppgifter1.csv**
pekka peloton 21
jaana javanainen 27
liisa virtanen 35

</sample-output>

Tips: Hårdkoda värdena medan du testar programmet, så behöver du inte hela tiden mata in dem på nytt:

```python
if False:
    # hit kommer vi aldrig
    studerande = input("Studerande (CSV): ")
    uppgifter = input("Uppgifter (CSV): ")
else:
    # de hårdkodade värdena
    studerande = "studerande1.csv"
    uppgifter = "uppgifter1.csv"
```

Den egentliga funktionaliteten är nu "gömd" bakom en `False`-förgrening som aldrig körs.

Om vi vill testa inmatning av information (på "normalt" sätt), kan vi ändra `False` till `True`:

```python
if True:
    studerande = input("Studerande (CSV): ")
    uppgifter = input("Uppgifter (CSV): ")
else:
    # hit kommer vi aldrig!
    studerande = "studerande1.csv"
    uppgifter = "uppgifter1.csv"
```

När koden är i skick kan if-satsen tas bort.

Obs! I dessa uppgifter ska kod inte placeras i `if __name__ == "__main__"` -blocket, om du inte ombeds göra det.

Obs! Om Visual Studio Code inte hittar filen även om namnet är korrekt skrivet, ska du följa instruktionerna här.

</programming-exercise>

<programming-exercise name='Kursresultat, del 2' tmcname='osa06-05_resultat_2'>

Vi utvidgar nu föregående uppgift så att de studerandes provpoäng också läses från en CSV-fil. Filens struktur är den följande:

```csv
studerandenr;u1;u2;u3
12345678;4;1;4
12345687;3;5;3
12345699;10;2;2
```

Till exempel studerande `12345678` har fått 4 + 1 + 4, alltså nio poäng.

Programmet ska fråga efter filnamnen och skriva ut vitsordet för varje studerande:

<sample-output>

Studerande (CSV): **studerande1.csv**
Uppgifter (CSV): **uppgifter1.csv**
Provpoäng (CSV): **provpoang1.csv**
pekka peloton 0
jaana javanainen 1
liisa virtanen 3

</sample-output>

Av gjorda uppgifter får man poäng så att 10 % gjorda uppgifter ger ett poäng ända till 100 % (40 uppgifter), som ger tio poäng. Poängen är ett heltal.

Vitsordet för kursen bildas på basis av prov- och uppgiftspoängsumman:

prov- och uppgiftspoäng tillsammans | vitsord
:----------------------------------:|:-------:
0-14                                | 0 (underkänt)
15-17                               | 1
18-20                               | 2
21-23                               | 3
24-27                               | 4
28-                                 | 5

Obs! I dessa uppgifter ska kod inte placeras i `if __name__ == "__main__"` -blocket, om du inte ombeds göra det.

</programming-exercise>

<programming-exercise name='Kursresultat, del 3' tmcname='osa06-06_resultat_3'>

I den här uppgiften formaterar vi utskriften från den föregående uppgiften:

<sample-output>

Studerande (CSV): **studerande1.csv**
Uppgifter (CSV): **uppgifter1.csv**
Provpoäng (CSV): **provpoang1.csv**
<pre>
namn                          uppg_ant  uppg_poang  provpoang  tot_poang  vitsord
pekka peloton                 21        5           9          14         0
jaana javanainen              27        6           11         17         1
liisa virtanen                35        8           14         22         3
</pre>

</sample-output>

På varje rad skrivs alltså ut den studerandes uppgiftsantal, uppgiftspoäng, provpoäng, totalpoäng samt vitsord. Det här görs "prydligt" så att namnkolumnen är 30 tecken bred och de övriga kolumnerna 10.

Det lönar sig att utnyttja f-strängar (modul fyra).

Märk att utskrift av strängar och siffror fungerar med lite olik logik i f-strängar:

```python
ord = "python"
print(f"{ord:10}fortsätter")
print(f"{ord:>10}fortsätter")
```

<sample-output>

<pre>
python    fortsätter
    pythonfortsätter
</pre>

</sample-output>

I vanliga fall är strängar vänsterjusterade, men med tecknet `>` kan man justera strängen till höger.

När siffror skrivs ut är logiken motsatt:

```python
siffra = 42
print(f"{siffra:10}fortsätter")
print(f"{siffra:<10}fortsätter")
```

<sample-output>

<pre>
        42fortsätter
42        fortsätter
</pre>

</sample-output>

Siffror är normalt högerjusterade men med tecknet `<` kan vi justera siffran till vänster.

Obs! I dessa uppgifter ska kod inte placeras i `if __name__ == "__main__"` -blocket, om du inte ombeds göra det.

</programming-exercise>

<programming-exercise name='Spell checker' tmcname='osa06-07_spellcheck'>

Skapa ett program som ber användaren ange text på engelska. Programmet ska utföra en språkkontroll och skriva ut texten så att felstavade ord är markerade med asterisker. Exempel:

<sample-output>

Write text: **We use ptython to make a spell checker**
<pre>
We use *ptython* to make a spell checker
</pre>

</sample-output>

<sample-output>

Write text: **This is acually a good and usefull program**
<pre>
This is *acually* good and *usefull* program
</pre>

</sample-output>

Bokstavsstorleken ska inte påverka programmets funktionalitet.

Programmet använder sig av filen `wordlist.txt` för att känna igen om orden är korrekt skrivna.

Obs! I dessa uppgifter ska kod inte placeras i `if __name__ == "__main__"` -blocket, om du inte ombeds göra det.

Obs! Om Visual Studio Code inte hittar filen även om namnet är korrekt skrivet, ska du följa instruktionerna här.

</programming-exercise>

<programming-exercise name='Receptsök' tmcname='osa06-08_receptsok'>

I den här uppgiften skapar vi ett program som låter användaren söka efter ett recept på basis av dess namn, tillagningstid eller ingrediens. Programmets recept finns lagrade i en fil.

Varje recept består av tre eller fler rader i receptfilen. Den första raden innehåller receptets namn, den andra tillagningstiden (heltal) och tredje raden framåt ingredienser. Ingredienslistan avsluts med en tom rad (exkl. det sista receptet). Filen kan inntehålla flera recept. Se exemplet nedan:

```sh
Plättdeg
15
mjölk
ägg
mjöl
socker
salt
smör

Köttbullar
45
malet kött
ägg
skorpmjöl

Tofurullar
30
tofu
ris
vatten
morot
gurka
avocado
wasabi

Bulldeg
60
mjölk
jäst
ägg
salt
socker
kardemumma
smör
```

Tips: I den här uppgiften lönar det sig kanske att läsa in filens rader i en lista och sedan behandla den här listan enligt den här uppgiftens specifikationer.

#### Sökning med receptnamn

Skapa funktionen `namnsok(fil: str, ord: str)` som söker efter recept vars namn innehåller den givna strängen. Funktionen ska returnera en lista med namnen på de matchande recepten.

Exempel:

```python
hittade = namnsok("recept1.txt", "bull")

for recept in hittade:
    print(recept)
```

<sample-output>

Köttbullar
Bulldeg

</sample-output>

Märk att bokstavsstorleken inte har någon skillnad. Med ordet `bull` hittar vi också `Bulldeg`.

Obs! Om Visual Studio Code inte hittar filen även om namnet är korrekt skrivet, ska du följa instruktionerna här.

#### Sökning med tillagningstid

Skapa funktionen `tidssok(fil: str, tid: int)` som söker efter de recept vars tillagningstid är högst det som angetts som argument.

Matchande recept returneras som en lista och nu ska också tillagningstiden inkluderas. Exempel:

```python
hittade = tidssok("recept1.txt", 20)

for recept in hittade:
    print(recept)
```

<sample-output>

Plättdeg, tillagningstid 15 min

</sample-output>

#### Sökning med ingrediens

Varning!! Den här delen är mycket svårare än de tidigare delarna. Om du har svårigheter, lönar det sig att göra de andra delarna först och sedan återkomma hit. Märk att du också kan skicka enskilda delar till servern.

Skapa funktionen `ingredienssok(fil: str, ingrediens: str)` som ska hitta recepten med den givna ingrediensen.

Matchande recept returneras som en lista. Exempel:

```python
hittade = ingredienssok("recept1.txt", "mjölk")

for recept in hittade:
    print(recept)
```

<sample-output>

Plättdeg, tillagningstid 15 min
Bulldeg, tillagningstid 60 min

</sample-output>

</programming-exercise>

<programming-exercise name='Stadscyklar' tmcname='osa06-09_stadscyklar'>

I den här uppgiften skapar vi några funktioner, med vilka vi kan inspektera en fil med information om [stadscyklars](https://www.hsl.fi/sv/stadscyklar) parkeringsstationer.

Så här ser filerna ut:

```csv
Longitude;Latitude;FID;name;total_slot;operative;id
24.950292890004903;60.155444793742276;1;Kaivopuisto;30;Yes;001
24.956347471358754;60.160959093887129;2;Laivasillankatu;12;Yes;002
24.944927399779715;60.158189199971673;3;Kapteeninpuistikko;16;Yes;003
```

För varje parkeringsstation finns det en skild rad i filen: här specificeras koordinater, namnet på stationen m.m.

#### Avstånd mellan stationer

Skapa funktionen `stationsinfo(fil: str)` som läser in stationsinfon och returnerar den som ett lexikon:

<sample-output>

<pre>
{
  "Kaivopuisto: (24.950292890004903, 60.155444793742276),
  "Laivasillankatu: (24.956347471358754, 60.160959093887129),
  "Kapteeninpuistikko: (24.944927399779715, 60.158189199971673)
}
</pre>

</sample-output>

Som nyckel kommer alltså stationens namn och som värde en tuple som består av longituden (1) och latituden (2).

Skapa nu funktionen `avstand(stationer: dict, station1: str, station2: str)` som returnerar avståndet mellan de två givna stationerna.

Följande formel används för att räkna avståndet:

```python
# det här behövs för att funktionen sqrt ska fungera
import math

x_km = (longitude1 - longitude2) * 55.26
y_km = (latitude1 - latitude2) * 111.2
avstand = math.sqrt(x_km**2 + y_km**2)
```

Exempel:

```python
stationer = stationsinfo('stations1.csv')
e = avstand(stationer, "Designmuseo", "Hietalahdentori")
print(e)
e = avstand(stationer, "Viiskulma", "Kaivopuisto")
print(e)
```

<sample-output>

0.9032737292463177
0.7753594392019532

</sample-output>

Obs! Om Visual Studio Code inte hittar filen även om namnet är korrekt skrivet, ska du följa instruktionerna här.

#### Längsta avstånd

Skapa funktionen `langsta_avstand(stationer: dict)` som ska ta reda på vilka stationer som är längst ifrån varandra. Funktionen ska returnera en tuple vars två första värden syftar till stationernas namn och det tredje värdet är avståndet i fråga.

```python
stationer = stationsinfo('stations1.csv')
station1, station2, suurin = langsta_avstand(stationer)
print(station1, station2, suurin)
```

<sample-output>

Laivasillankatu Hietalahdentori 1.478708873076181

</sample-output>

</programming-exercise>

<quiz id="cdac5075-c9cf-56f5-9ea3-eda73a48df4e"></quiz>
