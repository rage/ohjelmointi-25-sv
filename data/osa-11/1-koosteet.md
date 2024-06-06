---
path: '/osa-11/1-koosteet'
title: 'List comprehension'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Vet du vad list comprehension är
- Kommer du att kunna använda list comprehensions för att skapa nya listor

</text-box>

En av de situationer där programmering är som mest kraftfull är vid bearbetning av sekvenser av objekt och händelser. Datorer är bra på att upprepa saker. I de tidigare delarna av det här materialet har vi till exempel itererat strängar, listor och ordlistor på olika sätt.

Låt oss anta att vi har en lista med heltal och att vi skulle behöva samma lista med objekt i strängformat. Ett traditionellt sätt att utföra uppgiften skulle kunna se ut så här:

```python
luvut = [1, 2, 3, 6, 5, 4, 7]

merkkijonot = []
for luku in luvut:
    merkkijonot.append(str(luku))
```

## List comprehension

Det finns också ett mer "pythoniskt" sätt att generera listor från befintliga listor. Dessa kallas list comprehensions.

Tanken är att på en enda rad få plats med både beskrivningen av vad som ska göras med varje objekt i listan och tilldelningen av resultatet till en ny lista.

I exemplet ovan var operationen som utfördes på varje objekt i listan mycket enkel: varje heltal omvandlades till en sträng. Låt oss se hur detta skulle se ut implementerat med en list comprehension:

```python
luvut = [1, 2, 3, 6, 5, 4, 7]
merkkijonot = [str(luku) for luku in luvut]
```

Den andra raden ovan innehåller många av samma element som den mer traditionella iterativa metoden, men syntaxen är annorlunda. Ett sätt att generalisera en list comprehension skulle kunna vara

`[<uttryck> for <föremål> in <serie>]`

Hakparenteserna runt list comprehensionsatsen signalerar till Python att resultatet ska vara en ny lista. En efter en bearbetas varje objekt i den ursprungliga listan och resultatet lagras i den nya listan, precis som i det iterativa tillvägagångssättet ovan. Som resultat har vi en ny lista med exakt lika många objekt som i originalet, och alla objekt har behandlats på ett identiskt sätt.

(OBS: originalen till bilderna i denna del saknas tillfälligt, vilket är anledningen till att det finns en del finskt vokabulär i illustrationerna i denna del. Vi arbetar på att åtgärda detta).

<img src="11_1_2.png">

List comprehensions kan också hantera mycket mer komplicerade operationer. Vi kan utföra beräkningar, till exempel multiplicera de ursprungliga objekten med tio:

```python
luvut = list(range(1,10))
print(luvut)

luvut_kerrottuna = [luku * 10 for luku in luvut]
print(luvut_kerrottuna)
```

<sample-output>

[1, 2, 3, 4, 5, 6, 7, 8, 9]
[10, 20, 30, 40, 50, 60, 70, 80, 90]

</sample-output>

Faktum är att uttrycket i list comprehension-satsen kan vara vilket Python-uttryck som helst. Du kan till och med anropa funktioner som du själv har definierat:

```python
def kertoma(n: int):
    """ Funktio laskee positiivisen luvun n kertoman n! """
    k = 1
    while n >= 2:
        k *= n
        n -= 1
    return k

if __name__ == "__main__":
    lista = [5, 2, 4, 3, 0]
    kertomat = [kertoma(luku) for luku in lista]
    print(kertomat)
```

<sample-output>

[120, 2, 24, 6, 1]

</sample-output>

Med den mer välbekanta `for`-loopen skulle samma process kunna uttryckas så här:

```python

def kertoma(n: int):
    """ Funktio laskee positiivisen luvun n kertoman n! """
    k = 1
    while n >= 2:
        k *= n
        n -= 1
    return k

if __name__ == "__main__":
    lista = [5, 2, 4, 3, 0]
    kertomat = []
    for luku in lista:
        kertomat.append(kertoma(luku))
    print(kertomat)

```

