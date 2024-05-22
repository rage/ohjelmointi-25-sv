---
path: '/osa-6/3-virheet'
title: 'Förbered dig på fel'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* vet du hur du kan behandla icke-valida indata
* vet du vad som menas med undantag i programmeringskontext
* känner du till de vanligaste typerna av undantag i Python
* kan du behandla undantag i dina egna program.

</text-box>

Det finns två grundläggande kategorier av fel som uppkommer i program

* fel i syntax, som förhindrar körandet av ett program
* fel som sker medan programmet körs, och stoppar programmet

Fel i den första kategorin är vanligtvis enkla att korrigera eftersom Pythontolken berättar var felet ligger när man försöker köra programmet. Vanliga syntaxfel beror på kolon som fattas på någon inledande rad eller ett citattecken som fattas i slutet av en sträng.

Fel i den andra kategorin är ibland svårare att hitta, eftersom de endast sker vid något visst ställe i programmet i vissa situationer. Programmet kanske fungerar helt bra i de flesta situationer, men så finns det någon marginell situation då programmet stannar upp på grund av ett fel. Nu ska vi se hur vi kan behandla de här felen.

## Validering av indata

Flera fel som uppkommer då ett program körs beror på indata som är i fel format på något sätt. Här är några exempel:

* obligatoriska fält som fattas eller är tomma, till exempel tomma strängar i fall där strängens längd har betydelse
* negativa värden i fall där endast positiva värden är giltiga, till exempel -15 st. av en ingrediens i ett recept
* filer som saknas eller som har skrivfel i sina namn
* värden som är för stora eller för små, till exempel då vi arbetar med datum och klockslag
* icke-giltiga index, till exempel om vi försöker komma åt index 3 i strängen "hej"
* värden av fel typ, till exempel en sträng då vi förväntar oss ett heltal.

Till all lycka kan vi som programmerare förbereda oss för de flesta felen. Vi ser på ett program som frågar efter användarens ålder och kollar att siffran är giltig (mellan noll och 150):

```python
ika = int(input("Anna ikäsi: "))
if ika >= 0 and ika <= 150:
    print("Ikä kelpaa")
else:
    print("Virheellinen ikä")
```

<sample-output>

Anna ikäsi: **25**
Ikä kelpaa

</sample-output>

<sample-output>

Anna ikäsi: **-3**
Virheellinen ikä

</sample-output>

Så länge användaren ger ett heltal verkar valideringen fungera som den ska. Men om användaren ger en sträng?

<sample-output>

Anna ikäsi: **kakskytkolme**
ValueError: invalid literal for int() with base 10: 'kakskytkolme'

</sample-output>

Funktionen `int` kan inte behandla strängen `tjugotre` som ett heltal. Programmet stoppas och ett felmeddelande skrivs ut.

## Undantag

Fel som sker när programmet redan körs kallas undantag (exception). Det är möjligt att förbereda sig för undantag, så att programmet fortsätter köra även om undantag sker.

Undantag behandlas i Python med satserna `try` och `except`. Idén är att om något inom `try`-blocket orsakar ett undantag, kommer Python söka efter ett motsvarande `except`-block och köra koden under det blocket – och så fortsätter programmet att köra som normalt.

Låt oss ändra på exemplet ovan så att programmet är förberett för undantag av typen `ValueError`:

```python
try:
    ika = int(input("Anna ikäsi: "))
except ValueError:
    ika = -1

if ika >= 0 and ika <= 150:
    print("Ikä kelpaa")
else:
    print("Virheellinen ikä")
```

<sample-output>

Anna ikäsi: **kakskytkolme**
Virheellinen ikä

</sample-output>

Vi kan använda `try`-blocket för att markera att koden inom blocket möjligtvis kan orsaka ett fel. I `except`-satsen som direkt följer blocket nämns det felet vi kan förvänta oss. I exemplet ovan nämnde vi bara `ValueError`-undantaget. Om något annat fel skulle ha uppstått, skulle programmet ändå ha avslutats oavsett `try`- och `except`-blocken.

I exemplet ovan, om ett fel sker, tilldelas `alder` värdet `-1`. Det här är ett icke-giltigt värde som programmet redan sedan tidigare kan reagera på, eftersom programmet förväntar sig ett värde mellan noll och 150.

I det följande exemplet har vi funktionen `las_heltal` som ber användaren att ge ett heltal. Funktionen är också redo för icke-giltiga värden och fortsätter att fråga efter ett heltal tills ett giltigt värde har angetts.

```python
def lue_kokonaisluku():
    while True:
        try:
            syote = input("Syötä kokonaisluku: ")
            return int(syote)
        except ValueError:
            print("Virheellinen syöte")

luku = lue_kokonaisluku()
print("Kiitos!")
print(luku, "potenssiin kolme on", luku**3)
```

<sample-output>

Syötä kokonaisluku: **kolme**
Virheellinen syöte
Syötä kokonaisluku: **aybabtu**
Virheellinen syöte
Syötä kokonaisluku: **5**
Kiitos!
5 potenssiin kolme on 125

