---
path: "/osa-1/3-lisaa-muuttujista"
title: "Mer om variabler"
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* kan du använda variabler i olika situationer
* vet du vilken typ av data som kan lagras i variabler
* känner du till skillnaderna mellan strängar, heltal och flyttal.

</text-box>

Vänligen fyll i den här enkäten före du börjar med den här delen. Du får ett poäng efter att du har fyllt i enkäten.

<quiz id="696ae8ca-e032-58a1-9f55-76f59a01b3a7"></quiz>



Variabler har olika användningsområden inom programmering. Du kan använda variabler för att lagra vilken som helst typ av information som kan behövas senare medan ett program körs.

I Python skapas variabler på följande sätt:

`muuttujan_nimi = ...`

`...` ovan syftar till värdet som sparas i variabeln.

Till exempel när du använde kommandot `input` för att läsa in en sträng från användaren, sparade du strängen i en variabel och använde variabeln senare i ditt program.

```python
nimi = input("Anna nimesi: ")
print("Moi, " + nimi)
```

<sample-output>

Anna nimesi: **Kummitus**
Moi, Kummitus

</sample-output>

Värdet som lagras i variabeln kan också definieras med hjälp av andra variabler:

```python
etunimi = "Pekka"
sukunimi = "Pythonen"

nimi = etunimi + " " + sukunimi

print(nimi)
```

<sample-output>

Pekka Pythonen

</sample-output>

Värdena som lagras i variablerna ovan kommer inte från användaren. De förblir de samma varje gång programmet körs. Det här kallas att hårdkoda data i programmet.

## Att ändra på värdet av en variabel

Som namnet möjligtvis avslöjar, kan värdet på en _variabel_ ändra. I den förra delen observerade vi att ett nytt värde ersätter det tidigare värdet.

Medan vi kör följande program, kommer variabeln `ord` att ha tre olika värden:

```python
sana = input("Anna sana: ")
print(sana)

sana = input("Anna toinen sana: ")
print(sana)

sana = "kolmas"
print(sana)
```

<sample-output>

Anna sana: **eka**
eka
Anna toinen sana: **toka**
toka
kolmas

</sample-output>

Värdet som är lagrat i variabeln ändrar varje gång vi tilldelar variabeln ett nytt värde.

Det nya värdet på en variabel kan basera sig på det föregående värdet. I följande exempel tilldelas variabeln `ord` först ett värde på basis av indata från användaren. Därefter tilldelas variabeln ett nytt värde – som består av det gamla värdet och tre utropstecken i slutet.

```python
sana = input("Anna sana: ")
print(sana)

sana = sana + "!!!"
print(sana)
```

<sample-output>

Anna sana: **testi**
testi
testi!!!

</sample-output>

<text-box variant="hint" name="Att välja ett bra namn för en variabel">

* Det är vanligtvis en bra idé att namnge variabler enligt deras funktion. Exempelvis om en variabel innehåller ett ord, så är namnet `ord` ett mycket bättre namn än `a`.
* Det finns ingen begränsning på längden av ett namn på en variabel i Python, men det finns några andra begränsningar. Variabelns namn ska börja med en bokstav och det kan endast innehålla bokstäver, siffror och understreck (\_).
* Stora och små bokstäver är olika tecken. Variablerna `namn`, `Namn` och `NAMN` är alla olika variabler. Även om den här regeln har några undantag, så kommer vi att ignorera dem tills vidare.
* Det är ett vanligt tillvägagångssätt att i Python endast använda små bokstäver i variabelnamn. Om namnet består av flera ord använder man understreck mellan orden. Även om den här regeln också har några undantag, så kommer vi att ignorera dem tills vidare.

</text-box>

## Heltal

Hittills har vi enbart lagrat strängar i variabler, men det finns också flera andra datatyper som vi kommer att vilja lagra och använda senare. Vi tar en titt på heltal för att börja med. Heltal är tal utan en decimal- eller bråkdel. Exempelvis -15, 0 och 1.

Det följande programmet skapar variabeln `alder`, som är ett heltal:

```python
ika = 24
print(ika)
```

Utskriften ser helt enkelt ut så här:

<sample-output>

24

</sample-output>

Märk att citattecknen fattas. Om vi skulle lägga till citattecken runt siffran skulle det inte längre vara ett heltal, utan en sträng. En sträng kan innehålla siffror, men strängar behandlas på ett annat sätt.

Varför ska variabler då ha en typ när programmets utskrift ändå ser ut lika, oavsett?

```python
luku1 = 100
luku2 = "100"

print(luku1)
print(luku2)
```

