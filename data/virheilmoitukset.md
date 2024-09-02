---
path: "/felanmalningar"
title: "Vanliga felmeddelanden"
hidden: false
information_page: true
---

På den här sidan informerar vi om vanliga felmeddelanden som du kan stöta på när du programmerar.

### Uppgiften går inte igenom, trots att utskriften är identisk med exempelutskriften

Granska att ditt program inte skriver ut extra mellanslag. Observera att i `print`-funktionen skapar ett kommatecken automatiskt ett mellanslag mellan strängar.

```python
    print("Hello","World!")    # Skriver ut: Hello World!
```

### SyntaxError: bad input on line [radnummer]

Det här felmeddelandet inkluderar alla skrivfel som inte enkelt kan klassificeras. Vanliga exempel är villkorssatser som saknar kolon i slutet på raden, eller felskrivna nyckelord. Det enda sättet att lösa problemet är att undersöka den rad som felmeddelandet pekar på. 

```python
    tal1 = 1
    tal1 = 2
    if tal1 < tal2        # ':' saknas
        print('tal2 är större')
```

Ifall den angivna raden däremot ser helt rätt ut, kan det hända att felet finns på en tidigare eller senare rad. Granska särskilt raden som kommer före och den som kommer efter den angivna raden. 

### SyntaxError: unindent does not match any outer indentation level on line [radnummer]

Som felmeddelandet antyder, har något blivit fel med indenteringen. Kontrollera att instruktionen på den angivna raden är indenterad på rätt sätt, det vills säga i nivå med de övriga instruktionerna. Följande kod skulle till exempel ge upphov till den här typen av fel. 

```python
    if True:
        print('Rätt indenterat')
       print('Fel indenterat')
```

### NameError: name [variabel] is not defined on line [radnummer]

Detta fel uppstår när programmet försöker hänvisa till en variabel eller ett objekt som inte finns eller som inte 'syns'. Det kan hända att du har glömt att tilldela variabeln ett värde eller att variabeln inte hittas på grund av ett skrivfel (kolla exempel). Det kan också hända att variabeln är skapad innanför funktionen och därför är lokal – i sådana fall är variabeln inte synlig utanför funktionen. 

```python
    person = input('Skriv ditt namn: ')
    input('Skriv din ålder: ')

    print("Hej", persn)                   # fel: person skrivet persn
    print("Du är", alder, "år gammal")    # fel: variabeln alder är inte definierad
```

### TypeError: unsupported operand type(s) for Add: 'int' and 'str' on line [radnummer]

Det här felmeddelandet påpekar att programmet försöker addera ett heltal och en sträng, vilket inte är möjligt. För att det ska gå måste vi antingen först 1) omvandla strängen till ett heltal om vi vill utföra aritmetisk addition, eller 2) omvandla heltalet till en sträng om vi vill konkatenera två strängar. Kom alltså ihåg att omvandla värden till rätt typ med motsvarande funktion (t.ex. `str()` eller `int()`).

```python
    alder = input("Ange ålder: ")
    namn = input("Ange namn: ")

    print(alder//2)   # fel: input läser in data som strängar, och här har variabeln alder inte omvandlats till ett heltal
```

### TypeError: cannot concatenate 'str' and 'int' objects on line [radnummer]

Se ovanstående fel.
