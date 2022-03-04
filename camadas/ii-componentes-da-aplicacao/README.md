# 2.2. Componentes da Aplicação
> ### Sumário

1. [Introdução](https://github.com/Sancruz-dev/estudo-ampliado#1-introdução)

2. [Percorrendo Camadas](https://github.com/Sancruz-dev/estudo-ampliado#2-percorrendo-camadas)

   2.1. [Estrutura de Pastas](/camadas/i-estrutura-de-pastas#21-estrutura-de-pastas)
      1. [Diretório Frontend](/camadas/i-estrutura-de-pastas#-diretório-frontend)
      2. [Diretório Backend](/camadas/i-estrutura-de-pastas#-diretório-backend)

   2.2. [Componentes da Aplicação](#)
      1. [Front-end e seus Componentes](#i-front-end-e-seus-componentes)
      2. [Back-end e seus Componentes](#i-back-end-e-seus-componentes)

   2.3. [Fluxo de Dados](/camadas/iii-fluxo-de-dados-dos-componentes#23-fluxo-de-dados)

   2.4. [Disponibilidade](/camadas/iv-disponibilidade#24-disponibilidade)

   2.5. [E2E do Estudo Ampliado](/camadas/v-e2e-do-estudo-ampliado#25-e2e-do-estudo-ampliado)
***

### **2ª Camada**

Podemos entender como "componente", na maior parte dos cenários, os diversos constituintes de um aplicativo com diferentes responsabilidades, e isso influência a forma como a arquitetura de uma aplicação é feita.

Em uma aplicação front-end, por exemplo, podemos pensar nos componentes de interface e como eles interagem entre si ou com seus estados e requisições.

Já numa aplicação back-end, existem os módulos e pacotes responsáveis por diferentes operações, como: serialização de um JSON (quando uma requisição é feita), formatação de alguma resposta ou armazenamento de dados ao banco.

<br/>

## I. Front-end e seus Componentes

É de suma importância entender que o código fonte (src) React nada mais é do que a **interação de componentes**, isto é, TODAS as `function's` são componentes que retornam HTML.


### a-) A Interação entre Componentes 

Há duas imagens abaixo que ilustram o ligamento dos componentes. a figura 9 exibe o componente **Form**, e a figura 10 o **Listing**, portanto, vamos nomear cada um dos dois de "**componente-pai**", consequentemente tornando seus constituintes como seus filhos. 


###### <img style="border-radius: 12px" height="300" src="https://user-images.githubusercontent.com/83969467/154770034-309d7bea-831b-4a5d-97b5-135f84a1651d.png" alt="Figura 9: Componente-pai Form" title="Componente-pai Form" /> Figura 9: componente-pai Form


Vejamos então **Form**, por exemplo, contendo seu filho `FormCard` dentro de si. Logo, **Form** terá em seu código a instanciação somente do componente `FormCard`, e o mesmo, instanciará apenas `BASE_URL`, `Movie` e `Link` seguindo a lógica.

A mesma interação se encaixa em **Listing**:

###### <img style="border-radius: 12px" height="300" src="https://user-images.githubusercontent.com/83969467/154773044-f10e17b2-bd4d-492b-b0b3-37ca44009147.png" alt="Figura 10: Componente-pai Listing" title="Componente-pai Listing" /> Figura 10: componente-pai Listing


### b-) Estado e Requisição

Haja vista, o tratamento das requisições e seus estados, é o uso de ambos como resposta aos componentes que tem o objetivo de buscar tais valores/respostas. No projeto de demonstração, os componentes que lidam com essas funções são:

**FormCard** - captura o argumento passado na rota, sendo este o `id` do filme, para que assim, possa realizar o processo de `useEffect` e `useState`: requisição do backend do filme e atualização do estado de seus dados, respectivamente. Ademais, o componente lida com envio dados (**handleSubmit**) a partir do método PUT, tal dados em específico é referente ao _email_ e _score_.

<details> 
   <summary>Ver trechos citados (códigos)</summary>

``` tsx
type Props = {
   movieId: string;
}

function FormCard({ movieId }: Props) {

   const navigate = useNavigate();

   const [movie, setMovie] = useState<Movie>();
   
   // - useEffect para realizar a requisição. Busca do backend um filme a partir de seu id.
   // - O movieId que chegou de argumento para o Props, DEVE ser colocado como dependência desse useEffect. 
   useEffect(() => {
      axios.get(`${BASE_URL}/movies/${movieId}`)
         .then(response => {
            setMovie(response.data);
         })

   }, [movieId]);

   const handleSubmit = (event: React.FormEvent<HTMLFormElement>) => {
      event.preventDefault();
      const email = (event.target as any).email.value;
      const score = (event.target as any).score.value;

      if (!validateEmail(email)) { return; }

      // Configuração para ENVIO DE DADOS
      const config: AxiosRequestConfig = {
         baseURL: BASE_URL,
         method: 'PUT',
         url: '/scores',
         data: {
            email: email,
            movieId: movieId,
            score: score
         }
      }

      // Execução do ENVIO DE DADOS
      axios(config).then(response => {
         navigate("/");
         // console.log(response.data);
      })
   }

   return ( { /* [ ... ] */ } )
}
```

</details> 

<br/>


**Form** - pega o valor liberado em `<Route />` passado como argumento à `Props` `movieId` (propriedade movieId), que foi criada e preparada dentro do **FormCard** a fim de usar tal valor.

<details> 
   <summary>Ver trechos citados (códigos)</summary>

``` tsx
function Form() {
   const params = useParams();
   return (
      <FormCard movieId={`${params.movieId}`} />
   );
}
```

</details> 

<br/>

 **Listing** - executa a paginação de listagem dos filmes, ou seja, o NÚMERO de páginas no elemento respectivo será atualizado toda vez que for interagido. Isso através da mudança de evento monitorado por `onChange`, que consequentemente mudará seu estado. 
 
 Além disso, **Listing** faz a RENDERIZAÇÃO DINÂMICA DE COLEÇÃO: busca todos os filmes, porém, para conter um limite de cartões de filme (MovieCard) que serão mostrados em tela, há um mapeamento de conteúdo do "estado de `page`", pois dentro desse estado, a quantidade de cartões exibidos estão limitados.


<details> 
   <summary>Ver trechos citados (códigos)</summary>

``` tsx
function Listing() {

   // const [estado interno, função que altera esse estado] 
   const [pageNumber, setPageNumber] = useState(0);
   const [page, setPage] = useState<MoviePage>({
      content: [],
      last: true,
      totalPages: 0,
      totalElements: 0,
      size: 12,
      number: 0,
      first: true,
      numberOfElements: 0,
      empty: true
   });

   // - Parâmetro de ordernação (sort=id): Isso garante que a busca vai ser ordenada por id (os filmes virão na mesma ordem).
   // - Além do mais, assim como o 'id', pode-se fazer o mesmo com o title.
   useEffect(() => {
      axios.get(`${BASE_URL}/movies/?size=12&page=${pageNumber}&sort=id`)
         .then(response => {
            const data = response.data as MoviePage;
            setPage(data);
         });
   }, [pageNumber]);
   

   // Muda o estado do useState PageNumber
   const handlePageChange = (newPageNumber: number) => {
      setPageNumber(newPageNumber);
   }

     return (
      <>
         <Pagination page={page} onChange={handlePageChange} />

         <div className="container">
            <div className="row">

               {/* RENDERIZAÇÃO DINÂMICA DE COLEÇÃO
                  - map permite executar cada coisa com cada item no array (no filme) 
                  - NOTA: em uma renderização dinâmica de coleção, cada elemento renderizado 
                    DEVE possuir um atributo key. exemplo: key={movie.id}.
               */}
               {page.content.map(movie => (
                  <div key={movie.id} className="col-sm-6 col-lg-4 col-xl-3 mb-3">
                     <MovieCard movie={movie} />
                  </div>
               )
               )}


            </div>
         </div>

      </>
   );
}

```

</details> 

<br/>


## II. Back-end e seus Componentes  

Baseando-se nas informações do tópico java, extraída da estrutura de pastas do [Diretório Backend](/camadas/i-estrutura-de-pastas#-diretório-backend), o assunto será um pouco mais aprofundado para que entendamos melhor sua componentização.

Abaixo está a mais IMPORTANTE imagem para compreender todo o processo de interação entre os componentes back-end à aplicação front-end:

###### <img style="border-radius: 12px" height="300" src="https://user-images.githubusercontent.com/83969467/154807894-15856953-b78a-4ae2-a040-f745b4fd0e6c.png" alt="Figura 11: padrão-camadas" title="padrão-camadas" /> Figura 11: padrão-camadas

A figura 11 deve ser lida de baixo para cima, pois antes do **back-end** receber a requisição front-end (app) repassada pelo controlador REST, é preciso **prepará-lo** do começo ao topo. Desse modo, haverá uma ordem para a criação de cada função.

### a-) Construção e Acesso à Dados

**1°) entities** - primeiro cria-se as entidades, que vão estabelecer MÉTODOS de acesso ao banco de dados, para que assim sejam utilizados pelos repósitorios, e dessa maneira, a entidade não vai acessar diretamente o BD, pois tal tarefa é realizada pelos **repositories**.


<details> 
   <summary>Ver códigos</summary>

``` java
// ENTIDADE User /

@Entity
@Table(name = "tb_user")
public class User {

	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;
	private String email;
	
	public User() {}

	public User(Long id, String email) {
		this.id = id;
		this.email = email;
	}

	public Long getId() {
		return id;
	}

	public void setId(Long id) {
		this.id = id;
	}

	public String getEmail() {
		return email;
	}

	public void setEmail(String email) {
		this.email = email;
	}
}
```

</details> 

<br/>

**2°) repositories** - Obtem todo o acesso ao banco (através da sua extensão usando JpaRepository) para realizar o CRUD nas tabelas.

<details> 
   <summary>Ver códigos</summary>

``` java
// REPOSITÓRIO Movie 

// JpaRepository<Nome da entidade, tipo da id da entidade>
public interface MovieRepository extends JpaRepository<Movie, Long>{

}
```

</details> 

<br/>
 
**3°) dto** - Assim como as **entities**, o Objeto de Tranferência de Dados (DTO) define também métodos de acesso, mas com uma diferença: será feito de forma pura e independente, pois antes de criar os **services**, é preciso que o DTO de alguma entidade já exista, devido ser o objeto referenciado pelos serviços e responsável por transferir os dados para a próxima camada, controlador REST. 

<details> 
   <summary>Ver códigos</summary>

``` java
// DTO User 

public class ScoreDTO {
	
	private Long movieId;
	private String email;
	private Double score;
	
	public ScoreDTO() {}
	
	public Long getMovieId() {
		return movieId;
	}

	public void setMovieId(Long movieId) {
		this.movieId = movieId;
	}

	public String getEmail() {
		return email;
	}

	public void setEmail(String email) {
		this.email = email;
	}

	public Double getScore() {
		return score;
	}

	public void setScore(Double score) {
		this.score = score;
	}
}
```

</details> 

<br/>
 
### b-) Formatação das Respostas

**4°) services** - aqui ocorre a "edição" das respostas, sendo limitado a quantidade de dados que serão enviados ao front-end, ou especificado algum atribito a ser enviado também, como o `id`. Contudo, há a conversão dos dados em DTO, para que assim, possam ser transferidos ao **controller** como forma de objeto simples. 

<details> 
   <summary>Ver códigos</summary>

``` java
// SERVIÇO Movie

// Registra o MovieService como um componente do sistema
@Service
public class MovieService {
	
	@Autowired
	private MovieRepository repository;

	/* A função faz a busca no repositório retornando uma página (sublista)
	 	de Movie, convertendo-a para MovieDTO em seguida.
		@Transactional: garante que o método resolva tudo relacionado à JPA nessa camada.
		readOnly = true: para ser mais eficiente no banco.*/
	@Transactional(readOnly = true)
	public Page<MovieDTO> findAll(Pageable pageable) {
		Page<Movie> result = repository.findAll(pageable);
		Page<MovieDTO> page = result.map(x -> new MovieDTO(x));
		return page;
	}
	
	@Transactional(readOnly = true)
	public MovieDTO findById(Long id) {
		Movie result = repository.findById(id).get();
		MovieDTO dto = new MovieDTO(result);
		return dto;
	}
}
```

</details> 

<br/>
 
### c-) Serialização

**5°) controller** - Mapeia a resposta vinda de **services**, e realiza uma requisição passando um método get em seu caminho, para que o mesmo possa ser acessado pelo JSON estabelecendo uma conexão ao front-end. Essa função pode ser definida como **serialização**.

<details> 
   <summary>Ver códigos</summary>

``` java
// CONTROLADOR Movie //

@RestController
@RequestMapping(value = "/movies")
public class MovieController {
	
	@Autowired
	private MovieService service;
	
	@GetMapping
	public Page<MovieDTO> findAll(Pageable pageable) {
		return service.findAll(pageable);
	}
	
	@GetMapping(value = "/{id}")
	public MovieDTO findById(@PathVariable Long id) {
		return service.findById(id);
	}
}
```

</details> 

<br/>
 
#### A partir dessas configurações, o back-end já está pronto para receber as requisições front-end.

<br/>

> ### [Ir para a próxima camada :arrow_right:](/camadas/iii-fluxo-de-dados-dos-componentes#23-fluxo-de-dados)
