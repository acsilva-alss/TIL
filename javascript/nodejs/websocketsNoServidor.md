# Como fazer um servidor em node ficar esperando conexões de clientes via socket?
Muitas vezes, nós temos a necessidade de criar uma aplicação em que uma mensagem tem que ser enviada de um usuário para outro e em tempo real (como em um jogo multiplayer). No ambiente web, nós temos os websockets que é uma abstração que permite a comunicação entre diferentes processos rodandos em máquinas diferentes.
Mas como fazer um servidor em node capaz de escutar essas mensagens e replicar para outros clientes?
Para isso nós temos a biblioteca socket.io.
# Instalando socketio
```javascript
yarn add socketio
```
# Criando um servidor capaz de receber conexões
```javascript
const express = require('express');
const app = express();

const server = require('http').createServer(app); // Cria um canal http para a comunicação
const io = require('socket.io')(server); // aplicando ao socketio esse canal

io.on('connection', socket =>{ // io.on é responsável por ficar esperando conexão de clientes
    console.log(socket.id);
})


server.listen(3000);
```