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
class Vastaanottaja:
    def __init__(self, nimi: str, sposti: str):
        self.__nimi = nimi
        if self.__tarkasta_sposti(sposti):
            self.__sposti = sposti
        else:
            raise ValueError("Sähköposti ei kelpaa")

    def __tarkasta_sposti(self, sposti: str):
        # Yksinkertainen tarkastus: osoitteessa on yli 5 merkkiä ja piste ja @-merkki
        return len(sposti) > 5 and "." in sposti and "@" in sposti
```

Försök att kalla den privata metoden direkt orsakar ett fel:

```python
pertti = Vastaanottaja("Pertti Keinonen", "pertti@example.com")
pertti.__tarkasta_sposti("jokumuu@example.com")
```

<sample-output>

AttributeError: 'Vastaanottaja' object has no attribute '__tarkasta_sposti'

</sample-output>

Inom klassen kan metoden användas på normalt sätt, och det är vettigt att använda den även för att ange ett nytt värde för adressen. Låt oss lägga till getter- och sätter-metoder för e-postadressen:

```python
class Vastaanottaja:
    def __init__(self, nimi: str, sposti: str):
        self.__nimi = nimi
        if self.__tarkasta_sposti(sposti):
            self.__sposti = sposti
        else:
            raise ValueError("Sähköposti ei kelpaa")

    def __tarkasta_sposti(self, sposti: str):
        # Yksinkertainen tarkastus: osoitteessa on yli 5 merkkiä ja piste ja @-merkki
        return len(sposti) > 5 and "." in sposti and "@" in sposti

    @property
    def sposti(self):
        return self.__sposti

    @sposti.setter
    def sposti(self, sposti: str):
        if self.__tarkasta_sposti(sposti):
            self.__sposti = sposti
        else:
            raise ValueError("Sähköposti ei kelpaa")
```

I följande exempel är klassen `Kortlek` en modell för en kortlek med 52 kort. Den innehåller hjälpmetoden `__återställ_kortlek`, som skapar en ny blandad kortlek. Den privata metoden anropas för närvarande endast i konstruktörsmetoden, så implementationen skulle kunna placeras direkt i konstruktören. Att använda en separat metod gör dock koden mer lättläst och gör det också möjligt att komma åt funktionaliteten senare i andra metoder om det behövs.

```python
from random import shuffle

class Korttipakka:
    def __init__(self):
        self.__alusta_pakka()

    def __alusta_pakka(self):
        self.__pakka = []
        # Laitetaan kaikki kortit pakkaan
        maat = ["pata", "hertta", "risti", "ruutu"]
        for maa in maat:
            for numero in range(1, 14):
                self.__pakka.append((maa, numero))
        # Sekoitetaan pakka
        shuffle(self.__pakka)

    def jaa(self, korttien_maara: int):
        kasi = []
        # Siirretään pakasta ylimmät kortit käteen
        for i in range(korttien_maara):
            kasi.append(self.__pakka.pop())
        return kasi
```

Låt oss testa klassen:

```python
korttipakka = Korttipakka()
kasi1 = korttipakka.jaa(5)
print(kasi1)
kasi2 = korttipakka.jaa(5)
print(kasi2)
```

Eftersom händerna är slumpmässigt genererade, är följande endast ett exempel av det som kunde utskrivas:

<sample-output>

[('pata', 7), ('pata', 11), ('hertta', 7), ('ruutu', 3), ('pata', 4)]
[('risti', 8), ('pata', 12), ('ruutu', 13), ('risti', 11), ('pata', 10)]

</sample-output>

Privata metoder är i allmänhet mindre vanliga än privata attribut. En tumregel är att en metod ska döljas när klienten inte har något behov av att direkt komma åt den. Detta är särskilt fallet när det är möjligt att klienten kan påverka objektets integritet negativt genom att anropa metoden. 

<programming-exercise name='Palvelumaksu' tmcname='osa09-12_palvelumaksu'>

Kirjoita luokka `Pankkitili`, joka mallintaa pankkitiliä. Luokalla tulee olla

* konstruktori, joka saa parametrikseen tilinomistajan (str), tilinumeron (str) ja saldon (float)
* metodi `talleta(summa: float)`, jolla tilille voidaan tallettaa rahaa
* metodi `nosta(summa: float)`, joka nostaa tililtä rahasumman
* havainnointimetodi `saldo`, joka palauttaa tilin saldon

Lisäksi luokalla on yksityinen metodi

* `__palvelumaksu()`, joka vähentää tililtä yhden prosentin rahaa. Luokassa kutsutaan tätä metodia aina, kun asiakas kutsuu jompaa kumpaa metodeista `talleta` tai `nosta`. Prosentti vähennetään aina varsinaisen operaation jälkeen (eli. esimerkiksi vasta sitten, kun rahat on talletettu).

Kaikki luokan attribuutit ovat yksityisiä.

Esimerkki luokan käytöstä:

```python
tili = Pankkitili("Raimo Rahakas", "12345-6789", 1000)
tili.nosta(100)
print(tili.saldo)
tili.talleta(100)
print(tili.saldo)

```

<sample-output>

891.0
981.09

</sample-output>


</programming-exercise>
