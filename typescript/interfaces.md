 ## Interfaces
 One of the core principles in Typescript is that type checking focuses on the shape that the values have
 checking the shape === "duck typing" === "structural subtyping"


### Simple example
```typescript
function printFooTitle(foo: {title: string}): void {
    console.log(foo.title);
}
let obj1 = {title: "Ray tracing", timestamp: 1111111};
printFooTitle(obj1); //works compiler only checks title
```
###Same example with "interface"
```typescript
interface TitledObj {
    title: string
}
function printFoo2Title(foo: TitledObj) {
    console.log(foo.title)
}
const obj2 = {title: "RX3xxx", timestamp: 222222};
printFoo2Title(obj2);
```

### Optional Properties
```typescript
interface Game {
    width?: number,
    height?: number
}
function getGameRatio(game: Game){
    if(game.width && game.height) {
        return game.height/game.width;
    }
    return 1;
}
let ratio = getGameRatio({});
let ratio2 = getGameRatio({width: 2000, height: 900});
```

### Readonly properties
#### Add `readonly` before the name of the property - makes properties modifiable when first created
```typescript
interface Point {
    readonly x: number;
    readonly y: number;
}
let point: Point = {x: 10, y: 30};
p1.x = 5; //error
```
#### `ReadonlyArray<T>` the same as `Array<T>` with all mutating methods removed
```typescript
let a: number[] = [1,2,3,4];
let ro: ReadonlyArray<number> = a;
ro[0] = 12; //error
a = ro; //error - illegal
a = ro as number[] // ok 
``` 

#### readonly vs const
- readonly for properties
- const for variables


### Excess Property Checks
```typescript
interface SquareConfig {
  color?: string;
  width?: number;
}

function createSquare(config: SquareConfig): { color: string; area: number } {
  return { color: config.color || "red", area: config.width ? config.width*config.width : 20 };
}
createSquare({colour: "white", width: 100}) // error due excess property checking 
createSquare({colour: "white", width: 100} as SquareConfig) // ok 
interface SquareConfig {
    color?: string;
    width?: number;
    [propName: string]: any    // better using index signatures - this says SquareConfig can have as many properties as wanted
                                   // as long as is not color or width the type doesn't matter
} 
```

### Function types
Interfaces can describe functions too
```typescript
interface SearchFunc {
    (source: string, subString: string): boolean;
}
let mysearch: SearchFunc;
myseach = function (source: string, subString: string) {
    return source.search(subString) > -1;
}
```

### Indexable Types
```typescript
interface StringArray {
    [index: number]: string; //index signature
}
let myArray: StringArray;
myArray = ["Bob", "Johnny"];
let name: string = myArray[0];
```

### Class Types
Interfaces describe the public side of the class
```typescript
interface ClockInterface {
    currentType: Date;
    setTime(d: Date): void
}

class Clock implements ClockInterface {
    currentTime: Date = new Date();
    constructor(h: number, m: number) {}
    setTime(d: Date) {
        this.currentTime = d;
    }
}
```

### Extending Intefaces
Like classes, interfaces can extend each other
```typescript
interface Color {
    color: string
}
interface Square extends Color {
    sideLength: number
}
let square = {} as Square;
square.color = "lightblue";
square.sideLength = 200;
```

### Hybrid Types
Object that act as both an object and a function
```typescript
interface Counter {
    (start: number): string;
    interval: number;
    reset(): void;
}

function getCounter(): Counter {
    let counter = function(start: number) {} as Counter;
    counter.interval = 123;
    counter.reset = function () {}
    return counter;
}

let aCounter = getCounter();
c(10);
c.reset();
c.interval = 5.0;
```
