---
path: '/osa-2/4-loopar'
title: 'Enkla loopar'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* vet du vad en loop (slinga) betyder i programmeringssammanhang
* kan du använda dig av en `while True` -loop i dina program
* kommer du att kunna använda dig av `break`-instruktionen för att avbryta en loop.

</text-box>

Vi har nu undersökt if-satser som gör det möjligt för oss att skriva program där olika block körs i olika situationer (alternativ). Ett annat viktigt koncept inom programmering är repetition (eller iteration). Alternativ och repetition är två grundläggande konstruktioner som varje programmerare förväntas kunna. De är kontrollstrukturer – de ger dig möjlighet att påverka vilka kodrader som ska köras och när. Medan if-satser låter dig välja mellan olika delar av kod, används repetition för att köra delar av koden flera gånger. Programmet går alltså tillbaka till en viss rad i koden ett antal gånger. 

När man pratar om repetition i programmeringssammanhang använder man ofta det engelska begreppet loop även om det finns ett svenskt begrepp (slinga, silmukka på finska). En iteration är en "runda" i loopen – det vill säga när koden körs från början till slutet en gång. 

I den här delen presenterar vi en enkel while-loop. Dess struktur påminner om if-satsen. I nästa del dyker vi djupare in i de möjligheter som loopar ger.

Vi tar en titt på ett program som ber användaren att mata in ett tal som sedan skrivs ut upphöjt till två. Programmet körs tills användaren matar in -1:

```python
while True:
    tal = int(input("Ge ett tal, -1 avslutar programmet: "))

    if tal == -1:
        break

    print(tal ** 2)

print("Tack och hej!")
```

Så här kan det se ut när programmet körs:

<sample-output>

Ge ett tal, -1 avslutar programmet: **2**
4
Ge ett tal, -1 avslutar programmet: **4**
16
Ge ett tal, -1 avslutar programmet: **10**
100
Ge ett tal, -1 avslutar programmet: **-1**
Tack och hej!

</sample-output>

Som du ser ovan, frågar programmet om ett tal flera gånger tack vare while-satsen. När användaren anger siffran -1 kommer `break`-instruktionen att köras. Den gör att loopen genast avbryts och programkörningen fortsätter efter while-blocket.

En av de viktigaste sakerna att komma ihåg när man jobbar med while-loopar är att man måste se till att loopen avslutas i något skede. Annars kan vi få evighetsmaskiner, där loopen fortsätter för evigt (eller ja, tills vi stänger av programmet). Vi ändrar lite på ovanstående exempel för att åstadkomma en sådan situation:

```python
tal = int(input("Ge ett tal, -1 avslutar programmet: "))
while True:
    if tal == -1:
        break

    print(tal ** 2)

print("Tack och hej!")
```

I den här versionen frågar programmet användaren efter talet utanför loopen. Om användaren matar in något annat tal än -1 kommer loopen aldrig att avslutas. Vi har en oändlig loop vilket i princip betyder att koden körs oavbrutet, förevigt:

<sample-output>

Ge ett tal, -1 avslutar programmet: **2**
4
4
4
4
4
4
4
4
(fortsätter oändligt...)

</sample-output>

Följande program har en mycket liknande struktur jämfört med exemplet ovan, men för användaren ser det ganska annorlunda ut. Det här programmet låter användaren fortsätta endast då den korrekta pin-koden 1234 anges:

```python
while True:
    kod = input("Ange pin-kod: ")
    if kod == "1234":
        break
    print("Fel! Försök igen")

print("Korrekt pin-kod")
```

<sample-output>

Ange pin-kod: **0000**
Fel! Försök igen
Ange pin-kod: **9999**
Fel! Försök igen
Ange pin-kod: **1234**
Korrekt pin-kod

</sample-output>

<in-browser-programming-exercise name="Fortsätter vi?" tmcname="osa02-15_fortsatt">

