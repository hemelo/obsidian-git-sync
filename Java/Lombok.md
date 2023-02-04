>[!INFO]
>lombok é uma biblioteca que está presente em diversos projetos Java. A proposta é simplificar o trabalho do programador dado a verbosidade da linguagem. Com anotações, gera códigos boilerplate de classes. 

## Mal uso

```java
@Data 
public class ContaCorrente { 
	private String id; 
	private String agencia; 
	private String conta; 
	private BigDecimal saldo; 
	private List<Lancamento> lancamentos; 
}
```

>[!help] @Data é uma anotação que gera
>- construtores
>- toString
>- equal and hashCode
>- getters
>- setters

### Por que mal uso?

- Faz sentido mesmo um método _**setSaldo**_? Pela lógica (a mais simples a se pensar), o saldo de uma conta é o resultado de vários lançamentos de débito e crédito
- Dado um id para essa classe, faz sentido poder alterá-lo (método _**setId**_) ? Mais uma vez, é certo que não já que dado a identificação ela é única e imutável.
- Também não é correto alterar a lista de lançamentos (método _**setLancamentos**_). Pela lógica, é bem provável que a única modificação nesse caso seja adicionar novos lançamentos a conta.
- _**toString**_ é necessário?
- O construtor faz sentido?

### Corrigindo mal uso

>[!SUCCESS] Entender quais atributos de fato representam a igualdade do objeto

>[!SUCCESS] Entender como o objeto deve ser de fato construído e quais campos são obrigatórios para a sua criação

>[!SUCCESS] Identificar quais campos devem possuir _getters_ e _setters_

```java
@EqualsAndHashCode(onlyExplicitlyIncluded = true)
public class ContaCorrente { 
	@Getter @EqualsAndHashCode.Include 
	private String id; 
	
	@Getter private String agencia;
	
	@Getter private String conta; 
	@Getter private BigDecimal saldo; 
	
	private List<Lancamento> lancamentos; 
	
	public ContaCorrente(final String agencia, final String conta) { 
		this.id = UUID.randomUUID().toString(); 
		this.agencia = agencia; 
		this.conta = conta; 
		this.lancamentos = new ArrayList<>(); 
	} 
	
	public final List<Lancamento> getLancamentos() { 
		return List.of((Lancamento[]) lancamentos.toArray()); 
	} 
}
```

