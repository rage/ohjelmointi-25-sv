---
path: '/osa-14/1-spelprojekt'
title: 'Spelprojekt'
hidden: false
---

I den här modulen kommer vi att använda pygame för att skapa ett lite större spel. Det är en variant av det klassiska Sokoban spelet, där spelaren flyttar en robot på ett rutnät och skjuter lådor till rätt platser med så få drag som möjligt.

Slutresultatet kommer att se ut så här:

<img src="peli.png">

## Spelets karta

Låt oss börja med att rita den karta som används i spelet. Spelet implementeras i klassen `Sokoban`, som kommer att innehålla alla funktioner som krävs för att spela spelet. I detta första steg är innehållet i klassen följande:

```python
import pygame

class Sokoban:
    def __init__(self):
        pygame.init()

        self.ladda_bilder()
        self.nytt_spel()

        self.hojd = len(self.karta)
        self.bredd = len(self.karta[0])
        self.skala = self.bilder[0].get_width()

        fonster_hojd = self.skala * self.hojd
        fonster_bredd = self.skala * self.bredd
        self.fonster = pygame.display.set_mode((fonster_bredd, fonster_hojd))

        pygame.display.set_caption("Sokoban")

        self.huvudloop()

    def ladda_bilder(self):
        self.bilder = []
        for namn in ["golv", "vägg", "mål", "låda", "robot", "färdig", "målrobot"]:
            self.bilder.append(pygame.image.load(namn + ".png"))

    def nytt_spel(self):
        self.karta = [[1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
                       [1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1],
                       [1, 2, 3, 0, 0, 0, 1, 0, 0, 1, 2, 3, 0, 0, 0, 0, 1],
                       [1, 0, 0, 1, 2, 3, 0, 2, 3, 0, 0, 0, 1, 0, 0, 0, 1],
                       [1, 0, 4, 1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1],
                       [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]]

    def huvudloop(self):
        while True:
            self.kolla_handelser()
            self.rita_fonster()

    def kolla_handelser(self):
        for handelse in pygame.event.get():
            if handelse.type == pygame.QUIT:
                exit()

    def rita_fonster(self):
        self.fonster.fill((0, 0, 0))

        for y in range(self.hojd):
            for x in range(self.bredd):
                ruta = self.karta[y][x]
                self.fonster.blit(self.bilder[ruta], (x * self.skala, y * self.skala))

        pygame.display.flip()

if __name__ == "__main__":
    Sokoban()
```

Om du kör programmet visas ett fönster med spelets inledande tillstånd. Låt oss ta en närmare titt på koden som åstadkommer detta.

## Konstruktorn

Klassens konstruktor initierar pygame-modulerna och de väsentliga variabler och datastrukturer som är involverade i spelet. Den anropar också spelets huvudloop-metod.

```python
    def __init__(self):
        pygame.init()

        self.ladda_bilder()
        self.nytt_spel()

        self.hojd = len(self.karta)
        self.bredd = len(self.karta[0])
        self.skala = self.bilder[0].get_width()

        fonster_hojd = self.skala * self.hojd
        fonster_bredd = self.skala * self.bredd
        self.fonster = pygame.display.set_mode((fonster_bredd, fonster_hojd))

        pygame.display.set_caption("Sokoban")

        self.huvudloop()
```

Metoden `ladda_bilder` laddar de bilder som används i spelet till en lista med namnet `bilder`. Metoden `nytt_spel` skapar en tvådimensionell lista med namnet karta, som innehåller spelrutnätets tillstånd i början av spelet.

Variablerna `hojd` och `bredd` sätts baserat på spelrutnätets dimensioner. Variabeln `skala` innehåller längden på sidan av en kvadrat i rutnätet. Eftersom varje bild är en kvadrat av exakt samma storlek täcks storleken på alla kvadrater av denna enda variabel, och bredden på den första bilden räcker gott och väl för värdet. Samma värde kan användas för att beräkna bredden och höjden på hela rutnätet, vilket gör att vi kan skapa ett fönster av lämplig storlek för att visa spelrutnätet.

