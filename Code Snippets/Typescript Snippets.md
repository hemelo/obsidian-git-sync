

# Merging Interfaces

>[!DANGER] This is weird:

```ts
export type Intersected = {
	a: number;
} & {
	b: number;
} & {
	c: number;
}
```

```ts
let data?: Intersected;

// Hover above would show this terrible thing:
//
// type Intersected = {
//	  a: number;
// } & {
//	  b: number;
// } & {
// 	  c: number;
// }
```

>[!HELP] This is useful:

```ts
type Merge<T> = {
	[K in keyof T]: T[K];
} & {}

export type Result = Merge<Intersected>;
```

```ts
let data?: Result;

// Hover above would show this terrible thing:
//
// type Result = {
//    a: number;
//    b: number;
//    c: number;
// }
```

>[!STAR] This is better:


```ts

type ExpandRecursively<T> 
    = T extends Record<string, unknown> | Record<string, unknown>[] 
    ? T extends infer 0 
    ? { [K in keyof 0]: ExpandRecursively<0[K] }
    : never
    : T;

```

```ts
type Intersected = {
    a: number;
} & {
    data: { id: string, title: string } ;
} & {
    [x: string]: string;
} & {
	(..args: unknown[]): unknown; // This wouldn't appears on below type
}

type Merged = ExpandRecursively<Intersected>;
```

>[!SUCCESS] But this is the greatest

