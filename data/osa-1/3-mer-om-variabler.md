---
path: "/osa-1/3-mer-om-variabler"
title: "Mer om variabler"
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* kan du använda variabler i olika situationer
* vet du vilken typ av data som kan lagras i variabler
* känner du till skillnaderna mellan strängar, heltal och flyttal.

</text-box>

Vänligen fyll i den här enkäten före du börjar med den här delen. Du får ett poäng efter att du har fyllt i enkäten.

<quiz id="64c34f03-2a59-5f9e-8850-e2112625b111"></quiz>



Variabler har olika användningsområden inom programmering. Du kan använda variabler för att lagra vilken som helst typ av information som kan behövas senare medan ett program körs.

I Python skapas variabler på följande sätt:

`variabelns_namn = ...`

där `...` syftar till värdet som sparas i variabeln.

Till exempel när du använde `input` för att läsa in en sträng från användaren, sparade du strängen i en variabel och använde variabeln senare i ditt program.

```python
namn = input("Ange ditt namn: ")
print("Hejsan " + namn)
```

<sample-output>

Ange ditt namn: **Konstantin**
Hejsan Konstantin

</sample-output>

När man ger en variabel ett värde säger man att man _tilldelar_ den ett värde. I koden ovan tilldelar vi alltså variabeln `namn` det värde som användaren matar in som svar på frågan "Ange ditt namn:". 

Värdet som lagras i variabeln kan också definieras med hjälp av andra variabler:

```python
fornamn = "Gabrielle"
efternamn = "Gullholm"

namn = fornamn + " " + efternamn

print(namn)
```

<sample-output>

Gabrielle Gullholm

</sample-output>

Värdena som lagras i variablerna ovan kommer inte från användaren. De ändrar inte utan förblir de samma varje gång programmet körs. Det här kallas att hårdkoda data i programmet.

## Att byta värde på en variabel

Som namnet möjligtvis avslöjar, kan värdet på en _variabel_ variera, alltså ändra. I den förra delen observerade vi att ett nytt värde ersätter det tidigare värdet.

Medan vi kör följande program, kommer variabeln `ord` att ha tre olika värden:

```python
ord = input("Ge ett ord: ")
print(ord)

ord = input("Ge ett annat ord: ")
print(ord)

ord = "tredje"
print(ord)
```

<sample-output>

Ge ett ord: **första**
första
Ge ett annat ord: **andra**
andra
tredje

</sample-output>

Värdet som är lagrat i variabeln ändrar varje gång vi tilldelar variabeln ett nytt värde.

Det nya värdet på en variabel kan basera sig på det föregående värdet. I följande exempel tilldelas variabeln `ord` först ett värde på basis av indata från användaren. Därefter tilldelas variabeln ett nytt värde – som består av det gamla värdet följt av tre utropstecken.

```python
ord = input("Ge ett ord: ")
print(ord)

ord = ord + "!!!"
print(ord)
```

<sample-output>

Ge ett ord: **test**
test
test!!!

</sample-output>

<text-box variant="hint" name="Att välja ett bra namn för en variabel">

* Det är vanligtvis en bra idé att namnge variabler enligt deras funktion. Exempelvis om en variabel innehåller ett telefonnummer, så är `telnr` ett mycket bättre namn än `a`.
* Det finns ingen begränsning på variabelnamnens längd i Python, men det finns en del andra begränsningar. Variabelns namn ska börja med en bokstav och det kan endast innehålla bokstäver, siffror och understreck (\_).
* Stora och små bokstäver är olika tecken. Variablerna `namn`, `Namn` och `NAMN` är därför enligt Python olika variabler. Den här regeln har några undantag, men vi ignorera dem tills vidare.
* Det är ett vanligt tillvägagångssätt att i Python endast använda små bokstäver i variabelnamn. Om namnet består av flera ord använder man understreck mellan orden (t.ex. `start_hastighet`, `slut_hastighet`). Även den här regeln har några undantag, men vi ignorerar dem tills vidare.

</text-box>

## Heltal

Hittills har vi enbart lagrat strängar i variabler, men det finns också flera andra datatyper som vi kommer att vilja lagra och använda senare. Vi börjar med att titta på heltal. Heltal är tal utan decimal- eller bråkdel. Exempelvis -15, 0 och 1.

Följande program skapar variabeln `alder`. Eftersom vi tilldelar variabeln värdet 24, kommer variabeln att vara av typen heltal:

```python
alder = 24
print(alder)
```

Utskriften ser helt enkelt ut så här:

