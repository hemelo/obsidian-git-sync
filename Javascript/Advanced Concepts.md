# Generators

Funções que retornam um _generator object_ que impl. _iterator_, tendo um obj. `symbol.iterator`

>Qual a diferença pra _iterator_?

O generator pode suspenedr a própria execução

```js
function *generator {
	yield 1
	yield 2
	yield 3
}
```
