---
path: '/osa-8/2-luokat-ja-oliot'
title: 'Klasser och objekt'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter detta avsnitt

- Vet du vad en klass är
- Kommer du att förstå vad kopplingen mellan en klass och ett objekt är
- Kommer du att veta vad som menas med objektorienterad programmering

</text-box>

I föregående avsnitt arbetade vi med listor, tupler, ordlistor och strängar. Dessa är alla ganska speciella fall i Python-programmering. Pythons syntax har en unik, fördefinierad metod för att deklarera ett objekt som tillhör var och en av dessa typer:

```python
# Lista luodaan antamalla arvot hakasuluissa
lista = [1,2,3]

# Merkkijonovakio tunnistetaan lainausmerkeistä
mjono = "Moi kaikki!"

# Sanakirja luodaan aaltosulkeilla
sanakirja = {"yksi": 1, "kaksi:": 2}

# Tuplessa arvot ovat sulkeissa
oma_tuple = (1,2,3)
```

När någon annan typ av objekt deklareras måste vi anropa en speciell initialiseringsfunktion som kallas konstruktor. Låt oss ta en titt på hur man arbetar med bråk genom Fraction-klassen.

```python
# Tuodaan käyttöön luokka Fraction modulista fractions
from fractions import Fraction

# Luodaan pari uutta murtolukuoliota
puolikas = Fraction(1,2)

kolmasosa = Fraction(1,3)

kolmas = Fraction(3,11)

# Tulostetaan
print(puolikas)
print(kolmasosa)
print(kolmas)

# Murtoluvuilla voi myös laskea
print(puolikas + kolmasosa)
```

<sample-output>

1/2
1/3
3/11
5/6

</sample-output>

Som du kan se ovan, ser metodkallningar för konstruktorer lite annorlunda ut än de normala metodkallningar som vi har stött på tidigare. För det första är de inte kopplade till något objekt med punktnotationen (eftersom konstruktoranropet behövs för att skapa ett objekt i första hand). Konstruktorsmetoden skrivs också med stor bokstav: `[half = Fraction(1,2)]`. Låt oss titta närmare på hur objekt konstrueras genom att bekanta oss med begreppet klass.

## En klass är ritningen till ett objekt

Vi har redan använt termen klass i materialet många gånger. I exemplet ovan importerade vi t.ex. klassen `Fraction` från modulen `fractions`. Nya bråktalsobjekt skapades genom att kalla på konstruktorsmetoden för klassen `Fraction`.

En klassdefinition innehåller strukturen och funktionaliteterna för alla objekt som representerar den. Därför kallas klasser ibland till objektens ritningar. En klassdefinition berättar alltså till oss vilken typ av data ett objekt innehåller och definierar de metoder som kan användas på objektet. Objektorienterad programmering är ett programmeringsparadigm där programmets funktionalitet är knuten till användningen av klasser och objekt som skapas baserat på dessa.

En klassdefinition kan användas för att skapa flera objekt. Som tidigare nämnts är objekt oberoende av varandra. Ändringar som görs till ett objekt påverkar i allmänhet inte de andra objekten som är samma klass. Varje objekt har sin egen unika uppsättning dataattribut. Det kan vara bra att tänka på denna förenkling av förhållandet mellan klass och objekt:

* En klass definierar variablerna
* när ett objekt skapas tilldelas dessa variabler värden

Vi kan alltså använda ett objekt av typen `Fraction` för att komma åt täljaren och nämnaren i ett bråktal:

```python
from fractions import Fraction

luku = Fraction(2,5)

# Tulostetaan osoittaja
print(luku.numerator)

# ...ja sitten nimittäjä
print(luku.denominator)
```

<sample-output>

2
5

</sample-output>

Klassdefinitionen för `Fraction` innehåller deklarationer för variablerna `numerator` och `denominator`. Varje objekt som skapas baserat på klassen har sina egna specifika värden som tilldelas dessa variabler.

På samma sätt innehåller objekt som skapats baserat på klassen `date` sina egna unika värden för datumets år, månad och dag:

```python
from datetime import date

joulu = date(2020, 12, 24)
juhannus = date(2020, 6, 20)

# Tulostetaan kuukaudet molemmista
print(joulu.month)
print(juhannus.month)
```

<sample-output>

12
6

</sample-output>

Definitionen av klassen `date` innehåller deklarationer av variablerna `year`, `month` och `day`. När ett nytt datumobjekt skapas baserat på klassen tilldelas dessa variabler värden. Varje objekt har sina egna unika värden som tilldelas dessa variabler.

## Funktioner som arbetar med objekt

Att passera ett objekt som ett argument till en funktion borde vara bekant för dig vid det här laget eftersom vi har gjort det redan många gånger i den här kursen. Låt oss ta en titt på följande exempel. Här har vi en funktion som kontrollerar om `date`-objektet som passeras som argument infaller på en helg:

```python
def onko_viikonloppu(paiva: date):
    viikonpaiva = paiva.isoweekday()
    return viikonpaiva == 6 or viikonpaiva == 7
```

