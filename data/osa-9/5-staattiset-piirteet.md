---
path: '/osa-9/5-staattiset-piirteet'
title: 'Klassattribut'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Är du bekant med begreppen klassvariabel och klassmetod
- Vet du hur statiska egenskaper skiljer sig från egenskaper hos instanser
- Kommer du att kunna lägga till statiska egenskaper i dina egna klasser

</text-box>

Objektens egenskaper är ett centralt begrepp inom objektorienterad programmering. Termen egenskaper (eng. traits) omfattar de metoder och variabler som definieras i klassdefinitionen.  

Hittills har vi mest behandlat egenskaper hos objekt. Dessa inkluderar de metoder och attribut som är tillgängliga i alla instanser av en klass. Faktum är att klasser i sig också kan ha egenskaper, som ibland kallas statiska egenskaper, eller mer specifikt klassvariabler och klassmetoder.

## Klassvariabler

Varje instans av en klass har sina egna specifika värden för varje attribut som definieras i klassen, som vi har sett i exemplen i de tidigare avsnitten. Men vad händer om vi vill ha data som delas mellan de olika instanserna? Här kommer klassvariablerna in i bilden, även kallade statiska variabler. En klassvariabel är en variabel som nås via själva klassen, inte via de instanser som skapas baserat på klassen. Vid varje given tidpunkt under exekveringen av programmet har en klassvariabel ett enda värde, oavsett hur många instanser av klassen som skapas.

En klassvariabel deklareras utan `self`-prefixet och vanligtvis utanför varje metoddefinition eftersom den ska kunna nås var som helst inom klassen eller till och med utanför klassen.

```python
class Sparkonto:
    allman_ranta = 0.03

    def __init__(self, kontonummer: str, saldo: float, ranta: float):
        self.__kontonummer = kontonummer
        self.__saldo = saldo
        self.__ranta = ranta

    def tillsatt_ranta(self):
        # Räntan är allmänna räntan + kontots ränta
        ranta_totalt = Sparkonto.allman_ranta + self.__ranta
        self.__saldo += self.__saldo * ranta_totalt

    @property
    def saldo(self):
        return self.__saldo
```

Eftersom variabeln `allman_ranta` definieras inom klassen men utanför alla metoddefinitioner och inte använder prefixet `self`, är det en klassvariabel.

En klassvariabel nås via klassens namn, till exempel så här:

```python
# Den allmänna räntan är oberoende av andra instanser av objektet
print("Allmänna räntan är", Sparkonto.allman_ranta)

konto = Sparkonto("12345", 1000, 0.05)
# Lägg till totala räntant till kontots saldo
konto.tillsatt_ranta()
print(konto.saldo)
```

<sample-output>

Allmänna räntan är 0.03
1080.0

</sample-output>

Klassvariablerna nås alltså via klassens namn, till exempel `Sparkonto.allman_ranta`, medan instansvariablerna nås via objektvariabelns namn, till exempel `konto.saldo`. En instansvariabel existerar naturligtvis bara när en instans av klassen har skapats, men en klassvariabel är tillgänglig överallt och vid varje tidpunkt då klassen i sig är tillgänglig.

Klassvariabler är användbara när det finns behov av värden som delas av alla instanser av klassen. I exemplet ovan antog vi att den totala räntan för alla sparkonton består av två komponenter: den allmänna räntan delas av alla konton, men varje konto har också sin egen ränta i en instansvariabel. Den allmänna räntan kan också förändras, men förändringen kommer då att påverka alla instanser av klassen lika mycket.

```python
class Sparkonto:
    allman_ranta = 0.03

    def __init__(self, kontonummer: str, saldo: float, ranta: float):
        self.__kontonummer = kontonummer
        self.__saldo = saldo
        self.__ranta = ranta

    def tillsatt_ranta(self):
        # Räntan är allmänna räntan + kontots ränta
        ranta_totalt = Sparkonto.allman_ranta + self.__ranta
        self.__saldo += self.__saldo * ranta_totalt

    @property
    def saldo(self):
        return self.__saldo

    @property
    def totalranta(self):
        return self.__ranta + Sparkonto.allman_ranta
```

