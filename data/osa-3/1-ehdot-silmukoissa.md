---
path: '/osa-3/1-ehdot-silmukoissa'
title: 'Loopar med villkor'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* kan du skapa en loop med ett villkor
* vet du vad vilka roller initiering, villkoret och att uppdatering av variabler har i en loop
* kan du skapa loopar med olika typer av villkor.

</text-box>

## Osallistu tutkimukseen - vastaa kyselyyn

Alla olevan linkin takaa löytyy Hannu Pesosen väitöskirjatutkimukseen liittyvä kysely. Kurssin suorittaminen ei edellytä kyselyyn vastaamista, mutta yliopistoissa tutkimus on luonnollisesti tärkeässä osassa myös opetuksen kehittämisessä.

Jos sinulta siis löytyy hetki aikaa, niin [vastaa kyselyyn](https://link.webropolsurveys.com/S/EB89556E704FA59B).

Kyselyyn ei ole pakko antaa henkilötietoja (esimerkiksi nimeä), vaikka niitä ensimmäisellä sivulla kysytäänkin.


<!--vastaava teksti löytyy osioista 3-1, 5-1 ja 6-1, tsekkaa kaikki jos muokkaat tätä-->
<text-box variant='hint' name='Om uppgifterna i den här kursen'>

Att bli en skicklig programmerare kräver mycket övning. Man måste utveckla en problemlösningsförmåga och ha en förmåga att intuition komma fram till korrekta lösningar. Därför finns det massor av övningar av olika typer i den här kursen. Vissa övningar är enklare och baserar sig mera eller mindre direkt på materialet medan andra uppgifter är svårare och kräver tillämpande av kunskaper som man lärt sig under kursen.

En del uppgifter kan kännas svåra, men det är inte något att oroa sig över. Ingen av uppgifterna är obligatorisk och du behöver bara 25 % av poängen från varje modul för att klara den här kursen. Du kan läsa mera på kursens bedömningssida.

Uppgifterna är inte i svårighetsordning. Varje del introducerar vanligtvis några nya saker inom programmering och i samband finns relaterade uppgifter – både enklare och svårare. Om du stöter på en uppgift som känns oöverkomlig ska du fortsätta till nästa uppgift. Du kan alltid senare återkomma till tidigare uppgifter.

En uppgift som känns för svår just nu kommer sannolikt att vara ganska enkel om en månad.

</text-box>

I den förra delen bekantade vi oss med `while True` -loopen som ett medel att upprepa delar av kod. Så som loopen är uppbyggd är villkoret alltid `True`, alltså sant. Vi måste då avsluta loopen manuellt vid något skede för att undvika en oändlig loop. Exempelvis:

```python
# Tulosta lukuja kunnes muuttujan a arvo on 5
a = 1
while True:
    print(a)
    a += 1
    if a == 5:
        break
```

<sample-output>

1
2
3
4

</sample-output>

Men förstås behöver villkoret inte alltid vara True, utan det kan vara vilket som helst Boolean-uttryck. while-satsens struktur ser ut så här:

```python
while <ehtolauseke>:
    <lohko>
```

Idén är att koden körs om och om igen – villkoret kollas för varje iteration. Om villkoret vid något skede inte är sant kommer programmet att fortsätta med koden som kommer efter while-blocket.

<img src="3_1_1.png">

I den följande loopen har vi villkoret `nummer < 10`. Blocket inom loopen kommer bara att köras då variabeln nummer är mindre än tio.

```python
luku = int(input("Anna luku: "))

while luku < 10:
    print(luku)
    luku += 1

print("Suoritus valmis.")
```

Utskriften skulle kunna se ut så här:

<sample-output>

Anna luku: **4**
4
5
6
7
8
9
Suoritus valmis.

</sample-output>

Med den här strukturen kommer villkoret att kollas före blocket inom loopen körs. Det är möjligt att det här blocket inte kommer att köras en enda gång. Så här till exempel:

<sample-output>

Anna luku: **12**
Suoritus valmis.

</sample-output>

Tolv är inte mindre än tio, så programmet skriver inte ut någon siffra.

## Initialisering, villkor och uppdatering

För att skapa en loop behövs ofta tre olika steg: initialisering, ett villkor och uppdatering av variabler.

Initialisering syftar till att ge startvärden till de variabler som används i loopens villkor. Det här görs före man kommer till loopen. Villkoret bestämmer hur länge loopen körs. Det skrivs i början av loopen. För varje iteration ska variablerna som används i villkoret uppdateras, så att loopen steg för steg närmar sitt slut. Här presenterar vi stegen i ett exempel:

<img src="3_1_2.png">

Om någon av de här tre komponenterna fattas kommer loopen antagligen inte att fungera korrekt. Ett vanligt misstag är att låta bli att uppdatera variabler:

```python
luku = 1

while luku < 10:
    print(luku)

print("Suoritus valmis.")
```

Här kommer värdet på variabeln `nummer` aldrig att ändras. Programmet är fast i en oändlig loop. Samma kod upprepas tills användaren avslutar programmet, till exempel med tangentkombinationen Control + C:

<sample-output>

1
1
1
1
1
(tämä jatkuu ikuisesti...)

</sample-output>

<in-browser-programming-exercise name="Tulosta luvut" tmcname="osa03-00_tulosta_luvut">

Kirjoita ohjelma, joka tulostaa silmukassa luvut kahdesta kolmeenkymmeneen kahden luvun välein. Jokainen luku tulostetaan omalle rivilleen.

Ohjelman tulosteen alku näytää siis tältä:

<sample-output>
2
4
6
8
jne...
</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Lähtölaskenta" tmcname="osa03-01_lahtolaskenta">

Korjaa tehtäväpohjassa oleva ohjelma

```python
print("Valmiina?")
luku = int(input("Anna luku: "))
while luku = 0:
print(luku)
print("Nyt!")
```

siten että se toimii seuraavasti:

<sample-output>

Valmiina?
Anna luku: **5**
5
4
3
2
1
Nyt!

</sample-output>

Älä tällä kertaa käytä `while True` -silmukkaa!


</in-browser-programming-exercise>

## Skriva villkor

Alla Boolean-uttryck och kombinationer av dem kan användas som villkor i en loop. Till exempel följande program skriver ut var tredje nummer förutsatt att det är mindre än 100 och inte dividerbart med fem:

```python
luku = int(input("Anna luku: "))

while luku < 100 and luku % 5 != 0:
    print(luku)
    luku += 3
```

Här följer två exempel på utskriften från programmet:

<sample-output>

Anna luku: **28**
28
31
34
37

</sample-output>

<sample-output>

Anna luku: **96**
96
99

</sample-output>

När man ger programmet värdet 28 kommer loopen att avslutas med numret 37, eftersom nästa siffra är 40 – och är dividerbart med fem. När man ger värdet 96 kommer loopen att avsluta med numret 99 eftersom nästa siffra är 102 – som inte är mindre än 100.

När du skriver en loop är det viktigt att se till att loopen alltid kommer att avslutas vid något skede. Det här programmet avslutas – eller inte – beroende på det värde som ges:

```python
luku = int(input("Anna luku: "))

while luku != 10:
    print(luku)
    luku += 2
```

Om man ger ett jämnt tal som är lika med tio eller mindre, kommer loopen att avslutas:

<sample-output>

Anna luku: **4**
4
6
8

</sample-output>

I övriga fall kommer loopen att fortsätta oändligt eftersom det inte då finns något sätt för variabeln att vara lika med tio. Till exempel tre och tolv är värden som skulle förorsaka en oändlig loop.

<in-browser-programming-exercise name="Luvut" tmcname="osa03-02_luvut">

Tee ohjelma, joka tulostaa kaikki käyttäjän antamaa lukua pienemmät luvut alkaen luvusta yksi.

<sample-output>

Mihin asti: **5**
1
2
3
4

</sample-output>

Älä käytä tässä tehtävässä while-komennon ehtona arvoa `True`!

</in-browser-programming-exercise>

## Tips för debuggning

Föreställ att du håller på att skapa ett lite mera komplicerat program, som det i den följande uppgiften – _Potenser av två_. Så här skulle man kunna starta:

```python
asti = int(input("Mihin asti"))
luku = 1
while luku == asti:
   # koodia
```

Nu börjar programmet med att läsa in den data användaren ger och fortsätter till en loop med ett villkor.

Det är sannolikt att koden inte kommer att fungera på önskat sätt från början. Den kan behöva testas tio- eller till och med hundratals gånger före den fungerar korrekt.

Den här kodsnutten frågar alltid efter indata från användaren vilket gör testandet långsamt och arbetsdrygt. Varje gång programmet testas måste ett värde anges.

Ett sätt att bli av med problemet är att hårdkoda ett värde i koden medan den testas:

```python
# kovakoodataan syötteen arvo aluksi
asti = 8 # int(input("Mihin asti"))
luku = 1
while luku == asti:
   # koodia
```

När programmet fungerar med det hårdkodade värdet, kan man enkelt testa med andra hårdkodade värden. När allt fungerar korrekt kan man testa på programmet så att användaren anger värdet.

Det här tricket fungerar väl med flera av de tester som används i betygsättningen av den här kursens uppgifter. Om testet berättar att något är fel med till exempel värdet 42 så kan värdet tillfälligt hårdkodas i programmet medan du letar efter buggen:

```python
# testi ilmoitti että koodi toimii väärin kun syöte on 42
asti = 42 # int(input("Mihin asti"))
luku = 1
while luku == asti:
   # koodia
```

Debuggning med hjälp av `print`-satsen nämndes några gånger under förra modulen i den här kursen. De program som du skapar kommer att bli mer invecklade i och med att kursen framskrider. Då kommer mängden debuggning som du behöver göra också antagligen att öka i samma proportion. Vanliga orsaker till buggar finns ofta i de villkor som avslutar loopar – de fungerar eventuellt korrekt för vissa värden, medan andra värden orsakar problem. Alltid är det inte heller lätt att observera det här.

Därför är det nu dags att använda dig av `print`-satser för att debugga – om du inte redan har gjort det. Du hittar instruktioner i den första och fjärde delen av den föregående modulen.

Vid sidan om `print`-satser finns även andra verktyg som kan använda för debuggning. Ett av dem är visualiseringsverktyget på Python Tutor -webbsidan. Verktyget låter dig köra din kod rad för rad och visar också de värden som är lagrade i variabler vid varje steg.

Koden – med några problem – från den förra delen visualiseras med Python Tutor i följande bild:

<img src="3_1_0.png">

Den röda pilen visar var programmet körs för tillfället. Verktyget visar vad som har skrivits ut fram till pilen och visar också vilka värden varje variabel har i varje steg.

Det enda du behöver för att köra visualiseringsverktyget är att kopiera och klistra in din kod i verktygets kodfönster. Verktyget har en del begränsningar jämfört med den Python-version som används under den här kursen. Om du stöter på konstiga felmeddelanden kan det löna sig att använda någon annan metod för att debugga.

De som har sysslat med programmering en längre tid använder sällan visualiseringsverktyg men för en nybörjare kan verktyget verkligen vara till hjälp. Det är osannolikt att man av en slump får något program att fungera. Det är nödvändigt att man som programmerare förstår vilka värden ens programkod skapar vid ett visst skede medan programmet körs. Om de värden som lagras i variabler inte är sådana som man förväntar sig, finns det högst sannolikt en bugg i programmet.

Visualiseringsverktyget och `print`-satser är båda bra sätt för en programmerare att med egna ögon se att programmet gör exakt det som det ska göra.

<in-browser-programming-exercise name="Kahden potenssit" tmcname="osa03-03_kahden_potenssit">

Tee ohjelma, joka tulostaa ensin luvun 1 ja sen jälkeen kerta toisensa jälkeen aina kaksi kertaa suuremman luvun. Ohjelma siis tulostaa luvun kaksi potensseja.

Ohjelman suoritus päättyy, kun on tulostettu luku, joka on korkeintaan käyttäjän syötteen suuruinen. Yhtään käyttäjän syötettä suurempaa lukua ei siis tulosteta!

<sample-output>

Mihin asti: **8**
1
2
4
8

</sample-output>

<sample-output>

Mihin asti: **20**
1
2
4
8
16

</sample-output>

<sample-output>

Mihin asti: **100**
1
2
4
8
16
32
64

</sample-output>

Älä käytä tässä tehtävässä `while`-komennon ehtona arvoa `True`!

**Miten kahden potenssit lasketaan?** Ensimmäinen kahden potenssi on luku 1. Seuraava saadaan kertomalla 1 luvulla 2, eli se on 2. Sitä seuraava saadaan taas kertomalla edellinen kahden potenssi kahdella, eli kyseessä on 2 \* 2 eli 4, ja seuraava saadaan kertomalla kahdella 4 \* 2 eli kyseessä on 8, jne...

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Luvun n potenssit" tmcname="osa03-04_luvun_n_potenssit">

Muuta edellistä ohjelmaa siten, että käyttäjä saa määrätä kertoimen (edellisessä ohjelmassa kerroin oli aina 2), eli sen, minkä luvun potensseja ohjelma tulostaa.

<sample-output>

Mihin asti: **27**
Mikä kerroin: **3**
1
3
9
27

</sample-output>

<sample-output>

Mihin asti: **1234567**
Mikä kerroin: **10**
1
10
100
1000
10000
100000
1000000

</sample-output>

Älä käytä tässä tehtävässä `while`-komennon ehtona arvoa `True`!

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Peräkkäisten summa, versio 1" tmcname="osa03-04a_perakkaisten_summa_helpompi">

Tee ohjelma, joka laskee peräkkäisten lukujen summaa 1 + 2 + 3 + ... kunnes sen arvo on vähintään käyttäjän syöttämä luku. Ohjelma toimii seuraavasti:

<sample-output>

Mihin asti: **2**
3

</sample-output>

<sample-output>

Mihin asti: **10**
10

</sample-output>

<sample-output>

Mihin asti: **18**
21

</sample-output>

Voit olettaa, että käyttäjän antama luku on 2 tai suurempi.

</in-browser-programming-exercise>

## Bilda strängar

Under kursens första vecka lärde vi oss att det är möjligt att bilda strängar av kortare strängar med hjälp av `+`-operatorn. Till exempel detta är valid Python-kod:

```python
sanat = "suo"
sanat = sanat + ", kuokka"
sanat = sanat + " ja python"

print(sanat)
```

<sample-output>

suo, kuokka ja python

</sample-output>

`+=`-operatorn låter oss skriva ovanstående lite mer kompakt:

```python
sanat = "suo"
sanat += ", kuokka"
sanat += " ja python"

print(sanat)
```

Det här gäller också f-strängar som kan vara nyttiga då värden lagrade i strängar behövs som delar av en resulterande sträng. Det här skulle till exempel fungera:

```python
kurssi = "Ohjelmoinnin perusteet"
arvosana = 4

lausunto = "Olet saanut "
lausunto += f"kurssilta {kurssi} "
lausunto += f"arvosanan {arvosana}"

print(lausunto)
```

<sample-output>

Olet saanut kurssilta Ohjelmoinnin perusteet arvosanan 4

</sample-output>

I det förra exemplet räknade du summan av varandra påföljande siffror genom att alltid öka på värdet i loopen.

Samma fungerar också för strängar – du kan lägga till nya delar i en sträng inom en loop. Den här tekniken kan vara till nytta i följande uppgift.

<in-browser-programming-exercise name="Peräkkäisten summa, versio 2" tmcname="osa03-05_perakkaisten_summa">

Tee edellisestä ohjelmasta hieman kehittyneempi versio, joka tulostaa lopputuloksen lisäksi myös sen miten kyseinen summa lasketaan:

<sample-output>

Mihin asti: **2**
Laskettiin 1 + 2 = 3

</sample-output>

<sample-output>

Mihin asti: **10**
Laskettiin 1 + 2 + 3 + 4 = 10

</sample-output>

<sample-output>

Mihin asti: **18**
Laskettiin 1 + 2 + 3 + 4 + 5 + 6 = 21

</sample-output>

Voit olettaa, että käyttäjän antama luku on 2 tai suurempi.

</in-browser-programming-exercise>


<quiz id="742577d3-7a6c-5249-a0b8-10bbcaeea044"></quiz>
