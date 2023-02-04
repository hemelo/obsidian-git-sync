
Como o git funciona debaixo dos panos?

## Componentes do GIT

```bash
$ls -F1 .git

HEAD
config
description
hooks/
info/
objects/
refs/
```

<mark style="background: #BBFABBA6;">objects/</mark> é a pasta mais importante pois armazena todos os seus objetos

```bash
$find .git/objects

.git/objects/
.git/objects/pack
.git/objects/info

$find .git/objects -type f
```

Que tipo de armazenamento é esse?

Antes de tudo, vamos persistir um objeto e reparar no que o GIT realiza depois.

