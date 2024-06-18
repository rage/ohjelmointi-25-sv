---
path: '/osa-13/2-animaatio'
title: 'Animation'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Vet du hur man skapar en animation med pygame
- Kommer du att kunna använda en klocka för att ställa in hastigheten på ditt program
- Kommer du att kunna använda grundläggande trigonometriska funktioner i dina animationer

</text-box>

Många spel har rörliga karaktärer, så ett logiskt nästa steg är att skapa animationer. Vi kan skapa en illusion av rörelse genom att rita samma bild på olika ställen på skärmen och tajma ändringarna på rätt sätt.

## Skapa en animation

Följande kod skapar en animation där en robot rör sig från vänster till höger i ett pygame-fönster:

```python
import pygame

pygame.init()
fonster = pygame.display.set_mode((640, 480))

robot = pygame.image.load("robo.png")

x = 0
y = 0
klocka = pygame.time.Clock()

while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.QUIT:
            exit()

    fonster.fill((0, 0, 0))
    fonster.blit(robot, (x, y))
    pygame.display.flip()

    x += 1
    klocka.tick(60)
```

När detta exekveras, borde resultatet se ut så här:

<img src="pygame_animaatio.gif">

Låt oss ta en närmare titt på de instruktioner som är inblandade. Om vi vill spåra bildens rörelse på skärmen måste vi veta var den befinner sig. Därför har vi två variabler för koordinaterna för bildens övre vänstra hörn:

```python
x = 0
y = 0
```

Vi har även en klocka, som vi använder för att se till att animationens hastighet är korrekt:

```python
klocka = pygame.time.Clock()
```

Huvudloopen ritar bilden på sin aktuella plats vid varje iteration:

```python
    fonster.fill((0, 0, 0))
    fonster.blit(robot, (x, y))
    pygame.display.flip()
```

