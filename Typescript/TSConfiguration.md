The presence of **tsconfig.json** in a directory means the directory is the root of a Typescript project

# Base Configuration

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




