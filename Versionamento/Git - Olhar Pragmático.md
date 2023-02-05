
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

```bash
$git hash-object --stdin -w 8b73d29acc6ae79354c2b87ab791aecccf51701f
$find .git/objects

.git/objects/8b 
.git/objects/8b/73d29acc6ae79354c2b87ab791aecccf51701f

$git cat-file -p 8b73d29acc6ae79354c2b87ab791aecccf51701f
my precious
$git cat-file -t 8b73d29acc6ae79354c2b87ab791aecccf51701f
blob
```

Movendo pra área de stage

```bash
$git update-index -add --cacheinfo 100644 8b73d29acc6ae79354c2b87ab791aecccf51701f index.txt
```

Como agrupar blobs no stage?

```bash
$git write-tree 3725c9e313e5ae764b2451a8f3b1415bf67cf471

$git cat-file -t 3725c9e313e5ae764b2451a8f3b1415bf67cf471
tree
$git cat-file -p 3725c9e313e5ae764b2451a8f3b1415bf67cf471
100644 blob 8b73d29acc6ae79354c2b87ab791aecccf51701f index.txt
```

Adicionando metadados

```bash
$git commit-tree 3725c -m 'Initial Commit' 87281bbaa25e33bd0ff343fb49d746b8afcf9163
```

