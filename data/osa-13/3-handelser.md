---
path: '/osa-13/3-handelser'
title: 'Händelser'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Kommer du att vara bekant med pygame händelser
- Kommer du att kunna skriva ett program som reagerar på tangenttryckningar
- Kommer du att kunna skriva ett program som reagerar på mushändelser

</text-box>

Hittills har våra huvudloopar bara kört förutbestämda animationer och reagerat på händelser av typen `pygame.QUIT`, trots att loopen får en lista över alla händelser från operativsystemet. Låt oss nu ta itu med några andra typer av händelser.

## Hantering av händelser

Det här programmet skriver ut information om alla händelser som skickas från operativsystemet till programmet pygame, medan det körs:

```python
import pygame

pygame.init()
fonster = pygame.display.set_mode((640, 480))

while True:
    for handelse in pygame.event.get():
        print(handelse)
        if handelse.type == pygame.QUIT:
            exit()
```

Låt oss anta att programmet kördes ett tag och att man sedan klickade på avslutningsknappen. Programmet skriver ut följande information:

```x
<Event(4-MouseMotion {'pos': (495, 274), 'rel': (495, 274), 'buttons': (0, 0, 0), 'window': None})>
<Event(4-MouseMotion {'pos': (494, 274), 'rel': (-1, 0), 'buttons': (0, 0, 0), 'window': None})>
<Event(4-MouseMotion {'pos': (492, 274), 'rel': (-2, 0), 'buttons': (0, 0, 0), 'window': None})>
<Event(4-MouseMotion {'pos': (491, 274), 'rel': (-1, 0), 'buttons': (0, 0, 0), 'window': None})>
<Event(5-MouseButtonDown {'pos': (491, 274), 'button': 1, 'window': None})>
<Event(6-MouseButtonUp {'pos': (491, 274), 'button': 1, 'window': None})>
<Event(2-KeyDown {'unicode': 'a', 'key': 97, 'mod': 0, 'scancode': 38, 'window': None})>
<Event(3-KeyUp {'key': 97, 'mod': 0, 'scancode': 38, 'window': None})>
<Event(2-KeyDown {'unicode': 'b', 'key': 98, 'mod': 0, 'scancode': 56, 'window': None})>
<Event(3-KeyUp {'key': 98, 'mod': 0, 'scancode': 56, 'window': None})>
<Event(2-KeyDown {'unicode': 'c', 'key': 99, 'mod': 0, 'scancode': 54, 'window': None})>
<Event(3-KeyUp {'key': 99, 'mod': 0, 'scancode': 54, 'window': None})>
<Event(12-Quit {})>
```

De första händelserna gäller musanvändningen, därefter kommer några händelser från tangentbordet och slutligen stänger den sista händelsen programmet. Varje händelse har åtminstone en typ, men de kan också innehålla annan identifierande information, till exempel var muspekaren befinner sig eller vilken tangent som trycktes in.

Du kan leta efter händelsebeskrivningar i pygame-dokumentationen, men det kan ibland vara enklare att skriva ut händelser med koden ovan och leta efter den händelse som inträffar när något du vill reagera på händer.

## Tangentbordshändelser

Detta program kan behandla händelser där användaren trycker på piltangenten antingen till höger eller till vänster på sitt tangentbord. Programmet skriver ut vilken tangent som trycktes in.

```python
import pygame

pygame.init()
fonster = pygame.display.set_mode((640, 480))

while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.KEYDOWN:
            if handelse.key == pygame.K_LEFT:
                print("vänster")
            if handelse.key == pygame.K_RIGHT:
                print("höger")

        if handelse.type == pygame.QUIT:
            exit()
```

