
# Cookies

Categoria: Web Exploitation

Plataforma: CyLab

Dificuldade: Fácil

## Introdução

Este write-up apresenta a resolução do desafio *Cookies*, disponibilizado na plataforma CyLab como exercício prático de cibersegurança.

O desafio consiste em investigar o funcionamento dos cookies de um site e descobrir como a manipulação de seus valores pode revelar informações que normalmente não estão acessíveis pela interface da aplicação.

Seu principal objetivo é introduzir conceitos de segurança web, especialmente relacionados ao armazenamento de informações no navegador e à manipulação de cookies HTTP.

## Enunciado

O desafio apresenta a seguinte descrição:

"Who doesn't love cookies? Try to figure out the best one."

Além do enunciado, é fornecido um endereço para uma aplicação web, na qual podemos pesquisar diferentes tipos de cookies.

## Interpretação do desafio

O enunciado faz uma referência aos cookies, que podem representar tanto um tipo de alimento quanto um recurso utilizado por aplicações web.

Na computação, cookies são pequenos conjuntos de dados armazenados pelo navegador e enviados ao servidor em determinadas requisições HTTP.

Eles podem ser utilizados para manter sessões, armazenar preferências e identificar informações relacionadas à navegação.

Como o desafio pertence à categoria *Web Exploitation*, a referência aos cookies sugere que devemos investigar como o site utiliza esses dados.

Dessa forma, a estratégia foi acessar a aplicação, observar seu comportamento e utilizar as ferramentas de desenvolvedor do navegador para analisar e modificar os cookies armazenados.

## Resolução

### Etapa 1: Acessando a aplicação

Após iniciar o desafio, acessei o endereço disponibilizado pelo CyLab.

A página apresentava uma barra de pesquisa, na qual era possível inserir nomes de diferentes tipos de cookies.

<img width="1911" height="1001" alt="image" src="https://github.com/user-attachments/assets/06f721be-97db-453a-9c07-bda0b2ed8ded" />

Um detalhe interessante é que o próprio site sugere pesquisar pelo termo `snickerdoodle`.

Ao realizar essa pesquisa, a aplicação apresenta uma mensagem reconhecendo o cookie informado.

<img width="1906" height="987" alt="image" src="https://github.com/user-attachments/assets/0d281de8-33ce-4024-80df-37c5275fbb68" />

Isso indica que a aplicação possui algum mecanismo para identificar os valores pesquisados.

Entretanto, como o objetivo era encontrar o melhor cookie, seria necessário investigar melhor como esse mecanismo funcionava.

### Etapa 2: Inspecionando os cookies

Para analisar o funcionamento da aplicação, abri as ferramentas de desenvolvedor do navegador

Em seguida, acessei a aba:

```text
Aplicativo → Armazenamento → Cookies
```

Essa seção permite visualizar os cookies armazenados pelo navegador para o site.

<img width="696" height="947" alt="image" src="https://github.com/user-attachments/assets/b5ffffbf-760d-48af-bac7-af19d3860608" />

Ao analisar os dados, encontrei um cookie chamado `name`.

```text
Name:  name
Value: 0
```
### Etapa 3: Manipulando o valor do cookie

Comecei a modificar manualmente o campo `Value` do cookie `name`.

Por exemplo:

```text
name: bame
Value: 1
```

Após alterar o valor e atualizar a página, observei que a resposta apresentada pelo site também era modificada.

Isso confirmou que o servidor utilizava o valor do cookie para determinar qual conteúdo deveria apresentar.

Continuei testando diferentes valores numéricos, observando o resultado de cada alteração.

<img width="1912" height="992" alt="image" src="https://github.com/user-attachments/assets/ed42f12f-af1a-4108-b539-1ee9a181ba54" />


Essa etapa demonstrou que os dados armazenados no navegador podiam influenciar diretamente o comportamento da aplicação.

### Etapa 4: Encontrando o valor correto

Após testar diferentes valores, encontrei um comportamento diferente ao alterar o cookie para:

```text
Name:  name
Value: 18
```

Ao atualizar a página, a aplicação deixou de apresentar apenas informações sobre tipos de cookies e exibiu a flag do desafio.

<img width="1911" height="995" alt="image" src="https://github.com/user-attachments/assets/c6eb5f43-38bc-447d-8f8b-52814ff687bc" />

Dessa forma, foi possível concluir que o valor `18` correspondia ao conteúdo necessário para resolver o desafio.

### Etapa 5: Obtendo a flag

Após definir o cookie como `name=18` e atualizar a página, o site revelou a flag.

O resultado:

```text
academy{3v3ry1_l0v3s_c00k135_90a3a7cb}
```
Com isso, o desafio foi concluído.

## 5. Conclusão

O desafio *Cookies* demonstrou a importância de compreender o funcionamento dos cookies HTTP e como eles podem influenciar o comportamento de uma aplicação web.

Inicialmente, o site parecia apresentar apenas uma funcionalidade simples de pesquisa por tipos de biscoitos. Entretanto, ao investigar os dados armazenados pelo navegador, foi possível identificar um cookie que controlava as informações apresentadas na página.

Durante a resolução, foram utilizados os seguintes conhecimentos e ferramentas:

- **Cookies HTTP:** para compreender como informações são armazenadas no navegador e enviadas ao servidor.
- **DevTools:** para inspecionar os dados utilizados pela aplicação.
- **Application/Storage:** para localizar e modificar os cookies do site.
- **Manipulação de parâmetros:** para testar diferentes valores e observar as respostas do servidor.
- **Web Exploitation:** para investigar como uma aplicação processa informações controladas pelo usuário.

O principal aprendizado foi compreender que cookies podem ser modificados diretamente pelo usuário e, por isso, não devem ser considerados uma fonte confiável de informações pelo servidor.

Além disso, o desafio apresentou um exemplo de falha de validação de dados, na qual a aplicação permitia acessar um conteúdo especial simplesmente modificando o valor de um cookie.

Por fim, o desafio reforçou a importância de validar informações no lado do servidor, evitando que dados manipuláveis pelo cliente sejam utilizados para controlar o acesso a conteúdos restritos.

