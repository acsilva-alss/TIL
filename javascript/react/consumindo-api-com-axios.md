# Consumindo dados de uma api com React utilizando Axios

Uma das arquiteturas mais comuns no desenvolvimento web, é você ter um backend que trata os dados e as regras de negócio e um frontend que é responsável somente pela criação de componentes que serão apresentados na tela. Com isso, temos a necessidade de ter uma forma simples de acessar nosso backend (chamada a API) para buscar esses dados.
Uma forma muito simples de fazermos essas requisições a apis eé utilizando o axios. O Axios é uma biblioteca que basicamente trabalha como um cliente http podendo enviar e receber requisições via http. Vale a pena destacar que o axios pode ser usado em todo ecossistema javascript, ou seja, no frontend, backend e mobile.

## Instalando o Axios
---
No pasta do projeto react execute o comando:
```javascript
yarn add axios
```
Se estiver utilizando o npm execute
```javascript
npm install axios
```

## Configurando conxão
---
```javascript
import axios from 'axios';
const api =  axios.create({
    baseURL: 'https://localhost:3000'
});

export default api;
```

## Exemplo de como acessar uma rota da sua api
---
```javascript
import React, { useState } from 'react';
import api from './api';

export default function Login({ history }){
    const [login, setLogin] =useState('');
    async function handleSubmite(event){
        try{
            event.preventDefault();
            const response = await api.post('/authenticate', { login });
            history.push('/');
        }catch(err){
            alert('Login Error');
        }
    }  
    return(
        <form onSubmit={handleSubmite}>
                <p>
                    <label for="login">LOGIN </label>
                    <input 
                        id="email_login" 
                        name="email_login" 
                        required="required" 
                        type="text" 
                        value ={login}
                        onChange={event => setLogin(event.target.value)}/>
                </p>
                <p>
                    <input id="botao" type="submit" value="LOGAR" /> 
                </p>
        </form>        
    );
}
```
