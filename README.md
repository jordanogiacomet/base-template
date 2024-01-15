# Estrutura do Backend

Este repositório contém o código do backend de uma aplicação Node.js que utiliza o framework Express.js e o ORM Sequelize para a interação com o banco de dados MySQL.

## Estrutura de Arquivos

- `src`: Pasta fonte onde o código principal da aplicação está localizado.
  - `config`: Contém arquivos de configuração para diferentes ambientes (desenvolvimento, teste, produção).
  - `controllers`: Mantém as classes controladoras responsáveis por lidar com as solicitações HTTP, executando operações CRUD através dos serviços.
  - `migrations`: Diretório para os arquivos de migração do Sequelize, que gerenciam as alterações no esquema do banco de dados.
  - `models`: Contém os modelos do Sequelize que representam as tabelas do banco de dados na aplicação.
  - `routes`: Define as rotas HTTP que mapeiam para os métodos dos controladores.
  - `seeders`: Diretório para os arquivos de seed do Sequelize que populam o banco de dados com dados iniciais.
  - `services`: Camada de serviço que contém a lógica de negócios e interage com os modelos para consultar o banco de dados.

- `.eslintrc.json`: Configurações do ESLint para a padronização de código.
- `.sequelizerc`: Configurações do Sequelize CLI.
- `package.json` e `package-lock.json`: Contêm as dependências do projeto e outras informações.
- `server.js`: Arquivo de entrada da aplicação que configura o servidor Express.

## Configuração do Banco de Dados

O arquivo `config.json` localizado em `src/config` define as configurações do banco de dados para diferentes ambientes. Ele configura o usuário, senha, banco de dados, host e dialeto para o Sequelize.

## Controladores

Os controladores são responsáveis por manipular as solicitações e respostas HTTP. Eles utilizam os serviços para executar operações no banco de dados e enviar a resposta apropriada ao cliente.

Exemplo de um método do controlador:

```javascript
async pegaTodos(req, res) {
  try {
    const registros = await this.entidadeService.pegaTodosOsRegistros();
    return res.status(200).json(registros);
  } catch (erro) {
    // Tratamento do erro
  }
}
```

## Serviços

Os serviços interagem com os modelos do Sequelize para realizar operações no banco de dados. Eles são chamados pelos controladores e contêm a lógica de negócios da aplicação.

```javascript
class Services {
  // ...
  async pegaTodosOsRegistros() {
    return dataSource[this.model].findAll();
  }
  // ...
}

## Rotas

As rotas são definidas para especificar como a aplicação deve responder a uma requisição a um determinado endpoint, que é uma URI (ou caminho) e um método HTTP específico (GET, POST, etc.).

```javascript
const express = require('express');
const MeuController = require('../controllers/meuController');
const router = express.Router();

router.get('/entidade', MeuController.pegaTodos);
router.get('/entidade/:id', MeuController.pegaUmPorId);
router.post('/entidade', MeuController.criaNovo);
router.put('/entidade/:id', MeuController.atualiza);
router.delete('/entidade/:id', MeuController.exclui);

module.exports = router;

```

## Executando o Projeto

Para colocar o servidor em funcionamento localmente, siga os passos abaixo:

1. **Instalação de Dependências**:
   Utilize o comando abaixo para instalar todas as dependências necessárias listadas no arquivo `package.json`.

   ```
    npm install
   ```
   ```