```python
konto1 = Sparkonto("12345", 100, 0.03)
konto2 = Sparkonto("54321", 200, 0.06)

print("Allmänna räntan:", Sparkonto.allman_ranta)
print(konto1.totalranta)
print(konto2.totalranta)

# Vi ökar den allmänna räntan till 10 procent
Sparkonto.allman_ranta = 0.10

print("Allmänna räntan:", Sparkonto.allman_ranta)
print(konto1.totalranta)
print(konto2.totalranta)
```

<sample-output>

Allmänna räntan: 0.03
0.06
0.09
Allmänna räntan: 0.1
0.13
0.16

</sample-output>

När den allmänna räntan ändras, ändras den totala räntan för alla instanser av klassen. Som du kan se ovan är det möjligt att lägga till en getter-metod med `@property`-dekoratorn även om det inte finns ett attribut med samma namn i klassen. Denna metod returnerar summan av den allmänna räntan och den kontospecifika räntan.

Låt oss ta en titt på ett annat exempel. Klassen `Telefonnummer` används för att definiera ett enda telefonnummer, men den innehåller också några landskoder i en ordbok. Denna ordbok är en klassvariabel och delas därför av alla instanser av klassen, eftersom landskoden för telefonnummer från ett och samma land alltid är densamma.

```python
class Telefonnummer:
    landkoder = {"Finland": "+358", "Sverige": "+46", "USA": "+1"}

    def __init__(self, namn: str, telefonnummer: str, land: str):
        self.__namn = namn
        self.__telefonnummer = telefonnummer
        self.__land = land

    @property
    def telefonnummer(self):
        # Den första nollan tas bort då landskoden läggs till
        return Telefonnummer.landkoder[self.__land] + " " + self.__telefonnummer[1:]
```

```python
paulan_nro = Telefonnummer("Pernilla Pythonson", "050 1234 567", "Finland")
print(paulan_nro.telefonnummer)
```

<sample-output>

+358 50 1234 567

</sample-output>

Varje Telefonnummer-objekt innehåller namnet på ägaren, själva numret och det land där telefonnumret finns. När attributet som innehåller telefonnumret nås med getter-metoden hämtas lämplig landskod från klassvariabelns ordbok baserat på landattributet, och resultatet prefixeras till numret.

Implementeringsexemplet ovan är inte särskilt funktionellt i övrigt. I följande exempel har vi lagt till getter och sättare för alla attribut:

```python
class Telefonnummer:
    landkoder = {"Finland": "+358", "Sverige": "+46", "USA": "+1"}

    def __init__(self, namn: str, telefonnummer: str, land: str):
        self.__namn = namn
        # Det här kallar metoden telefonnummer.setter
        self.telefonnummer = telefonnummer
        # Det här kallar metoden land.setter
        self.land = land

    # Getter-metoden för telefonnummer kombinerar landskoden och attributet telefonnummer
    @property
    def telefonnummer(self):
        # Den första nollan tas bort då landskoden läggs till
        return Telefonnummer.landkoder[self.__land] + " " + self.__telefonnummer[1:]

    @telefonnummer.setter
    def telefonnummer(self, nummer):
        # Vi granksar att numret endast innehåller siffror och mellanslag
        for marke in nummer:
            if marke not in "1234567890 ":
                raise ValueError("Telefonnummer får innehålla endast siffror och mellanslag")
        self.__telefonnummer = nummer

    # Endast telefonnummer utan landskod
    @property
    def lokalt_nummer(self):
        return self.__telefonnummer

    @property
    def land(self):
        return self.__land

    @land.setter
    def land(self, land):
        # Vi granskar att landet är en nyckel i ordlistan
        if land not in Telefonnummer.landkoder:
            raise ValueError("Det angivna landet hittades inte på listan")
        self.__land = land

    @property
    def namn(self):
        return self.__namn

    @namn.setter
    def namn(self, namn):
        self.__namn = namn

    def __str__(self):
        return f"{self.telefonnummer} ({self.__namn})"
```

```python
if __name__ == "__main__":
    tlfnnmr = Telefonnummer("Petter Python", "040 111 1111", "Sverige")
    print(tlfnnmr)
    print(tlfnnmr.telefonnummer)
    print(tlfnnmr.lokalt_nummer)
```

<sample-output>

+46 40 111 1111 (Petter Python)
+46 40 111 1111
040 111 1111

</sample-output>

<programming-exercise name='Postinumerot' tmcname='osa09-13_postinumerot'>