<sample-output>

100
100

</sample-output>

Variabeltyper har skillnad eftersom olika operationer påverkar olika typer av variabler på olika sätt. Ta en titt på följande exempel:

```python
luku1 = 100
luku2 = "100"

print(luku1 + luku1)
print(luku2 + luku2)
```

Koden skriver ut det följande:

<sample-output>

200
100100

</sample-output>

För heltal betyder operatorn `+` addition, medan den för strängar innebär kombination av två strängar.

Alla operatorer är inte tillgängliga för alla typer av variabler. Siffror kan divideras med operatorn /, men en sträng kan inte divideras. Försök av det senare orsakar ett felmeddelande:

## Att kombinera värden i samband med utskrift

Det följande kommer inte att fungera eftersom `"Resultatet är "` och `resultat` är av olika typer:

```python
tulos = 10 * 25
# seuraava rivi tuottaa virheen
print("Tulos on " + tulos)
```

Programmet skriver inte ut någonting – istället får vi ett fel:

<sample-output>

TypeError: unsupported operand type(s) for +: 'str' and 'int'

</sample-output>

I felet berättar Python att kombination av två olika typer av värden inte går så här enkelt. I den här situationen är `"Resultatet är "` av typen sträng medan värdet i variabeln `resultat` är ett heltal.

Om vi vill skriva ut en sträng och ett heltal i ett och samma kommando kan vi konvertera heltalet till en sträng med `str`-funktionen. Därefter kan de två strängarna kombineras normalt. Till exempel så här:

```python
tulos = 10 * 25
print("Tulos on " + str(tulos))
```

<sample-output>

Tulos on 250

</sample-output>

`print`-kommandot har också inbyggd funktionalitet som stödjer kombination av olika typer av värden. Det enklaste sättet är att lägga in ett komma mellan värdena. Alla värden kommer då att skrivas ut – oavsett typ:

```python
tulos = 10 * 25
print("Tulos on", tulos)
```

<sample-output>

Tulos on 250

</sample-output>

Observera att det i detta fall automatiskt läggs till ett mellanslag mellan värdena.

## Utskrift med f-strängar

Hur kan vi gå till väga om vi önskar oss mera flexibilitet och kontroll över det som skrivs ut? F-strängar är ett annat sätt som vi kan använda oss för att påverka formatet på en utskrift i Python. Syntaxen kan till att börja med verka en aning konstig, men f-strängar är ändå ofta det enklaste sättet att påverka formatet på en text.

Med f-strängar skulle det föregående exemplet se ut så här:

```python
tulos = 10 * 25
print(f"Tulos on {tulos}")
```

Låt oss se hur ovanstående exempel fungerar, del för del. Helt i början av strängen som vi håller på att skriva ut finns bokstaven f. Den här bokstaven berättar för Python att följande sträng är en f-sträng. Inom strängen finns variabelnamnet `resultat`, omringat av klammerparenteser. Värdet på variabeln kommer på det sättet att bli en del av strängen som skrivs ut. Utskriften ser helt likadan ut som i de föregående exemplen:

<sample-output>

Tulos on 250

</sample-output>

En och samma f-sträng kan innehålla flera variabler. Den här koden…

```python
nimi = "Arto"
ika = 39
kaupunki = "Espoo"
print(f"Hei {nimi}, olet {ika}-vuotias. Asuinpaikkasi on {kaupunki}.")
```

…skriver ut det följande:

<sample-output>

Hei Arto, olet 39-vuotias. Asuinpaikkasi on Espoo.

</sample-output>

Det är svårt att åstadkomma en likadan utskrift med hjälp av kommanotationen i `print`-kommandot. Exempelvis programmet…

```python
nimi = "Arto"
ika = 39
kaupunki = "Espoo"
print("Hei", nimi, ", olet", ika, "-vuotias. Asuinpaikkasi on", kaupunki, ".")
```

…skriver ut det följande:

<sample-output>

Hei Arto , olet 39 -vuotias. Asuinpaikkasi on Espoo .

</sample-output>

Observera mellanslagen som automatiskt har lagts till mellan varje kommaseparerade del i kommandot. Det är tekniskt sett möjligt att förhindra `print`-kommandot från att lägga till mellanslag, men det är inte värt det eftersom vi kan använda oss av f-strängar.

Kommanotationen kan vara till nytta ibland, men ofta orsakar den mera problem än vad den löser. F-strängar är i flera fall en pålitligare metod. I modul fyra kommer du att lära dig mera om nyttiga egenskaper som f-strängar har – de kan användas för att påverka den utskrivna textens format på flera sätt.

