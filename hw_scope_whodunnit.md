# Scope Homework: Who Dunnit

### Learning Objectives

- Understand function scope
- Know the difference in between the let and const keywords

## Brief

Using your knowledge about scope and variable declarations in JavaScript, look at the following code snippets and predict what the output or error will be and why. Copy the following episodes into a JavaScript file and add comments under each one detailing the reason for your predicted output.

### MVP

#### Episode 1

```js
const scenario = {
  murderer: 'Miss Scarlet',
  room: 'Library',
  weapon: 'Rope'
};

const declareMurderer = function() {
  return `The murderer is ${scenario.murderer}.`;
}

const verdict = declareMurderer();
console.log(verdict);

```
###This returns Miss Scarlet as the murderer. This is a simple reading of the value associated with the murderer key belonging to the scenario object.

#### Episode 2

```js
const murderer = 'Professor Plum';

const changeMurderer = function() {
  murderer = 'Mrs. Peacock';
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```
###This returns an error because murderer is defined as a constant but changeMurderer tries to update this.

#### Episode 3

```js
let murderer = 'Professor Plum';

const declareMurderer = function() {
  let murderer = 'Mrs. Peacock';
  return `The murderer is ${murderer}.`;
}

const firstVerdict = declareMurderer();
console.log('First Verdict: ', firstVerdict);

const secondVerdict = `The murderer is ${murderer}.`;
console.log('Second Verdict: ', secondVerdict);
```
###The First Verdict is Mrs Peacock and the second verdict is Professor Plum
###Although the murderer is initially set to be Professor Plum this is temporary superseded by the let murderer statement on line 58. The declareMurder function then returns Mrs Peacock as the murder. Subsequently after this function the murderer variable is then holding the Professor Plum variable again and this is reported as the second verdict.

#### Episode 4

```js
let suspectOne = 'Miss Scarlet';
let suspectTwo = 'Professor Plum';
let suspectThree = 'Mrs. Peacock';

const declareAllSuspects = function() {
  let suspectThree = 'Colonel Mustard';
  return `The suspects are ${suspectOne}, ${suspectTwo}, ${suspectThree}.`;
}

const suspects = declareAllSuspects();
console.log(suspects);
console.log(`Suspect three is ${suspectThree}.`);
```
###The verdict is Suspect three is Mrs Peacock
###Although suspectThree is updated within declareAllSuspects because it is a let the scope of this change exists only within the function which is seen when declareAllsuspects prints its suspects.
###After this the log references suspect three which is simply the original suspectThree variable.

#### Episode 5

```js
const scenario = {
  murderer: 'Miss Scarlet',
  room: 'Kitchen',
  weapon: 'Candle Stick'
};

const changeWeapon = function(newWeapon) {
  scenario.weapon = newWeapon;
}

const declareWeapon = function() {
  return `The weapon is the ${scenario.weapon}.`;
}

changeWeapon('Revolver');
const verdict = declareWeapon();
console.log(verdict);
```
###The verdict is "The Weapon is the Revolver"
###The weapon starts off as the Candle Stick but then changeWeapon changes this to Candle Stick.


#### Episode 6

```js
let murderer = 'Colonel Mustard';

const changeMurderer = function() {
  murderer = 'Mr. Green';

  const plotTwist = function() {
    murderer = 'Mrs. White';
  }

  plotTwist();
}

const declareMurderer = function () {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```
###The verdict is The murderer is Mrs White
###The murderer starts off as being Colonel Mustard but the changeMurder functon changes this to be Mr Green. There is then a further change via the plotTwist which changes it to Mrs White. Only the first murderer variable is define as let and so the further murderer variables keep the subsequent changes that happen.


#### Episode 7

```js
let murderer = 'Professor Plum';

const changeMurderer = function() {
  murderer = 'Mr. Green';

  const plotTwist = function() {
    let murderer = 'Colonel Mustard';

    const unexpectedOutcome = function() {
      murderer = 'Miss Scarlet';
    }

    unexpectedOutcome();
  }

  plotTwist();
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```
###The verdict is The murderer is Mr Green
###changeMurder changes the murderer from Professor Plum to Mr Green. Any subsequent changes have scope-restricted murderer variables and so by the time the changeMurder function is exited the value is Mr Green


#### Episode 8

```js
const scenario = {
  murderer: 'Mrs. Peacock',
  room: 'Conservatory',
  weapon: 'Lead Pipe'
};

const changeScenario = function() {
  scenario.murderer = 'Mrs. Peacock';
  scenario.room = 'Dining Room';

  const plotTwist = function(room) {
    if (scenario.room === room) {
      scenario.murderer = 'Colonel Mustard';
    }

    const unexpectedOutcome = function(murderer) {
      if (scenario.murderer === murderer) {
        scenario.weapon = 'Candle Stick';
      }
    }

    unexpectedOutcome('Colonel Mustard');
  }

  plotTwist('Dining Room');
}

const declareWeapon = function() {
  return `The weapon is ${scenario.weapon}.`
}

changeScenario();
const verdict = declareWeapon();
console.log(verdict);
```
###The verdict is The weapon is Candle Stick
###Scenario.weapon starts off as Lead Pipe but then changeScenario is called which in turn calls plotTwist which in turn calls unexpectedOutcome.
###unexpectedOutcome updates the weapon to candlestick because the unexpectedoutcome of Colonel Mustard matches what is currently being held by scenario.murderer. Before this scenario.murderer is updated to colonel mustard because the expected room in the plot twist (the dining room) matches what is held in scenario.room


#### Episode 9

```js
let murderer = 'Professor Plum';

if (murderer === 'Professor Plum') {
  let murderer = 'Mrs. Peacock';
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

const verdict = declareMurderer();
console.log(verdict);
```
###The verdict is "The murder is Professor Plum"
###On the face of it it looks like it should return Mrs Peacock however the murder variable that is defined inside of the if statement doesn't exist outisde of it and so the decalreMurder function returns the value of the original murderer variable.

### Extensions

Make up your own episode!
