---
path: '/osa-4/6-lisaa-rakenteista'
title: 'Mera strängar och listor'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* kommer du att vara bekant med flera metoder för att extrahera delar av strängar och listor
* förstår du vad oföränderlighet hos strängar innebär
* kan du använda dig av metoderna `count` och `replace`.

</text-box>

Du är redan bekant med syntaxen `[]` för att ta fram en delsträng:

```python
mjono = "esimerkki"
print(mjono[3:7])
```

<sample-output>

merk

</sample-output>

Samma syntax fungerar med listor. Dellistor kan extraheras på samma sätt som delsträngar:

```python
lista = [3,4,2,4,6,1,2,4,2]
print(lista[3:7])
```

<sample-output>

[4, 6, 1, 2]

</sample-output>

## Mera extrahering

Syntaxen `[]` fungerar faktiskt mycket lika som `range`-funktionen, vilket innebär att vi också kan ge den ett steg:

```python
mjono = "esimerkki"
print(mjono[0:7:2])
lista = [1,2,3,4,5,6,7,8]
print(lista[6:2:-1])
```

<sample-output>

eiek
[7, 6, 5, 4]

</sample-output>

Om vi lämnar bort något av indexen kommer operatorn att inkludera alla element. Tack vare detta kan vi till exempel skriva ett mycket kort program som vänder om en sträng:

```python
mjono = input("Kirjoita merkkijono: ")
print(mjono[::-1])
```

<sample-output>

Kirjoita merkkijono: **esimerkki**
ikkremise

</sample-output>

<!--vastaava varoitusteksti löytyy osioista 3-4, 4-6 ja 5-1, tsekkaa kaikki jos muokkaat-->
## Varoitus: globaalin muuttujan käyttö funktion sisällä

Funktioiden sisällä on mahdollista määritellä muuttujia, mutta tämän lisäksi funktio näkee sen ulkopuolella pääohjelmassa määritellyt muuttujat. Tälläisia muuttujia sanotaan _globaaleiksi_ muuttujiksi.

Globaalien muuttujien käyttämistä funktioista käsin ei useimmiten pidetä hyvänä asiana muun muassa siksi, että ne saattavat johtaa ikäviin bugeihin.

Seuraavassa on esimerkki funktiosta, joka käyttää "vahingossa" globaalia muuttujaa:

```python
def tulosta_vaarinpain(nimet: list):
    # käytetään vahingossa parametrin sijaan globaalia muuttujaa nimilista
    i = len(nimilista) - 1
    while i >= 0:
        print(nimilista[i])
        i -= 1

# globaali muuttuja
nimilista = ["Antti", "Emilia", "Erkki", "Margaret"]
tulosta_vaarinpain(nimilista)
print()
tulosta_vaarinpain(["Tupu", "Hupu", "Lupu"])
```

<sample-output>

Margaret
Erkki
Emilia
Antti

Margaret
Erkki
Emilia
Antti

</sample-output>

Vaikka funktiota kutsutaan oikein, se tulostaa aina globaalissa muuttujassa _nimilista_ olevat nimet.

Kaikki funktioita testaava koodi on kirjoitettava erillisen lohkon sisälle, jotta TMC-testit hyväksyisivät koodin. Edellinen esimerkki siis tulisi toteuttaa seuraavasti:

```python
def tulosta_vaarinpain(nimet: list):
    # käytetään vahingossa parametrin sijaan globaalia muuttujaa nimilista
    i = len(nimilista) - 1
    while i>=0:
        print(nimilista[i])
        i -= 1

# kaikki funktiota testaava koodi tämän lohkon sisälle
if __name__ == "__main__":
    # globaali muuttuja
    nimilista = ["Antti", "Emilia", "Erkki", "Margaret"]
    tulosta_vaarinpain(nimilista)
    print()
    tulosta_vaarinpain(["Tupu", "Hupu", "Lupu"])
```

Nyt myös globaalin muuttujan määrittely on siirtynyt `if`-lohkoon.

TMC-testit suoritetaan aina siten, että mitään `if`-lohkon sisällä olevaa koodia ei suoriteta. Tämän takia funktio ei voi edes teoriassa toimia, sillä se viittaa muuttujaan `nimilista`, jota ei testejä suoritettaessa ole lainkaan olemassa.

