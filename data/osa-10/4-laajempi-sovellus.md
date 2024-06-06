---
path: '/osa-10/4-lisaa-esimerkkeja'
title: 'Att utveckla en större applikation '
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Känner du till några grundläggande principer för applikationsutveckling
- Kommer du att känna dig bekväm med att skilja mellan de olika delarna av en applikation (användargränssnitt, programlogik och filhantering)
- Har du övat på att skriva din egna lite större applikation

</text-box>

Hittills i detta kursmaterial har vi gått igenom ett stort antal Python-funktioner.

I Introduktion till programmering-kursen introducerades kontrollstrukturer som while och for, funktioner samt grundläggande datastrukturer som listor, tupler och ordlistor. I princip är dessa verktyg allt som behövs för att uttrycka vad som helst som en programmerare kan tänka sig vilja uttrycka med Python.

På denna avancerade kurs i programmering, med början i del 8 av materialet, har du blivit bekant med klasser och objekt. Låt oss ta en stund att fundera på när och varför de är nödvändiga, ifall de grundläggande verktygen från del 1 till 7 borde räcka.

## Att hantera komplexitet

Objekt och klasser är långt ifrån nödvändiga i alla programmeringssammanhang. Om du t.ex. programmerar ett litet skript för engångsbruk är objekt oftast överflödiga. Men när du ska programmera något större och mer komplicerat blir objekten mycket användbara.

När programmen blir allt mer komplexa blir mängden detaljer snabbt ohanterlig, såvida inte programmet är organiserat på något systematiskt sätt. Även några av de mer komplicerade övningarna på den här kursen hittills skulle ha haft nytta av de exempel som ges i den här delen av materialet.

