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



<mark style="background: #FF5582A6;">ATENÇÃO:</mark> Misturar código strict e não strict pode ser problemático durante o transicionamento de código.