Först fyller metoden fill fönstret med svart, precis som tidigare. Färgen skickas som en tupel som innehåller RGB-värdena för färgen. I det här fallet är argumentet `(0, 0, 0)`, vilket innebär att alla tre komponenterna - röd, grön och blå - har värdet 0. Varje komponent kan ha ett värde mellan 0 och 255. Om vi skickar `(255, 255, 255)` som argument får vi alltså ett vitt fönster, och med `(255, 0, 0)` får vi ett rött fönster. RGB-färgkoder utgör ryggraden i digital färgläggning, och det finns många verktyg online för att arbeta med dem, till exempel [RGB Color Codes Chart](https://www.rapidtables.com/web/color/RGB_Color.html).

När fönstret har fyllts med färg ritas bilden på den angivna platsen med blit-metoden. Sedan uppdateras innehållet i fönstret med funktionen `pygame.display.flip`.

Slutligen ökas värdet som lagras i x, vilket gör att bilden flyttas en pixel åt höger för varje iteration:

```python
    x += 1
```

Klock-metoden `tick` kallas i slutet:

```python
    klocka.tick(60)
```

Metoden `tick` tar hand om hastigheten på animationen. Argumentet 60 anger att loopen ska exekveras `60` gånger per sekund, vilket innebär att bilden förflyttas 60 pixlar åt höger varje sekund. Detta motsvarar ungefär det värde för FPS eller bilder per sekund som används i spel.

I princip ser `tick`-metoden till att animationen körs med samma hastighet på alla datorer. Om det inte fanns någon sådan timing skulle animationens hastighet bero på datorns hastighet.

## Studsa av en vägg

Den föregående animationen var annars utmärkt, men när roboten nådde en vägg fortsatte den bara att försvinna ur syn. Låt oss få roboten att studsa mot väggen.

```python
import pygame

pygame.init()
fonster = pygame.display.set_mode((640, 480))

robot = pygame.image.load("robo.png")

x = 0
y = 0
hastighet = 1
klocka = pygame.time.Clock()

while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.QUIT:
            exit()

    fonster.fill((0, 0, 0))
    fonster.blit(robot, (x, y))
    pygame.display.flip()

    x += hastighet
    if hastighet > 0 and x+robot.get_width() >= 640:
        hastighet = -hastighet
    if hastighet < 0 and x <= 0:
        hastighet = -hastighet

    klocka.tick(60)
```

Exekvering av koden ovan borde se ut så här:

<img src="pygame_animaatio2.gif">

Det finns en ny variabel, `hastighet`, som bestämmer rörelseriktningen. Om värdet är över noll sker förflyttningen åt höger och om det är under noll sker förflyttningen åt vänster. I det här fallet rör sig roboten åt höger om värdet är `1`, åt vänster om värdet är `-1`.

Följande rader gör att roboten studsar mot sidoväggarna:

```python
    if hastighet > 0 and x+robot.get_width() >= 640:
        hastighet = -hastighet
    if hastighet < 0 and x <= 0:
        hastighet = -hastighet
```

Om hastigheten är över noll så att roboten rör sig åt höger, och högerkanten på bilden går utanför fönstrets högra kant, vänds riktningen och roboten börjar röra sig åt vänster. På samma sätt, om hastigheten är under noll så att roboten rör sig åt vänster, och bildens vänstra kant når fönstrets vänstra kant, vänds riktningen igen och roboten börjar röra sig åt höger igen.

Detta gör att roboten rör sig på en bana från fönstrets vänstra kant till den högra kanten, och tillbaka till vänster, och sedan till höger igen, upprepat i all oändlighet.

## Rotation

Låt oss skapa ytterligare en animation. Den här gången ska roboten rotera i en cirkel runt fönstrets mitt:

```python
import pygame
import math

pygame.init()
fonster = pygame.display.set_mode((640, 480))

robot = pygame.image.load("robo.png")

vinkel = 0
klocka = pygame.time.Clock()

while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.QUIT:
            exit()

    x = 320+math.cos(vinkel)*100-robot.get_width()/2
    y = 240+math.sin(vinkel)*100-robot.get_height()/2

    fonster.fill((0, 0, 0))
    fonster.blit(robot, (x, y))
    pygame.display.flip()

    vinkel += 0.01
    klocka.tick(60)
```

Exekvering av koden ovan borde se ut så här:

<img src="pygame_pyorinta.gif">

Rotation i en relativt exakt cirkel uppnås med hjälp av några grundläggande trigonometriska funktioner. Variabeln `vinkel` innehåller vinkeln för robotens position i förhållande till fönstrets mittpunkt och den horisontella linjen som går genom fönstret. Sinus- och cosinusfunktionerna från Pythons matematikbibliotek används här för att beräkna koordinaterna för robotens position:

```python
        x = 320+math.cos(vinkel)*100-robot.get_width()/2
        y = 240+math.sin(vinkel)*100-robot.get_height()/2
```

Roboten roterar runt en cirkel med radien 100 runt fönstrets mittpunkt. Hypotenusan i detta scenario är cirkelns radie. Cosinusfunktionen anger längden på den angränsande sidan i en rätvinklig triangel i förhållande till hypotenusan, vilket innebär att den ger oss platsens `x`-koordinat. Sinusfunktionen ger längden på den motsatta sidan, dvs. `y`-koordinaten. Platsen justeras sedan för bildens storlek, så att cirkelns mittpunkt ligger i fönstrets mittpunkt.

För varje iteration ökar storleken på `vinkel` med 0,01. Eftersom vi använder radianer är en hel cirkel 2π, vilket motsvarar ca 6,28. Det tar cirka 628 iterationer för roboten att gå en hel cirkel, och med 60 iterationer per sekund tar detta drygt 10 sekunder. 

<programming-exercise name='Pystyliike' tmcname='osa13-05_pystyliike'>

Skapa en animation där roboten rör sig upp och ner i en ändlös loop. Slutresultatet ska se ut så här:

<img src="pygame_pysty.gif">

</programming-exercise>

<programming-exercise name='Reunan kierto' tmcname='osa13-06_reunan_kierto'>

Skapa en animation där roboten följer fönstrets omkrets. Slutresultatet ska se ut så här:

<img src="pygame_kierto.gif">

</programming-exercise>

<programming-exercise name='Kaksi robottia' tmcname='osa13-07_kaksi_robottia'>

Skapa en animation där två robotar rör sig fram och tillbaka till vänster och höger. Den nedre roboten ska röra sig med dubbelt så hög hastighet som den övre. Slutresultatet ska se ut så här:

<img src="pygame_liike2.gif">

</programming-exercise>

<programming-exercise name='Piirileikki' tmcname='osa13-08_piirileikki'>

Skapa en animation där tio robotar går runt i en cirkel. Slutresultatet ska se ut så här:

<img src="pygame_piiri.gif">

</programming-exercise>

<programming-exercise name='Pomppiva pallo' tmcname='osa13-09_pomppiva_pallo'>

Skapa en animation där en boll studsar från fönstrets kanter. Slutresultatet ska se ut så här:

<img src="pygame_pallo.gif">

Övningsmallen innehåller bilden `pallo.png`.

</programming-exercise>

<programming-exercise name='Robotti-invaasio' tmcname='osa13-10_robotti_invaasio'>

Skapa en animation där robotar faller från himlen slumpmässigt. När en robot når marken börjar den röra sig åt vänster eller höger och försvinner till slut från skärmen. Slutresultatet ska se ut så här:

<img src="pygame_invaasio.gif">

</programming-exercise>
