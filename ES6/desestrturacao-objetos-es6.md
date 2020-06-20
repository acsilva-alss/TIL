# Desestruração de objetos
Em muitos casos, temos a necessidade de acessar várias propriedades de um objeto, fazendo com que tenhamos repetição de código como no exemplo abaixo:
```javascript
const Aluno = {
    nome: Alisson,
    sobrenome: Silva,
    nota: 10
}

const nome = Aluno.nome;
const sobrenome = Aluno.sobrenome
const nota = Aluno.nota
```
Note que utilizamos três linhas de código para acessar as informações do objeto aluno. Será que existe uma forma menos verbosa de fazer isso? 
Com o ES6 ganhamos uma forma muito simples de acessar propriedades de objetos, a chamada desestruturação, como vemos no exemplo abaixo:
```javascript
const Aluno = {
    nome: Alisson,
    sobrenome: Silva,
    nota: 10
}

const {nome, sobrenome, nota} = Aluno;
```