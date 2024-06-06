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
class Korkotili:
    yleiskorko = 0.03

    def __init__(self, tilinumero: str, saldo: float, korko: float):
        self.__tilinumero = tilinumero
        self.__saldo = saldo
        self.__korko = korko

    def lisaa_korko(self):
        # Korko on yleiskorko + tilin korko
        korko_yhteensa = Korkotili.yleiskorko + self.__korko
        self.__saldo += self.__saldo * korko_yhteensa

    @property
    def saldo(self):
        return self.__saldo
```

Eftersom variabeln `allman_ranta` definieras inom klassen men utanför alla metoddefinitioner och inte använder prefixet `self`, är det en klassvariabel.

En klassvariabel nås via klassens namn, till exempel så här:

```python
# Yleiskorko on olioista riippumaton
print("Yleiskorko on", Korkotili.yleiskorko)

tili = Korkotili("12345", 1000, 0.05)
# Lisätään kokonaiskorko saldoon
tili.lisaa_korko()
print(tili.saldo)
```

<sample-output>

Yleiskorko on 0.03
1080.0

</sample-output>

Klassvariablerna nås alltså via klassens namn, till exempel `Sparkonto.allman_ranta`, medan instansvariablerna nås via objektvariabelns namn, till exempel `konto.saldo`. En instansvariabel existerar naturligtvis bara när en instans av klassen har skapats, men en klassvariabel är tillgänglig överallt och vid varje tidpunkt då klassen i sig är tillgänglig.

Klassvariabler är användbara när det finns behov av värden som delas av alla instanser av klassen. I exemplet ovan antog vi att den totala räntan för alla sparkonton består av två komponenter: den allmänna räntan delas av alla konton, men varje konto har också sin egen ränta i en instansvariabel. Den allmänna räntan kan också förändras, men förändringen kommer då att påverka alla instanser av klassen lika mycket.

```python
class Korkotili:
    yleiskorko = 0.03

    def __init__(self, tilinumero: str, saldo: float, korko: float):
        self.__tilinumero = tilinumero
        self.__saldo = saldo
        self.__korko = korko

    def lisaa_korko(self):
        # Korko on yleiskorko + tilin korko
        korko_yhteensa = Korkotili.yleiskorko + self.__korko
        self.__saldo += self.__saldo * korko_yhteensa

    @property
    def saldo(self):
        return self.__saldo

    @property
    def kokonaiskorko(self):
        return self.__korko + Korkotili.yleiskorko
```

```python
tili1 = Korkotili("12345", 100, 0.03)
tili2 = Korkotili("54321", 200, 0.06)

print("Yleiskorko:", Korkotili.yleiskorko)
print(tili1.kokonaiskorko)
print(tili2.kokonaiskorko)

# Nostetaan yleiskorko 10 prosenttiin
Korkotili.yleiskorko = 0.10

print("Yleiskorko:", Korkotili.yleiskorko)
print(tili1.kokonaiskorko)
print(tili2.kokonaiskorko)
```

<sample-output>

Yleiskorko: 0.03
0.06
0.09
Yleiskorko: 0.1
0.13
0.16

</sample-output>

När den allmänna räntan ändras, ändras den totala räntan för alla instanser av klassen. Som du kan se ovan är det möjligt att lägga till en getter-metod med `@property`-dekoratorn även om det inte finns ett attribut med samma namn i klassen. Denna metod returnerar summan av den allmänna räntan och den kontospecifika räntan.

Låt oss ta en titt på ett annat exempel. Klassen `TelefonNummer` används för att definiera ett enda telefonnummer, men den innehåller också några landskoder i en ordbok. Denna ordbok är en klassvariabel och delas därför av alla instanser av klassen, eftersom landskoden för telefonnummer från ett och samma land alltid är densamma.

```python
class Puhelinnumero:
    maatunnukset = {"Suomi": "+358", "Ruotsi": "+46", "Yhdysvallat": "+1"}

    def __init__(self, nimi: str, puhelinnumero: str, maa: str):
        self.__nimi = nimi
        self.__puhelinnumero = puhelinnumero
        self.__maa = maa

    @property
    def puhelinnumero(self):
        # Puhelinnumerosta jää etunolla pois, kun maatunnus lisätään alkuun
        return Puhelinnumero.maatunnukset[self.__maa] + " " + self.__puhelinnumero[1:]
