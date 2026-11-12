
# First Find

Categoria: General Skills / Forense Digital  

Plataforma: CyLab

Dificuldade: Fácil

## Introdução

Este write-up apresenta a resolução do desafio *First Find*, disponibilizado na plataforma CyLab como exercício prático de cibersegurança.

O desafio consiste em localizar um arquivo específico dentro de uma estrutura de diretórios, utilizando comandos do terminal Linux.

Seu principal objetivo é desenvolver a familiaridade com a navegação e pesquisa de arquivos, especialmente quando existem diversas pastas e subpastas.

## Enunciado

O desafio apresenta a seguinte descrição:

"Unzip this archive and find the file named 'uber-secret.txt'."

Além do enunciado, é disponibilizado um arquivo compactado chamado `files.zip`.

## Interpretação do desafio

O enunciado nos informa que precisamos descompactar um arquivo ZIP e localizar um documento chamado `uber-secret.txt`.

Entretanto, não sabemos exatamente em qual diretório esse arquivo está armazenado.

Como o conteúdo compactado pode apresentar diversas pastas e subpastas, procurar manualmente por cada arquivo seria um processo demorado.

Dessa forma, a estratégia foi utilizar ferramentas do terminal para extrair o conteúdo e localizar o arquivo desejado de maneira eficiente.

## Resolução

### Etapa 1: Extração do arquivo ZIP

Após realizar o download de `files.zip`, iniciei o desafio utilizando o seguinte comando:

```bash
unzip files.zip
```

O comando `unzip` permite descompactar arquivos no formato ZIP, extraindo seu conteúdo para o diretório atual.

<img width="452" height="126" alt="image" src="https://github.com/user-attachments/assets/8cfa6fb0-5a7e-47be-81e3-883ac8fe87be" />

Após a execução, foi criado um diretório chamado `files`, contendo diversas pastas e arquivos de texto.

### Etapa 2: Investigando os diretórios

Ao observar a estrutura extraída, percebi que havia diversos diretórios, alguns contendo outras subpastas.

Nesse caso, navegar manualmente por todos eles utilizando `cd` e `ls` seria possível, porém pouco eficiente.

Como o enunciado já informava o nome do arquivo que precisávamos encontrar, poderíamos utilizar uma ferramenta específica para pesquisar arquivos no Linux.

Essa ferramenta é o comando `find`.

### Etapa 3: Localizando o arquivo escondido

Para encontrar o arquivo `uber-secret.txt`, executei:

```bash
find -name uber-secret.txt
```

O comando `find` permite pesquisar arquivos e diretórios dentro de uma estrutura de pastas.

```text
files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
```

<img width="635" height="40" alt="image" src="https://github.com/user-attachments/assets/003c82d5-2c99-49b9-b4bc-8f7af89de473" />


Com isso, encontramos o caminho completo do arquivo.

Um detalhe importante é a presença de uma pasta chamada `.secret`.

No Linux, arquivos e diretórios cujo nome começa com um ponto são considerados ocultos, não aparecendo normalmente na listagem do comando `ls`.

Para visualizar arquivos ocultos, podemos utilizar:

```bash
ls -a
```

O parâmetro `-a` permite mostrar todos os arquivos, incluindo os ocultos.

Entretanto, o comando `find` já consegue pesquisar nesses diretórios, não sendo necessário acessá-los manualmente.

### Etapa 4: Obtendo a flag

Após localizar o arquivo, bastava visualizar seu conteúdo.

Para isso, utilizei:

```bash
cat files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
```

O comando `cat` permite visualizar o conteúdo de arquivos de texto diretamente no terminal.

<img width="630" height="73" alt="image" src="https://github.com/user-attachments/assets/625a5d7e-3c4a-49d1-b3c3-91269843f258" />


O arquivo continha a flag:

```text
academy{f1nd_15_f457_ab443fd1}
```

Assim, foi possível concluir o desafio sem precisar navegar manualmente por todos os diretórios.

## 5: Conclusão

O desafio *First Find* demonstrou a importância de conhecer ferramentas de pesquisa e navegação de arquivos no Linux.

Embora a tarefa inicialmente parecesse exigir a exploração manual de diversos diretórios, foi possível encontrar o arquivo desejado rapidamente utilizando o comando `find`.

Durante a resolução, foram utilizadas as seguintes ferramentas:

- **Unzip:** para extrair o conteúdo do arquivo compactado.
- **Ls:** para visualizar os arquivos e diretórios existentes.
- **Find:** para localizar um arquivo específico dentro de uma estrutura de diretórios.
- **Cat:** para visualizar o conteúdo do arquivo encontrado.

Além disso, o desafio permitiu compreender melhor o funcionamento dos arquivos e diretórios ocultos no Linux.

O principal aprendizado foi que, ao trabalhar com grandes estruturas de arquivos, utilizar ferramentas de pesquisa automatizada pode ser muito mais eficiente do que navegar manualmente por cada diretório.

Por fim, o desafio reforçou a importância do domínio dos comandos básicos do terminal, que são frequentemente utilizados em atividades de análise forense e cibersegurança.

