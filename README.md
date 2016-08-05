# Construindo uma Aplicação E-commerce com MEAN (livro)

## Resumo dos Capítulos e Anotações Relevantes

### Capítulo 1 - Introdução

* **MongoDB**;  
* **ExpressJS**;  
* **AngularJS**;  
* **NodeJS**.

Algumas empresas, como Walmart, Groupon, Netflix, etc, optaram pelo NodeJS devido a sua escalabilidade e ganho em performance e produtividade. E desistiram de frameworks *enterprise*, como Spring MVC, Java e RoR (Ruby on Rails).


* Programação assíncrona;
* Uma única linguagem, desde o front-end ao back-end, JAVASCRIPT s2;
* APIs baseadas em JSON, SPAs, real time apps.


#### Funcionamento das SPAs e aplicativos MEAN

Quando uma solicitação do cliente, via navegador, chega para o servidor, o primeiro a recebe-lá é o *ExpressJS*, que roda sobre o *NodeJS*, que conecta, se necessário, ao *MongoDB*. E por fim, o *ExpressJS* devolve a resposta do pedido pro cliente.

1. Usuário envia requisição;
2. ExpressJS recebe e trata, sobre o *NodeJS*;
3. Chama o MongoDB, se necessário;
4. Devolve a resposta da requisição pro usuário.


#### NodeJS

Plataforma que permite rodar código JS no servidor, fora do navegador.

#### ExpressJS

É um framework web para o NodeJS. É um servidor web bastante transparente que não permite apenas criarmos apps web, mas como expor APIs, RESTful, JSON. Bastante modular.

#### MongoDB

Banco de dados orientado a documentos, NoSQL.

#### AngularJS

Framework MVC, para o front-end. Para aprimorarmos as tags HTML e manter o sincronismo das views e models em tempo real. Facilita a criação de SPAs.


#### Comandos para Rodar a aplicação

`grunt`: monta a aplicação;  
`grunt serve`: visualiza o app em modo de desenvolvimento;  
`grunt serve:dist`: visualiza o app em modo de produção.  
*Para rodar o app, o serviço do MongoDB deve estar sendo executado*


#### Estrutura de arquivos

```
app
|--- client
|------ app > componentes específicos do app
|------ assets > fontes, img, etc
|------ components > componentes reusaveis ou que não sejam específicos do app
|
|
|--- e2e > end to end > testes
|
|
|--- server
|------ api > API do srv para as aplicações
|------ auth > autenticação
|------ components > componentes reusáveis do app
|------ config > configuração do app
|--------- local.env.js > variáveis de ambiente
|--------- environment > configuração de ambiente do Node
|------ views > views renderizadas pelo servidor
```


#### Requisitos do MVP

* Adicionar produtos com título, preço, descrição, foto e quantidade;
* Página de checkout (pagamento) de produtos para usuários não cadastrados;
* Uma integração de pagamento (PayPal).

##### User stories

1. Como **vendedor**  
1.1 **criar produtos**;

2. Como **usuário**  
2.1 **ver todos os produtos publicados e informações sobre eles** quando clico no link do produto;  
2.2 **buscar produtos** para encontrar rapidamente o que estou procurando;  
2.3 ter um **menu por categoria**;  
2.4 ter **informação em tempo real** sobre o produto, se tem em estoque, esgotado;  
2.5 **pagar os produtos sem fazer login**;  
2.6 **criar um conta** para salvar meus dados, endereço de entrega, histório de compras, vender produtos;  

3. Como **administrador**  
3.1 **gerenciar os papéis dos usuários**, para criar admins, vendedores e também revogar permissão de vendas;  
3.2 **gerenciar todos os produtos**, banir os que não forem apropriados;  
3.3 **resumo de atividades** e estado dos pedidos.  


### Capítulo 2 - AngularJS

AngularJS > *HTML enhanced for web apps* (HTML apriomarado para apps web)

Nos últimos 20 anos, O JS tem sido usado basicamente para validação de formulários, animações e efeitos visuais. No seu inicio, testes de código JS era manual. O AngularJS é conhecido por sua excelência em testabilidade e possui inúmeros testes e *test runners*. Karma, para automação nativa de testes; Protractor para testes fim a fim.


#### Diretivas

São extensões HTML na forma de atributos, tags, classes CSS e até mesmo comentários HTML.

* ng-app;  
* ng-class;  
* ng-view;  
* ui-views;  
* etc.


#### Módulos

O AngularJS oferece uma variável global que contém muitas funções, como `module`.

A função `angular.module` pode funcionar tanto como *getter* ou *setter*.  

* *getter*: chamando o módulo;  
* *setter*: configurando o módulo.


#### Rotas no AngularUI

A funcionalidade de roteamento permite que o usuário tenh uma URL, que vai refletir exatamente o estado atual da aplicação.  

O roteador do AngularJS UI permite definir views e estados. Rotas, controllers e estados são associados a templates HTML através do `$stateProvider`.


#### Controllers e Escopos

Um *controller* interage com as views e os models. Os *controllers* são responsáveis pela carga dos dados e sua representação nas *views*.


##### O que é o `$http`?

É um serviço nativo do AngularJS que facilita a comunicação com servidores remotos. Será utilizado para fazer a comunicação com o servidor ExpressJS.