<programming-exercise name='Kaikki väärinpäin' tmcname='osa04-21_kaikki_vaarinpain'>

Kirjoita funktio `kaikki_vaarinpain`, joka saa parametrikseen listan merkkijonoja. Funktio luo ja palauttaa uuden listan, jossa kaikki alkuperäisellä listalla olevat merkkijonot on käännetty. Myös listan alkioiden järjestys muutetaan käänteiseksi.

Esimerkki funktion käytöstä:

```python
lista = ["Moi", "kaikki", "esimerkki", "vielä yksi"]
lista2 = kaikki_vaarinpain(lista)
print(lista2)
```

<sample-output>

['isky äleiv', 'ikkremise', 'ikkiak', 'ioM']

</sample-output>

</programming-exercise>

## Strängar är oföränderliga

Strängar och listor har en hel del likheter, framför allt då det kommer till hur de fungerar med olika operatorer. En nyckelskillnad är att strängar är oföränderliga. Det betyder att de inte kan ändras.

```python
mjono = "esimerkki"
mjono[0] = "a"
```

Strängar kan inte ändras på, så det här programmet kommer att ge ett felmeddelande:

<sample-output>

TypeError: 'str' object does not support item assignment

</sample-output>

Ett liknande fel uppstår om du försöker ordna en sträng med `sort`-metoden.

Strängar är oföränderliga, men variablerna som lagrar dem är inte det. En sträng kan ersättas med en annan sträng.

De följande exemplen är alltså till sin grund olika:

```python
lista = [1,2,3]
lista[0] = 10
```

<img src="4_4_1.png">

```python
mjono = "Moi"
mjono = mjono + "!"
```

<img src="4_4_2.png">

Det första exemplet ändrar på innehållet i den lista som man hänvisar till. I det andra exemplet ersätts hänvisningen till den ursprungliga strängen med en hänvisning till en ny sträng. Den ursprungliga strängen finns fortfarande någonstans i datorns minne, men det saknas en referens till strängen så den kan inte längre användas i programmet.

Vi återkommer till det här ämnet senare. Då utforskar vi hänvisningar till listor närmare.

## Mera metoder hos listor och strängar

Metoden `count` räknar antalet gånger ett element eller en delsträng finns i en lista eller sträng:

```python
mjono = "Vesihiisi sihisi hississä"
print(mjono.count("si"))

lista = [1,2,3,1,4,5,1,6]
print(lista.count(1))
```

<sample-output>

5
3

</sample-output>

Metoden räknar inte överlappande förekomster. Till exempel i strängen `aaaa` räknar metoden upp till två förekomster av delsträngen `aa`, även om det finns tre stycken om överlappande förekomster skulle tillåtas.

Metoden `replace` skapar en ny sträng där en specifik delsträng har ersatts med en annan sträng:

```python
mjono = "Moi kaikki"
uusi = mjono.replace("Moi", "Hei")
print(uusi)
```

<sample-output>

Hei kaikki

</sample-output>

Metoden påverkar alla delsträngar som hittas:

```python
lause = "hei heilan löysin minä heinikosta hei"
print(lause.replace("hei", "HEI"))
```

<sample-output>

HEI HEIlan löysin minä HEInikosta HEI

</sample-output>

När `replace`-metoden används, är ett vanligt misstag att man glömmer att strängar är oföränderliga:

```python
mjono = "Python on kivaa"

# Korvataan alijono, muttei tallenneta tulosta mihinkään...
mjono.replace("Python", "Java")
print(mjono)
```

<sample-output>

Python on kivaa

</sample-output>

Om den gamla strängen inte längre behövs kan man tilldela den nya strängen till samma variabel:

```python
mjono = "Python on kivaa"

# Korvataan alijono, tallennetaan tulos samaan muuttujaan
mjono = mjono.replace("Python", "Java")
print(mjono)
```

<sample-output>

Java on kivaa

</sample-output>

<programming-exercise name='Eniten kirjaimia' tmcname='osa04-22_eniten_kirjaimia'>

