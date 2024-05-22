---
path: '/osa-4/2-lisaa-funktioista'
title: 'Mer om funktioner'
hidden: false
---


<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* vet du mera om argument och parametrar hos funktioner
* kan du returnera värden från funktioner och använda dessa värden i koden
* kan du ge typledtrådar för parametrar och värden som returneras.

</text-box>

Nu är det dags för en snabbrepetition av funktioner i Python. Funktioner definieras med nyckelordet `def`:

```python
def viesti():
    print("Tämä tulee funktiosta")
```

Funktionen kan anropas i koden på följande sätt:


```python
viesti()
```

I det här fallet skulle programmet skriva ut följande:

<sample-output>

Tämä tulee funktiosta

</sample-output>

## Parametrar och argument hos en funktion

En funktion kan motta en eller flera argument. När funktionen anropas tilldelas argumenten till variabler som är definierade i funktionsdefinitionen. Dessa variabler kallas parametrar och de listas inom parenteserna som följer funktionens namn.

I den följande koden har funktionen `halsa` en definierad parameter, medan funktionen `summa` har två:

```python
def tervehdi(nimi):
    print("Moikka,", nimi)

def summa(a, b):
    print("Parametrien summa on", a + b)
```

```python
tervehdi("Emilia")
summa(2, 3)
```

<sample-output>

Moikka, Emilia
Parametrien summa on 5

</sample-output>

<text-box variant='hint' name='Formell och riktig, parameter och argument'>

Terminologin kring data som ges till en funktion kan kännas förvirrande. För att göra situationen svårare, använder en del källor uttryck som formella och riktiga parametrar eller formella och riktiga argument. Pythons dokumentation nämner endast termerna argument och parameter. Därför använder vi också dessa termer.

Vad händer det egentligen när funktionsanropet `halsa("Emilia")` körs?

I funktionsdefinitionen `halsa(namn)` beter sig parametern namn som en normal variabel. Vi kan använda den inom funktionen på samma sätt som vi har använt variabler i huvudfunktionen i flera program hittills.

I funktionsanropet `halsa("Emilia")` är argumentet `"Emilia"` som vilken som helst annan sträng vi stött på tidigare. Vi kan till exempel tilldela den till en variabel.

Alltså, när funktionsanropet körs kommer värdet på argumentet – `"Emilia"` – att tilldelas till variabeln `namn`. Under den här körningen av funktionen kommer `namn = "Emilia"`. När funktionen anropas med ett annat argument kommer värdet på namn att vara olikt.

Terminologin kan kännas överflödig, men datavetenskapen strävar att vara så exakt vetenskap som möjligt. Att använda noga definierad terminologi hjälper.

</text-box>

## Felmeddelanden som uppstår i testen

De flesta uppgifter under den här kursen inkluderar automatiska test. Om programmet inte fungerar på det sätt som förutsätts av uppgiften, kommer testet att visa ett felmeddelande. Det här meddelandet kan vara till nytta – eller sen inte. Det kan vara värt att läsa meddelandet noga.

I vissa fall berättar felmeddelandet inte egentligen så mycket. I nästa övning kan du stöta på det här felmeddelandet:

<img src="4_2_0a.png">

Meddelandet berättar att man borde kunna köra funktionen `rad` med de specificerade argumenten:

```python
viiva(5, "")
```

Det riktiga problemet får vi reda på när vi kör det funktionsanrop som stod i felmeddelandet. Du kan göra det genom att kopiera funktionsanropet till ditt program och klicka på triangeln:

<img src="4_2_0b.png">

De sista raderna som uppstår när programmet körs (markerade i bilden ovan) berättar att rad fyra i koden orsakar felet `IndexError`. I den förra modulen fanns det ett liknande exempel, där vi försökte använda ett index som inte var en del av en sträng. Den här gången orsakas problemet av att vi försöker hämta den första bokstaven hos en tom sträng – dvs. en sträng med längden noll.

<programming-exercise name='Viiva' tmcname='osa04-02_viiva'>

Tee funktio `viiva`, joka saa kaksi parametria (leveys, merkkijono). Funktio tulostaa ensimmäisen parametrin määrittämän pituisen viivan käyttäen toisena parametrina olevan merkkijonon ensimmäistä merkkiä. Jos parametrina oleva merkkijono on tyhjä, tulostuu viiva tähtinä.