Skriv enligt föregående exempel ett program som skriver ut texten "hej" och frågar "Fortsätter vi?" tills användaren svarar "nej". Efter det här skriver programmet ut "inte då" varpå programmet avslutas.

Exempel:

<sample-output>

hej
Fortsätter vi? **ja**
hej
Fortsätter vi? **yes**
hej
Fortsätter vi? **jawohl**
hej
Fortsätter vi? **nej**
inte då

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Valida värden" tmcname="osa02-16_validering">

Skapa ett program som ber användaren mata in tal. 

Om talet är negativt, ska programmet skriva ut meddelandet "Ogiltigt tal" och fråga efter ett nytt tal. 
Om talet är noll, avslutas loopen.
Om talet är positivt, skriver programmet ut siffrans kvadratrot med hjälp av `sqrt`-funktionen som vi kan få tillgång till med hjälp av `import`-satsen (vi importerar funktionen ur matematik-modulen, mer om detta senare i kursen). Exempel på funktionen:

```python
# from... import måste finnas i början av programmet för att sqrt ska fungera
from math import sqrt

print(sqrt(9))
```

<sample-output>

3.0

</sample-output>

Exempel på programmet:

<sample-output>

Ange tal: **16**
4.0
Ange tal: **4**
2.0
Ange tal: **-3**
Ogiltigt tal
Ange tal: **1**
1.0
Ange tal: **0**
Avslutar...

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Nedräkning" tmcname="osa02-17_nedrakning">

Det här programmet...

```python
siffra = 5
print("Nedräkning till start!")
while True:
  print(siffra)
  siffra = siffra - 1
  if siffra > 0:
    break

print("Gå!!")
```

...borde fungera så här:

<sample-output>

Nedräkning till start!
5
4
3
2
1
Gå!!

</sample-output>

Korrigera problemet i koden.

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Lösenord på nytt" tmcname="osa02-18_losenord">

Skapa ett program som ber användaren att ange ett lösenord och upprepa lösenordet. Så länge som de två inmatade lösenorden inte matchar, ska programmet be användaren upprepa lösenordet. 

<sample-output>

Lösenord: **hemligt?**
Upprepa lösenordet: **hemlighet**
Stämmer inte!
Upprepa lösenordet: **intminnsjanumer321**
Stämmer inte!
Upprepa lösenordet: **hemligt?**
Kontot skapat!

</sample-output>

</in-browser-programming-exercise>

## Loopar och hjälpvariabler

Vi gör nu pin-kodsexemplet en aning mer realistiskt. Det här exemplet tillåter användaren endast tre försök i att ge korrekt pin-kod.

Programmet består av två hjälpvariabler: `forsok` håller reda på hur många gånger användaren angett en pin-kod och `lyckades` är antingen `True` eller `False` beroende på om användaren har matat in den korrekta koden eller inte.

```python
forsok = 0

while True:
    kod = input("Ange pin-kod: ")
    forsok += 1

    if kod == "1234":
        lyckades = True
        break

    if forsok == 3:
        lyckades = False
        break

    # vi kommer hit om pin-koden är fel OCH tre försök inte ännu gjorts
    print("Fel! Försök igen")

if lyckades:
    print("Korrekt pin-kod")
else:
    print("För många försök...")
```

<sample-output>

Ange pin-kod: **0000**
Fel! Försök igen
Ange pin-kod: **1234**
Korrekt pin-kod

</sample-output>

<sample-output>

Ange pin-kod: **0000**
Fel! Försök igen
Ange pin-kod: **9999**
Fel! Försök igen
Ange pin-kod: **4321**
För många försök...

</sample-output>

Loopen avslutas antingen då pin-koden är korrekt eller maxantalet försök har uppnåtts. Efterföljande if-sats kollar variabeln `lyckades` värde och skriver ut ett meddelande baserat på det.

## print-satser för debuggning i loopar

