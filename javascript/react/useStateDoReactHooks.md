# Utilizando o useState da api React Hooks

Basicamente os hooks nos permitem utilizar o state e outros recursos do react sem escrever uma classe.

## Problemas a serem resolvidos pelos hooks
- No react é difícil reutilizar lógica com estado entre componenetes
- Componentes começam simples mas crescem para uma bagunça incontrolável de lógica com estado.
- Muitas vezes, classes podem ser uma barreira para aprendizado do react.

## Como os hooks resolvem esses problemas:
- Utilizando recat hooks, podemos extrair lógica com estado de um componenete de uma forma que possa ser reutilizada. Com isso podemos reutilizar lógica com estado sem mudar a hierarquia de componentes.
- Com hooks podemos quebrar o código de um componente em funções menores, baseadas em pedaços que são relacionados.
- Com hooks podemos utilizar mais das funcionalidades do react sem classes, o que parece ser mais lógico visto que os componentes do react tem mais a ver com funções do que com classes.

## Utilizando State Hook
O 'useSTate' é um Hook que te permite adicionar o state do React a um componente de função. Com isso ao escrevermos um componente de função, se precisarmos adicionar algum state para ele não precisaremos convertê-lo em uma classe.

- Declarando uma variável de state:
```javascript
import React, { useState } from 'react';

function Login(){
    const [login, setLogin] =useState('');
}
```
Perceba que o useState() tem as mesmas capacidades que o this.state de uma classe.
Como parâmetro, passamos o state inicial; diferentemente de quando usamos classes, o state não tem que ser um objeto, podemos ter uma string, numero e etc.
O useState retorna um par de valores, o state atual e uma função que atualiza o state.
A cada renderização o react vai lembrar o valor atual e fornecer o valor mais recente para a função. Se quiser atualizar o login, usamos setLogin

- Atualizando o state
```javascript
<input             
required="required" 
type="text" 
value ={login}
onChange={event => setLogin(event.target.value)}
/>
```

Cada vez que o usuário digitar seu login no input de texto, a variável login será atualizada.
