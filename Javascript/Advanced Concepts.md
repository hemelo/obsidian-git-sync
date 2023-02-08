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

## Usos

```js
const g = generator ();
g.next();
```

```js
const g = generator();
console.log([...g])
```

### Database Query Result

```js
const linha = [{
  nome: 'Alan Turing', 
  id: 1,
  idade: 42,
  titulo: 'Pai da computação'
}, {
  nome: 'Ada Lovelace',
  id: 2,
  idade: 36,
  titulo: 'Primeira programadora'
}, {
  nome: 'Grace Hopper',
  id: 3,
  idade: 85,
  titulo: 'Inventora do compilador'
}]

const findInDatabase = (skip, limit) => {
  return linha.slice(skip, skip + limit)
}

function* recordSet() {
  let skip = 0
  const limit = 1
  let currentRecord = findInDatabase(skip, limit)

  while (currentRecord.length > 0) {
    skip += limit
    yield currentRecord[0]
    currentRecord = findInDatabase(skip, limit)
  }
}
```

```js
records = recordSet();
```

### Funções Utilitárias

#### Take

```js
const take = (n) => function *(iterable) {
	let i = 0

	for (let element of iterable) {
		if (i >= n) return
		yield element
		i++
	}
} 
```

#### Repeat

```js
function * repeat(value) {
	while (true)
		yield value
}
```

#### Scan



### Contador de promises

```js
function* sequence() {
  var i = 1
  while (true) {
    yield i++
  }
}

const promisesCreatedCounter = sequence()
let promisesCreatedTotal = 0


const proxyPromise = new Proxy(Promise, {
  get(target, prop) {
    if (prop === 'prototype') {
      promisesCreatedTotal = promisesCreatedCounter.next().value
    }
    return target[prop]
  }
})

const p = new proxyPromise((resolve) => {
  resolve('done')
})

p.then(() => {
  console.log('Promise resolved')
})

console.log('Promises created: ' + promisesCreatedTotal) // Promises Created: 1
```


# Proxies