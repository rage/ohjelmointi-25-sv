---
path: '/osa-7/3-aikojen-kasittely'
title: 'Tid och datum'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* kan du behandla tid och datum med Python
* kan du skapa och använda `datetime`-objekt
* kan du jämföra och räkna skillnaden mellan två datum eller tidpunkter.

</text-box>

## Objektet datetime

Pythons `datetime`-modul innehåller funktionen `now`, som returnerar ett `datetime`-objekt med det nuvarande datumet och tidpunkten. Så här ser det normalt ut när man skriver ut ett `datetime`-objekt:

```python
from datetime import datetime

aika = datetime.now()
print(aika)
```

<sample-output>

2020-10-13 12:46:49.311393

</sample-output>

Du kan också definiera objektet själv:

```python
from datetime import datetime

aika = datetime(1952, 12, 24)
print(aika)
```

<sample-output>

1952-12-24 00:00:00

</sample-output>

Tidpunkten är vid midnatt om vi inte själv definierar den.

Olika element i `datetime`-objektet kan kommas åt på följande sätt:

```python
from datetime import datetime

aika = datetime(1952, 12, 24)
print("Päivä:", aika.day)
print("Kuukausi:", aika.month)
print("Vuosi:", aika.year)
```

<sample-output>

Päivä: 24
Kuukausi: 12
Vuosi: 1952

</sample-output>

Tidpunkten under dagen kan också specificeras. Precisionen kan variera:

```python
from datetime import datetime

pv1 = datetime(2020, 6, 30, 13, 00) # 30.6.2020 klo 13.00
pv2 = datetime(2020, 6, 30, 18, 45) # 30.6.2020 klo 18.45
```

## Jämföra tider och räkna skillnaden mellan dem

De bekanta jämförelseoperatorerna fungerar också för `datetime`-objekt:

```python
from datetime import datetime

nyt = datetime.now()
juhannus = datetime(2020, 6, 20)

if nyt < juhannus:
    print("Ei ole vielä juhannus")
elif nyt == juhannus:
    print("Hyvää juhannusta!")
elif nyt > juhannus:
    print("Juhannus on mennyt")
```

<sample-output>

Juhannus on mennyt

</sample-output>

Skillnaden mellan två `datetime`-objekt kan enkelt räknas med subtraktionsoperatorn:

```python
from datetime import datetime

nyt = datetime.now()
juhannus = datetime(2020, 6, 20)

ero = juhannus - nyt
print("Juhannukseen on vielä", ero.days, "päivää")
```

<sample-output>

Juhannukseen on vielä 37 päivää

</sample-output>

Obs! Resultatet för en subtraktion med `datetime`-objekt är ett `timedelta`-objekt. Det är inte lika flexibelt som `datetime`-objektet. Du kan till exempel komma åt antalet dagar i ett `timedelta`-objekt, men inte antalet år, eftersom längden på ett år varierar. Ett `timedelta`-objekt innehåller attributen `days`, `seconds` och `microseconds`. Andra storheter kan ges som argument och de konverteras automatiskt till korrekt format.

Addition med `datetime`- och `timedelta`-objekt är också möjligt. Resultatet är ett `datetime`-objekt där det specificerade antalet dagar (eller veckor, sekunder o.s.v.) är adderade:

```python
from datetime import datetime, timedelta
juhannus = datetime(2020, 6, 20)

viikko = timedelta(days=7)
viikon_paasta = juhannus + viikko

print("Kun viikko juhannuksesta kuluu on", viikon_paasta)

pitka_aika = timedelta(weeks=32, days=15)

print("Kun juhannuksesta kuluu 32 viikkoa ja 15 päivää on", juhannus + pitka_aika)
```

<sample-output>

Kun viikko juhannuksesta kuluu on 2020-06-27 00:00:00
Kun juhannuksesta kuluu 32 viikkoa ja 15 päivää on 2021-02-14 00:00:00

</sample-output>

Vi kollar ännu hur det ser ut med högre precision:

```python
nyt = datetime.now()
keskiyo = datetime(2020, 6, 30)
erotus = keskiyo-nyt
print(f"keskiyöhön on vielä {erotus.seconds} sekuntia")
```

<sample-output>

keskiyöhön on vielä 8188 sekuntia

</sample-output>

<programming-exercise name='Kuinka vanha' tmcname='osa07-09_kuinka_vanha'>

Tee ohjelma, joka kysyy käyttäjän syntymäajan (erikseen päivä, kuukausi ja vuosi) ja tulostaa, kuinka monta päivää vanha käyttäjä oli 31.12.1999 seuraavan esimerkin mukaisesti:

<sample-output>

Päivä: **10**
Kuukausi: **9**
Vuosi: **1979**
Olit 7417 päivää vanha, kun vuosituhat vaihtui.

</sample-output>

<sample-output>

Päivä: **28**
Kuukausi: **3**
Vuosi: **2005**
Et ollut syntynyt, kun vuosituhat vaihtui.

</sample-output>

Voit olettaa, että kaikki annetut päivä-kuukausi-vuosi-yhdistelmät ovat mahdollisia (eli käyttäjä ei siis anna esim. syötettä 31.2.1999).

</programming-exercise>

