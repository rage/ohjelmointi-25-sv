---
path: '/osa-11/4-lisaa-esimerkkeja'
title: 'Fler exempel på rekursion'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Kommer du att känna till binära träd och några rekursiva algoritmer som används för att bearbeta dem

</text-box>


De verkliga fördelarna med rekursion blir uppenbara när vi stöter på problem där iterativa lösningar är svåra att skriva. Låt oss ta en titt på binära träd, till exempel. Ett binärt träd är en förgrenad struktur där vi har noder och vid varje nod förgrenar sig strukturen, som mest, i två underordnade grenar med egna noder. Ett binärt träd skulle då kunna se ut så här (datavetenskap betraktas ofta som en gren av naturvetenskapen, men vår förståelse av träd är lite upp och ner, som du kommer att märka):

<img src="11_4_1.png">

Binära träd bör åtminstone teoretiskt sett vara lätta att hantera rekursivt: om vi vill utföra någon operation på varje nod i trädet behöver vår algoritm helt enkelt

1. Behandla den aktuella noden
2. Anropa sig själv på barnnoden till vänster
3. Anropa sig själv på barnnoden till höger

<img src="11_4_2.png">

Som du kan se på bilden ovan är både de vänstra och högra "underträden" fullfjädrade binära träd i sig, och den enda nod som lämnas utanför de rekursiva anropen är den överordnade noden, som bearbetas i steg 1 innan funktionen anropas rekursivt. På så sätt kan vi vara säkra på att varje nod har besökts exakt en gång när funktionen är klar.

En iterativ version av en binär trädtraversering skulle vara mycket mer komplicerad, eftersom vi på något sätt skulle behöva hålla reda på alla noder som vi redan har besökt. Samma principer gäller för alla beräkningsbara trädstrukturer, inte bara binära.

Ett binärt träd är också lätt att modellera i Python-kod. Vi behöver bara skriva en klassdefinition för en enda nod. Den har ett värdeattribut och attribut för de vänstra och högra underordnade noderna:

```python

class Alkio:
    """ Luokka mallintaa yhtä alkiota binääripuussa """
    def __init__(self, arvo, vasen_lapsi:'Alkio' = None, oikea_lapsi:'Alkio' = None):
        self.arvo = arvo
        self.vasen_lapsi = vasen_lapsi
        self.oikea_lapsi = oikea_lapsi
```

Låt oss anta att vi vill modellera följande träd:

<img src="11_4_3.png">

Vi kunde uppnå detta med följande kod:

```python
if __name__ == "__main__":
    puu = Alkio(2)

    puu.vasen_lapsi = Alkio(3)
    puu.vasen_lapsi.vasen_lapsi = Alkio(5)
    puu.vasen_lapsi.oikea_lapsi = Alkio(8)

    puu.oikea_lapsi = Alkio(4)
    puu.oikea_lapsi.oikea_lapsi = Alkio(11)

```

## Algoritmer för rekursiva binära träd

Låt oss först ta en titt på en algoritm som skriver ut alla noder i ett binärt träd en efter en. I de följande exemplen kommer vi att arbeta med det binära träd som definieras ovan.

Argumentet till utskriftsfunktionen är rotnoden i det binära trädet. Detta är noden högst upp i vår illustration ovan. Alla andra noder är barn till den här noden:

```python

def tulosta_alkiot(juuri: Alkio):
    print(juuri.arvo)

    if juuri.vasen_lapsi is not None:
        tulosta_alkiot(juuri.vasen_lapsi)

    if juuri.oikea_lapsi is not None:
        tulosta_alkiot(juuri.oikea_lapsi)

```

Funktionen skriver ut värdet på den nod som skickas som argument och anropar sedan sig själv på de vänstra och högra underordnade noderna, förutsatt att noderna är definierade. Det här är en mycket enkel algoritm, men den går på ett effektivt och tillförlitligt sätt igenom alla noder i trädet, oavsett trädets storlek. Avgörande är att ingen nod besöks två gånger. Varje värde skrivs bara ut en gång.

Om vi skickar rotnoden `trad` i det binära trädet som illustreras ovan som ett argument till funktionen, skriver den ut

