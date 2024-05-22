---
path: '/osa-6/2-tiedostojen-kirjoittaminen'
title: 'Skriva filer'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

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
with open("uusi_tiedosto.txt", "w") as tiedosto:
    # tiedostoon kirjoittaminen
```

Obs! Om filen redan finns, kommer allt innehåll att skrivas över. Man ska vara väldigt försiktig när man skapar nya filer.

När filen är öppen, kan du skriva data i den. Du kan använda metoden `write`, som tar strängen som ska skrivas som sitt argument:

```python
with open("uusi_tiedosto.txt", "w") as tiedosto:
    tiedosto.write("Moi kaikki!")
```

När du kör programmet, dyker en ny fil med namnet `ny_fil.txt` upp i mappen. Innehållet borde se ut så här:

<sample-data>

Moi kaikki!

</sample-data>

Om du vill ha radbyten i filen, måste du lägga till dem för hand. Funktionen `write` fungerar inte som print-funktionen, även om de har likheter. Följande program…

```python
with open("uusi_tiedosto.txt", "w") as tiedosto:
    tiedosto.write("Moi kaikki!")
    tiedosto.write("Toinen rivi")
    tiedosto.write("Viimeinen rivi")
```

…skulle resultera i en fil som denna:

<sample-data>

Moi kaikki!Toinen riviViimeinen rivi

</sample-data>

Radbrytningar får man till stånd med att inkludera `\n` i strängarna som ges som argument till `write`-funktionen:

```python
with open("uusi_tiedosto.txt", "w") as tiedosto:
    tiedosto.write("Moi kaikki!\n")
    tiedosto.write("Toinen rivi\n")
    tiedosto.write("Viimeinen rivi\n")
```

Nu borde innehållet i `ny_fil.txt` se ut så här:

<sample-data>

Moi kaikki!
Toinen rivi
Viimeinen rivi

</sample-data>

<programming-exercise name='Omistuskirjoitus' tmcname='osa06-10_omistuskirjoitus'>

Tee ohjelma, joka kysyy nimeä ja luo "omistuskirjoituksen" käyttäjän haluamaan tiedostoon. Seuraavassa ohjelman esimerkkisuoritus:

<sample-output>

Kenelle teos omistetaan: **Arto**
Mihin kirjoitetaan: **omistettu.txt**

</sample-output>

Tiedoston `omistettu.txt` sisällöksi tulee

<sample-data>

Hei Arto, toivomme viihtyisiä hetkiä python-kurssimateriaalin parissa! Terveisin mooc.fi-tiimi

</sample-data>

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!


</programming-exercise>

## Lägga till data i en befintlig fil

Om du vill lägga till data i slutet av en fil istället för att skriva över en hel fil, kan du använda argumentet `a` istället för `w`.

Om filen inte ännu finns, fungerar det här läget på samma sätt som skrivläget.

Följande program öppnar filen `ny_fil.txt` och lägger till några rader text i slutet:

```python
with open("uusi_tiedosto.txt", "a") as tiedosto:
    tiedosto.write("Rivi numero 4\n")
    tiedosto.write("Ja taas yksi.\n")