Kirjoita funktio `eniten_kirjainta`, joka saa parametrikseen merkkijonon. Funktio palauttaa kirjaimen, jota esiintyy eniten merkkijonossa. Jos yhtä yleisiä kirjaimia on monta, funktion tulee palauttaa niistä ensimmäisenä merkkijonossa esiintyvä.

Esimerkki funktion käytöstä:

```python
mjono = "abcbdbe"
print(eniten_kirjainta(mjono))

toinen_jono = "esimerkkimerkkijonokki"
print(eniten_kirjainta(toinen_jono))
```

<sample-output>

b
k

</sample-output>

</programming-exercise>


<programming-exercise name='Vokaalit pois' tmcname='osa04-23_vokaalit_pois'>

Kirjoita funktio `ilman_vokaaleja`, joka saa parametrikseen merkkijonon. Funktio palauttaa uuden merkkijonon, jossa alkuperäisen merkkijonon vokaalit on poistettu.

Voit olettaa, että merkkijono koostuu pelkästään pienistä suomen kielen kirjaimista a...ö.

Esimerkki funktion käytöstä:

```python
mjono = "tämä on esimerkki"
print(ilman_vokaaleja(mjono))
```

<sample-output>

tm n smrkk

</sample-output>

</programming-exercise>


<programming-exercise name='Poista isot' tmcname='osa04-24_poista_isot'>

Pythonin merkkijonometodi `isupper()` palauttaa arvon `True`, jos merkkijono koostuu _pelkästään isoista kirjaimista_.

Esimerkiksi:

```python
print("XYZ".isupper())

onko_iso = "Abc".isupper()
print(onko_iso)
```

<sample-output>

True
False

</sample-output>

Kirjoita metodia hyödyntäen funktio `poista_isot`, joka saa parametrikseen listan merkkijonoja. Funktio palauttaa uuden listan, jolla on sen parametrina olevasta listasta ne merkkijonot, jotka eivät koostu kokonaan isoista kirjaimista.


Esimerkki funktion käytöstä:

```python
lista = ["ABC", "def", "ISO", "TOINENISO", "pieni", "toinen pieni", "Osittain Iso"]
karsittu_lista = poista_isot(lista)
print(karsittu_lista)
```

<sample-output>

['def', 'pieni', 'toinen pieni', 'Osittain Iso']

</sample-output>

</programming-exercise>

<programming-exercise name='Naapureita listassa' tmcname='osa04-25_naapureita_listassa'>

Määritellään, että listan alkiot ovat naapureita, jos niiden erotus on 1. Naapureita olisivat siis esim alkiot 1 ja 2 tai alkiot 56 ja 55.

Kirjoita funktio `pisin_naapurijono`, joka etsii listasta pisimmän peräkkäisiä naapureita sisältävän osalistan ja palauttaa sen pituuden.

Esimerkiksi listassa `[1, 2, 5, 4, 3, 4]` pisin tällainen osalista olisi `[5, 4, 3, 4]`, ja sen pituus 4.

Esimerkki funktion kutsumisesta:

```python
lista = [1, 2, 5, 7, 6, 5, 6, 3, 4, 1, 0]
print(pisin_naapurijono(lista))
```

<sample-output>

4

</sample-output>

</programming-exercise>

## Skapa ett större programmeringsprojekt

Den här fjärde modulen avslutas med ett lite större programmeringsprojekt där du får utnyttja det du lärt dig hittills.

Den viktigaste regeln när man börjar med ett programmeringsprojekt är att man inte ska försöka lösa alla problem samtidigt. Programmet ska bestå av mindre delar, till exempel hjälpfunktioner. Du ska testa att varje del fungerar före du fortsätter framåt. Om du försöker göra för mycket samtidigt kommer du högst antagligen hamna i en situation som präglas av kaos och mera kaos.

Du kommer att behöva ett sätt att testa dina funktioner utanför huvudfunktionen. Du kan uppnå det här genom att definiera en skild huvudfunktion som du anropar utanför alla andra funktioner i programmet. Det är enkelt att tillfälligt kommentera bort ett funktionsanrop när man testar programmet. De första stegen i utförandet av programmeringsprojektet skulle kunna se ut så här:

```python
def main():
    pisteet = []
    # ohjelman koodi tänne

main()
```

Nu kan hjälpfunktionerna köras utan att huvudfunktionen körs:

