# Entendendo garbage collector no c#
O garbage collector do .Net framwork, gerencia a alocação e liberação de memória da sua aplicação.
Quando iniciamos um processo, o runtime reserva uma área contígua de memória para esse processo. Cada vez que criamos um objeto, o CLR aloca esse objeto no heap. Porém a memória não é infinita, e eventualmente uma limpeza tem que ser executada.

## Benefícios do GC
- Todo desenvolvedor que já trabalhou com a linguagem C, sabe o quão chato é ter que gerenciar a memória. Sendo assim, terceirizar essa responsabilidade traz mais facilidade ao desenvolvimento.
- A alocação dos objetos no heap é bastante eficiente.
- Garante que um objeto não possa acessar o conteúdo de outro (evitando o famoso segmantation fault do c).

## Liberação de memoria pelo GC

O mecanismo de otimização do GC determina o melhor momento para executar uma limpeza, levando em consideração as alocações que estão sendo feitas.
Quando uma limpeza é executada, o GC libera a memória de objetos que não estão mais sendo usados pelo aplicativo. Existem 3 condições para que uma coleta de lixo seja feita:
- Quando o sistema operacional começa avisar que o sistema está com pouca memória.
- O heap alocado para o processo está cheio
- O método GC.Collect() é chamado.

## Objetos não gerenciados

Mas nem tudo são flores, existem alguns tipos de objetos que o GC não consegue fazer uma limpeza, como:
- Identificadores de arquivos
- Identificadores de janelas
Para esses objetos não gerenciáveis, nós como desenvolvedores teremos a responsabilidade de, quando o objeto terminar, liberar explicitamente sua memória através do dispose().