```

När programmet körs, borde innehållet i filen se ut på följande sätt:

<sample-output>

Moi kaikki!
Toinen rivi
Viimeinen rivi
Rivi numero 4
Ja taas yksi.

</sample-output>

I praktiken är det inte så vanligt att man lägger till innehåll i en befintlig fil.

Oftare läser man en fil, behandlar man data och till sist skrivs filen över med nya data. Till exempel om man vill ändra på innehållet i mitten av en fil, är det vanligtvis enklast att skriva över hela filen.

<programming-exercise name='Päiväkirja' tmcname='osa06-11_paivakirja'>

Tee ohjelma, joka mallintaa yksinkertaista päiväkirjaa. Ohjelman tulee tallentaa päiväkirjamerkinnät tiedostoon `paivakirja.txt`. Kun ohjelma käynnistetään, se lukee merkinnät tiedostosta.

Huom! Paikalliset testit voivat muuttaa tiedoston sisältöä - kopioi siis tiedosto talteen ennen testien ajamista, jos haluat säilyttää sen sisällön.

Ohjelman tulee toimia seuraavan esimerkin mukaisesti:

<sample-output>

1 - lisää merkintä, 2 - lue merkinnät, 0 - lopeta
Valinta: **1**
Anna merkintä: **Tänään söin puuroa**
Päiväkirja tallennettu

1 - lisää merkintä, 2 - lue merkinnät, 0 - lopeta
Valinta: **2**
Merkinnät:
Tänään söin puuroa
1 - lisää merkintä, 2 - lue merkinnät, 0 - lopeta
Valinta: **1**
Anna merkintä: **Illalla kävin saunassa**
Päiväkirja tallennettu

1 - lisää merkintä, 2 - lue merkinnät, 0 - lopeta
Valinta: **2**
Merkinnät:
Tänään söin puuroa
Illalla kävin saunassa
1 - lisää merkintä, 2 - lue merkinnät, 0 - lopeta
Valinta: **0**
Heippa!

</sample-output>

Uusi käynnistys:

<sample-output>

1 - lisää merkintä, 2 - lue merkinnät, 0 - lopeta
Valinta: **2**
Merkinnät:
Tänään söin puuroa
Illalla kävin saunassa
1 - lisää merkintä, 2 - lue merkinnät, 0 - lopeta
Valinta: **0**
Heippa!

</sample-output>

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!


</programming-exercise>

## Skriva CSV-filer

CSV-filer kan skrivas rad för rad med `write`-metoden, precis som med vilken som helst annan fil. Det följande exemplet skapar filen `programmerare.csv` som innehåller namnet, programmeringsmiljön, favoritprogrammeringsspråket och antalet år arbetserfarenhet hos en programmerare. Fälten skiljs åt med semikolon.

```python
with open("koodarit.csv", "w") as tiedosto:
    tiedosto.write("Erkki;Windows;Pascal;10\n")
    tiedosto.write("Matti;Linux;PHP;2\n")
    tiedosto.write("Antti;Linux;Java;17\n")
    tiedosto.write("Emilia;Mac;Cobol;9\n")
```

När programmet körs får vi följande fil:

<sample-output>

Erkki;Windows;Pascal;10
Matti;Linux;PHP;2
Antti;Linux;Java;17
Emilia;Mac;Cobol;9

</sample-output>

Hur är det om data som ska skrivas finns i en lista i datorns minne?

```python
koodarit = []
koodarit.append(["Erkki", "Windows", "Pascal", 10])
koodarit.append(["Matti", "Linux", "PHP", 2])
koodarit.append(["Antti", "Linux", "Java", 17])
koodarit.append(["Emilia", "Mac", "Cobol", 9])
```

Vi kan konstruera den sträng som vi vill skriva som en f-sträng, och skriva den klara raden i filen:

```python
with open("koodarit.csv", "w") as tiedosto:
    for koodari in koodarit:
        rivi = f"{koodari[0]};{koodari[1]};{koodari[2]};{koodari[3]}"
        tiedosto.write(rivi+"\n")
```

Om varje lista skulle vara väldigt lång, skulle det vara arbetsdrygt att konstruera strängen för hand och då skulle vi istället kunna använda en for-loop:

```python
with open("koodarit.csv", "w") as tiedosto:
    for koodari in koodarit:
        rivi = ""
        for arvo in koodari:
            rivi += f"{arvo};"
        rivi = rivi[:-1]
        tiedosto.write(rivi+"\n")
```

## Tömma innehållet i en fil och ta bort en fil

Ibland behöver vi tömma innehållet i en fil. Då kan vi helt enkelt öppna filen i skrivläge och därefter stänga filen:

```python
with open("tyhjennettava_tiedosto.txt", "w") as tiedosto:
    pass
```

Observera att `with`-blocket nu bara innehåller kommandot `pass`, som inte gör något. Python tillåter inte tomma block, så därför använder vi det här kommandot här.

Det är också möjligt att undvika `with`-blocket och istället använda följande kommando:

```python
open('tyhjennettava_tiedosto.txt', 'w').close()
```

<text-box variant='hint' name='Ta bort filer'>

Du kan också helt och hållet avlägsna en fil. Vi måste be operativsystemet om hjälp för att uppnå detta:

```python
# poisto-komento tuodaan koodin käyttöön import-lauseella
import os

