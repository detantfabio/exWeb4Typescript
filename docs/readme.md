# Oefening Typescript

## Voorbereiding

Clone de oefening (https://github.com/stefaandc/exWeb4Typescript).

Open Visual Studio Code en open de folder met de gekloonde oefening.    
Installeer de extension ESLint. Meer inormatie vind je op https://eslint.org/.     
Installeer Typescript Compiler. Open terminal in VSC en geef volgend commendo in: _npm install -g typescript_.      
Geef vervolgens het volgende commando in om de typescript configuration file (_tsconfig.json_) aan te maken: _tsc --init_.        
We zullen eerst een HelloWorl script maken. Maak in de folder _script_ het volgende bestand aan _HelloWorl.ts_ met volgende code:
```
let message: string = 'Hello World';
console.log(message);
```
Nadat je de code hebt geschreven kan je een task aanmaken via de menu Terminal:          

![Terminal.PNG](/docs/images/Terminal.PNG)    
Om de task te runnen, ga je weer via menu Terminal en kies je voor _Run Task_. Je typescript wordt gecompileerd naar javascript en geeft eventueel errors. Los deze eerst op en Run de Task opnieuw.     
Om je script te runnen geef je in de terminal node HelloWorl.js in.


## De oefening: Afrikaans dobbelen

### Omschrijving van de pagina
Dit spel hebben jullie vorig jaar geprogrammeerd in Webaplicaties II in javascript (Hoofdstuk 3).
De bedoeling is om dit opnieuw te doen, maar dan in typescript.

Alle nodige informatie over typescript vind je op https://www.typescriptlang.org/

Het te programmeren spel is een vereenvoudigde versie van het _Afrikaans dobbelspel_. Meer hierover vind je op http://www.spelensite.be/spel/afrikaans-dobbelen

In het begin van het spel wordt gevraagd hoeveel _spelers_ deelnemen. Dan wordt de _naam_ van elke speler opgevraagd. Dit gebeurt via een prompt. Voorbeeld:
![dobbelAantalSpelers.PNG](/docs/images/dobbelAantalSpelersVragen.PNG 'Hoeveel spelers?')
![dobbelNaamSpelers.PNG](/docs/images/dobbelSpelerNaamIngeven.PNG 'Hoeveel spelers?')

Om beurt gooit een speler met _vijf dobbelstenen_. De speler verdient _punten_ volgens het aantal ogen van de dobbelstenen, enkel 1 en 5 leveren punten op.

- 1 = 100 punten
- 5 = 50 punten
- 2, 3, 4 en 6 = 0 punten

De eerste speler die _10.000_ punten behaalt wint het spel.
Een voorbeeld van de initiële scherm layout: speler Jan is aan zet

![janAanZet.PNG](/docs/images/janAanZet.PNG 'Jan aan zet')

Jan heeft de dobbelstenen gerold:

![janGerold.PNG](/docs/images/janGerold.PNG 'Jan heeft gerold')

Merk op dat de knop ‘Rol dobbelstenen’ nu de knop ‘Vogende speler’ is geworden.
Je kan steeds het scorebord raadplegen via de knop ‘Scorebord’:

![scorebord.PNG](/docs/images/scorebord.PNG 'Scorebord')

We bouwen het spel stap per stap op, volg de opgave...

### Opgave

1. Declareer een klasse Dobbelsteen met volgende properties:

    - \_aantalOgen: krijgt initieel de waarde 1, voorzie een get methode aantalOgen
    - rol: methode die een random getal tussen 1 en 6 genereert voor \_aantalOgen.

2. Declareer een functie toHtml(dobbelsteen) die een dobbelsteen object in de index pagina weergeeft.

    - in het img-element met id 1 geef je het juiste beeldje weer. Gebruik document.getElementById(...) om het juiste element op te halen. Geef het src attribuut van dat element de waarde ‘images/DiceX.PNG’ waarbij X het aantalOgen van de dobbelsteen is.

3. Declareer een functie init(). In deze functie maak je een nieuwe Dobbelsteen aan en roep je toHtml(dobbelsteen) aan.
4. Zorg dat wanneer het load event van window afgevuurd wordt, de functie init aangeroepen wordt.
5. Als je index.html bekijkt krijg je nu één dobbelsteen te zien met aantalOgen gelijk aan 1.
6. Declareer een klasse Speler met volgende properties:

    - \_naam: de naam van de speler, dit is een parameter van de constructor; voorzie een getter
    - \_score: de totale score van de reeds gespeelde beurten, voorzie een getter
    - \_dobbelstenen: een array van 5 dobbelstenen, voorzie een getter
    - speel: methode waarbij de 5 dobbelstenen worden gerold en de score wordt verhoogd volgens de domeinregels

7. Pas de functie toHtml aan zodat deze nu een speler object kan weergeven: toHtml(speler).

    - in de img-elementen toon je de waarde van elke dobbelsteen van de speler.
    - in het span element met id score wordt ‘Score = [de score van de speler]’ Maak gebruik van document.getElementById om de span op te halen, en gebruik de innerHTML property om de waarde van de span aan te passen.

8. Pas de init functie aan.

    - maak een nieuwe Speler aan.
    - event handling: zorg dat wanneer er geklikt wordt op de knop “Rol dobbelstenen”, de dobbelstenen van de speler effectief gerold worden, en de methode toHtml aangeroepen wordt.

9. Als je index.html bekijkt krijg je de 5 dobbelstenen van de speler te zien met de score. Telkens je op “Rol dobbelstenen” klikt past het scherm zich aan.
10. Declareer een klasse Spel met volgende properties:

    - \_spelers: een array van spelers; de spelers worden via de constructor aangeleverd
    - \_spelerAanZet: initieel de eerste speler uit de lijst van spelers; voorzie een getter
    - aantalSpelers: dit is een get-methode die de lengte van de spelers-array retourneert
    - heeftWinaar: dit is een get-methode die true retourneert indien 1 van de spelers een score heeft >= 10000 (tip: tijdens het testen van je spel wil je deze waarde waarschijnlijk iets lager zetten)
    - scoreOverzicht: dit is een get-methode die een string retourneert met het overzicht van de spelers en hun score (zie afbeelding scorebord in de inleiding van de oefening)
    - speel: methode die, indien er nog geen winnaar is, de speel methode van de spelerAanzet aanroept
    - bepaalVolgendeSpeler: methode die, indien er nog geen winnaar is, de volgende spelerAanZet instelt (1 voor 1 komen de spelers aan beurt, na de laatste speler is de eerste speler weer aan de beurt)

11. Pas de toHtml functie aan, zodat deze nu het spel kan weergeven: toHtml(spel)

    - in het element met id speler komt de tekst: “Speler aan zet: [naamSpelerAanZet]”, gebruik hiervoor de innerHTML property van het element
    - in het element met id score komt op analoge manier “Score = [scoreSpelerAanZet]”
    - de vijf dobbelstenen van de spelerAanZet worden in de img-elementen getoond
    - indien het spel een winnaar heeft, geef je een alert en feliciteer je de winnaar bij naam

12. Pas de init functie aan.

    - vraag via een prompt naar het aantal spelers
    - prompt naar de naam van elke speler en maak een array van Speler-objecten aan
    - maak een nieuw Spel-object aan, geef de net gemaakte spelers-array door
    - event-handling
    - wanneer op de “Rol dobbelstenen” knop wordt geklikt roep je de speel methode van spel aan en roep je nadien toHtml aan
    - wanneer op de knop “Scoreboard” wordt geklikt dan wordt in een alert het scoreOverzicht van spel getoond

13. Je kan nu het spel spelen maar enkel de eerste speler van alle opgegeven spelers doet mee...
14. Maak gebruik van het stukje code die je in commentaar in dobbelspel.js vindt. Dit stukje code moet uitgevoerd worden in de toHtml functie indien het spel geen winnaar heeft. Bekijk de code goed: er wordt gezorgd dat de knop (value en onclick event handler) zich aanpast en zo de correcte flow in de applicatie verzekert… Veel speelplezier!


## Oefening 2: OXO

Vorm als eerste speler drie op een rij! Op een bord van 3x3 zetten twee spelers om beurt hun symbool (de ene speler speelt met het symbool X, de andere met symbool O. De winnaar is diegene die er als eerste erin slaagt om met zijn symbool een drie op een rij te vormen. Dit kan horizontaal, verticaal of diagonaal. Het spel kan ook eindigen in een gelijkspel. Dit gebeurt wanneer alle 9 vakjes van het bord een symbool bevatten, zonder dat er een drie op een rij is gevormd. De speler met symbool O mag het spel beginnen.

![oxoSpelvoorbeelden.PNG](/docs/images/oxoSpelvoorbeelden.PNG 'Voorbeelden')

De inhoud en opmaak zijn reeds voorzien in index.html en oxo.css. Er wordt gebruik gemaakt van drie afbeeldingen:  wit.png, x.png en o.png. Initieel start je met een leeg bord en bevatten alle img- elementen de afbeelding wit.png.

![oxoStart.PNG](/docs/images/oxoStart.PNG 'Start')

We gaan stap voor stap gedrag aan onze pagina toevoegen.
1.	Maak in de map ‘OXO’ een submap genaamd js aan en maak hierin een bestand oxo.js aan.
2.	Wijzig index.html zodat het script oxo.js geladen wordt wanneer de pagina in de browser geladen wordt.
3.	Declareer in oxo.js een klasse Spelbord met volgende properties
    -	_bord: in de constructor wordt een tweedimensionale array aangemaakt en aan _bord toegekend. Elk element van de array bevat null
    - plaatsSymbool(symbool, rij, kol): een methode die het symbool op de juiste plaats op _bord plaatst
4.	Declareer een init functie. In de functie doe je het volgende:
    -	maak een nieuw spelbord aan
    -	haal alle img- elementen op en stop deze in een array, dit kan je als volgt doen
const imgElementen = document.getElementsByTagName('img');
    -	overloop deze array en definieer de onclick event handler voor elk element:
      1.	je roept de methode plaatsSymbool aan van spelbord; als argument voor de parameter symbool geef je ‘O’ door, de argumenten voor de rij en kol parameters zal je uit het id van het img-element moeten halen. Denk eraan dat arrays in JavaScript 0-based zijn en dat de id’s van de img-elementen 1-based zijn.
      2.	stel het src-attribuut het img-element in op ‘images/O.png’
5.	Stel de init functie in als event handler voor het load event van window
6.	Je kan nu de index pagina laden in de browser en kan op een correcte manier (klik op vakje vult dat vakje met O), het bord volledig opvullen met het symbool O…

      ![oxoAlleenO.PNG](/docs/images/oxoAlleenO.PNG 'Start')
7.	Declareer een klasse Spel.js met volgende properties
    -	_spelbord: instantie van Spelbord, aan te maken in de constructor
    -	_tePlaatsenSymbool, initieel ‘O’, voorzie een getter
    -	_geplaatsteSymbool, initieel ‘X’, voorzie een getter
    -	_winnaarsSymbool, initieel null, voorzie een getter
    -	plaatsSymbool(rij, kol): methode die het te _plaatsenSymbool op rij, kolom zet op het spelbord en nadien _teplaatsenSymbool en _geplaatsteSymbool swapt. Zorg dat dit niet gebeurt indien het bewuste vak op het spelbord niet vrij is. Voeg hiertoe een methode isVrij(rij, kol) toe aan Spelbord.
8.	Declareer een toHtml(spel) functie. In deze functie ga je de innerHTML van div-element met id message instellen: ‘Speler [s] is aan de beurt’ waarbij [s] het tePlaatsenSymbool is
9.	Pas de init-functie aan 
    -	instantieer een Spel ipv een Spelbord
    -	zorg dat het img-element nu volgens het geplaatsteSymbool aangepast wordt (niet langer steeds een ‘O’)
    -	roep de toHtml functie aan zodat er getoond wordt wie aan zet is.
10.	Je kan nu de index pagina laden in de browser en het bord afwisselend met X en O opvullen. Je ziet steeds wie aan de beurt is

      ![oxoIndex.PNG](/docs/images/oxoIndex.PNG 'Index')
11.	Je kan nu de klasse Spelbord en Spel finaliseren.
    -	Spelbord 
      1.	voeg een methode bevatDrieOpEenrij(symbool, rij, kol) toe die retourneert of er al dan niet een drie op een rij wordt gevormd door het zetten van symbool op rij, kol
      2.	voeg een methode isVolzet() toe die retourneert of het bord al dan niet volledig opgevuld is
    -	Spel
      1.	voeg een methode isEindeSpel() toe. Deze methode retourneert true als het bord volzet is of indien er een drie op een rij is gevormd
      2.	pas de methode plaatsSymbool(…) aan. Er kan geen symbool geplaatst worden als het einde van het spel is bereikt. Als het einde van het spel wordt bereikt bij het plaatsen van een symbool dan wordt het winnaarsSymbool ingesteld
12.	Pas de toHtml functie aan zodat afhankelijk van de toestand van het spel, de juiste message weergegeven wordt: volgende speler/gelijkspel/winnaar. Veel speelplezier!
![oxoComplete.PNG](/docs/images/oxoComplete.PNG 'Complete')
