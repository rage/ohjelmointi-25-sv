---
path: '/osa-6/1-tiedostojen-lukeminen'
title: 'Läsa filer'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* kan du läsa en fil med Python
* vet du vad en textfil och en CSV-fil är
* kan du behandla innehållet i en CSV-fil i dina program.

</text-box>

<!--vastaava teksti löytyy osioista 3-1, 5-1 ja 6-1, tsekkaa kaikki jos muokkaat tätä-->
<text-box variant='hint' name='Kurssin tehtävien tekemisestä'>

Ohjelmointitaidon kehittyminen edellyttää vahvaa rutiinia ja myös omaa soveltavaa oivaltamista. Tämän takia kurssilla on paljon tehtäviä. Osa tehtävistä on kohtuullisen suoraviivaisesti materiaalia hyödyntäviä ja osa taas aivan tarkoituksella haastavampia soveltavia tehtäviä.

Ei kannata huolestua, vaikka osa kurssin tehtävistä tuntuisikin ensiyrittämällä liian vaikealta. Kaikkia tehtäviä ei ole pakko tehdä, kuten [arvosteluperusteet](/arvostelu-ja-kokeet) toteavat, _kurssin läpipääsyyn vaaditaan vähintään 25 % jokaisen osan ohjelmointitehtävien pisteistä._

**Kurssin osien tehtävät eivät etene vaikeusjärjestyksessä.** Jokaisessa aliosassa esitellään yleensä muutama uusi konsepti, joita harjoitellaan sekä helpommilla että soveltavimmilla tehtävillä. **Jos törmäät liian haastavan tuntuiseen tehtävään, hyppää seuraavaan**. Voit palata vaikeimpiin tehtäviin osan lopuksi, jos aikaa vielä jää.

Lohdutuksen sanana todettakoon, että tällä viikolla mahdottomalta vaikuttava tehtävä näyttää melko varmasti neljän viikon päästä melko helpolta.

</text-box>

När man programmerar kan det uppstå ett behov att behandla data som finns lagrad i filer. Datorprogram kan läsa data från filer och skriva data till filer. Också stora mängder data i filer kan enkelt behandlas automatiskt.

Under den här kursen kommer vi endast att arbeta med textfiler. De här filerna består av rader med text. Till exempel kodeditorn Visual Studio Code är kompatibel med textfiler. Obs! Även om ordbehandlingsprogram som Microsoft Word ofta används med filer som innehåller text, är Word-dokument inte textfiler. Dokumenten innehåller också annan information om till exempel textformat, vilket gör det mer komplicerat att behandla filerna i ett program.

## Att läsa data från en fil

Vi börjar att arbeta med filen `exempel.txt` som innehållet det följande:

<sample-data>

Moi kaikki!
Esimerkkitiedostomme on kolmerivinen.
Viimeinen rivi.

</sample-data>

Ett enkelt sätt att använda filer i Python är med `with`-satsen. Den inledande raden öppnar filen och blocket där vi kan komma åt filen följer. Efter blocket stängs filen automatiskt och då kan den inte mera behandlas.

Den här koden öppnar alltså filen, läser dess innehåll och skriver det ut, och till slut stängs filen:

```python
with open("esimerkki.txt") as tiedosto:
    sisalto = tiedosto.read()
    print(sisalto)
```

<sample-output>

Moi kaikki!
Esimerkkitiedostomme on kolmerivinen.
Viimeinen rivi.

</sample-output>

Variabeln `ny_fil` är en file handle (”filhandtag”). Via variabeln kan vi komma åt filen så länge den är öppen. Här använde vi metoden `read` som returnerar filens innehåll som en hel sträng. I det här fallet skulle strängen se ut så här:

```
"Moi kaikki!\nEsimerkkitiedostomme on kolmerivinen.\nViimeinen rivi."
```

## Gå igenom innehållet i en fil

Metoden `read` fungerar väl för att skriva ut hela innehållet i en fil, men ofta vill vi gå igenom innehållet rad för rad.

Man kan tänka att textfiler är som listor med strängar, där varje sträng finns på sin egen rad i filen. Vi kan gå igenom listan med en for-loop.

Följande exempel läser in vår exempelfil med hjälp av en for-loop, tar bort radbrytningarna, räknar antalet rader och skriver ut varje rad med sitt radnummer. Programmet håller också koll på radernas längder:

```python
with open("esimerkki.txt") as tiedosto:
    laskuri = 0
    yhteispituus = 0

    for rivi in tiedosto:
        rivi = rivi.replace("\n", "")
        laskuri += 1
        print("Rivi", laskuri, rivi)
        pituus = len(rivi)
        yhteispituus += pituus

print("Rivien yhteispituus:", yhteispituus)
```