Att introducera loopar i ett program ökar risken för buggar. Därför är det viktigt att senast nu börja vänja dig vid att utnyttja print-satser i debuggningssyfte – dem såg vi på i den första delen av denna modul.

Vi kikar på ett nästan identiskt program som i det föregående exemplet. Det finns dock en märkbar skillnad:

```python
forsok = 0

while True:
    kod = input("Ange pin-kod: ")
    forsok += 1

    if forsok == 3:
        lyckades = False
        break

    if kod == "1234":
        lyckades = True
        break

    print("Fel! Försök igen")

if lyckades:
    print("Korrekt pin-kod")
else:
    print("För många försök...")
```

Den här versionen fungerar konstigt när användaren anger den korrekta koden på det tredje försöket:

<sample-output>

Ange pin-kod: **0000**
Fel! Försök igen
Ange pin-kod: **9999**
Fel! Försök igen
Ange pin-kod: **1234**
För många försök...

</sample-output>

Nu borde vi alltså reda ut det här problemet. Några `print`-satser borde hjälpa oss att debugga – så låt oss lägga till sådana i loopen:

```python
while True:
    print("while-blocket inleds:")
    kod = input("Ange pin-kod: ")
    forsok += 1

    print("försök:", forsok)
    print("villkor 1:", forsok == 3)
    if forsok == 3:
        lyckades = False
        break

    print("kod:", kod)
    print("villkor 2:", kod == "1234")
    if kod == "1234":
        lyckades = True
        break

    print("Fel! Försök igen")
```

<sample-output>

while-blocket inleds:
Ange pin-kod: **2233**
försök: 1
villkor 1: False
kod: 2233
villkor 2: False
Fel! Försök igen
while-blocket inleds:
Ange pin-kod: **4545**
försök: 2
villkor 1: False
kod: 4545
villkor 2: False
Fel! Försök igen
while-blocket inleds:
Ange pin-kod: **1234**
försök: 3
villkor 1: True
För många försök...

</sample-output>

Från utskriften ovan märker vi att under den tredje iterationen kommer villkoret i den första if-satsen att vara sant och därmed hinner vi aldrig fram till den andra if-satsen i och med att loopen avslutas. Därmed kontrolleras koden aldrig:

```python
  while True:
    # ....

    # det här blocket kommer för tidigt
    if forsok == 3:
        lyckades = False
        break

    # vi når inte hit på det tredje försöket
    if kod == "1234":
        lyckades = True
        break
```

Ordningen på if-satser eller grenar inom if-satser är vanliga orsaker till buggar – framför allt när man nästlar if-satser innanför loopar. Debuggning med hjälp av print-satser hjälper förvånansvärt ofta.

<in-browser-programming-exercise name="Pin och antal försök" tmcname="osa02-19_pin">

Skapa ett program som frågar användaren om en pin-kod tills hen anger den korrekta pin-koden 4321. Programmet berättar hur många försök som har gjorts:

<sample-output>

Pin-kod: **3245**
Fel
Pin-kod: **1234**
Fel
Pin-kod: **0000**
Fel
Pin-kod: **4321**
Korrekt, du gjorde 4 försök

</sample-output>

Utskriften skiljer sig om användaren ger rätt pin-kod på första försöket: 

<sample-output>

Pin-kod: **4321**
Korrekt, du behövde bara ett försök!

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Nästa skottår" tmcname="osa02-20_nasta_skottar">

Skapa ett program som ber användaren ange ett årtal. Programmet ska berätta när nästa skottår är.

<sample-output>

År: **2019**
Nästa skottår efter 2019 är 2020

</sample-output>

Om året användaren anger är ett skottår (t.ex. 2020), ska programmet ändå berätta när det följande skottåret är:

<sample-output>

År: **2020**
Nästa skottår efter 2020 är 2024

</sample-output>

</in-browser-programming-exercise>

## Kombinera strängar med `+`-operatorn