Käyttöesimerkki:

```python
viiva(7, "%")
viiva(10, "LOL")
viiva(3, "")
```

<sample-output>

<pre>
%%%%%%%
LLLLLLLLLL
***
</pre>

</sample-output>

</programming-exercise>

## Funktionsanrop inom funktionsanrop

Du kan anropa en funktion från en annan funktion. Vi har faktiskt gjort det här flera gånger – vi har anropat `print`-funktionen inom våra egna funktioner i den förra modulen. Våra egna funktioner fungerar på samma sätt. I det följande exemplet anropar funktionen `halsa_flera_ganger` funktionen `halsa` så många gånger som specificerats i argumentet ganger:

```python
def tervehdi(nimi):
    print("Moikka,", nimi)

def tervehdi_monesti(nimi, kerrat):
    while kerrat > 0:
        tervehdi(nimi)
        kerrat -= 1

tervehdi_monesti("Emilia", 3)
```

<sample-output>

Moikka, Emilia
Moikka, Emilia
Moikka, Emilia

</sample-output>


<programming-exercise name='Risulaatikko' tmcname='osa04-02a_risulaatikko'>

Tee funktio `risulaatikko`, joka piirtää risuaitamerkkiä käyttäen parametrinsa korkuisen, kymmenen merkkiä leveän risulaatikon.

Funktion tulee kutsua edellisen tehtävän funktiota `viiva` kaiken tulostuksen tekemiseen! Kopioi edellisen tehtävän funktion koodi tämän tehtävän funktion koodin yläpuolelle. Älä muuta funktiota mitenkään!

Pari käyttöesimerkkiä:

```python
risulaatikko(5)
print()
risulaatikko(2)
```

<sample-output>

<pre>
##########
##########
##########
##########
##########

##########
##########
</pre>

</sample-output>

</programming-exercise>

<programming-exercise name='Risuneliö' tmcname='osa04-02b_risunelio'>

Tee funktio `risunelio`, joka piirtää risuaitamerkkiä käyttäen parametrinsa kokoisen risuneliön.

Funktion tulee kutsua edellisen tehtävän funktiota `viiva` kaiken tulostuksen tekemiseen! Kopioi edellisen tehtävän funktion koodi tämän tehtävän funktion koodin yläpuolelle. Älä muuta funktiota mitenkaan!

Pari käyttöesimerkkiä:

```python
risunelio(5)
print()
risunelio(3)
```

<sample-output>

<pre>
#####
#####
#####
#####
#####

###
###
###
</pre>

</sample-output>

</programming-exercise>

<programming-exercise name='Neliö' tmcname='osa04-02c_nelio'>

Tee funktio `nelio`, joka saa kaksi parametria. Funktio tulostaa neliön jonka korkeuden ja leveyden kertoo ensimmäinen parametri.  Toinen parametri määrittelee mitä merkkiä käyttäen neliö piirretään.

Funktion tulee kutsua edellisen tehtävän funktiota `viiva` kaiken tulostuksen tekemiseen! Kopioi edellisen tehtävän funktion koodi tämän tehtävän funktion koodin yläpuolelle. Älä muuta funktiota mitenkaan!

Pari käyttöesimerkkiä:

```python
nelio(5, "*")
print()
nelio(3, "o")
```

<sample-output>

<pre>
*****
*****
*****
*****
*****

ooo
ooo
ooo
</pre>

</sample-output>

</programming-exercise>

<programming-exercise name='Kolmio' tmcname='osa04-02d_kolmio'>

Tee funktio `kolmio`, joka piirtää risuaitamerkkiä käyttäen parametrinsa korkuisen ja levyisen, risuaitakolmion.

Funktion tulee kutsua edellisen tehtävän funktiota `viiva` kaiken tulostuksen tekemiseen! Kopioi edellisen tehtävän funktion koodi tämän tehtävän funktion koodin yläpuolelle. Älä muuta funktiota mitenkaan!

Pari käyttöesimerkkiä:

```python
kolmio(6)
print()
kolmio(3)
```

<sample-output>

<pre>
#
##
###
####
#####
######

#
##
###
</pre>

</sample-output>

</programming-exercise>

<programming-exercise name='Kuvio' tmcname='osa04-03_kuvio'>

