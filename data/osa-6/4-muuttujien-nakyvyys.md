---
path: '/osa-6/4-paikalliset-muuttujat'
title: 'Lokala och globala variabler'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* vet du vad en lokal variabel är
* känner du till hur definitionsområdet för en variabel påverkar dess användning
* vet du vad nyckelordet global betyder i Python
* kan du använda lokala och globala variabler korrekt.

</text-box>

Definitionsområdet för en variabel hänvisar till de områden i ett program där en specifik variabel är tillgänglig. En lokal variabel är endast tillgänglig på vissa ställen i ett program medan en global variabel kan användas överallt i programmet.

## Lokala variabler

Variabler som tilldelas i Python är lokala variabler. De är endast tillgängliga i den funktion där de tilldelats. Det här gäller både funktionsparametrar och andra variabler som tilldelats inom funktionsdefinitionen. En variabel som är lokal existerar inte utanför funktionen.

I det följande exemplet försöker vi komma åt variabeln `x` i huvudfunktionen, men det orsakar ett fel:

```python
def testi():
    x = 5
    print(x)

testi()
print(x)
```

<sample-output>

5
NameError: name 'x' is not defined

</sample-output>

Variabeln `x` existerar endast då funktionen `test` körs. Andra funktioner – också huvudfunktionen – kan inte komma åt variabeln.

## Globala variabler

Variabler som tilldelas i huvudfunktionen är globala variabler. Vi har tidigare definierat att huvudfunktionen är de delar av koden i Python som inte tillhör någon annan funktion. Ett värde som lagrats i en global variabel kan användas i vilken som helst funktion i programmet. Därmed fungerar den här koden utan problem:

```python
def testi():
    print(x)

x = 3
testi()
```

<sample-output>

3

</sample-output>

En global variabel kan inte ändras på direkt via en annan funktion. Den här funktionen har ingen påverkan på den globala variabeln:

```python
def testi():
    x = 5
    print(x)

x = 3
testi()
print(x)
```

<sample-output>

5
3

</sample-output>

Här skapar funktionen `test` en ny lokal variabel `x`, som ”maskerar” den globala variabeln medan funktionen körs. Variabeln har värdet 5, men det är en annan variabel än den som tilldelats i huvudfunktionen.

Vad skulle den här kodsnutten då göra?

```python
def testi():
    print(x)
    x = 5

x = 3
testi()
print(x)
```

<sample-output>

UnboundLocalError: local variable 'x' referenced before assignment

</sample-output>

Funktionen `test` tilldelar ett värde till variabeln `x`, så Python antar att `x` är en lokal variabel istället för en global variabel med samma namn. Funktionen försöker komma åt variabeln före den skapats, vilket orsakar ett fel.

Om vi vill ändra på en global variabel inom en funktion behöver vi Pythons nyckelord `global`:

```python
def testi():
    global x
    x = 3
    print(x)

x = 5
testi()
print(x)
```

<sample-output>

3
3

</sample-output>

Nu påverkar tilldelningen `x = 3` inom funktionen också i huvudfunktionen. Alla delar av programmet använder den samma globala variabeln `x`.

## När borde man använda globala variabler?

Globala variabler är inte ett sätt att undvika parametrar eller return-värden hos funktioner. De ska inte användas för det ändamålet. Det är dock möjligt att skriva en funktion som lagrar sina resultat direkt i en global variabel:

```python
def laske_summa(a, b):
    global tulos
    tulos = a + b

laske_summa(2, 3)
print(tulos)
```

Men det är bättre att göra en funktion som returnerar ett värde, så som vi har vant oss med:

```python
def laske_summa(a, b):
    return a + b

tulos = laske_summa(2, 3)
print(tulos)
```

Fördelen med det senare tillvägagångssättet är att funktionen är en självständig helhet. Den har specifika, fördefinierade parametrar och den returnerar ett resultat. Den har inga sidoeffekter, så den kan testas och ändras utan att man behöver bry sig om andra delar av programmet.

Globala variabler är nyttiga i situationer där vi behöver någon gemensam information på ”högre nivå”, och den här informationen ska vara tillgänglig för alla funktioner i programmet. Det här är ett exempel på en sådan situation:

```python
def laske_summa(a, b):
    global laskuri
    laskuri += 1
    return a + b

def laske_erotus(a, b):
    global laskuri
    laskuri += 1
    return a - b


laskuri = 0
print(laske_summa(2, 3))
print(laske_summa(5, 5))
print(laske_erotus(5, 2))
print(laske_summa(1, 0))
print("Funktioita kutsuttiin", laskuri, "kertaa")
```

