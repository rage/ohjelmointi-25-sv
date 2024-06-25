---
path: '/osa-7/6-funktionaliteter-python'
title: 'Flera funktionaliteter i Python'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* har du bekantat dig med några fler funktionaliteter i Python.

</text-box>

För att knyta ihop den här kursen, ska du ännu få en lista av nyttiga funktionaliteter som Python har att erbjuda.

## If-satser på en rad

Följande satser ger samma resultat:

```python
if x%2 == 0:
    print("jämn")
else:
    print("ojämn")
```

```python
print("jämn" if x%2 == 0 else "ojämn")
```

I det senare exemplet har vi en if-sats i enradsformat: `a if [villkor] else b`. Värdet för uttrycket blir `a` då villkoret är sant och `b` i övriga fall. På engelska kallas detta ternary operator.

If-satser kan användas då man vill tilldela något värde baserat på ett villkor. Till exempel om du har variablerna `x` och `y` och vill antingen öka eller ändra på `y`:s värde baserat på `x` paritet (jämnt/udda tal), kan du använda en normal if-else-sats:

```python
if x%2 == 0:
    y += 1
else:
    y = 0
```

Eller så kan du göra det hela med en rad kod:

```python
y = y + 1 if x%2 == 0 else 0
```

## Ett "tomt" block

Du minns kanske att block inte kan vara tomma i Python. Om du behöver ett block som inte gör någonting – till exempel då du testar någon annan funktionalitet – kan du använda `pass`-instruktionen. Du kan till exempel skapa en funktion som inte gör någonting:

```python
def test():
    pass
```

Funktionen kommer att returnera direkt. Om `pass`-instruktionen lämnas bort, kommer koden att ge ett fel, eftersom block inte kan vara tomma.

```python
def test():
```

## Loopar med else-block

I Python kan loopar också ett `else`-block. Koden inom det här blocket körs då loopen avslutas normalt.

Till exempel här går vi igenom en lista med siffror. Om det finns ett jämnt tal i listan, kommer ett meddelande att skrivas ut och loopen avslutas. Om det inte finns några jämna tal, kommer loopen att avslutas vanligt, men ett annat meddelande skrivs ut:

```python
lista = [3,5,2,8,1]
for x in lista:
    if x%2 == 0:
        print("hittade jämnt tal", x)
        break
else:
    print("hittade inte jämnt tal")
```

Ett mera traditionellt sätt att göra det här är att använda en hjälpvariabel som minns om en viss typ av element har hittats:

```python
lista = [3,5,2,8,1]
hittades = False
for x in lista:
    if x%2 == 0:
        print("hittade jämnt tal", x)
        hittades = True
        break
if not hittades:
    print("hittade inte jämnt tal")
```

Att använda en for-else-sats sparar oss den tid som skulle krävas för att skapa en hjälpvariabel och logiken kring den.

## Standardvärde för en parameter

I Python kan funktioners parametrar ha ett standardvärde. Det används då ett argument inte ges till en funktion då den anropas. Se följande exempel:

```python
def tervehdi(nimi="Emilia"):
    print("Hej,", nimi)

tervehdi()
tervehdi("Elin")
tervehdi("Malin")
```

<sample-output>

Hej, Emilia
Hej, Elin
Hej, Malin

</sample-output>

Obs! En tom sträng är fortfarande en sträng. Standardvärdet kommer inte att användas om en tom sträng ges som argument till en funktion.

## Ändrande antal parametrar

Du kan också definiera att en funktion har ett ändrande antal parametrar, genom att lägga till en asterisk för parameternamnet. Alla argument som ges till funktionen lagras i en tuple som kan kommas åt genom den namngivna parametern.

Följande funktion räknar antalet argument som getts samt summan av dem:

```python
def test(*lista):
    print("Du gav", len(lista), "argument")
    print("Deras summa är", sum(lista))

test(1, 2, 3, 4, 5)
```

<sample-output>

Du gav 5 argument
Deras summa är 15

</sample-output>

<programming-exercise name='Eget programmeringsspråk' tmcname='osa07-18_programmeringssprak'>

I den här uppgifter skapar vi ett program som kan köra vårt eget programmeringsspråk. Du kan använda allt du lärt dig under den här kursen när du utför den här uppgiften.

Programmen består av rader, som kan följa något av dessa format:

