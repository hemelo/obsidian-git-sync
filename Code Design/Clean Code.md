Aplicar técnicas simples que visam facilitar a escrita e leitura de um código, tornando-o de fácil compreensão e revelando a sua real intenção.

>[!INFO]
>Os programadores passam a maior parte do tempo lendo e entendendo o código do que programando.

> _"Qualquer um consegue escrever código que um computador entende. Bons programadores escrevem códigos que humanos conseguem entender"_

>_"Uma diferença entre um programador inteligente e um programador profissional é que o profissional entende a clareza que é rei. Profissionais usam seus poderes para o bem e escrever código que outros possam entender"_

# Boas práticas

## Nomenclatura

### Usar nomes significativos e passíveis de busca

```php
var $workDays = 0;
$currentDate = date('Y-m-d');

foreach ($people as $person) {
	echo $person->name;
}

for ($i = 0; $i < count($people); $i++) {
	echo $people[$i]->name;
}
```

---
### Evitar números mágicos
---

```php
const GRUPO_ADMINISTRADOR = 10;

private function deveExecutar() {
	$gruposAcesso = explode(',', $_SESSION['access']);

	if (in_array(self::GRUPO_ADMINISTRADOR, $gruposAcesso)) {
		return true;
	}

	return false;
}
```

---
### Nomenclaturas distinguíveis
---

>[!DANGER] Evite letras do alfabeto

```php
private function criaMatrizComNumerosAleatorios($l, $m) {

	$numeros = array();

	for ($i = 0; $i < $l; $i++) {

		$linha = array();

		for ($j = 0; $j < $m; $j++) {
			array_push($linha, rand());
		}

		array_unshift($numeros, $linha);
	}
}
```

> [!SUCCESS] Exceto quando é uma única variável

```php
public static void copyChars(char a1[], char a2[]) { 
	for (int i = 0; i < a1.length; i++) { 
		a2[i] = a1[i]; 
	} 
}
```

>[!DANGER] Evite singular/plural do mesmo método/variável

```php
public interface Bank {
	getActiveAccount();
	getActiveAccounts();
	getActiveAccountInfo();
}
```

>[!DANGER] Evitar sinônimos

```php
class Product {
	public ProductData $productData;
	public ProductInfo $productInfo;

	public function retrieveData() {}
	public function retrieveInfo() {}
}
```

---
### Evitar redundância
---

>[!DANGER] Evitar nomes com tipos

```php
PhoneNumber $phoneString;
```

A variável acima era provavelmente do tipo String e foi encapsulada em um objeto

```php
Phone $phoneObject; 
String $phoneNumber; 
var_dump($phoneObject->number);
```

- Aplicar ciência da computação
- Não causar o efeito de verossimilhança
- Também conhecido como efeito de confundir as dicas de preenchimento de código. 
- Usar componentes com nomes muitos semelhantes entre si induz ao erro de leitura, interpretação e até mesmo durante o processo de desenvolvimento


- Contextualizar tudo
- 