</sample-output>

Ibland räcker det med att fånga undantag med en try-except-struktur utan att göra något speciellt därtill. Vi kan alltså ignorera situationen i `except`-blocket.

Om vi ändrar på exemplet ovan så att vi endast accepterar heltal som är under 100, skulle det kunna se ut så här:

```python
def lue_pieni_kokonaisluku():
    while True:
        try:
            syote = input("Syötä kokonaisluku: ")
            luku = int(syote)
            if luku < 100:
                return luku
        except ValueError:
            pass # tämä komento ei tee mitään

        print("Virheellinen syöte")

luku = lue_pieni_kokonaisluku()
print(luku, "potenssiin kolme on", luku**3)
```

<sample-output>

Syötä kokonaisluku: **kolme**
Virheellinen syöte
Syötä kokonaisluku: **1000**
Virheellinen syöte
Syötä kokonaisluku: **5**
Kiitos!
5 potenssiin kolme on 125

</sample-output>

Nu innehåller except-blocket endast kommandot `pass`, som inte gör något. Python tillåter inte tomma block, så kommandot är nödvändigt.

<programming-exercise name='Syötteen luku' tmcname='osa06-17_syotteen_luku'>

Tee funktio `lue`, joka kysyy käyttäjältä syötettä, kunnes se on parametrien määrittelemällä välillä oleva kokonaisluku. Funktio palauttaa käyttäjän antaman syötteen.

Funktio toimii seuraavasti:

```python
luku = lue("syötä luku: ", 5, 10)
print("syötit luvun:", luku)
```

<sample-output>

syötä luku: **seitsemän**
Syötteen on oltava kokonaisluku väliltä 5...10
syötä luku: **-3**
Syötteen on oltava kokonaisluku väliltä 5...10
syötä luku: **8**
syötit luvun: 8

</sample-output>

</programming-exercise>

## Vanliga fel

Här är en samling av vanliga fel som du sannolikt kommer att stöta på. Vi kollar också i hurdana situationer dessa kan uppstå.

**ValueError**

Det här felet uppstår vanligtvis då ett argument som ges till en funktion på något sätt är ogiltigt. Till exempel anropet `float("1,23")` orsakar ett fel eftersom decimaler alltid skiljs åt med punkt i Python.

**TypeError**

Det här felet uppstår då ett värde har fel typ. Om vi till exempel anropar `len(10)` får vi ett fel, eftersom funktionen `len` kräver ett värde vars längd kan räknas – till exempel en sträng eller lista.

**IndexError**

Det här felet uppstår då vi försöker hänvisa till ett index som inte finns. Till exempel uttrycket `"abc"[5]` orsakar ett fel eftersom strängen i fråga inte har indexet 5.

**ZeroDivisionError**

Det här felet uppstår då man försöker dividera med noll. Om vi till exempel försöker ta reda på medeltalet av värden i en lista med uttrycket `sum(min_lista) / len(min_lista)` och listans längd är noll, kommer vi att få ett fel.

**Undantag när filer behandlas**

Några vanliga undantag som kan uppstå när filer behandlas är `FileNotFoundError` (filen som man försöker komma åt finns inte), `io.UnsupportedOperation` (man försöker göra något åt filen som inte tillåts i det läge filen öppnats i) och `PermissionError` (programmet har inte åtkomst till filen).

## Behandla flera undantag samtidigt

Ett `try`-block kan följas av flera `except`-block. Det här programmet kan exempelvis behandla situationer där `FileNotFoundException`- och `PermissionError`-undantagen uppkommer:

```python
try:
    with open("esimerkki.txt") as tiedosto:
        for rivi in tiedosto:
            print(rivi)
except FileNotFoundError:
    print("Tiedostoa esimerkki.txt ei löytynyt")
except PermissionError:
    print("Ei oikeutta avata tiedostoa esimerkki.txt")
```

Ibland är det inte nödvändigt att specificera det fel som programmet förbereder sig för. Speciellt då man arbetar med filer, räcker det med att veta att något fel har skett och därmed avsluta programmet på ett säkert sätt. Man behöver inte alltid veta varför ett fel har uppstått. Om vi vill vara förberedda på alla möjliga undantag kan vi använda `except`-blocket utan att specificera felet:

```python

try:
    with open("esimerkki.txt") as tiedosto:
        for rivi in tiedosto:
            print(rivi)
except:
    print("Tapahtui virhe tiedoston lukemisessa")

```

Obs! Den här `except`-satsen körs nu i alla möjliga felsituationer – det här gäller också misstag som programmeraren gjort. Endast syntaxfel kommer att orsaka fel som förhindrar programmet från att köras – detta eftersom den här typen av fel inte låter koden köras över huvud taget.

Till exempel det här programmet kommer alltid att ge ett fel, eftersom variabelnamnet `mitt_namn` har skrivits i formen mittnamn på den tredje raden:

```python
try:
    with open("esimerkki.txt") as tiedosto:
        for rivi in tiedotso:
            print(rivi)
except:
    print("Tapahtui virhe tiedoston lukemisessa.")
```

