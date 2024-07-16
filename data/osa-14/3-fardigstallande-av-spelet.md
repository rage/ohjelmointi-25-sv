---
path: '/osa-14/3-fardigstallande-av-spelet'
title: 'Färdigställande av spelet'
hidden: false
---

Vårt spel är redan ganska fungerande, så det är dags att lägga till några sista detaljer. Vi lägger till en räknare för att visa antalet drag, en möjlighet att starta ett nytt spel och stänga spelet med tangentbordsinmatning samt ett meddelande när spelaren lyckas vinna spelet.

## Räknare för mängden drag

Dragräknaren i nedre kanten av spelfönstret visar antalet drag som spelaren har gjort hittills. Detta kan användas för att hitta den lösning som kräver minst antal drag.

Räknaren kräver några ändringar i koden. Först ändrar vi konstruktorn så att det finns tillräckligt med utrymme för räknaren och att vi har ett lämpligt teckensnitt till vårt förfogande för att rita texten:

```python
    def __init__(self):
        ...
        self.fonster = pygame.display.set_mode((fonster_bredd, fonster_hojd + self.skala))

        self.font = pygame.font.SysFont("Arial", 24)
        ...
```

Dragräknaren ställs in till noll i början av spelet. Varje drag ökar den med ett:

```python
    def nytt_spel(self):
        ...
        self.drag = 0
```

```python
    def flytta(self, flytta_y, flytta_x):
        ...
        self.drag += 1

```

Varje gång innehållet i fönstret uppdateras, bör även antalet drag som visas på skärmen uppdateras:

```python
    def rita_fonster(self):
        ...
        speltext = self.font.render("Drag: " + str(self.drag), True, (255, 0, 0))
        self.fonster.blit(speltext, (25, self.hojd * self.skala + 10))
        ...
```

## Nytt spel och att avsluta spelet

Nu ska vi lägga till tangentbordsinstruktioner för att starta ett nytt spel med F2 och avsluta spelet med Esc. Båda är ganska enkla att implementera:

```python
    def kolla_handelser(self):
        ...
                if handelse.key == pygame.K_F2:
                    self.nytt_spel()
                if handelse.key == pygame.K_ESCAPE:
                    exit()
        ...
```

Vi bör också lägga till information om den här funktionen så att spelaren kan se den:

```python
    def rita_fonster(self):
        ...
        speltext = self.font.render("F2 = nytt spel", True, (255, 0, 0))
        self.fonster.blit(speltext, (200, self.hojd * self.skala + 10))

        speltext = self.font.render("Esc = stäng spel", True, (255, 0, 0))
        self.fonster.blit(speltext, (400, self.hojd * self.skala + 10))
        ...
```

## Vinna spelet

Spelaren har vunnit spelet när varje låda befinner sig i en av målrutorna. Följande metod tar hand om att kontrollera detta:

```python
    def spelet_lost(self):
        for y in range(self.hojd):
            for x in range(self.bredd):
                if self.karta[y][x] in [2, 6]:
                    return False
        return True
```

Metoden går igenom alla rutor i rutnätet. Om någon av rutorna är en 2:a (en tom målruta) eller en 6:a (en robot i en målruta) är spelet ännu inte löst och metoden returnerar `False`. Om det inte finns någon sådan ruta i rutnätet måste alla målrutor vara upptagna av lådor, spelet är löst och metoden returnerar `True`.

Om spelaren löser spelet bör vi visa ett lämpligt meddelande med metoden `rita_fonster`:

```python
    def rita_fonster(self):
        ...
        if self.spelet_lost():
            speltext = self.font.render("Gratulerar, du löste spelet!", True, (255, 0, 0))
            speltext_x = self.skala * self.bredd / 2 - speltext.get_width() / 2
            speltext_y = self.skala * self.hojd / 2 - speltext.get_height() / 2
            pygame.draw.rect(self.fonster, (0, 0, 0), (speltext_x, speltext_y, speltext.get_width(), speltext.get_height()))
            self.fonster.blit(speltext, (speltext_x, speltext_y))
        ...
```

För fullständighetens skull ändrar vi också `flytta`-metoden så att spelaren inte längre kan flytta när han eller hon har löst spelet:

```python
    def flytta(self, flytta_y, flytta_x):
        if self.spelet_lost():
            return
        ...
```

Spelaren kan dock fortfarande se rutnätet och det slutliga läget i spelet.

## Ett tips för testning

När man utvecklar spel händer det ofta att man vill kontrollera vad som händer i någon senare situation i spelet. I det här spelet är till exempel det ögonblick då spelet vinns en sådan situation.

Det kan vara svårt att testa att en sådan situation fungerar korrekt, eftersom man normalt sett måste lösa spelet för att komma till den punkten i spelet. Som programmerare kan vi göra några tillfälliga underlättningar i våra spel, för att göra det lättare att testa dem. Vi skulle till exempel kunna lägga till följande för att göra det tillfälligt lättare att lösa spelet:

```python
    def spelet_lost(self):
        return True
```

Nu returnerar metoden alltid `True`, vilket innebär att spelet är "löst" till att börja med. Detta gör det enkelt att kontrollera att notifieringen i slutet ser bra ut och att spelaren inte längre kan röra sig på rutnätet efter lösningen. När denna funktionalitet är noggrant testad kan vi återkalla ändringarna.

## Ditt spel på GitHub?

Spelet är nu färdigt. Om du vill ha ett enkelt sätt att leka med koden och bilderna kan du hämta källkoden från GitHub:

* [https://github.com/moocfi/sokoban](https://github.com/moocfi/sokoban)

GitHub är en populär plats för många typer av programmeringsprojekt. Det kan användas för att lagra källkoden och annat material för alla dina egna programmeringsprojekt också, och ditt program kommer då att underhållas genom git-versionskontroll, och det kan enkelt delas med andra. Du kommer att bli mycket bekant med git och GitHub om du fortsätter med andra programmeringskurser på mooc.fi.

## Hur många drag krävs?

Rutnätet i det här spelet är ganska litet, men spelet är inte så lätt. Den första utmaningen är att helt enkelt klara spelet, men nästa steg är att försöka göra det med så få drag som möjligt. Hur kort är den kortaste vägen till en lösning?

Att leta efter den kortaste möjliga lösningen är inte alls en lätt uppgift, men det finns beräkningslösningar för detta också. Detta är ett av ämnena i kursen Datastrukturer och algoritmer.
