# 2.2. Componentes da Aplicação
> ### Sumário

1. [Introdução](https://github.com/Sancruz-dev/estudo-ampliado#1-introdução)

2. [Percorrendo Camadas](https://github.com/Sancruz-dev/estudo-ampliado#2-percorrendo-camadas)

   2.1. [Estrutura de Pastas](/camadas/i-estrutura-de-pastas#21-estrutura-de-pastas)
      1. [Diretório Frontend](/camadas/i-estrutura-de-pastas#-diretório-frontend)
      2. [Diretório Backend](/camadas/i-estrutura-de-pastas#-diretório-backend)

   2.2. [Componentes da Aplicação](#)

   2.3. [Fluxo de Dados dos Componentes](/camadas/iii-fluxo-de-dados-dos-componentes#23-fluxo-de-dados-dos-componentes)

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


### A Interação entre Componentes 

Há duas imagens abaixo que ilustram o ligamento dos componentes. a figura 9 exibe o componente **Form**, e a figura 10 o **Listing**, portanto, vamos nomear cada um dos dois de "**componente-pai**", consequentemente tornando seus constituintes como seus filhos. 


###### <img style="border-radius: 12px" height="300" src="https://user-images.githubusercontent.com/83969467/154770034-309d7bea-831b-4a5d-97b5-135f84a1651d.png" alt="Figura 9: Componente-pai Form" title="Componente-pai Form" /> Figura 9: componente-pai Form


Vejamos então **Form**, por exemplo, contendo seu filho `FormCard` dentro de si. Logo, **Form** terá em seu código a instanciação somente do componente `FormCard`, e o mesmo, instanciará apenas `BASE_URL`, `Movie` e `Link` seguindo a lógica.

A mesma interação se encaixa em **Listing**:

###### <img style="border-radius: 12px" height="300" src="https://user-images.githubusercontent.com/83969467/154773044-f10e17b2-bd4d-492b-b0b3-37ca44009147.png" alt="Figura 10: Componente-pai Listing" title="Componente-pai Listing" /> Figura 10: componente-pai Listing


### Estado e Requisição

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

**1°) entities** - primeiro cria-se as entidades, que vão estabelecer MÉTODOS de acesso ao banco de dados, para que assim sejam utilizados pelos repósitorios, dessa maneira, a entidade não vai acessar diretamente o BD, pois tal tarefa é realizada pelo seu "componente usuário", **repositories**.

**2°) repositories** - Oferece o acesso ao banco para realizar o CRUD nas tabelas.

**3°) dto** - Assim como as **entities**, o Objeto de Tranferência de Dados (DTO) define métodos de acesso à dados, mas com uma diferença: será feito de forma pura e independente, pois antes de criar os **services**, é preciso que o DTO já exista, devido ser o objeto referenciado pelos serviços e responsável por transferir os dados para a próxima camada, controlador REST. 

**4°) services** - aqui ocorre a formatação de sua resposta, sendo limitado a quantidade de dados que serão enviados ao front-end, ou especificado algum atrbito a ser enviado também, como o `id`. Contudo, também há a conversão dos dados recebidos, para que assim, possam transferidos ao **controller**. 

**5°) controller** - Mapeia a resposta vinda de **services**, e realiza uma requisição passando um método get em seu caminho, para que tal método possa ser usado pelo JSON, estabelecendo uma conexão com o front-end.

### Armazenamento de Dados



- requisição - formatação de algumas resposta - armazenamento de dados ao banco;