```

```python
paulan_nro = Puhelinnumero("Paula Pythonen", "050 1234 567", "Suomi")
print(paulan_nro.puhelinnumero)
```

<sample-output>

+358 50 1234 567

</sample-output>

Varje TelefonNummer-objekt innehåller namnet på ägaren, själva numret och det land där telefonnumret finns. När attributet som innehåller telefonnumret nås med getter-metoden hämtas lämplig landskod från klassvariabelns ordbok baserat på landattributet, och resultatet prefixeras till numret.

Implementeringsexemplet ovan är inte särskilt funktionellt i övrigt. I följande exempel har vi lagt till getter och sättare för alla attribut:

```python
class Puhelinnumero:
    maatunnukset = {"Suomi": "+358", "Ruotsi": "+46", "Yhdysvallat": "+1"}

    def __init__(self, nimi: str, puhelinnumero: str, maa: str):
        self.__nimi = nimi
        # Tämä kutsuu metodia puhelinnumero.setter
        self.puhelinnumero = puhelinnumero
        # Tämä kutsuu metodia maa.setter
        self.maa = maa

    # Havainnointimetodissa yhdistetään maatunnus ja puhelinnumero
    @property
    def puhelinnumero(self):
        # Puhelinnumerosta jää etunolla pois, kun maatunnus lisätään alkuun
        return Puhelinnumero.maatunnukset[self.__maa] + " " + self.__puhelinnumero[1:]

    @puhelinnumero.setter
    def puhelinnumero(self, numero):
        # Varmistetaan, että puhelinnumerossa on vain numeroita ja välilyöntejä
        for merkki in numero:
            if merkki not in "1234567890 ":
                raise ValueError("Puhelinnumero saa sisältää vain lukuja ja välilyöntejä")
        self.__puhelinnumero = numero

    # Pelkkä puhelinnumero ilman maatunnusta
    @property
    def paikallinen_numero(self):
        return self.__puhelinnumero

    @property
    def maa(self):
        return self.__maa

    @maa.setter
    def maa(self, maa):
        # Varmistetaan, että maa on maatunnusten listalla
        if maa not in Puhelinnumero.maatunnukset:
            raise ValueError("Annettua maata ei löydy listalta.")
        self.__maa = maa

    @property
    def nimi(self):
        return self.__nimi

    @nimi.setter
    def nimi(self, nimi):
        self.__nimi = nimi

    def __str__(self):
        return f"{self.puhelinnumero} ({self.__nimi})"
```

```python
if __name__ == "__main__":
    pnro = Puhelinnumero("Pertti Python", "040 111 1111", "Ruotsi")
    print(pnro)
    print(pnro.puhelinnumero)
    print(pnro.paikallinen_numero)
