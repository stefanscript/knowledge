 ### Interfaces
 One of the core principles in Typescript is that type checking focuses on the shape that the values have
 checking the shape === "duck typing" === "structural subtyping"


### Simple example
```
function printFooTitle(foo: {title: string}): void {
    console.log(foo.title);
}
let obj1 = {title: "Ray tracing", timestamp: 1111111};
printFooTitle(obj1); //works compiler only checks title
```
###Same example with "interface"
```
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
```
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
