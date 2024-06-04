---
path: '/osa-7/3-aikojen-kasittely'
title: 'Tid och datum'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* kan du behandla tid och datum med Python
* kan du skapa och använda `datetime`-objekt
* kan du jämföra och räkna skillnaden mellan två datum eller tidpunkter.

</text-box>

## Objektet datetime

Pythons `datetime`-modul innehåller funktionen `now`, som returnerar ett `datetime`-objekt med det nuvarande datumet och tidpunkten. Så här ser det normalt ut när man skriver ut ett `datetime`-objekt:

```python
from datetime import datetime

tid = datetime.now()
print(tid)
```

<sample-output>

2020-10-13 12:46:49.311393

</sample-output>

Du kan också definiera objektet själv:

```python
from datetime import datetime

tid = datetime(1952, 12, 24)
print(tid)
```

<sample-output>

1952-12-24 00:00:00

</sample-output>

Tidpunkten är vid midnatt om vi inte själv definierar den.

Olika element i `datetime`-objektet kan kommas åt på följande sätt:

```python
from datetime import datetime

tid = datetime(1952, 12, 24)
print("Dag:", tid.day)
print("Månad:", tid.month)
print("År:", tid.year)
```

<sample-output>

Dag: 24
Månad: 12
År: 1952

</sample-output>

Tidpunkten under dagen kan också specificeras. Precisionen kan variera:

```python
from datetime import datetime

tid1 = datetime(2020, 6, 30, 13, 00) # 30/6 2020 kl 13:00
tid2 = datetime(2020, 6, 30, 18, 45) # 30/6 2020 kl 18:45
```

## Jämföra tider och räkna skillnaden mellan dem

De bekanta jämförelseoperatorerna fungerar också för `datetime`-objekt:

```python
from datetime import datetime

nu = datetime.now()
midsommar = datetime(2020, 6, 20)

if nu < midsommar:
    print("Inte än midsommar")
elif nu == midsommar:
    print("Trevlig midsommar!")
elif nu > midsommar:
    print("Midsommaren kom och gick")
```

<sample-output>

Midsommaren kom och gick

</sample-output>

Skillnaden mellan två `datetime`-objekt kan enkelt räknas med subtraktionsoperatorn:

```python
from datetime import datetime

nu = datetime.now()
midsommar = datetime(2020, 6, 20)

skillnad = midsommar - nu
print("Det är ännu", skillnad.days, "dagar till midsommar")
```

<sample-output>

Det är ännu 37 dagar till midsommar

</sample-output>

Obs! Resultatet för en subtraktion med `datetime`-objekt är ett `timedelta`-objekt. Det är inte lika flexibelt som `datetime`-objektet. Du kan till exempel komma åt antalet dagar i ett `timedelta`-objekt, men inte antalet år, eftersom längden på ett år varierar. Ett `timedelta`-objekt innehåller attributen `days`, `seconds` och `microseconds`. Andra storheter kan ges som argument och de konverteras automatiskt till korrekt format.

Addition med `datetime`- och `timedelta`-objekt är också möjligt. Resultatet är ett `datetime`-objekt där det specificerade antalet dagar (eller veckor, sekunder o.s.v.) är adderade:

```python
from datetime import datetime, timedelta
midsommar = datetime(2020, 6, 20)

vecka = timedelta(days=7)
vecka_senare = midsommar + vecka

print("En vecka efter midsommar är", vecka_senare)

lang_tid = timedelta(weeks=32, days=15)

print("32 veckor och 15 dagar efter midsommar är", midsommar + lang_tid)
```

<sample-output>

En vecka efter midsommar är 2020-06-27 00:00:00
32 veckor och 15 dagar efter midsommar är 2021-02-14 00:00:00

</sample-output>

Vi kollar ännu hur det ser ut med högre precision:

```python
nu = datetime.now()
midnatt = datetime(2020, 6, 30)
skillnad = midnatt-nu
print(f"Det är ännu {skillnad.seconds} sekunder till midnatt")
```

<sample-output>

Det är ännu 8188 sekunder till midnatt

</sample-output>

<programming-exercise name='Kuinka vanha' tmcname='osa07-09_kuinka_vanha'>