os.remove("tarpeeton_tiedosto.csv")
```

Obs! Det här fungerar inte i testmiljön som används för de automatiska testen. Om du ombeds tömma innehållet i en fil, ska du använda någon av metoderna som beskrevs ovan.

</text-box>


<programming-exercise name='Aineiston suodatus' tmcname='osa06-12_aineiston_suodatus'>

Tiedostossa laskut.csv on tehtävien ratkaisuja seuraavan esimerkin mukaisesti:

```csv
Arto;2+5;7
Pekka;3-2;1
Erkki;9+3;11
Arto;8-3;4
Pekka;5+5;10
...jne...
```

Jokaisella rivin muoto on siis `oppilaan_nimi;lasku;lopputulos`. Laskut ovat kaikki esimerkin mukaisesti joko yhteen- tai vähennyslaskuja, ja kaikissa on kaksi operandia.

Kirjoita funktio `suodata_laskut()`, joka

* Lukee tiedoston `laskut.csv` sisällön ja
* kirjoittaa tiedostoon `oikeat.csv` ne rivit, joilla laskutoimituksen lopputulos on oikein sekä
* kirjoittaa tiedostoon `vaarat.csv` ne rivit, joilla laskutoimituksen lopputulos on väärin.

Edellisestä esimerkistä tiedostoon `oikeat.csv` olisi siis kirjoitettu rivit

```sh
Arto;2+5;7
Pekka;3-2;1
Pekka;5+5;10
```

Kaksi muuta riviä olisi kirjoitettu tiedostoon `vaarat.csv`.

Kirjoita rivit samassa järjestyksessä kuin ne esiintyvät alkuperäisessä tiedostossa. Älä muuta alkuperäistä tiedostoa.

*Huomaa* että funktion tulee toimia oikein siinäkin tapauksessa että funktiota kutsutaan monta kertaa perkkäin. Eli riippumatta siitä suoritatko funktion vain kerran

```python
suodata_laskut()
```

tai useita kertoja peräkkän

```python
suodata_laskut()
suodata_laskut()
suodata_laskut()
suodata_laskut()
```

tiedostojen sisältöjen tulee lopulta olla samat.

</programming-exercise>

<programming-exercise name='Henkilöt talteen' tmcname='osa06-13_henkilot_talteen'>

Kirjoita funktio `tallenna_henkilo(henkilo: tuple)` joka saa parametrikseen henkilöä kuvaavan tuplen. Tuplessa on seuraavat tiedot tässä järjestyksessä:

* Nimi (merkkijono)
* Ikä (kokonaisluku)
* Pituus (liukuluku)

Tallenna henkilön tiedot tiedostoon `henkilot.csv` olemassa olevien tietojen perään. Tiedot tulee tallentaa muodosssa

nimi;ikä;pituus

eli yhden henkilön tiedot tulevat yhdelle riville. Jos funktiota esim. kutsuttaisiin parametrien arvoilla `("Kimmo Kimmonen", 37, 175.5)`, ohjelma kirjoittaisi tiedoston loppuun rivin

`Kimmo Kimmonen;37;175.5`

</programming-exercise>

## Behandla data i CSV-format

Låt oss skapa ett program som utvärderar elevernas framgång under en kurs. Programmet läser en CSV-fil som innehåller de veckovisa poängen som den studerande fått under kursens lopp. Programmet räknar ihop poängen och utvärderar därefter vilket vitsord de räcker till. Till slut skapar programmet en CSV-fil som innehåller poängsumman och vitsordet för varje elev.

CSV-filen som vi har tillgång till när vi börjar ser ut så här:

<sample-data>

Pekka;4;2;3;5;4;0;0
Paula;7;2;8;3;5;4;5
Pirjo;3;4;3;5;3;4;4
Emilia;6;6;5;5;0;4;8

</sample-data>

Programmets logik är uppdelad i tre funktioner: läsande av filen och behandlande av innehållet, vitsordsberäkning och skrivande av en ny fil.

Filens inläsning sker enligt det vi lärt oss i den förra delen. Data lagras i ett lexikon där nyckeln är elevens namn och värdet är en lista på poängen som eleven i fråga har fått, i heltalsform:

```python
def lue_viikkopisteet(tiedostonimi):
    viikkopisteet = {}
    with open(tiedostonimi) as tiedosto:
        for rivi in tiedosto:
            osat = rivi.split(";")
            lista = []
            for pisteet in osat[1:]:
                lista.append(int(pisteet))
            viikkopisteet[osat[0]] = lista

    return viikkopisteet
