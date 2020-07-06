# Pulando os efeitos aplicados pelo hook useEffect
No react utilizamos o hook useEffect para executar efeitos colaterais em componenetes, esses efeitos podem ser tanto a busca de dados como uma mudança na DOM.
O useEffect por padrão, executa esse efeito depois da primeira renderização e depois de toda atualização.
Porém a aplicação desse efeito em cada renderização, pode causar um problema de performance.
Para isso podemos dizer ao react para pular a aplicação de um efeito se certos valores não tiverem mudado entre as renderizações.
Exemplo:
```javascript
useEffect(() => {
  document.title = `Você clicou ${count} vezes`;
}, [count]);
```
O efeito acima só será executado, quando mudarmos o count, utilizando algo como setCount();

### Fonte:
https://pt-br.reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects