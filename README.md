# Questões

## Deadlock

Deadlock é quando várias threads estão bloqueadas e não conseguem continuar suas respectivas execuções por uma estar esperando liberação de recursos da outra.

Explicando com um pouco pouco melhor este problema, com um mesmo recurso compartilhado entre a Thread A e Thread B:

- Thread A acessa e bloqueia o recurso 1, e espera pelo recurso 2 para prosseguir
- Thread B acessa e bloqueia o recurso 2, e espera pelo recurso 1 para prosseguir

Como podemos ver, as duas threads não conseguem continuar a executar, pois uma está bloqueando a outra.

Sobre as possíveis soluções:

- A mais básica, é não utilizar várias threads, executando uma thread por vez. Porém, na maioria dos casos a utilização de várias threads é obrigatória, tornando esta solução inviável;
- Timeout ao tentar adquirir o lock;
- Desenvolver uma forma de ordenação de locks desses recursos
- Desenvolver a aplicação para que este tipo de dependência não ocorra.

## Stream / ParallelStream

A diferença do Stream para o ParallelStream é a forma de execução de cada um. Na API Stream, as operações são executadas de forma sequencial - usando o loop como exemplo, cada registro é acessado de forma sequencial, um por vez. Já na ParallelStream a execução é realizada de forma paralelizada, aproveitando melhor o número de CPU's disponível no ambiente em que o código estiver sendo executado, com uma API de uso simples, sem muito esforço para o desenvolvedor.

Em relação a quando devemos utilizar cada um deles, os casos de uso recomendados do ParallelStream dependem de alguns fatores: 
- Número de CPU's do ambiente;
- Quantidade muito grande de itens que serão processados e o tipo de operação que está sendo executada (percorrer uma stream muito grande pode ter a vantagem do uso de mais cores, por exemplo);
- Uma operação que não depende da ordem da execução pode ser mais rápida;
- Tipo de aplicação utilizada. Por exemplo: uma aplicação com várias operações paralelas pode ter a performance prejudicada ao adicionar mais threads;

Se o caso de uso não tiver alguma das características acima, é recomendado utilizar a API Stream sequencial.

Mesmo com tudo isso, a melhor maneira de se ter certeza qual das duas versões da API é indicada seria com a realização de testes para uma comparação precisa.