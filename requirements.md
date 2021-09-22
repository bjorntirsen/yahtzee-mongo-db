Inlämningsuppgift 2 - MongoDB
Yatzy
Vi ska bygga en databas som kan hålla reda på våra Yatzy-spel från JS-kursen. Vi behöver hålla koll på olika egenskaper. Några exempel är följande:

Games
Ett spel består av två eller flera spelare och deras resultat. Det finns även ett speldatum.

Spelare
Med egenskaper som namn, poäng osv

Resultat
En spelares “formulärdata” från en match

Topplista
De spelare som har dragit in flest poäng

Klura på de frågor som ni kan behöva ställa till databasen under ett normalt spelflöde, t ex:

Användarna ska kunna skriva in sina namn någonstans, användaren ska skapas och läggas till i collection
Vi kanske behöver kunna skapa ett spel med spelare och lägga till i collection games
För varje omgång fylls ett resultat på, t ex Anders fick 2 poäng i "tvåor"
När spelet är klart -> vad händer med resultatet? Vad händer med ev topplista?
Grupperna ska komma fram till en möjlig dokumentdesign. Den måste inte följa exemplet.

Ni ska skriva frågor som CRUD:ar det data som behövs i alla era collections. Man ska alltså t ex kunna uppdatera resultatet för en spelare när den väljer att spara resultatet 18 i tvåpar. Andra frågor som krävs:

Hur många poäng varje användare har fått i en match

Hur topplistan ser ut

Hur många matcher en spelare har spelat

Vi kommer att ha en muntlig genomgång på torsdag där ni får redovisa era databaser och beskriva hur ni har designat dem. Ni kommer att få feedback som kanske resulterar små ändringar.

Senast söndag ska ni skicka in en export av databasen och de frågor man ska kunna ställa mot den i ett textdokument.