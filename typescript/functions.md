## Functions

### Function type
```typescript
let myAdd: (x: number, y: number) => number = function(
    x: number,
    y: number
): number {
    return x + y;
}
```
### Inferring the types
```typescript
let myAdd2: (baseValue: number, increment: number) => number = function(x, y) {
    return x + y;
} 
```
### Optional and default parameters
```typescript
function buildName(firstName: string, lastName: string) {
    return firstName + " " + lastName;
  
}
// needs to match the number of params
let result1 = buildName("Bob"); // error - to few parameters
let result2 = buildName("Bob", "DrX", "Zen"); // error - to many parameters

//to make params optional we need ?
function buildName2(firstName: string, lastName?: string) {
  return firstName + " " + lastName;
}
let result3 = buildName2("Jacob");

// for default params
function buildName3(firstName: string, secondName = "Monroe") {
  return firstName + " " + secondName;
}
let result4 = buildName3("Kate");
```

### Rest Parameters
```typescript
function buildName(firstName: string, ...resOfName: string[]) {
  return firstName + " " + resOfName.join(" ");
}
let buildNameFun: (fname: string, ...rest: string[]) => string = buildName;
```
### This
```typescript
interface Card {
    suit: string;
    card: number;
}
interface Deck {
    suits: string[];
    cards: number[];
    createCardPicker(this: Deck): () => Card; // notice `this` here
}
let deck: Deck = {
  suits: ["hearts", "spades", "clubs", "diamonds"],
  cards: Array(52),
  // NOTE: The function now explicitly specifies that its callee must be of type Deck
  createCardPicker: function (this: Deck) {
    return () => {
      let pickedCard = Math.floor(Math.random() * 52);
      let pickedSuit = Math.floor(pickedCard / 13);

      return { suit: this.suits[pickedSuit], card: pickedCard % 13 };
    };
  },
};

let cardPicker = deck.createCardPicker();
let pickedCard = cardPicker();

alert("card: " + pickedCard.card + " of " + pickedCard.suit);

//this in callbacks
interface UIElement {
    addClickListener(onclick: (this: void, e: Event) => void): void; //this: void - expects onclick to not require this
}
```

### Overloads
```typescript
let suits = ["hears", "spades", "clubs", "diamonds"];

function pickCard(x: { suit: string; card: number }[]): number;
function pickCard(x: number): { suit: string; card: number };
function pickCard(x: any): any {
  // Check to see if we're working with an object/array
  // if so, they gave us the deck and we'll pick the card
  if (typeof x == "object") {
    let pickedCard = Math.floor(Math.random() * x.length);
    return pickedCard;
  }
  // Otherwise just let them pick the card
  else if (typeof x == "number") {
    let pickedSuit = Math.floor(x / 13);
    return { suit: suits[pickedSuit], card: x % 13 };
  }
}
let pickedCard2 = pickCard(15);
```
