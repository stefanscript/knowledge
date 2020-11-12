## Basic Types
### boolean
```typescript
let isLoggedIn: boolean = true;
```

### number (as in js floating point values or BigInt => type `number` or `bigint` respectively)
```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b10;
let octal: number = 0o744;
// @ts-ignore
let big: bigint = 100n;
```

### string
```typescript
let color: string = "blue";
color = "lightblue";

let queueNumber: number = 200;
let sentence: string = `Hello ${name}, you are no ${queueNumber} in line`
```

### array
```typescript
let list: number[] = [1,2,3];
let list2: Array<number> = [2,8,9];
```

### tuple
```typescript
let x: [number, string];
x = [2, "boat"];
x[1].slice(0, 2);
// x[3] will not work
```

### enum
```typescript
enum Color {
    Red,
    Green,
    Blue
}
let c: Color = Color.Green;
enum Palette {
    LightBlue = 9,
    PinkRose = 12,
    MorningYellow = 3
} // Enum start at 0 but this can be changed
const myColor:string = Palette[9];
```

###  unknown - intentionally accept all values, we don't know when we are writing, value comes from user
```typescript
let notSure: unknown = 3;
notSure = "a string?";
notSure = 1;
notSure = null;
```

###  any - to opt-out of type checking
```typescript
declare function getValue(key: string): any;
const str: string = getValue("myKey");
let b: any; b.someProps; //any in comparison to unknown allows you to access props
```

###  void - seen in function that don't return a value
```typescript
function warnUser(): void {
    console.log("this is a warn message");
}
let unusable: void = undefined; //declaring variables with void is not useful can only assign null or undefined
```

### null and undefined - much like void not extremely useful
```typescript
let boo: null = null;
let voo: undefined = undefined;
let aNumber: number = null; // they are subtypes to all other types
//NOTE: when using --strictNullChecks flag, null and undefined are only assignable to unknown, any and their respective types
```

###  never - type of values that never occur, imagine function expression that always throw or one that never returns
```typescript
function error(message: string): never {
    throw new Error(message)
}
```

###  object - represent the non primitive type, i.e. anything that is not number, bigint, string, boolean,symbol, null or undefined.
```typescript
declare function create(o: object | null): void;
create({prop: 0});
create(null);
create(42);
create("string");
```

### Type assertions - type cast in other language; tell compiler: "Trust me I know what I'm doing"
// ***as*** (works for JSX)
```typescript
let someVal: unknown = "this is string";
let partialString: string = (someVal as string).slice(0, 2);
```
// ***"angle-bracket"***
```typescript
let someValue2: unknown = "this is another string";
let lengthStr2: number = (<string>someValue2).length;
```

#### Note on Number, String, Boolean, Symbol and Object - don't use them as types
Always use the lowercase version

