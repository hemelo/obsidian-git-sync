

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

>[!SUCCESS] This is useful:

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

>[!IMPORTANT] But this is awesome:

```ts

type ExpandRecursively<T> 
    = T extends Record<string, unknown> | Record<string, unknown>[] 
    ? T extends infer 0 
    ? { [K in keyof 0]: ExpandRecursively<0[K] }
    : never
    : T;

```