```

Den andra funktionen beräknar vilket vitsord ett visst antal poäng räcker till. Funktionen används av den tredje funktionen, som skriver resultaten i en fil:

```python
def arvosana(pisteet):
    if pisteet < 20:
        return 0
    elif pisteet < 25:
        return 1
    elif pisteet < 30:
        return 2
    elif pisteet < 35:
        return 3
    elif pisteet < 40:
        return 4
    else:
        return 5

def tallenna_tulokset(tiedostonimi, viikkopisteet):
    with open(tiedostonimi, "w") as tiedosto:
        for nimi, lista in viikkopisteet.items():
            summa = sum(lista)
            tiedosto.write(f"{nimi};{summa};{arvosana(summa)}\n")
```

Strukturen tillåter oss skapa en mycket enkel huvudfunktion. Observera att filnamnen ges som argument i huvudfunktionen:

```python
viikkopisteet = lue_viikkopisteet("viikkopisteet.csv")
tallenna_tulokset("tulokset.csv", viikkopisteet)
```

När huvudfunktionen körs, skapas filen `resultat.csv` med följande innehåll:

<sample-data>

Pekka;18;0
Paula;34;3
Pirjo;26;2
Emilia;41;5

</sample-data>

Notera att alla funktioner ovan är relativt enkla till sin funktionalitet – de har en uppgift var. Det här är ett vanligt och rekommenderat sätt att skapa större helheter när man programmerar. När en funktion har en uppgift är det enklare att säkerställa att den fungerar på önskat sätt. Det här gör det också enklare att senare ändra på programmet och lägga till ny funktionalitet.

Om vi till exempel vill ha en funktion för att skriva ut vitsordet för enskild studerande, kan vi skapa en ny funktion som använder sig av en befintlig funktion i koden:

```python
def hae_arvosana(haettava, viikkopisteet):
    for nimi, lista in viikkopisteet.items():
        if nimi == haettava:
            return arvosana(sum(lista))


viikkopisteet = lue_viikkopisteet("viikkopisteet.csv")
print(hae_arvosana("Paula", viikkopisteet))

```

<sample-data>

3

</sample-data>

Om vi märker att någon funktionalitet i programmet kräver åtgärdande, kommer ändringar inte att orsaka följder överallt i koden. Om vi till exempel vill ändra på vitsordsgränserna, behöver vi bara ändra på funktionen som räknar ut vitsordet – alla andra funktioner som använder den här funktionen skulle fortfarande fungera, med de nya gränserna. Om koden för den här funktionaliteten skulle vara splittrad, finns det en risk att vi glömmer att uppdatera koden på något ställe. Det här skulle antagligen orsaka problem.

<programming-exercise name='Kurssin tulokset, osa 4' tmcname='osa06-14_kurssin_tulokset_osa4'>

Laajennetaan vielä hieman aiemmin kurssien tulokset generoivaa sovellusta.

Tällä hetkellä tiedostosta luetaan opiskelijoiden nimet, tehtäväpisteet sekä koepisteet. Laajennetaan ohjelmaa siten, että myös kurssin nimi ja laajuus luetaan tiedostosta, jonka muoto on seuraava (tiedosto on kirjoitettu ilman ääkkösiä, jotta se ei aiheuttaisi ongelmia Windowsissa):

<sample-data>

<pre>

nimi: Ohjelmoinnin perusteet
laajuus opintopisteina: 5
</pre>

</sample-data>

Ohjelma luo kaksi tiedostoa. Tiedoston `tulos.txt` muoto on seuraava:

<sample-data>

<pre>
Ohjelmoinnin perusteet, 5 opintopistettä
========================================
nimi                          teht_lkm  teht_pist koe_pist  yht_pist  arvosana
pekka peloton                 21        5         9         14        0
jaana javanainen              27        6         11        17        1
liisa virtanen                35        8         14        22        3
</pre>

</sample-data>

Tulokset kertova osa on siis samanlainen kuin tehtävän edellisen osan tulostus.

Tämän lisäksi luodaan tiedosto `tulos.csv`, jonka muoto on seuraava:

<sample-data>

<pre>
12345678;pekka peloton;0
12345687;jaana javanainen;1
12345699;liisa virtanen;3
</pre>

</sample-data>

Ohjelman suoritus näyttää seuraavalta:

<sample-output>

opiskelijatiedot: **opiskelijat1.csv**
tehtävätiedot: **tehtavat1.csv**
koepisteet: **koepisteet1.csv**
kurssin tiedot: **kurssi1.txt**
Tulokset talletettu tiedostoihin tulos.txt ja tulos.csv

</sample-output>

Ohjelma siis ainoastaan kyselee tiedostojen nimet ja varsinaiset tulokset tallennetaan vain tiedostoihin.

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!

</programming-exercise>



<programming-exercise name='Sanahaku' tmcname='osa06-15_sanahaku'>

Tehtäväpohjasta löytyy tiedosto `sanat.txt`, joka sisältää englanninkielisiä sanoja.

Tehtäväsi on kirjoittaa funktio `hae_sanat(hakusana: str)`, joka palauttaa listana annetun hakusanan mukaiset sanat tiedostosta.

Hakusanassa voi käyttää pienten kirjainten lisäksi seuraavia erikoismerkkejä:

* Piste `.` tarkoittaa, että mikä tahansa merkki käy (esim `ca.` vastaa vaikkapa sanoja cat ja car, `p.ng` sanoja ping ja pong ja `.a.e` sanoja sane, care tai late.
* Asteriski `*` tarkoittaa, että sanan alku- tai loppuosaksi käy mikä tahansa jono, esim. `ca*` vastaa vaikkapa sanoja california, cat, caring tai catapult. Vastaavasti hakusana `*ane` vastaa vaikkapa sanoja crane, insane tai aeroplane. Voit olettaa, että asteriski on aina joko hakusanan alussa tai lopussa, ja että hakusanassa esiintyy korkeintaan yksi asteriski.
* Jos hakusanassa ei ole erikoismerkkejä, haetaan vain täsmälleen hakusanaa vastaava sana.

Sovitaan, että samassa hakusanassa ei voi käyttää molempia erikoismerkkejä.

Sanat ovat tiedostossa kokonaan pienillä kirjaimilla kirjoitettuna. Voit myös olettaa, että funktion parametri on annettu kokonaan pienillä kirjaimilla.

Jos yhtään tulosta ei löydy, funktio palauttaa tyhjän listan.

Vinkki: Pythonin merkkijonometodeista startswith() ja endswith() saattaa olla hyötyä tehtävässä, googlaa niiden toiminta tarvittaessa tarkemmin!

Esimerkki funktion kutsumisesta:

```python

