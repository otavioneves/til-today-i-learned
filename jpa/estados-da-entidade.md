O ciclo de vida de uma entidade são os estados de um entidade durante o seu uso pela JPA, que é muito semelhante ao estado de alterações gerenciadas pelo Git.

### Estados no comando insert (criação de uma entidade)
- Transient: estado de quando a entidade é instanciada, dando new. Significa que a entidade não foi persistida, não foi gravada no banco de dados e não está sendo gerenciada pela JPA. Qualquer alteração feita nesse estado o EntityManager não irá atualizar no banco de dados, justamente porque nesse momento ainda é um objeto java puro e não um objeto persistido;
- Managed: estado de quando a entidade é persistida pelo método persist. Nesse estado a JPA está gerenciando a entidade, e todas as alterações nela a JPA está percebendo. Após persistido, o método flush pode sincronizar as ações feitas e o método commit salva e executa as ações feitas.
- Detached: estado de quanto a entidade persistida é fechada ou limpa antes de ser commitada ou flusheada. Todas as alterações feitas após o método close ou clear não são monitoradas pela JPA.

### Estados no comando update (atualização de uma entidade)
Para voltar uma entidade do estado Detached para o estado Managed utilizamos o método `merge()`. Após chamar o método merge, ele não muda necessariamente o estado dessa entidade para Managed, ele na verdade cria outra referência e que essa sim está no estado Managed. Para isso precisamos atribuir, por exemplo: `celulares = em.merge(celulares)`, aonde o celulares irá receber a entidade Managed que o método merge devolve. Quando a entidade já está no banco de dados, trazendo do banco para o estado Managed. Para isso podemos usar os métodos `find()` ou `createQuery`. 

### Estados no comando delete (exclusão de uma entidade)
Para excluir uma entidade levamos ela do estado Managed para Removed, através do método `remove()`. Após essa ação, se fizermos um flush ou commit, o JPA rodará um DELETE no banco de dados.

```
	public void cadastrar(Categoria categoria) {
		this.em.persist(categoria);
	}	
	
	public void atualizar(Categoria categoria) {
		this.em.merge(categoria);	// garante que a categoria se torne Managed
	}
	
	public void remover (Categoria categoria) {
		categoria = em.merge(categoria);	
		this.em.remove(categoria);
	}
```