## Conditional typing

```ts
type NonNullable<T> = T extends null | undefined ? never : T
```


### Infer

```ts
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any
```

```ts
type Unpromise<P> = P extends Promise<infer T> ? T : never
```

```ts
type FirstArgument<T> = T extends (first: infer F, ...args: any[]) => any ? F : never
```

```ts
type ArrayType<T> = T extends (infer A)[] ? A : T
```

```ts
type ExtractType<T> = T extends Promise<infer R>
  ? R
  : T extends (...args: any[]) => any
    	? ExtractType<ReturnType<T>>
		: T
```

Veja mais em [[Typescript Snippets#Merging Interfaces]]
