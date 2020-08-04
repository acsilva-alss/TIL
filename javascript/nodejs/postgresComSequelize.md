# Postgres no Node.js com sequelize

Apesar da maioria dos exemplos e explicações do Node.js utilizarem bancos de dados NoSql, nem sempre essa é a melhor opção. Isso porque bancos de dados NoSql não lidam bem com relacionamentos, pois não foi pra isso que eles foram criados. 
Sendo assim resolvi aprender um pouco mais sobre como utilizar um banco de dados relacional no Node.js e achei o sequelize.

## O que é o sequelize?
Sequelize é um ORM para Node.js que tem suporte a diversos bancos de dados. Ele é responsável por fazer o mapeamento de dados relacionais (tabelas) para objetos javascript.

## Configurando o sequelize
Primeiro precisamos instalar o sequelize no projeto com o seguinte comando:
```javascript
npm install sequelize
npm install -D sequelize-cli

//ou

yarn add sequelize
yarn add -D sequelize-cli
```

Após instalá-lo, precisamos adicionar alguns arquivos ao nosso projeto.

- Crie um arquivo na raiz do projeto chamado .sequelizerc. Esse arquivo vai indicar ao sequelize o caminho dos arquivos de configuração :
```javascript
const path = require('path');
module.exports = {
    config: path.resolve(__dirname, 'src', 'config', 'database.js'),
    'migrations-path': path.resolve(__dirname, 'src', 'database', 'migrations'),
}
```

- Crie uma pasta chamada config(dentro de src), e um arquivo database.js dentro dela com as seguintes configurações

```javascript
module.exports = {
    dialect: 'postgres',
    host: DATABASE_HOST,
    username: DATABASE_USERNAME,
    password: DATABASE_PASSWORD,
    database: DATABASE_NAME,
    define: {
        timestamps: true,
        underscored: true, // diz se as tabelas terão underscore como separador
    },
};
```
- Crie uma pasta chamada database(dentro de src) com um arquivo index.js e uma pasta migrations. Essa pasta migrations irá conter os scripts de cração das tabelas. Coloque o seguinte código dentro de index.js:
```javascript
const Sequelize = require('sequelize');
const dbConfig = require('../config/database');
const connection = new Sequelize(dbConfig);

module.exports = connection;
```

Depois de ter tudo criado, podemos criar nosso banco de dados com o seguinte comando:
```javascript
yarn sequelize db:create 
```

Com o banco de dados criado, podemos começar a criar as migrations com o seguinte comando:
```javascript
yarn sequelize migration:create --name=create-NOMEDOQUEAMIGRATIONFAZ
```
Se tudo ocorreu bem, na pasta migrations deve ter um arquivo, criado pelo sequelize, com o nome que você informou e a data da execução.

## Modificando migration para adicionar colunas na tabela

Ao abrir o arquivo criado pelo sequelize na pasta migrations, você vai perceber que existem dois métodos, chamados up e down. O up quer dizer o que a migration vai realizar na base de dados, por exemplo, a criação de uma nova tabela. Já o método down, diz o que o sequelize deve fazer quando precisar desfazer a migration. Um exemplo de criação da tabela de usuários seria o seguinte:
```javascript

module.exports = {
  up: async (queryInterface, Sequelize) => {
    return queryInterface.createTable('users', { 
      id: {
        type: Sequelize.INTEGER,
        primaryKey: true,
        autoIncrement: true,
        allowNull: false,
      },
      email: {
        type: Sequelize.STRING,
        allowNull: false,
      },
      password: {
        type: Sequelize.STRING,
        allowNull: false,
      },
      created_at: {
        type: Sequelize.DATE,
        allowNull: false,
      },
      updated_at: {
        type: Sequelize.DATE,
        allowNull: false,
      },
    });
     
  },

  down: async (queryInterface, Sequelize) => {
    return queryInterface.dropTable('users');
     
  }
};

```
Após modificar as migrations criadas, execute o seguinte comando para as tabelas serem criadas no banco de dados:
```javascript
yarn sequelize db:migrate
```

## Criando model da tabela
Após criar a tabela no banco, crie uma pasta em ./src/app/ chamada models, e crie o model da tabela. Utilizando o exemplo de usuários ficaria da seguinte forma:
```javascript
const {Model, DataTypes} = require('sequelize');

class User extends Model {
    static init(connection){
        super.init({
            email: DataTypes.STRING,
            password: DataTypes.STRING,
        },{
            sequelize: connection
        })
    }
}

module.exports = User;
```

Agora em src/database/index.js, instancie a classe recém criada passando o objeto de conexão da seguinte forma:
```javascript
const Sequelize = require('sequelize');
const dbConfig = require('../config/database');
const User = require('../app/models/User');

const connection = new Sequelize(dbConfig);

User.init(connection);

module.exports = connection;
```

Pronto, agora já podemos começar a realizar inserções e consultas na nossa base de dados