Ett `except`-block kan gömma bakomliggande fel. Problemet här berodde inte på hur filer behandlades utan på en variabel med inkorrekt namn. Utan ett `except`-block skulle vi kunna se vilket fel som orsakats och kunde därmed hitta källan till felet enklare. Därför lönar det sig att endast använda `except`-blocket för fördefinierade specifika typer av fel.

## Förmedling av undantag

Om körandet av en funktion orsakar ett undantag som inte behandlas kommer undantaget att förmedlas till koden som anropat koden och fortsätta kliva upp till huvudfunktionen. Om felet inte här heller behandlas, kommer programmet att stoppas och undantaget skrivs ut för användaren att se.

I det följande exemplet har vi funktionen `test`. Om den orsakar ett undantag, kommer det inte att behandlas inne i funktionen utan i huvudfunktionen:

```python
def testi(x):
    print(int(x) + 1)

try:
    luku = input("Anna luku: ")
    testi(luku)
except:
    print("Jotain meni pieleen")
```

<sample-output>

Anna luku: **kolme**
Jotain meni pieleen

</sample-output>

## Åstadkomma undantag

Du kan åstadkomma undantag med kommandot `raise`. Det kan verka som en konstig idé att själv åstadkomma fel i ditt program, men det kan vara nyttigt i olika situationer.

Det kan till exempel löna sig att åstadkomma ett fel när man märker icke-valida parametrar. Hittills har vi skrivit ut meddelanden när vi har validerat indata, men om vi gör en funktion som ska köras från något annat ställe så kan det hända att en utskrift inte noteras när funktionen anropas. Att åstadkomma ett fel kan göra debuggande enklare.

I det följande exempel har vi en funktion som räknar ut fakulteten av en siffra (t.ex. för siffran fem är fakulteten 1 * 2 * 3 * 4 * 5). Om argumentet som ges till funktionen är negativt, kommer ett fel att åstadkommas:

```python
def kertoma(n):
    if n < 0:
        raise ValueError("Negatiivinen syöte: " + str(n))
    k = 1
    for i in range(2, n + 1):
        k *= i
    return k

print(kertoma(3))
print(kertoma(6))
print(kertoma(-1))
```

<sample-output>

6
720
Traceback (most recent call last):
  File "testi.py", line 11, in <module>
    print(kertoma(-1))
  File "testi.py", line 3, in kertoma
    raise ValueError("Negatiivinen syöte: " + str(n))
ValueError: Negatiivinen syöte: -1

</sample-output>


<programming-exercise name='Parametrien validointi ' tmcname='osa06-18_parametrien_validointi'>

Kirjoita funktio `uusi_henkilo(nimi: str, ika: int)`, joka luo ja palauttaa uuden henkilö-tuplen. Tuplessa ensimmäinen alkio on nimi ja jälkimmäinen ikä.

Jos funktion parametrit ovat virheelliset, sen tulee tuplen palauttamisen sijasta tuottaa `ValueError`-poikkeus.

Virheellisiä parametreja tässä tapauksessa ovat:

* nimi on tyhjä merkkijono
* nimi ei koostu vähintään kahdesta sanasta
* nimen pituus on yli 40 merkkiä
* ikä on negatiivinen luku
* ikä on suurempi kuin 150

</programming-exercise>

<programming-exercise name='Virheelliset lottonumerot' tmcname='osa06-19_virheelliset_lottonumerot'>

Tiedostoon `lottonumerot.csv` on tallennettu lottonumeroita seuraavan esimerkin mukaisesti:

<sample-data>

viikko 1;5,7,11,13,23,24,30
viikko 2;9,13,14,24,34,35,37
...jne...

</sample-data>

Aluksi pitäisi olla siis otsikko `viikko x`, ja sen jälkeen seitsemän numeroa väliltä 1...39.

Tiedosto on kuitenkin osittain korruptoitunut. Seuraavat rivit ovat esimerkkejä virheellisistä riveistä (huomaa, että tehtäväpohjassa olevassa tiedostossa ei ole juuri näitä virheitä):

Viikkonumero pielessä:

<sample-data>

viikko zzc;1,5,13,22,24,25,26

</sample-data>

Numero tai numeroita pielessä:

<sample-data>

viikko 22;1,**,5,6,13,2b,34

</sample-data>

Liian vähän numeroita:

<sample-data>

viikko 13;4,6,17,19,24,33

</sample-data>

Liian pieniä tai suuria numeroita:

<sample-data>

viikko 39;5,9,15,35,39,41,105

</sample-data>

Rivissä esiintyy sama numero kahdesti:

<sample-data>

viikko 41;5,12,3,35,12,14,36

</sample-data>

Kirjoita funktio `suodata_virheelliset()`, joka luo tiedoston `korjatut_numerot.csv`. Tiedostoon on kopioitu kelvolliset rivit alkuperäisestä tiedostosta.

</programming-exercise>

<quiz id="22f95adb-d57f-5380-87c6-4857dda1e79f"></quiz>
