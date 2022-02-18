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

## I. Front-end e seus Componentes

É de suma importância entender que o código fonte (src) React nada mais é do que a **interação de componentes**, isto é, TODAS as `function's` são componentes que retornam HTML.

Há duas imagens abaixo que ilustram o ligamento dos componentes. a figura 9 mostra o componente **Form**, e a figura 10 exibe **Listing**, portanto, vamos nomear cada um dos dois de "**componente-pai**", consequentemente tornando seus constituintes como seus filhos:

###

###### <img style="border-radius: 20px" height="300" src="https://user-images.githubusercontent.com/83969467/154770034-309d7bea-831b-4a5d-97b5-135f84a1651d.png" alt="Figura 9: Componente-pai Form" title="Componente-pai Form" /> Figura 9: componente-pai Form

<br/>

###### <img style="border-radius: 20px" height="300" src="https://user-images.githubusercontent.com/83969467/154773044-f10e17b2-bd4d-492b-b0b3-37ca44009147.png" alt="Figura 10: Componente-pai Listing" title="Componente-pai Listing" /> Figura 10: componente-pai Listing

<br/>

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

 **Listing** - executa a paginação de listagem dos filmes, ou seja, o NÚMERO de páginas no elemento respectivo será atualizado toda vez que for interagido. Isso através da mudança de evento monitorado por `onChange`, que consequentemente mudará seu estado. Além disso, **Listing** faz a RENDERIZAÇÃO DINÂMICA DE COLEÇÃO: busca todos os filmes, porém, para conter um limite de cartões de filme (MovieCard) que serão mostrados em tela, há um mapeamento de conteúdo do "estado de `page`", pois dentro desse estado, a quantidade de cartões exibidos estão limitados.


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


<br/>

## II. Back-end e seus Componentes
...