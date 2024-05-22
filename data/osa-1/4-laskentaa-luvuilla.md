---
path: "/osa-1/4-laskentaa-luvuilla"
title: "Räkneoperationer"
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* kan du använda dig av variabler i olika slags räkneoperationer
* kan du hantera siffor i indata från användare
* kan du konvertera värden till olika grundläggande datatyper.

</text-box>

I de tidigare delarna har du sett exempel med enkla räkneoperationer. Följande tabell listar de mest allmänna operatorerna som kan användas för att räkna i Python:

| Operator | Betydelse                       | Exempel    | Resultat |
|:--------:|---------------------------------|------------|----------|
| `+`      | Addition                        | `2 + 4`    |`6`       |
| `-`      | Subtraktion                     | `10 - 2.5` |`7.5`     |
| `*`      | Multiplikation                  | `-2 * 123` |`-246`    |
| `/`      | Division (resultat som flyttal) | `9 / 2`    |`4.5`     |
| `//`     | Division (resultat som heltal)  | `9 // 2`   |`4`       |
| `%`      | Rest                            | `9 % 2`    |`1`       |
| `**`     | Potens                          | `2 ** 3`   |`8`       |

Ordningen för operationerna är bekant från matematiken: potensuttryck räknas först, sedan multiplikation och division, till sist addition och subtraktion. Ordningen kan ändras genom att använda parenteser.

Till exempel denna kodsnutt…

```python
print(2 + 3 * 3)
print((2 + 3) * 3)
```

…resulterar i följande utskrift:

<sample-output>

11
15

</sample-output>

## Operand, operator och datatyper

En räkneoperation består oftast av operander och operatorer:

<img src="1_5.png">

Datatypen hos en operand bestämmer i regel datatypen hos resultatet: om två heltal adderas är resultatet också ett heltal. Om ett flyttal subtraheras från ett annat flyttal är resultatet ett flyttal. Vidare kan man notera att om en av operanderna är ett flyttal, kommer resultatet att vara ett flyttal oavsett de andra operanderna.

Division med operatorn `/` är ett undantag. Dess resultat är ett flyttal även om operanderna är heltal. Till exempel kommer operationen `1 / 5` att ge flyttalet `0.2`. Observera att Python använder punkt som decimaltecken, inte decimalkomma som vanligtvis används på svenska.

Exempel:

```python
pituus = 172.5
paino = 68.55

# painoindeksi lasketaan jakamalla paino pituuden neliöllä
# pituus ilmoitetaan kaavassa metreinä
bmi = paino / (pituus / 100) ** 2

print(f"Painoindeksi on {bmi}")
```

Programmets utskrift ser ut så här:

<sample-output>

Painoindeksi on 23.037177063642087

</sample-output>

Märk att Python också har operatorn `//`, för division med heltal som resultat. Om operanderna är heltal, kommer resultatet också att vara ett heltal. Resultatet rundas ner till närmaste heltal. Exempelvis detta program…

```python
x = 3
y = 2

print(f"/-operaattori {x/y}")
print(f"//-operaattori {x//y}")
```

…skriver ut följande:

<sample-output>

/-operaattori 1.5
//-operaattori 1

</sample-output>

## Nummer som indata

Vi har redan använt oss av `input`-funktionen för att läsa in strängar som användaren matat in. Samma funktion kan också användas för att läsa in nummer, men då måste strängen som funktionen returnerar först konverteras till någon av de datatyper som representerar ett nummer i programkoden. I den förra delen konverterade vi heltal till strängar med `str`-funktionen. Nu gäller samma princip, men vi ska använda en annan funktion eftersom vi gör konverteringen åt motsatt håll.

En sträng kan konverteras till ett heltal med funktionen `int`. Det följande programmet frågar användarens födelseår och sparar det i variabeln `indata_strang`. Programmet skapar därefter variabeln `ar` som innehåller året konverterat till heltal. Efter det går det att räkna `2021 - ar`, med hjälp av det värde användaren angett.

```python
syote = input("Minä vuonna olet syntynyt? ")
vuosi = int(syote)
print(f"Ikäsi vuoden 2020 lopussa: {2020 - vuosi}" )
```
<sample-output>

Minä vuonna olet syntynyt? **1995**
Ikäsi vuoden 2020 lopussa: 25

</sample-output>

Allt som oftast behöver man inte skapa två separata variabler (som ovan) för att läsa en siffra från användaren. Istället kan användarens text läsas in och konverteras till heltal samtidigt:

```python
vuosi = int(input("Minä vuonna olet syntynyt? "))
print(f"Ikäsi vuoden 2020 lopussa: {2020 - vuosi}" )
```

En sträng kan också konverteras till flyttal. Det sker med funktionen `float`. Det här programmet frågar användaren om hennes eller hans längd och vikt, och använder svaren för att räkna ut BMI:

