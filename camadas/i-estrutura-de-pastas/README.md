# 2.1. Estrutura de Pastas

> ### Sumário

1. [Introdução](https://github.com/Sancruz-dev/estudo-ampliado#1-introdução)

2. [Percorrendo Camadas](https://github.com/Sancruz-dev/estudo-ampliado#2-percorrendo-camadas)

   2.1. [Estrutura de Pastas](#)
      1. [Diretório Frontend](#-diretório-frontend)
      2. [Diretório Backend](#-diretório-backend)

   2.2. [Componentes da Aplicação](/camadas/ii-componentes-da-aplicacao#22-componentes-da-aplicação)
      1. [Front-end e seus Componentes](#i-front-end-e-seus-componentes)
      2. [Back-end e seus Componentes](#i-back-end-e-seus-componentes)

   2.3. [Fluxo de Dados dos Componentes](/camadas/iii-fluxo-de-dados-dos-componentes#23-fluxo-de-dados-dos-componentes)

   2.4. [Disponibilidade](/camadas/iv-disponibilidade#24-disponibilidade)

   2.5. [E2E do Estudo Ampliado](/camadas/v-e2e-do-estudo-ampliado#25-e2e-do-estudo-ampliado) 
***

### **1ª Camada**

**Primordialmente, será analizado as principais pastas contidas no projeto, mas antes, abriremos o diretório raíz:**

###### <img height="210" style="border-radius: 8px" src="https://user-images.githubusercontent.com/83969467/151673984-0735a035-4851-4797-a134-e7ee85b6a9a2.png" alt="Diretório Raíz" title="Diretório Raíz"> Figura 1 - Diretório Raíz



Daqui pra frente, o estudo das estruturas de pastas será dividido entre os dois principais diretórios: **Frontend** e **Backend**. 

<br/>

## I. Diretório Frontend

###### <img height="200" align="bottom" style="border-radius: 8px" src="https://user-images.githubusercontent.com/83969467/152814920-e7a37634-de52-4dbc-a294-b93dc9cb7315.png" alt="Figura 2: Diretório Frontend" title="Diretório Frontend"> Figura 2: Diretório Frontend

Temos então `public` e `src` como as duas principais pastas para a criação da página, sendo **public** responsável por desenhar, redirecionar e mostrar o resultado do nosso código fonte buscado diretamente do **src** (source).

###

**public** - contém apenas dois arquivos: o primeiro é o **index.html**, cuja função é trazer e renderizar todo o código vindo de **src**, e o segundo é o **_redirects**, usado para a configuração de redirecionamento para hospedar o website no [Netlify](https://www.netlify.com/).
<details> 
   <summary>Ver pasta</summary>

   ###
   ###### <img align="bottom" style="border-radius: 8px" src="https://user-images.githubusercontent.com/83969467/152815294-83b61296-8ec5-4cfa-b0f9-23af62138e4b.png" alt="Figura 3: Pasta public em Frontend" title="Pasta public"> Figura 3: Pasta public (Frontend)
</details> 

<br/>

**source/src** - É compostos por algumas pastas (havendo mais pastas e/ou arquivos dentro) que vão formar módulos e componentes, para depois serem encapsulados na tag `<App/>` dentro do renderizador `ReactDOM`, que também faz a busca do `id="root"` que foi criado em **public**.

<details>
   <summary>Ver pasta + detalhes</summary> 

   ###

   ###### <img align="bottom" style="border-radius: 8px" src="https://user-images.githubusercontent.com/83969467/152855598-e3472f7c-58f7-4a43-a84a-7f5ff27bd1b5.png" alt="Figura 4: Pasta src em Frontend" title="Pasta src"> Figura 4: Pasta src (Frontend)

   ###

   - **assets** - contém nossos bens/recursos de folha de estilo, imagens, fontes e até scripts. Ou seja, é o complemento de conteúdo.

   - **components** - permite você dividir a UI em partes independentes, reutilizáveis e pensar em cada parte isoladamente. 

   - **pages** - obtém a interface completa de cada página, com a adição da regra de negócio, captura de argumento passado na rota determinada e manipulação de estrutura de dados.

   - **types** - cria a estrutura de tipos do frontend integrando-a à API.

   - **ultils** - guarda arquivos utilitários para auxiliar funções específicas no projeto, como por exemplo a validação de email e criação da variável de ambiente. 

</details> 

<br/>

## II. Diretório Backend
###### <img align="bottom" style="border-radius: 8px" src="https://user-images.githubusercontent.com/83969467/153297522-5595d587-40b6-4a52-9494-918db914d0d2.png" alt="Figura 5: Diretório Backend" title="Diretório Backend"> Figura 5: Diretório Backend

Com exceção do arquivo create.sql, a figura 5 mostra toda a **estrutura de pastas de um projeto [Maven](https://maven.apache.org/)**, usado para **gerenciar nosso backend** de ponta à ponta, desde a instalação de dependências, até suas configurações. 

Desse modo, analisaremos as pastas **java** e **resources** do caminho `backend/src/main`.


###### <img align="bottom" style="border-radius: 8px" src="https://user-images.githubusercontent.com/83969467/154117049-88d05ac5-7326-4965-bd9a-dbd7f473f636.png" alt="Figura 6: pasta src em Backend" title="Pasta src"> Figura 6: Pasta src (Backend)

**Java** - é uma pasta onde contêm os arquivos de origem Java, e o código-fonte de teste de unidade respectiva à ele, e desse modo, tudo pode ser organizado por pacotes que podem ser criados pelo desenvolvedor.

<details>
   <summary>+ informações</summary> 

   ###

   ###### <img align="bottom" style="border-radius: 8px" src="https://user-images.githubusercontent.com/83969467/154122581-4a21fd26-60e4-4031-b94a-2381301c3ed6.png" alt="Figura 7: Pasta Java" title="Pasta java"> Figura 7: Pasta java

   ###

   - **1. entities** - basicamente são as entidades/tabelas do nosso banco de dados, que declaram atributos, tipos de dados, cria construtores (para instanciar um objeto da classe) e métodos de acesso `get` e `set`. Também estabelecem a conexão entre a camada de serviço e a camada de acesso à dados, sempre monitoradas pela JPA (que é nossa ORM);

   - **2. repositories** - resposáveis por realizar o CRUD das `entities`, tendo o ACESSO À DADOS.

   - **3. dto** - objetos simples para TRAFEGAR dados INTERLIGADOS entre o serviços e controntroladores REST, e por outro lado, não é monitorado pela JPA e nem faz parte do banco de dados.

   - **4. services** - orquestra a camada de acesso à dados, trabalhando com armazenamento ao banco, transação e regra de negócio.

   - **5. controllers** - controladores REST que mapeiam e estabelecem o método GET no caminho da requisição.  

   - **6. config** - contém os arquivos de propriedades com dados de configuração a serem passados ​​para o servidor. Quando você publica o pacote configurável do projeto no servidor, os arquivos nesse diretório são extraídos do pacote configurável e instalados em um diretório comum no servidor, que contém todos os arquivos de configuração desse servidor. No caso do nosso arquivo **SecurityConfig**, a configuração é baseada em [CORS](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/CORS).
</details> 

<br/>

**Resources** - A pasta de recursos contém todos os arquivos de **origem não Java**, e por fazer parte da estrutura de projeto maven, podemos colocar a configuração e arquivos de DADOS relacionados ao aplicativo. (Os arquivos e pastas que você define aqui são incluídos no caminho do diretório raiz do pacote configurável do projeto.)


<details>
   <summary>+ informações</summary> 

   ###

   ###### <img align="bottom" style="border-radius: 8px" src="https://user-images.githubusercontent.com/83969467/154154114-3bc20688-bba4-414a-99b5-95ee6ccb92e0.png" alt="Figura 8: Pasta resources" title="Pasta resources"> Figura 8: Pasta resources (backend)

   ###

   Os recursos do tipo *properties* definem perfis de projeto fazerem o uso de um determinado banco de dados, e na figura 8 existem desses perfis:

   **application-test.properties** - para testes rápidos e práticos, que usa um pequeno espaço na memória. `H2 Database`

   **application-dev.properties** - banco de dados local. `PostgreSQL`
   
   **application-prod.properties** - para lançar em um banco na nuvem e deixar em produção. `Heroku`

   O recurso sem nenhuma definição de perfil (application.properties) configura o perfil de projeto que ficará ativo, estando em desenvolvimento ou produção.

   O import.sql está fazendo a inserção de todos os dados nas tabelas do projeto, tornando-se um arquivo de dados.
</details> 

<br/>

> ### [Ir para a próxima camada :arrow_right:](/camadas/ii-componentes-da-aplicacao#22-componentes-da-aplicação)