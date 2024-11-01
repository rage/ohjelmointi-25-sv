---
path: '/osa-8/4-metoder-i-egna-klasser'
title: 'Metoder i egna klasser'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen:

- Vet du hur klassmetoder fungerar
- Kan du skriva nya metoder i dina egna klasser
- Kommer du att förstå begreppen inkapsling och klient inom objektorienterad programmering

</text-box>

Klasser som endast innehåller dataattribut skiljer sig inte så mycket från ordlistor. Nedan kan du se två sätt att modellera ett bankkonto, först med en klassdefinition och sedan med hjälp av en ordlista.

```python
# Exempel 1: bankkonto med klassdefinition
class Bankkonto:

    def __init__(self, kontonummer: str, agare: str, saldo: float, arsranta: float):
        self.kontonummer = kontonummer
        self.agare = agare
        self.saldo = saldo
        self.arsranta = arsranta

peters_konto = Bankkonto("12345-678", "Peter Python", 1500.0, 0.015)
```

```python
# Exempel2: bankkonto med ordlista
peters_konto = {"kontonummer": "12345-678", "agare": "Peter Python", "saldo": 1500.0, "arsranta": 0.0}
```

Med en ordlista är implementeringen mycket kortare och enklare. Med en klass är strukturen däremot mer "hårt bunden", så vi kan förvänta oss att alla `Bankkonto`-objekt är strukturellt lika. Dessutom är en klass också namngiven. Klassen `Bankkonto` refereras till när ett nytt bankkonto skapas, och objektets typ är `Bankkonto`, inte dict.

En annan stor fördel med klasser är att de förutom data även kan innehålla funktionalitet. En av de vägledande principerna för objektorienterad programmering är att ett objekt används för att komma åt både den data som är kopplad till ett objekt och funktionaliteten för att bearbeta denna data.

## Metoder i klasser

En metod är ett underprogram eller en funktion som är knuten till en specifik klass. Vanligtvis påverkar en metod bara ett enda objekt. En metod definieras inom klassdefinitionen och den kan komma åt klassens dataattribut precis som vilken annan variabel som helst.

Låt oss fortsätta med klassen `Bankkonto` som introducerades ovan. Nedan har vi en ny metod som lägger till ränta på kontot:

```python
class Bankkonto:

    def __init__(self, kontonummer: str, agare: str, saldo: float, arsranta: float):
        self.kontonummer = kontonummer
        self.agare = agare
        self.saldo = saldo
        self.arsranta = arsranta

    # Metoden lägger till den årliga räntat till saldot
    def lagg_till_ranta(self):
        self.saldo += self.saldo * self.arsranta


peters_konto = Bankkonto("12345-678", "Peter Python", 1500.0, 0.015)
peters_konto.lagg_till_ranta()
print(peters_konto.saldo)
```

<sample-output>

1522.5

</sample-output>

Metoden `lagg_till_ranta` multiplicerar saldot på kontot med den årliga ränteprocenten och lägger sedan till resultatet till det aktuella saldot. Metoden verkar bara på det objekt som den anropas på.

Låt oss se hur detta fungerar när vi har skapat flera instanser av klassen:

```python
# Klassen Bankkonto är definierat såsom i förra exemplet

peters_konto = Bankkonto("12345-678", "Peter Python", 1500.0, 0.015)
pernillas_konto = Bankkonto("99999-999", "Pernilla Pythonson", 1500.0, 0.05)
pers_konto = Bankkonto("1111-222", "Per Persson", 1500.0, 0.001)

# Vi tillsätter ränta till Peters och Pernillas konton, men inte Pers
peters_konto.lagg_till_ranta()
pernillas_konto.lagg_till_ranta()

# Vi skriver ut alla
print(peters_konto.saldo)
print(pernillas_konto.saldo)
print(pers_konto.saldo)
```

<sample-output>

1522.5
1575.0
1500.0

</sample-output>

Som du kan se ovan läggs den årliga räntan endast till på de konton som metoden anropas på. Eftersom den årliga räntan är olika för Peters och Paulas konton, blir resultatet olika för dessa två konton. Saldot på Pernillas konto ändras inte, eftersom metoden `lagg_till_ranta` inte anropas på objektet `pernillas_konto`.

## Inkapsling

Inom objektorienterad programmering dyker ordet klient upp då och då. Det används för att hänvisa till ett kodavsnitt som skapar ett objekt och använder dem med hjälp av de metoder som motsvarande klass ger möjlighet till. När data som finns i ett objekt endast används genom de metoder som definierats i klassen, garanteras objektets interna integritet. I praktiken innebär detta att t.ex. en `Bankkonto`-klass erbjuder metoder för att hantera `saldo`-attributet, så att saldot aldrig nås direkt av klienten. Dessa metoder kan sedan verifiera att saldot till exempel inte tillåts gå under noll.