Exemplet ovan använde hjälpvariabeln `forsok` för att hålla koll på hur många gånger användaren skrivit in en pin-kod:

```python
forsok = 0

while True:
    kod = input("Ange pin-kod: ")
    forsok += 1
    # ...
```

Variabeln tilldelas värdet noll utanför loopen och varje iteration ökar dess värde med ett.

Man kan också göra motsvarande sak med strängar. Programmet kan till exempel hålla koll på de pin-koder användaren angett:

```python
koder = ""
forsok = 0

while True:
    kod = input("Ange pin-kod: ")
    forsok += 1
    koder += kod + ", "
    # ...
```

Hjälpvariabeln kan tilldelas värdet `""` – det vill säga en tom sträng:

```python
koder = ""
```

För varje iteration blir strängen längre i och med att koden användaren angett läggs till i slutet av strängen tillsammans med ett komma och ett mellanslag.

```python
    kod = input("Ange pin-kod: ")
    koder += kod + ", "
```

Om användaren anger koderna 1111 2222 1234 kommer värdet på `koder` till slut att vara:

<sample-output>

1111, 2222, 1234,

</sample-output>


<in-browser-programming-exercise name="Berättelse" tmcname="osa02-21_berattelse">

### Del 1

Skapa ett program som ber användaren mata in ord. Då användaren matar in ordet `slut`, ska programmet skriva ut en berättelse som bildas av orden, varefter programmet avslutas.

<sample-output>

Ange ord: **Det**
Ange ord: **var**
Ange ord: **en**
Ange ord: **gång**
Ange ord: **...**
Ange ord: **slut**
Det var en gång ...

</sample-output>

### Del 2

Redigera programmet så att det slutar fråga efter ord då ordet `slut` anges eller då samma ord skrivs in två gånger efter varandra. 

<sample-output>

Ange ord: **I**
Ange ord: **början**
Ange ord: **fanns**
Ange ord: **hönan**
Ange ord: **eller**
Ange ord: **ägget**
Ange ord: **ägget**
I början fanns hönan eller ägget

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Behandling av tal" tmcname="osa02-22_tal">

Skapa ett program som ber användaren ange heltal. Programmet ber om tal tills användaren matar in 0.

<sample-output>

Ange heltal, 0 avslutar programmet:
Tal: **5**
Tal: **22**
Tal: **9**
Tal: **-2**
Tal: **0**

</sample-output>

### Del 1: Antal

Efter att talen har matats in ska programmet skriva ut antalet tal. Nollan ska inte tas i beaktande.

Du behöver en ny variabel som håller koll på antalet inmatade tal.

<sample-output>

(användaren anger tal)
Tillsammans 4 tal

</sample-output>

### Del 2: Summa

Utvidga programmet så att det skriver ut summan av de inmatade talen. Nollan ska inte tas i beaktande.

Så här ser utskriften ut nu:

<sample-output>

(användaren anger tal)
Tillsammans 4 tal
Summan av talen är 34

</sample-output>

### Del 3: Medelvärde

Utveckla programmet så att det räknar medelvärdet av de inmatade talen. Nollan ska inte tas i beaktande. Du kan anta att användaren matar in minst ett tal.

<sample-output>

(användaren anger tal)
Tillsammans 4 tal
Summan av talen är 34
Medelvärdet av talen är 8.5

</sample-output>

#### Del 4: Positiva och negativa

Gör nu så att programmet också skriver ut antalet positiva och negativa tal.

<sample-output>

(användaren anger tal)
Tillsammans 4 tal
Summan av talen är 34
Medelvärdet av talen är 8.5
Positiva 3
Negativa 1

</sample-output>

</in-browser-programming-exercise>

<quiz id="da2b29cc-7454-5bf8-a1e5-b2c879230dc7"></quiz>

Vänligen svara på en kort enkät som behandlar den här veckans material.

<quiz id="8599db93-abaa-5db3-9fbd-1af1281d8f76"></quiz>