<sample-output>

24

</sample-output>

Märk att citattecknen fattas. Om vi skulle lägga till citattecken runt siffran skulle det inte längre vara ett heltal, utan en sträng. En sträng kan innehålla siffror, men strängar behandlas på ett annat sätt.

Varför ska variabler då ha en typ när programmets utskrift ändå ser lika ut i vilket fall som helst? 

```python
siffra1 = 100
siffra2 = "100"

print(siffra1)
print(siffra2)
```

<sample-output>

100
100

</sample-output>

Variabelns datatyp spelar en viktig roll, eftersom olika operationer påverkar olika typer av variabler på olika sätt. Ta en titt på följande exempel:

```python
siffra1 = 100
siffra2 = "100"

print(siffra1 + siffra1)
print(siffra2 + siffra2)
```

Koden skriver ut följande:

<sample-output>

200
100100

</sample-output>

För heltal betyder operatorn `+` addition, medan den för strängar innebär kombination av två strängar.

Alla operatorer är inte tillgängliga för alla typer av variabler. Vi kan dividera tal med operatorn /, men det går inte med strängar. Att försöka göra det ger upphov till ett felmeddelande.

## Att kombinera värden i samband med utskrift

Det följande kommer inte att fungera eftersom `"Resultatet är "` och `resultat` är av olika typer:

```python
resultat = 10 * 25
# nästa rad orsakar ett fel
print("Resultatet är: " + resultat)
```

Programmet skriver inte ut någonting – istället får vi ett fel:

<sample-output>

TypeError: unsupported operand type(s) for +: 'str' and 'int'

</sample-output>

I felet berättar Python att det inte går att kombinera två värden av olika typ så här enkelt. I det här exemplet är `"Resultatet är "` av typen sträng medan värdet i variabeln `resultat` är ett heltal.

Om vi vill skriva ut en sträng och ett heltal i en och samma instruktion kan vi konvertera heltalet till en sträng med `str`-funktionen. Därefter kan de två strängarna kombineras normalt. Till exempel så här:

```python
resultat = 10 * 25
print("Resultatet är: " + str(resultat))
```

<sample-output>

Resultatet är: 250

</sample-output>

`print` har också inbyggd funktionalitet för att skriva ut en kombination av olika typer av värden. Det enklaste sättet är att lägga in ett komma mellan värdena. Alla värden kommer då att skrivas ut – oavsett typ:

```python
resultat = 10 * 25
print("Resultatet är", resultat)
```

<sample-output>

Resultatet är: 250

</sample-output>

Observera att det i detta fall automatiskt läggs till ett mellanslag mellan värdena.

## Utskrift med f-strängar

Hur kan vi gå till väga om vi önskar mera flexibilitet och kontroll över det som skrivs ut? Ett sätt är att använda f-strängar. Syntaxen kan till att börja med verka en aning konstig, men f-strängar är ändå ofta det enklaste sättet att påverka formatet på en text.

Med f-strängar skulle det föregående exemplet se ut så här:

```python
resultat = 10 * 25
print(f"Resultatet är: {resultat}")
```

Låt oss se hur ovanstående exempel fungerar, del för del. Före strängen som vi vill skriva ut finns bokstaven f. Den här bokstaven berättar för Python att följande sträng ska tolkas som en f-sträng. Inom strängen finns variabelnamnet `resultat` innanför klamrar (måsvingar). Detta anger att variabelns värde kommer att bli en del av strängen då den skrivs ut. Utskriften ser helt likadan ut som i de föregående exemplen:

<sample-output>

Resultatet är: 250

</sample-output>

En och samma f-sträng kan innehålla flera variabler. Den här koden…

```python
namn = "Joline"
alder = 24
stad = "Kyrkslätt"
print(f"Hej {namn}, du är {alder} år. Du bor i {stad}.")
```

…skriver ut det följande:

<sample-output>

Hej Joline, du är 24 år. Du bor i Kyrkslätt.

</sample-output>

Det är svårt att åstadkomma en likadan utskrift med hjälp av kommanotationen i `print`. Exempelvis skriver programmet…

```python
namn = "Joline"
alder = 24
stad = "Kyrkslätt"
print("Hej", namn, ", du är", alder, " år. Du bor i", stad, ".")
```

… ut följande:

<sample-output>

Hej Joline , du är 24  år. Du bor i Kyrkslätt .

</sample-output>