Ett exempel på hur detta skulle fungera:

```python
class Bankkonto:

    def __init__(self, kontonummer: str, agare: str, saldo: float, arsranta: float):
        self.kontonummer = kontonummer
        self.agare = agare
        self.saldo = saldo
        self.arsranta = arsranta

    # Metoden tillsätter den årliga räntat till saldot av kontot
    def tillsatt_ranta(self):
        self.saldo += self.saldo * self.arsranta

    # Den här metoden "tar ut" pengar från kontot
    # Metoden returnerar True ifall det lyckades, och False ifall det misslyckades
    def uttag(self, uttagssumma: float):
        if uttagssumma <= self.saldo:
            self.saldo -= uttagssumma
            return True

        return False

peters_konto = Bankkonto("12345-678", "Peter Python", 1500.0, 0.015)

if peters_konto.uttag(1000):
    print("Uttaget lyckades, kontots saldo är nu", peters_konto.saldo)
else:
    print("Uttaget lyckades inte, saldot var otillräckligt")

# Vi försöker på nytt
if peters_konto.uttag(1000):
    print("Uttaget lyckades, kontots saldo är nu", peters_konto.saldo)
else:
    print("Uttaget lyckades inte, saldot var otillräckligt")
```

<sample-output>

Uttaget lyckades, kontots saldo är nu 500.0
Uttaget lyckades inte, saldot var otillräckligt

</sample-output>

Att bibehålla objektets interna integritet och erbjuda lämpliga metoder för att säkerställa detta kallas inkapsling. Tanken är att objektets inre arbete är dolt för klienten, men objektet erbjuder metoder som kan användas för att komma åt den data som lagras i objektet.

Att lägga till en metod innebär inte att attributet automatiskt döljs. Även om klassdefinitionen `Bankkonto` innehåller metoden `uttag` för att ta ut pengar, kan klientkoden fortfarande komma åt och ändra attributet `saldo` direkt:

```python
peters_konto = Bankkonto("12345-678", "Peter Python", 1500.0, 0.015)

# Vi försöker lyfta 2000
if peters_konto.uttag(2000):
    print("Uttaget lyckades, kontots saldo är nu", peters_konto.saldo)
else:
    print("Uttaget lyckades inte, saldot var otillräckligt")

    # Vi "tvingar" ett uttag på 2000
    peters_konto.saldo -= 2000

print("Saldot är nu:", peters_konto.saldo)
```

Det är möjligt att dölja dataattributen från klientkoden, vilket kan bidra till att lösa detta problem. Vi återkommer till detta ämne i nästa del.

<programming-exercise name='Minskande räknare' tmcname='osa08-10_minskande_raknare'>

Denna övning har flera delar. Varje del är värt ett poäng och kan lämnas in separat.

Övningsmallen innehåller en delvis ifylld klass `MinskandeRaknare`:

```python
class MinskandeRaknare:
    def __init__(self, borjan_varde: int):
        self.varde = borjan_varde

    def skriv_ut_varde(self):
        print("värde:", self.varde)

    def minska(self):
        pass

    # resten av metoderna här
```

Klassen används på följande sätt:

```python
raknare = MinskandeRaknare(10)
raknare.skriv_ut_varde()
raknare.minska()
raknare.skriv_ut_varde()
raknare.minska()
raknare.skriv_ut_varde()
```

<sample-output>

värde: 10
värde: 9
värde: 8

</sample-output>


### Minska räknarens värde

Komplettera metoden `minska` som definieras i mallen, så att den minskar värdet som lagras i räknaren med ett. Se exemplet ovan för förväntat beteende.

### Räknaren får inte ha ett negativt värde

Lägg till funktionalitet till din `minska`-metod, så att räknarens värde aldrig når negativa värden. Om värdet på räknaren är 0 kommer den inte att minskas ytterligare.

```python
raknare = MinskandeRaknare(2)
raknare.skriv_ut_varde()
raknare.minska()
raknare.skriv_ut_varde()
raknare.minska()
raknare.skriv_ut_varde()
raknare.minska()
raknare.skriv_ut_varde()
```

<sample-output>

värde: 2
värde: 1
värde: 0
värde: 0

</sample-output>

### Nollande av räknaren

Skapa en metod `nolla` som sätter värdet på räknaren till 0:

```python
raknare = MinskandeRaknare(100)
raknare.skriv_ut_varde()
raknare.nolla()
raknare.skriv_ut_varde()
```