```python
# apufunktio, joka laskee arvosanan pisteiden perusteella
def arvosana(pisteet):
    # koodia

def main():
    pisteet = []
    # ohjelman koodi tänne

# kommentoidaan pääohjelma pois
#main()

# testataan apufunktiota
pistemaara = 35
tulos = arvosana(pistemaara)
print(tulos)
```

## Skicka data från en funktion till en annan

När ett program innehåller flera funktioner uppstår en fråga: hur skickar jag data från en funktion till en annan?

I följande exempel frågar man efter några heltal från användaren. Programmet skriver sedan ut dessa värden och utför en "analys" på dem. Programmet är uppdelat i tre skilda funktioner:

```python
def lue_kayttajalta(maara: int):
    print(f"Syötä {maara} lukua:")
    luvut = []

    for i in range(maara):
        luku = int(input("Anna luku: "))
        luvut.append(luku)

    return luvut

def tulosta(luvut: list):
    print("Luvut ovat: ")
    for luku in luvut:
        print(luku)

def analysoi(luvut: list):
    keskiarvo = sum(luvut) / len(luvut)
    return f"Lukuja yhteensä {len(luvut)}, keskiarvo {keskiarvo}, pienin {min(luvut)} ja suurin {max(luvut)}"

# funktioita käyttävä "pääohjelma"
syotteet = lue_kayttajalta(5)
tulosta(syotteet)
analyysin_tulos = analysoi(syotteet)
print(analyysin_tulos)
```

När programmet körs, skulle det kunna se ut så här:

<sample-output>

Syötä 5 lukua:
Anna luku: **10**
Anna luku: **34**
Anna luku: **-32**
Anna luku: **99**
Anna luku: **-53**
Luvut ovat:
10
34
-32
99
-53
Lukuja yhteensä 5, keskiarvo 11.6, pienin -53 ja suurin 99

</sample-output>

Idén är att huvudfunktionen "lagrar" all data som behandlas av programmet. I det här fallet är det enda som vi behöver de värden som användaren gett, i variabeln `siffror`.

Om det här behövs i en funktion ges det som ett argument. Det här sker med funktionerna `skriv_ut_resultat` och `analysera`. Om funktionen resulterar i data som behövs på annat håll i programmet, returnerar funktionen det. Det här sparas i en variabel i huvudfunktionen. Det här sker med funktionerna `indata_fran_anvandare` och `analysera`.

Du kunde använda den globala variabeln siffror från huvudfunktionen direkt i hjälpfunktionerna. Vi har redan gått igenom varför det är en dålig idé, men här följer ännu en annan förklaring. Om funktionerna kan ändra på den globala variabeln kan oförutsedda saker börja hända i programmet, framför allt då antalet funktioner ökar.

Att skicka data ut och in från funktioner gör man alltså helst med hjälp av argument och return-värden.

Du kunde också göra huvudfunktionen till sin egen funktion. Då skulle variabeln siffor inte längre vara en global variabel, utan en lokal variabel i `main`-funktionen:

```python
# pääohjelmaa edustava funktio
def main():
    syotteet = lue_kayttajalta(5)
    tulosta(syotteet)
    analyysin_tulos = analysoi(syotteet)

    print(analyysin_tulos)

# ohjelman käynnistys
main()
```

<programming-exercise name='Arvosanatilasto' tmcname='osa04-26_arvosanatilasto'>

Tässä tehtävässä toteutetaan ohjelma kurssin arvosanatilastojen tulostamiseen.

Ohjelmalle syötetään rivejä, jotka sisältävät yhden opiskelijan koepistemäärän sekä tehtyjen harjoitustehtävien määrän. Ohjelma tulostaa niiden perusteella arvosanoihin liittyviä tilastoja.

Koepisteet ovat kokonaislukuja väliltä 0–20. Tehtyjen harjoitustehtävien lukumäärät taas kokonaislukuja väliltä 0–100.

Ohjelma kyselee käyttäjältä rivejä niin kauan, kunnes käyttäjä syöttää tyhjän rivin. Voit olettaa, että kaikki rivit on syötetty "oikein", eli rivillä on joko kaksi kokonaislukua tai rivi on tyhjä.