List Comprehensions gör att vi kan uttrycka samma funktionalitet på ett mer konsekvent sätt, vanligtvis utan att förlora något av läsbarheten.

Vi kan också returnera en list comprehension-sats direkt från en funktion. Om vi behövde en funktion för att producera faktorialtal för listor med tal, skulle vi kunna göra det på ett mycket kortfattat sätt:

```python
def kertomat(luvut: list):
    return [kertoma(luku) for luku in luvut]
```

<programming-exercise name='Neliojuuret' tmcname='osa11-01_neliojuuret'>

Tee funktio `neliojuuret(luvut: list)`, joka saa parametriksi listan kokonaislukuja. Funktio palauttaa listan parametrina olevien lukujen neliöjuurista. Neliöjuuren laskemiseen löytyy sopiva funktio moduulista [math](https://docs.python.org/3/library/math.html)

Funktion tulee käyttää listakoostetta. Funktion maksimipituus on siis (mukaanlukien `def`-sanalla alkava otsikkorivi) kokonaisuudessaan kaksi riviä!

Funktio toimii seuraavasti:

```python
rivit = neliojuuret([1,2,3,4])
for rivi in rivit:
    print(rivi)
```

<sample-output>

1.0
1.4142135623730951
1.7320508075688772
2.0

</sample-output>

</programming-exercise>

<programming-exercise name='Tähtirivit' tmcname='osa11-02_tahtirivit'>

Tee funktio `tahtirivit(luvut: list)`, joka saa parametriksi listan kokonaislukuja. Funktio palauttaa listan, joka koostuu tähtiriveistä, joiden pituus vastaa parametrina olevan listan lukuja. Funktion tulee käyttää listakoostetta.

Funktion maksimipituus on siis (mukaanlukien `def`-sanalla alkava otsikkorivi) kokonaisuudessaan kaksi riviä!

Funktio toimii seuraavasti:

```python
rivit = tahtirivit([1,2,3,4])
for rivi in rivit:
    print(rivi)

print()

rivit = tahtirivit([4, 3, 2, 1, 10])
for rivi in rivit:
    print(rivi)
```

<sample-output>

<pre>
*
**
***
****

****
***
**
*
**********
</pre>

</sample-output>

</programming-exercise>

<programming-exercise name='Paras koetulos' tmcname='osa11-03_paras_koetulos'>

Tehtäväpohjassa on valmiina luokka `Koesuoritus`, jolla on seuraavat julkiset attribuutit:

* nimi
* arvosana1
* arvosana2
* arvosana3

Kirjoita funktio `parhaat_tulokset(suoritukset: list)`. Funktio saa parametrikseen listan koesuoritusolioita.

Funktio palauttaa listakoostetta käyttäen uuden listan, johon on tallennettu jokaisen suorituksen paras arvosana.

Funktion maksimipituus on siis (mukaanlukien def-sanalla alkava otsikkorivi) kokonaisuudessaan kaksi riviä!

Esimerkki suorituksesta:

```python
suoritus1 = Koesuoritus("Pekka",5,3,4)
suoritus2 = Koesuoritus("Pirjo",3,4,1)
suoritus3 = Koesuoritus("Paavo",2,1,3)
suoritukset = [suoritus1, suoritus2, suoritus3]
print(parhaat_tulokset(suoritukset))
```

<sample-output>

[5, 4, 3]

</sample-output>

</programming-exercise>

<programming-exercise name='Pituudet' tmcname='osa11-04_pituudet'>

Tee funktio `pituudet(listat: list)` joka saa parametriksi listan, joka sisältää listoja, jotka sisältävät kokonaislukuja. Funktio palauttaa listan, joka sisältää parametrina olevien listojen pituudet.

Funktio tulee toteuttaa listakoosteen avulla. Funktion maksimipituus on siis (mukaanlukien `def`-sanalla alkava otsikkorivi) kokonaisuudessaan kaksi riviä!

Funktio toimii seuraavasti

```python
listat = [[1,2,3,4,5], [324, -1, 31, 7],[]]
print(pituudet(listat))
```

<sample-output>

[5, 4, 0]

</sample-output>

</programming-exercise>


## Att filtrera föremål

I exemplen ovan var alla våra listor lika långa före och efter en list comprehension-operation. I varje fall användes alla föremål i den ursprungliga listan som grund för den nya listan. Men ibland behöver vi bara några av de ursprungliga föremålen. Hur kan detta åstadkommas?

En list comprehension-sats kan också innehålla ett villkor, så att vi kan kontrollera objekten mot villkoret och bara välja ut dem som matchar. Den allmänna syntaxen är enligt följande:

`[<uttryck> for <föremål> in <serie> if <boolskt uttryck>]`

Satsen ovan är i övrigt identisk med den allmänna form som introducerades i början av detta avsnitt, men nu finns det en if-sats i slutet. Endast de objekt från den ursprungliga listan för vilka det booleska uttrycket är sant används som grund för den nya listan.

I exemplet nedan väljer vi alla jämna objekt från den ursprungliga listan som bas för den nya listan. I själva verket bearbetas inte dessa objekt ytterligare på något sätt, utan de tilldelas den nya listan som de är:

```python
lista = [1, 1, 2, 3, 4, 6, 4, 5, 7, 10, 12, 3]

parilliset = [alkio for alkio in lista if alkio % 2 == 0]
print(parilliset)
```

<sample-output>

[2, 4, 6, 4, 10, 12]

</sample-output>

Uttrycket i list comprehension-satsen ovan är bara ett enkelt `foremal`, vilket innebär att inga operationer ska utföras på föremålen i listan. Uttrycket kan vara vilket Python-uttryck som helst, precis som i de tidigare exemplen. Följande list comprehension-sats tar till exempel alla jämna föremål i en lista, multiplicerar varje föremål med tio och lagrar resultatet i en ny lista:

```python
lista = [1, 1, 2, 3, 4, 6, 4, 5, 7, 10, 12, 3]

parilliset = [alkio * 10 for alkio in lista if alkio % 2 == 0]
print(parilliset)
```

<sample-output>

[20, 40, 60, 40, 100, 120]

</sample-output>

När du stöter på mer och mer komplicerade list comprehensions kan det vara bra att försöka läsa villkoret först. Föremålen bearbetas ändå bara om de klarar testet, så det är ofta vettigt att först ta reda på vilka objekt som klarar filtreringssteget. Ibland skulle uttrycket i en list comprehension-sats inte ens vara möjligt för alla föremål i den ursprungliga listan.

Till exempel är faktorialtal bara definierat för icke-negativa heltal. Om vi inte kan vara säkra på att en lista bara innehåller värden på noll eller högre, måste innehållet filtreras innan det skickas vidare till den faktorialfunktion som vi skapade tidigare:

```python
def kertoma(n: int):
    """ Funktio laskee positiivisen luvun n kertoman n! """
    k = 1
    while n >= 2:
        k *= n
        n -= 1
    return k

if __name__ == "__main__":
    lista = [-2, 3, -1, 4, -10, 5, 1]
    kertomat = [kertoma(luku) for luku in lista if luku > 0]
    print(kertomat)
```

<sample-output>

[6, 24, 120, 1]

</sample-output>

Som vi såg i vårt allra första exempel på list comprehension, där heltal omvandlades till strängar, behöver föremålen i den nya listan inte vara av samma typ som föremålen i den ursprungliga listan. Om vi fortsätter från faktorialexemplet ovan kan vi skapa en tupel från varje originella föremål och dess bearbetade motsvarighet och lagra dessa i en lista, vilket kombinerar allt vi har lärt oss hittills i en enda list comprehension-sats:

```python

def kertoma(n: int):
    """ Funktio laskee positiivisen luvun n kertoman n! """
    k = 1
    while n >= 2:
        k *= n
        n -= 1
    return k

if __name__ == "__main__":
    lista = [-2, 3, 2, 1, 4, -10, 5, 1, 6]
    kertomat = [(luku, kertoma(luku)) for luku in lista if luku > 0 and luku % 2 == 0]
    print(kertomat)

```

<sample-output>

[(2, 2), (4, 24), (6, 720)]

</sample-output>

Om vi plockar isär exemplet ovan har vi det booleska uttrycket `n > 0 and n % 2 == 0`. Detta innebär att endast föremål som är både positiva och delbara med två accepteras för vidare bearbetning från den ursprungliga listan.

Dessa positiva, jämna tal bearbetas sedan i tur och ordning till formatet `(n, faktorial(n))`. Detta är en tupel, där det första objektet är själva talet och det andra objektet är resultatet som returneras av faktorialfunktionen.

<programming-exercise name='Poista pienemmät' tmcname='osa11-05_poista_pienemmat'>

Kirjoita funktio `poista_pienemmat(luvut: list, raja: int)`, joka saa parametrikseen listan kokonaislukuja sekä raja-arvon, joka on myös kokonaisluku.

Funktio muodostaa listakoostetta käyttäen uuden listan, josta on jätetty pois raja-arvoa pienemmät luvut.

Funktion maksimipituus on siis (mukaanlukien `def`-sanalla alkava otsikkorivi) kokonaisuudessaan kaksi riviä!

Esimerkki funktion käytöstä:

```python
lukuja = [1,65, 32, -6, 9, 11]
print(poista_pienemmat(lukuja, 10))

print(poista_pienemmat([-4, 7, 8, -100], 0))
```

<sample-output>

[65, 32, 11]
[7, 8]

</sample-output>

</programming-exercise>

<programming-exercise name='Vokaalilla alkavat' tmcname='osa11-06_vokaalilla_alkavat'>

Kirjoita funktio `vokaalilla_alkavat(sanat: list)`, joka saa parametrikseen listan merkkijonoja.

Tehtävänäsi on listakoostetta hyödyntäen muodostaa ja palauttaa uusi lista, joka sisältää vain alkuperäisen listan ne sanat, jotka alkavat vokaalilla (a, e, i, o, u, y, ä, ö). Sekä pienien että suurten kirjaimien pitää kelvata.

Funktion maksimipituus on (mukaanlukien `def`-sanalla alkava otsikkorivi) kokonaisuudessaan kaksi riviä!

Esimerkki funktion käytöstä:

```python
klista = ["auto","mopo","Etana","kissa","Koira","OMENA","appelsiini"]
for vok in vokaalilla_alkavat(klista):
    print(vok)
```

<sample-output>

auto
Etana
OMENA
appelsiini

</sample-output>

</programming-exercise>

## Alternativ exekvering med list comprehension

Ofta när vi har en villkorlig sats inkluderar vi också en else-gren. Eftersom vi kan använda villkor i list comprehensions är else-grenen också tillgänglig med list comprehension. Den allmänna syntaxen för villkoret som används med list comprehension ser ut så här:

`<uttryck 1> if <villkor> else <uttryck 2>`

Vi stötte på dessa enradiga villkor, eller ternära operatorer, redan i [del 7](https://programming-24.mooc.fi/part-7/6-more-features). Uttrycket ovan utvärderas till antingen `uttryck 1` eller `uttryck 2`, beroende på om villkoret är sant eller falskt.

Som en uppfräschning av ämnet kan vi säga att om vi behöver skriva ut det större av två tal och vi bara vill använda en enda utskriftssats, kan vi få plats med allt på en enda rad:

```python
luku1 = int(input("Anna luku 1:"))
luku2 = int(input("Anna luku 2:"))
print (luku1 if luku1 > luku2 else luku2)
```

Genom att kombinera den ternära operatorssyntaxen med en list comprehension-sats får man följande allmänna struktur:

`[<uttryck 1> if <villkor> else <uttryck 2> for <föremål> in <serie>]`

Det här kan se lite förvirrande ut, eftersom den villkorliga strukturen nu kommer före den faktiska list comprehensionen. Det är bara så här syntaxen har definierats, åtminstone för tillfället. Om det också finns en `else`-gren kommer villkoret först. Om det bara finns ett `if`, kommer det sist. Du kan prova att byta ut dem och se vad som händer.

Att inkludera en else-operator innebär att vi återigen kommer att bearbeta varje objekt från den ursprungliga listan. Beroende på om villkoret är sant eller falskt utförs antingen `uttryck 1` eller `uttryck 2` på varje objekt i listan.

I följande exempel kontrolleras om föremåleni en lista är noll eller högre. Alla sådana föremål accepteras som de är, men alla negativa föremål negeras, så att tecknet ändras från negativt till positivt. Resultatet är en lista som innehåller de absoluta värdena för föremålen i den ursprungliga listan.

```python

luvut = [1, -3, 45, -110, 2, 9, -11]
itseisarvot = [luku if luku >= 0 else -luku for luku in luvut]
print(itseisarvot)

```

<sample-output>

[1, 3, 45, 110, 2, 9, 11]

</sample-output>

Vi upprepar vad som händer ovan: om villkoret `nummer >= 0` är sant, genomgår föremålet uttrycket `nummer`, och resultatet är själva föremålet. Om villkoret är falskt genomgår föremålet uttrycket `–nummer`, så att det får ett positivt värde.

I följande exempel har vi funktionen `strang_langder` som tar en lista som sitt argument och returnerar en annan lista med längderna på alla strängar i den ursprungliga listan. Den här funktionen är dock okej med listföremål av alla typer. Om föremålet är en sträng beräknar den dess längd. Om objektet är något annat infogar den -1 i listan som den returnerar. 

```python

def merkkijonojen_pituudet(lista: list):
    """ Funktio palauttaa uudessa listassa merkkijonojen pituudet """
    return [len(alkio) if type(alkio) == str else -1 for alkio in lista]

if __name__ == "__main__":
    testilista = ["moi", 3, True, "kaikki", -123.344, "heipparallaa", 2, False]
    pituudet = merkkijonojen_pituudet(testilista)
    print(pituudet)

```

<sample-output>

[3, -1, -1, 6, -1, 12, -1, -1]

</sample-output>


<programming-exercise name='Lottorivi' tmcname='osa11-07_lottorivi'>

## Lottorivi, osa 1

Kirjoita luokka `Lottorivi`, joka saa konstruktorissaan parametrikseen kierroksen numeron (kokonaisluku) sekä seitsemänalkioisen kokonaislukulistan. Lista kuvaa kierroksen oikeita numeroita (eli oikeaa _riviä_). Kirjoita lisäksi luokalle metodi

`osumien_maara(pelattu_rivi: list)`

...joka palauttaa kokonaislukuna tiedon siitä, kuinka monta osumaa rivissä oli. Metodin tulee käyttää listakoostetta! Metodin pituus kokonaisuudessaan (def-rivi mukaanlukien) saa olla korkeintaan 2 riviä.

Esimerkki luokan käytöstä:

```python
oikea = Lottorivi(5, [1,2,3,4,5,6,7])
oma_rivi = [1,4,7,11,13,19,24]

print(oikea.osumien_maara(oma_rivi))
```

<sample-output>

3

</sample-output>

## Lottorivi, osa 2

Kirjoita luokkaan metodi `osumat_paikoillaan(pelattu_rivi)`, joka palauttaa uuden listan. Uudessa listassa on vanhoilla paikoillaan oikeat numerot (eli ne, jotka löytyvät myös oikeasta rivistä), muiden paikalla on -1.

Metodin tulee käyttää listakoostetta. Metodin pituus kokonaisuudessaan (def-rivi mukaanlukien) saa olla korkeintaan 2 riviä.

Esimerkki metodin käytöstä:

```python
oikea = Lottorivi(8, [1,2,3,10,20,30,33])
oma_rivi = [1,4,7,10,11,20,30]

print(oikea.osumat_paikoillaan(oma_rivi))
```

<sample-output>

[1, -1, -1, 10, -1, 20, 30]

</sample-output>

</programming-exercises>