Tee funktio `kuvio`, joka saa neljä parametria. Funktio tulostaa kuvion, jonka yläosana on kahden ensimmäisen parametrin määrittelemä kolmio ja alaosana ensimmäisen ja kahden jälkimmäisen parametrin määrittelemä suorakulmio.

Funktion tulee kutsua edellisen tehtävän funktiota `viiva` kaiken tulostuksen tekemiseen! Kopioi edellisen tehtävän funktion koodi tämän tehtävän funktion koodin yläpuolelle.

Pari käyttöesimerkkiä:

```python
kuvio(5, "X", 3, "*")
print()
kuvio(2, "o", 4, "+")
print()
kuvio(3, ".", 0, ",")
```

<sample-output>

<pre>
X
XX
XXX
XXXX
XXXXX
*****
*****
*****

o
oo
++
++
++
++

.
..
...
</pre>

</sample-output>

**Vihje**

Älä yritä ratkaista tehtävässä "kaikkia asioita" yhtä aikaa. Keskity ensin esim. siihen että saat kuvion yläosan kolmion piirtymään oikein, ja vasta sen jälkeen jatka kuvion täydentämistä alaosan suorakulmiolla.

Tämä on ylipäätänsäkin ohjelmoinnissa erittäin tärkeää: **keskity pieniin osiin kerrallaan**, varmista että ne toimivat ennen kuin laajennat ratkaisuasi.

</programming-exercise>

<programming-exercise name='Joulukuusi' tmcname='osa04-04_joulukuusi'>

Tee funktio `joulukuusi`, joka saa yhden parametrin. Funktio tulostaa tekstin joulukuusi! ja parametrinsa kokoisen joulukuusen.

Esim. kutsuttaessa `joulukuusi(3)` tulostuu

<sample-output>

<pre>
joulukuusi!
  *
 ***
*****
  *
</pre>

</sample-output>

Esim. kutsuttaessa `joulukuusi(5)` tulostuu

<sample-output>

<pre>
joulukuusi!
    *
   ***
  *****
 *******
*********
    *
</pre>

</sample-output>

**Huomaa, että joulukuusen vasemmalla puolella pitää olla täsmälleen oikea määrä välilyöntejä**. Eli vaikka kuusen muoto olisi täysin oikea, mutta sen alin "neulastaso" ei lähde ruudun vasemmasta reunasta, ei vastaus kelpaa testeille.

</programming-exercise>

## Return-värdet hos en funktion

Funktioner kan också returnera värden. Till exempel Pythons inbyggda funktion `input` returnerar en sträng som användaren angett. Värdet som returneras av en funktion kan lagras i en variabel:

```python
sana = input("Anna sana: ")
```

När du vill ha ett heltalsvärde från användaren måste indatat från användaren konverteras till ett heltal. För det använder vi `int`-funktionen som också returnerar ett värde:

```python
luku = int(input("Anna kokonaisluku: "))
```

Funktionen `int` tar den sträng som returneras av `input`-funktionen som argument och returnerar värdet i heltalsform om möjligt.

## `return`-satsen

Funktioner som du själv definierar kan också returnera värden. För det här ändamålet behöver du `return`-satsen. Till exempel funktionen `min_summa` nedan returnerar summan av dess parametrar:

```python
def summa(a, b):
    return a + b

vastaus = summa(2, 3)

print("Summa:", vastaus)
```

<sample-output>

Summa: 5

</sample-output>

Här är ett annat exempel på ett returnerat värde. Funktionen ber om användarens namn och returnerar den sträng som användaren anger:

```python
def kysy_nimi():
    nimi = input("Mikä on nimesi? ")
    return nimi

nimi = kysy_nimi()
print("Moikka,", nimi)
```

<sample-output>

Mikä on nimesi? **Anna**
Moikka, Anna

</sample-output>

`return`-satsen avslutar körandet av funktionen genast. Det här är ett sätt att göra en jämförelsefunktion:

```python
def pienin(a,b):
    if a < b:
        return a
    return b

print(pienin(3, 7))
print(pienin(5, 2))
```

Idén är att om `a` är mindre än `b` så kommer funktionen att returnera `a` och avslutas direkt. Annars fortsätter man till nästa rad som returnerar värdet `b`. En return-sats kan inte köras flera gånger i samma funktion under samma funktionsanrop.

