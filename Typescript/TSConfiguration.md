The presence of **tsconfig.json** in a directory means the directory is the root of a Typescript project

# Top Level

## Base Configuration

`"extends": "@tsconfig/recommended/tsconfig.json"`

What does it contain?
```json
{
  "compilerOptions": {
    "target": "ES2015",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  },
  "$schema": "https://json.schemastore.org/tsconfig",
  "display": "Recommended"
}
```

* Its value must be Node.js style resolution
* The configuration from base are loaded first, then overriden by those in the inheriting config
* The only top-level property that is excluded from inheritance is *references*

## Files

Specifies an allowlist of files to include

```json
{
	"files": ["core.ts", "index.ts"]
}
```

- An error occurs if any of the files can't be found
- Useful when you only have a small number of files
- Otherwise, use [[TSConfiguration#Include and Exclude]]
- Default is `"files": false`

## Include and Exclude

Specifies an array of filenames or patterns to include or exclude in  the program. These filenames are resolved relative to the directory containing the configuration file.

Default:

```json
{
	"include": ["**"],
	"exclude": ["node_modules", "bower_compor"]
}
```

```json
{
	"files": []
	"include": [], // If files is different of false
	"exclude": ["node_modules", "bower_compor"]
}
```
---

```json
{
	"include": ["src/**/*", "tests/**/*"],
	"exclude": ["tests/utils.ts"]
}
```

Results on:

```c
. ├── scripts ⨯ 
│ ├── lint.ts ⨯ 
│ ├── update_deps.ts ⨯ 
│ └── utils.ts ⨯ 
├── src ✓ 
│ ├── client ✓ 
│ │ ├── index.ts ✓ 
│ │ └── utils.ts ✓ 
│ ├── server ✓ 
│ │ └── index.ts ✓ 
├── tests ✓ 
│ ├── app.test.ts ✓ 
│ ├── utils.ts ⨯ 
│ └── tests.d.ts ✓ 
├── package.json 
├── tsconfig.json 
└── yarn.lock
```

Exclude only changes which files are included as a result of the include config.

Side note: It is not a mechanism that prevents a file from being included in the codebase.

>Regex
- `*` matches zero or more characters (except path separator)
- `?` matches any other character (except path separator)
- `**` matches any directory nested to any level

>What if no extension?

.ts, .tsx, .d.ts
.js, .jsx when `"allowJs": true`, see here


# Compiler Options

## Type Checking

### Unreachable Code

```ts
const fn = (n: number) {
	if (n > 5)  return true;
	else return false;
	return true; // Unreachable
}
```

>allowUnreachableCode

- `undefined` => Warnings
- `true` => Ignored
- `false` => Compilation error

## Unused Labels

```ts
function verifyAge(age: number) {
	// Forgot 'return' statement

	if (age > 18) {
		verified: true;
	}
}
```

>allowUnusedLabels

- `undefined` => Warnings
- `true` => Ignored
- `false` => Compilation error

### Always Strict

Ensures that [[ECMAScript#Strict Mode]] is being used. 
It forces "use strict" on every single file that is included on [[TSConfiguration#Files]] or [[TSConfiguration#Include and Exclude]]

>alwaysStrict

Automatically enabled when `"strict": true`

- `true` or `false`

### Exact Optional Property Types

Makes typescript truly enforce the definition provided as an optional provided.

```ts
interface UserConfig {
	colorTheme?: "dark" | "light";
}
```

>exactOptionalPropertyTypes

- `true`

```ts
implemented.colorTheme = undefined; // Error
```

Setting this var as undefined is not the same of not being defined

- `false`

### No Fallthrough Cases In Switch

```ts
switch (a) {  
	case 0:  
		console.log("even"); // Fallthrough
	case 1:  
		console.log("odd");  
		break;  
}   
```

>noFallthroughCasesInSwitch

Ensures that you won't accidentaly create a bug without `break` or `return`

- `true` or `false`

### No implicit `any`

Typescript will fall back to `any` whenever it can't infer the type

```ts
function fn(s) {
	console.log(s.length)
}
```

>noImplicitAny

Automatically enabled when `"strict": true`

- `true` or `false`

### No implicit override

When working with classes which use inheritance, it’s possible for a sub-class to get “out of sync” with the functions it overloads when they are renamed in the base class.

```ts
class Album {
	setup() {}
}

class MLAlbum extends Album {
	override setup() {}
}

class SharedAlbum extends Album {
	setup() {} // Error, must have override modifier when noImplicitOverride is enabled
}
```

>noImplicitOverride

- `true` or `false`

### No implicit Returns

When enabled, it will check all code paths in a function to ensure they return a value

```ts
function getHeadphonesManufacturer(color: "blue" | "black") : string {
	if (color === "blue") {
		return "beats";
	} else {
		"bose"; // Lack of return statement
	}
}
```
The properly way to return nothing is setting `| undefined |` as one of the return possibilities.

>noImplicitReturns

- `true` or `false`

### No implicit `this`

Raises error on `this` expressions with an implied `any` type

```ts
class Rectangle {
	
	constructor(private width: number, private height: number) { }

	getAreaFunction() {
		return function() {
			return this.width * this.height; // Error when noImplicitThis enabled
		}
	}
}

```

>noImplicitThis

Automatically enabled when `"strict": true`

- `true` or `false`

### Index Signature

>noPropertyAccessFromIndexSignature

Ensures consistency between `obj.key` and `obj["key"]` syntax. Without this flag TS will allow to use the dot syntax to access fields which aren't defined..

- `false`
```ts
interface GameSettings {
	[key: string]: string;
}

const settings = getSettings();

// Unknown access are allowed and they will be resolved to string
settings.username; 
```

- `true`
```ts

settings.username; // Error, property 'username' comes from an index signature, so it must be accessed with ["username"]

settings["username"]
```

>noUncheckedIndexedAccess

Typescript has a way to describe objects which have unknown keys but known values on an object, via index signatures

- `false`
```ts
interface EnvironmentVars {
	NAME: string;
	OS: string;
	
	// Unknown properties are covered by this index signature.
	[propName: string]: string;
}

declare const env: EnvironmentVars;

// Declared as existing

const sysName = env.NAME;
const os = env.OS;

// Not declared, but because of the index
// signature, then it is considered a string
const nodeEnv = env.NODE_ENV;
```

- `true`

When true, the property will be considered as possible `undefined`

```ts
// It will be consider like this, but implicity
[propName: string]: string | undefined;
```

### No unused locals

Report error on unused local variables

```ts
const createKeyboard = (modelID: number) => {
	const defaultModelID = 23; // Unused var
	return { type: "keyboard", modelID };
}
```

>noUnusedLocals

- `true` or `false`

### No unused parameters

Report errors on unused parameters in functions

```ts
const createKeyboard = (modelID: number) => { // Unused param.
	const defaultModelID = 23;
	return { type: "keyboard", defaultModelID };
}

```

>noUnusedParameters

- `true` or `false`

### Strict Bind Call Apply

>strictBindCallApply

### Strict Function Types

>strictFunctionTypes

### Strict Null Checks

>strictNullChecks

### Strict Property Initialization

>strictPropertyInitialization




### <mark style="background: #BBFABBA6;">Strict</mark>

Enables a wide range of type checking behavior in strong guarantees of program correctness. 

It enables the entire strict mode *family* options

- [[TSConfiguration#Always Strict]] - `alwaysStrict`
- [[TSConfiguration#No implicit `any`]] - `noImplicitAny`
- [[TSConfiguration#No implicit `this`]] - `noImplicitThis`

Future versions may break code when this is enabled. But is for the good, cause strict mode gets more security when it is updated.