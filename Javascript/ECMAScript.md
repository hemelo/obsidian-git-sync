>O que é?

Regras e padrões internacionais de código Javascript para que o mesmo funcione igual em qualquer lugar.

>Por que foi criado?

Padronização. O javascript possui falhas e comportamentos estranhos

Exemplos:

- 0.1 + 0.2 é diferente de 0.3
- Números e strings podem ser somados e subtraídos
- A comparação entre 0 e null
```js
null > 0; // false
null < 0; // false
null == 0; // false
null >= 0; // true
null <= 0; // true
```
- Sort só ordena strings
```js
[10, 1, 12, 2, 3, 25].sort(); //[ 1, 10, 12, 2, 25, 3 ]
```
- Mais comparação do zero
```js
0 == "0"; // true
0 == [] // true
"0" == [] // false
```

> O javascript possui 8 valores considerados falsos. Qualquer coisa diferente disso é considerado verdadeiro:

- `0` 
- `-0`
- `0n`
- `""`
- `null`
- `undefined`
- `NaN`

>Como o javascript lida com igualdade?

A norma <mark style="background: #FFB8EBA6;"> Abstract Equality Comparison </mark> que cita os inúmeros tipos de conversão de informações

Em `0 == []`, lê-se:

*"Se `Type(x)` é `String, Number or Symbol` and `Type(y)` is `Object`, return the result of the comparison `x == ToPrimitive(y)`"*

## Strict Mode

- Variante restrita do JavaScript
- Semântica diferente do normal
- Navegadores que não suportam executarão o código com comportamento diferente
- *Código strict* e *não strict* podem coexistir
- Faz lançar mais exceções
- Proíbe e controla construções que ainda serão definidas em versões futuras do ECMA
- Impede equívocos na performance dos motores

### Ativando 

Pode ser aplicado em qualquer bloco de código, até mesmo arquivos e projetos inteiros.

O jeito é adicionar `"use strict"` no escopo que desejar.

```js
"use strict";

var v = "Oi! Eu sou um script strict mode!"

```

```js
function fn() {
	'use strict';

	function nested() { return "Eu também sou uma função strict mode!"}
	return "E eu sou uma função strict!"
}
```


### Convertendo Equívocos em Erros

Qualquer exceção que falha silenciosamente no Javascript convencional vai lançar erro aqui

#### Variáveis globais acidentais

Impede de criar variável no objeto global sem querer 

```js
"use strict";

let variavel = 2;
variavell = 17; // ReferenceError: Variável com erro de digitação
```

#### Atribuição inválida

```js
"use strict";

var obj1 = {};
Object.defineProperty(obj1, "x", { value: 42, writable: false });
obj1.x = 9; // TypeError
```

```js
"use strict"

var obj2 = { get x() { return 17; } };
obj2.x = 5; // TypeError
```

#### Adicionar propriedade a objeto não-extensível

```js
"use strict"

var fixed = {}
Object.preventExtensions(fixed);
fixed.newProp = "Ohai"; // TypeError
```

#### Deletar propriedades não-deletáveis

```js
"use strict"

delete Object.prototype; // TypeError
```

#### Duplicação

##### Propriedades duplicadas

```js
"use strict"

var o = { p: 1, p: 2 }; // Syntax Error
```

##### Parâmetros duplicados

```js
function sum(a, a, c){ // !!! erro de sintaxe
  "use strict";
  return a + b + c; // Error
}
```

Curiosidade: Sem o Strict Mode a função só teria dois parâmetros, sendo o último 'a' considerado a variável correta. No entanto, é possível acessar as 3 variáveis no `arguments[i]`

#### Octal

Basta adicionar `0o` 

```js
var old_octal = 010;

{
	"use strict"
	var strict_octal = 0o10; // ES6: Octal
}
```

<mark style="background: #FFF3A3A6;">NOTA:</mark> ES5 proibe Octal.

#### Propriedades em valores primitivos

É proibido adicionar valores em tipos primitivos

```js
{
	false.true = ""; // TypeError
	(14).goingTo = "home"; // TypeError
}
```

### Simplificando usos de variáveis

#### Proibição do With

O problema com `with` é que qualquer nome dentro do bloco pode mapear tanto para uma propriedade do objeto passado quanto para uma variável no escopo ou global. Em tempo de execução é impossível saber de antemão

