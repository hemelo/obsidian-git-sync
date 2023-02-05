>[!QUESTION] Como o git funciona debaixo dos panos?

## Comandos internos do git


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

Verificando dados commit

```bash
$git cat-file -t 87281bbaa25e33bd0ff343fb49d746b8afcf9163
commit
```

```bash
$git cat-file -p 87281bbaa25e33bd0ff343fb49d746b8afcf9163 
tree 3725c9e313e5ae764b2451a8f3b1415bf67cf471 
author henrique <hmelo2509@gmail.com> 1670171001 -0300 
committer henrique <hmelo2509@gmail.com> 1670171001 -0300 Initial Commit
```

Commits também são indexados

```bash
$find .gits/objects

.git/objects/
.git/objects/pack/
.git/objects/87/
.git/objects/87/281bbaa25e33bd0ff343fb49d746b8afcf9163
.git/objects/37/
.git/objects/37/25c9e313e5ae764b2451a8f3b1415bf67cf471
.git/objects/8b/
.git/objects/8b/73d29acc6ae79354c2b87ab791aecccf51701f
```

Adicionando um novo commit

```bash
$git commit-tree 3725c -p 87281b -m 'Second Commit'
```

Verificando dados commit

```bash
$git cat-file -p 06474 
ree 3725c9e313e5ae764b2451a8f3b1415bf67cf471 
parent 87281bbaa25e33bd0ff343fb49d746b8afcf9163 
author henrique <hmelo2509@gmail.com> 1670171092 -0300 
committer henrique <hmelo2509@gmail.com> 1670171092 -0300 Second Commit
```

Verificando logs

```bash
$git log 06474

commit 06474da697cff53c4a97080728d17a00b0c6db2 # Mais recente 
Author: henrique <hmelo2509@gmail.com> 
Date: Sun Dec 04 13:23:21 2022 -0300 

commit 87281bbaa25e33bd0ff343fb49d746b8afcf9163 
Author: henrique <hmelo2509@gmail.com> 
Date: Sun Dec 04 13:24:52 2022 -0300
```

### Estrutura de grafos

![[Pasted image 20230205193142.png]]

### Referência para commit

Executar toda hora `git log <hash>` não é tão eficiente. Como alternativa existem referências pra commit. 

```bash
$git update-ref refs/heads/test 06474da697cff53c4a97080728d17a00b0c6db2
```

```bash
$find .git/refs

.git/refs
.git/refs/heads
.git/refs/tags
```

>[!SUCCESS] Isso soa bem familiar né? Pois é, o nome disso é **Branch**

#### HEAD

>[!QUESTION] Como o Git automaticamente sabe que estamos querendo ver o log da main?
>Por causa da HEAD

```bash
$cat .git/HEAD
ref: refs/heads/master

$git branch
* main
```

>[!INFO]
>Head é a referência simbólica da branch atual de trabalho. Manipular o HEAD significa modificar o ponteiro do primeiro commit

Alterando a referência simbólica

```bash
$git symbolic-ref HEAD refs/heads/test
```

---
## Comandos na Prática

### add

>Hash-Object + Update-Index

![[Pasted image 20230205200318.png]]


### commit

>Write-Tree + Commit-Tree

![[Pasted image 20230205200430.png]]
![[Pasted image 20230205200503.png]]
![[Pasted image 20230205200534.png]]

### checkout

>Symbolic-Ref

![[Pasted image 20230205200608.png]]
### reset

Altera o ponteiro da branch

>`update-ref`

![[Pasted image 20230205200723.png]]

### merge

##### fast-forward

![[Pasted image 20230205201410.png]]
![[Pasted image 20230205201424.png]]

##### three-way

![[Pasted image 20230205201501.png]]
![[Pasted image 20230205201624.png]]
![[Pasted image 20230205201641.png]]

### cherry-pick

Move o ponteiro da branch atual para o commit passado como parâmetro

![[Pasted image 20230205202300.png]]
![[Pasted image 20230205202306.png]]

### rebase

![[Pasted image 20230205202424.png]]
![[Pasted image 20230205202537.png]]
![[Pasted image 20230205202544.png]]

### fetch

![[Pasted image 20230205202721.png]]

### push

![[Pasted image 20230205202742.png]]

### tag

São imutáveis

![[Pasted image 20230205202758.png]]

```bash
$find .git/refs 

.git/refs/ 
.git/refs/heads 
.git/refs/heads/main 
.git/refs/tags 
.git/refs/tags/v1.0 
.git/refs/remotes 
.git/refs/remotes/origin 
.git/refs/remotes/origin/main
```


## Merge vs Rebase

>[!SUCCESS] Merge é uma operação não destrutiva

>[!DANGER] Merge deixa muitos commits estranhos no log

![[02 Merging main into the feature branh.svg]]
>[!SUCCESS] Rebase deixa o histórico bem limpo, sem bifurcações

>[!DANGER] Perde rastreabilidade e contexto do commit extra

![[03 Rebasing the feature branch into main.svg]]

### Regras de Ouro

Nunca usar `rebase` em ramificações públicas
![[05 Rebasing the main branch.svg]]