---
path: '/osa-6/4-paikalliset-muuttujat'
title: 'Lokala och globala variabler'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

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
def test():
    x = 5
    print(x)

test()
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
def test():
    print(x)

x = 3
test()
```

<sample-output>

3

</sample-output>

En global variabel kan inte ändras på direkt via en annan funktion. Den här funktionen har ingen påverkan på den globala variabeln:

```python
def test():
    x = 5
    print(x)

x = 3
test()
print(x)
```

<sample-output>

5
3

</sample-output>

Här skapar funktionen `test` en ny lokal variabel `x`, som "maskerar" den globala variabeln medan funktionen körs. Variabeln har värdet 5, men det är en annan variabel än den som tilldelats i huvudfunktionen.

Vad skulle den här kodsnutten då göra?

```python
def test():
    print(x)
    x = 5

x = 3
test()
print(x)
```

<sample-output>

UnboundLocalError: local variable 'x' referenced before assignment

</sample-output>

Funktionen `test` tilldelar ett värde till variabeln `x`, så Python antar att `x` är en lokal variabel istället för en global variabel med samma namn. Funktionen försöker komma åt variabeln före den skapats, vilket orsakar ett fel.

Om vi vill ändra på en global variabel inom en funktion behöver vi Pythons nyckelord `global`:

```python
def test():
    global x
    x = 3
    print(x)

x = 5
test()
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
def rakna_summa(a, b):
    global resultat
    resultat = a + b

rakna_summa(2, 3)
print(resultat)
```

Men det är bättre att göra en funktion som returnerar ett värde, så som vi har vant oss med:

```python
def rakna_summa(a, b):
    return a + b

resultat = rakna_summa(2, 3)
print(resultat)
```

Fördelen med det senare tillvägagångssättet är att funktionen är en självständig helhet. Den har specifika, fördefinierade parametrar och den returnerar ett resultat. Den har inga sidoeffekter, så den kan testas och ändras utan att man behöver bry sig om andra delar av programmet.

Globala variabler är nyttiga i situationer där vi behöver någon gemensam information på "högre nivå", och den här informationen ska vara tillgänglig för alla funktioner i programmet. Det här är ett exempel på en sådan situation:

```python
def rakna_summa(a, b):
    global raknare
    raknare += 1
    return a + b

def rakna_differens(a, b):
    global raknare
    raknare += 1
    return a - b


raknare = 0
print(rakna_summa(2, 3))
print(rakna_summa(5, 5))
print(rakna_differens(5, 2))
print(rakna_summa(1, 0))
print("Funkionerna anropades", raknare, "gånger")
```

<sample-output>
5
10
3
1
Funkionerna anropades 4 gånger

</sample-output>

I det här fallet vill vi hålla koll på hur många gånger någondera av funktionerna har anropats medan programmet körts. Den globala variabeln `raknare` är nyttig i den här situationen, eftersom vi kan öka på siffran inom funktionerna när de körs samtidigt som värdet också är tillgängligt via huvudfunktionen.

## Förmedla data från funktion till funktion – en andra titt

Om ett program består av flera funktioner, dyker ofta frågan om att förmedla data från en funktion till en annan upp.

När vi såg på den här frågan senast, hade vi ett program som frågar användaren efter några heltal, skriver dem ut och analyserar sifforna. Programmet var uppdelat i tre funktioner:

```python
def las_fran_anvandaren(antal: int):
    print(f"Ange {antal} siffror:")
    siffror = []

    i = antal
    while i>0:
        siffra = int(input("Ange siffra: "))
        siffror.append(siffra)
        i -= 1

    return siffror

def skriv_ut(siffror: list):
    print("Siffrorna är: ")
    for siffra in siffror:
        print(siffra)

def analysera(siffror: list):
    medeltal = sum(siffror) / len(siffror)
    return f"Tillsammans {len(siffror)} siffror, medelvärde {medeltal}, minsta {min(siffror)} och största {max(siffror)}"

# "huvudprogram" som använder funktionerna
indata = las_fran_anvandaren(5)
skriv_ut(indata)
analys = analysera(indata)
print(analys)
```

Exempel på hur det ser ut när programmet körs:

<sample-output>

Ange 5 siffror:
Ange siffra: **10**
Ange siffra: **34**
Ange siffra: **-32**
Ange siffra: **99**
Ange siffra: **-53**
Siffrorna är:
10
34
-32
99
-53
Tillsammans 5 siffror, medelvärde 11.6, minsta- 53 och största 99

</sample-output>

Basidén är att huvudfunktionen "lagrar" den data som behandlas av programmet. I det här fallet innebär det att sifforna som användaren anger lagras i variabeln `siffor`.

Om siffrorna behövs i någon funktion, ger vi variabeln som argument, vilket vi ser med funktionerna `skriv_ut_resultat` och `analysera`. Om funktionen ger upphov till ett resultat som behövs på ett annat ställe i programmet, returneras det – så som i funktionerna `indata_fran_anvandare` och `analysera`.

Som alltid när man programmerar, finns det flera sätt att uppnå likadan funktionalitet. Det skulle vara möjligt att använda nyckelordet `global` och låta funktionerna direkt komma åt variabeln `siffror` som tilldelats i huvudfunktionen. Det finns bra orsaker till att det här inte är en god idé. Om flera funktioner kan komma åt och möjligtvis ändra på en variabel, blir det snabbt svårt att hålla koll på programmets status och programmet blir oförutsägbart. Det här märks speciellt då antalet funktioner ökar, vilket det gör oundvikligen i större programmeringsprojekt.

Sammanfattningsvis kan man konstatera att det är bäst att använda argument och returnera värden när man arbetar med funktioner.

Du kan också ha en skild `main`-funktion. I det fallet skulle variabeln siffror inte längre vara global, utan en lokal variabel under `main`-funktionen:

```python
def las_fran_anvandaren(antal: int):
    print(f"Ange {antal} siffror:")
    siffror = []

    i = antal
    while i>0:
        siffra = int(input("Ange siffra: "))
        siffror.append(siffra)
        i -= 1

    return siffror

def skriv_ut(siffror: list):
    print("Siffrorna är: ")
    for siffra in siffror:
        print(siffra)

def analysera(siffror: list):
    medeltal = sum(siffror) / len(siffror)
    return f"Tillsammans {len(siffror)} siffror, medelvärde {medeltal}, minsta {min(siffror)} och största {max(siffror)}"

# funktion som representerar huvudprogrammet
def main():
    indata = las_fran_anvandaren(5)
    skriv_ut(indata)
    analys = analysera(indata)

    print(analys)

# start av programmet
main()
```

<quiz id="940683ab-207c-5bd8-8fb4-eb40f65a33f4"></quiz>

Vänligen svara på en kort enkät gällande materialet för den här veckan.

<quiz id="cc370bd2-a6b7-5d00-bddc-f0aa5f1c1237"></quiz>
