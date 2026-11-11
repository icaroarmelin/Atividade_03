# Matryoshka Doll

Categoria: Forense Digital

Plataforma: CyLab

Dificuldade: Média

## 1. Introdução

Este write-up apresenta a resolução do desafio *Matryoshka Doll*, da plataforma CyLab, recomendado pelos professores como exercício prático de forense digital.

O desafio consiste em investigar uma imagem e identificar arquivos ocultos em seu interior, utilizando ferramentas de análise e extração de arquivos no Linux.

## 2. Enunciado

O desafio apresenta a seguinte descrição:

> "Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one?"

Além do enunciado, é fornecido um arquivo de imagem chamado `dolls.jpg`.

As Matryoshkas são bonecas tradicionais russas, caracterizadas por conterem outras bonecas menores dentro de si. Esse conceito está associado à maternidade e à continuidade das gerações, já que cada boneca abriga outra semelhante, progressivamente menor.

## 3. Interpretação do desafio

A descrição fornece uma pista importante sobre como o desafio deve ser resolvido.

Assim como uma Matryoshka contém outras bonecas em seu interior, o arquivo fornecido poderia conter outros arquivos ocultos, que precisariam ser extraídos sucessivamente até encontrar o conteúdo final.

A partir dessa interpretação, a estratégia foi utilizar o **Binwalk** para identificar arquivos embutidos na imagem e o **7-Zip** para extrair os conteúdos encontrados.

## 4. Resolução

### Etapa 1: Análise da imagem original

Após realizar o download do arquivo `dolls.jpg`, iniciei a investigação utilizando o seguinte comando:

```bash
binwalk dolls.jpg
```

O Binwalk é uma ferramenta utilizada para identificar assinaturas de arquivos, sendo especialmente útil na análise de arquivos que podem conter outros formatos de dados em seu interior.

<img width="635" height="236" alt="image" src="https://github.com/user-attachments/assets/3b711175-ff88-447d-a81c-8acecd1ff93a" />




A análise identificou a presença de dados de um arquivo ZIP dentro da imagem.

Para extrair seu conteúdo, utilizei:

```bash
7z x dolls.jpg
```

O comando `7z` executa o programa 7-Zip, enquanto o parâmetro `x` extrai os arquivos encontrados, preservando a estrutura dos diretórios.

Após a extração, verifiquei os arquivos presentes na pasta `base_images`:

```bash
ls base_images
```

<img width="340" height="46" alt="image" src="https://github.com/user-attachments/assets/846d384d-8d2a-4e6a-926e-89fe178ca85c" />





Foi encontrado um novo arquivo de imagem, chamado `2_c.jpg`.

### Etapa 2 — Análise da segunda imagem

Seguindo a lógica do enunciado, executei novamente o Binwalk, dessa vez na imagem extraída:

```bash
binwalk base_images/2_c.jpg
```

<img width="781" height="320" alt="image" src="https://github.com/user-attachments/assets/19de5500-fe0e-4a7e-ba32-435378001e24" />




Novamente, foi identificada a presença de um arquivo ZIP, contendo uma nova imagem chamada `3_c.jpg`.

Para extrair esse arquivo, executei:

```bash
7z x base_images/2_c.jpg
```

Assim, foi possível avançar para a próxima camada do desafio.

### Etapa 3 — Extração da terceira imagem

Após a extração, confirmei a presença do arquivo `3_c.jpg` no diretório `base_images`.

<img width="632" height="638" alt="image" src="https://github.com/user-attachments/assets/f88232bf-3386-4713-83d0-6f23c37de9d1" />



Em seguida, utilizei novamente o Binwalk:

```bash
binwalk base_images/3_c.jpg
```

<img width="657" height="247" alt="image" src="https://github.com/user-attachments/assets/07f27838-a4cc-4cd3-8d69-78166e11e40e" />



A análise revelou outro ZIP, dessa vez contendo o arquivo `4_c.jpg`.

Esse resultado confirmou o padrão observado desde o início: cada imagem continha uma nova camada de arquivos compactados.

### Etapa 4 — Extração e análise da quarta imagem

Para continuar, executei:

```bash
7z x base_images/3_c.jpg
```


<img width="633" height="652" alt="image" src="https://github.com/user-attachments/assets/670f7dbe-662f-477d-a6ed-61ea141562aa" />


Com o arquivo `4_c.jpg` disponível, realizei mais uma análise:

```bash
binwalk base_images/4_c.jpg
```

<img width="625" height="282" alt="image" src="https://github.com/user-attachments/assets/6288df1b-7c18-410e-affc-cadbf820480d" />

Dessa vez, o conteúdo identificado indicava que estávamos próximos da etapa final, pois havia um arquivo chamado `flag.txt` armazenado no conteúdo compactado.

### Etapa 5 — Obtendo a flag

Para extrair o conteúdo final, utilizei:

```bash
7z x base_images/4_c.jpg
```

Após a extração, foi possível acessar o arquivo `flag.txt`.

Para ler seu conteúdo, executei:

```bash
cat flag.txt
```

O comando `cat` permite visualizar o conteúdo de arquivos de texto diretamente no terminal.

<img width="350" height="53" alt="image" src="https://github.com/user-attachments/assets/ed87a8e9-dae7-4843-9a9c-e1396b758d31" />



Com isso, a flag foi encontrada e o desafio concluído.

## 5. Conclusão

O desafio *Matryoshka Doll* demonstrou como arquivos de diferentes formatos podem estar embutidos dentro de uma imagem, exigindo uma investigação de sua estrutura interna.

A principal dificuldade foi o processo ser tão repetitivo, é um ótimo desafio, porém muito fácil de se perder a qualquer momento, como vc repete diversas vezes o processo, saber se tem que fazer mais uma ou não te deixa meio perdido.

Durante a resolução, foram utilizadas três ferramentas principais:

- **Binwalk:** para identificar assinaturas de arquivos ocultos nas imagens.
- **7-Zip:** para extrair os conteúdos compactados, preservando a estrutura dos diretórios.
- **Cat:** para visualizar o conteúdo do arquivo de texto que continha a flag.

O desafio também mostrou a importância de não analisar um arquivo apenas por sua extensão, já que uma imagem `.jpg` pode conter outros formatos de dados em seu interior.

Por fim, o nome *Matryoshka Doll* representa exatamente a estrutura do desafio: uma imagem dentro de outra, até encontrar o conteúdo final.







