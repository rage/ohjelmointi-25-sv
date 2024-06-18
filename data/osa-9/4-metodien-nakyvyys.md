---
path: '/osa-9/4-metodien-nakyvyys'
title: 'Metodernas räckvidd'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Vet du hur du kan begränsa synligheten för en metod i Python
- Kommer du att kunna skriva privata metoder

</text-box>

De metoder som definieras inom en klass kan döljas på exakt samma sätt som attributen i föregående avsnitt. Om metoden börjar med två understreck `__` är den inte direkt åtkomlig för klienten.

Tekniken är alltså densamma för både metoder och attribut, men användningsfallen är oftast lite annorlunda. Privata attribut kommer ofta tillsammans med getter- och sättar-metoder för att kontrollera åtkomsten till dem. Privata metoder å andra sidan är vanligtvis endast avsedda för internt bruk, som hjälpmetoder för processer som klienten inte behöver känna till.

En privat metod kan användas inom klassen precis som vilken annan metod som helst, men man måste naturligtvis komma ihåg att inkludera `self`-prefixet. Följande är en enkel klass som representerar mottagaren av e-postbrev. Den innehåller en privat hjälpmetod för att kontrollera att e-postadressen är i ett giltigt format:

```python
class Mottagare:
    def __init__(self, namn: str, epost: str):
        self.__namn = namn
        if self.__granska_epost(epost):
            self.__epost = epost
        else:
            raise ValueError("Eposten duger inte")

    def __granska_epost(self, epost: str):
        # En enkel granksning: adressen måste vara över 5 symboler lång och innehålla en punkt och en @-symbol
        return len(epost) > 5 and "." in epost and "@" in epost
```

Försök att kalla den privata metoden direkt orsakar ett fel:

```python
petter = Mottagare("Petter Keinonen", "petter@example.com")
petter.__granska_epost("naganannan@example.com")
```

<sample-output>

AttributeError: 'Mottagare' object has no attribute '__granska_epost'

</sample-output>

Inom klassen kan metoden användas på normalt sätt, och det är vettigt att använda den även för att ange ett nytt värde för adressen. Låt oss lägga till getter- och sättar-metoder för e-postadressen:

```python
class Mottagare:
    def __init__(self, namn: str, epost: str):
        self.__namn = namn
        if self.__granska_epost(epost):
            self.__epost = epost
        else:
            raise ValueError("Eposten duger inte")

    def __granska_epost(self, epost: str):
        # En enkel granksning: adressen måste vara över 5 symboler lång och innehålla en punkt och en @-symbol
        return len(epost) > 5 and "." in epost and "@" in epost

    @property
    def epost(self):
        return self.__epost

    @epost.setter
    def epost(self, epost: str):
        if self.__granska_epost(epost):
            self.__epost = epost
        else:
            raise ValueError("Eposten duger inte")
```

I följande exempel är klassen `Kortlek` en modell för en kortlek med 52 kort. Den innehåller hjälpmetoden `__aterstall_kortlek`, som skapar en ny blandad kortlek. Den privata metoden anropas för närvarande endast i konstruktörsmetoden, så implementationen skulle kunna placeras direkt i konstruktören. Att använda en separat metod gör dock koden mer lättläst och gör det också möjligt att komma åt funktionaliteten senare i andra metoder om det behövs.

```python
from random import shuffle

class Kortlek:
    def __init__(self):
        self.__aterstall_kortlek()

    def __aterstall_kortlek(self):
        self.__packe = []
        # Vi lägger alla korten i packen
        sviter = ["spader", "hjarter", "klover", "ruter"]
        for svit in sviter:
            for nummer in range(1, 14):
                self.__packe.append((svit, nummer))
        # Blanda packen
        shuffle(self.__packe)

    def dela(self, kortens_antal: int):
        hand = []
        # Flytta korten på toppen av packen till handen
        for i in range(kortens_antal):
            hand.append(self.__packe.pop())
        return hand
```

Låt oss testa klassen:

```python
kortlek = Kortlek()
hand1 = kortlek.dela(5)
print(hand1)
hand2 = kortlek.dela(5)
print(hand2)
```

Eftersom händerna är slumpmässigt genererade, är följande endast ett exempel av det som kunde utskrivas:

<sample-output>

[('spader', 7), ('spader', 11), ('hjarter', 7), ('ruter', 3), ('spader', 4)]
[('klover', 8), ('spader', 12), ('ruter', 13), ('klover', 11), ('spader', 10)]

</sample-output>

Privata metoder är i allmänhet mindre vanliga än privata attribut. En tumregel är att en metod ska döljas när klienten inte har något behov av att direkt komma åt den. Detta är särskilt fallet när det är möjligt att klienten kan påverka objektets integritet negativt genom att anropa metoden. 

<programming-exercise name='Palvelumaksu' tmcname='osa09-12_palvelumaksu'>

Skapa en klass `Bankkonto`, som modellerar ett bankkonto. Klassen ska innehålla

* en konstruktor, som får som argument namnet på ägaren (str), kontonumret (str) och saldot (float)
* metoden `insattning(summa: float)`, som sätter till pengar på kontot
* metoden `uttag(summa: float)`, som tar ut pengar från kontot
* gettermetoden `saldo`, som returnerar kontots saldo

Klassen ska också innehålla en privat metod

* `__service_avgift()`, som minskar saldot på kontot med en procent. När någon av metoderna `insattning` eller `uttag` anropas bör även denna metod anropas. Serviceavgiften beräknas och subtraheras först efter att den faktiska åtgärden har slutförts (det vill säga efter att det angivna beloppet har lagts till eller subtraherats från saldot).

Alla dataattribut inom klassdefinitionen ska vara privata.

Exempel på användning av klassen:

```python
konto = Bankkonto("Ragnar Rikedom", "12345-6789", 1000)
konto.uttag(100)
print(konto.saldo)
konto.tillsatt(100)
print(konto.saldo)

```

<sample-output>

891.0
981.09

</sample-output>


</programming-exercise>