<sample-output>

3
2

</sample-output>

Du kan använda dig av `return`-satsen även om funktionen inte returnerar något värde. Då är dess uppgift helt enkelt att avsluta körandet av funktionen:

```python
def tervehdi(nimi):
    if nimi == "":
        print("???")
        return
    print("Moikka,", nimi)

tervehdi("Emilia")
tervehdi("")
tervehdi("Matti")
```

Om argumentet som sparas i variabeln `namn` är en tom sträng, kommer texten `???` att skrivas ut och funktionen avslutas:

<sample-output>

Moikka, Emilia
???
Moikka, Matti

</sample-output>

## Att använda return-värden från funktioner

Vi känner redan till att värden som returneras från funktioner kan lagras i variabler:

```python
def summa(a, b):
    return a + b

tulos = summa(4, 6)
print("Summa on", tulos)
```

<sample-output>

Summa on 10

</sample-output>

Return-värdet hos en funktion kan jämföras med vilket som helst annat värde. Det är inte nödvändigt att lagra värdet i en variabel för att ge det som argument till `print`-kommandot:

```python
print("Summa on", summa(4, 6))
```

Return-värdet hos en funktion kan vara ett argument för en funktion:

```python
def summa(a, b):
    return a+b

def erotus(a, b):
    return a-b

tulos = erotus(summa(5, 2), summa(2, 3))
print("Vastaus on", tulos)
```

<sample-output>

Vastaus on 2

</sample-output>

I det här fallet körs de inre funktionsanropen `min_summa(5, 2)` och `min_summa(2, 3)` först. Värdena som returneras (sju och fem) används som argument för det yttre funktionsanropet.

Det yttre funktionsanropet `differens(7, 5)` returnerar värdet 2, som lagras i variabeln `resultat` och skrivs ut.

För att sammanfatta: värden som returneras av funktioner fungerar som alla andra värden i Python. De kan skrivas ut, lagras i variabler och användas i uttryck och som argument i funktionsanrop.

## Skillnaden mellan `return` och `print`

Ibland kan skillnaden mellan att använda `return` och `print` inom en funktion vara oklara. Vi undersöker två olika sätt att göra en funktion som berättar vilket av två värden är större:

```python
def maksimi1(a, b):
    if a > b:
        return a
    else:
        return b

def maksimi2(a, b):
    if a > b:
        print(a)
    else:
        print(b)

vastaus = maksimi1(3, 5)
print(vastaus)

maksimi2(7, 2)
```

<sample-output>

5
7

</sample-output>

Båda versionerna verkar fungera i och med att det större av värdena skrivs ut korrekt. Det finns ändå en central skillnad mellan dessa två funktioner. Den första, `max1`, skriver inte ut något. Den använder sig istället av `return`-satsen. Om vi kör den följande kodraden…

```python
maksimi1(3, 5)
```

…verkar ingenting hända. Funktionens return-värde måste användas på något sätt i den kod som anropar funktionen. Det kan till exempel lagras i en variabel och skrivas ut:

```python
vastaus = maksimi1(3, 5)
print(vastaus)
```

Den andra versionen, `max2`, använder sig av `print`-kommandot inom funktionen. Om vi vill se värdet, kan vi helt enkelt anropa funktionen…

```python
maksimi2(7, 5)
```

…och det större värdet kommer att skrivas ut. Det dåliga med den här funktionen är att värdet som funktionen räknar ut inte kan användas av själva programmet. Därför är funktioner som returnerar ett värde ofta ett bättre alternativ.

<programming-exercise name='Luvuista suurin' tmcname='osa04-05_luvuista_suurin'>

Tee funktio  `luvuista_suurin`, joka saa parametriksi kolme kokonaislukua. Funktio palauttaa return-lausetta käyttäen luvuista suurimman.

Käyttöesimerkki

```python
print(luvuista_suurin(3, 4, 1)) # 4
print(luvuista_suurin(99, -4, 7)) # 99
print(luvuista_suurin(0, 0, 0)) # 0
```

</programming-exercise>

<programming-exercise name='Merkit samat' tmcname='osa04-06_merkit_samat'>