<in-browser-programming-exercise name="Välilyönnillä vai ilman" tmcname="osa01-10b_valilyonnilla_vai_ilman" height=400px>

Saat seuraavan koodinpätkän työnhakijoille suunnatun sovelluksen parissa työskentelevältä tuttavaltasi:

```python
nimi = "Teppo Testaaja"
ika = 20
taito1 = "python"
taso1 = "aloittelija"
taito2 = "java"
taso2 = "veteraani"
taito3 = "ohjelmointi"
taso3 = "puoliammattilainen"
ala = 2000
yla = 3000

print("nimeni on ", nimi, " , olen ", ika, "-vuotias")
print("taitoihini kuuluvat")
print("- ", taito1, " (", taso1, ")")
print("- ", taito2, " (", taso2, ")")
print("- ", taito3, " (", taso3, " )")
print("haen työtä, josta maksetaan palkkaa", ala, "-", yla, "euroa kuussa")
```

Koodin pitäisi tuottaa _täsmälleen_ seuraavanlainen tulostus:

<sample-output>

<pre>
nimeni on Teppo Testaaja, olen 20-vuotias

taitoihini kuuluvat
 - python (aloittelija)
 - java (veteraani)
 - ohjelmointi (puoliammattilainen)

haen työtä, josta maksetaan palkkaa 2000-3000 euroa kuussa
</pre>

</sample-output>

Koodi toimii melkein oikein, mutta ei kuitenkaan ihan. Tässä tehtävässä on todella tarkat testit, jotka vaativat, että tulostus on välilyönnilleen oikein.

Korjaa siis koodi siten, että tulostus näyttää oikealta. Huomaa, että erityisesti `print`-komennon muoto, jossa tulostettavat osat eritellään pilkulla, voi tuottaa yllätyksiä, sillä se lisää osien väliin välilyönnin.

Helpoiten saat muutettua koodin toimivaksi käyttämällä tulostukseen f-merkkijonoja.

Vihje: saat tulostettua tyhjän rivin komennolla `print` tai lisäämällä tulostettavaan merkkijonoon merkinnän `\n`.

Muista olla tarkkana tulostusten muodon suhteen jatkossakin kurssin tehtävissä. Osassa tehtävissä testit vaativat täsmälleen esimerkkitulostusten mukaisen muotoilun.

</in-browser-programming-exercise>

## Flyttal

Flyttal är en term som du ofta kommer att stöta på i programmering. Det hänvisar till tal med decimaltecken. Flyttal kan användas mycket lika som heltal.

Följande program räknar medeltalet av tre flyttal:

```python
luku1 = 2.5
luku2 = -1.25
luku3 = 3.62

keskiarvo = (luku1 + luku2 + luku3) / 3
print(f"Keskiarvo: {keskiarvo}")
```

<sample-output>

Keskiarvo: 1.6233333333333333

</sample-output>

<in-browser-programming-exercise name="Laskutoimitukset" tmcname="osa01-11_laskutoimitukset">

Ohjelman tehtäväpohjassa on määritelty kaksi kokonaislukumuuttujaa `x` ja `y`:

```python
x = 27
y = 15
```

Täydennä ohjelma siten, että sen tulostus on seuraava:

<sample-output>

27 + 15 = 42
27 - 15 = 12
27 * 15 = 405
27 / 15 = 1.8

</sample-output>

Ohjelman tulee toimia siinäkin tapauksessa, että muuttujien arvoa vaihdetaan. Eli jos ensimmäiset rivit muuttuvat muotoon

```python
x = 4
y = 9
```

niin tulostus on seuraava:

<sample-output>

4 + 9 = 13
4 - 9 = -5
4 * 9 = 36
4 / 9 = 0.4444444444444444

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Korjaa ohjelma: Tulostukset samalle riville" tmcname="osa01-12_korjaa_ohjelma_tulostukset_samalle_riville">

Jos `print`-komennolle annetaan lisäparametri `end = ""`, komento ei tulosta rivinvaihtoa merkkijonon jälkeen.

Esimerkiksi:

```python
print("Moi ", end="")
print("kaikki!")
```

<sample-output>

Moi kaikki!

</sample-output>

Korjaa ohjelma niin, että koko lasku tuloksineen tulostetaan yhdelle riville muuttamatta kuitenkaan `print`-komentojen määrää:

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

Kertauskysely tämän osan asioihin liittyen:

<quiz id="664b560c-e4cd-585f-beba-401fe45ee11b"></quiz>
