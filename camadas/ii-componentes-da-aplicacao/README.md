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

É de suma importância entender que o código fonte (src) React nada mais é do que **interação de componentes**, isto é, TODAS as `function's` são componentes que  retornam HTML.

Haja vista, o tratamento das requisições e seus estados - do projeto de demonstração - é o uso de seus valores como resposta às funções que tem como objetivo buscá-las, tais componentes como:

- **FormCard** - Captura o argumento passado na rota, sendo esse, o identificador do filme escolhido para avaliar. 

- **Form** - a partir da obtenção da `id` do filme passado como argumento, o Form faz a requisição utlizando o useEffect.

- **Listing**

<br/>

## II. Back-end e seus Componentes
...