Tee funktio `samat`, joka saa parametriksi merkkijonon ja kaksi merkkijonon indeksejä kuvaavaa kokonaislukua. Funktio palauttaa `return`-lausetta käyttäen tiedon (`True` tai `False`) siitä, ovatko merkkijonon parametreina olevien indeksien osoittamissa paikoissa olevat merkit samat. Jos jompikumpi indekseistä ei osu merkkijonon sisälle, palauttaa metodi `False`.

Muutama esimerkki:

```python
# samat merkit o ja o
print(samat("koodari", 1, 2)) # True

# eri merkit k ja a
print(samat("koodari", 0, 4)) # False

# toinen indeksi ei ole merkkijonon sisällä
print(samat("koodari", 0, 10)) # False
```

</programming-exercise>

<programming-exercise name='Eka, toka ja vika sana' tmcname='osa04-07_eka_toka_vika_sana'>

Tee kolme funktiota: `eka_sana`, `toka_sana` ja `vika_sana`. Jokainen funktioista saa parametrikseen lauseen (eli merkkijonon).

Funktiot palauttavat nimensä mukaisesti lauseen ensimmäisen, toisen tai viimeisen sanan.

Voit olettaa jokaisessa tapauksessa, että merkkijono koostuu vähintään kahdesta sanasta, ja että sanojen välillä on aina täsmälleen yksi välilyönti, ja että merkkijonon alussa ja lopussa ei ole välilyöntejä.

```python
lause = "olipa kerran kauan sitten ohjelmoija"

print(eka_sana(lause)) # olipa
print(toka_sana(lause)) # kerran
print(vika_sana(lause)) # ohjelmoija
```

<sample-output>

olipa
kerran
ohjelmoija

</sample-output>

```python
lause = "olipa kerran"

print(toka_sana(lause)) # kerran
print(vika_sana(lause)) # kerran
```

</programming-exercise>

## Typen av ett argument

Här är en kort repetition av de datatyper vi bekantat oss med hittills:

Tyyppi        | I Python | Exempel
:-------------|:--------:|-----------
Heltal        | `int`    | `23`
Flyttal       | `float`  | `-0.45`
Sträng        | `str`    | `"Petra Python"`
Sanningsvärde | `bool`   | `True`

När du anropar en funktion, kommer den bara att fungera korrekt då argumenten du ger åt den är av korrekt typ. Ta en titt på det här exemplet:

```python
def tulosta_monesti(viesti, kerrat):
    while kerrat > 0:
        print(viesti)
        kerrat -= 1
```

Funktionen fungerar korrekt om vi anropar den på följande sätt:

```python
tulosta_monesti("Moikka", 5)
```

<sample-output>

Moikka
Moikka
Moikka
Moikka
Moikka

</sample-output>

Om vi däremot ger funktionen ett argument av fel typ så kommer funktionen inte att fungera:

```python
tulosta_monesti("Moikka", "Emilia")
```

<sample-output>

TypeError: '>' not supported between instances of 'str' and 'int'

</sample-output>

Problemet här är att den andra parametern `ganger` jämförs med ett heltal (0) på den andra raden av funktionsdefinitionen. Det givna argumentet `"Emilia"` är en sträng och inte ett heltal. Strängar och heltal kan inte jämföras så här enkelt – därmed felmeddelandet.

För att undvika problem som dessa kan du inkludera typledtrådar (type hints) när du definierar funktioner. Typledtråden berättar vilken typ av argument funktionen förväntar sig motta:

```python
def tulosta_monesti(viesti : str, kerrat : int):
    while kerrat > 0:
        print(viesti)
        kerrat -= 1
```

Det här berättar för alla användare av funktionen att argumentet som lagras i `meddelande` ska vara en sträng medan argumentet som lagras i `ganger` ska vara ett heltal.

Också typen av return-värdet kan specificeras när funktionen definieras:

```python
def kysy_nimi() -> str:
    nimi = input("Mikä on nimesi? ")
    return nimi
 ```

Det här berättar för användaren att funktionen borde returnera en sträng.

Obs! Typledtrådar är bokstavligen ledtrådar. Det är inte en garanti och kan inte säkerställa att felaktiga datatyper inte ges till eller returneras av en funktion. Om det här sker kommer funktionen ändå att köras, men den fungerar inte nödvändigtvis korrekt.

<quiz id="8e93e885-fda8-5930-8232-80dd3dc01642"></quiz>