<sample-output>

Rivi 1 Moi kaikki!
Rivi 2 Esimerkkitiedostomme on kolmerivinen.
Rivi 3 Viimeinen rivi.
Rivien yhteispituus: 63

</sample-output>

Det finns en radbrytning `\n` i slutet av varje rad i filen, men `print`-funktionen lägger också automatiskt till en rad i slutet av utskriften. Det finns inga extra radbyten i utskriften ovan eftersom radbrytningarna avlägsnats med hjälp av `replace`-metoden. Metoden ersätter alla radbrytningstecken med en tom sträng. I och med detta räknas radernas längder också korrekt.

<programming-exercise name='Suurin luku' tmcname='osa06-01_suurin_luku'>

Tiedostoon `luvut.txt` on tallennettu lukuja, yksi luku per rivi seuraavan esimerkin mukaisesti:

```sh
2
45
108
3
-10
1100
...jne...
```

Kirjoita funktio `suurin`, joka lukee tiedoston ja palauttaa suurimman tiedostosta löytyvän luvun.

Huomaa, että tiedoston nimi on aina `luvut.txt` eikä funktiolle anneta parametria.

**Huom!** Jos VS Code ei löydä tiedostoa vaikka olet tarkastanut tiedoston nimen kirjoitusasun, voit kokeilla seuraavaa heti tehtävän jälkeen olevaa ohjetta.

</programming-exercise>

## Om Visual Studio Code inte hittar min fil?

När du kör din kod är det möjligt att Visual Studio Code meddelar att filen – även efter att du kollat att filen finns och att namnet är korrekt skrivet. Att ändra på följande inställning kan lösa problemet:

* öppna inställningarna från menyraden: File -> Preferences -> Settings
* sök efter den inställning som ska ändras med sökordet ”executeinfile”
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
teksti = "apina,banaani,cembalo"
sanat = teksti.split(",")
for sana in sanat:
    print(sana)
```

<sample-output>

apina
banaani
cembalo

</sample-output>

Låt oss säga att vi har filen `vitsord.csv`, som innehåller namn på elever samt vitsord de fått av olika kurser. Varje rad har data som tillhör en studerande och data separeras med semikolon.

<sample-data>

Pekka;5;4;5;3;4;5;5;4;2;4
Paula;3;4;2;4;4;2;3;1;3;3
Pirjo;4;5;5;4;5;5;4;5;4;4

</sample-data>

Följande program går igenom filen rad för rad, delar upp raderna i delar och skriver ut namnen på eleverna samt deras vitsord:

```python
with open("arvosanat.csv") as tiedosto:
    for rivi in tiedosto:
        rivi = rivi.replace("\n", "")
        osat = rivi.split(";")
        nimi = osat[0]
        arvosanat = osat[1:]
        print("Nimi:", nimi)
        print("Arvosanat:", arvosanat)