```

<sample-output>

+46 40 111 1111 (Pertti Python)
+46 40 111 1111
040 111 1111

</sample-output>

<programming-exercise name='Postinumerot' tmcname='osa09-13_postinumerot'>

Tehtäväpohjassa on määritelty luokka `Kaupunki`, joka mallintaa yksittäistä kaupunkia.

Lisää luokkaan luokkamuuttuja postinumerot, joka viittaa sanakirjaan. Sanakirjassa jokainen avain on kaupungin nimi ja arvo postinumero. Molemmat ovat merkkijonoja.

Sanakirjasta tulee löytyä seuraavat postinumerot:

* Helsinki 00100
* Turku 20100
* Tampere 33100
* Jyväskylä 40100
* Oulu 90100

Muuta toiminnallisuutta ei tarvitse toteuttaa.

</programming-exercise>

## Klassmetoder

En klassmetod, även kallad statisk metod, är en metod som inte är knuten till någon enskild instans av klassen. En klassmetod kan anropas utan att några instanser av klassen skapas.

Klassmetoder är vanligen verktyg som har något att göra med klassens syfte, men som är fristående i den meningen att det inte ska vara nödvändigt att skapa instanser av klassen för att kunna anropa dem. Klassmetoder är vanligtvis offentliga, så att de kan anropas både utanför klassen och inom klassen, inklusive inom instanser av klassen.

En klassmetod definieras med annotationen `@classmethod`. Den första parametern är alltid `cls`. Variabelnamnet `cls` liknar `self`-parametern. Skillnaden är att `cls` pekar på klassen medan `self` pekar på en instans av klassen. Ingen av parametrarna ingår i argumentlistan när funktionen anropas, utan Python fyller i lämpligt värde automatiskt.

I följande exempel har vi en klass som modellerar fordonsregistreringar. Klassen `Registration` innehåller en statisk metod för att kontrollera om en registreringsskylt är giltig. Metoden är en statisk klassmetod eftersom det är användbart att kunna kontrollera om en registreringsskylt är giltig redan innan ett enda Registration-objekt har skapats:

```python
class Rekisteriote:
    def __init__(self, omistaja: str, merkki: str, vuosi: int, rekisteritunnus: str):
        self.__omistaja = omistaja
        self.__merkki = merkki
        self.__vuosi = vuosi

        # Kutsutaan metodia rekisteritunnus.setter
        self.rekisteritunnus = rekisteritunnus

    @property
    def rekisteritunnus(self):
        return self.__rekisteritunnus

    @rekisteritunnus.setter
    def rekisteritunnus(self, tunnus):
        if Rekisteriote.rekisteritunnus_kelpaa(tunnus):
            self.__rekisteritunnus = tunnus
        else:
            raise ValueError("Rekisteritunnus ei kelpaa")

    # Luokkametodi tunnuksen validoimiseksi
    @classmethod
    def rekisteritunnus_kelpaa(cls, tunnus: str):
        if len(tunnus) < 3 or "-" not in tunnus:
            return False

        # Tarkastellaan alku- ja loppuosaa erikseen
        alku, loppu = tunnus.split("-")

        # Alkuosassa saa olla vain kirjaimia
        for merkki in alku:
            if merkki.lower() not in "abcdefghijklmnopqrstuvwxyzåäö":
                return False

        # Loppuosassa saa olla vain numeroita
        for merkki in loppu:
            if merkki not in "1234567890":
                return False

        return True
```

```python
ote = Rekisteriote("Arto Autoilija", "Volvo", "1992", "abc-123")

if Rekisteriote.rekisteritunnus_kelpaa("xyz-789"):
    print("Tämä on validi tunnus!")
```

<sample-output>

Tämä on validi tunnus!

</sample-output>

Giltigheten för en registreringsskylt kan kontrolleras även utan att skapa en enda instans av klassen, t.ex. med `Registration.nummer_plat_giltig("xyz-789")`. Samma metod anropas i klassens konstruktor. OBS: även inom konstruktören är denna metod åtkomlig via klassens namn, inte `self`! 

<programming-exercise name='Lista-apuri' tmcname='osa09-14_lista_apuri'>

Kirjoita luokka `ListaApuri`, jossa on seuraavat kaksi luokkametodia:

* Metodi `suurin_frekvenssi(lista: list)` palauttaa alkion, jota esiintyy annetussa listassa eniten
* Metodi `tuplia(lista: list)` palauttaa sellaisten alkioden lukumäärän, jotka esiintyvät listassa vähintään kahdesti

Metodeja tulee voida käyttää ilman, että luokasta luodaan oliota. Esimerkki luokan käytöstä:

```python
luvut = [1, 1, 2, 1, 3, 3, 4, 5, 5, 5, 6, 5, 5, 5]
print(ListaApuri.suurin_frekvenssi(luvut))
print(ListaApuri.tuplia(luvut))
```

<sample-output>

5
3

</sample-output>

</progarmming-exercise>