<sample-output>

värde: 100
värde: 0

</sample-output>

### Återställning av räknaren

Skapa en metod `aterstall_ursprungligt_varde()`, som återställer räknaren till sitt ursprungliga tillstånd:

```python
raknare = MinskandeRaknare(55)
raknare.minska()
raknare.minska()
raknare.minska()
raknare.minska()
raknare.skriv_ut_varde()
raknare.aterstall_ursprungligt_varde()
raknare.skriv_ut_varde()
```

<sample-output>

värde: 51
värde: 55

</sample-output>

</programming-exercise>

Som avslutning på detta avsnitt tittar vi på en klass som modellerar en spelares personliga bästa. Klassdefinitionen innehåller separata valideringsmetoder som kontrollerar att de argument som skickas är giltiga. Metoderna anropas redan i konstruktorn. Detta säkerställer att det skapade objektet är sunt internt.

```python
from datetime import date

class PersonligtRekord:

    def __init__(self, spelare: str, dag: int, manad: int, ar: int, poang: int):
        # Standardvärden
        self.spelare = ""
        self.datum = date(1900, 1, 1)
        self.poang = 0

        if self.namn_ok(spelare):
            self.spelare = spelare

        if self.dtm_ok(dag, manad, ar):
            self.datum = date(ar, manad, dag)

        if self.poang_ok(poang):
            self.poang = poang

    # Hjälparmetoder som kollar att argumenten är giltiga
    def namn_ok(self, namn: str):
        return len(namn) >= 2 # Namnet ska vara minst två tecken

    def dtm_ok(self, dag, manad, ar):
        try:
            date(ar, manad, dag)
            return True
        except:
            # Ett undantag ifall datumet inte är giltigt
            return False

    def poang_ok(self, poang):
        return poang >= 0

if __name__ == "__main__":
    resultat1 = PersonligtRekord("Peter", 1, 11, 2020, 235)
    print(resultat1.poang)
    print(resultat1.spelare)
    print(resultat1.datum)

    # Datumet är inte giltigt
    resultat2 = PersonligtRekord("Pernilla", 4, 13, 2019, 4555)
    print(resultat2.poang)
    print(resultat2.spelare)
    print(resultat2.datum) # Skriver ut standardvärdet 1900-01-01
```

<sample-output>

235
Peter
2020-11-01
4555
Pernilla
1900-01-01

</sample-output>

I exemplet ovan anropades även hjälpmetoderna via parameternamnet `self` när de användes i konstruktorn. Det är också möjligt att inkludera /statiska/ metoddefinitioner i klassdefinitioner. Dessa är metoder som kan anropas utan att det någonsin skapas en instans av klassen. Vi återkommer till detta i nästa del.

Parameternamnet `self` används endast när man hänvisar till /objektets egenskaper som en instans av klassen/. Det gäller både dataattributen och de metoder som är knutna till ett objekt. För att göra terminologin mer förvirrande kallas dataattributen och metoderna tillsammans ibland helt enkelt för objektets attribut, vilket är anledningen till att vi i detta material ofta har angett dataattribut när vi menar de variabler som definieras inom klassen. Det är här terminologin hos vissa Python-programmerare skiljer sig något från den terminologi som mer allmänt används inom objektorienterad programmering, där attribut vanligtvis bara hänvisar till dataattributen hos ett objekt.

Det är också möjligt att skapa lokala variabler inom metoddefinitioner utan att hänvisa till `self`. Detta bör du göra om det inte finns något behov av att komma åt variablerna utanför metoden. Lokala variabler inom metoder har inga speciella nyckelord; de används precis som alla vanliga variabler som du har stött på hittills. .

Så här skulle det till exempel fungera:

```python
class Bonuskort:
    def __init__(self, namn: str, saldo: float):
        self.namn = namn
        self.saldo = saldo

    def tillsatt_bonus(self):
        # Nu är variabeln bonus en lokal variabel, inte ett
        # data attribut till objektet
        # Den kan inte nås genom ett objekt
        bonus = self.saldo * 0.25
        self.saldo += bonus

    def tillsatt_superbonus(self):
        # Variabeln superbonus är också en lokal variabel.
        # Vanligtvis är hjälpvariabler lokala variabler eftersom
        # det inte finns något behov av att komma åt dem från andra
        # metoder i klassen eller direkt via ett objekt.
        superbonus = self.saldo * 0.5
        self.saldo += superbonus

    def __str__(self):
        return f"Bonuskort(namn={self.namn}, saldo={self.saldo})"
```

<programming-exercise name="För- och efternamn" tmcname='osa08-10b_for_och_efternamn'>

