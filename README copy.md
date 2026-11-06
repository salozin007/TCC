# DOCUMENTAÇÃO TÉCNICA DO SISTEMA
# E.E. MONSENHOR BICUDO

**Projeto:** Sistema de gerenciamento escolar E.E. Monsenhor Bicudo  
**Área:** Desenvolvimento de Sistemas  
**Tipo de aplicação:** Sistema Web  
**Tecnologias principais:** Angular, Node.js, Express e MySQL  
**Versão do documento:** 1.0 – Documentação preliminar

---

# 1. INTRODUÇÃO

O Sistema E.E. Monsenhor Bicudo é uma aplicação web desenvolvida com o objetivo de facilitar a divulgação e o gerenciamento de informações escolares.

A plataforma reúne informações importantes da instituição em um único ambiente, permitindo que os usuários consultem o cardápio semanal, acompanhem avisos e comunicados e visualizem eventos escolares por meio de um calendário integrado.

O sistema também possui uma área administrativa protegida por autenticação, destinada ao gerenciamento das informações disponibilizadas no site.

A aplicação utiliza uma arquitetura dividida entre Front-end, Back-end e banco de dados, permitindo a organização das funcionalidades e a comunicação entre a interface e os dados armazenados.

# 2. OBJETIVOS DO PROJETO

## 2.1 Objetivo geral

Desenvolver um sistema web para centralizar informações da Escola Estadual Monsenhor Bicudo, facilitando o acesso da comunidade escolar a comunicados, cardápios e eventos.

## 2.2 Objetivos específicos

- Disponibilizar o cardápio escolar de maneira organizada.
- Facilitar a consulta de avisos e comunicados.
- Apresentar os eventos escolares em um calendário.
- Permitir o gerenciamento das informações por meio de uma área administrativa.
- Armazenar os dados em um banco de dados MySQL.
- Implementar autenticação para o acesso administrativo.
- Organizar a interface para facilitar a navegação dos usuários.

# 3. JUSTIFICATIVA

A utilização de uma plataforma digital contribui para melhorar a organização e a divulgação das informações escolares.

A centralização de conteúdos como cardápios, avisos e eventos facilita a consulta por parte dos estudantes e demais integrantes da comunidade escolar.

Além disso, a área administrativa permite que as informações sejam gerenciadas de forma centralizada, reduzindo a necessidade de alterações diretamente no código-fonte para atualizar os conteúdos do site.

# 4. TECNOLOGIAS UTILIZADAS

O projeto utiliza tecnologias voltadas ao desenvolvimento de aplicações web.

## 4.1 Angular

O Angular é utilizado no desenvolvimento do Front-end, responsável pela interface visual e pela interação dos usuários com o sistema.

Por meio dele são organizadas as páginas, os componentes, as rotas e os serviços responsáveis pela comunicação com o Back-end.

## 4.2 Node.js

O Node.js é utilizado para executar o Back-end da aplicação, permitindo a execução de código JavaScript no servidor.

Ele é responsável por processar as solicitações recebidas pelo sistema e realizar operações relacionadas aos dados.

## 4.3 Express

O Express é um framework utilizado junto ao Node.js para estruturar o servidor e criar as rotas da API.

Ele permite implementar operações de consulta, cadastro, atualização e exclusão de informações.

## 4.4 MySQL

O MySQL é o sistema de gerenciamento de banco de dados utilizado para armazenar as informações do projeto.

Ele organiza os dados em tabelas relacionadas, permitindo que o sistema consulte e atualize informações de maneira estruturada.

## 4.5 Bcrypt

O Bcrypt é utilizado para realizar a verificação das senhas dos usuários administrativos.

O sistema compara a senha informada no login com o hash armazenado no banco de dados.

## 4.6 CORS

O CORS é utilizado no servidor para configurar o controle de acesso às solicitações realizadas entre diferentes origens.

## 4.7 Outras dependências

