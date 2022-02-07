# 🔎 Estudo Ampliado


<img height="185" src="https://user-images.githubusercontent.com/83969467/150009028-382503a7-c4b6-421a-8f85-5b25cf1e1a06.gif">

###
> _Amplie seu entendimento a cada passo..._

<br/>


## Sumário

1. [Introdução](#1-o-que-é)

2. [Percorrendo Camadas](#2-Percorrendo-Camadas)

   2.1. [Estrutura de Pastas](#21-estrutura-de-pastas)
      - [Front End Dir](#a-Front-End)
      - [Back End Dir](#a-Back-End)

   2.2. [Componentes da Aplicação](#22-componentes-da-aplicação)

   2.3. [Fluxo de Dados dos Componentes](#23-fluxo-de-dados-dos-componentes)

   2.4. [Disponibilidade](#24-disponibilidade)
   
   2.5. [E2E do Estudo Ampliado](#25-e2e-do-estudo-ampliado)
***

<br/>

## 1. O que é?
Estudo Ampliado é um método que consiste em organizar determinado projeto, baseando-se em **camadas**, facilitando a compreensão de toda a obra do sistema.

<details> 
   <summary>Saiba mais aqui</summary>

   - Em resumo, o método é separado por todo um processo de consulta ao projeto, desde seu diretório raíz até seus códigos, isto é, quando for aberta a pasta onde está a aplicação, considera-se que você já esteja realizando o primeiro processo (na primeira camada), no qual irá ser completado apenas quando for aberta e analizada todas as outras pastas restantes.

   - E você deve estar se perguntando: como assim baseado em camadas? Bom, como exemplo vamos utilizar esse estudo para comparar: uma imagem de ultra resolução e um projeto:

      - **Sobre a imagem:** Suponhamos que seja uma figura de uma cidade vista de cima, sendo possível enxergar somente sua forma, pois as ruas, casas, prédios e tudo o que há nela está minúsculo, entretanto, se a ampliarmos um pouco, aí sim veremos seus componentes. Em virtude disso, a cada aproximação será visto mais detalhes dessa zona urbana, fazendo com que saibamos toda sua composição obtendo mais informação possível.

      - **Comparando ao projeto:** no sistema, a primeira camada começa quando é **analizado** e **entendido** todas as principais pastas contidas nele, por outro lado, a partir do momento em que **analizamos** aquela imagem e **entendemos** que se trata de uma cidade, a lógica é a mesma quando abrimos a [estrutura de pastas](#I-Estrutura-de-Pastas) e descobrimos suas funções.

   ###
</details>

<br>

## 2. Percorrendo Camadas
As camadas, vão determinar em qual nível de entendimento você está em relação ao software, além disso, uma vez que é iniciado cada etapa, a forma de análise varia conforme o avanço. Como propósito de demonstração, será utilizado uma aplicação real logo abaixo.

### 2.1. Estrutura de Pastas
> **Camada I**

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


### • Front End

Temos então `public` e `src` como as duas principais pastas para a criação da página, sendo **public** responsável por desenhar, redirecionar e mostrar o resultado do nosso código fonte, buscado diretamente do **src** (source).

###

<img height="200" align="center" src="https://user-images.githubusercontent.com/83969467/152814920-e7a37634-de52-4dbc-a294-b93dc9cb7315.png" alt="Diretório Raíz" title="Diretório Raíz">

###

**public** - contém apenas dois arquivos: o primeiro é o **index.html**, cuja função é trazer e renderizar todo o código vindo de **src**. E o segundo é o **_redirects** usado como configuração de redirecionamento para hospedar o website no [Netlify](https://www.netlify.com/).

<details> 
   <summary>Ver pasta</summary>

   ###
   <img align="center" src="https://user-images.githubusercontent.com/83969467/152815294-83b61296-8ec5-4cfa-b0f9-23af62138e4b.png" alt="Diretório Raíz" title="Diretório Raíz"> 
</details> 

<br/>

**source/src** - É compostos por algumas pastas (havendo mais pastas e/ou arquivos dentro) que vão formar módulos e componentes, para depois serem encapsulados na tag `<App/>` dentro do renderizador do `ReactDOM`, que também faz a busca do `id="root"` que foi criado em **public**.

<details>
   <summary>Ver pasta e mais detalhes</summary> 

   ###

   <img align="center" src="https://user-images.githubusercontent.com/83969467/152816811-7660c14c-5fcd-4d09-bc22-3a3023232f1c.png" alt="Diretório Raíz" title="Diretório Raíz"> 

   ###
   Todas os nomes citados abaixo, são pastas que vão conter outras pastas e/ou arquivos dentro delas.

   - **assets**: contém nossos bens/recursos de folha de estilo, imagens, fontes e até scripts. Ou seja, é o complemento de conteúdo.

   - **components**: permite você dividir a UI em partes independentes, reutilizáveis e pensar em cada parte isoladamente. 

   - **pages**: obtém cada página com sua interface completa, acrescentado de regra de negócio, captura de argumento passado na rota determinada e manipulação de estrutura de dados.

   - **types**: cria a estrutura de tipos do frontend integrando-a à API.

   - **ultils**: guarda arquivos utilitários para axiliar funções específicas no projeto, como por exemplo a validação de email e criação de variável de ambiente. 

</details> 

<br>

### • Back End
### 2.2. Componentes da Aplicação
> **Camada II**

... 

### 2.3. Fluxo de Dados dos Componentes
> **Camada III**

...

### 2.4. Disponibilidade
> **Camada IV**

...

### 2.5. E2E do Estudo Ampliado
> **Camada V**

...