```python
pituus = float(input("Anna pituus: "))
paino = float(input("Anna paino: "))

pituus = pituus / 100
bmi = paino / pituus ** 2

print(f"Painoindeksi on {bmi}")
```

Här är ett exempel på en utskrift från programmet:

<sample-output>

Anna pituus: **163**
Anna paino: **74.45**
Painoindeksi on 28.02137829801649

</sample-output>

<in-browser-programming-exercise name="Luku kertaa viisi" tmcname="osa01-13_kerrottuna_viidella">

Tee ohjelma, joka kysyy käyttäjältä lukua. Ohjelma tulostaa luvun kerrottuna viidellä.

Ohjelman tulee toimia seuraavasti:

<sample-output>

Anna luku: **3**
Kun kerrotaan 3 luvulla 5, saadaan 15

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Nimi ja ikä" tmcname="osa01-14_nimi_ja_ika">

Tee ohjelma, joka kysyy käyttäjältä tämän nimen ja syntymävuoden. Ohjelma tulostaa sitten viestin seuraavan esimerkin mukaisesti:

<sample-output>

Anna nimi: **Keijo Keksitty**
Anna syntymävuosi: **1990**
Moi Keijo Keksitty, olet 30 vuotta vanha vuoden 2020 lopussa

</sample-output>

</in-browser-programming-exercise>

## Att använda variabler

Låt oss kika på ett program som räknar summan av tre siffror som användaren anger:

```python
luku1 = int(input("Ensimmäinen luku: "))
luku2 = int(input("Toinen luku: "))
luku3 = int(input("Kolmas luku: "))

summa = luku1 + luku2 + luku3
print(f"Lukujen summa: {summa}")
```

Här har vi ett exempel på när vi kör programmet:

<sample-output>

Ensimmäinen luku: **5**
Toinen luku: **21**
Kolmas luku: **7**
Lukujen summa: 33

</sample-output>

Programmet använder fyra variabler, men i det här fallet skulle det faktiskt räcka med två variabler:

```python
summa = 0

luku = int(input("Ensimmäinen luku: "))
summa = summa + luku

luku = int(input("Toinen luku: "))
summa = summa + luku

luku = int(input("kolmas luku: "))
summa = summa + luku

print(f"Lukujen summa: {summa}")
```

Nu läses alla siffor som användaren ges in i en och samma variabel, `nummer`. Värdet på variabeln `summa` ökas med värdet på variabeln nummer varje gång användaren skriver in ett nytt nummer.

Vi tar en lite närmare titt på kommandot:

```python
summa = summa + luku
```

Här adderas värdena i variablerna `summa` och `nummer` ihop – för att lagras i variabeln summa. Till exempel om värdet på `summa` är `3` och värdet på `nummer` är `2`, kommer värdet på summa att vara `5` efter att kommandot körts.

Att öka på värdet hos en variabel är en vanlig operation. Därför finns det en liten genväg till förfogande. Den här notationen fungerar i praktiken som kommandot ovan:

```python
summa += luku
```

Det här tillåter oss skriva programmet lite mer koncist:

```python
summa = 0

luku = int(input("Ensimmäinen luku: "))
summa += luku

luku = int(input("Toinen luku: "))
summa += luku

luku = int(input("kolmas luku: "))
summa += luku

print(f"Lukujen summa: {summa}")
```

Egentligen behöver vi inte alls variabeln `nummer`. Vi kan också behandla siffrorna som användaren anger på följande sätt:

```python
summa = 0

summa += int(input("Ensimmäinen luku: "))
summa += int(input("Toinen luku: "))
summa += int(input("Kolmas luku: "))

print(f"Lukujen summa: {summa}")
```

I praktiken beror antalet variabler som behövs på situationen. Om man behöver minnas enskilda värden som användaren anger, är det inte möjligt att ”återanvända” samma variabel för att läsa in olika värden. Här är ett exempel på en sådan situation:

```python
luku1 = int(input("Ensimmäinen luku: "))
luku2 = int(input("Toinen luku: "))

print(f"{luku1} + {luku2} = {luku1+luku2}")
```

<sample-output>

Ensimmäinen luku: **2**
Toinen luku: **3**
2 + 3 = 5

</sample-output>

Å andra sidan så har programmet inte en namngiven variabel där summan av de två angivna värdena skulle lagras.

Att ”återanvända” en variabel lönar sig bara då när det finns ett tillfälligt behov att lagra värden av samma typ och orsak – till exempel då man summar ihop siffror.

I följande exempel används variabeln `data` för att lagra användarens namn och därefter dess ålder. Det finns absolut ingen logik i det!

```python
tieto = input("Mikä on nimesi? ")
print("Hei " + tieto + "!")

tieto = int(input("Mikä on ikäsi? "))
# ohjelma jatkuu...
```

