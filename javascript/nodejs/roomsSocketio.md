# Rooms no socket.io
Muitas vezes queremos separar os clientes em "salas" diferentes, para podermos enviar um tipo de mensagem para um grupo específico, e não todos.
Para isso, a biblioteca socket.io disponiliza uma feature para segmentação de usuários chamada rooms.

# Atribuindo clientes a uma Room
Primeiramente, vamos verificar como um cliente pode ser atribuído a uma determinada room:
```javascript
// Servidor
socket.on('addRoom', function(roomName){
    socket.join(roomName);
})
``` 

# Retirando cliente de uma room
```javascript
socket.on('leaveRoom', function(roomName){
    socket.leave(roomName);
})
```

# Enviando mensagens para todos os clientes conectados em uma determianda Room
```javascript
socket.broadcast.to("roomName").emit("mensagem");
```
