
# Scavenger Hunt

Categoria: OSINT

Plataforma: CyLab  

Dificuldade: Fácil

## Introdução

Este write-up apresenta a resolução do desafio *Scavenger Hunt*, disponibilizado na plataforma CyLab como exercício prático de cibersegurança.

O desafio consiste em investigar diferentes arquivos de uma aplicação web para encontrar partes de uma flag que estão escondidas em diferentes locais do site.

Seu principal objetivo é desenvolver habilidades de reconhecimento e investigação de aplicações web, utilizando ferramentas do navegador e conhecimentos sobre arquivos utilizados por servidores e sistemas operacionais.

## Enunciado

O desafio apresenta a seguinte descrição:

"There is some interesting information hidden around this site. Can you find it?"

Além do enunciado, é fornecido um endereço para uma aplicação web.

## Interpretação do desafio

O nome *Scavenger Hunt* pode ser traduzido como "caça ao tesouro", uma atividade na qual precisamos procurar diferentes pistas para chegar a um objetivo final.

Dessa forma, o nome do desafio sugere que a flag não estaria disponível diretamente na página inicial, mas escondida em diferentes partes da aplicação.

A estratégia inicial foi investigar o código-fonte da página, procurando comentários, arquivos externos e possíveis informações que não estivessem visíveis na interface do site.

## Resolução

### Etapa 1: Analisando a página inicial

Após iniciar o desafio, acessei o endereço fornecido pelo CyLab.

A página apresentava um site simples, com algumas informações sobre seu funcionamento.

<img width="1912" height="996" alt="image" src="https://github.com/user-attachments/assets/120f4f43-56c8-464e-83fd-cd5b73d21371" />


Ao observar a aplicação, percebi que ela mencionava tecnologias utilizadas no desenvolvimento web, como HTML, CSS e JavaScript.

Isso chamou minha atenção, pois esses arquivos poderiam conter informações que não aparecem diretamente na página.

Para investigar, abri o código-fonte 

### Etapa 2: Encontrando a primeira parte da flag

Ao analisar o código HTML, encontrei um comentário contendo a primeira parte da flag.

```html
<!-- Here's the first part of the flag: academy{t -->
```

<img width="702" height="582" alt="image" src="https://github.com/user-attachments/assets/9a27ab2d-b81f-460c-b9a5-e32e69b7ed76" />


Comentários HTML são utilizados para adicionar observações ao código, mas não aparecem normalmente na página renderizada.

Entretanto, eles continuam acessíveis para qualquer usuário que visualize o código-fonte.

Assim, encontramos a primeira parte

Como a flag estava incompleta, seria necessário continuar investigando os outros arquivos do site.

### Etapa 3: Investigando o CSS

Após encontrar a primeira parte da flag no HTML, decidi analisar o arquivo CSS utilizado pela aplicação.

O CSS é responsável pela aparência visual de uma página, definindo características como cores, tamanhos, fontes e posicionamento dos elementos.

No código HTML, podemos identificar arquivos CSS por meio de elementos semelhantes a:

```html
<link rel="stylesheet" href="mycss.css">
```

Ao acessar o arquivo `mycss.css`, encontrei outro comentário:

```css
/* CSS makes the page look nice, and yes, it also has part of the flag. Here's part 2: h4ts_4_l0 */
```

<img width="915" height="932" alt="image" src="https://github.com/user-attachments/assets/55e2daa7-9bab-4e79-9ae0-e902fbba80b4" />


Esse comentário revelou a segunda parte da flag:

```text
h4ts_4_l0
```

Juntando as duas partes encontradas, temos:

```text
picoCTF{th4ts_4_l0
```

Entretanto, a flag ainda estava incompleta.

### Etapa 4: Investigando o JavaScript

Seguindo a mesma lógica, decidi analisar o arquivo JavaScript da aplicação.

O JavaScript é uma linguagem de programação amplamente utilizada no desenvolvimento web, responsável por adicionar interatividade e funcionalidades às páginas.

No código HTML, podemos identificar arquivos JavaScript por meio de elementos semelhantes a:

```html
<script src="myjs.js"></script>
```

Ao acessar o arquivo `myjs.js`, encontrei o seguinte comentário:

```javascript
/* How can I keep Google from indexing my website? */
```

<img width="907" height="842" alt="image" src="https://github.com/user-attachments/assets/1b91fb14-81ff-4e4b-a570-556929c7f3a1" />


Diferentemente dos arquivos anteriores, o JavaScript não apresentava diretamente uma parte da flag.

Entretanto, o comentário fornecia uma pista importante, perguntando como impedir que o Google indexasse um site.

Pesquisando sobre esse funcionamento, podemos encontrar um arquivo chamado `robots.txt`.

Esse arquivo é utilizado para fornecer orientações aos mecanismos de busca sobre quais caminhos de um site podem ou não ser rastreados.

Assim, a próxima etapa foi investigar esse arquivo.

### Etapa 5: Investigando o robots.txt

Para acessar o arquivo `robots.txt`, adicionei seu nome ao final do endereço do site:

```text
http://ENDERECO_DO_DESAFIO/robots.txt
```

<img width="1917" height="978" alt="image" src="https://github.com/user-attachments/assets/1d63364d-0775-4dda-8b1e-f0926bc4134e" />