print(hae_sanat("*vokes"))

```

<sample-output>

['convokes', 'equivokes', 'evokes', 'invokes', 'provokes', 'reinvokes', 'revokes']

</sample-output>

</programming-exercise>

<programming-exercise name='Muistava sanakirja' tmcname='osa06-16_muistava_sanakirja'>

Tee sanakirjaa mallintava ohjelma, johon voi syöttää uusia sanoja tai josta voi hakea syötettyjä sanoja.

Ohjelman tulee toimia näin:

<sample-output>

1 - Lisää sana, 2 - Hae sanaa, 3 - Poistu
Valinta: **1**
Anna sana suomeksi: **auto**
Anna sana englanniksi: **car**
Sanapari lisätty
1 - Lisää sana, 2 - Hae sanaa, 3 - Poistu
Valinta: **1**
Anna sana suomeksi: **roska**
Anna sana englanniksi: **garbage**
Sanapari lisätty
1 - Lisää sana, 2 - Hae sanaa, 3 - Poistu
Valinta: **1**
Anna sana suomeksi: **laukku**
Anna sana englanniksi: **bag**
Sanapari lisätty
1 - Lisää sana, 2 - Hae sanaa, 3 - Poistu
Valinta: **2**
Anna sana: **bag**
roska - garbage
laukku - bag
1 - Lisää sana, 2 - Hae sanaa, 3 - Poistu
Valinta: **2**
Anna sana: **car**
auto - car
1 - Lisää sana, 2 - Hae sanaa, 3 - Poistu
Valinta: **2**
Anna sana: **laukku**
laukku - bag
1 - Lisää sana, 2 - Hae sanaa, 3 - Poistu
Valinta: **3**
Moi!

</sample-output>

Sanat tallennetaan tiedostoon `sanakirja.txt`. Ohjelma lukee tiedoston sisällön kun se käynnistetään. Uudet sanaparit lisätään tiedostoon aina tallennuksen yhteydessä.

Voit itse päättää tiedostoon tallennettavan tiedon muodon.

Huomaa, että paikallisten TMC-testien ajaminen voi tyhjentää sanakirja-tiedoston.

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!


</programming-exercise>

<quiz id="58b92c76-559a-588f-8662-6c430d212bc2"></quiz>