```

<sample-output>

Nimi: Pekka
Arvosanat: ['5', '4', '5', '3', '4', '5', '5', '4', '2', '4']
Nimi: Paula
Arvosanat: ['3', '4', '2', '4', '4', '2', '3', '1', '3', '3']
Nimi: Pirjo
Arvosanat: ['4', '5', '5', '4', '5', '5', '4', '5', '4', '4']

</sample-output>

<programming-exercise name='Hedelmäkauppa' tmcname='osa06-02_hedelmakauppa'>

Tiedostossa `hedelmat.csv` on hedelmiä hintoineen seuraavan esimerkin mukaisesti:

```sh
banaani;6.50
omena;4.95
appelsiini;8.0
...jne...
```

Kirjoita funktio `lue_hedelmat`, joka lukee hedelmätiedoston ja muodostaa siitä sanakirjan, jossa hedelmän nimi on avain ja hinta arvo. Hinnan tulee olla `float`-arvona sanakirjassa.

Huomaa, että tiedoston nimi on aina `hedelmat.csv` eikä funktiolle anneta parametria.

Lopuksi funktio palauttaa tämän sanakirjan.

**Huom!** Jos VS Code ei löydä tiedostoa vaikka olet tarkastanut tiedoston nimen kirjoitusasun, voit kokeilla [täällä](/osa-6/1-tiedostojen-lukeminen#mita-jos-vs-code-ei-loyda-tiedostoja-koodia-suoritettaessa) olevaa ohjetta.

</programming-exercise>

<programming-exercise name='Matriisi' tmcname='osa06-03_matriisi'>

Tiedostossa `matriisi.txt` on seuraavan esimerkin kaltainen matriisi:

```sh
1,0,2,8,2,1,3,2,5,2,2,2
9,2,4,5,2,4,2,4,1,10,4,2
...jne...
```

Kirjoita funktiot `summa` ja `maksimi`, jotka lukevat ja palauttavat nimensä mukaisesti matriisin kaikkien alkioiden summan ja suurimman alkion.

Kirjoita lisäksi funktio `rivisummat`, joka palauttaa listassa kaikkien matriisin rivien summat. Esimerkiksi matriisille

```sh
1,2,3
2,3,4
```

funktio palauttaisi listan `[6, 9]`.

Vinkki: Voit kirjoittaa ohjelmaan myös muita funktioita – kannattaa siis miettiä, mitä kaikkia yhteisiä toimintoja kolmea funktiota varten vaaditaan. Huomaa, että tiedoston nimi on aina `matriisi.txt` eikä tehtävänannossa määritellyille funktioille anneta parametreja. Itse lisäämäsi funktiot voivat hyödyntää myös parametreja.

**Huom!** Jos VS Code ei löydä tiedostoa vaikka olet tarkastanut tiedoston nimen kirjoitusasun, voit kokeilla [täällä](/osa-6/1-tiedostojen-lukeminen#mita-jos-vs-code-ei-loyda-tiedostoja-koodia-suoritettaessa) olevaa ohjetta.

</programming-exercise>

## Läsa samma fil flera gånger

Ibland kan man behöva läsa innehållet i en fil flera gånger i samma program. Vi tittar på ett program som behandlar data om några personer i en CSV-fil:

<sample-data>
Pekka;40;Helsinki
Emilia;34;Espoo
Erkki;42;Turku
Antti;100;Helsinki
Liisa;58;Suonenjoki
</sample-data>

```python
with open("henkilot.csv") as tiedosto:
    # tulostetaan nimet
    for rivi in tiedosto:
        osat = rivi.split(";")
        print("Nimi:", osat[0])

    # etsitään vanhin
    vanhimman_ika = -1
    for rivi in tiedosto:
        osat = rivi.split(";")
        nimi = osat[0]
        ika = int(osat[1])
        if ika > vanhimman_ika:
            vanhimman_ika = ika
            vanhin = nimi
    print("vanhin on", vanhin)
```

När vi kör programmet får vi det här felmeddelandet:

```python
Traceback (most recent call last):
    print("vanhin on"; vanhin)
UnboundLocalError: local variable 'vanhin' referenced before assignment
```

Orsaken till at det här sker är att den andra for-loopen aldrig körs. Detta eftersom filen endast kan behandlas en gång. När den sista raden har lästs stannar file handlen i slutet av filen och data i filen kan inte längre kommas åt.

Om vi vill komma åt innehållet i filen i den andra for-loopen, måste vi öppna filen på nytt:

```python
with open("henkilot.csv") as tiedosto:
    # tulostetaan nimet
    for rivi in tiedosto:
        osat = rivi.split(";")
        print("Nimi:", osat[0])

with open("henkilot.csv") as tiedosto:
    # etsitään vanhin
    vanhimman_ika = -1
    for rivi in tiedosto:
        osat = rivi.split(";")
        nimi = osat[0]
        ika = int(osat[1])
        if ika > vanhimman_ika:
            vanhimman_ika = ika
            vanhin = nimi
    print("vanhin on", vanhin)
```

Även om den ovanstående koden fungerar, innehåller den onödig upprepning. Det lönar sig vanligtvis att läsa filen bara en gång, och spara dess innehåll i ett passligt format för fortsatt behandling:

```python
henkilot = []
# luetaan tiedostosta henkilöt listaan
with open("henkilot.csv") as tiedosto:
    for rivi in tiedosto:
        osat = rivi.split(";")
        henkilot.append((osat[0], int(osat[1]), osat[2]))

# tulostetaan nimet
for henkilo in henkilot:
    print("Nimi:", henkilo[0])

# etsitään vanhin
vanhimman_ika = -1
for henkilo in henkilot:
    nimi = henkilo[0]
    ika = henkilo[1]
    if ika > vanhimman_ika:
        vanhimman_ika = ika
        vanhin = nimi
