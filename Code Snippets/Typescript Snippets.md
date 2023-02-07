

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

```