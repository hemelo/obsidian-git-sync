> *Existe diferença entre `() => {}` e `function()`?*

Existe. As arrow functions são normalmente confundidas com as functions do ES5

* Arrow functions -> Herdam o contexto do local onde houve a declaração

* Functions -> Herdam o contexto do objeto que está vinculado no momento da chamada. Se não tiver nenhum objeto, será assumido o objeto global automaticamente (ex.: window)

```javascript
var normal = function() {
  return this === obj;
};

var arrow = () => {
  return this === window;
};

var obj = { normal: normal, arrow: arrow };

// true
obj.normal(); 
obj.arrow(); 

normal(); // false
```

###### Construtores

* Arrow functions não podem ser constructors
```javascript
var Normal = function() {}
var Arrow = () => {}

new Normal(); // Normal{}
new Arrow(); // Arrow ow is not a constructor
```

###### Argumentos

* Arrow functions não possuem `arguments`
```javascript
var noop = () => {
  return arguments;
}

noop(); // ReferenceError: arguments is not defined
```

###### Rastreabilidade

* Functions são melhores porque dão um contexto melhor na StackTrace
```javascript
var fn = function nome() {};
fn.name; // nome

var fn = () => {};
fn.name; // fn
```

#### Equivalência

```javascript
var name = (() => {})
var name = (function name() { }.bind(this))

(() => {})
(function() {}).bind(this)
```
