## Literal Types
In Typescript today there are 3 literal types: strings, numbers and booleans

### String
```typescript
//string literal types combine nicely with union types
type Easing = "ease-in" | "ease-out" | "ease-in-out";
```


### Number
```typescript
interface MapConfig {
  lng: number;
  lat: number;
  tileSize: 8 | 16 | 32;
} 
```

### Booleans
```typescript
interface FooterLink {
    title: string;
    showsInFooter: true;
}
```


