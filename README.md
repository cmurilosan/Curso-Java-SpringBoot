# Estudo com base em Spring Boot

## Construa uma API Rest
- Aplicações Java com o Spring Boot
- Aplicação Spring sem o uso de arquivos XML.
- Desenvolvimento web com ajuda do Spring Devtools
- Estilo arquitetural REST
- Spring Data e Bean Validation

#### 01 - Introdução ao Spring Boot
- Inicial commmit (introdução)
- Hello World
- Resumo:
  - Um resumo da história e evolução do Spring;
  - Para criar um projeto com **Spring Boot**, utilizamos o **Spring Initialzr**, através do site https://start.spring.io;
  - Como importar um projeto com Spring Boot na IDE **Eclipse**;
  - Como é o **pom.xml** de uma aplicação que utiliza o Spring Boot;
  - Para inicializar o projeto com Spring Boot, devemos utilizar a classe com o método `main`;
  - Para criar um *controller*, utilizamos as anotações `@Controller`(para o Spring fazer o gerenciamento da Classe),  `@RequestMapping`(dizer qual a URL) e `@ResponseBody`(para o Spring não procurar uma página web, mas sim apresentar o que está no "body" da Classe).

#### 02 - Publicando Endpoints
- Conhecendo o projeto
- Primeiro Endpoint da API
- Usando DTO
- Resumo:
  - Sobre a API que desenvolveremos ao longo do curso e sobre as classes de domínio dela;
  - Para um método no controller não encaminhar a requisição a uma página `JSP`, ou `Thymeleaf`, devemos utilizar a anotação `@ResponseBody`;
  - Spring, por padrão, converte os dados no formato JSON, utilizando a biblioteca `Jackson`;
  - Para não repetir a anotação `@ResponseBody` em todos os métodos do controller, devemos utilizar a anotação `@RestController` no início da Classe;
  - Para não precisar reiniciar manualmente o servidor a cada alteração feita no código, basta utilizar o módulo **Spring Boot DevTools**;
  - Não é uma boa prática retornar entidades JPA nos métodos dos controllers, sendo mais indicado retornar classes que seguem o padrão **DTO** (Data Transfer Object);
  - Os principais conceitos sobre o modelo arquitetural **REST**, como **recursos, URIs, verbos HTTP, Representações** e comunicação **stateless**.

#### 03 - Usando Spring Data
- Começando com Spring Data JPA
- Utilizando Repository
- Consulta com filtros
- Resumo:
  - Para utilizar o JPA no projeto, devemos incluir o módulo `Spring Boot Data JPA`, que utiliza o **Hibernate**, por padrão, como sua implementação;
  - Para configurar o banco de dados da aplicação, devemos adicionar as propriedades do *datasource* e do JPA no arquivo **src/main/resources/application.properties**;
  - Para acessar a página de gerenciamento do banco de dados H2, devemos configurar o *console* do H2 com propriedades no arquivo **src/main/resources/application.properties**;
  - Para mapear as classes de domínio da aplicação como entidade JPA, devemos utilizar as anotações `@Entity`, `@Id`, `@GeneratedValue`, `@ManyToOne`, `@OneToMany` e `@Enumerated`;
  - Para que o Spring Boot popule automaticamente o banco de dados da aplicação, devemos criar o arquivo **src/main/resources/data.sql**;
  - Para criar um *Repository*, devemos criar uma interface, que herda da interface `JPARepository` do Spring Data JPA;
  - Para criar consultas que filtram por atributos da entidade, devemos seguir o padrão de nomenclatura de métodos do Spring, como por exemplo `findByCursoNome`;
  - Para criar manualmente a consulta com JPQL, devemos utilizar a anotação `@Query`;

#### 04 - Trabalhando com Post
- Cadastrando tópicos
- Boas práticas no cadastro
- Resumo:
  - Que para evitar repetir a URL em todos os métodos, devemos utilizar a anotação `@RequestMapping` em cima da classe *controller*;
  - Que para mapear requisições do tipo POST, devemos utilizar a anotação `@PostMapping`;
  - Que para receber dados enviados no corpo da requisição, a boa prática é criar uma classe que também siga o padrão **DTO** (*Data Transfer Object*);
  - Que a boa prática para métodos que cadastram informações é devolver o código HTTP 201, ao invés do código 200;
  - Que para montar uma resposta a ser devolvida ao cliente da API, devemos utilizar a classe `ResponseEntity` do Spring;
  - Que para testar requisições do tipo POST, precisamos utilizar alguma ferramenta de testes de API Rest;
  - Como utilizar o Postman para testar uma API Rest;

