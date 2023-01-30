Ferramenta para transferir dados de/para um servidor. Exemplos de protocolos: HTTP, GOPHER, IMAP, LDAP

>cURL -> Interface para o libcurl

# Introdução

>**Como visualizar um HTML?**

```bash
curl -L -i www.alura.com/
```

-L => Redirect www para https:/www
-i => Resposta com detalhes de cabeçalho

```bash
curl -I https://www.alura.com/
```

-I => Apenas cabeçalho

>**Como fazer um download?**

```bash
curl -o -s https://releases.ubuntu.com/20.04.1/ubuntu-20.04.1-desktop-amd64.iso ubuntu20.iso
```

-o => Nome vai ser o nome provido por parametro
-s => Silencioso, não exibe informações de progresso do download

>**Continuar downloads interrompidos

```bash
curl -C - -O https://releases.ubuntu.com/20.04.1/ubuntu-20.04.1-desktop-amd64.iso 
```

-O => Nome vai ser o nome do download
-C => Continuar download
'-' => Descobrir automaticamente onde parou o download

>**Limitando BitRate**

```bash
curl --limit-rate 1000B -O http://www.gnu.org/software/gettext/manual/gettext.html
```

>**Como consumir REST?**

```bash
curl -X GET https://jsonplaceholder.typicode.com/posts
```

```bash
curl -i -X POST ttps://jsonplaceholder.typicode.com/comments \
	-H 'Content-Type: application/json' \
	-d $'{
			 "postId": 34890
			 "replyTo": "Antony Garbelini",
			 "email": "antony.garbelini@gmail.com",
			 "body": "Olha eu acho que..."
		 }'
```

-X => Método da Requisição
-d => Body
-H => Header

>**Como enviar Cookies?**

```bash
curl -b "cookie1=valor1; cookie2=valor2" https://google.com
curl -b "cookies_file.txt" https://google.com
```

-b => Cookies

>**Se passar por outro "user-agent"**

Isso pode ser útil quando a requisição só aceita request de alguns navegadores

```bash
curl --user-agent "Meu Próprio Browser 1.0" https://google.com
```

>Forçando HTTP2

```bash
curl --http2 -L www.google.com
```

## Testes Automatizados

- Criar arquivo de urls

```
https://jsonplaceholder.typicode.com/posts https://jsonplaceholder.typicode.com/posts/1 https://jsonplaceholder.typicode.com/posts/1/comments
```

```bash
#!/bin/bash

URL_LIST = "urls.txt"

readarray URLS < ${URL_LIST}

for URL in ${URLS[@]}
do
	RESPONSE="$(curl -s -I ${URL})"
	STATUS=$(echo $RESPONSE | grep "HTTP" | cut -d " " -f 2)

	if [[ ${STATUS} -eq "200" ]]
	then
		echo $URL [SUCESSO]
	fi
done
```

# Avançando um Pouco

>***Baixar arquivo apenas se a data de modificação for menor ou maior** 

```bash
curl -z 21-Dec-11 http://www.example.com/yy.html
curl -z -21-Dec-11 http://www.example.com/yy.html
```

>