<sample-output>
5
10
3
1
Funktioita kutsuttiin 4 kertaa

</sample-output>

I det här fallet vill vi hålla koll på hur många gånger någondera av funktionerna har anropats medan programmet körts. Den globala variabeln `antal` är nyttig i den här situationen, eftersom vi kan öka på siffran inom funktionerna när de körs samtidigt som värdet också är tillgängligt via huvudfunktionen.

## Förmedla data från funktion till funktion – en andra titt

Om ett program består av flera funktioner, dyker ofta frågan om att förmedla data från en funktion till en annan upp.

När vi såg på den här frågan senast, hade vi ett program som frågar användaren efter några heltal, skriver dem ut och analyserar sifforna. Programmet var uppdelat i tre funktioner:

```python
def lue_kayttajalta(maara: int):
    print(f"syötä {maara} lukua:")
    luvut = []

    i = maara
    while i>0:
        luku = int(input("anna luku: "))
        luvut.append(luku)
        i -= 1

    return luvut

def tulosta(luvut: list):
    print("luvut ovat: ")
    for luku in luvut:
        print(luku)

def analysoi(luvut: list):
    ka = sum(luvut) / len(luvut)
    return f"lukuja yhteensä {len(luvut)}, keskikarvo {ka}, pienin {min(luvut)} ja suurin {max(luvut)}"

# funktioita käyttävä  "pääohjelma"
syotteet = lue_kayttajalta(5)
tulosta(syotteet)
analyysin_tulos = analysoi(syotteet)
print(analyysin_tulos)
```

Exempel på hur det ser ut när programmet körs:

<sample-output>

syötä 5 lukua:
anna luku: **10**
anna luku: **34**
anna luku: **-32**
anna luku: **99**
anna luku: **-53**
luvut ovat:
10
34
-32
99
-53
lukuja yhteensä 5, keskikarvo 11.6, pienin- 53 ja suurin 99

</sample-output>

Basidén är att huvudfunktionen ”lagrar” den data som behandlas av programmet. I det här fallet innebär det att sifforna som användaren anger lagras i variabeln `siffor`.

Om siffrorna behövs i någon funktion, ger vi variabeln som argument, vilket vi ser med funktionerna `skriv_ut_resultat` och `analysera`. Om funktionen ger upphov till ett resultat som behövs på ett annat ställe i programmet, returneras det – så som i funktionerna `indata_fran_anvandare` och `analysera`.

Som alltid när man programmerar, finns det flera sätt att uppnå likadan funktionalitet. Det skulle vara möjligt att använda nyckelordet `global` och låta funktionerna direkt komma åt variabeln `siffror` som tilldelats i huvudfunktionen. Det finns bra orsaker till att det här inte är en god idé. Om flera funktioner kan komma åt och möjligtvis ändra på en variabel, blir det snabbt svårt att hålla koll på programmets status och programmet blir oförutsägbart. Det här märks speciellt då antalet funktioner ökar, vilket det gör oundvikligen i större programmeringsprojekt.

Sammanfattningsvis kan man konstatera att det är bäst att använda argument och returnera värden när man arbetar med funktioner.

Du kan också ha en skild `main`-funktion. I det fallet skulle variabeln siffror inte längre vara global, utan en lokal variabel under `main`-funktionen:

```python
def lue_kayttajalta(maara: int):
    print(f"syötä {maara} lukua:")
    luvut = []

    i = maara
    while i>0:
        luku = int(input("anna luku: "))
        luvut.append(luku)
        i -= 1

    return luvut

def tulosta(luvut: list):
    print("luvut ovat: ")
    for luku in luvut:
        print(luku)

def analysoi(luvut: list):
    ka = sum(luvut) / len(luvut)
    return f"lukuja yhteensä {len(luvut)} keskikarvo {ka} pienin{min(luvut)} ja suurin {max(luvut)}"

# pääohjelmaa edustava funktio
def main():
    syotteet = lue_kayttajalta(5)
    tulosta(syotteet)
    analyysin_tulos = analysoi(syotteet)

    print(analyysin_tulos)

# ohjelman käynnistys
main()
```

<quiz id="940683ab-207c-5bd8-8fb4-eb40f65a33f4"></quiz>

Vänligen svara på en kort enkät gällande materialet för den här veckan.

<quiz id="cc370bd2-a6b7-5d00-bddc-f0aa5f1c1237"></quiz>