* `PRINT [värde]`: skriver ut det givna värdet
* `MOV [variabel] [värde]`: tilldelar variabeln det givna värdet
* `ADD [variabel] [värde]`: adderar till den givna variabeln
* `SUB [variabel] [värde]`: subtraherar från den givna variabeln
* `MUL [variabel] [värde]`: multiplicerar den givna variabeln
* `[ställe]:`: definierar ett ställe dit man senare kan förflyttas till
* `JUMP [ställe]`: gå till specificerat ställe
* `IF [villkor] JUMP [ställe]`: om villkoret är sant, gå till specificerat ställe
* `END`: avslutar programmet

Programmet körs rad för rad från och med den första raden. Programmet avslutas vid `END` eller då den sista raden passeras.

Programmet har 26 variabler (`[variabel]`) namngivna `A` till `Z`. Alla variabler är 0 då programmet startar.

Alla värden som behandlas är helta. `[värde]` hänvisar till en variabel eller ett givet heltal.

Ett `[ställe]` består av bokstäverna `a` till `z` och siffrorna 0-9. Olika ställen kan inte ha samma namn.

`[villkor]` ges i formatet `[värde] [jämförelse] [värde]`. `[jämförelse]` är något av de följande: `==`, `!=`, `<`, `<=`, `>` eller `>=`.

Skapa funktionen `kor(program)` som tar emot programmet som en lista. Ett element i listan representerar en rad kod. Funktionen ska returnera resultaten från alla `PRINT`-instruktioner.

Du kan anta att det program som ges till funktionen har korrekt syntax. Funktionen behöver inte alltså kunna behandla sådana här fel.

Du kan få två poäng av den här uppgiften: ett poäng om instruktionerna `PRINT`, `MOV`, `ADD`, `SUB`, `MUL` och `END` fungerar, och ett poäng om resterande instruktioner fungerar.

Exempel 1:

```python
program1 = []
program1.append("MOV A 1")
program1.append("MOV B 2")
program1.append("PRINT A")
program1.append("PRINT B")
program1.append("ADD A B")
program1.append("PRINT A")
program1.append("END")
resultat = kor(program1)
print(resultat)
```

<sample-output>

[1, 2, 3]

</sample-output>

Exempel 2:

```python
program2 = []
program2.append("MOV A 1")
program2.append("MOV B 10")
program2.append("start:")
program2.append("IF A >= B JUMP slut")
program2.append("PRINT A")
program2.append("PRINT B")
program2.append("ADD A 1")
program2.append("SUB B 1")
program2.append("JUMP start")
program2.append("slut:")
program2.append("END")
resultat = kor(program2)
print(resultat)
```

<sample-output>

[1, 10, 2, 9, 3, 8, 4, 7, 5, 6]

</sample-output>

Exempel 3 (fakultet):

```python
program3 = []
program3.append("MOV A 1")
program3.append("MOV B 1")
program3.append("start:")
program3.append("PRINT A")
program3.append("ADD B 1")
program3.append("MUL A B")
program3.append("IF B <= 10 JUMP start")
program3.append("END")
resultat = kor(program3)
print(resultat)
```

<sample-output>

[1, 2, 6, 24, 120, 720, 5040, 40320, 362880, 3628800]

</sample-output>

Exempel 4 (primtal):

```python
program4 = []
program4.append("MOV N 50")
program4.append("PRINT 2")
program4.append("MOV A 3")
program4.append("start:")
program4.append("MOV B 2")
program4.append("MOV Z 0")
program4.append("test:")
program4.append("MOV C B")
program4.append("nytt:")
program4.append("IF C == A JUMP fel")
program4.append("IF C > A JUMP skippa")
program4.append("ADD C B")
program4.append("JUMP nytt")
program4.append("fel:")
program4.append("MOV Z 1")
program4.append("JUMP skippa2")
program4.append("skippa:")
program4.append("ADD B 1")
program4.append("IF B < A JUMP test")
program4.append("skippa2:")
program4.append("IF Z == 1 JUMP skippa3")
program4.append("PRINT A")
program4.append("skippa3:")
program4.append("ADD A 1")
program4.append("IF A <= N JUMP start")
resultat = kor(program4)
print(resultat)
```

<sample-output>

[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]

</sample-output>

</programming-exercise>

Vänligen svara på kursfeedbacksenkäten här nedan. Enkätens resultat hjälper oss att utveckla och förbättra den här kursen.

<quiz id="e5513330-0599-5fa0-bfd0-a2d40a89773e"></quiz>
