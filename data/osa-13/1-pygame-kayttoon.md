---
path: '/osa-13/1-pygame-kayttoon'
title: 'Pygame'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Har du installerat pygame-biblioteket på din dator
- Vet du hur man skapar ett pygame-fönster och hur man avslutar ett program
- Kommer du att kunna använda en bild som lagras i en fil i ett pygame-fönster

</text-box>

I de här två sista delarna av kursmaterialet kommer vi att bekanta oss med pygame-biblioteket. Det är ett Python-bibliotek för programmering av spel. Det hjälper dig att skapa grafiska element, hantera händelser från tangentbordet och musen samt implementera andra funktioner som är nödvändiga i spel.

## Att installera pygame

### Linux

Öppna en instruktionsrad, skriv in `pip3 install pygame` och tryck på `enter`.

<img src="pygame_linux.png">

Detta borde installera pygame-biblioteket på din dator.

### Windows

Öppna Windows-terminalen genom att öppna menyn, skriva `cmd` och trycka på `enter`:

<img src="13_1_1.png">

Fönstret för kommandoradstolken borde öppnas. Skriv in `pip3 install pygame` och tryck på `enter`.

Detta borde installera pygame-biblioteket på din dator.

Installationen kan kräva systemadministratörsbehörighet. Om ovanstående inte fungerar kan du prova på att köra terminalprogrammet som administratör: öppna Windows-menyn, leta reda på CMD-programmet, högerklicka på det och välj "Kör som administratör".