O arquivo apresentava informações semelhantes a:

```text
User-agent: *
Disallow: /index.html

# Part 3: t_0f_pl4c
# I think this is an apache server... can you Access the next flag?
```

O conteúdo pode ser dividido em algumas partes:

- `User-agent: *`: indica que a orientação se aplica a todos os robôs de busca.
- `Disallow: /index.html`: solicita que os robôs não rastreiem o caminho informado.
- `#`: indica um comentário dentro do arquivo.

É importante destacar que o `robots.txt` não é um mecanismo de segurança, pois seu conteúdo pode ser acessado publicamente e suas orientações não impedem o acesso direto aos arquivos.

Nesse arquivo, encontramos a terceira parte da flag:

```text
t_0f_pl4c
```

Além disso, o comentário mencionava que a aplicação utilizava um servidor Apache.

Essa informação fornecia uma pista para a próxima etapa.

### Etapa 6: Investigando o .htaccess

Após identificar a referência ao Apache, procurei compreender quais arquivos estão associados a esse servidor.

O Apache é um servidor HTTP bastante utilizado para hospedar aplicações web.

Um de seus arquivos de configuração é o `.htaccess`, que pode ser utilizado para definir regras de acesso, redirecionamentos e outras configurações de diretórios.

Como o comentário anterior mencionava o Apache, decidi verificar se esse arquivo estava acessível.

Para isso, utilizei o seguinte endereço:

```text
http://ENDERECO_DO_DESAFIO/.htaccess
```
<img width="1917" height="963" alt="image" src="https://github.com/user-attachments/assets/57e83d82-4581-4a80-bb4e-33b04c33613f" />

O arquivo apresentava o seguinte comentário:

```text
# Part 4: 3s_2_lO0k
# I love making websites on my Mac, I can Store a lot of information there.
```

Assim, encontramos a quarta parte da flag:

```text
3s_2_lO0k
```

Entretanto, ainda faltava encontrar a última parte.

O comentário também mencionava um computador Mac e destacava a palavra "Store", fornecendo outra pista.

### Etapa 7: Investigando o .DS_Store

A partir da referência ao sistema macOS, investiguei arquivos que poderiam ser criados automaticamente por esse sistema operacional.

Um desses arquivos é o `.DS_Store`, utilizado pelo macOS para armazenar informações sobre a visualização de pastas, como a organização de ícones e outras preferências.

Embora normalmente não seja necessário para o funcionamento de um site, esse arquivo pode acabar sendo enviado acidentalmente para um servidor durante o desenvolvimento de uma aplicação.

Seguindo essa pista, tentei acessar:

```text
http://ENDERECO_DO_DESAFIO/.DS_Store
```
<img width="1903" height="961" alt="image" src="https://github.com/user-attachments/assets/524d3632-b7a7-41dd-85b7-86db1dff81e4" />


O conteúdo encontrado revelou a última parte da flag.

```text
Congrats! You completed the scavenger hunt.
Part 5: _2b9c61f}
```

### Etapa 8 — Montando a flag

Após investigar os diferentes arquivos do site, foi possível reunir todas as partes encontradas.

| Arquivo | Parte encontrada |
|---------|------------------|
| HTML | `academy{t` |
| CSS | `h4ts_4_l0` |
| robots.txt | `t_0f_pl4c` |
| .htaccess | `3s_2_lO0k` |
| .DS_Store | `_2b9c61f}` |

Juntando os fragmentos na ordem correta, chegamos à estrutura:

```text
academy{th4ts_4_l0t_0f_pl4c3s_2_lO0k_2b9c61f}
```

Com isso, o desafio foi concluído.

## 5: Conclusão

O desafio *Scavenger Hunt* demonstrou a importância da investigação de diferentes arquivos durante a análise de uma aplicação web.

Inicialmente, a página parecia apresentar apenas informações simples sobre HTML, CSS e JavaScript. Entretanto, ao investigar seus arquivos, foi possível encontrar pistas que levaram a diferentes recursos do servidor.

Durante a resolução, foram utilizados os seguintes conhecimentos e ferramentas:

- **HTML:** para investigar o código-fonte e identificar comentários ocultos.
- **CSS:** para analisar arquivos responsáveis pela aparência da página.
- **JavaScript:** para encontrar pistas relacionadas ao funcionamento da aplicação.
- **DevTools:** para inspecionar os recursos utilizados pelo site.
- **Robots.txt:** para compreender como aplicações fornecem orientações aos mecanismos de busca.
- **.htaccess:** para conhecer arquivos de configuração utilizados pelo servidor Apache.
- **.DS_Store:** para identificar arquivos de metadados criados pelo macOS.
- **Reconhecimento web:** para investigar recursos públicos e localizar informações expostas.

O principal aprendizado foi compreender que informações sensíveis podem ser expostas em arquivos aparentemente comuns de uma aplicação web.

Além disso, o desafio mostrou que arquivos de configuração, comentários no código-fonte e metadados do sistema operacional podem revelar informações importantes quando disponibilizados publicamente.

Por fim, o desafio reforçou a importância de verificar quais arquivos estão acessíveis em um servidor e evitar a exposição de informações que não deveriam estar disponíveis aos usuários.

