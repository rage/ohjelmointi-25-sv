---
path: '/osa-14/2-robot-och-ladar'
title: 'Robot och lådor'
hidden: false
---

Det svåraste att implementera i ett Sokoban-spel brukar vara att flytta roboten så att den kan skjuta lådor i önskad riktning. Spelet ska kunna avgöra när roboten kan röra sig i en angiven riktning och kunna hantera alla situationer där en låda också ska röra sig. Låt oss ta an den här utmaningen nu.

## Att hantera viktiga händelser

Spelaren styr roboten med de fyra piltangenterna, så vår händelsehanterare ska också kunna reagera på lämpliga tangenthändelser:

```python
    def granska_handelser(self):
        for handelse in pygame.event.get():
            if handelse.type == pygame.KEYDOWN:
                if handelse.key == pygame.K_LEFT:
                    self.flytta(0, -1)
                if handelse.key == pygame.K_RIGHT:
                    self.flytta(0, 1)
                if handelse.key == pygame.K_UP:
                    self.flytta(-1, 0)
                if handelse.key == pygame.K_DOWN:
                    self.flytta(1, 0)

            if handelse.type == pygame.QUIT:
                exit()
```

När spelaren nu trycker på en piltangent anropas metoden `flytta` med ett lämpligt par av argument. Det första argumentet innehåller förflyttningen i vertikal riktning, medan det andra innehåller förflyttningen i horisontell riktning.

## Sökning av roboten

Spelet måste veta var roboten befinner sig för att kunna förflytta den på rätt sätt. Låt oss lägga till metoden `hitta_robot` som räknar ut var roboten befinner sig:

```python
    def hitta_robot(self):
        for y in range(self.hojd):
            for x in range(self.bredd):
                if self.karta[y][x] in [4, 6]:
                    return (y, x)
```

Metoden går igenom alla rutor i rutnätet och returnerar koordinaterna för den ruta som innehåller antingen siffran 4 (roboten på egen hand) eller siffran 6 (roboten på en målruta).

Tanken är att varje gång spelaren trycker på en piltangent ska robotens position först fastställas genom att gå igenom rutorna i rutnätet. Detta kan tyckas lite långsamt och överflödigt, eftersom vi lika gärna kan hålla robotens plats i en separat variabel eller två. Fördelen med denna sökmetod är att vi inte lagrar robotens position på två olika ställen (i spelrutan och i separata variabler), utan vi behöver bara bry oss om ett ställe (spelrutan), vilket innebär att spelets tillstånd i datorminnet blir enklare att hantera.

## Förändringar av rutnätet

Vi har redan anropat metoden `flytta` ovan, men vi har inte definierat den än. Låt oss göra det nu.

Metoden `flytta` tar som argument den riktning som spelaren vill förflytta sig till. Den uppdaterar sedan rutnätet i enlighet med detta, eller fastställer att förflyttningen inte är tillåten och lämnar rutnätet oförändrad.

```python
    def flytta(self, flytta_y, flytta_x):
        robot_tidigare_y, robot_tidigare_x = self.hitta_robot()
        robot_nya_y = robot_tidigare_y + flytta_y
        robot_nya_x = robot_tidigare_x + flytta_x

        if self.karta[robot_nya_y][robot_nya_x] == 1:
            return

        if self.karta[robot_nya_y][robot_nya_x] in [3, 5]:
            lada_ny_y = robot_nya_y + flytta_y
            lada_ny_x = robot_nya_x + flytta_x

            if self.karta[lada_ny_y][lada_ny_x] in [1, 3, 5]:
                return

            self.karta[robot_nya_y][robot_nya_x] -= 3
            self.karta[lada_ny_y][lada_ny_x] += 3

        self.karta[robot_tidigare_y][robot_tidigare_x] -= 4
        self.karta[robot_nya_y][robot_nya_x] += 4
```

Metoden har en hel del olika steg, så låt oss ta en titt på vart och ett i tur och ordning:

### Robotens gamla och nya plats

```python
        robot_tidigare_y, robot_tidigare_x = self.hitta_robot()
        robot_nya_y = robot_tidigare_y + flytta_y
        robot_nya_x = robot_tidigare_x + flytta_x
```

Först anropas metoden `hitta_robot` för att ta reda på robotens aktuella position innan förflyttningen. Detta lagras i variablerna `robot_tidigare_y` och `robot_tidigare_x`.

Därefter lagras robotens nya position efter den tänkta förflyttningen i variablerna `robot_nya_y` och `robot_nya_x`. De nya koordinaterna kan enkelt beräknas genom att lägga till de värden som skickats som argument till robotens gamla position, eftersom både vertikala och horisontella värden ingår.

