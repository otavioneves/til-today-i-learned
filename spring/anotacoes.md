Para trabalhar com injeção de dependências utilizamos Beans. Beans são classes aonde passamos a responsabilidade do gerenciamento delas para o Spring. Para fazer isso, utilizamos anotações.
- @Component: é uma anotações básica para criar qualquer tipo de Bean gerenciado pelo Spring Framework. Normalmente usada quando não se define um bean como @Repository ou @Service.
- @Repository: define um Bean como sendo do tpo persistente, que é uma classe de acesso ao banco de dados. Com essa anotação é liberado recursos de persistência, como tratar exceções expecíficas para este fim.
- @Service: usado para classes do tipo serviço, que possuem, por exemplo, regras de negócios.
Para injetar Beans, utilizamos a anotação:
- @Autowired: usada para informar ao Spring que ele deve injetar a variável anotada na classe em que está declarada. Dessa forma, quando o Spring cria a classe @Service ou @Repository ele garante que a variável já vai ser criado uma instância, com isso, já podemos utilizar a variável em métodos dessa classe, evitando NullPointerExecption.
Existem 3 formas de utilizar o @Autowired:
- através de uma variável de instância;
```
public class ComputadorService{
    @Autowired
    private ComputadorDao computadorDao;
}
```
- através de um método set();
```
@Service
public class ComputadorService{
    private ComputadorDao computadorDao;

    @Autowired
    public void setComputadorDao(ComputadorDao computadorDao){
        this.computadorDao = computadorDao;
    }

    public void salvar(Computador computador){
        computadorDao.saveOrUpdate(computador)
    }
}
```
- através de um construtor.
```
@Service
public class ComputadorService{
    private ComputadorDao computadorDao;

    @Autowired
    public void ComputadorService(ComputadorDao computadorDao){
        this.computadorDao = computadorDao;
    }

    public void salvar(Computador computador){
        computadorDao.saveOrUpdate(computador)
    }
}
```