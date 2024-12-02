---
path: '/osa-8/2-klasser-och-objekt'
title: 'Klasser och objekt'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter detta avsnitt

- Vet du vad en klass är
- Kommer du att förstå vad kopplingen mellan en klass och ett objekt är
- Kommer du att veta vad som menas med objektorienterad programmering

</text-box>

I föregående avsnitt arbetade vi med listor, tupler, ordlistor och strängar. Dessa är alla ganska speciella fall i Python-programmering. Pythons syntax har en unik, fördefinierad metod för att skapa ett objekt som tillhör var och en av dessa typer:

```python
# Listor deklareras med hakparenteser
lista = [1,2,3]

# Strängar deklareras med citationstecken
strang = "Hej alla!"

# Ordlistor deklareras med klammerparenteser
ordlista = {"ett": 1, "två:": 2}

# tuplar deklareras med parenteser
tupel = (1,2,3)
```

När någon annan typ av objekt deklareras måste vi anropa en speciell initialiseringsfunktion som kallas konstruktor. Låt oss ta en titt på hur man arbetar med bråk med hjälp av `Fraction`-klassen.

```python
# vi använder klassen Fraction från modulen fractions
from fractions import Fraction

# vi skapar några nya bråktal
halv = Fraction(1,2)

tredjedel = Fraction(1,3)

tredje = Fraction(3,11)

# vi skriver ut
print(halv)
print(tredjedel)
print(tredje)

# vi kan också räkna med bråk
print(halv + tredjedel)
```

<sample-output>

1/2
1/3
3/11
5/6

</sample-output>

Metodanrop för konstruktorer ser alltså lite annorlunda ut än de vanliga metodanrop som vi har stött på tidigare. För det första är de inte kopplade till något objekt med punktnotation (eftersom konstruktoranropet behövs för att skapa ett objekt i första hand). Dessutom skrivs konstruktorsmetoden med stor bokstav: `[half = Fraction(1,2)]`. Låt oss titta närmare på hur objekt konstrueras genom att bekanta oss med begreppet klass.

## En klass är ritningen på ett objekt

Vi har redan använt termen klass i materialet många gånger. I exemplet ovan importerade vi t.ex. klassen `Fraction` från modulen `fractions`. Vi skapade nya bråktalsobjekt genom att anropa konstruktorsmetoden för klassen `Fraction`.

En klassdefinition innehåller strukturen och funktionaliteterna för alla objekt som representerar den givna klassen. Därför kallas klasser ibland för objektens ritningar. En klassdefinition berättar alltså för oss vilken typ av data ett objekt innehåller och definierar de metoder som kan användas på objektet. Objektorienterad programmering är ett programmeringsparadigm där programmets funktionalitet är knuten till användningen av klasser, och de objekt som skapas utgående från de olika klasserna. 

En klassdefinition kan användas för att skapa flera objekt. Som tidigare nämnts är objekt oberoende av varandra. Ändringar som görs i ett objekt påverkar i allmänhet inte de andra objekten som hör till samma klass. Varje objekt har sin egen unika uppsättning av variabler. Det kan vara bra att tänka på denna förenkling av förhållandet mellan klass och objekt:

* En klass definierar variablerna
* När ett objekt skapas tilldelas dessa variabler värden

Vi kan alltså använda ett objekt av typen `Fraction` för att komma åt täljaren och nämnaren i ett bråktal:

```python
from fractions import Fraction

tal = Fraction(2,5)

# Skriv ut täljaren
print(tal.numerator)

# ... och sedan nämnaren
print(tal.denominator)
```

<sample-output>

2
5

</sample-output>

Klassdefinitionen för `Fraction` innehåller deklarationer för variablerna `numerator` och `denominator`. Varje objekt som skapas baserat på klassen kommer att ha sina egna specifika värden på dessa variabler.

På samma sätt innehåller objekt som skapats baserat på klassen `date` sina egna unika värden för datumets år, månad och dag:

```python
from datetime import date

jul = date(2020, 12, 24)
midsommar = date(2020, 6, 20)

# Vi skriver ut bägges månad
print(jul.month)
print(midsommar.month)
```

<sample-output>

12
6

</sample-output>

Definitionen av klassen `date` innehåller deklarationer av variablerna `year`, `month` och `day`. När ett nytt datumobjekt skapas baserat på klassen tilldelas dessa variabler värden. Varje objekt har sina egna unika värden utgående från de tilldelade värdena.

## Funktioner som arbetar med objekt

Att skicka ett objekt som ett argument till en funktion borde vara bekant vid det här laget eftersom vi redan har gjort det många gånger i den här kursen. Låt oss ta en titt på följande exempel. Här har vi en funktion som kontrollerar om `date`-objektet som skickas som argument infaller på en helg:

```python
def redan_veckoslut(dag: date):
    veckodag = dag.isoweekday()
    return veckodag == 6 or veckodag == 7
```

Denna funktion använder metoden [isoweekday](https://docs.python.org/3/library/datetime.html#datetime.date.isoweekday), som definieras i klassdefinitionen för klassen `date`, och returnerar ett heltalsvärde enligt följande: om det angivna datumet är en måndag returnerar den 1, och om det är en tisdag returnerar den 2, och så vidare.

```python
jul = date(2020, 12, 24)
midsommar = date(2020, 6, 20)

print(redan_veckoslut(jul))
print(redan_veckoslut(midsommar))
```

<sample-output>

False
True

</sample-output>

## Metoder vs variabler

När du arbetar med ett objekt av typen `date` kanske du märker att det finns en liten skillnad mellan hur man kommer åt variablerna i objektet jämfört med hur man anropar objektets metoder: 

```python
dag = date(2020, 12, 24)

# vi anropar metoden
veckodag = dag.isoweekday()

# vi använder en variabel
manad = dag.month

print("Veckodag:", veckodag)
print("Månad:", kuukausi)
```

<sample-output>

Veckodag: 4
Månad: 12

</sample-output>

Veckodagen som datumet infaller på är tillgänglig via metoden `isoweekday`:

```python
veckodag = dag.isoweekday()
```

Detta är ett metodanrop, alltså finns det parenteser efter namnet på metoden. Om du lämnar bort parenteserna uppstår inget fel, men resultatet blir konstigt:

```python
veckodag =  dag.isoweekday
print("Veckodag:", veckodag)
```

<sample-output>

Veckodag: <built-in method isoweekday of datetime.date object at 0x10ed66450>

</sample-output>

Månaden för ett date-objekt är en variabel, alltså kan man komma åt det tilldelade värdet med en referens.

```python
manad = dag.month
```

Lägg märke till att det inte finns parenteser här. Att sätta in parenteser skulle orsaka ett fel, eftersom det inte är frågan om en metod:

```python
manad = dag.month()
```

<sample-output>

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'int' object is not callable

</sample-output>

<programming-exercise name='Lista år' tmcname='osa08-03_lista_ar'>

Skapa funktionen `lista_ar(datum: list)`, som får en lista med `date`-objekt som argument. Funktionen returnerar en ny lista, som innehåller _åren i den originella listan i kronologisk ordning_, från tidigast till äldst.

Ett exempel:

```python
dag1 = date(2019, 2, 3)
dag2 = date(2006, 10, 10)
dag3 = date(1993, 5, 9)

ar = lista_ar([dag1, dag2, dag3])
print(ar)
```

<sample-output>

[1993, 2006, 2019]

</sample-output>

</programming-exercise>


<programming-exercise name='Affarslista' tmcname='osa08-04_affarslista'>

I denna övningsbotten finns en färdigt definierad `Affarslista`-klass, som kan användas för att modellera en affärslista.

Anta nu att vi har ett `Affarslista`-objekt som refereras till i en variabel med namnet affarslista. Då kan vi hantera objektet med följande metoder:

```python

print(affarslista.mangden_foremal())
print(affarslista.foremal(1))
print(affarslista.mangd(1))
print(affarslista.foremal(2))
print(affarslista.mangd(2))

```

<sample-output>

2
Bananer
4
Mjölk
1

</sample-output>

Även följande går:

```python
# Föremålen på affärslistan är indexerade från 1
for i in range(1, affarslista.mangden_foremal()+1):
    foremal = affarslista.foremal(i)
    mangd = affarslista.mangd(i)
    print(f"{foremal}: {mangd} st")
```


<sample-output>

Bananer 4 st
Mjölk 1 st

</sample-output>

Som du kan se fungerar en `Affarslista` ungefär som en vanlig lista, men den nås via de metoder som tillhandahålls av Affarslista-klassen. Till skillnad från vanliga Python-listor börjar indexeringen från 1, inte 0.

Skapa en funktion med namnet `totala_mangd(lista: Affarslista)`, som tar ett objekt av typen `Affarslista` som sitt argument. Funktionen ska beräkna det totala antalet enheter i listan och returnera värdet.

Du kan använda följande kod för att testa din funktion:

```python
if __name__ == "__main__":
    lista = Affarslista()
    lista.tillagg("banaaner", 10)
    lista.tillagg("appel", 5)
    lista.tillagg("ananas", 1)

    print(totala_mangd(lista))
```

<sample-output>

16

</sample-output>

**OBS:** Definitionen av klassen Affarslista ingår redan i övningsmallen. Du behöver inte använda en `import`-sats för att importera den, till skillnad från i exemplen ovan med Python standardbiblioteksklasserna `Fraction` och `date`.

</programming-exercise>
