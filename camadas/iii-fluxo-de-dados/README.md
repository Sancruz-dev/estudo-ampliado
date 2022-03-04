# 2.3. Fluxo de Dados
> ### Sumário

1. [Introdução](https://github.com/Sancruz-dev/estudo-ampliado#1-introdução)

2. [Percorrendo Camadas](https://github.com/Sancruz-dev/estudo-ampliado#2-percorrendo-camadas)

   2.1. [Estrutura de Pastas](/camadas/i-estrutura-de-pastas#21-estrutura-de-pastas)
      1. [Diretório Frontend](/camadas/i-estrutura-de-pastas#i-diretório-frontend)
      2. [Diretório Backend](/camadas/i-estrutura-de-pastas#ii-diretório-backend)

   2.2. [Componentes da Aplicação](/camadas/ii-componentes-da-aplicacao#22-componentes-da-aplicação)
      1. [Front-end e seus Componentes](#i-front-end-e-seus-componentes)
      2. [Back-end e seus Componentes](#ii-back-end-e-seus-componentes)

   2.3. [Fluxo de Dados](#)
      1. [Entrada e Saída](#i-entrada-e-saída)
      2. [Armazenamento e Processo](#ii-armazenamento-e-processo)
      3. [Tratamento](#iii-tratamento)

   2.4. [Disponibilidade](/camadas/iv-disponibilidade#24-disponibilidade)
      1. [Comunicação API RESTful](/camadas/iv-disponibilidade#i-comunicação-api-restful)
      2. [Endpoints](/camadas/iv-disponibilidade#ii-endpoints)
***

### **3ª Camada**

> _"Como os dados fluem entre as **camadas dos componentes**?"_

A pergunta acima pode ser genérica, mas sem dúvidas desencadeará outras, que vão dar a resposta de como funciona o fluxo de dados em seu projeto. Com efeito, há duas questões essenciais para entender todo o processo: 

- _"Como funciona o fluxo de entrada e saída?"_

- _"As informações são salvas ou processadas por alguma tarefa em segundo plano?"_

<br/>

## I. Entrada e Saída

O **fluxo de entrada e saída** terá como referência o método padrão-camadas (já citado no tópico anterior), devido também estar conectado ao fluxo de dados.

###### <img style="border-radius: 12px" height="300" src="https://user-images.githubusercontent.com/83969467/154807894-15856953-b78a-4ae2-a040-f745b4fd0e6c.png" alt="Figura 12: padrão-camadas" title="padrão-camadas" /> Figura 12: padrão-camadas

De forma geral, podemos imaginar que uma página (qualquer que seja) está abrindo, carregando as informações para serem exibidas em tela: ocasionalmente, o front-end dará **ENTRADA** à requisição para buscar as informações do back-end, e como resposta, é devolvida a **SAÍDA** dessa requisição, que é os dados trazidos do banco.

Sob o mesmo ponto de vista podemos comparar com o método INPUT e OUTPUT através da página de formulário. <br/> Bom, existem dois campos de preenchimento na página: email e avaliação sobre o filme. Uma vez que o usuário envia dados ao banco para que sejam processados e armazenados, já considera-se como uma **entrada** de dados, mas não feita por uma requisição, e sim pelo envio (input) de informações (feito pelo usuário) que serão salvas no sistema. 

Por conseguinte, a saída (output) do campo de avaliação será a exibição da média de avaliações, definidas por todos os usuários do filme correspondente. E o campo de email, não terá uma saída, pois não há uma tela de perfil do usuário que mostre seu email por exemplo, não neste atual projeto.

<br/>

## II. Armazenamento e Processo

Os dados do nosso software podem ser armazenados ou processados por [três tipos de perfis](/camadas/i-estrutura-de-pastas#-resources): **teste, desenvolvimento e produção**.

- O tipo **teste** implementa o processo das informações em segundo plano, para que o sistema seja testado e seus dados salvos de maneira simples e rápida. Tarefa exercida pelo _H2 Database_.

- O perfil de **desenvolvimento** estabelece uma simulação de produção, para que os elementos sejam guardados num banco de dados local, usando o _PostgreSQL_.

- Por fim, o perfil do tipo **produção** é o "deploy do banco", ou seja, os dados são implantados na nuvem para que possam ser acessados via web, sendo gerenciado pelo SGBD Heroku.

<br/>

## III. Tratamento

A forma de tratamento dos dados na aplicação é realizado através do Mapeamento Objeto-Relacional JPA (Java Persistence API), ou seja, é utilizado um framework no intuito de atingir os objetos Java simples e comuns.

E para que o sistema seja monitoriado pelo JPA, usa-se _**@annotations**_ na intenção de "pré-processar" funções determinadas. Existem várias _annotations_ disponibilizadas pelo framework, então abaixo está algumas utilizadas no projeto:

``` java
@Entity
@Table(name = "tb_movie")
public class Movie {
	
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;

   /* [ ... ] */
}
```

Perceba que antes que da classe há uma instanciação `@Entity`, isto é, uma _JPA annotation_ que vai tratar a classe como uma entidade dentro do seu sistema, e por analogia, `@Table` vai definir como a tabela será chamada no SGBD. <br/> Além disso, no código há o `@Id` e `@GenerateValue`: respectivamente, indicam que o atributo criado abaixo deles será um **id** com **numeração automática** a cada nova linha adicionada à tabela.

<br/>

*** 

> ### [Próxima camada :arrow_right:](/camadas/iv-disponibilidade#24-disponibilidade)

> ### [Voltar camada :leftwards_arrow_with_hook:](/camadas/ii-componentes-da-aplicacao#22-componentes-da-aplicação)