---
path: '/osa-14/3-pelin-viimeistely'
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
        self.naytto = pygame.display.set_mode((nayton_leveys, nayton_korkeus + self.skaala))

        self.fontti = pygame.font.SysFont("Arial", 24)
        ...
```

Dragräknaren ställs in till noll i början av spelet. Varje drag ökar den med ett:

```python
    def uusi_peli(self):
        ...
        self.siirrot = 0
```

```python
    def liiku(self, liike_y, liike_x):
        ...
        self.siirrot += 1

```

Varje gång innehållet i fönstret uppdateras, bör även antalet drag som visas på skärmen uppdateras:

```python
    def piirra_naytto(self):
        ...
        teksti = self.fontti.render("Siirrot: " + str(self.siirrot), True, (255, 0, 0))
        self.naytto.blit(teksti, (25, self.korkeus * self.skaala + 10))
        ...
```

## Nytt spel och att avsluta spelet

Nu ska vi lägga till tangentbordsinstruktioner för att starta ett nytt spel med F2 och avsluta spelet med Esc. Båda är ganska enkla att implementera:

```python
    def tutki_tapahtumat(self):
        ...
                if tapahtuma.key == pygame.K_F2:
                    self.uusi_peli()
                if tapahtuma.key == pygame.K_ESCAPE:
                    exit()
        ...
```

Vi bör också lägga till information om den här funktionen så att spelaren kan se den:

```python
    def piirra_naytto(self):
        ...
        teksti = self.fontti.render("F2 = uusi peli", True, (255, 0, 0))
        self.naytto.blit(teksti, (200, self.korkeus * self.skaala + 10))

        teksti = self.fontti.render("Esc = sulje peli", True, (255, 0, 0))
        self.naytto.blit(teksti, (400, self.korkeus * self.skaala + 10))
        ...
```

## Vinna spelet

Spelaren har vunnit spelet när varje låda befinner sig i en av målrutorna. Följande metod tar hand om att kontrollera detta:

```python
    def peli_lapi(self):
        for y in range(self.korkeus):
            for x in range(self.leveys):
                if self.kartta[y][x] in [2, 6]:
                    return False
        return True
```

Metoden går igenom alla rutor i rutnätet. Om någon av rutorna är en 2:a (en tom målruta) eller en 6:a (en robot i en målruta) är spelet ännu inte löst och metoden returnerar `False`. Om det inte finns någon sådan ruta i rutnätet måste alla målrutor vara upptagna av lådor, spelet är löst och metoden returnerar `True`.

Om spelaren löser spelet bör vi visa ett lämpligt meddelande med metoden `rita_fonster`:

```python
    def piirra_naytto(self):
        ...
        if self.peli_lapi():
            teksti = self.fontti.render("Onnittelut, läpäisit pelin!", True, (255, 0, 0))
            teksti_x = self.skaala * self.leveys / 2 - teksti.get_width() / 2
            teksti_y = self.skaala * self.korkeus / 2 - teksti.get_height() / 2
            pygame.draw.rect(self.naytto, (0, 0, 0), (teksti_x, teksti_y, teksti.get_width(), teksti.get_height()))
            self.naytto.blit(teksti, (teksti_x, teksti_y))
        ...
```

För fullständighetens skull ändrar vi också `flytta`-metoden så att spelaren inte längre kan flytta när han eller hon har löst spelet:

```python
    def liiku(self, liike_y, liike_x):
        if self.peli_lapi():
            return
        ...
```

Spelaren kan dock fortfarande se rutnätet och det slutliga läget i spelet.

## Ett tips för testning

När man utvecklar spel händer det ofta att man vill kontrollera vad som händer i någon senare situation i spelet. I det här spelet är till exempel det ögonblick då spelet vinns en sådan situation.

Det kan vara svårt att testa att en sådan situation fungerar korrekt, eftersom man normalt sett måste lösa spelet för att komma till den punkten i spelet. Som programmerare kan vi göra några tillfälliga underlättningar i våra spel, för att göra det lättare att testa dem. Vi skulle till exempel kunna lägga till följande för att göra det tillfälligt lättare att lösa spelet:

```python
    def peli_lapi(self):
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