```js
"use strict";

var x = 17;
with (obj) { // Syntax Error
  // Se isto não fosse strict mode, isso seria var x ou obj.x?
  // No geral, é impossível saber sem executar o código, então o nome não pode ser otimizado.
  x;
}
```

#### Eval

Eval de código strict não introduz novas variáveis no escopo envolvente. 

- Em código normal, `eval("var x;")` introduz uma variável `x` no escopo. Ou seja, sem strict é necessário cuidado para não mapear indevidamente e perder o valor anterior porque o `eval` pode ter introduzido uma nova variável que esconderia a externa.
- <mark style="background: #ADCCFFA6;">No modo strict, <code>eval</code> possui contexto próprio</mark>

```js
var x = 17;
var evalX = eval("'use strict'; var x = 42; x");
console.assert(x === 17);
console.assert(evalX === 42);
```

- Se `eval` for invocada em código strict mode, o código será avaliado como strict. Podendo conter ou não explicitamente o `'use strict'`

#### Deleção de nomes simples

```js
"use strict"

var x;
delete x; // Syntax Error

eval("var y; delete y;"); // Syntax Error
```

### Tornando eval e arguments mais simples

Ambos envolvem bastante magia

>Eval

Adicionar ou remover bindings e para mudar valores de bindings

>Arguments

Propriedades indexadas como alias de argumentos nomeados. Acessar parâmetros (basicamente)

```js
"use strict"

// Tudo abaixo resulta em Syntax Error

eval = 17;
arguments++;
++eval;
var obj =  { set p(arguments) };
var eval;
try { } catch (arguments) { }
function x(eval) { }
var y = function eval() { };
```

Tudo acima é considerado erro de sintaxe porque o ES trata as duas palavras como palavras-chave e em breve serão consideradas oficiais.

#### Imutabilidade dos argumentos

Em código normal, mudar arguments[0] mudaria o valor do parâmetro original. Contudo, com strict o valor é mantido

```js
function f(a){
  "use strict";
  a = 42;
  return [a, arguments[0]];
}

var pair = f(17);
console.assert(pair[0] === 42);
console.assert(pair[1] === 17);
```


### <mark style="background: #BBFABBA6;">Tornando o Javascript "Seguro"</mark>

- JS é invasivo
- Deve ser parcialmente transformado antes de executado em browsers
- Devido a sua flexibilidade é necessário verificar em tempo de execução
- Perda de desempenho considerável

A vantagem do strict mode é que reduz substancialmente a necessidade de realizar verificações em tempo de execução

#### `This` como parâmetro

O valor passado como `this` para uma função em strict mode não é forçado a ser um objeto. Já para uma função normal, `this` é sempre um objeto: seja um objeto literal, o valor encapsulado (Boolean, Number, String), o objeto global, `undefined` ou `null`

Resumo: <mark style="background: #FFB8EBA6;">No modo strict, <code>this</code> não é encapsulado em um objeto, e se não for especificado será <code>undefined</code></mark>. Utilize [[Bind, Call and Apply]]

```js
"use strict"

function fun() { return this; }
console.assert(fun() === undefined);
console.assert(fun.call(2) === 2);
console.assert(fun.apply(null) === null);
console.assert(fun.call(undefined) === undefined);
console.assert(fun.bind(true)() === true);

```

<mark style="background: #FFF3A3A6;">NOTA:</mark> Não é mais possível referenciar `window` através de this dentro de uma função strict mode

#### Pilha de execução

Não é mais possível acessar a pilha de execução pelo código

- `fun.caller` => acessa a função que chamou recentemente
- `fun.arguments` => argumentos recentes
- `arguments.caller` => acessa a função que chamou recentemente

```js
function restrita()
{
  "use strict";
  restrita.caller;    // lança TypeError
  restrita.arguments; // lança TypeError
}

function invocadorPrivilegiado()
{
  return restrita();
}

invocadorPrivilegiado();
```

```js
"use strict";
function fun(a, b)
{
  "use strict";
  var v = 12;
  return arguments.caller; // lança TypeError
}
fun(1, 2); // não expõe v (or a or b)
```

Se `fun` estiver em strict mode, todas propriedades citadas são não-deletáveis e lançam exception.

---

<mark style="background: #FF5582A6;">ATENÇÃO:</mark> Misturar código strict e não strict pode ser problemático durante o transicionamento de código.

---