- `mysql2/promise`: utilizado para realizar a comunicação com o MySQL por meio de operações assíncronas.
- `express.json()`: permite que o servidor interprete dados enviados em formato JSON.

# 5. ARQUITETURA DO SISTEMA

O sistema está organizado em três partes principais:

**Front-end:** responsável pela interface visual, navegação e interação com os usuários.

**Back-end:** responsável pelo processamento das solicitações, autenticação e execução das operações relacionadas aos dados.

**Banco de dados:** responsável pelo armazenamento das informações utilizadas pela aplicação.

## 5.1 Fluxo de funcionamento

1. O usuário acessa o site pelo navegador.
2. O Front-end apresenta as informações e funcionalidades disponíveis.
3. Quando necessário, o Front-end realiza uma solicitação à API.
4. O Back-end recebe e processa a solicitação.
5. O servidor realiza consultas ou alterações no banco de dados.
6. O resultado é retornado ao Front-end.
7. A interface apresenta as informações ao usuário.

# 6. ESTRUTURA DO BANCO DE DADOS

O banco de dados utilizado no projeto é denominado `monsenhor_bicudo`.

Ele possui tabelas responsáveis pelo armazenamento dos usuários, horários, cardápios, avisos e outras informações utilizadas pelo sistema.

## 6.1 Tabela Usuario

Armazena os dados dos usuários cadastrados para acessar o sistema.

| Campo | Descrição |
|---|---|
| id_usuario | Identificador único do usuário |
| email | Endereço de e-mail |
| senha | Hash da senha armazenada |
| criado_em | Data de criação do registro, presente na estrutura criada pelo Back-end |

O campo `id_usuario` é a chave primária, enquanto o e-mail possui restrição de unicidade.

## 6.2 Tabela Horario

Armazena os horários e os dias associados às refeições do cardápio.

| Campo | Descrição |
|---|---|
| id_horario | Identificador do horário |
| hora | Código correspondente ao período da refeição |
| dia | Data ou identificação do dia, conforme a estrutura utilizada |

Os códigos de refeição são:

- `0` – Café da manhã.
- `1` – Almoço.
- `2` – Café da tarde.

## 6.3 Tabela Cardapio

Armazena os alimentos e refeições disponibilizados no cardápio escolar.

| Campo | Descrição |
|---|---|
| id_cardapio | Identificador do item |
| comida | Nome ou descrição do alimento |
| fk_id_horario | Referência ao horário correspondente |

O campo `fk_id_horario` estabelece um relacionamento com a tabela `Horario`.

A exclusão de um horário também pode excluir os itens de cardápio relacionados, devido à configuração `ON DELETE CASCADE`.

## 6.4 Tabela Aviso

Armazena os comunicados e avisos divulgados pela instituição.

| Campo | Descrição |
|---|---|
| id_aviso | Identificador do aviso |
| titulo | Título do comunicado |
| categoria | Categoria do aviso |
| descricao | Descrição do comunicado |
| data | Data relacionada ao aviso |
| horario_comeco | Horário de início |
| horario_final | Horário de término |
| evento_dia | Indica se existe relação com um evento do dia |
| importante | Identifica avisos importantes |
| publicado | Situação de publicação, presente na estrutura do Back-end |
| criado_em | Data de criação do registro |

## 6.5 Tabela OpcaoAlimento

Essa tabela é criada pelo Back-end e armazena opções de alimentos associadas às refeições.

Entre seus campos estão:

- `id_opcao`: identificador da opção.
- `refeicao_id`: referência da refeição.
- `nome`: nome da opção de alimento.

Existe uma restrição para evitar a repetição do mesmo nome de opção para uma mesma refeição.

## 6.6 Tabela Evento

Armazena informações dos eventos apresentados no calendário escolar.

Entre os campos utilizados estão:

- `id_evento`: identificador do evento.
- `titulo`: título do evento.
- `descricao`: descrição.
- `categoria`: categoria do evento.
- `cor`: identificação visual por cor.
- `data`: data do evento.
- `horario`: horário.
- `local`: local de realização.
- `criado_em`: data de criação do registro.