En bättre idé vore att använda skilda variabler med namn som tydligt beskriver deras funktion:

```python
nimi = input("Mikä on nimesi? ")
print("Hei " + nimi + "!")

ika = int(input("Mikä on ikäsi? "))
# ohjelma jatkuu...
```

<in-browser-programming-exercise name="Vuorokaudet sekunteina" tmcname="osa01-15_sekunteja_vuorokaudessa">

Tee ohjelma, joka kysyy käyttäjältä vuorokausien lukumäärän. Tämän jälkeen ohjelma tulostaa sekuntien määrän annetuissa vuorokausissa.

Ohjelman tulee toimia seuraavasti:

<sample-output>

Kuinka monen vuorokauden sekunnit tulostetaan? **1**
86400

</sample-output>

Toinen esimerkki:

<sample-output>

Kuinka monen vuorokauden sekunnit tulostetaan? **7**
604800

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Korjaa ohjelma: Lukujen tulo" tmcname="osa01-20_korjaa_ohjelma_lukujen_tulo">

Oheinen ohjelma kysyy käyttäjältä kolme lukua ja tulostaa näiden tulon (eli luvut kerrottuna toisillaan).
Ohjelmassa on kuitenkin virhe tai virheitä, joiden takia se ei toimi. Korjaa ohjelma sellaiseksi, että se toimii oikein.

Ohjelman siis pitäisi toimia esimerkiksi näin:

<sample-output>

Anna luku 1: **2**
Anna luku 2: **3**
Anna luku 3: **5**
Tulo on 30

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Lukujen summa ja tulo" tmcname="osa01-16_lukujen_summa_ja_tulo">

Tee ohjelma joka kysyy käyttäjältä kaksi lukua. Ohjelma tulostaa lukujen summan ja tulon.

Ohjelman tulee toimia seuraavasti:

<sample-output>

Luku 1: **3**
Luku 2: **7**
Lukujen summa 10
Lukujen tulo 21

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Lukujen summa ja keskiarvo" tmcname="osa01-17_lukujen_summa_ja_keskiarvo">

Tee ohjelma, joka lukee käyttäjältä neljä lukua ja tulostaa niiden summan ja keskiarvon

Ohjelman tulee toimia seuraavasti:

<sample-output>

Luku 1: **2**
Luku 2: **1**
Luku 3: **6**
Luku 4: **7**
Lukujen summa on 16 ja keskiarvo 4.0

</sample-output>

</in-browser-programming-exercise>



<in-browser-programming-exercise name="Ruokailukustannukset" tmcname="osa01-19_ruokailukustannukset">

Tee ohjelma, joka arvioi käyttäjän keskimääräisiä ruokailukustannuksia.

Ohjelma kysyy, kuinka monta kertaa viikossa käyttäjä käy Unicafessa ja Unicafe-lounaan hinnan sekä viikon muiden ruokaostosten hinnan.

Näiden tietojen perusteella ohjelma laskee käyttäjän keskimääräiset ruokamenot sekä viikossa että yhtenä päivänä.

Ohjelman tulee toimia seuraavasti:

<sample-output>

Montako kertaa viikossa syöt Unicafessa? **4**
Unicafe-lounaan hinta? **2.5**
Paljonko käytät viikossa ruokaostoksiin? **28.5**

Kustannukset keskimäärin:
Päivässä 5.5 euroa
Viikossa 38.5 euroa

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Opiskelijat ryhmiin" tmcname="osa01-18_opiskelijat_ryhmiin">

Tee ohjelma, joka kysyy kurssin opiskelijoiden määrän ja ryhmän koon ja ilmoittaa, montako ryhmää opiskelijoista muodostuu. Jos jako ei mene tasan, yhdessä ryhmässä voi olla vähemmän opiskelijoita, mutta kaikissa muissa on oltava haluttu määrä.

<sample-output>

Montako opiskelijaa? **8**
Mikä on ryhmän koko? **4**
Ryhmien määrä: 2

</sample-output>

<sample-output>

Montako opiskelijaa? **11**
Mikä on ryhmän koko? **3**
Ryhmien määrä: 4

</sample-output>

Vihje: tehtävän tekeminen onnistuu kokonaislukujakolaskuoperaattorilla `//`

Vihje2: jos et keksi miten tehtävä ratkeaa, älä huolestu suotta vaan tutustu [seuraavassa luvussa](/osa-1/5-ehtorakenne) esiteltävään <i>ehtorakenteeseen</i>. Ehtorakenteen avulla tehtävä on huomattavasti helpompi ratkaista.

</in-browser-programming-exercise>

Kertauskysely tämän osan asioihin liittyen:

<quiz id="3fd3df29-665e-5280-9fcf-f0e002316918"></quiz>