#### 05 - Validação com Bean Validation
- Validações com Bean Validation
	- Utilizamos no `TopicoForm` as anotações `@NotNull`, `@NotEmpty` e `@Lengh(min=5)` limitando o mínimo de caracteres obrigatórios, podendo limitar conforme desejado.
	- Não podemos esquecer de anotar `@Valid`dentro do método **cadastrar** na **Classe TopicosController** para o *spring* executar essas validações feitas no **form**
- Simplificando o JSON
	- Criamos uma **Classe** para tratar a simplificação do JSON
- Resumo da Aula 05:
	- Para fazer validações das informações enviadas pelos clientes da API, podemos utilizar a especificação **Bean Validation**, com as anotações `@NotNull`, `@NotEmpty`, `@Size`, dentre outras;
	- Para o Spring disparar as validações do *Bean Validation* e devolver um erro 400, caso alguma informação enviada pelo cliente esteja inválida, devemos utilizar a anotação `@Valid`;
	- Para interceptar as `exceptions` que forem lançadas nos métodos das classes *controller*, devemos criar uma classe anotada com `@RestControllerAdvice`;
	- Para tratar os erros de validação do *Bean Validation* e personalizar o JSON, que será devolvido ao cliente da API, com as mensagens de erro, devemos criar um método na classe `@RestControllerAdvice` e anotá-lo com `@ExceptionHandler` e `@ResponseStatus`.


#### 06 - Métodos PUT, DELETE e tratamento de erro
- Detalhando topicos
	- Recebendo um **PATH DINÂMICO** através da anotação `@PathVariable`
- Atualizando tópicos
	- Utilização da anotação `@PutMapping` para atualizações e `@Transactional` para commitar a atualização
- Removendo tópicos
	- Utilização da anotação `@DeleteMapping` para deletar o tópico.
- Tratando o erro 404
	- Alteração para o método **findById** e que devolve um **optional de topico** para caso não encontre o *id* solicitado o cliente não receba uma **exception** e sim um erro **404**
- Resumo da aula 06:
	- Para receber parâmetros dinâmicos no path da URL, devemos utilizar a anotação `@PathVariable`;
Para mapear requisições do tipo **PUT**, devemos utilizar a anotação `@PutMapping`;
Para fazer o controle transacional automático, devemos utilizar a anotação `@Transactional` nos métodos do *controller*;
Para mapear requisições do tipo **DELETE**, devemos utilizar a anotação `@DeleteMapping`;
Para tratar o erro 404 na classe *controller*, devemos utilizar o método `findById`, ao invés do método `getOne`, e utilizar a classe `ResponseEntity` para montar a resposta de *not found*;
O método `getOne` lança uma *exception* quando o `id` passado como parâmetro não existir no banco de dados;
O método `findById` retorna um objeto `Optional<>`, que pode ou não conter um objeto.

 ##Segurança da API, Cache e Monitoramento
 
 #### 01 - Paginação e Ordenação de Recursos
 - Intro
 - Paginação
 - Ordenação
 - Simplificando a paginação e ordenação
 - Resumo:
    - Para realizar paginação com Spring Data JPA, devemos utilizar a interface `Pageable`;
    -  Nas classes `Repository`, os métodos que recebem um `pageable` como parâmetro retornam objetos do tipo `Page<>`, ao invés de `List<>`;
    -  Para o Spring incluir informações sobre a paginação no JSON de resposta enviado ao cliente da API, devemos alterar o retorno do método do controller de `List<>` para `Page<>`;
    -  Para fazer a ordenação na consulta ao banco de dados, devemos utilizar também a interface `Pageable`, passando como parâmetro a direção da ordenação, utilizando a classe `Direction`, e o nome do atributo para ordenar;
    -  Para receber os parâmetros de ordenação e paginação diretamente nos métodos do controller, devemos habilitar o módulo `SpringDataWebSupport`, adicionando a anotação `@EnableSpringDataWebSupport` na classe `ForumApplication`.