print("vanhin on", vanhin)
```

## Mera om att behandla CSV-filer

Vi fortsätter behandla filen `vitsord.csv`, som innehåller det följande:

<sample-data>

Pekka;5;4;5;3;4;5;5;4;2;4
Paula;3;4;2;4;4;2;3;1;3;3
Pirjo;4;5;5;4;5;5;4;5;4;4

</sample-data>

Följande program skapar lexikonet `vitsord` baserat på innehållet i filen. Nycklarna är elevernas namn och värdet som är kopplat till nycklarna innehåller elevens vitsord. Programmet konverterar vitsorden till heltal så att de kan behandlas enklare.

```python
arvosanat = {}
with open("arvosanat.csv") as tiedosto:
    for rivi in tiedosto:
        rivi = rivi.replace("\n", "")
        osat = rivi.split(";")
        nimi = osat[0]
        arvosanat[nimi] = []
        for arvosana in osat[1:]:
            arvosanat[nimi].append(int(arvosana))

print(arvosanat)
```

<sample-output>

{'Pekka': [5, 4, 5, 3, 4, 5, 5, 4, 2, 4], 'Paula': [3, 4, 2, 4, 4, 2, 3, 1, 3, 3], 'Pirjo': [4, 5, 5, 4, 5, 5, 4, 5, 4, 4]}

</sample-output>

Nu kan vi skriva ut statistik om varje studerande, baserat på värdena i lexikonet:

```python
for nimi, lista in arvosanat.items():
    paras = max(lista)
    keskiarvo = sum(lista) / len(lista)
    print(f"{nimi}: paras arvosana {paras}, keskiarvo {keskiarvo:.2f}")
```

<sample-output>

Pekka: paras arvosana 5, keskiarvo 4.10
Paula: paras arvosana 4, keskiarvo 2.90
Pirjo: paras arvosana 5, keskiarvo 4.50

</sample-output>

Ta en titt på programmet i exemplet ovan. Det kan verka något komplicerat på en första titt, men tekniken kan användas med flera olika typer av data.

## Ta bort överflödiga rader, mellanslag och radbrytningar

Låt oss säga att vi har en CSV-fil med namn, exporterat från Excel:

```sh
etunimi; sukunimi
Pekka; Python
Jaana; Java
Heikki; Haskell
```

Excel är ökänt för att lägga till extra mellanrum lite här och där. Här har vi ett extra mellanrum mellan elementen, efter varje semikolon.

Vi skulle vilja skriva ut efternamnet på varje person som finns i listan. Den första raden i filen innehåller information om den data som följer och kan skippas:

```python
sukunimet = []
with open("henkilot.csv") as tiedosto:
    for rivi in tiedosto:
        osat = rivi.split(";")
        # ohitetaan otsikkorivi
        if osat[0] == "etunimi":
            continue
        sukunimet.append(osat[1])

print(sukunimet)
```

När koden körs får vi den här utskriften:

<sample-output>

[' Python\n', ' Java\n', ' Haskell']

</sample-output>

De två första elementen har ett radbrytningstecken i slutet och alla tre element har ett mellanslag i början. Vi har redan använt `replace`-metoden för att ta bort onödigt mellanrum, men ett bättre sätt är `strip`-metoden hos strängar. Den här metoden tar bort mellanrum från början och slutet av en sträng. Metoden tar bort mellanrum, radbrytningar, samt tabb- och andra tecken som normalt inte skulle skrivas ut.

Vi kan testa på metoden i Python-terminalen:

```python
>>> " koe ".strip()
'koe'
>>> "\n\ntesti\n".strip()
'testi'
>>>
```

Att ta bort de onödiga tecknen kräver bara en liten ändring i programmet:

```python
sukunimet = []
with open("henkilot.csv") as tiedosto:
    for rivi in tiedosto:
        osat = rivi.split(';')
        if osat[0] == "etunimi":
            continue # tämä oli otsikkorivi, ei huomioida!
        sukunimet.append(osat[1].strip())