<sample-output>

2
3
5
8
4
11

</sample-output>

Som du kan se av ordningen på noderna i utskriften rör sig algoritmen först längs trädets "vänstra ben" ner till botten, och därifrån går den igenom de andra noderna i ordning.

På samma sätt kan vi skriva en algoritm för att beräkna summan av alla de värden som finns lagrade i trädets noder:

```python

def alkioiden_summa(juuri: Alkio):
    summa = juuri.arvo

    if juuri.vasen_lapsi is not None:
        summa += alkioiden_summa(juuri.vasen_lapsi)

    if juuri.oikea_lapsi is not None:
        summa += alkioiden_summa(juuri.oikea_lapsi)

    return summa

```

Variabeln `nod_summa` initieras till att vara lika med värdet för den aktuella noden. Värdet i variabeln ökas sedan genom rekursiva anrop till nodens summor i det vänstra och högra underordnade trädet (först kontrolleras naturligtvis att de finns). Detta resultat returneras sedan.

<programming-exercise name='Suurin alkio' tmcname='osa11-16_suurin_alkio'>

Kirjoita funktio `suurin_alkio(juuri: Alkio)`, joka saa parametrikseen binääripuun juurialkion.

Funktion palauttaa puun suurimman alkion. Puun arvot tulee käydä läpi rekursiivisesti.

Vinkki: voit hyödyntää ratkaisussasi ylempänä esitettyä `alkoiden_summa` -funktiota.

Esimerkki funktion kutsumisesta:

```python

if __name__ == "__main__":
    puu = Alkio(2)

    puu.vasen_lapsi = Alkio(3)
    puu.vasen_lapsi.vasen_lapsi = Alkio(5)
    puu.vasen_lapsi.oikea_lapsi = Alkio(8)

    puu.oikea_lapsi = Alkio(4)
    puu.oikea_lapsi.oikea_lapsi = Alkio(11)

    print(suurin_alkio(puu))

```

<sample-output>

11

</sample-output>

</programming-exercise>

## Sorterat binärt träd

Ett binärt träd är särskilt användbart när noderna är sorterade på ett visst sätt. Det gör att det går snabbt och effektivt att hitta noder i trädet.

Låt oss ta en titt på ett träd som är sorterat på följande sätt: det vänstra barnet till varje nod är mindre än själva noden och det högra barnet är på motsvarande sätt större.

<img src="11_4_1.png">

Nu kan vi skriva en rekursiv algoritm för att söka efter noder. Idén är mycket lik den binära sökningen från föregående avsnitt: om den aktuella noden är den nod vi letar efter, returnera `True`. Annars fortsätter vi rekursivt med antingen det vänstra eller det högra underordnade trädet. Om noden inte är definierad returneras `False`.

```python

def etsi_alkio(juuri: Alkio, arvo):
    if juuri is None:
        return False

    if arvo == juuri.arvo:
        return True

    if arvo > juuri.arvo:
        return etsi_alkio(juuri.oikea_lapsi, arvo)

    return etsi_alkio(juuri.vasen_lapsi, arvo)

```

<programming-exercise name='Pomot ja alaiset' tmcname='osa11-17_pomot_ja_alaiset'>

Luokka `Tyontekija` mallintaa yrityksen työntekijää:

```python
class Tyontekija:
    def __init__(self, nimi: str):
        self.nimi = nimi
        self.alaiset = []

    def lisaa_alainen(self, tyontekija: 'Tyontekija'):
        self.alaiset.append(tyontekija)
```

Tee funktio `laske_alaiset(tyontekija: Tyontekija)`, joka laskee rekursiivisesti annetun työntekijän alaisten määrän.

Esimerkki funktion käyttämisestä:

```python
if __name__ == "__main__":
    t1 = Tyontekija("Sasu")
    t2 = Tyontekija("Erkki")
    t3 = Tyontekija("Matti")
    t4 = Tyontekija("Emilia")
    t5 = Tyontekija("Antti")
    t6 = Tyontekija("Kjell")
    t1.lisaa_alainen(t4)
    t1.lisaa_alainen(t6)
    t4.lisaa_alainen(t2)
    t4.lisaa_alainen(t3)
    t4.lisaa_alainen(t5)
    print(laske_alaiset(t1))
    print(laske_alaiset(t4))
    print(laske_alaiset(t5))
```