<programming-exercise name='Henkilötunnus oikein?' tmcname='osa07-10_henkilotunnus_oikein'>

Tee funktio `onko_validi(hetu: str)`, joka palauttaa `True` tai `False` sen mukaan, onko annettu henkilötunnus oikea. Henkilötunnus on muotoa `ppkkvvXyyyz`, jossa `ppkkvv` kertoo syntymäajan (päivä/kuukausi/vuosi), `X` on syntymävuosisadasta riippuva välimerkki, `yyy` henkilökohtainen yksilönumero ja `z` tarkistemerkki.

Ohjelman tulee tarkastaa, että

* alkuosassa on ppkkvv-muodossa oleva päivämäärä, joka on olemassa oleva päivämäärä
* välimerkki on `+` (1800-luku), `-` (1900-luku) tai `A` (2000-luku) ja
* lopussa oleva tarkastusmerkki on oikein.

Tarkastusmerkki lasketaan jakamalla syntymäajasta ja yksilönumerosta muodostuva numerosarja 31:llä ja ottamalla tästä jakojäännös. Merkki valitaan sitten jakojäännöksen mukaisesta indeksistä merkkijonosta `0123456789ABCDEFHJKLMNPRSTUVWXY`. Esimerkiksi jos jakojäännös on 12, valitaan indeksissä 12 oleva merkki `C`.

Lisätietoa laskemisesta löydät esimerkiksi [Digi- ja väestötietoviraston sivuilta](https://dvv.fi/henkilotunnus).

**HUOM!** Pidä huolta, ettet jaa omaa henkilötunnustasi esimerkiksi testikoodin mukana, jos kysyt neuvoja tehtävään kurssin keskustelualueella tai muualla.

Oikeamuotoisia henkilötunnuksia testaamiseen ovat esimerkiksi seuraavat:

* 230827-906F
* 120488+246L
* 310823A9877

</programming-exercise>

## Formatera tid och datum

Modulen `datetime` innehåller metoden `strftime` som kan användas för att formatera hur ett datum representeras som sträng. Till exempel följande kodsnutt kommer att skriva ut det nuvarande datumet i formatet `dd.mm.åååå` och därefter datumet och tiden i ett annat format:

```python
from datetime import datetime

aika = datetime.now()
print(aika.strftime("%d.%m.%Y"))
```

<sample-output>

04.02.2020

</sample-output>

Tidsformatering använder specifika tecken för att indikera ett visst format. Här är ett antal tecken (flera finns i Pythons dokumentation):

Förkortning | Betydelse
:-----------|:---------
`%d`        | dag (01–31)
`%m`        | månad (01–12)
`%Y`        | år (fyra siffor)
`%H`        | timme (24 timmars format)
`%M`        | minut (00–59)
`%S`        | sekund (00–59)

Du kan också specificera vilket tecken som används för att skilja elementen i ett datum, så som du såg i exemplet ovan.

Formatering för `datetime` fungerar också åt det andra hållet, det vill säga om du tar emot ett datum som en sträng från en användare och vill få det i `datetime`-format. Använd då metoden `strptime`:

```python
from datetime import datetime

syote = input("Anna syntymäpäiväsi muodossa pv.kk.vvvv: ")
aika = datetime.strptime(syote, "%d.%m.%Y")

if aika < datetime(2000, 1, 1):
    print("Synnyit viime vuosituhannella")
else:
    print("Synnyit tällä vuosituhannella")
```

<sample-output>

Anna syntymäpäiväsi muodossa pv.kk.vvvv: **5.11.1986**
Synnyit viime vuosituhannella

</sample-output>

<programming-exercise name='Ruutuaika' tmcname='osa07-11_ruutuaika'>

Ohjelmassa kirjoitetaan käyttäjän määrittelemään tiedostoon "ruutuaikoja", eli käyttäjän television, tietokoneen ja mobiililaitteen ääressä tiettyinä päivinä viettämää aikaa.

Ohjelma toimii seuraavasti:

<sample-output>

Tiedosto: **kesakuun_loppu.txt**
Aloituspäivä: **24.6.2020**
Montako päivää: **5**
Anna ruutuajat kunakin päivänä minuutteina (TV tietokone mobiililaite):
Ruutuaika 24.06.2020: **60 120 0**
Ruutuaika 25.06.2020: **0 0 0**
Ruutuaika 26.06.2020: **180 0 0**
Ruutuaika 27.06.2020: **25 240 15**
Ruutuaika 28.06.2020: **45 90 5**
Tiedot tallennettu tiedostoon kesakuun_loppu.txt

</sample-output>

Kunkin päivän riville on siis annettu välilyönnillä eroteltuna kolme minuuttimäärää.

Ohjelma tallentaa tilaston ruutuajoista tiedostoon `kesakuun_loppu.txt`, joka näyttää yllä olevalla syötteellä seuraavalta:

<sample-data>

Ajanjakso: 24.06.2020-28.06.2020
Yht. minuutteja: 780
Keskim. minuutteja: 156.0
24.06.2020: 60/120/0
25.06.2020: 0/0/0
26.06.2020: 180/0/0
27.06.2020: 25/240/15
28.06.2020: 45/90/5

</sample-data>

</programming-exercise>

<quiz id="272963db-2dee-56c0-8be6-258e68a3e166"></quiz>
