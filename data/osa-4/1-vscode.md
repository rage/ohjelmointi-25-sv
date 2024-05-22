---
path: '/osa-4/1-vscode'
title: 'Editorn Visual Studio Code, Pythontolken och det inbyggda debuggningsverktyget'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Efter den här delen

* kommer du att vara förberedd på att använda Visual Studio Code för att göra den här kursens övningar
* kommer du att vara bekant med den interaktiva Pythontolken, som du kan använda för att köra kod.

</text-box>

Hittills har alla övningar i den här kursen gjorts direkt på kurssidorna i de inbäddade kodeditorerna. Att programmera i webbläddraren fungerar bra när man börjar lära sig att programmering. Nu är det ändå dags att börja använda en separat kodeditor som är anpassad just för att redigera kod.

Det finns en hel del olika editorer som är skräddarsydda för programmering. På den här kursen kommer vi att använda Visual Studio Code – en editor som under de senaste åren fått allt större fotfäste på marknaden.

Din uppgift är att nu installera Visual Studio Code på din dator. Det kan hända att du också måste installera Python och Python-tillägget (plugin) i Visual Studio Code. Du behöver också TMC-tillägget som tar hand om att köra de tester som finns i samband med övningarna. I TMC:s inställningar ska du välja MOOC som organisation och Python-programmering 2024 som kurs.

Här hittar du en guide som berättar hur du kan installera allt som nämnts ovan. Läs instruktionerna och gör sedan uppgiften nedan:

<programming-exercise name='Hello Visual Studio Code' tmcname='osa04-01_hello_visualstudio_code'>

Tee ohjelma, joka kysyy käyttäjältä, mikä editori on käytössä. Ohjelma jatkaa, kunnes vastaus on _Visual Studio Code_.

Seuraava käyttöesimerkki havainnollistaa ohjelman haluttua tulostusta:

<sample-output>

Editori: **Emacs**
ei ole hyvä
Editori: **Vim**
ei ole hyvä
Editori: **Word**
surkea
Editori: **Atom**
ei ole hyvä
Editori: **Visual Studio Code**
loistava valinta!

</sample-output>

Jos käyttäjä kirjoittaa Word tai Notepad, ohjelma vastaa _surkea_. Muissa epäkelvoissa tapauksissa vastaus on _ei ole hyvä_.

Ohjelman tulee toimia siten, että "oikean vastauksen" kirjoitusasu ei riipu siitä, kirjoitetaanko vastaus isoja vai pieniä kirjaimia käyttämällä:

<sample-output>

Editori: **NOTEPAD**
surkea
Editori: **viSUal STudiO cODe**
loistava valinta!

</sample-output>

Kirjainten koon voi jättää huomiotta esim. muuttamalla kirjaimet pieniksi merkkijonojen metodilla `lower`, jota voi käyttää seuraavasti:

```python
mjono = "Visual Studio CODE"
if "visual studio code" == mjono.lower():
    print("merkkijono oli etsitty!")
```

**Huom:** tässä tehtävässä (eikä missään muussakaan tehtävissä missä _ei_ erikseen pyydetä funktioiden toteuttamista) mitään koodia __ei tule sijoittaa__
`if __name__ == "__main__"`-lohkoon!

</programming-exercise>

## Köra kod

I Visual Studio Code är det enklaste sättet att köra kod att klicka på triangeln uppe i hörnet till höger. Ibland kan det hända att något program blir och köra i bakgrunden – det kanske väntar på att användaren ger någon data eller är fast i en oändlig loop – utan att du märker det. Du märker det eventuellt först när du försöker köra nästa program som helt enkelt inte kommer att köra eftersom det föregående programmet tar upp alla resurser. En snabb lösning på det här är att trycka på tangenterna Control + C samtidigt. Det här avslutar den pågående processen. Nästa program borde nu kunna köra normalt.

## Den interaktiva Pythontolken

Ett av de viktigaste verktygen för en Python-programmerare är den interaktiva Python-tolken.

Hur du får tolken igång beror eventuellt på den miljö där du kör Python i. På Linux och Mac kan du skriva `python3` i terminalen. På Windows kan kommandot heta `python`. Så här ser tolken ut på Mac:

<img src="4_1_1.png">

Det är också möjligt att starta tolken i Visual Studio Code. Kör först ett program genom att klicka på triangeln. Nu borde en ”Terminal”-del öppnas på din skärm. Där kan du skriva `python3` (eller `python`):

<img src="4_1_2.png">

Du kan också testa på en webbaserad Pythontolk, till exempel: <https://www.python.org/shell/>.

Med hjälp av tolken kan du köra Python-kod rad för rad, i realtid. När du skriver en rad kod och trycker på Enter, kommer tolken att köra den omedelbart och visa dess resultat:

<img src="4_1_3.png">

All Python-kod som skrivs i en fil kan också skrivas i tolken. Du kan till och med tilldela variabler och definiera metoder:

