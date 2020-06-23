# Diferenças entre let, var e const
A principal diferença está no escopo. Vejamos alguns exemplos bem interessantes

## Var
Ao declararmos uma váriável com var, conseguimos acessar um mecanismo muito interessante do javascript chamado hoisting. Basicamente hoisting quer dizer que o escopo da variável vai ser elevado até o topo do seu contexto de execução. Vamos ver alguns exemplos:
```javascript
function somaComUm(n) {
    if(n>0)
        var soma = n+1;
    console.log(soma);
}
```
Perceba que no exemplo acima, estamos declarando uma variável dentro de um bloco if. Para quem vem de linguagens como c, C# e Java pode achar isso estranho, mas ao declarar uma variável com var, temos acesso a essa variável em todo o contexto. Vejamos outro exemplo interessante:
```javascript
function somaComUm(n){
    soma = n+1;
    console.log(soma);
    var soma;
}
```
Apesar da variável soma ser declarada somente depois da utilização, esse código funciona sem erros pois o escopo é elevado.

## Let
O var é muito legal mas nem sempre queremos toda essa flexibilidade. Foi pensando nisso que o ES6 trouxe o let, que traz o escopo de bloco assim como na maioria das linguagens.

## Const
Como o nome já sugere, const é usada para declarar constantes. Assim como o let, as variáveis declaradas com const tem o escopo de bloco.