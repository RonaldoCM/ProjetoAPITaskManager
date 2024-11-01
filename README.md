
# APITaskManager
API RESTful para gerenciar tarefas.
A ideia é que a API permita a criação, leitura, atualização e exclusão de tarefas usando o banco de dados em memória do Entity Framework Core.
O maior objetivo é explorar o banco de dados em memória do Entity Framework Core.

Para esse objetivo criei a APITaskManager, com a ideia de ter uma API que realizasse as premissas citadas acima (CRUD), utilizando o Swagger como documentação e teste.

## Requisitos Funcionais
Instalação prévia de um IDE (Integrated Development Environment) que possa abrir um projeto 
do tipo API .Net Core. (Vs ou Vs Code).
E a instalação dos packages: 
* Autofac
* EntityFrameworkCore
* EntityFrameworkCore.InMemory
O Swashbuckle.AspNetCore é instalado automaticamente na criação do projeto.

<img src="https://github.com/RonaldoCM/API/blob/main/APITaskManager/Imagens/requisitos.png" alt="Requisitos">

## Descrição
A APITaskManager, foi criada com a ideia de ter uma API que realizasse as premissas de inclusão, edição e 
exclusão de tarefas, utilizando o Swagger como documentação e testes.
O projeto segue a seguinte estrutura:

<img src="https://github.com/RonaldoCM/API/blob/main/APITaskManager/Imagens/descricao.png" alt="Descrição">

Onde separei as responsabilidades por diretórios.
* Controllers = Implementação dos controllers onde as requisições externas serão recebidas.
* DTO – Data Transfer Objects => Para definir as classes de comunicação. A implementação Global permitirá a criação de subdiretórios a medida que o projeto evoluir. Por hora, tenho 
apenas a classe TarefaDTO que implementa a estrutura de comunicação com os Endpoints.
* IoC – Inversion of Control – Implementação da Inversão de controle, para permitir o registro dos serviços e suas dependências (para possibilitar a injeção de dependências e seu cambiamento) na mesma implementação.
* Model – Estruturação da classe e seus requisitos para a manipulação dos serviços da Tarefa e ações com o repositório.
* Repository – Diretório que contém a construção do DbContext da Tarefa.
* Services – Diretório onde foram implementadas as ações e lógica das classes:

<img src="https://github.com/RonaldoCM/API/blob/main/APITaskManager/Imagens/services.png" alt="Services">

Classe FakeTarefasService – A classe em que expandida a aplicação, poderá servir como um controle Fake, que implementa a mesma interface de serviços ITarefaService que a classe oficial (de produção) TarefasService.
Classe ITarefaService – Define as implementações, ações que são obrigatórias para as classes que a herdam.
TarefaService – Seria a implementação oficial dos serviços disponíveis no Controller.

Com essa descrição da Estrutura está disponível para requisições os métodos:

<img src="https://github.com/RonaldoCM/API/blob/main/APITaskManager/Imagens/verbos.png" alt="Verbos">

Para serem requisitados por chamadas externas vindas do controller TarefasController.
O construtor desse controller está preparado para inicializar os objetos de ITarefaService.
Podendo receber e inicializar outras implementações de outras interfaces que possam vir a 
serem implementadas.

<img src="https://github.com/RonaldoCM/API/blob/main/APITaskManager/Imagens/controller.png" alt="Controller">

## Observações Gerais

Sobre o Banco de dados em memória do Entity Framework Core. Essa funcionalidade permite que você utilize um banco de dados totalmente funcional em memória do seu aplicativo.
Particularmente, sabia que existia, mas nunca havia utilizado. As APIs as quais eu dou manutenção são conectadas diretamente com um banco de dados relacional e as poucas experiências que tive criando APIs, geralmente, começo criando um diretório de entidades, para criação da base de dados, antes de qualquer evolução, abordagem Model-First.
A maior dificuldade dessa implementação foi evoluir as implementações de Injeção de dependências e Inversão de controle.
Como o projeto está aberto, existem possibilidades de mudanças, a medida que novas implementações ocorrerem, alguns arquivos ou diretórios podem surgir ou mudar de nó na estrutura.
O DTO, por exemplo é um diretório que pode se tornar subdiretório do Services, para indicar que apenas DTO’s relacionados aos serviços de Tarefas estarão ali, dando características da abordagem de micro serviços.

## Autor
Ronaldo Costa Miranda
