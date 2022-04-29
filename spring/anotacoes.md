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

Outros anotações, agora do Spring MVC, são:
- @Controller: transforma uma classe em um bean do tipo controlle do MVC.
```
@Controller
public class ComputadorController{

}
```
- @RequestMapping: usada para mapear as URLs de acesso a um controller e aos métodos contidos nele. Também nessa anotação podemos utilizar os atributos definindo verbos HTTP, como POST e GET, de acesso aos métodos. A requisição padrão, caso não informar nenhum tipo, é sempre GET
```
@Controller
@RequestMapping("/computadores")
public class ComputadorController{

    @RequestMapping(path = "/listagem", method = RequestMethode.GET)
    public String getComputadores(){

    }
}
```
- Outros anotações que podem substituir a @RequestMapping é a @GetMapping, @PostMapping, @PutMapping, @DeleteMapping e @PatchMapping, que já colocam automaticamente o verbo HTTP.
- @PathVariable: utilizada para extratir da URL um parâmetro que foi incluído como path da URL.
```
http://localhost:8080/demo/computadores/listagem/ibm
```
Nesse caso o /ibm seria o parâmetro.
```
@Controller
@RequestMapping("/computadores")
public class ComputadorController{

    @RequestMapping(path = "/listagem/{marca}", method = RequestMethode.GET)
    public String getComputadores(@PathVariable("marca") String marca){

    }
}
```
- @RequestParam: utilizada para capturar um parâmetro de consulta (Query Param) enviado por uma solicitação no seu corpo.
```
http://localhost:8080/demo/computadores/listagem?marca=ibm
```
```
@Controller
@RequestMapping("/computadores")
public class ComputadorController{

    @RequestMapping(path = "/listagem", method = RequestMethode.GET)
    public String getComputadores(@RequestParam(name="marca") String marca){

    }
}
```
- @ModelAttribute: pode ser usada sobre a assinatura de um método ou como argumento de um método.
```
@Controller
@RequestMapping("/computadores")
public class ComputadorController{

    @PostMapping("/save")
    public String salvar (@ModelAtribute Computador computador){

    }

    // ou, do seguinte modo:

    @ModelAttribute("cpus")
    public CpuType[] populacaoComboBoxCpus {
        return CpuType.values();
    }
}
```

- @Valid: anotação responsável por injetar a validação back-end via Hibernate Validator, Bean Validaton ou Spring Validator.
```
@Controller
@RequestMapping("/computadores")
public class ComputadorController{

    @PostMapping("/save")
    public String salvar (@Valid Computador computador){

    }
}
```
- @ModelMap: objeto usado para enviar dados a página como resposta de uma solicitação. Trabalha como uma resposta do tipo forward.
```
@Controller
@RequestMapping("/computadores")
public class ComputadorController{

    @Autowired
    private ComputadorDao computadorDao;

    @PostMapping("/save")
    public String getComputadores (ModelMap model){
        List<Computador> computadores = computadorDao.findAll();
        model.addAttribute("computadores", computadores);
        return "lista";
    }
}
```

-@ModelAndView: objeto usado para enviar dados a página como resposta de uma solicitação.
```
@Controller
@RequestMapping("/computadores")
public class ComputadorController{

    @Autowired
    private ComputadorDao computadorDao;

    @PostMapping("/save")
    public String getComputadores (ModelMap model){
        List<Computador> computadores = computadorDao.findAll();
        ModelAndView model = new ModelAndView("lista");
        model.addObject("computadores", computadores);
        return model;
    }
}
```

- Podemos usar o @ModelMap junto com @ModelAndView, adicionamos parâmetros no objeto ModelMap e retornamos um ModelAndView.

```
@Controller
@RequestMapping("/computadores")
public class ComputadorController{

    @Autowired
    private ComputadorDao computadorDao;

    @GetMapping("/listagem")
    public ModelAndView getComputadores (ModelMap model){   // ao passar o objeto como parâmetro ele já vem instanciado, não precisa instanciar dentro do método.
        List<Computador> computadores = computadorDao.findAll();
        model.addAttribute("computadores", computadores);
        return new ModelAndView ("lista", model);
    }
}
```

- Redirect é uma operação de resposta usada para redirecionar a resposta de uma solicitação a outra solicitação.

```
@Controller
@RequestMapping("/computadores")
public class ComputadorController{

    @Autowired
    private ComputadorDao computadorDao;

    @GetMapping("/listagem")
    public ModelAndView getComputadores (ModelMap model){
        List<Computador> computadores = computadorDao.findAll();
        model.addAttribute("computadores", computadores);
        return new ModelAndView ("lista", model);
    }

    @PostMappin("/save")
    public String addComputador (Computador computador, RedirectAttributes attrib){
        computadorDao.save(computador);
        attrib.addFlashAttribute("mensagem","Computador inserido com sucesso"); // mensagem que chegará na próxima página
        return "redirect:/computadores/listagem"
    }
}
```

- @SpringBootApplication: anotação utilizada para informar qual a classe que contém o método main.

```
@SpringBootApplication
public class DemoMvcApplication {

    public static void main (String[] args) {
        SpringApplication.run(DemoMvcApplication.class,args)
    }

}
```