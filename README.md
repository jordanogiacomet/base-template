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

```
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

```
class Services {
  // ...
  async pegaTodosOsRegistros() {
    return dataSource[this.model].findAll();
  }
  // ...
}

## Rotas

As rotas são definidas para especificar como a aplicação deve responder a uma requisição a um determinado endpoint, que é uma URI (ou caminho) e um método HTTP específico (GET, POST, etc.).

```
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
2. **Configuração do Banco de Dados**:
Configure seu banco de dados MySQL de acordo com as configurações encontradas em `src/config/config.json`. Certifique-se de que as credenciais e o nome do banco de dados estejam corretos para os ambientes de desenvolvimento, teste e produção.

3. **Migrações do Banco de Dados**:
Execute as migrações para criar as tabelas no banco de dados usando o Sequelize CLI com o comando:
```
npx sequelize-cli db:migrate
```
4. **Populando o Banco de Dados** (opcional):
Se necessário, você pode popular o banco de dados com dados iniciais utilizando o comando:
```
npx sequelize-cli db:seed:all
```
5. **Executando o Servidor**:
Inicie o servidor em modo de desenvolvimento com o seguinte comando:
```
npm run dev
```
Isso iniciará o servidor usando `nodemon`, que irá automaticamente reiniciar o servidor sempre que houver alterações no código.

6. **Testando a API**:
Após o servidor estar em execução, você pode testar as rotas da API utilizando um cliente de API como Postman ou simplesmente acessando-as através do navegador, dependendo do tipo de requisição (GET, POST, etc.).

Tenha certeza de verificar os logs no console para qualquer erro e mensagens de sucesso indicando que o servidor está rodando corretamente.