print(sukunimet)
```

Nu har får vi den önskade utskriften:

<sample-output>

['Python', 'Java', 'Haskell']

</sample-output>

Strängmetoderna `lstrip` och `rstrip` fungerar lika som metoden `strip`, men gör det då bara för antingen vänstra (l) eller högra (r) kanten av strängen:

```python
>>> " testimerkkijono  ".rstrip()
' testimerkkijono'
>>> " testimerkkijono  ".lstrip()
'testimerkkijono  '
```

## Kombinera data från olika filer

Det är mycket vanligt att data som behandlas av ett program finns utspritt i flera filer. Vi tar en titt på ett exempel där personalens information i ett företag finns i filen `personal.csv`:

```csv
hetu;nimi;osoite;kaupunki
080488-123X;Pekka Mikkola;Vilppulantie 7;00700 Helsinki
290274-044S;Liisa Marttinen;Mannerheimintie 100 A 10;00100 Helsinki
010479-007Z;Arto Vihavainen;Pihapolku 4;01010 Kerava
010499-345K;Leevi Hellas;Tapiolantie 11 B;02000 Espoo
```

Löneuppgifterna finns i en skild fil, `lon.csv`:

```csv
hetu;palkka;bonus
080488-123X;3300;0
290274-044S;4150;200
010479-007Z;1300;1200
```

Alla rader i båda filerna innehåller en personlig id-kod (pic) som identifierar vems data vi arbetar med. När vi använder det här id:t som gemensam faktor, är det lätt att koppla en arbetstagares namn med hennes lön. Vi kan till exempel skriva ut en lista över de månatliga inkomsterna:

<sample-output>

<pre>
ansiot:
Pekka Mikkola    3300 euroa
Liisa Marttinen  4350 euroa
Arto Vihavainen  2500 euroa
</pre>

</sample-output>

Programmet använder två lexikon som hjälpdatastrukturer: `namn` och `loner`. Båda använder pic som nyckel:

```python
nimet = {}

with open("tyontekijat.csv") as tiedosto:
    for rivi in tiedosto:
        osat = rivi.split(';')
        if osat[0] == "hetu":
            continue
        nimet[osat[0]] = osat[1]

palkat = {}

with open("palkat.csv") as tiedosto:
    for rivi in tiedosto:
        osat = rivi.split(';')
        if osat[0] == "hetu":
            continue
        palkat[osat[0]] = int(osat[1]) +int(osat[2])

print("ansiot:")

for hetu, nimi in nimet.items():
    if hetu in palkat:
        palkka = palkat[hetu]
        print(f"{nimi:16} {palkka} euroa")
    else:
        print(f"{nimi:16} 0 euroa")