För att installera och få åtkomst till pygame krävs att din Python-installation läggs till i sökvägen, enligt [instruktionerna](https://www.mooc.fi/fi/installation/vscode#python3) här.

### Mac

Öppna Terminalen, t.ex. genom förstoringsglas-symbolen i det övre högra hörnet:

<img src="13-1-2.png">

Sökverktyget borde öppna. Skriv in `terminal` och tryck `enter`:

<img src="13-1-3.png">

Skriv in följande och tryck `enter`:

`pip3 install pygame`

<img src="13-1-4.png">


Detta borde installera pygame-biblioteket på din dator.

## Ditt första program

Här är ett enkelt program för att kontrollera att din pygame-installation fungerar korrekt:

```python
import pygame

pygame.init()
fonster = pygame.display.set_mode((640, 480))

fonster.fill((0,0,0))
pygame.display.flip()

while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.QUIT:
            exit()
```

När detta program körs borde det visa ett fönster:

<img src="pygame_eka.gif">

Programmet visar endast ett fönster, och det körs tills användaren stänger fönstret.

Låt oss ta en närmare titt på de steg som krävs för att uppnå detta. Den första raden tar pygame-biblioteket i bruk: `import pygame`. Nästa instruktion, `pygame.init`, initierar pygame-modulerna, och nästa skapar ett fönster med funktionen `pygame.display.set_mode`.

```python
pygame.init()
fonster = pygame.display.set_mode((640, 480))
```

Funktionen `set_mode` tar fönstrets dimensioner som ett argument. Tupeln `(640, 480)` anger att fönstret är 640 pixlar brett och 480 pixlar högt. Variabelnamnet `fonster` kan senare användas för att komma åt fönstret, t.ex. för att rita något i det.

De följande två instruktionerna gör just detta:

```python
fonster.fill((0, 0, 0))
pygame.display.flip()
```

Metoden `fill` fyller fönstret med den färg som anges som argument. I det här fallet är färgen svart, som skickas som ett RGB-värde i tupeln `(0, 0, 0)`. Metoden `pygame.display.flip` uppdaterar innehållet i fönstret.

Efter dessa initialiseringsinstruktioner börjar programmets huvudloop:

```python
while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.QUIT:
            exit()
```

Huvudloopen hanterar alla händelser som operativsystemet skickar till programmet. Vid varje iteration returnerar funktionen `pygame.event.get` en lista över alla händelser som har samlats in sedan föregående iteration.

I exemplet ovan hanterar programmet endast händelser av typen `pygame.QUIT`. Denna händelse uppstår t.ex. genom att man klickar på exit-knappen i fönstrets hörn. Om händelsen `pygame.QUIT` utlöses avslutas programmet genom funktionen exit.

Du kan prova och se vad som händer om ditt program inte hanterar händelsen `pygame.QUIT`. Detta borde innebära att det inte händer någonting om man klickar på exit-knappen, vilket skulle vara förvirrande för användaren. Eftersom programmet körs från kommandoraden kan du fortfarande stoppa det från kommandoraden med Control+C.

## Lägg till en bild

Låt oss lägga till en bild i fönstret:

```python
import pygame

pygame.init()
fonster = pygame.display.set_mode((640, 480))

robot = pygame.image.load("robo.png")

fonster.fill((0, 0, 0))
fonster.blit(robot, (100, 50))
pygame.display.flip()

while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.QUIT:
            exit()
```

Programmet använder denna bild av en robot, som finns lagrad i filen `robot.png`:

<img src="robo.png">

Filen `robot.png` måste finnas i samma katalog som källkoden för ditt program, annars kan programmet inte hitta den. I övningsmallarna för denna del väntar bilderna i övningskatalogen.

Fönstret borde nu se ut så här:

<img src="pygame_kuva.gif">

Funktionen `pygame.image.load` laddar in bilden i filen `robot.png` och lagrar en referens till den i variabeln `robot`. Metoden `blit` ritar bilden på platsen `(100, 50)`, och funktionen `pygame.display.flip` uppdaterar fönstrets innehåll, som tidigare. Platsen `(100, 50)` innebär att bildens övre vänstra hörn befinner sig på den platsen i fönstret.

I pygame ligger origo-punkten `(0, 0)` i fönstrets övre vänstra hörn. X-koordinaterna ökar åt höger och y-koordinaterna ökar nedåt, så att det nedre högra hörnet har koordinaterna `(640, 480)`. Detta är tvärtemot hur koordinater brukar hanteras inom t.ex. matematiken, men det är ganska vanligt i programmeringssammanhang och värt att vänja sig vid.

När du har laddat en bild kan du använda den många gånger i samma fönster. I följande kod ritas bilden av roboten på tre olika platser:

```python
fonster.blit(robot, (0, 0))
fonster.blit(robot, (300, 0))
fonster.blit(robot, (100, 200))
```

Resultatet borde vara att fönstret ser ut så här:

<img src="pygame_kuva2.gif">

Här sätter vi lokationen av bilden så, att den ligger i mitten av fönstret:

```python
bredd = robot.get_width()
hojd = robot.get_height()
fonster.blit(robot, (320-bredd/2, 240-hojd/2))
```

Fönstret borde nu se ut så här:

<img src="pygame_kuva3.gif">

Metoden `get_width` ger bildens bredd och metoden `get_height` ger dess höjd, båda i pixlar. Fönstrets mittpunkt ligger på halva bredden och höjden, alltså på `(320, 240)`, vilket vi kan använda för att beräkna en lämplig plats för bildens övre vänstra hörn, så att det ligger exakt i mitten.

<text-box variant='hint' name='Pygame-övningar'>

Övningarna i den här delen av kursen har inga automatiserade tester, eftersom resultaten verifieras visuellt. Testerna ger poäng automatiskt när du skickar in din lösning till servern, oavsett hur du har implementerat den. Skicka bara in din lösning när du är redo och din lösning matchar övningsbeskrivningen. Övningarna kanske inte har automatiska tester, men kurspersonalen kommer ändå att se din lösning. Att skicka in en ofullständig lösning till TMC Paste ger också poäng automatiskt, så det bör inte användas när du ber om hjälp med övningarna i den här delen. Du kan använda [Pastebin.com](https://pastebin.com/) eller någon annan pastebin-tjänst på internet när du ber om hjälp i kursens stödkanaler.

Om din lösning helt klart inte stämmer överens med övningsbeskrivningen kan du förlora de poäng som du har fått för övningarna i den här delen. 

</text-box>


<programming-exercise name='Neljä robottia' tmcname='osa13-01_nelja_robottia'>

Skriv ett program som ritar en robot i vart och ett av de fyra hörnen av fönstret. Slutresultatet ska se ut så här:

<img src="pygame_nelja.gif">

</programming-exercise>

<programming-exercise name='Robotit rivissä' tmcname='osa13-02_robotit_rivissa'>

Skriv ett program som ritar tio robotar i rad. Slutresultatet ska se ut så här:

<img src="pygame_rivi.gif">

</programming-exercise>

<programming-exercise name='Sata robottia' tmcname='osa13-03_sata_robottia'>

Var snäll och skriv ett program som ritar hundra robotar: tio rader med tio robotar i varje rad. Slutresultatet ska se ut så här:

<img src="pygame_sata.gif">

</programming-exercise>

<programming-exercise name='Satunnaiset robotit' tmcname='osa13-04_satunnaiset_robotit'>

Skriv ett program som ritar _tusen_ robotar på slumpmässiga platser. Slutresultatet ska se ut så här:

<img src="pygame_tuhat.gif">

</programming-exercise>
