---
path: '/osa-13/4-fler-pygame-tekniker'
title: 'Fler pygame-tekniker'
hidden: false
---

<text-box variant='learningObjectives' name='Inlärningsmål'>

Efter den här delen

- Kommer du att veta hur man titlar pygame-fönstret
- Kommer du att kunna rita former med pygame
- Kommer du att veta hur du visar text i ditt fönster

</text-box>

## Fönstrets titel

Dina program kommer att se mer professionella ut om fönstertiteln istället för "pygame window" innehåller det faktiska namnet på programmet. Titeln ställs in med funktionen `pygame.display.set_caption`:

```python
pygame.display.set_caption("Det stora äventyret")
```

## Att rita former

Följande program ritar en rektangel, en cirkel och en linje på skärmen:

```python
import pygame

pygame.init()
fonster = pygame.display.set_mode((640, 480))
fonster.fill((0, 0, 0))

pygame.draw.rect(fonster, (0, 255, 0), (50, 100, 200, 250))
pygame.draw.circle(fonster, (255, 0, 0), (200, 150), 40)
pygame.draw.line(fonster, (0, 0, 255), (80, 120), (300, 160), 2)

pygame.display.flip()

while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.QUIT:
            exit()
```

Körning av koden ovan borde se ut enligt följande:

<img src="pygame_kuviot.gif">

## Att rita text

Text i pygame ritas i två steg: först skapar vi en bild som innehåller den önskade texten, och sedan ritas denna bild på skärmen. Det fungerar på följande sätt:

```python
import pygame

pygame.init()
fonster = pygame.display.set_mode((640, 480))
fonster.fill((0, 0, 0))

font = pygame.font.SysFont("Arial", 24)
text = font.render("<Moikka!>", True, (255, 0, 0))
fonster.blit(text, (100, 50))
pygame.display.flip()

while True:
    for handelse in pygame.event.get():
        if handelse.type == pygame.QUIT:
            exit()
```

Körning av koden ovan borde se ut enligt följande:

<img src="pygame_teksti.gif">

Här skapar metoden `pygame.font.SysFont` ett typsnittsobjekt, som använder systemtypsnittet Arial i storlek 24. Metoden `render` skapar sedan en bild av den angivna texten i den angivna färgen. Denna bild ritas på fönstret med metoden `blit`, precis som tidigare.

OBS: olika system kommer att ha olika teckensnitt tillgängliga. Om det system som det här programmet körs på inte har teckensnittet Arial, trots att Arial är ett mycket vanligt teckensnitt som finns på de flesta system, används istället systemets standardteckensnitt. Om du behöver ha ett specifikt teckensnitt tillgängligt för ditt spel kan du inkludera teckensnittsfilen i spelkatalogen och ange dess plats för metoden `pygame.font.Font`.

## Övningar

Här är några mer avancerade övningar för att öva på det du har lärt dig i denna del av kursmaterialet.

<programming-exercise name='Kello' tmcname='osa13-16_kello'>

Skriv ett program som visar en urtavla som visar systemtiden. Slutresultatet ska se ut så här:

<img src="pygame_kello.gif">

</programming-exercise>

<programming-exercise name='Asteroider' tmcname='osa13-17_asteroider'>

Skapa ett spel där asteroider faller från himlen. Spelaren flyttar en robot till höger och vänster och försöker samla upp de fallande stenarna. Spelaren får ett poäng för varje asteroid som samlas in och den totala poängen visas högst upp i fönstret. Spelet tar slut när spelaren missar en asteroid. Slutresultatet bör se ut så här:

<img src="pygame_asteroidit.gif">

I uppgiftsbotten finns bilden `sten.png` för asteroiden.

</programming-exercise>


Svara vänligen på en snabb enkät om denna del av kursen:

<quiz id="a43f2a08-b665-5bea-ac53-1e8c421b0c28"></quiz>
