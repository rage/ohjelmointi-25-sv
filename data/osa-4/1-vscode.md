---
path: '/osa-4/1-vscode'
title: 'Editorn Visual Studio Code, Pythontolken och det inbyggda debuggningsverktyget'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* kommer du att vara förberedd på att använda Visual Studio Code för att göra den här kursens övningar
* kommer du att vara bekant med den interaktiva Pythontolken, som du kan använda för att köra kod.

</text-box>

Hittills har alla övningar i den här kursen gjorts direkt på kurssidorna i de inbäddade kodeditorerna. Att programmera i webbläsaren fungerar bra när man börjar lära sig programmering. Nu är det ändå dags att börja använda en separat kodeditor som är anpassad just för att redigera kod.

Det finns en hel del olika editorer som är skräddarsydda för programmering. På den här kursen kommer vi att använda [Visual Studio Code](https://code.visualstudio.com/) – en editor som under de senaste åren fått allt större fotfäste på marknaden.

Din uppgift är att nu installera Visual Studio Code på din dator. Det kan hända att du också måste installera Python och Python-tillägget (plugin) i Visual Studio Code. Du behöver också TMC-tillägget som tar hand om att köra de tester som finns i samband med övningarna. I TMC:s inställningar ska du välja MOOC som organisation och Programmering 2025 som kurs.

[Här hittar du en guide](https://www.mooc.fi/en/installation/vscode/) som berättar hur du kan installera allt som nämnts ovan. Kom ihåg att du ska välja den svenska kursen (Programmering 2025). Läs instruktionerna och gör sedan uppgiften nedan:

<programming-exercise name='Hello Visual Studio Code' tmcname='osa04-01_vs_code'>

Skapa ett program som frågar användaren om vilken kodeditor hen har. Programmet fortsätter köra tills användaren svarar Visual Studio Code.

Exempel:

<sample-output>

Editor: **Emacs**
inte bra
Editor: **Vim**
inte bra
Editor: **Word**
usel
Editor: **Atom**
inte bra
Editor: **Visual Studio Code**
perfekt val!

</sample-output>

Om användaren svarar Word eller Notepad ger programmet kommentaren "usel". I övriga icke-giltiga fall "inte bra".

Programmet ska fungera oberoende hur namnet skrivs, dvs. bruket av gemener/versaler ska inte påverka:

<sample-output>

Editor: **NOTEPAD**
usel
Editor: **viSUal STudiO cODe**
perfekt val!

</sample-output>

Du kan ignorera storleken på bokstäverna, till exempel genom att ändra bokstäverna till gemener med strängmetoden `lower`, som kan användas enligt följande:

```python
strang = "Visual Studio CODE"
if "visual studio code" == strang.lower():
    print("strängen hittades")
```

Obs! Placera inte någon kod i `if __name__ == "__main__"` -blocket i dessa uppgifter, om du inte ombeds göra det.

</programming-exercise>

## Att köra kod

I Visual Studio Code är det enklaste sättet att köra kod att klicka på triangeln ("play"-knappen) uppe i hörnet till höger. Ibland kan det hända att något program blir och köra i bakgrunden – det kanske väntar på att användaren ger någon data eller är fast i en oändlig loop – utan att du märker det. Du märker det eventuellt först när du försöker köra nästa program som helt enkelt inte kommer att köra eftersom det föregående programmet tar upp alla resurser. En snabb lösning på det här är att trycka på tangenterna Control + C samtidigt. Det här avslutar den pågående processen. Nästa program borde nu kunna köra normalt.

## Den interaktiva Pythontolken

Ett av de viktigaste verktygen för en Python-programmerare är den interaktiva Python-tolken.

Man startar tolken på olika sätt beroende på den miljö som du kör Python i. På Linux och Mac kan du skriva `python3` i terminalen. På Windows kan kommandot heta `python`. Så här ser tolken ut på Mac:

<img src="4_1_1.png">

Det är också möjligt att starta tolken i Visual Studio Code. Kör först ett program genom att klicka på play-knappen (triangeln). Nu borde en "Terminal"-del öppnas på din skärm. Där kan du skriva `python3` (eller `python`):

<img src="4_1_2.png">

Du kan också testa på en webbaserad Pythontolk, till exempel: <https://www.python.org/shell/>.

Med hjälp av tolken kan du köra Python-kod rad för rad, i realtid. När du skriver en rad kod och trycker på Enter, kommer tolken att köra den omedelbart och visa dess resultat:

<img src="4_1_3.png">

All Python-kod som skrivs i en fil kan också skrivas i tolken. Du kan till och med tilldela variabler och definiera metoder:

```python
>>> t = [1,2,3,4,5]
>>> for siffra in t:
...   print(siffra)
...
1
2
3
4
5
>>> def absolutbelopp(siffra):
...   if siffra<0:
...      siffra = -siffra
...   return siffra
...
>>> x = 10
>>> y = -7
>>> absolutbelopp(siffra)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'siffra' is not defined
>>> absolutbelopp(x)
10
>>> absolutbelopp(y)
7
>>>
```

Tolken kan framför allt användas för att göra små kontroller. Du kan till exempel testa funktioner eller metoder – eller kolla om de existerar över huvud taget:

```python
>>> "teXt".toupper()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'str' object has no attribute 'toupper'
>>> "teXt".upper()
'TEXT'
>>>
```

Om det finns en metod som du behöver, och du minns ungefär vad dess namn är, kan det ibland vara snabbare att skippa Google och istället använda `dir`-funktionen i tolken. Funktionen berättar vilka metoder kan användas hos ett specifikt objekt:

```python
>>> dir("text")
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

Som du ser ovan, har strängar i Python en hel del metoder. För tillfället lönar det sig att ignorera metoder som har understreck i sina namn, men andra metoder kan visa sig vara nyttiga. Vissa får du kanske att fungera på egen hand, andra kan du söka mera information om på nätet.

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
>>> siffror = [1,2,3,4,5]
>>> siffror.reverse()
>>> siffror
[5, 4, 3, 2, 1]
>>> siffror.clear()
>>> siffror
[]
```

Som du kan notera, gör dessa metoder just det man skulle kunna anta.

Märk att tolken inte skriver ut någonting när du kör instruktionen `siffror.reverse()`. Detta beror på att tolken endast skriver ut något då kodraden returnerar ett värde. Metoden `reverse()` returnerar däremot inget värde, utan ändrar på ordningen i listan "in-place". Listan ändras, men det syns inte innan vi skriver ut den eller använder den på annat sätt. 

I det ovanstående exemplet skrev vi ut värdet på listan `siffror` med hjälp av namnet på variabeln. I tolken behöver man sällan använda sig av `print`-instruktionen. Det är däremot inte förbjudet att använda dem.

Kom ihåg att stänga tolken när du är klar. Kommandona `quit()` och `exit()` fungerar bra för det här ändamålet. Även tangentkombinationerna Control + D (Linux/Mac) och Control + Z (Windows) har samma funktion. Speciellt i Visual Studio Code är det här viktigt. Om du nämligen försöker köra ett annat Python-program medan tolken är igång, kommer du att få ett ganska konstigt felmeddelande:

<img src="4_1_4.png">

## Det inbyggda debuggningsverktyget

Vi har redan övat en hel del på att debugga – främst med hjälp av print-satser. Visual Studio Code erbjuder dig ett ytterligare verktyg för ändamålet: en inbyggd visuell debuggare.

För att börja debugga måste du lägga till en breakpoint – ett ställe där debuggaren stannar programkörningen. Du kan lägga till en breakpoint genom att klicka på det vänstra hörnet av vilken som helst kodrad i ditt program.

Det följande exemplet innehåller en icke-fungerande lösning på övningen Summan av påvarandra följande tal från den förra modulen. På rad fem finns en breakpoint:

<img src="4_1_5.png">

När breakpointen har skapats ska du välja Start debugging från Run-menyn. Det här öppnar en lista med alternativ av vilka du bör välja Python File:

<img src="4_1_6.png">

Det här startar debuggaren som kör din kod normalt tills vi kommer till breakpointen: här stannar körandet upp. Om koden ber om indata ska du minnas att mata in det i terminalen:

<img src="4_1_7.png">

Till vänster finns nu en Variables-vy som innehåller de nuvarande värdena på alla aktiva variabler i koden. Du kan fortsätta att köra koden rad för rad genom att klicka på den nedåtriktade pilen – Step into.

I den följande bilden har loopen i koden upprepats några gånger:

<img src="4_1_8.png">

Debuggaren har en Debug console -flik som låter dig köra uttryck med nuvarande variabelvärden. Du kan till exempel kolla värdet på Boolean-uttrycket som finns i loopens villkor:

<img src="4_1_9.png">

Du kan ha flera breakpoints i din kod. När programkörningen har stannat kan du starta den igen genom att klicka på den blå triangeln. Körandet fortsätter tills nästa breakpoint nås.

Den inbyggda visuella debuggaren är ett bra alternativ till debuggning med print-satser. Det är upp till dig själv vilken metod du använder dig av i fortsättningen. Alla programmerare har sina egna preferenser, men det är alltid en bra idé att testa på olika alternativ förrän man bestämmer sig för att göra på ett visst sätt.
