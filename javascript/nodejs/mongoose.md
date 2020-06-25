# Mongoose 
O MongoDb é um dos bancos de dados mais utilizados no mercado, pela sua praticidade e por usar documentos semelhantes a Json como esquema. 
Uma das principais bibliotecas utilizadas para construir uma abstração do Mongodb em node é o mongoose. Basicamente o mongoose é uma biblioteca que proporciona uma solução baseada em esquemas para modelar os dados e  traduz esses dados do banco de dados para objetos JavaScript, para que possam ser utilizados por sua aplicação.

## Instalando o mongoose
---
Considerando que você já tenha o MongoDb rodando na sua máquina, juntamente com o node, yarn, dotenv e express, basta executar o seguinte comando:

```
yarn add mongoose
```

## Conectando com o MongoDB
---
Crie um arquivo chamado database.js da seguinte forma:

```javascript
const mongoose = require('mongoose');
require('dotenv/config.js'); // necessário para buscar a string de conexão. Será necessário criar um arquivo .env que contenha a string de conexão


// Criando conexão com o mongo
mongoose.connect(process.env.MONGO_URL, { useNewUrlParser: true, useUnifiedTopology: true, useCreateIndex: true })
.then(response=>console.log('Conected to Database..'))
.catch(error=> console.log('error ->', error.message));

mongoose.Promise = global.Promise;
module.exports = mongoose;
```

## Criando um schema
```javascript
const Database = require('./database.js'); // importando arquivo de conexão
//Estrutura de usuário
const UserSchema = new Database.Schema({
    email: {
        type: String,
        required: true,
    },
    login: {
        type: String,
        require: true,
        unique: true,
    },
    password: {
        type: String,
        required: true,
        select: false,
    },
    createAt: {
        type: Date,
        default: Date.now,
    },
});


const User = Database.model('User', UserSchema);

module.exports = User;
```
## Fazendo uma consulta ao banco
```javascript
const User= require('./user.js'); // importando o schema criado

module.exports = {
     async register(req, res){ 
        const { login } = req.body;
        try{
            if(await User.findOne({ login }))// Procura pelo usuário no banco.
                return res.status(400).send({ error: 'User already exists' }); 
            
            const user = await User.create(req.body);// cria o usuário no banco

            return res.send({ user });
        } catch(err){
            return res.status(400).send({ error: 'Registration failed ' + err });
        }
    }
}
```