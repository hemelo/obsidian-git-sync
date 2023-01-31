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

Ensure that [[ECMAScript#Strict Mode]] is being used. 

>alwaysStrict

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

### No implicity any

Typescript will fall back to `any` whenever it can't infer the type

```ts
function fn(s) {
	console.log(s.length)
}
```

>noImplicitAny

Automatically enabled when Strict 

- `true` or `false`

### No implicity override