### Gick roboten in i en vägg?

```python
        if self.karta[robot_nya_y][robot_nya_x] == 1:
            return
```

`if`-satsen ovan tar hand om situationen där roboten skulle träffa en vägg som ett resultat av förflyttningen. Kom ihåg att 1 var positionen för en väggruta i listan med bilder. Detta är inte tillåtet, så metoden returnerar helt enkelt utan vidare.

### Flyttning av låda

```python
        if self.karta[robot_nya_y][robot_nya_x] in [3, 5]:
            lada_ny_y = robot_nya_y + flytta_y
            lada_ny_x = robot_nya_x + flytta_x

            if self.karta[lada_ny_y][lada_ny_x] in [1, 3, 5]:
                return

            self.karta[robot_nya_y][robot_nya_x] -= 3
            self.karta[lada_ny_y][lada_ny_x] += 3
```

Om robotens nytänkta position innehåller siffran 3 (en egen låda) eller siffran 5 (en låda i en målruta) försöker roboten flytta lådan till nästa ruta. För detta ändamål behöver vi två nya variabler: `lada_ny_y` och `lada_ny_x`, som innehåller lådans placering efter flytten.

På samma sätt som roboten kan lådan inte flyttas till en väggruta med identifieraren 1. Lådan kan inte heller flyttas till en annan låda eller till en målruta med en låda på. Om detta skulle hända till följd av förflyttningen, återgår metoden helt enkelt utan att göra några ändringar i rutnätet.

I alla andra fall kan lådan röra sig. Värdet på lådans nuvarande rutnätsplats minskas med 3 och värdet på dess nya rutnätsplats ökas med 3. På grund av den smarta ordningen på objekten i listan `bilder` fungerar detta korrekt både när det gäller golvrutor och målrutor.

### Förflyttning av roboten

```python
        self.karta[robot_tidigare_y][robot_tidigare_x] -= 4
        self.karta[robot_nya_y][robot_nya_x] += 4
```

Om metoden har nått denna punkt utan att återvända, är det dags att flytta roboten också. Proceduren är densamma som när lådan flyttas, men det värde som dras från och läggs till på de aktuella platserna i rutnätet är 4 den här gången. Detta säkerställer, återigen genom den smarta ordningen av objekten i bildlistan, att slutresultatet i rutnätet blir korrekt både när golv- och målrutor är inblandade i förflyttningen.

## Omfaktorisering?

Att endast använda rutnätet för att lagra spelets tillstånd hela tiden är mycket praktiskt i den meningen att endast en variabel är permanent inblandad i hela processen, och det är relativt enkelt att uppdatera rutnätets tillstånd genom enkla additioner och subtraktioner.

Nackdelen är att det kan vara en aning svårt att förstå spelets programkod. Om någon som inte är bekant med den logik som används såg följande kodrad skulle de troligen bli lite förvirrade:

```python
            if self.karta[lada_ny_y][lada_ny_x] in [1, 3, 5]:
```

Kodsnutten ovan använder magiska siffror för att representera rutorna i rutnätet. Den som läser koden måste veta att 1 betyder vägg, 3 betyder en låda och 5 betyder en låda i en målruta.

Raderna med de smarta subtraktionerna och adderingarna skulle se ännu mer förvirrande ut:

```python
            self.karta[robot_nya_y][robot_nya_x] -= 3
```

Siffran 3 betydde en ruta precis som tidigare, men nu subtraheras den från värdet på en ruta i rutnätet. Detta fungerar inom ramen för vårt numreringssystem, eftersom det ändrar en låda (3) till en normal golvruta (0) eller en målruta med en låda (5) till en tom målruta (2), men för att förstå detta krävs kännedom i det numreringssystem som används.

Vi kan göra det enklare för alla som läser koden genom att omfaktorisera vår implementation. Det innebär att vi förbättrar kodens struktur och läsbarhet. Ett sätt att uppnå detta skulle vara att använda namnen på rutorna i stället för siffrorna 0 till 6, även om detta fortfarande inte skulle förklara hur och varför siffror kan adderas och subtraheras samtidigt som rutnätets integritet bibehålls.

För att göra programkoden verkligt tillgänglig skulle det sannolikt krävas mycket mer grundläggande transformativ omfaktorisering. Vi skulle till exempel kunna behålla spelkartans struktur på en plats och lagra robotens och lådornas platser i en separat datastruktur. Nackdelen med detta skulle vara att det sannolikt skulle resultera i mycket mer kod och att spelets interna struktur skulle bli mycket mer komplicerad.

Omfaktorisering och kodkvalitet är ett ämne för en del efterföljande kurser, t.ex. Software Development Methods och Software Engineering.