Skapa en klass `Person`, som får _endast ett attribut_ `namn`, som ges till konstruktorn.

Skapa dessutom två metoder:

Metoden `ge_fornamn` returnerar personens förnamn och metoden `ge_efternamn` på samma sätt personens efternamn.

Du kan anta att det namn som skickas till konstruktorn kommer att innehålla endast för- och efternamn åtskilda med ett mellanslag.

Exempel på användning:

```python
if __name__ == "__main__":
    peter = Person("Peter Python")
    print(peter.ge_fornamn())
    print(peter.ge_efternamn())

    pauli = Person("Pernilla Pythonson")
    print(pernilla.ge_fornamn())
    print(pernilla.ge_efternamn())
```

<sample-output>

Peter
Python
Pernilla
Pythonson

</sample-output>


</programming-exercise>

<programming-exercise name='Nummerstatistik' tmcname='osa08-11_nummerstatistik'>

I den här övningen ska du skapa ett program för att arbeta med siffror, på samma sätt som i [slutet av modul 2](https://rage.github.io/ohjelmointi-24-sv/osa-8/4-metoder-i-egna-klasser) i kursen Introduktion till Programmering. Den här gången ska du definiera en klass för ändamålet.

### Mängden nummer

Skapa en klass med namnet `Nummerstatistik`, med följande metoder:

- metoden `tillsatt_nummer` lägger till ett nytt nummer till statistiken
- metoden `mangden_nummer` returnerar mängden nummer som har tillsatts

I det här skedet finns det inget behov av att lagra själva siffrorna i någon datastruktur. Det räcker att bara komma ihåg hur många som har lagts till. Metoden `tillsatt_nummer` tar emot ett argument, men det finns inget behov av att bearbeta det faktiska värdet på något sätt ännu.

Funktionen borde ha följande struktur:

```python
class  NummerStatistik:
    def __init__(self):
        self.nummer = 0

    def tillsatt_nummer(self, nummer:int):
        pass

    def mangden_nummer(self):
        pass
```

```python
statistik = NummerStatistik()
statistik.tillsatt_nummer(3)
statistik.tillsatt_nummer(5)
statistik.tillsatt_nummer(1)
statistik.tillsatt_nummer(2)
print("Mängden nummer:", statistik.mangden_nummer())
```

<sample-output>

Mängden nummer: 4

</sample-output>

### Summa och medeltal

Tillsätt följande metoder till klassdefinitionen:

- metoden `summa` returnerar summan av talen som satts till (en tom statistik returnerar 0)
- metoden `medeltat` returnerar medeltalet av numren (en tom statistiks medeltal är 0)

```python
statistik = NummerStatistik()
statistik.tillsatt_nummer(3)
statistik.tillsatt_nummer(5)
statistik.tillsatt_nummer(1)
statistik.tillsatt_nummer(2)
print("Mängden nummer:", statistik.mangden_nummer())
print("Summa:", statistik.summa())
print("Medeltal:", statistik.medeltal())
```

<sample-output>

Mängd: 4
Summa: 11
Medeltal: 2.75

</sample-output>

### Användarinmatning

Skriv ett huvudprogram som fortsätter att fråga användaren om heltal tills användaren skriver in -1. Programmet ska sedan skriva ut summan och medelvärdet av de inmatade talen.

Ditt program ska använda `NummerStatistik`-objekt för att hålla koll på numren som läggs till.

OBS: Du behöver inte ändra `NummerStatistik`-klassen, i denna del, använd en instans av klassen för att slutföra denna del.

OBS2: Ditt huvudprogram ska inte vara inuti ett `if __name__ == "__main__"`-block, annars fungerar inte testen.

<sample-output>

Ange nummer:
**4**
**2**
**5**
**2**
**-1**
Summa: 13
Medeltal: 3.25

</sample-output>

### Flera summor

Bygg på ditt huvudprogram så att det också separat räknar summan av de jämna och udda tal som läggs till.

OBS: Ändra inte din `NummerStatistik`-klassdefinition i denna del av övningen heller. Definiera i stället tre `NummerStatistik`-objekt. Ett av dem ska hålla reda på alla siffror, ett annat ska hålla reda på de jämna siffrorna och det tredje ska hålla reda på de udda siffror som skrivs in.

OBS2: Ditt huvudprogram ska inte vara inuti ett `if __name__ == "__main__"`-block, annars fungerar inte testen.

Programmet ska fungera så här:

<sample-output>

Ange nummer:
**4**
**2**
**5**
**2**
**-1**
Summa: 13
Medeltal: 3.25
Jämna talens summa: 8
Udda talens summa: 5

</sample-output>



</programming-exercise>