## Att ladda bilder

Metoden `ladda_bilder` laddar alla bilder som används i spelet:

```python
    def ladda_bilder(self):
        self.bilder = []
        for namn in ["golv", "vägg", "mål", "låda", "robot", "färdig", "målrobot"]:
            self.bilder.append(pygame.image.load(namn + ".png"))
```

Spelet använder följande bilder:

### Golvruta

<img src="lattia.png">

* Filnamn: `golv.png`
* Position i listan: 0

### Väggruta

<img src="seina.png">

* Filnamn: `vägg.png`
* Position i listan: 1

### Målruta

<img src="kohde.png">

* Filnamn: `mål.png`
* Position i listan: 2
* Roboten ska flytta en låda till den här rutan

### Låda

<img src="laatikko.png">

* Filnamn: `låda.png`
* Position i listan: 3

### Robot

<img src="robo.png">

* Filnamn `robot.png`
* Position i listan: 4

### Låda på målruta

<img src="valmis.png">

* Filnamn: `färdig.png`
* Position i listan: 5
* Lådan har flyttats till målrutan

### Målruta och robot

<img src="kohderobo.png">

* Filnamn: `målrobot.png`
* Position i listan: 6
* Roboten kan också vara på en tom målruta

## Att skapa spelrutan

Metoden `nytt_spel` skapar den ursprungliga spelrutan:

```python
    def nytt_spel(self):
        self.karta = [[1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
                       [1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1],
                       [1, 2, 3, 0, 0, 0, 1, 0, 0, 1, 2, 3, 0, 0, 0, 0, 1],
                       [1, 0, 0, 1, 2, 3, 0, 2, 3, 0, 0, 0, 1, 0, 0, 0, 1],
                       [1, 0, 4, 1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1],
                       [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]]
```

Metoden skapar en tvådimensionell lista med namnet `karta` som använder de numrerade positionerna för bilderna i listan för att markera vilken bild som ska vara var. På så sätt innehåller spelet ett register över spelrutans tillstånd vid alla tidpunkter.

OBS: I början innehåller alla rutor på spelplanen ett nummer mellan 0 och 4. Siffrorna 5 och 6 ingår inte, eftersom det i början inte finns någon låda eller robot på en målruta.

## Huvudloopen

Metoden `huvudloop` är ganska kort. Vid varje iteration anropar den två metoder: `kolla_handelser` går igenom alla händelser som samlats in sedan föregående iteration, och metoden `rita_fonster` uppdaterar innehållet i fönstret.

```python
    def huvudloop(self):
        while True:
            self.kolla_handelser()
            self.rita_fonster()

    def kolla_handelser(self):
        for handelse in pygame.event.get():
            if handelse.type == pygame.QUIT:
                exit()

    def rita_fonster(self):
        self.fonster.fill((0, 0, 0))

        for y in range(self.hojd):
            for x in range(self.bredd):
                ruta = self.karta[y][x]
                self.fonster.blit(self.bilder[ruta], (x * self.skala, y * self.skala))

        pygame.display.flip()
```

I det här skedet är den enda händelse som faktiskt hanteras av spelet att stänga spelfönstret, t.ex. med exit-knappen. Spelet avslutas sedan genom att anropa Pythons `exit`-funktion.

Varje gång metoden `rita_fonster` anropas korsas hela spelrutnätet igenom och den bild som motsvarar varje ruta i rutnätet ritas på rätt plats.

OBS: koordinaterna x och y används på två olika sätt i spelet. När man hanterar index i en tvådimensionell lista är det logiskt att ange y-koordinaten först, eftersom y hänvisar till numret på raden medan x är numret på kolumnen. Å andra sidan, när man använder pygame-metoder, skickas x vanligtvis först, vilket det ganska ofta gör när man arbetar med grafik och även i matematiska sammanhang.