**Observação sobre a estrutura do banco:** o script SQL enviado manualmente apresenta as tabelas `Usuario`, `Horario`, `Cardapio` e `Aviso`. Entretanto, o arquivo `db.js` também cria as tabelas `OpcaoAlimento` e `Evento`, além de acrescentar alguns campos e utilizar tipos diferentes em determinadas colunas. Portanto, a estrutura efetivamente utilizada deve ser conferida no banco criado pelo Back-end.

# 7. DESCRIÇÃO DAS TELAS DO SISTEMA

## 7.1 Tela de Login

A tela de login é destinada ao acesso administrativo.

Ela apresenta campos para preenchimento de e-mail e senha, permitindo que o usuário informe suas credenciais para acessar a área de administração.

O Back-end realiza a consulta do usuário no banco de dados e utiliza o Bcrypt para verificar a senha informada.

Caso as credenciais sejam válidas, o login é autorizado. Caso contrário, o servidor retorna uma resposta indicando falha na autenticação.

## 7.2 Página Inicial

A página inicial apresenta a identidade visual da Escola Estadual Monsenhor Bicudo.

Ela funciona como ponto de entrada para os usuários e reúne informações de destaque, incluindo o cardápio do dia e os avisos escolares.

A navegação permite acessar as demais áreas públicas do sistema.

## 7.3 Página Cardápio Semanal

A página do cardápio apresenta as refeições organizadas por dia da semana.

As refeições são divididas em três períodos:

- Café da manhã.
- Almoço.
- Café da tarde.

A organização permite que os estudantes consultem os alimentos previstos para cada dia.

Os dados são obtidos por meio da API e relacionados aos horários armazenados no banco de dados.

## 7.4 Página de Avisos

A página de avisos reúne comunicados e informações importantes da escola.

Os avisos possuem informações como título, categoria, descrição e data.

Também podem apresentar horários, indicação de evento do dia e identificação de importância.

Essa organização facilita a consulta dos comunicados escolares.

## 7.5 Página Sobre Nós

A página Sobre Nós apresenta informações institucionais da escola.

Entre os conteúdos identificados na interface estão:

- História da instituição.
- Missão.
- Visão.
- Valores.
- Tecnologias.
- Informações sobre o curso técnico.

A página tem a finalidade de apresentar a instituição e seu contexto educacional.

## 7.6 Painel Administrativo

O painel administrativo é destinado ao gerenciamento das informações do site.

A interface apresenta opções para acessar o gerenciamento de cardápios e avisos.

O acesso à área administrativa é associado ao processo de autenticação por e-mail e senha.

## 7.7 Gerenciamento de Cardápio

O gerenciamento do cardápio permite trabalhar com os itens e horários das refeições.

O Back-end disponibiliza operações para consultar, cadastrar, atualizar e excluir itens do cardápio.

Também existe uma operação específica para salvar uma refeição completa, além de rotas para consultar e cadastrar opções de alimentos.

## 7.8 Gerenciamento de Avisos

A área de gerenciamento de avisos permite realizar operações relacionadas aos comunicados escolares.

O servidor disponibiliza funcionalidades para:

- Consultar avisos.
- Consultar um aviso específico.
- Cadastrar novos avisos.
- Atualizar avisos existentes.
- Excluir avisos.

## 7.9 Calendário Escolar

O calendário apresenta os eventos organizados por datas.

A interface recebida mostra uma visualização mensal, categorias e uma lista de eventos.

O Back-end possui uma estrutura própria para armazenar os eventos e disponibiliza operações de consulta, cadastro, atualização e exclusão.

# 8. BACK-END E API

O Back-end foi desenvolvido utilizando Node.js e Express.

O arquivo `server.js` concentra a configuração do servidor e as rotas responsáveis pela comunicação com o banco de dados.

A API recebe solicitações HTTP e retorna respostas, normalmente em formato JSON.