<sample-output>

5
3
0

</sample-output>

</programming-exercise>

## Besök till tiden innan rekursion

Låt oss avsluta denna del av materialet med en lite större övning som koncentrerar sig på objektorienterade programmeringsprinciper. Vi rekommenderar inte att du använder rekursion i denna serie av uppgifter, men tekniker för list comprehension kommer att vara användbara. 

<programming-exercise name='Tilauskirja' tmcname='osa11-18_tilauskirja'>

Teemme tässä tehtävässä kaksi luokkaa, joitka toimivat rakennuspalikoina seuraavassa tehtävässä aiheena olevassa sovelluksessa.

## Tehtava

Toteuta luokka `Tehtava`, joka mallintaa ohjelmistoyritykselle annettavia työtehtäviä. Tehtävillä on
- kuvaus
- arvio sen viemästä työmäärästä
- tieto koodarista, joka toteuttaa tehtävän
- tieto siitä, onko tehtävä valmis vai ei
- yksikäsitteinen tunniste eli id

Luokka toimii seuraavasti:

```python
t1 = Tehtava("koodaa hello world", "Erkki", 3)
print(t1.id, t1.kuvaus, t1.koodari, t1.tyomaara)
print(t1)
print(t1.on_valmis())
t1.merkkaa_valmiiksi()
print(t1)
print(t1.on_valmis())
t2 = Tehtava("koodaa webbikauppa", "Antti", 10)
t3 = Tehtava("tee mobiilisovellus työaikakirjanpitoon", "Erkki", 25)
print(t2)
print(t3)
```

<sample-output>

1 koodaa hello world Erkki 3
1: koodaa hello world (3 tuntia), koodari Erkki EI VALMIS
False
1: koodaa hello world (3 tuntia), koodari Erkki VALMIS
True
2: koodaa webbikauppa (10 tuntia), koodari Antti EI VALMIS
3: tee mobiilisovellus työaikakirjanpitoon (25 tuntia), koodari Erkki EI VALMIS

</sample-output>

Täsmennyksiä:
- tehtävän tilan (valmis vai ei vielä valmis) voi tarkistaa metodilla `on_valmis(self)` joka palauttaa totuusarvon
- tehtävä ei ole siinä vaiheessa valmis kun se luodaan
- tehtävä merkataan valmiiksi kutsumalla metodia `merkkaa_valmiiksi(self)`
- tehtävien id on juokseva numero, joka alkaa arvosta 1 (ensimmäisenä luotava tehtävä saa id:n 1, seuraava id:n 2 jne.)