Denna funktion använder metoden [isoweekday](https://docs.python.org/3/library/datetime.html#datetime.date.isoweekday), som definieras i klassdefinitionen för klassen date, och returnerar ett heltalsvärde på det sättet att om det angivna datumet är en måndag returnerar den 1, och om det är en tisdag returnerar den 2, och så vidare.

```python
joulu = date(2020, 12, 24)
juhannus = date(2020, 6, 20)

print(onko_viikonloppu(joulu))
print(onko_viikonloppu(juhannus))
```

<sample-output>

False
True

</sample-output>

## Metoder vs variabler

När du arbetar med ett objekt av typen `date` kanske du märker att det finns en liten skillnad mellan hur variablerna i objektet åtkoms jämfört med hur metoderna som är kopplade till objekten åtkoms:

```python
paiva = date(2020, 12, 24)

# kutsutaan metodia
viikonpaiva = paiva.isoweekday()

# viitataan olion muuttujaan
kuukausi = paiva.month

print("Viikonpäivä:", viikonpaiva)
print("Kuukausi:", kuukausi)
```

<sample-output>

Viikonpäivä: 4
Kuukausi: 12

</sample-output>

Veckodagen som datumet infaller på är tillgänglig via metoden isoweekday:

```python
viikonpaiva = paiva.isoweekday()
```

Detta är en metodkallelse, alltså finns det parenteser efter namnet på metoden. Om du lämnar bort parenteserna uppstår det inte något fel, men resultatet blir konstigt:

```python
viikonpaiva =  paiva.isoweekday
print("Viikonpäivä:", viikonpaiva)
```

<sample-output>

Viikonpäivä: <built-in method isoweekday of datetime.date object at 0x10ed66450>

</sample-output>

Månaden av ett date-objekt är en variabel, alltså kan det tillgivna värdet kommas åt med en referens.

```python
kuukausi = paiva.month
```

Lägg märke till att det inte finns parenteser här. Att sätta in parenteser skulle orsaka ett fel:

```python
kuukausi = paiva.month()
```

<sample-output>

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'int' object is not callable

</sample-output>

<programming-exercise name='Vuodet listaan' tmcname='osa08-03_vuodet_listaan'>

Tee funktio `vuodet_listaan(paivamaarat: list)`, joka saa parametrikseen listan, joka sisältää `date`-tyyppisiä olioita. Funktio palauttaa uuden listan, jossa on päivämäärien _vuodet suuruusjärjestyksessä pienimmästä suurimpaan_.

Esimerkki funktion kutsumisesta:

```python
paiva1 = date(2019, 2, 3)
paiva2 = date(2006, 10, 10)
paiva3 = date(1993, 5, 9)

vuodet = vuodet_listaan([paiva1, paiva2, paiva3])
print(vuodet)
```

<sample-output>

[1993, 2006, 2019]

</sample-output>

</programming-exercise>


<programming-exercise name='Kauppalista' tmcname='osa08-04_kauppalista'>

Tehtäväpohjassa on määritelty valmiiksi `Kauppalista`-luokka, jolla voidaan mallintaa yhtä kauppalistaa.

Jos kauppalistaolio on tallennettu esimerkiksi muuttujaan `kauppalista`, sitä voidaan käsitellä seuraavan esimerkin mukaisesti:

```python

print(kauppalista.tuotteita())
print(kauppalista.tuote(1))
print(kauppalista.maara(1))
print(kauppalista.tuote(2))
print(kauppalista.maara(2))

```

<sample-output>

2
Banaanit
4
Maito
1

</sample-output>

Myös seuraava onnistuu:

```python
# kauppalistalla tuotteet on indeksöity ykkösestä alkaen
for i in range(1, kauppalista.tuotteita()+1):
    tuote = kauppalista.tuote(i)
    maara = kauppalista.maara(i)
    print(f"{tuote}: {maara} kpl")
```


<sample-output>

banaanit 4 kpl
maito 1 kpl

</sample-output>

Kauppalistat siis käyttäytyvät hieman listojen tavoin, mutta niitä käsitellään kuitenkin kauppalistan tarjoamien metodien kautta. Toisin kuin listoissa, kauppalistan tuotteet on numeroitu ykkösestä alkaen.

Tee esimerkkejä hyödyntäen funktio `tuotteita_yhteensa(lista: Kauppalista)`, joka saa parametrikseen `Kauppalista`-tyyppisen olion. Funktio laskee listalla yhteensä olevien tuotteiden määrän ja palauttaa sen.

Huomaa, että kauppalistalla tuotteet indeksoidaan ykkösestä alkaen, ei nollasta. Voit testata ohjelmaasi esim. tällä esimerkkikoodilla:

```python
if __name__ == "__main__":
    lista = Kauppalista()
    lista.lisaa("banaanit", 10)
    lista.lisaa("omenat", 5)
    lista.lisaa("ananas", 1)

    print(tuotteita_yhteensa(lista))
```

<sample-output>

16

</sample-output>

**Huom** koska luokan `Kauppalista` koodi on tehtäväpohjassa valmiina, ei koodissa tarvitse käyttää `import`-lausetta kuten edellisissä esimerkeissä, tehtävissä, jotka käyttävät Pythonin valmiita luokkia `Fraction` ja `date`.

</programming-exercise>
