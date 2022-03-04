# 2.4. Disponibilidade
> ### Sumário

1. [Introdução](https://github.com/Sancruz-dev/estudo-ampliado#1-introdução)

2. [Percorrendo Camadas](https://github.com/Sancruz-dev/estudo-ampliado#2-percorrendo-camadas)

   2.1. [Estrutura de Pastas](/camadas/i-estrutura-de-pastas#21-estrutura-de-pastas)
      1. [Diretório Frontend](/camadas/i-estrutura-de-pastas#i-diretório-frontend)
      2. [Diretório Backend](/camadas/i-estrutura-de-pastas#ii-diretório-backend)

   2.2. [Componentes da Aplicação](/camadas/ii-componentes-da-aplicacao#22-componentes-da-aplicação)
      1. [Front-end e seus Componentes](/camadas/ii-componentes-da-aplicacao#i-front-end-e-seus-componentes)
      2. [Back-end e seus Componentes](/camadas/ii-componentes-da-aplicacao#ii-back-end-e-seus-componentes)

   2.3. [Fluxo de Dados](/camadas/iii-fluxo-de-dados#23-fluxo-de-dados)
      1. [Entrada e Saída](/camadas/iii-fluxo-de-dados#i-entrada-e-saída)
      2. [Armazenamento e Processo](/camadas/iii-fluxo-de-dados#ii-armazenamento-e-processo)
      3. [Tratamento](/camadas/iii-fluxo-de-dados#iii-tratamento)

   2.4. [Disponibilidade](#)
      1. [Comunicação API RESTful](#i-comunicação-api-restful)
      2. [Endpoints](#ii-endpoints)
***

### **4ª Camada**

A forma como uma aplicação é disponibilizada para quem vai utilizá-la, faz parte da arquitetura de projetos. Portanto, o aplicativo que analisamos é uma API em REST, ou seja, é uma API que se modela aos princípios de projeto do estilo de arquitetura do Representational State Transfer.

## I. Comunicação API RESTful

A comunicação, é feita por via de solicitações HTTP para executar o CRUD em um recurso. Por exemplo, uma API REST usaria uma solicitação GET para recuperar um registro, uma solicitação POST para criar um registro, uma solicitação PUT para atualizar um registro e uma solicitação DELETE para excluir um registro. 

Todos os métodos HTTP podem ser usados em chamadas da API. Uma API de REST bem projetada é semelhante a um website em execução em um navegador da web com funcionalidade HTTP integrada.

<br/>

## II. Endpoints

Os ***endpoints*** disponibilizados no projeto são: cliente, servidor do Netlify juntamente com o servidor do Heroku.

Os dados que a API espera receber dos ***endpoints***, é simplesmente as informações que estão armazenadas nos servidores com as que o usuário inserir na aplicação. Em suma, é os dados relacionados ao filme (como o nome, imagem, média e quantidade total de avaliação), e ao usuário (como seu email e avaliação sobre o filme). 

Quando os ***endpoints*** forem chamados, as respostas serão fornecidas à API de acordo com o que a página pede: 

- Se a página for a de listagem, então a saída será todas as informações de cada filme, para serem exibidas em tela. 

- E se for uma página de formulário, a respota será as informações do filme ESCOLHIDO pelo usuário, juntamente com o armazenamento dos dados inseridos (email e avaliação).

<br/>

> ### [Voltar ao início :leftwards_arrow_with_hook:](https://github.com/Sancruz-dev/estudo-ampliado)