**Vihje**: id kannattaa toteuttaa [luokkamuuttujana](/osa-9/5-staattiset-piirteet#luokkamuuttujat).

## Tilauskirja

Tehdään nyt luokka `Tilauskirja`, joka kokoaa kaikki ohjelmistoyritykseltä tilatut työtehtävät, joita siis mallinnetaan luokan `Tehtava` olioilla.


Tilauskirjan perusversiota käytetään seuraavasti:

```python
tilaukset = Tilauskirja()
tilaukset.lisaa_tilaus("koodaa webbikauppa", "Antti", 10)
tilaukset.lisaa_tilaus("tee mobiilisovellus työaikakirjanpitoon", "Erkki", 25)
tilaukset.lisaa_tilaus("tee ohjelma matematiikan harjoitteluun", "Antti", 100)

for tilaus in tilaukset.kaikki_tilaukset():
    print(tilaus)

print()

for koodari in tilaukset.koodarit():
    print(koodari)
```

<sample-output>

1: koodaa webbikauppa (10 tuntia), koodari Antti EI VALMIS
2: tee mobiilisovellus työaikakirjanpitoon (25 tuntia), koodari Erkki EI VALMIS
3: tee ohjelma matematiikan harjoitteluun (100 tuntia), koodari Antti EI VALMIS

Antti
Erkki

</sample-output>

Tässä vaiheessa `Tilauskirja` tarjoaa kolme metodia:
- `lisaa_tilaus(self, kuvaus, koodari, tyomaara)` lisää uuden tilauksen tilauskirjaan. Tilauskirja tallettaa tilaukset sisäisesti `Tehtava`-olioina. Huomaa, että metodilla täytyy olla juuri nämä parametrit, muuten testit eivät hyväksy metodia!
- `kaikki_tilaukset(self)` palauttaa listana kaikki tilauskirjalla olevat tehtävät
- `koodarit(self)` palauttaa listana kaikki koodarit, joille on tehtävä tilauskirjassa, metodin palauttama lista ei saa sisältää yhtä koodia useampaan kertaan

**Vihje** Listalta on helppo poistaa duplikaatit siten että muutetaan ensin lista [set](https://docs.python.org/3.8/library/stdtypes.html#set)-tyyppiseksi. Set siis tarkoittaa joukkoa, ja joukossa kutakin alkiota voi olla vain yksi kappale. Tämän jälkeen `set` voidaan muuttaa takaisin listaksi, ja duplikaatit ovat kadonneet:

```python
lista = [1,1,3,6,4,1,3]
lista2 = list(set(lista))
print(lista)
print(lista2)
```

<sample-output>

[1, 1, 3, 6, 4, 1, 3]
[1, 3, 4, 6]

</sample-output>

## Tilauskirjan viimeistely

Tehdään luokalle `Tilauskirja` vielä kolme uutta metodia.

Metodi `merkkaa_valmiiksi(self, id: int)` saa parametriksi tehtävän id:n ja merkkaa kyseisen tehtävän valmiiksi:

```python
tilaukset = Tilauskirja()
tilaukset.lisaa_tilaus("koodaa webbikauppa", "Antti", 10)
tilaukset.lisaa_tilaus("tee mobiilisovellus työaikakirjanpitoon", "Erkki", 25)
tilaukset.lisaa_tilaus("tee ohjelma matematiikan harjoitteluun", "Antti", 100)

tilaukset.merkkaa_valmiiksi(1)
tilaukset.merkkaa_valmiiksi(2)

for tilaus in tilaukset.kaikki_tilaukset():
    print(tilaus)
```

<sample-output>

1: koodaa webbikauppa (10 tuntia), koodari Antti VALMIS
2: tee mobiilisovellus työaikakirjanpitoon (25 tuntia), koodari Erkki VALMIS
3: tee ohjelma matematiikan harjoitteluun (100 tuntia), koodari Antti EI VALMIS

</sample-output>

Jos parametria vastaavaa tilausta ei löydy, tuottaa metodi poikkeuksen `ValueError`. Kertaa tarvittaessa [täältä](/osa-6/3-virheet#poikkeusten-tuottaminen), miten poikkeus tuotetaan.

Metodit `valmiit_tilaukset(self)` ja `ei_valmiit_tilaukset(self)` toimivat kuten olettaa saattaa, ne palauttavat nimensä mukaisen osajoukon tilauskirjan tehtävistä listana.

## Tilauskirjan loppusilaus

Tehdään luokalle `Tilauskirja` vielä metodi `koodarin_status(self, koodari: str)`, joka palauttaa _tuplen_, joka kertoo koodarin valmistuneiden ja vielä valmistumattomien töiden määrän sekä näihin kuluneiden työtuntien summan.

```python
tilaukset = Tilauskirja()
tilaukset.lisaa_tilaus("koodaa webbikauppa", "Antti", 10)
tilaukset.lisaa_tilaus("tee mobiilisovellus työaikakirjanpitoon", "Antti", 25)
tilaukset.lisaa_tilaus("tee ohjelma matematiikan harjoitteluun", "Antti", 100)
tilaukset.lisaa_tilaus("tee uusi facebook", "Erkki", 1000)

tilaukset.merkkaa_valmiiksi(1)
tilaukset.merkkaa_valmiiksi(2)

status = tilaukset.koodarin_status("Antti")
print(status)
```

<sample-output>

(2, 1, 35, 100)

</sample-output>

Tuplen ensimmäinen alkio siis kertoo valmiiden töiden määrän ja toinen valmistumattomien töiden määrän. Kolmas alkio on valmiiden töiden työaika-arvioiden summa ja neljäs alkio vielä valmistumattomien töiden työmääräarvioiden summan.

Jos parametria vastaavaa koodaria ei löydy, tuottaa metodi poikkeuksen `ValueError`.


</programming-exercise>

<programming-exercise name='Tilauskirjasovellus' tmcname='osa11-19_tilauskirjasovellus'>

Tässä tehtävässä tehdään interaktiivinen sovellus softafirmalta tilattujen tehtävien hallintaan. Tyyli on täysin vapaa, mutta voit hyödyntää sovelluksessa edellisen tehtävän aikana koodattuja rakennuspalikoita. Myös [edellisen osan viimeisen luvun](/osa-10/4-lisaa-esimerkkeja) materiaalin kertaaminen saattaa olla hyödyksi.

## Ei virheiden käsittelyä

Sovelluksen tulee toimia _täsmälleen_ seuraavasti:

<sample-output>

komennot:
0 lopetus
1 lisää tilaus
2 listaa valmiit
3 listaa ei valmiit
4 merkitse tehtävä valmiiksi
5 koodarit
6 koodarin status

komento: **1**
kuvaus: **koodaa uusi facebook**
koodari ja työmääräarvio: **joona 1000**
lisätty!

komento: **1**
kuvaus: **tee sovellus ajanhallintaan**
koodari ja työmääräarvio: **erkki 25**
lisätty!

komento: **1**
kuvaus: **ohjelma musiikin teorian harjoitteluun**
koodari ja työmääräarvio: **niina 12**
lisätty!

komento: **1**
kuvaus: **koodaa uusi twitter**
koodari ja työmääräarvio: **joona 55**
lisätty!

komento: **2**
ei valmiita

komento: **3**
1: koodaa uusi facebook (1000 tuntia), koodari joona EI VALMIS
2: tee sovellus ajanhallintaan (25 tuntia), koodari erkki EI VALMIS
3: ohjelma musiikin teorian  harjoitteluun (12 tuntia), koodari niina EI VALMIS
4: koodaa uusi twitter (55 tuntia), koodari joona EI VALMIS

komento: **4**
tunniste: **2**
merkitty valmiiksi

komento: **4**
tunniste: **4**
merkitty valmiiksi

komento: **2**
2: tee sovellus ajanhallintaan (25 tuntia), koodari erkki VALMIS
4: koodaa uusi twitter (55 tuntia), koodari joona VALMIS

komento: **3**
1: koodaa uusi facebook (1000 tuntia), koodari joona EI VALMIS
3: ohjelma musiikin teorian harjoitteluun (12 tuntia), koodari niina EI VALMIS

komento: **5**
joona
erkki
niina

komento: **6**
koodari: **joona**
työt: valmiina 2 ei valmiina 1, tunteja: tehty 55 tekemättä 1000

</sample-output>

Ensimmäiseen tehtäväpisteeseen riittää, että sovellus toimii jos kaikki syötteet ovat virheettömiä.

## Virheiden käsittely

Toiseen tehtäväpisteeseen edellytetään, että sovellus toipuu käyttäjän syötteessä olevista virheistä. Virheiden käsittelyn tulee toimia siten, että missä tahansa syötteessa annettu virheellinen syöte aiheuttaa virheilmoituksen _virheellinen syöte_, ja johtaa siihen, että komentoa pyydetään uudelleen:

<sample-output>

komento: **1**
kuvaus: **tee sovellus ajanhallintaan**
koodari ja työmääräarvio: **erkki xxx**
virheellinen syöte

komento: **1**
kuvaus: **tee sovellus ajanhallintaan**
koodari ja työmääräarvio: **erkki**
virheellinen syöte

komento: **4**
tunniste: **1000000**
virheellinen syöte

komento: **4**
tunniste: **XXXX**
virheellinen syöte

komento: **6**
koodari: **tuntematonkoodari**
virheellinen syöte

</sample-output>

</programming-exercise>

Vastaa lopuksi osion loppukyselyyn:

<quiz id="4acb2792-f51e-55f0-b482-addf1977c630"></quiz>