I uppgiftsbotten finns klassen `Stad` definierad, som modellerar en enskild stad.

Tillsätt en klassvariabel med namnet `postnummer`, som refererar till en ordlista. I ordlistan används städernas namn som nycklar, och värdena som fås är städernas postnummer. Båda är strängar.

I ordlistan ska åtminstone följande postnummer hittas:

* Helsingfors 00100
* Åbo 20100
* Tammerfors 33100
* Jyväskylä 40100
* Uleåborg 90100

Annan funktionalitet behövs inte implementeras.

</programming-exercise>

## Klassmetoder

En klassmetod, även kallad statisk metod, är en metod som inte är knuten till någon enskild instans av klassen. En klassmetod kan anropas utan att några instanser av klassen skapas.

Klassmetoder är vanligen verktyg som har något att göra med klassens syfte, men som är fristående i den meningen att det inte ska vara nödvändigt att skapa instanser av klassen för att kunna anropa dem. Klassmetoder är vanligtvis offentliga, så att de kan anropas både utanför klassen och inom klassen, inklusive inom instanser av klassen.

En klassmetod definieras med annotationen `@classmethod`. Den första parametern är alltid `cls`. Variabelnamnet `cls` liknar `self`-parametern. Skillnaden är att `cls` pekar på klassen medan `self` pekar på en instans av klassen. Ingen av parametrarna ingår i argumentlistan när funktionen anropas, utan Python fyller i lämpligt värde automatiskt.

I följande exempel har vi en klass som modellerar fordonsregistreringar. Klassen `Registration` innehåller en statisk metod för att kontrollera om en registernummer är giltig. Metoden är en statisk klassmetod eftersom det är användbart att kunna kontrollera om en registernummer är giltig redan innan ett enda Registration-objekt har skapats:

```python
class Registration:
    def __init__(self, agare: str, marke: str, ar: int, registernummer: str):
        self.__agare = agare
        self.__marke = marke
        self.__ar = ar

        # Vi anropar metoden registernummer.setter
        self.registernummer = registernummer

    @property
    def registernummer(self):
        return self.__registernummer

    @registernummer.setter
    def registernummer(self, nummer):
        if Registration.registernummer_giltigt(nummer):
            self.__registernummer = nummer
        else:
            raise ValueError("Registernummer inte giltigt")

    # Klassmetod som validerar registernumret
    @classmethod
    def registernummer_giltigt(cls, nummer: str):
        if len(nummer) < 3 or "-" not in nummer:
            return False

        # Granska början och slutet av numret skilt
        borjan, slutet = nummer.split("-")

        # Börjandelen får endast innehålla bokstäver
        for marke in borjan:
            if marke.lower() not in "abcdefghijklmnopqrstuvwxyzåäö":
                return False

        # Slutdelen får endast innehålla siffror
        for marke in slutet:
            if marke not in "1234567890":
                return False

        return True
```

```python
reg = Registration("Bertil Bilist", "Volvo", "1992", "abc-123")

if Registration.registernummer_giltigt("xyz-789"):
    print("Detta är ett giltigt nummer!")
```

<sample-output>

Detta är ett giltigt nummer!

</sample-output>

Giltigheten för en registernummer kan kontrolleras även utan att skapa en enda instans av klassen, t.ex. med `Registration.nummer_plat_giltig("xyz-789")`. Samma metod anropas i klassens konstruktor. OBS: även inom konstruktören är denna metod åtkomlig via klassens namn, inte `self`! 

<programming-exercise name='Lista-apuri' tmcname='osa09-14_lista_apuri'>

Skapa en klass med namnet `ListHjalpare` som innehåller följande två klassmetoder:

* Metoden `storsta_frekvensen(lista: list)` returnerar det mest förekommande föremålet på listan
* Metoden `dubbletter(lista: list)` returnerar antalet unika tal som förekommer åtminstone två gånger på listan

Det ska vara möjligt att använda dessa metoder utan att skapa en instans av klassen. Ett exempel på hur metoderna kan användas:

```python
tal = [1, 1, 2, 1, 3, 3, 4, 5, 5, 5, 6, 5, 5, 5]
print(ListHjalpare.storsta_frekvensen(tal))
print(ListHjalpare.dubbletter(tal))
```

<sample-output>

5
3

</sample-output>

</progarmming-exercise>
