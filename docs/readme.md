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

## Code javascript - Webapplicaties II

```
class Dobbelsteen {
  constructor() {
    this._aantalOgen = 1;
  }
  get aantalOgen() {
    return this._aantalOgen;
  }
  rol() {
    this._aantalOgen = Math.floor(Math.random() * 6) + 1;
  }
}

class Speler {
  constructor(naam) {
    this._naam = naam;
    this._score = 0;
    this._dobbelstenen = [];
    for (let index = 0; index < 5; index++) {
      this._dobbelstenen.push(new Dobbelsteen());
    }
  }
  get score() {
    return this._score;
  }
  get naam() {
    return this._naam;
  }
  get dobbelstenen() {
    return this._dobbelstenen;
  }
  speel() {
    this._dobbelstenen.forEach(dobbelsteen => {
      dobbelsteen.rol();
      if (dobbelsteen.aantalOgen === 1) this._score += 100;
      else if (dobbelsteen.aantalOgen === 5) this._score += 50;
    }
  }
}

class Spel {
  constructor(spelers) {
    this._spelers = spelers;
    this._spelerAanZet = spelers[0];
  }
  get aantalSpelers() {
    return this._spelers.length;
  }
  get spelerAanZet() {
    return this._spelerAanZet;
  }
  get heeftWinnaar() {
    return (
			this._spelers.filter((speler) => speler.score >= 1000).length > 0
		);
  }
  get scoreOverzicht() {
    let resultaat = '';
    this._spelers.forEach((speler) => {
			resultaat += `${speler.naam}: ${speler.score}\n`;
		});
    return resultaat;
  }
  speel() {
    if (!this.heeftWinnaar) this._spelerAanZet.speel();
  }
  bepaalVolgendeSpeler() {
    if (!this.heeftWinnaar) {
      this._spelerAanZet = this._spelers[
        (this._spelers.indexOf(this._spelerAanZet) + 1) % this.aantalSpelers
      ];
    }
  }
}

function toHtml(spel) {
  document.getElementById('speler').innerHTML = `Speler aan zet: ${
    spel.spelerAanZet.naam
  }`;
  document.getElementById('score').innerHTML = `Score = ${
    spel.spelerAanZet.score
  }`;
  
  for (let index = 0; index < spel.spelerAanZet.dobbelstenen.length; index++) {
    document.getElementById(index + 1).src = `images/Dice${
      spel.spelerAanZet.dobbelstenen[index].aantalOgen
    }.png`;
  }
  if (spel.heeftWinnaar) {
    alert(
      `De winnaar is ${spel.spelerAanZet.naam}. Proficiat!\n${
        spel.scoreOverzicht
      }`
    );
  } else {
    if (document.getElementById('play').value === 'Rol dobbelstenen') {
      document.getElementById('play').value = 'Volgende speler';
      document.getElementById('play').onclick = function() {
        spel.bepaalVolgendeSpeler();
        toHtml(spel);
      };
    } else {
      document.getElementById('play').value = 'Rol dobbelstenen';
      document.getElementById('play').onclick = function() {
        spel.speel();
        toHtml(spel);
      };
    }
  }
}

function init() {
  const aantalSpelers = prompt('Met hoeveel spelers gaan we spelen?');
  const spelers = [];
  for (let index = 0; index < aantalSpelers; index++) {
    spelers.push(new Speler(prompt(`Geef naam van speler ${index + 1}`)));
  }
  const spel = new Spel(spelers);
  toHtml(spel);
  document.getElementById('play').onclick = function() {
    spel.speel();
    toHtml(spel);
  };
  document.getElementById('scorebord').onclick = function() {
    alert(spel.scoreOverzicht);
  };
}

window.onload = init;

```