Observera mellanslagen som automatiskt har lagts till mellan varje kommaseparerad del i instruktionen. Det är tekniskt sett möjligt att förhindra `print`-instruktionen från att lägga till mellanslag, men det är inte värt det eftersom vi kan använda oss av f-strängar.

Kommanotationen kan vara till nytta ibland, men ofta orsakar den mer problem än vad den löser. f-strängar är ofta en pålitligare metod. I modul fyra kommer du att lära dig om andra egenskaper hos f-strängar som för att vi kan påverka den utskrivna textens format på flera sätt.

<in-browser-programming-exercise name="Med mellanslag eller utan" tmcname="osa01-10b_mellanslag_eller_inte" height=400px>

Du får följande kodsnutt av en bekant:

```python
namn = "Tindra Testare"
alder = 20
kunskap1 = "python"
niva1 = "nybörjare"
kunskap2 = "java"
niva2 = "expert"
kunskap3 = "programmering"
niva3 = "nästan proffs"
min = 2000
max = 3000

print("mitt namn är ", namn, " , jag är ", alder, " år")
print("till mina kunskaper hör")
print("- ", kunskap1, " (", niva1, ")")
print("- ", kunskap2, " (", niva2, ")")
print("- ", kunskap3, " (", niva3, " )")
print("jag söker jobb vars lön är", min, "-", max, "euro i månaden")
```

Koden borde resultera i en exakt lika utskrift som följande:

<sample-output>

<pre>
mitt namn är Tindra Testare, jag är 20 år

till mina kunskaper hör
 - python (nybörjare)
 - java (expert)
 - programmering (nästan proffs)

jag söker jobb vars lön är 2000-3000 euro i månaden
</pre>

</sample-output>

Koden fungerar ungefär korrekt. Din uppgift är att korrigera koden. Testen i den här uppgiften är noggranna. Till och med ett litet mellanslag på fel ställe kommer att orsaka problem.

Koden ska alltså korrigeras så att utskriften ser korrekt ut. Observera att framför allt kommanotationen i `print` ofta orsakar mellanslag på ställen där de är oönskade.

Det enklaste sättet att korrigera koden är att använda f-strängar.

Tips: Du kan lägga till ett radbyte med hjälp av `print()` eller genom att inkludera `\n` på det stället i en sträng där radbytet ska vara.

Kom ihåg att lägga märke till utskriftsformatet i alla övningar även under resten av kursen. Vissa uppgifter kräver att utskriften från programmet är exakt densamma som i de givna exemplen.

</in-browser-programming-exercise>

## Flyttal

Flyttal är en term som du ofta kommer att stöta på i programmering. Det hänvisar till tal med decimaltecken. Flyttal kan användas på väldigt liknande sätt som heltal.

Följande program beräknar medeltalet av tre flyttal:

```python
tal1 = 2.5
tal2 = -1.25
tal3 = 3.62

medeltal = (tal1 + tal2 + tal3) / 3
print(f"Medelvärde: {medeltal}")
```

<sample-output>

Medelvärde: 1.6233333333333333

</sample-output>

<in-browser-programming-exercise name="Räkneoperationer" tmcname="osa01-11_rakneoperationer">

I den här övningen finns ett färdigt program med heltal tilldelade till variablerna `x` och `y`:

```python
x = 27
y = 15
```

Utveckla programmet vidare så att utskriften ser ut så här:

<sample-output>

27 + 15 = 42
27 - 15 = 12
27 * 15 = 405
27 / 15 = 1.8

</sample-output>

Programmet ska också fungera då värdet på variablerna ändras. I följande fall...

```python
x = 4
y = 9
```

...ser utskriften ut så här:

<sample-output>

4 + 9 = 13
4 - 9 = -5
4 * 9 = 36
4 / 9 = 0.4444444444444444

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Fixa programmet: Utskrifterna på samma rad" tmcname="osa01-12_utskrifter_pa_samma_rad">

Om man ger `print` parametern `end = ""`, kommer utskriften inte att avslutas med ett radbyte.

Exempel:

```python
print("Hej ", end="")
print("allesammans!")
```

<sample-output>

Hej allesammans!

</sample-output>

Korrigera programmet så att räkneoperationen och resultatet skrivs ut på en rad. Antalet `print`-instruktioner får dock inte ändras.

```python
print(5)
print(" + ")
print(8)
print(" - ")
print(4)
print(" = ")
print(5 + 8 - 4)
```

</in-browser-programming-exercise>

Du hittar ett repetitionsquiz för denna del här: 

<quiz id="5e01aa77-89a6-5ccd-ba2d-6890180680e2"></quiz>
