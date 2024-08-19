---
path: "/felanmalningar"
title: "Allmänna felanmälningar"
hidden: false
information_page: true
banner: true
separator_after: "Ohjelmoinnin perusteet"
---

På den här sidan berrätas om allänna felanmälningar vilka du kan stöta på under kursen.

### Uppgiften går inte igenom, trots att utskriften är identisk med exempelutskriften

Granska att ditt program inte skriver ut extra mellanslag. Märk att innanför `print` -funktionen skapar ett kommatecken automatiskt ett mellanslag mellan strängar.

```python
    print("Hello","World!")    # Skriver ut: Hello World!
```

### SyntaxError: bad input on line [radnummer]

Detta behandlar alla sådana skrivfel i koden som inte kan klassifieras enkelt. Till exempel en villkorssats kan sakna ett kolon i slutet eller ett nyckelord såsom 'while' kan vara skrivet fel. Enda sättet att lösa problemet är att undersöka felanmälans angivna rader.

```python
    tal1 = 1
    tal1 = 2
    if tal1 < tal2        # ':' saknas
        print('tal2 är större')
```

Ifall den angivna raden däremot ser helt rätt ut, kan det även hända att felet är en rad nedanför eller ovanför. Granska alltså även de raderna.

### SyntaxError: unindent does not match any outer indentation level on line [radnummer]

Koden är indenterad konstigt på felanmälans angivna rad. Indentera rad så att den är i nivå med resten av raderna. Till exempel följande kod åstadkommer ett sådant här fel.

```python
    if True:
        print('Rätt indenterat')
       print('Fel indenterat')
```

### NameError: name [variabel] is not defined on line [radnummer]

Koden försöker referera till en variabel eller ett objekt som inte finns eller som inte 'syns'. Det kan hända att variabeln har glömts att tilldelas ett värde eller att variabeln inte hittas på grund av ett skrivfel (kolla exempel). Det kan också hända att variabeln är skapad innanför funktionen och försöker refereras till ytterom funktionen.

```python
    person = input('Skriv ditt namn: ')
    input('Skriv din ålder: ')

    print("Hej", persn)                   # fel: person skrivet persn
    print("Du är", alder, "år gammal")    # fel: variabeln alder är inte definierad
```

### TypeError: unsupported operand type(s) for Add: 'int' and 'str' on line [radnummer]

Koden försöker räkna ihop ett heltal och en sträng utan att strängen är ändrad till ett heltal. Kom alltså ihåg att ändra strängar med `int()` -funktionen. Det kan också hända att den försökte slå ihop ett heltal till en sträng. För detta måste du ändra heltalet till en sträng med `str()` -metoden.

```python
    alder = input("Ange ålder: ")
    namn = input("Ange namn: ")

    print(alder//2)   # fel: variabeln alder är inte ändrat till ett heltal
```

### TypeError: cannot concatenate 'str' and 'int' objects on line [radnummer]

Se ovanstående del.