## 8.1 Rota principal

| Método | Rota | Finalidade |
|---|---|---|
| GET | `/` | Verificar o funcionamento do servidor |

## 8.2 Autenticação e usuários

| Método | Rota | Finalidade |
|---|---|---|
| POST | `/login` | Realizar a autenticação |
| GET | `/usuario/:id` | Consultar informações de um usuário pelo identificador |

## 8.3 Rotas do cardápio

| Método | Rota | Finalidade |
|---|---|---|
| GET | `/cardapio` | Consultar todos os itens do cardápio |
| GET | `/cardapio/opcoes` | Consultar opções de alimentos |
| POST | `/cardapio/opcoes` | Cadastrar uma opção de alimento |
| GET | `/cardapio/id/:id` | Consultar um item pelo identificador |
| GET | `/cardapio/:dia` | Consultar o cardápio de uma data |
| POST | `/cardapio/refeicao` | Salvar uma refeição completa |
| POST | `/cardapio` | Cadastrar um item |
| PUT | `/cardapio/:id` | Atualizar um item |
| DELETE | `/cardapio/:id` | Excluir um item |

## 8.4 Rotas de avisos

| Método | Rota | Finalidade |
|---|---|---|
| GET | `/avisos` | Consultar os avisos |
| GET | `/avisos/:id` | Consultar um aviso específico |
| POST | `/avisos` | Cadastrar um aviso |
| PUT | `/avisos/:id` | Atualizar um aviso |
| DELETE | `/avisos/:id` | Excluir um aviso |

## 8.5 Rotas de eventos

| Método | Rota | Finalidade |
|---|---|---|
| GET | `/eventos` | Consultar os eventos |
| GET | `/eventos/:id` | Consultar um evento específico |
| POST | `/eventos` | Cadastrar um evento |
| PUT | `/eventos/:id` | Atualizar um evento |
| DELETE | `/eventos/:id` | Excluir um evento |

# 9. AUTENTICAÇÃO E SEGURANÇA

O sistema possui um mecanismo de autenticação para o acesso administrativo.

O processo identificado no Back-end funciona da seguinte maneira:

1. O administrador informa o e-mail e a senha na tela de login.
2. O Front-end envia os dados ao servidor por meio da rota `POST /login`.
3. O servidor consulta o banco de dados para localizar o usuário.
4. O Bcrypt realiza a comparação entre a senha informada e o hash armazenado.
5. O servidor retorna uma resposta indicando se a autenticação foi realizada com sucesso.

O arquivo `db.js` também utiliza variáveis de ambiente para configurar os dados de conexão com o banco de dados.

**Ponto que ainda precisa ser confirmado:** o código do Front-end e do `adminGuard` ainda não foi analisado. Por isso, não é possível descrever com precisão como o acesso permanece ativo depois do login ou como as rotas administrativas são protegidas. Também não foi identificada emissão de token JWT ou criação de sessão no código do Back-end recebido.

# 10. INICIALIZAÇÃO E CONFIGURAÇÃO DO BANCO

O arquivo `db.js` é responsável pela conexão e inicialização do banco de dados.

Entre suas funções estão:

- Configurar a conexão com o MySQL.
- Verificar se a conexão está funcionando.
- Criar o banco de dados caso ele ainda não exista.
- Criar as tabelas necessárias.
- Executar alterações de estrutura quando necessário.
- Inserir dados iniciais para utilização do sistema.

A inicialização também inclui a criação de um usuário administrativo inicial, com senha armazenada em formato de hash.

Para a configuração do ambiente, o projeto utiliza variáveis como:

- `DB_HOST`: endereço do servidor MySQL.
- `DB_USER`: usuário do banco de dados.
- `DB_PASSWORD`: senha do banco de dados.
- `DB_NAME`: nome do banco.
- `DB_PORT`: porta de conexão.

As credenciais de acesso devem ser configuradas de forma segura, sem serem expostas publicamente no repositório.

