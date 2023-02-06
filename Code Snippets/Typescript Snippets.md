

# Prettify Interface Intersections

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
type Prettify<T> = {
	[K in keyof T]: T[K];
} & {}

export type Result = Prettify<Intersected>;
```

```ts
let data?: Result;

// Hover above would show this terrible thing:
//
// type Result = {
//
}
```

>[!IMPORTANT] But this is awesome:

```

```