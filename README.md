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