##### O que é o `$scope`?

É um objeto que "cola" o *controller* às *views*, providenciando a famosa vinculação de mão dupla. Cada vez que uma variável é atualizada no `$scope`, a alteração é renderizada automaticamente no HTML. E vice-versa.


#### Fábricas (`factory`) e Serviços (`services`)

Serviços são objetos ou funções únicas vinculadas aos *controllers* ou outros componentes usando um recurso chamado **Injeção de Dependência (Dependency Injection - DI)**. O `this` assume a instância da função. Retornam um construtor de função, e é necessário usar o operador `new`.

As fábricas permitem criar *closures*. Onde o `this` assume o valor devolvido pela função ao ser chamada.


#### Criando um catálogo

* `ui-sref`: chama o estado especificado e passa os parâmetros que combinem com o URL definido nas rotas.


#### Filtros

Permitem modificar a saída de uma expressão. Seja no DOM com pipe ou usando o serviço `$filter`.


#### CRUD

* Create;  
* Read;  
* Update;  
* Delete.

Primeiramente será feito um CRUD independente do servidor, os dados estarão na memória.

* `query` vai retornar todos os produtos da coleção;  
* `get` vai retornar apenas um dos produtos.

Nada externo à fábrica terá acesso a `example_products`. Ela é privada, enquanto todos os métodos no objeto devolvido são públicos. Essa técnica é conhecida como **fechamento (closure)**.

* `$state`: permite redirecionamento para um estado ou rota diferente;  
* `$stateParams`: é um objeto que contém todas as variáveis da URL.


#### Rotas

* `ng-model`: ele vincula o produto a `$scope.product`.

> Os nomes de templates parciais, por exemplo, o formulário de novo produto, devem começar com um caractere de sublinhado.


### Capítulo 3 - MongoDB

Os banco de dados são a parte mais crítica em uma aplicação de ecommerce. Eles precisam ser flexíveis o bastante para se adaptar as necessidades de crescimento e ser adequado ao catálogo atual de produtos. Além disso, a escalabilidade é outro fator importante.

* Quantos pedidos por minuto a aplicação suporta?  
* Qual o tempo médio de resposta durante os picos de acesso? E durante os periodos tranquilos?  
* Quanto tempo leva para encontrar um produto quando o inventário é grande?  
* O schema usado hoje é suficiente para demandas futuras?  

O NoSQL concentra-se em **escalabilidade**, **desempenho** e **alta disponibilidade**.

O fato de o MongoDB ser independentes de *schemas* traz uma grande flexibilidade para a aplicação, devido que podemos adicionar campos sem que seja necessário alterar os dados anteriores.


#### Aggregators (Agregadores)  

* `$sum`: soma todas as linhas/campos;  
* `$match`: filtra documentos baseado na query informada;  
* `$group`: GROUP BY;  
* `$sort`: ORDER BY.


##### Exemplo 1 - Soma o preço de todos os produtos

```js
db.products.aggregate([{
  $group: {
    _id: null,
    total: { $sum: $price }
  }
}])
```

##### Exemplo 2 - Soma o preço de todos os produtos por título e mosta apenas cujo título é Product

```js
db.products.aggregate([
  {
    $match: { title: 'Product' }
  },
  {
    $group: {
      _id: '$title',
      total: { $sum: '$price' }
    }
  }
])
```


#### Schemas

São a maneira pela qual o Mongoose define tipos de dados e a validação aos documentos do MongoDB. O Mongoose permite que sejam estabelecidos *schemas* rigorosos e flexíveis.


#### Middlewares no Mongoose

É um conjunto de *hooks* que são executados antes (**pre**) ou depois (**post**) de certas ações, como inicialização, validação, atualização, gravação ou apagamento. São normalmente usados para disparar eventos personalizados e executar tarefas assíncronas ou validações complexas.


#### CommonJS

Oferece módulos em JavaScript para rodarem no servidor e resolverem problemas de dependência e escopo.  

* `require`;  
* `module.exports`;  
* `exports`: função similiar a `module.exports`. Sempre devolvem o objeto `module.exports` e não a função `exports`.


### Capítulo 4 - NodeJS e ExpressJS

#### API RESTful

**- REST: REpresentation State Transfer** ou **transferência de estado representacional**

É um padrão moderno para criar serviços web escalonáveis. Sua aceitação se dá conta devido a sua simplicidade, desempenho e facilidade de manutenção. O ExpressJS é um dos servidores web mais populares que rodam sobre o NodeJS e tem suporte nativo a APIs do tipo RESTful sobre HTTP e JSON.  

O REST é uma interface uniforme, não orientada a eventos. Baseia-se no protocolo HTTP, usando os métodos verbais: **GET**, **POST**, **PUT**, **PATCH** e **DELETE**.  

**- URI - Uniform Resource Identifier** ou **identificador uniforme de recursos**.  

* PUT vs PATCH: PUT é usado para substituir completamente um recurso existente, enquanto PATCH é usado para atualizações parciais desse recurso.


#### ExpressJS

É um servidor web composto principalmente de rotas, middlewares e views. No MEANSHOP será usado apenas as rotas e middlewares, as views ficam com o AngularJS.

O middleware é uma função que possui 3 parâmetros: `request`, `response` e `next`. Diferente das rotas que não possui `next`.