# 11. ESTRUTURA DO PROJETO

O repositório GitHub informado apresenta a seguinte estrutura principal:

```text
TCC/
│
├── backend/
│   ├── db.js
│   └── server.js
│
├── frontend/
│   └── Arquivos do Angular
│
├── .gitignore
│
└── package.json
```

O diretório `backend` contém os arquivos responsáveis pelo servidor e pela conexão com o banco de dados.

O diretório `frontend` é destinado à aplicação Angular.

O arquivo `package.json` principal apresenta os comandos utilizados para iniciar o Back-end, iniciar o Front-end e executar os testes do Back-end.

# 12. EXECUÇÃO DO PROJETO

O `package.json` principal apresenta os seguintes comandos:

**Iniciar o Back-end:**

```bash
npm start
```

**Iniciar o Front-end:**

```bash
npm run start:frontend
```

**Executar os testes do Back-end:**

```bash
npm run test:backend
```

Antes da execução, é necessário instalar as dependências do projeto e configurar corretamente a conexão com o banco de dados.

A configuração completa de instalação do Angular e os comandos específicos de preparação do ambiente ainda precisam ser confirmados no Front-end.

# 13. TESTES DO SISTEMA

O projeto possui um comando específico para executar os testes do Back-end:

```bash
npm run test:backend
```

Esse comando executa o arquivo `backend/test-crud.js`, conforme indicado no `package.json`.

Entretanto, os resultados dos testes ainda não foram enviados. Portanto, não é possível afirmar quais operações foram aprovadas ou se todas as funcionalidades estão funcionando corretamente.

Para uma documentação definitiva, recomenda-se registrar testes de:

- Autenticação com credenciais válidas.
- Autenticação com credenciais inválidas.
- Consulta do cardápio.
- Cadastro, atualização e exclusão de refeições.
- Consulta e gerenciamento de avisos.
- Consulta e gerenciamento de eventos.
- Comunicação entre Front-end e Back-end.
- Persistência das informações no banco de dados.

# 14. CONSIDERAÇÕES SOBRE O DESENVOLVIMENTO

O desenvolvimento do Sistema E.E. Monsenhor Bicudo reúne recursos de desenvolvimento Front-end, programação Back-end e gerenciamento de banco de dados.

A divisão entre essas camadas permite organizar o projeto e facilitar a manutenção de suas funcionalidades.

A aplicação busca centralizar informações importantes da instituição, oferecendo um ambiente para consulta pública e outro para gerenciamento administrativo.

# 15. CONCLUSÃO

O Sistema E.E. Monsenhor Bicudo representa uma solução digital voltada à organização e à divulgação de informações escolares.

Por meio das funcionalidades de cardápio semanal, avisos e calendário, a plataforma reúne conteúdos relevantes para a comunidade escolar em um único ambiente.

A área administrativa permite gerenciar informações por meio de operações disponibilizadas pelo Back-end, enquanto o banco de dados MySQL mantém os registros necessários para o funcionamento da aplicação.

O projeto também proporciona a aplicação prática de conhecimentos relacionados ao desenvolvimento web, integração entre sistemas, programação, autenticação e modelagem de banco de dados.

# 16. REFERÊNCIAS TÉCNICAS

As principais referências utilizadas na elaboração desta documentação foram os próprios arquivos e materiais do projeto:

- Repositório do projeto: https://github.com/salozin007/TCC
- Arquivo `server.js` – implementação do Back-end.
- Arquivo `db.js` – conexão, criação e inicialização do banco de dados.
- Script SQL – estrutura inicial do banco `monsenhor_bicudo`.
- Imagens das interfaces do sistema.
- Arquivo `package.json` – dependências e comandos de execução.

**Observação:** esta é uma primeira versão da documentação, elaborada com os materiais disponíveis até o momento. Os detalhes do Front-end, das rotas Angular, dos serviços, da proteção administrativa e dos testes ainda precisam ser conferidos para que a versão final represente integralmente o funcionamento do sistema.