I flera decennier har begreppet [Separation of concerns](https://en.wikipedia.org/wiki/Separation_of_concerns) varit en av de centrala principerna inom programmering och inom datavetenskapen i stort. Citat från Wikipedia:

_Separation of concerns is a design principle for separating a computer program into distinct sections such that each section addresses a separate concern. A concern is a set of information that affects the code of a computer program_

Genom att dela upp programmet i olika delar, så att varje del har sina egna problem att hantera, blir det lättare att hantera den oundvikliga komplexiteten i ett datorprogram.

Funktioner är ett sätt att organisera ett program i distinkta, hanterbara helheter. I stället för att skriva ett enda skript är tanken att formulera små, separat verifierbara funktioner som var och en löser en del av det större problemet.

En annan vanlig metod för att hantera större program är objekt, genom objektorienterade programmeringsprinciper. Det finns fördelar och nackdelar med båda metoderna, och varje programmerare har sin egen favorit. Som vi har sett hittills kan vi med hjälp av objekt och klasser samla alla data och den kod som bearbetar dessa data i en enda enhet, i ett objekts attribut och metoder. Dessutom ger objekten ett sätt att kapsla in de data de kontrollerar, så att andra delar av programmet inte behöver oroa sig för de interna detaljerna i ett objekt.

## Ett fungerande exempel: telefonkatalog

Hur ska ett program delas in i klasser och objekt? Det här är inte alls en enkel fråga med ett enda godtagbart svar, så vi fortsätter med ett exempel. I del fem genomförde du en [telefonkatalogsapplikation](/osa-5/3-dictionary#programming-exercise-puhelinluettelo-versio-2), och nu ska vi genomföra något liknande med hjälp av objektorienterade programmeringsprinciper.  

Enligt principen om separation of concerns bör ett program delas upp i sektioner som var och en har sin egen sak att ta hand om. I objektorienterad programmering översätts detta till [principen om ett ansvar](https://en.wikipedia.org/wiki/Single-responsibility_principle). Utan att gå in på detaljerna framgår det grundläggande syftet redan av namnet: en enda klass och de objekt som skapas utifrån den ska ha ett enda ansvar i programmet.


Objektorienterad programmering används ofta som ett sätt att modellera objekt och fenomen i den verkliga världen. Ett enskilt objekt i den verkliga världen modelleras med en enda klass i programkoden. I fallet med en telefonkatalog kan sådana objekt vara
- en person
- ett namn
- ett telefonnummer

Ett namn och ett telefonnummer kan uppfattas som data som inte förtjänar egna klasser, men en person är en distinkt fysisk enhet i den verkliga världen, och i programmeringsvärlden skulle den kunna fungera som en klass. Ett Person-objekt skulle vara ansvarigt för att knyta ihop ett namn och de telefonnummer som är kopplade till det.

En telefonkatalog i sig skulle kunna vara en bra kandidat för en klass. Dess ansvar skulle vara att hantera olika personobjekt och de data de innehåller.

Nu har vi skissat kärnan i vår applikation: telefonkatalog och person utgör programmeringslogiken i vår applikation, eller applikationslogiken i korthet. Vår applikation skulle behöva några andra klasser också.

Det är oftast en bra idé att hålla all interaktion med en användare skild från applikationslogiken. Det är ju trots allt ett helt eget ansvar. Förutom den centrala applikationslogiken bör vårt program därför innehålla en klass som hanterar användargränssnittet.

Dessutom bör vår telefonkatalog ha någon form av beständig lagring mellan exekveringar. Filhanteringen är återigen ett tydligt separat ansvar, så den förtjänar en egen klass.

Nu när vi har en översikt över de grundläggande komponenterna i vårt program uppstår frågan: var ska vi börja programmera? Inte heller här finns det något rätt eller fel svar, men det är ofta en bra idé att börja med någon del av programlogiken.

## Steg 1: en skiss för applikationslogiken

Låt oss börja med klassen Telefonkatalog. En skelettimplementering skulle kunna se ut så här:

```python
class Puhelinluettelo:
    def __init__(self):
        self.__henkilot = []

    def lisaa_numero(self, nimi: str, numero: str):
        pass

    def hae_numerot(self, nimi: str):
        pass

```

Denna klass består av en lista med personer samt metoder för att både lägga till och hämta data.

Varje person kan vara kopplad till flera nummer, så låt oss implementera den interna strukturen för `personer` med en ordlista. En ordlista ger oss möjlighet att söka efter nycklar enligt namn, och värdet som är kopplat till en ordlistas nyckel kan vara en lista. Hittills ser det ut som att vi inte behöver en separat klass för att representera en person – ett inlägg i en ordlista räcker.

Låt oss implementera de metoder som listas ovan och testa vår telefonkatalog:

```python
class Puhelinluettelo:
    def __init__(self):
        self.__henkilot = {}

    def lisaa_numero(self, nimi: str, numero: str):
        if not nimi in self.__henkilot:
            # henkilöön liittyy lista puhelinnumeroja
            self.__henkilot[nimi] = []

        self.__henkilot[nimi].append(numero)

    def hae_numerot(self, nimi: str):
        if not nimi in self.__henkilot:
            return None

        return self.__henkilot[nimi]

# testikoodi
luettelo = Puhelinluettelo()
luettelo.lisaa_numero("Erkki", "02-123456")
print(luettelo.hae_numerot("Erkki"))
print(luettelo.hae_numerot("Emilia"))
```

Detta borde utskriva följande:

<sample-output>

['02-123456']
None

</sample-output>

Metoden `hamta_nummer` returnerar `None` om ett namn inte finns med i telefonkatalogen. Om namnet finns returneras listan med de nummer som är kopplade till namnet.

När man gör ändringar i ett program är det alltid värt att testa att koden fungerar som förväntat innan man går vidare med andra ändringar. Den kod som används för testning är vanligtvis något som raderas strax efteråt, och därför kanske du tycker att det inte är värt besväret att skriva några tester i första hand. I de flesta fall är detta inte sant. Testning är en förutsättning för bra programmeringsresultat.

En bugg i programmet bör fångas upp och åtgärdas så snart som möjligt. Om du tar för vana att kontrollera funktionaliteten i praktiskt taget varje ny kodrad kommer du att upptäcka att buggarna oftast är lätta att hitta och åtgärda, eftersom du kan vara helt säker på att buggen orsakades av den senaste ändringen. Om du bara testar programmet efter att ha lagt till dussintals rader kod ökar de potentiella källorna till buggar också med dussintals gånger.

## Steg 2: en skiss för användargränssnittet

Med den grundläggande applikationslogiken ur vägen är det dags att implementera ett textbaserat användargränssnitt. Vi kommer att behöva en ny klass, `TelefonkatalogApplikation`, med följande inledande funktionalitet:

```python
class PuhelinluetteloSovellus:
    def __init__(self):
        self.__luettelo = Puhelinluettelo()

    def ohje(self):
        print("komennot: ")
        print("0 lopetus")

    def suorita(self):
        self.ohje()
        while True:
            print("")
            komento = input("komento: ")
            if komento == "0":
                break

sovellus = PuhelinluetteloSovellus()
sovellus.suorita()
```

Det här programmet gör inte så mycket ännu, men låt oss gå igenom innehållet. Konstruktormetoden skapar en ny Telefonkatalog, som lagras i ett privat attribut. Metoden `exekvera(self)` startar programmets textbaserade användargränssnitt, vars kärna är `while`-loopen, som fortsätter att be användaren om instruktioner tills de skriver in instruktionen för att avsluta. Det finns också en metod för instruktioner, `hjalp(self)`, som anropas innan man går in i loopen, så att instruktionerna skrivs ut.

Låt oss nu lägga till lite faktisk funktionalitet. Först implementerar vi att kunna lägga till nya data i telefonkatalogen:

```python
class PuhelinluetteloSovellus:
    def __init__(self):
        self.__luettelo = Puhelinluettelo()

    def ohje(self):
        print("komennot: ")
        print("0 lopetus")
        print("1 lisäys")

    def suorita(self):
        self.ohje()
        while True:
            print("")
            komento = input("komento: ")
            if komento == "0":
                break
            elif komento == "1":
                nimi = input("nimi: ")
                numero = input("numero: ")
                self.__luettelo.lisaa_numero(nimi, numero)

sovellus = PuhelinluetteloSovellus()
sovellus.suorita()
```

Om användaren skriver in 1 för att lägga till ett nytt nummer, frågar användargränssnittet efter ett namn och ett nummer och lägger till dessa i telefonkatalogen med hjälp av den lämpliga metod som definieras i klassen.

Användargränssnittets enda ansvar är att kommunicera med användaren. All annan funktionalitet, t.ex. att lagra ett nytt namn- och nummerpar, är Telefonkatalog-objektets ansvar.

Det finns utrymme för förbättringar i strukturen i vår användargränssnittsklass. Låt oss skapa en metod `tillägg_inlägg(self)` som hanterar instruktionen för att lägga till ett nytt inlägg:

```python
class PuhelinluetteloSovellus:
    def __init__(self):
        self.__luettelo = Puhelinluettelo()

    def ohje(self):
        print("komennot: ")
        print("0 lopetus")
        print("1 lisäys")

    # eriytetään uusien tietojen lisääminen omaksi metodiksi
    def lisays(self):
        nimi = input("nimi: ")
        numero = input("numero: ")
        self.__luettelo.lisaa_numero(nimi, numero)

    def suorita(self):
        self.ohje()
        while True:
            print("")
            komento = input("komento: ")
            if komento == "0":
                break
            elif komento == "1":
                self.lisays()

sovellus = PuhelinluetteloSovellus()
sovellus.suorita()
```

Separation of concerns-principen sträcker sig även till metodnivå. Vi skulle kunna ha hela användargränssnittets funktionalitet i en enda komplicerad `while`-loop, men det är bättre att separera varje funktionalitet i en egen metod. Ansvaret för `exekvera()`-metoden är bara att delegera de instruktioner som användaren skriver in till relevanta metoder. Detta hjälper till att hantera den växande komplexiteten i vårt program. Om vi till exempel senare vill ändra hur det fungerar att lägga till inlägg, är det omedelbart klart att vi då måste fokusera våra ansträngningar på `tillägg_inlägg()`-metoden.

Låt oss inkludera funktionalitet för att söka efter inlägg i vårt användargränssnitt. Detta bör också ha sin egen metod:

```python

class PuhelinluetteloSovellus:
    def __init__(self):
        self.__luettelo = Puhelinluettelo()

    def ohje(self):
        print("komennot: ")
        print("0 lopetus")
        print("1 lisäys")
        print("2 haku")

    def lisays(self):
        nimi = input("nimi: ")
        numero = input("numero: ")
        self.__luettelo.lisaa_numero(nimi, numero)

    def haku(self):
        nimi = input("nimi: ")
        numerot = self.__luettelo.hae_numerot(nimi)
        if numerot == None:
            print("numero ei tiedossa")
            return
        for numero in numerot:
            print(numero)

    def suorita(self):
        self.ohje()
        while True:
            print("")
            komento = input("komento: ")
            if komento == "0":
                break
            elif komento == "1":
                self.lisays()
            elif komento == "2":
                self.haku()
            else:
                self.ohje()

sovellus = PuhelinluetteloSovellus()
sovellus.suorita()
```

Vi har nu en enkel fungerande telefonkatalogsapplikation som är redo för testning. Följande är ett exempel på en körning:

<sample-output>

komennot:
0 lopetus
1 lisäys
2 haku

komento: **1**
nimi: **Erkki**
numero: **02-123456**

komento: **1**
nimi: **Erkki**
numero: **045-4356713**

komento: **2**
nimi: **Erkki**
02-123456
045-4356713

komento: **2**
nimi: Emilia
numero ei tiedossa

komento: **0**

</sample-output>

För en så enkel applikation har vi skrivit ganska mycket kod. Om vi hade skrivit allt i den enda `while`-loopen hade vi förmodligen kunnat komma undan med mycket mindre kod. Det är dock ganska lätt att läsa koden, strukturen är tydlig och vi borde inte ha några problem med att lägga till nya funktioner.

## Steg 3: Importera data från en fil

Låt oss anta att vi redan har några telefonnummer lagrade i en fil, och att vi vill läsa detta när programmet startar. Datafilen är i följande CSV-format:

```csv
Erkki;02-1234567;045-4356713
Emilia;040-324344
```

Hantering av filer är helt klart ett eget ansvarsområde, så det förtjänar en klass för sig:

```python
class Tiedostonkasittelija():
    def __init__(self, tiedosto):
        self.__tiedosto = tiedosto

    def lataa(self):
        nimet = {}
        with open(self.__tiedosto) as f:
            for rivi in f:
                osat = rivi.strip().split(';')
                nimi, *numerot = osat
                nimet[nimi] = numerot

        return nimet
```

Konstruktörsmetoden tar namnet på filen som sitt argument. Metoden `ladda_fil(self)` läser innehållet i filen. Varje rad delas upp i två delar: ett namn och en lista med siffror. Sedan läggs dessa till i en ordbok, med namnet som nyckel och listan som värde.

Metoden använder en smidig Python-funktion: det är möjligt att först välja några objekt från en lista separat och sedan ta resten av objekten i en ny lista. Du kan se ett exempel på detta nedan. Du kanske minns från [del 6](osa-6/1-tiedostojen-lukeminen#csv-tiedoston-lukeminen) att strängmetoden `split` returnerar en lista.

```python
lista = [1, 2, 3, 4, 5]
eka, toka, *loput = lista
print(eka)
print(toka)
print(loput)
```

<sample-output>

1
2
[3, 4, 5]

</sample-output>

Tecknet `*` framför variabelnamnet `resten` i ovanstående exempel betyder att den sista variabeln ska innehålla alla återstående poster i listan, från den tredje och framåt.

Vi bör absolut testa filhanteraren separat innan vi inkluderar den i vår applikation:

```python
t = Tiedostonkasittelija("luettelo.txt")
print(t.lataa())
```

<sample-output>

{'Erkki': ['02-1234567', '045-4356713'], 'Emilia': ['040-324344']}

</sample-output>

Eftersom filhanteraren verkar fungera bra kan vi lägga till den i vår applikation. Låt oss anta att vi vill läsa filen som det första varje gång programmet körs. Den logiska platsen för att läsa filen skulle vara konstruktören för klassen `TelefonkatalogApplikation`:

```python
class PuhelinluetteloSovellus:
    def __init__(self):
        self.__luettelo = Puhelinluettelo()
        self.__tiedosto = Tiedostonkasittelija("luettelo.txt")

        # listään tiedostossa olevat nimet luetteloon
        for nimi, numerot in self.__tiedosto.lataa().items():
            for numero in numerot:
                self.__luettelo.lisaa_numero(nimi, numero)

    # muu koodi
```

Denna funktionalitet bör också testas. När vi har försäkrat oss om att filens innehåll är tillgängligt via användargränssnittet i vår applikation kan vi gå vidare till nästa steg.

## Steg 4: exportera data till en fil

Den sista funktionen i vår grundversion av applikationen är att spara innehållet i telefonkatalogen tillbaka i samma fil som data lästes från.

Detta innebär en förändring av `Telefonkatalog`-klassen. Vi måste kunna exportera innehållet i telefonkatalogen:

```python
class Puhelinluettelo:
    def __init__(self):
        self.__henkilot = {}

    # ...

    # palautetaan tiedostoon tallentamista varten kaikki tiedot
    def kaikki_tiedot(self):
        return self.__henkilot
```

Själva sparandet till filen bör hanteras av `FilHanterare`-klassen. Låt oss lägga till metoden `spara_fil` som tar en ordlistsrepresentation av telefonkatalogen som argument:

```python
class Tiedostonkasittelija():
    def __init__(self, tiedosto):
        self.__tiedosto = tiedosto

    def lataa(self):
        # ...

    def talleta(self, luettelo: dict):
        with open(self.__tiedosto, "w") as f:
            for nimi, numerot in luettelo.items():
                rivi = [nimi] + numerot
                f.write(";".join(rivi) + "\n")
```

Sparandet bör ske när programmet avslutas. Låt oss lägga till en metod för detta ändamål i användargränssnittet och anropa den innan vi bryter ut ur `while`-loopen:

```python

class PuhelinluetteloSovellus:
    # muu koodi

    # metodi, joka suoritetaan lopetettaessa sovelluksen käyttö
    def lopetus(self):
        self.__tiedosto.talleta(self.__luettelo.kaikki_tiedot())

    def suorita(self):
        self.ohje()
        while True:
            print("")
            komento = input("komento: ")
            if komento == "0":

                self.lopetus()
                break
            elif komento == "1":
                self.lisays()
            elif komento == "2":
                self.haku()
            else:
                self.ohje()
```

<programming-exercise name='Puhelinluettelon laajennus, osa 1' tmcname='osa10-10_puhelinluettelo_osa1'>

Tässä tehtävässä tehdään pieni laajennus puhelinluettelosovellukseen. Yllä kehitetty koodi löytyy tehtäväpohjasta. Laajenna ratkaisuasi komennolla, joka mahdollistaa nimen etsimisen numeron perusteella. Laajennuksen jälkeen sovelluksen pitäisi toimia seuraavasti:

<sample-output>

komennot:
0 lopetus
1 lisäys
2 haku
3 haku numeron perusteella

komento: **1**
nimi: **Erkki**
numero: **02-123456**

komento: **1**
nimi: **Erkki**
numero: **045-4356713**

komento: **3**
numero: **02-123456**
Erkki

komento: **3**
numero: **0100100**
tuntematon numero

komento: **0**

</sample-output>

Tee laajennus sitten, että kunnioitat ohjelman rakennetta. Eli lisää luokkaan `PuhelinluetteloSovellus` uutta ominaisuutta varten sopiva apumetodi sekä oma haara while-silmukkaan. Lisää myös sovelluslogiikkaan eli luokkaan `Puhelinluettelo` metodi, joka mahdollistaa nimen hakemisen numeron perusteella.

</programming-exercise>

## Objekt i en ordlista

I nästa övning ombeds du att ändra din telefonkatalog så att värdena i ordlistan är objekt, inte listor.

Det är inget konstigt med det i sig, men det är första gången på den här kursen som något sådant föreslås, så låt oss gå igenom ett enklare exempel innan vi dyker ner i övningen.

Här har vi en applikation som håller reda på hur många övningar som studenterna har gjort på en kurs. Varje elevs antal övningar lagras i ett enkelt objekt:

```python
class Tehtavalaskuri:
    def __init__(self):
        self.__tehtavia = 0

    def merkkaa(self):
        self.__tehtavia += 1

    def tehtyja(self):
        return self.__tehtavia
```

Följande huvudfunktion använder klassen ovan:

```python
opiskelijat = {}

print("merkataan tehtäviä")
while True:
    nimi = input("opiskelija: ")
    if len(nimi) == 0:
        break

    # luodaan tarvittaessa olio tehtävämäärän laskemista varten
    if not nimi in opiskelijat:
        opiskelijat[nimi] = Tehtavalaskuri()

    # merkataan tehdyksi nimeä vastaavaan olioon
    opiskelijat[nimi].merkkaa()

print()
print("tehdyt tehtävät:")

for opiskelija, tehtavat in opiskelijat.items():
    print(f"{opiskelija} tehtäviä {tehtavat.tehtyja()} kpl")
```

Att exekvera koden ovan kunde se ut enligt följande:

<sample-output>

merkataan tehtäviä
opiskelija: **pekka**
opiskelija: **sara**
opiskelija: **antti**
opiskelija: **sara**
opiskelija: **juuso**
opiskelija: **juuso**
opiskelija: **antti**
opiskelija: **sara**
opiskelija:

tehdyt tehtävät:
pekka tehtäviä 1 kpl
antti tehtäviä 2 kpl
sara tehtäviä 3 kpl
juuso tehtäviä 2 kpl

</sample-output>

Det finns ett par saker att tänka på i exemplet ovan. När användaren matar in ett namn kontrollerar programmet först om namnet redan är en nyckel i ordlistan. Om namnet inte finns skapas ett nytt objekt som läggs till som en post i ordlistan:

```python
if not nimi in opiskelijat:
    opiskelijat[nimi] = Tehtavalaskuri()
```

Efter detta kan vi vara säkra på att objektet existerar, kopplat till namnet på den student som används som nyckel. Antingen skapades det precis, eller så fanns det redan från en tidigare iteration av loopen. I vilket fall som helst kan vi nu hämta objektet med nyckeln och kalla metoden `klar`:

```python
opiskelijat[nimi].merkkaa()
```

Raden ovan innehåller egentligen två separata händelser. Vi kan lika gärna använda en hjälpvariabel och skriva den på två separata kodrader:

```python
opiskelijan_laskuri = opiskelijat[nimi]
opiskelijan_laskuri.merkkaa()
```

OBS: Även om objektet här tilldelas en hjälpvariabel, så finns objektet kvar i ordlistan precis som tidigare. Hjälparvariabeln innehåller en referens till objektet i ordlistan.

Om du inte är helt säker på vad som egentligen händer i koden ovan kan du prova med [visualiseringsverktyget](http://www.pythontutor.com/visualize.html#mode=edit).

<programming-exercise name='Puhelinluettelon laajennus, osa 2' tmcname='osa10-11_puhelinluettelo_osa2'>

Tässä tehtävässä laajennetaan puhelinluettelosovellusta siten, että henkilöihin voi liittyä myös osoite. Yksinkertaisuuden vuoksi koodista on kuitenkin poistettu tiedostoon tallentaminen. Myös muutama metodi on uudelleennimetty vastaamaan paremmin laajennuksen jälkeistä tilannetta.

## Luokka henkilön tietojen esittämiseen

Siirretään henkilön tietojen (eli puhelinnumerojen sekä osoitteen) esittäminen oman luokkansa `Henkilo` vastuulle. Toteuta luokka siten, että se toimii seuraavasti:


```python
henkilo = Henkilo("Erkki")
print(henkilo.nimi())
print(henkilo.numerot())
print(henkilo.osoite())
henkilo.lisaa_numero("040-123456")
henkilo.lisaa_osoite("Mannerheimintie 10 Helsinki")
print(henkilo.numerot())
print(henkilo.osoite())
```

<sample-output>

Erkki
[]
None
['040-123456']
Mannerheimintie 10 Helsinki

</sample-output>

## Puhelinluettelo käyttämään luokkaa Henkilo

Muuta koodiasi siten, että se toimii käyttäjän näkökulmasta täysin samoin kuin aiemmin, mutta luokka `Puhelinluettelo` tallettaakin henkilöt sisäisesti käyttäen luokan `Henkilo` olioita. Käytännössä siis oliomuuttujana `__henkilot` tulee olla sanakirja, johon listojen sijaan talletetaan henkilö-olioita.

**VAROITUS:** kun teet koodiin tämän tehtävän kaltaista rakenteellista muutosta, etene pienin askelin. Älä missään tapauksessa yritä tehdä kaikkea kerrallaan, se on **varma keino ajautua pahoihin ongelmiin**.

Sopiva pieni askel nyt voi olla se, että tarkastat ensin erikseen luokan `Puhelinluettelo` toimivuuden. Esimerkiksi seuraavan koodin tulee toimia kuten olettaa saattaa:

```python
luettelo = Puhelinluettelo()
luettelo.lisaa_numero("Erkki", "02-123456")
print(luettelo.hae_tiedot("Erkki"))
print(luettelo.hae_tiedot("Emilia"))
```

Tehtävässä ei tarkisteta, millainen tulostusasu `hae_tiedot`-metodin palauttamalla tuloksella on, mutta varmista ettei koodi aiheuta virheitä, ja että tulos on järkevä. Kun olet 100% varma, että kaikki toimii luokan `Puhelinluettelo` osalta, voit edetä varmistamaan, että kaikki toimii edelleen entiseen tapaan käyttöliittymää käytettäessä.

## Osoitteen lisääminen

Laajenna nyt sovellusta siten, että puhelinluetteloon on mahdollista tallettaa myös henkilöiden osoitteet. Ohjelman tulisi toimia seuraavasti:

<sample-output>

komennot:
0 lopetus
1 nimen lisäys
2 haku
3 osoitteen lisäys

komento: **1**
nimi: **Erkki**
numero: **02-123456**

komento: **3**
nimi: **Emilia**
osoite: **Viherlaaksontie 7, Espoo**

komento: **2**
nimi: **Erkki**
02-123456
osoite ei tiedossa

komento: **2**
nimi: **Emilia**
numero ei tiedossa
Viherlaaksontie 7, Espoo

komento: **3**
nimi: **Erkki**
osoite: **Linnankatu 75, Turku**

komento: 2
nimi: **Erkki**
02-123456
Linnankatu 75, Turku

komento: **2**
nimi: **Wilhelm**
osoite ei tiedossa
numero ei tiedossa

komento: **0**

</sample-output>

**VAROITUS ja vihje:** kuten tehtävän edellisessä osassa sanottiin, älä missään tapauksessa yritä tehdä kaikkea kerrallaan, se on **varma keino ajautua pahoihin ongelmiin**.

Varmista ensin että voit lisätä osoitteita luokkaan `Puhelinluettelo` ja kun olet 100% varma, että se toimii, voit laajentaa sovelluksen käyttöliittymää uuden toiminnallisuuden osalta.

</programming-exercise>

## Några avslutande anmärkningar

Strukturen i Telefonkatalog-exemplet ovan följer de grundläggande principerna för objektorienterad programmering ganska väl. Den centrala principen är att identifiera de olika ansvarsområdena i programmet och fördela dessa logiskt mellan de olika klasserna och metoderna. Ett av de viktigaste motiven för denna uppdelning är att hantera komplexiteten. Ett annat viktigt motiv är att en logisk uppdelning av ansvarsområden - modularitet i facktermer - ofta gör koden lättare att underhålla och bygga vidare på.

I de programvarupaket som utvecklas och används ute i världen är underhåll och utbyggnad, dvs felsökning av befintlig programvara och implementering av nya funktioner, den absolut dyraste delen av utvecklingen. Korrekt implementerad modularitet är ekonomiskt sett en mycket viktig funktion i programvaruutvecklingen.

Det finns några fler objektorienterade programmeringsprinciper som är värda att lyfta fram här. Telefonkatalog är ett bra exempel på hur den centrala programlogiken kan (och bör) separeras från både användargränssnitt och datalagring. Detta är viktigt på grund av ett par olika skäl. För det första gör denna separation det möjligt att testa koden i mindre enheter, en klass och metod i taget. För det andra, eftersom kärnlogiken nu är oberoende av gränssnitten som kommer till omvärlden, är det möjligt att i viss utsträckning ändra implementeringen av antingen kärnlogiken eller gränssnitten utan att hela applikationen går sönder.

Filhanteringen i Telefonkatalog-programmet går till på följande sätt: Programmet läser filen en enda gång, när det startar. Efter detta lagras all data i variabler i programmet. När programmet avslutas lagras alla data igen, vilket i praktiken innebär att filen skrivs över. I de flesta fall är detta det rekommenderade sättet att hantera externa filer, eftersom det ofta är mycket mer komplicerat att redigera data på plats.

Det finns många bra guideböcker för att lära sig om god programmeringspraxis. En sådan är [Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) av Robert Martin. Kodexemplen i boken är dock implementerade i Java, så att arbeta igenom exemplen kan vara ganska besvärligt vid denna tidpunkt i din programmeringskarriär, även om boken i sig rekommenderas mycket av kurspersonalen. Teman som lätt underhållen, utbyggbar kod av god kvalitet kommer att utforskas ytterligare på kurserna [Software Development Methods](https://studies.helsinki.fi/opintotarjonta/cu/hy-CU-118024742-2020-08-01) och [Software Engineering](https://studies.helsinki.fi/opintotarjonta/cu/hy-CU-118024909-2020-08-01).

Att skriva kod enligt etablerade principer för objektorienterad programmering har ett pris. Du kommer sannolikt att få skriva mer kod än om du skulle skriva din implementation i en enda kontinuerlig stöt av spaghettikod. En av de viktigaste färdigheterna hos en programmerare är att bestämma det bästa tillvägagångssättet för varje situation. Ibland är det nödvändigt att bara hacka ihop något snabbt för omedelbar användning. Å andra sidan, om det inom överskådlig framtid kan förväntas att koden kommer att återanvändas, underhållas eller vidareutvecklas, antingen av dig eller, mer kritiskt, av någon helt annan, blir programkodens läsbarhet och logiska modularitet väsentlig. Oftast är det så att om det är värt att göra, så är det värt att göra det bra, även i de allra tidigaste utvecklingsstadierna.

För att avsluta denna del av materialet kommer du att implementera ytterligare en större applikation.

<programming-exercise name='Opintorekisteri' tmcname='osa10-12_opintorekisteri'>

Tee interaktiivinen ohjelma, jonka avulla voit pitää kirjaa opintomenestyksestäsi. Sovelluksen rakenteen saat päättää itse, mutta nyt on hyvä tilaisuus harjoitella Puhelinluettelo-esimerkin kaltaisen oliorakenteen muodostamista.

Ohjelman tulee toimia seuraavasti:

<sample-output>

1 lisää suoritus
2 hae suoritus
3 tilastot
0 lopetus

komento: **1**
kurssi: **Ohpe**
arvosana: **3**
opintopisteet: **5**

komento: **2**
kurssi: **Ohpe**
Ohpe (5 op) arvosana 3

komento: **1**
kurssi: **Ohpe**
arvosana: **5**
opintopisteet: **5**

komento: **2**
kurssi: **Ohpe**
Ohpe (5 op) arvosana 5

komento: **1**
kurssi: **Ohpe**
arvosana: **1**
opintopisteet: **5**

komento: **2**
kurssi: **Ohpe**
Ohpe (5 op) arvosana 5

komento: **2**
kurssi: **Java-ohjelmointi**
ei suoritusta

komento: **1**
kurssi: **Tira**
arvosana: **1**
opintopisteet: **10**

komento: **1**
kurssi: **Tilpe**
arvosana: **2**
opintopisteet: **5**

komento: **1**
kurssi: **Lapio**
arvosana: **4**
opintopisteet: **1**

komento: **1**
kurssi: **Lama**
arvosana: **5**
opintopisteet: **8**

komento: **3**
suorituksia 5 kurssilta, yhteensä 29 opintopistettä
keskiarvo 3.4
arvosanajakauma
5: xx
4: x
3:
2: x
1: x

komento: **0**

</sample-output>

Muutama huomio: kultakin kurssilta tallentuu ainoastaan yksi arvosana. Arvosanaa voi korottaa, mutta se ei voi laskea.

Tehtävästä on tarjolla kaksi tehtäväpistettä. Ensimmäisen pisteen saa jos toiminnot 1 ja 2 sekä lopetus toimivat. Toisen pisteen saa jos myös toiminto 3 on toteutettu.

</programming-exercise>

## Epilog

För att avsluta den här delen av materialet återvänder vi till användargränssnittet i telefonkatalogsexemplet för en stund.

```python
class PuhelinluetteloSovellus:
    def __init__(self):
        self.__luettelo = Puhelinluettelo()
        self.__tiedosto = Tiedostonkasittelija("luettelo.txt")

    # muu koodi

sovellus = PuhelinluetteloSovellus()
sovellus.suorita()
```

Ett `TelefonkatalogApplikation`-objekt innehåller både ett `Telefonkatalog`-objekt och ett `FilHanterare`-objekt. Namnet på den fil som skickas till FilHanterare är för närvarande hårdkodat i `TelefonkatalogApplikation`-klassen. Detta är en helt irrelevant detalj när det gäller applikationens användargränssnitt. Faktum är att den bryter mot principen om separation of concerns: var ett `Telefonkatalog`-objekt sparar sitt innehåll ska inte vara en angelägenhet för en `TelefonkatalogApplikation`, men om vi vill ändra platsen måste vi ändra koden för `TelefonkatalogApplikation`.

Det skulle vara en bättre idé att skapa ett FilHanterare-objekt någonstans utanför `TelefonkatalogApplikation`-klassen och skicka det som ett argument till applikationen:

```python
class PuhelinluetteloSovellus:
    def __init__(self, tiedosto):
        self.__luettelo = Puhelinluettelo()
        self.__tiedosto = tiedosto

    # muu koodi

# luodaan tallennuksen hoitava olio
tallennuspalvelu = Tiedostonkasittelija("luettelo.txt")
# ja annetaan se PuhelinluetteloSovellus-oliolle konsturuktorin parametrina
sovellus = PuhelinluetteloSovellus(tallennuspalvelu)
sovellus.suorita()
```

Detta tar bort ett onödigt beroende från `TelefonkatalogApplikation`-klassen. Om namnet på filen ändras behöver användargränssnittet inte längre ändras. Vi behöver bara skicka ett annat argument till konstruktören:


```python
class PuhelinluetteloSovellus:
    def __init__(self, tiedosto):
        self.__luettelo = Puhelinluettelo()
        self.__tiedosto = tiedosto

    # muu koodi

# vaihdetaan tiedostoa
tallennuspalvelu = Tiedostonkasittelija("uusi_luettelotiedosto.txt")
sovellus = PuhelinluetteloSovellus(tallennuspalvelu)
sovellus.suorita()
```

Denna förändring gör det också möjligt för oss att överväga mer exotiska lagringsplatser, till exempel en molntjänst på internet. Vi behöver bara implementera en klass som använder molntjänsten och erbjuder `TelefonkatalogApplikation` exakt samma metoder som `FilHanterare`.

En instans av denna nya "moln hanterar"-klass kan skickas som ett argument till konstruktören och inte en enda rad kod behöver ändras i användargränssnittet:

```python
class InternetTallennin:
    # koodi joka tallentaa luettelon tiedot internetissä olevaan pilvipalveluun

tallennuspalvelu = InternetTallennin("amazon-cloud", "mluukkai", "passwrd")
sovellus = PuhelinluetteloSovellus(tallennuspalvelu)
sovellus.suorita()
```

Som du har sett tidigare har den här typen av tekniker ett pris, eftersom det blir mer kod att skriva, så en programmerare måste överväga om det är en acceptabel avvägning.

Den teknik som beskrivs ovan kallas beroendeinjektion. Som namnet antyder är tanken att alla beroenden som krävs av ett objekt ska tillhandahållas utanför objektet. Det är ett mycket användbart verktyg i en programmerares verktygslåda, eftersom det gör det lättare att implementera nya funktioner i program och underlättar automatisk testning. Detta tema kommer att utforskas ytterligare på de tidigare nämnda kurserna [Software Development](https://studies.helsinki.fi/opintotarjonta/cu/hy-CU-118024742-2020-08-01) och [Software Engineering](https://studies.helsinki.fi/opintotarjonta/cu/hy-CU-118024909-2020-08-01).


Svara vänligen på en snabb enkät om denna del av kursen.

<quiz id="a5d5c420-b834-5a04-a8e3-a442912adcfa"></quiz>
