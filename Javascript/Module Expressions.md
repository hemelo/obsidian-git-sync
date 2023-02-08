
```js
let mod = module {
  export let y = 1;
};
let moduleExports = await import(mod);
assert(moduleExports.y === 1);

assert(await import(mod) === moduleExports);
```

![[Pasted image 20230208070041.png]]

- Por conta de só poderem ser importados em tempo de execução, eles contam com a natureza assíncrona dos `import()` porque um módulo pode importar outro módulo pela rede