

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
    ? T extends infer O 
    ? { [K in keyof O]: ExpandRecursively<O[K] }
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

```ts
type DifferentKeys<
    T,
    U,
    T0 = Omit<T, keyof U> & Omit<U, keyof T>,
    T1 = { [ K in keyof T0]: T0[K] }
> = T1;

type IntersectionKeys<T, U> = Omit<T | U, keyof DifferentKeys<T, U>>;

type Head<T> = T extends [infer I, ...infer _Rest] ? I : never;

type Tail<T> = T extends [infer _I, ...infer Rest] ? Rest : never;

type ZipDeepMergeTypes<T, U>
    = T extends []
    ? U
    : U extends []
    ? T
    : [
        DeepMergeTypes<Head<T>, Head<U>>,
        ...ZipDeepMergeTypes<Tail<T>, Tail<U>>
    ];

type MergeTypes<
    T, U,
    T0 = Partial<DifferentKeys<T, U>>
	   & {[ K in keyof IntersectionKeys<T, U> ]: DeepMergeTypes<T[K], U[K]> },
    T1 = { [K in keyof T0]: T0[K] }> = T1;

type DeepMergeTypes<T, U>
    = [T, U] extends [any[], any[]]
    ? ZipDeepMergeTypes<T, U>
    : [T, U] extends [{ [key: string]: unknown}, { [key: string]: unknown } ]
    ? MergeTypes<T, U>
    : T | U;
```

```ts
type A = { key1: { a: { b: 'c'} }, key2: undefined }
type B = { key1: { a: {} }, key3: string }


type MergedAB = DeepMergeTwoTypes<A, B>
```

[Fonte e Demonstração](https://dev.to/svehla/typescript-how-to-deep-merge-170c) 
 - [ ] 