```python
>>> t = [1,2,3,4,5]
>>> for luku in t:
...   print(luku)
...
1
2
3
4
5
>>> def itseisarvo(luku):
...   if luku<0:
...      luku = -luku
...   return luku
...
>>> x = 10
>>> y = -7
>>> itseisarvo(luku)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'luku' is not defined
>>> itseisarvo(x)
10
>>> itseisarvo(y)
7
>>>
```

Tolken kan framför allt användas för att göra små kontroller. Du kan till exempel testa funktioner eller metoder – eller kolla om de existerar över huvud taget:

```python
>>> "TekstIä".toupper()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'str' object has no attribute 'toupper'
>>> "TekstIä".upper()
'TEKSTIÄ'
>>>
```

Om det finns en metod som du behöver, och du minns ungefär vad dess namn är, kan det ibland vara snabbare att skippa Google och istället använda `dir`-funktionen i tolken. Funktionen berättar vilka metoder kan användas hos ett specifikt objekt:

```python
>>> dir("teksti")
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__',
'__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__',
'__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__',
'__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__',
'__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__',
'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find',
'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isascii', 'isdecimal', 'isdigit',
'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join',
'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust','rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase',
'title', 'translate', 'upper', 'zfill']
```

Som du ser ovan, har strängar i Python har en hel del metoder. För tillfället lönar det sig att ignorera metoder som har understreck i sina namn, men andra metoder kan visa sig vara nyttiga. Vissa får du kanske att fungera på egen hand, andra kan du söka mera information om på nätet.

Listor i Python verkar inte ha så många metoder:

```python
>>> dir([])
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__',
'__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__',
'__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__',
'__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__',
'__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__',
'__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop',
'remove', 'reverse', 'sort']
>>>
```

Vi testar på några av dem – `reverse` och `clear` verkar lovande:

```python
>>> luvut = [1,2,3,4,5]
>>> luvut.reverse()
>>> luvut
[5, 4, 3, 2, 1]
>>> luvut.clear()
>>> luvut
[]
```

Som du kan notera, gör dessa metoder just det man skulle kunna anta.

Märk att tolken inte skriver ut någonting när du kör kommandot `siffror.reverse()`. Detta beror på att tolken endast skriver ut något då kodraden har ett värde. Metoden `reverse()` här returnerar inget värde.

I det ovanstående exemplet skrev vi ut värdet på listan `siffor` med att skriva namnet på variabeln. I tolken behöver man sällan använda sig av `print`-kommandon. Det är däremot inte förbjudet att använda dem.

Kom ihåg att stänga tolken när du är klar. Kommandona `quit()` och `exit()` fungerar bra för det här ändamålet. Även tangentkombinationerna Control + D (Linux/Mac) och Control + Z (Windows) har samma funktion. Speciellt i Visual Studio Code är det här viktigt. Om du nämligen försöker köra ett annat Python-program medan tolken är igång, kommer du att få ett ganska konstigt felmeddelande:

<img src="4_1_4.png">

## Det inbyggda debuggningsverktyget

Vi har redan övat en hel del på att debugga – främst med hjälp av print-satser. Visual Studio Code erbjuder dig ett ytterligare verktyg för ändamålet: en inbyggd visuell debuggare.

För att börja debugga måste du lägga till en breakpoint – ett ställe där debuggaren stannar körandet av koden. Du kan lägga till en breakpoint genom att klicka på det vänstra hörnet av vilken som helst kodrad i ditt program.

Det följande exemplet innehåller en icke-fungerande lösning på övningen Summan av på varandra följande tal från den förra modulen. På rad fem finns en breakpoint:

<img src="4_1_5.png">

När breakpointen har skapats ska du välja Start debugging från Run-menyn. Det här öppnar en lista med alternativ av vilka du bör välja Python File:

<img src="4_1_6.png">

Det här startar debuggaren som kör din kod normalt tills man när breakpointen: här stannar körandet upp. Om koden ber om indata ska du minnas att skriva det in i terminalen:

<img src="4_1_7.png">

Till vänster finns nu en Variables-vy som innehåller de nuvarande värdena på alla aktiva variabler i koden. Du kan fortsätta att köra koden rad för rad genom att klicka på pilen som riktar neråt – Step into.

I den följande bilden har loopen i koden upprepat några gånger:

<img src="4_1_8.png">

Debuggaren har en Debug console -flik som låter dig köra uttryck med de nuvarande variabelvärdena. Du kan till exempel kolla värdet på Boolean-uttrycket som finns i loopens villkor:

<img src="4_1_9.png">

Du kan ha flera breakpoints i din kod. När körandet av koden har stannat upp kan du starta det genom att klicka på den blå triangeln. Körandet fortsätter tills nästa breakpoint nås.

Den inbyggda visuella debuggaren är ett bra alternativ till debuggning med print-satser. Det är upp till dig själv vilken metod du använder dig av i fortsättningen. Alla programmerare har sina egna preferenser, men det är alltid en bra idé att testa på olika alternativ förrän man bestämmer sig för att göra på ett visst sätt.