Skapa ett program som frågar om användarens födelsetid och skriver därefter ut hur gammal hon var 31/12 1999.

Exempel:

<sample-output>

Dag: **10**
Månad: **9**
År: **1979**
Du var 7417 dagar gammal vid millennieskiftet.

</sample-output>

<sample-output>

Dag: **28**
Månad: **3**
År: **2005**
Du var inte född vid millennieskiftet.

</sample-output>

Du kan anta att användaren ger ett korrekt datum (inte t.ex. 31/2 1999).

</programming-exercise>

<programming-exercise name='Henkilötunnus oikein?' tmcname='osa07-10_henkilotunnus_oikein'>

Skapa funktionen `valid(personbeteckning: str)` som returnerar `True` eller `False` beroende på om den givna personbeteckningen är korrekt. Formatet på beteckningen är `ddmmååxyyyz` där `ddmmåå` indikerar födelsetid, `x` är ett skiljetecken, `yyy` födelsenummer och `z` ett kontrolltecken.

Programmet ska kontrollera att

* födelsetiden är ett datum som finns
* skiljetecknet är `+` (1800-talet), `-` (1900-talet) eller `A` (2000-talet)
* kontrolltecknet är korrekt.

Kontrolltecknet får man genom att dividera den siffra som består av födelsetiden och -numret med 31. Resten av denna operationen indikerar från vilket index i strängen `0123456789ABCDEFHJKLMNPRSTUVWXY` kontrolltecknet tas ifrån. Om resten är t.ex. 12, är kontrolltecknet vid index 12, dvs. `C`.

Se mer på webbplatsen för Myndigheten för digitalisering och befolkningsdata.

Obs! Se till att du inte delar din egen personbeteckning av misstag, t.ex. om du frågar om hjälp när du löser den här uppgiften.

För att underlätta testandet listas några valida personbeteckningar nedan:

* 230827-906F
* 120488+246L
* 310823A9877

</programming-exercise>

## Formatera tid och datum

Modulen `datetime` innehåller metoden `strftime` som kan användas för att formatera hur ett datum representeras som sträng. Till exempel följande kodsnutt kommer att skriva ut det nuvarande datumet i formatet `dd.mm.åååå` och därefter datumet och tiden i ett annat format:

```python
from datetime import datetime

tid = datetime.now()
print(tid.strftime("%d.%m.%Y"))
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

syote = input("Ange din födelsetid i formatet dd.mm.åååå: ")
tid = datetime.strptime(syote, "%d.%m.%Y")

if tid < datetime(2000, 1, 1):
    print("Du föddes på förra årtusendet")
else:
    print("Du föddes på det här årtusendet")
```

<sample-output>

Ange din födelsetid i formatet dd.mm.åååå: **5.11.1986**
Du föddes på förra årtusendet

</sample-output>

<programming-exercise name='Ruutuaika' tmcname='osa07-11_ruutuaika'>

I det här programmet antecknar vi användarens dagliga skärmtid (tv, dator, mobil) i en fil.

Så här ska programmet fungera:

<sample-output>

Fil: **juni.txt**
Första dagen: **24.6.2020**
Antal dagar: **5**
Ange skärmtiden i minuter (tv dator mobil):
Skärmtid 24.06.2020: **60 120 0**
Skärmtid 25.06.2020: **0 0 0**
Skärmtid 26.06.2020: **180 0 0**
Skärmtid 27.06.2020: **25 240 15**
Skärmtid 28.06.2020: **45 90 5**
Infon lagrad i filen juni.txt

</sample-output>

För varje dag anger man alltså tre minutvärden skilda med mellanslag.

Programmet lagrar statistik i filen `juni.txt` som i vårt fall ser ut så här:

<sample-data>

Tidsperiod: 24.06.2020-28.06.2020
Minuter tillsammans: 780
Minuter i genomsnitt: 156.0
24.06.2020: 60/120/0
25.06.2020: 0/0/0
26.06.2020: 180/0/0
27.06.2020: 25/240/15
28.06.2020: 45/90/5

</sample-data>

</programming-exercise>

<quiz id="272963db-2dee-56c0-8be6-258e68a3e166"></quiz>
