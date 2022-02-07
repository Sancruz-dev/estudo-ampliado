# 2.1. Estrutura de Pastas
> **1ª Camada**

Primordialmente, será analizado as principais pastas contidas no projeto, mas antes, abriremos o diretório raíz:

<img height="210" src="https://user-images.githubusercontent.com/83969467/151673984-0735a035-4851-4797-a134-e7ee85b6a9a2.png" alt="Diretório Raíz" title="Diretório Raíz">

> Figura 1 - Diretório Raíz

###### Obs: Serão ignoradas algumas pastas e arquivos na maioria das  ilustrações, não pela inutilidade, mas por não serem esseciais nesse processo. Seus nomes estão informados logo abaixo.

<details> 
   <summary>Pastas e arquivos ignorados:</summary> 

   - **Pastas**: node_modules, project_guide, 

   - **Arquivos**: package.json, tsconfig.json, README.md, yarn.lock, .gitignore 
</details> 

<br/>

Daqui pra frente, focaremos em duas partes: **Frontend** e **Backend**. 


## • Diretório Frontend

Temos então `public` e `src` como as duas principais pastas para a criação da página, sendo **public** responsável por desenhar, redirecionar e mostrar o resultado do nosso código fonte, buscado diretamente do **src** (source).

###

<img height="200" align="center" src="https://user-images.githubusercontent.com/83969467/152814920-e7a37634-de52-4dbc-a294-b93dc9cb7315.png" alt="Diretório Raíz" title="Diretório Raíz">

###

**public** - contém apenas dois arquivos: o primeiro é o **index.html**, cuja função é trazer e renderizar todo o código vindo de **src**, e o segundo é o **_redirects**, usado para a configuração de redirecionamento para hospedar o website no [Netlify](https://www.netlify.com/).
.
<details> 
   <summary>Ver pasta</summary>

   ###
   <img align="center" src="https://user-images.githubusercontent.com/83969467/152815294-83b61296-8ec5-4cfa-b0f9-23af62138e4b.png" alt="Pasta public" title="Pasta public"> 
</details> 

<br/>

**source/src** - É compostos por algumas pastas (havendo mais pastas e/ou arquivos dentro) que vão formar módulos e componentes, para depois serem encapsulados na tag `<App/>` dentro do renderizador `ReactDOM`, que também faz a busca do `id="root"` que foi criado em **public**.

<details>
   <summary>Ver pasta + detalhes</summary> 

   ###

   <img align="center" src="https://user-images.githubusercontent.com/83969467/152855598-e3472f7c-58f7-4a43-a84a-7f5ff27bd1b5.png" alt="Pasta src" title="Pasta src"> 

   ###
   Todas os nomes citados abaixo, são pastas compostas por outras pastas e/ou arquivos.

   - **assets**: contém nossos bens/recursos de folha de estilo, imagens, fontes e até scripts. Ou seja, é o complemento de conteúdo.

   - **components**: permite você dividir a UI em partes independentes, reutilizáveis e pensar em cada parte isoladamente. 

   - **pages**: obtém cada página com sua interface completa, com a adição da regra de negócio, captura de argumento passado na rota determinada e manipulação de estrutura de dados.

   - **types**: cria a estrutura de tipos do frontend integrando-a à API.

   - **ultils**: guarda arquivos utilitários para auxiliar funções específicas no projeto, como por exemplo a validação de email e criação da variável de ambiente. 

</details> 

<br/>

## II. Back End
...