Koepisteiden ja harjoitustehtävien syöttäminen etenee seuraavasti:

<sample-output>

Koepisteet ja harjoitusten määrä: **15 87**
Koepisteet ja harjoitusten määrä: **10 55**
Koepisteet ja harjoitusten määrä: **11 40**
Koepisteet ja harjoitusten määrä: **4 17**
Koepisteet ja harjoitusten määrä:
Tilasto:

</sample-output>

Kun käyttäjä on syöttänyt tyhjän rivin, tulostaa ohjelma tilastot.

Tilastot muodostuvat seuraavasti:

Tehtyjen harjoitustehtävien lukumäärästä saa _harjoituspisteitä_ siten, että vähintään 10 % tehtävämäärästä tuo yhden harjoituspisteen, 20 % tuo 2 harjoituspistettä, jne., ja 100 % eli 100 harjoitustehtävää tuo 10 harjoituspistettä. Harjoitustehtävistä saatava pistemäärä on kokonaisluku.

Kurssin arvosana määräytyy kokeen pistemäärän ja harjoitustehtävistä saatavien pisteiden summasta seuraavan taulukon mukaan:

koepisteet+harjoituspisteet   | arvosana
:--:|:----:
0–14 | 0 (eli hylätty)
15–17 | 1
18–20 | 2
21–23 | 3
24–27 | 4
28–30 | 5

Edelliseen on kuitenkin poikkeus: jos kokeen pistemäärä on alle 10, on arvosana kokonaispistemäärästä riippumatta 0 eli hylätty.

Yllä olevalla esimerkkisyötteellä ohjelma tulostaa seuraavat tilastot:

<sample-output>

<pre>
Tilasto:
Pisteiden keskiarvo: 14.5
Hyväksymisprosentti: 75.0
Arvosanajakauma:
  5:
  4:
  3: *
  2:
  1: **
  0: *
</pre>

</sample-output>

Desimaaliluvut tulostetaan yhden desimaalin tarkkuudella.

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon! Eli jos ohjelmasi toiminnallisuus on esim. funktiossa `main`, tulee sitä kutsuva koodi kirjoittaa normaaliin tapaan, eikä ym. if-lohkoon kuten on tehtävä niissä tehtävissä, joissa edellytetään funktioiden toteuttamista.

**Vihje:**

Ohjelman syöte koostuu riveistä joilla on peräkkäin kaksi numeroa:

<sample-output>

Koepisteet ja harjoitusten määrä: **15 87**

</sample-output>

Syöterivi pitää pilkkoa ensin kahtia ja muuttaa palaset kokonaisluvuksi `int`-funktiolla. Rivin pilkkominen onnistuu samalla tavalla kun tehtävässä [Eka, toka ja vika sana](/osa-4/2-lisaa-funktioista). Siihen on olemassa myös hieman helpompi keino, merkkijonojen metodi `split`. Googlaa jos haluat, käytä esim. hakusanoja *python string split*.

<!-- **Huomaa** että tällä hetkellä Windowsissa on ongelmia joidenkin tehtävien testien suorittamisessa. Jos törmäät seuraavaan virheilmoitukseen

<img src="4_3_2.png" alt="Listan iterointi">

voit suorittaa testit lähettämällä ne palvelimelle valitsemalla testien suoritusnapin oikealla puolella olevasta symbolista avautuvasta TMC-valikosta _Submit solutions_.

Ongelman saa korjattua menemällä laajennuksen asennusvalikkoon ja muuttamalla "TMC Data" -kohdassa tehtävien sijainnin johonkin toiseen sijaintiin, jonka tiedostopolku on lyhempi, allaolevassa kuvassa nappi _change path_. Siirrossa saattaa kestää hetken, joten odotathan operaation päättymistä.

<img src="4_3_3.png" alt="Listan iterointi">

Ongelmaan pyritään saamaan parempi ratkaisu lähipäivinä. -->


</programming-exercise>


<quiz id="00a23e8f-ecc1-59b7-bd22-a78c4c3e2d4b"></quiz>

Vänligen svara på en kort enkät om den här veckans material.

<quiz id="a0b1296c-99b2-5bed-accc-2872ad2f59b6"></quiz>
