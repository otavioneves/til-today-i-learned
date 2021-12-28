A perda de performance acontece devido ao mapeamento, aonde por termos relacionamento de FK que possua ToOne, por padrão a JPA puxa mais informações do que é necessário. Existem dois comportamentos padrão o Eager (carregamento dos dados antecipadamente, mesmo que não utilize esses dados. Esse é o padrão dos relacionamento que terminam com ToOne) e o Lazy (carregamento tardio, aonde só carrega os dados caso vá utilizar algum dado desse. Esse é padrão dos relacionamentos que terminam com ToMany).<br>
Podemos forçar o Lazy no relacionamento ToOne, para que dessa maneira não carregue desnecessariamente dados sem ser utilizado. Para isso, utilizamos o atributo fetch na anotação.
```
@ManyToOne(fetch = FetchType.LAZY)
```
Com isso a consulta tem maior performance mas como efeito colateral temos que se o EntityManager já estiver fechado, não conseguimos puxar mais nada no banco de dados, lançando a exception LazyInitialiationExecption. É comum que em aplicações que o tempo de vida de um EntityManager seja de apenas um método, ou seja, tudo que quisermos puxar após ele ter fechado, não conseguimos puxar.<br>
Para resolver a situação, caso precisarmos de informações de relacionamentos que sejam Lazy, precisamos deixar claro através da montagem de uma query específica, para garantir que os dados sejam puxados. Isso é chamado de Query Planejada, aonde utilizamos o JOIN FETCH, fazendo com que nessa consulta, um relacionamento Lazy seja tratado como Eager.
```
	public Pedido buscarPedidoComCliente(int id) {
		return em.createQuery("SELECT p FROM Pedido p JOIN FETCH p.cliente WHERE p.id = :id", Pedido.class).setParameter("id", id).getSingleResult();
	}
```