```

Först skapar programmet lexikonen `namn` och `loner`. De har dessa innehåll:

```sh
{
    '080488-123X': 'Pekka Mikkola',
    '290274-044S': 'Liisa Marttinen',
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

<programming-exercise name='Kurssin tulokset, osa 1' tmcname='osa06-04_kurssin_tulokset_osa1'>

Ohjelma käsittelee kahta CSV-muotoista tiedostoa. Toisessa on tieto opiskelijoista:

```csv
opnro;etunimi;sukunimi
12345678;pekka;peloton
12345687;jaana;javanainen
12345699;liisa;virtanen
```

ja toisessa opiskelijoiden viikoittaisesta tehtävien lukumäärästä:

```csv
opnro;v1;v2;v3;v4;v5;v6;v7
12345678;4;1;1;4;5;2;4
12345687;3;5;3;1;5;4;6
12345699;10;2;2;7;10;2;2
```

Molempien CSV-tiedostojen ensimmäinen rivi on otsikkorivi, joka kertoo kunkin kentän sisällön.

Tee ohjelma, joka kysyy tiedostojen nimet ja tämän jälkeen tulostaa kunkin opiskelijan tehtävien yhteenlasketun määrän. Ohjelma toimii seuraavasti, kun tiedostojen sisältö on yllä oleva:

<sample-output>

Opiskelijatiedot: **opiskelijat1.csv**
Tehtävätiedot: **tehtavat1.csv**
pekka peloton 21
jaana javanainen 27
liisa virtanen 35

</sample-output>

Vinkki: Ohjelman testaileminen on toivottoman hidasta, jos käyttäjä joutuu kirjoittamaan syötteen aina käsin. Testausvaiheessa syötteet kannattaakin antaa "kovakoodaamalla" ne esim. seuraavasti:

```python
if False:
    # tänne ei tulla
    opiskelijatiedot = input("Opiskelijatiedot: ")
    tehtavatiedot = input("Tehtävätiedot: ")
else:
    # kovakoodatut syötteet
    opiskelijatiedot = "opiskelijat1.csv"
    tehtavatiedot = "tehtavat1.csv"
```

Ohjelman varsinainen toiminnallisuus on nyt "piilotettu" ehdon `False`-haaraan, jota ei suoriteta koskaan.

Jos taas halutaan nopeasti tarkastaa, toimiiko ohjelma myös käyttäjän kirjoittaessa syötteen, voidaan arvo `False` muuttaa arvoksi `True`:

```python

if True:
    opiskelijatiedot = input("Opiskelijatiedot: ")
    tehtavatiedot = input("Tehtävätiedot: ")
else:
    # tänne ei tulla!
    opiskelijatiedot = "opiskelijat1.csv"
    tehtavatiedot = "tehtavat1.csv"
```

Kun koodi on kunnossa, voi ehtorakenteen poistaa.

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!

**Toinen huomio** Jos VS Code ei löydä tiedostoa vaikka olet tarkastanut tiedoston nimen kirjoitusasun, voit [täällä](/osa-6/1-tiedostojen-lukeminen#mita-jos-vs-code-ei-loyda-tiedostoja-koodia-suoritettaessa) kokeilla olevaa ohjetta.

</programming-exercise>

<programming-exercise name='Kurssin tulokset, osa 2' tmcname='osa06-05_kurssin_tulokset_osa2'>

Edellinen tehtävä laajenee vielä siten, että myös opiskelijan koepisteet luetaan CSV-tiedostosta. Tiedoston sisältö näyttää seuraavalta:

```csv
opnro;k1;k2;k3
12345678;4;1;4
12345687;3;5;3
12345699;10;2;2
```

Esimerkiksi opiskelija jonka opiskelijanumero on 12345678 on saanut kokeesta 4+1+4 eli yhteensä 9 pistettä.

Ohjelma kysyy tiedostojen nimet ja tulostaa jokaisen opiskelijan arvosanan:

<sample-output>

Opiskelijatiedot: **opiskelijat1.csv**
Tehtävätiedot: **tehtavat1.csv**
Koepisteet: **koepisteet1.csv**
pekka peloton 0
jaana javanainen 1
liisa virtanen 3

</sample-output>

Tehtyjen harjoitustehtävien määrästä saa _pisteitä_ siten, että vähintään 10 % tehtävämäärästä tuo 1 pisteen, vähintään 20% tuo 2 pistettä jne., ja 100 % eli 40 harjoitustehtävää tuo 10 pistettä. Harjoitustehtävistä saatava pistemäärä on kokonaisluku.

Kurssin arvosana määräytyy kokeen ja harjoituspisteiden summan perusteella seuraavan taulukon mukaan:

kokeen pisteet + harjoitusten pisteet   | arvosana
:--:|:----:
0-14 | 0 (eli hylätty)
15-17 | 1
18-20 | 2
21-23 | 3
24-27 | 4
28- | 5

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!

</programming-exercise>

<programming-exercise name='Kurssin tulokset, osa 3' tmcname='osa06-06_kurssin_tulokset_osa3'>

Tässä tehtävässä muotoillaan edellisen tehtävän tulostus parempaan muotoon:

<sample-output>

Opiskelijatiedot: **opiskelijat1.csv**
Tehtävätiedot: **tehtavat1.csv**
Koepisteet: **koepisteet1.csv**
<pre>
nimi                          teht_lkm  teht_pist koe_pist  yht_pist  arvosana
pekka peloton                 21        5         9         14        0
jaana javanainen              27        6         11        17        1
liisa virtanen                35        8         14        22        3
</pre>

</sample-output>

Jokaisella rivillä siis tulostetaan opiskelijan tehtävien lukumäärä, tehtävistä saatavat pisteet, kokeen pisteet, yhteispisteet (koe+harjoitukset) sekä arvosana "siististi" siten, että tulostus on jaoteltu sarakkeisiin. Nimisarakkeen leveys on 30 merkkiä ja muiden sarakkeiden leveys on tasan 10 merkkiä.

Tehtävässä kannattaa käyttää [osassa 4](/osa-4/5-tulostuksen-muotoilu) käsiteltyjä f-merkkijonoja.

Kannattaa huomata, että merkkijonojen ja lukujen tulostaminen noudattaa hieman erilaista logiikkaa f-merkkijonoissa:

```python
sana = "python"
print(f"{sana:10}jatkuu")
print(f"{sana:>10}jatkuu")
```

<sample-output>

<pre>
python    jatkuu
    pythonjatkuu
</pre>

</sample-output>

Oletusarvoisesti siis merkkijono sisentyy määritellyn levyisen alueen _vasempaan_ reunaan. Merkillä `>`voidaan ohjata tulostus sisentymään oikeaan reunaan.

Lukuja tulostettaessa logiikka on päinvastainen

```python
luku = 42
print(f"{luku:10}jatkuu")
print(f"{luku:<10}jatkuu")
```

<sample-output>

<pre>
        42jatkuu
42        jatkuu
</pre>

</sample-output>

Oletusarvo lukujen yhteydessä on tulostuksen sisentyminen _oikeaan_ reunaan. Merkillä `<` voidaan ohjata luvun tulostus sisentymään vasempaan reunaan.

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!

</programming-exercise>

<programming-exercise name='Spell checker' tmcname='osa06-07_spellchecker'>

Tee ohjelma, joka pyytää käyttäjää kirjoittamaan rivin englanninkielistä tekstiä. Ohjelma suorittaa tekstille oikeinkirjoitustarkistuksen ja tulostaa saman tekstin siten, että kaikki väärin kirjoitetut sanat on ympäröity tähdillä. Seuraavassa kaksi käyttöesimerkkiä:

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

Kirjainten koolla ei ole merkitystä ohjelman toiminnan kannalta.

Ohjelma tunnistaa oikein kirjoitetut sanat käyttämällä tehtäväpohjassa olevaa tiedostoa `wordlist.txt`.

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!

**Toinen huomio** Jos VS Code ei löydä tiedostoa vaikka olet tarkastanut tiedoston nimen kirjoitusasun, voit [täällä](/osa-6/1-tiedostojen-lukeminen#mita-jos-vs-code-ei-loyda-tiedostoja-koodia-suoritettaessa) kokeilla olevaa ohjetta.


</programming-exercise>

<programming-exercise name='Reseptihaku' tmcname='osa06-08_reseptihaku'>

Tässä tehtävässä tehdään ohjelma, joka tarjoaa käyttäjälle mahdollisuuden reseptien hakuun reseptin nimen, valmistusajan tai raaka-aineen nimen perusteella. Ohjelma lukee reseptit käyttäjän antamasta tiedostosta.

Jokainen resepti koostuu kolmesta tai useammasta rivistä reseptitiedostossa. Ensimmäisellä rivillä on reseptin nimi, toisella rivillä reseptin valmistusaika (kokonaisluku), ja kolmas ja sitä seuraavat rivit kertovat reseptin raaka-aineet. Reseptin raaka-aineiden kuvaus päättyy tyhjään riviin, poislukien viimeinen resepti. Tiedostossa voi olla useampia reseptejä. Alla kuvattuna esimerkkitiedosto.

```sh
Lettutaikina
15
maito
kananmuna
jauho
sokeri
suola
voi

Lihapullat
45
jauheliha
kananmuna
korppujauho

Tofurullat
30
tofu
riisi
vesi
porkkana
kurkku
avokado
wasabi

Pullataikina
60
maito
hiiva
kananmuna
suola
sokeri
kardemumma
voi
```

**Vihje** tässä tehtävässä lienee järkevintä lukea ensin tiedoston rivit listalle ja käsitellä sitten tätä listaa tehtävän edellyttämällä tavalla.

#### reseptien haku nimen perusteella

Tee funktio `hae_nimi(tiedosto: str, sana: str)` joka hakee parametrina annetun nimisestä tiedostosta reseptit, joiden nimessä esiintyy toisena parametrina annettu merkkijono. Funktio palauttaa listan, jossa kutakin löydettyä reseptiä vastaa merkkijono, joka kertoo reseptin nimen.

Esimerkki funktion käytöstä:

```python
loydetyt = hae_nimi("reseptit1.txt", "pulla")

for resepti in loydetyt:
    print(resepti)
```

<sample-output>

Lihapullat
Pullataikina

</sample-output>

Huomaa, että hakusanojen kirjainten koolla ei ole merkitystä, eli hakusana _pulla_ löytää myös reseptin _Pullataikina_, joka alkaa isolla kirjaimella.

**Huom!** Jos VS Code ei löydä tiedostoa vaikka olet tarkastanut tiedoston nimen kirjoitusasun, voit [täällä](/osa-6/1-tiedostojen-lukeminen#mita-jos-vs-code-ei-loyda-tiedostoja-koodia-suoritettaessa) kokeilla olevaa ohjetta.


#### reseptien hakeminen valmistusajan perusteella

Tee funktio `hae_aika(tiedosto: str, aika: int)` joka hakee parametrina annetun nimisestä tiedostosta reseptit, joiden valmistusaika on korkeintaan parametrina kerrottu minuuttimäärä.

Kriteerin täyttävät reseptit palautetaan edellisen tehtävän tapaan listana, nyt kerrotaan myös reseptin valmistumisaika. Esimerkki funktion käytöstä:

```python
loydetyt = hae_aika("reseptit1.txt", 20)

for resepti in loydetyt:
    print(resepti)
```

<sample-output>

Lettutaikina, valmistusaika 15 min

</sample-output>

#### reseptien hakeminen raaka-aineen perusteella

**Varoitus** tämä osa on edellisiä selvästi haastavampi. Jos tehtävä ei lähde heti aukenemaan, kannattanee tehdä ensin osan muut tehtävät ja palata lopuksi takaisin tähän. Huomaa, että voit lähettää moniosaisessa tehtävässä palvelimelle myös yksittäiset osat

Tee funktio `hae_raakaaine(tiedosto: str, aine: str)` joka hakee parametrina annetun nimisestä tiedostosta reseptit, jotka sisältävät toisena parametrina annetun raaka-aineen.

Kriteerin täyttävät reseptit palautetaan edellisen tehtävän tapaan listana. Esimerkki funktion käytöstä:

```python
loydetyt = hae_raakaaine("reseptit1.txt", "maito")

for resepti in loydetyt:
    print(resepti)
```

<sample-output>

Lettutaikina, valmistusaika 15 min
Pullataikina, valmistusaika 60 min

</sample-output>

</programming-exercise>

<programming-exercise name='Kaupunkipyörät' tmcname='osa06-09_kaupunkipyorat'>

Tässä tehtävässä tehdään muutama funktio, joiden avulla voidaan tarkastella [kaupunkipyörien](https://kaupunkipyorat.hsl.fi/fi) asemien sijaintia sisältävää tiedostoa.

Tiedostot näyttävät seuraavilta:

```csv
Longitude;Latitude;FID;name;total_slot;operative;id
24.950292890004903;60.155444793742276;1;Kaivopuisto;30;Yes;001
24.956347471358754;60.160959093887129;2;Laivasillankatu;12;Yes;002
24.944927399779715;60.158189199971673;3;Kapteeninpuistikko;16;Yes;003
```

Kutakin asemaa kohti tiedostossa on yksi rivi, joka kertoo aseman koordinaatit, aseman nimen ja muuta tunnistetietoa.

#### asemien välinen etäisyys

Tee ensin funktio `hae_asematiedot(tiedosto: str)`, joka lukee asematiedot tiedostosta ja palauttaa ne sanakirjana, joka näyttää tältä:

<sample-output>

<pre>
{
  "Kaivopuisto: (24.950292890004903, 60.155444793742276),
  "Laivasillankatu: (24.956347471358754, 60.160959093887129),
  "Kapteeninpuistikko: (24.944927399779715, 60.158189199971673)
}
</pre>

</sample-output>

Eli sanakirjan avaimena on aseman nimi ja arvona tuple, joka koostuu aseman koordinaateista, ensimmäisenä _Longitude_ ja toisena _Latitude_.

Tee seuraavaksi funktio `etaisyys(asemat: dict, asema1: str, asema2: str)`, joka palauttaa parametrina kerrottujen asemien välisen etäisyyden.

Etäisyys lasketaan seuraavalla kaavalla (hyödyntäen Pythagoraan lausetta):

```python
# tämä rivi tarvitaan, jotta saadaan käyttöön metodi sqrt
import math

x_kilometreina = (longitude1 - longitude2) * 55.26
y_kilometreina = (latitude1 - latitude2) * 111.2
etaisyys = math.sqrt(x_kilometreina**2 + y_kilometreina**2)
```

Esimerkkisuorituksia:

```python
asemat = hae_asematiedot('stations1.csv')
e = etaisyys(asemat, "Designmuseo", "Hietalahdentori")
print(e)
e = etaisyys(asemat, "Viiskulma", "Kaivopuisto")
print(e)
```

<sample-output>

0.9032737292463177
0.7753594392019532

</sample-output>

**Huom!** Jos VS Code ei löydä tiedostoa vaikka olet tarkastanut tiedoston nimen kirjoitusasun, voit [täällä](/osa-6/1-tiedostojen-lukeminen#mita-jos-vs-code-ei-loyda-tiedostoja-koodia-suoritettaessa) kokeilla olevaa ohjetta.

#### pisin välimatka

Tee funktio `suurin_etaisyys(asemat: dict)`, joka selvittää, mitkä kaksi asemaa ovat kauimpana toisistaan. Funktio palauttaa tuplen, jonka ensimmäiset kaksi arvoa kertovat asemien nimet ja kolmas arvo niiden välisen etäisyyden.

```python
asemat = hae_asematiedot('stations1.csv')
asema1, asema2, suurin = suurin_etaisyys(asemat)
print(asema1, asema2, suurin)
```

<sample-output>

Laivasillankatu Hietalahdentori 1.478708873076181

</sample-output>

</programming-exercise>


<quiz id="cdac5075-c9cf-56f5-9ea3-eda73a48df4e"></quiz>