Konstanterna `pygame.K_LEFT` och `pygame.K_RIGHT` avser piltangenterna till vänster och höger. Konstanterna för pygame-tangenterna för de olika tangenterna på ett tangentbord anges i [Pygame dokumentationen](https://www.pygame.org/docs/ref/key.html#key-constants-label).

Om användaren t.ex. trycker på piltangenten till höger två gånger, sedan den vänstra en gång och sedan den högra en gång till, skriver programmet ut

```x
höger
höger
vänster
höger
```

Vi har nu alla verktyg som behövs för att flytta en karaktär, eller sprite, på skärmen till höger och vänster med piltangenterna. Följande kod kommer att uppnå detta:

```python
import pygame

pygame.init()
fonster = pygame.display.set_mode((640, 480))

robot = pygame.image.load("robot.png")
x = 0
y = 480-robot.get_height()

while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.KEYDOWN:
            if handelse.key == pygame.K_LEFT:
                x -= 10
            if handelse.key == pygame.K_RIGHT:
                x += 10

        if handelse.type == pygame.QUIT:
            exit()

    fonster.fill((0, 0, 0))
    fonster.blit(robot, (x, y))
    pygame.display.flip()
```

Beroende på hur du använder piltangenterna kunde programmet köra på följande sätt:

<img src="pygame_liikutus.gif">

I koden ovan har vi variablerna `x` och `y` som innehåller sprite-koordinaterna. Variabeln `y` är inställd så att spriten visas längst ned i fönstret. Värdet för `y` ändras inte under hela körningen av programmet. `x`-värdet ökar däremot med 10 när användaren trycker på piltangenten till höger och minskar med 10 när användaren trycker på piltangenten till vänster.

Programmet fungerar i övrigt ganska bra, men tangenten måste tryckas in igen varje gång vi vill förflytta oss igen. Det skulle vara bättre om rörelsen var kontinuerlig när tangenten hölls nedtryckt. Följande program erbjuder denna funktionalitet:

```python
import pygame

pygame.init()
fonster = pygame.display.set_mode((640, 480))

robot = pygame.image.load("robot.png")
x = 0
y = 480-robot.get_height()

hoger = False
vanster = False

klocka = pygame.time.Clock()

while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.KEYDOWN:
            if handelse.key == pygame.K_LEFT:
                vanster = True
            if handelse.key == pygame.K_RIGHT:
                hoger = True

        if handelse.type == pygame.KEYUP:
            if handelse.key == pygame.K_LEFT:
                vanster = False
            if handelse.key == pygame.K_RIGHT:
                hoger = False

        if handelse.type == pygame.QUIT:
            exit()

    if hoger:
        x += 2
    if vanster:
        x -= 2

    fonster.fill((0, 0, 0))
    fonster.blit(robot, (x, y))
    pygame.display.flip()

    klocka.tick(60)
```

Koden innehåller nu variablerna `hoger` och `vanster`. Dessa innehåller vetskap om huruvida spriten ska röra sig åt höger eller vänster vid ett givet tillfälle. När användaren trycker ner en piltangent blir värdet som lagras i den relevanta variabeln `True`. När tangenten släpps ändras värdet till `False`.

Klockan används för att tidsbestämma spritens rörelser, så att de potentiellt sker 60 gånger per sekund. Om en piltangent trycks ned förflyttas spriten två pixlar åt höger eller vänster. Detta innebär att spriten rör sig 120 pixlar per sekund om tangenten hålls nedtryckt.

<programming-exercise name='Fyra riktningar' tmcname='osa13-11_fyra_riktningar'>

Skriv ett program där spelaren kan flytta en robot i fyra riktningar med piltangenterna på tangentbordet. Slutresultatet ska se ut så här:

<img src="pygame_nelja_suuntaa.gif">

</programming-exercise>

<programming-exercise name='Fyra väggar' tmcname='osa13-12_fyra_vaggar'>

Förbättra programmet i den föregående övningen så att roboten inte kan passera utanför fönstret i någon av de fyra riktningarna. Slutresultatet ska se ut så här:

<img src="pygame_nelja_seinaa.gif">

</programming-exercise>

<programming-exercise name='Två spelare' tmcname='osa13-13_tva_spelare'>

Skriv ett program där två spelare styr var sin robot. En av spelarna ska använda piltangenterna medan den andra kan använda t.ex. w-a-s-d-tangenterna. Slutresultatet ska se ut så här:

<img src="pygame_kaksi_pelaajaa.gif">

</programming-exercise>

## Händelser med musen

Följande kod reagerar på händelser där en musknapp trycks ned medan markören befinner sig inom fönsterområdet:

```python
import pygame

pygame.init()
fonster = pygame.display.set_mode((640, 480))

while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.MOUSEBUTTONDOWN:
            print("du tryckte knappen", handelse.button, "på lokationen", handelse.pos)

        if handelse.type == pygame.QUIT:
            exit()
```

Exekveringen av detta program borde mer eller mindre se ut så här:

```x
du tryckte knappen 1 på lokationen (82, 135)
du tryckte knappen 1 på lokationen (369, 135)
du tryckte knappen 1 på lokationen (269, 297)
du tryckte knappen 3 på lokationen (515, 324)
```

Knapp nummer 1 avser vänster musknapp och knapp nummer 3 avser höger musknapp.

Nästa program kombinerar hantering av mushändelser och ritning av en bild på skärmen. När användaren trycker på en musknapp medan muspekaren befinner sig inom fönstrets gränser ritas en bild av en robot på den platsen.

```python
import pygame

pygame.init()
fonster = pygame.display.set_mode((640, 480))

robot = pygame.image.load("robot.png")

while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.MOUSEBUTTONDOWN:
            x = handelse.pos[0]-robot.get_width()/2
            y = handelse.pos[1]-robot.get_height()/2

            fonster.fill((0, 0, 0))
            fonster.blit(robot, (x, y))
            pygame.display.flip()

        if handelse.type == pygame.QUIT:
            exit()
```

Exekveringen av programmet borde se ut så här:

<img src="pygame_hiiri.gif">

Följande program innehåller en animation där robotspriten följer muspekaren. Spritens position lagras i variablerna `robot_x` och `robot_y`. När musen rör sig lagras dess position i variablerna `mal_x` och `mal_y`. Om roboten inte befinner sig på denna plats förflyttar den sig i lämplig riktning.

```python
import pygame

pygame.init()
fonster = pygame.display.set_mode((640, 480))

robot = pygame.image.load("robot.png")

robot_x = 0
robot_y = 0
mal_x = 0
mal_y = 0

klocka = pygame.time.Clock()

while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.MOUSEMOTION:
            mal_x = handelse.pos[0]-robot.get_width()/2
            mal_y = handelse.pos[1]-robot.get_height()/2

        if handelse.type == pygame.QUIT:
            exit(0)

    if robot_x > mal_x:
        robot_x -= 1
    if robot_x < mal_x:
        robot_x += 1
    if robot_y > mal_y:
        robot_y -= 1
    if robot_y < mal_y:
        robot_y += 1

    fonster.fill((0, 0, 0))
    fonster.blit(robot, (robot_x, robot_y))
    pygame.display.flip()

    klocka.tick(60)
```

Exekveringen av programmet borde se ut så här:

<img src="pygame_hiiri2.gif">

<programming-exercise name='Roboten och musen' tmcname='osa13-14_roboten_och_musen'>

Skriv ett program där roboten följer muspekaren så att robotens mittpunkt alltid är direkt vid muspekaren. Slutresultatet ska se ut så här:

<img src="pygame_robotti_hiiri.gif">

</programming-exercise>

<programming-exercise name='Robotens plats' tmcname='osa13-15_robotens_plats'>

Skriv ett program där roboten dyker upp på en slumpmässig plats i fönstret. När spelaren klickar på roboten med musen förflyttar sig roboten till en ny plats. Slutresultatet ska se ut så här:

<img src="pygame_robotti_paikka.gif">

</programming-exercise>
