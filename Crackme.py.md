# Crackme.py

**Categoria:** Engenharia Reversa  
**Plataforma:** CyLab  
**Dificuldade:** A confirmar

## Introdução

Este write-up apresenta a resolução do desafio *Crackme.py*, disponibilizado na plataforma CyLab como exercício prático de engenharia reversa.

O objetivo do desafio é analisar um programa escrito em Python, compreender seu funcionamento e encontrar uma flag escondida no código.

## Enunciado

O desafio disponibiliza um arquivo chamado `crackme.py`, que contém um programa escrito em Python.

O objetivo é investigar o código e descobrir como recuperar a informação escondida.

## Interpretação do desafio

O nome *Crackme* é geralmente utilizado em desafios de engenharia reversa, nos quais precisamos analisar um programa para descobrir uma senha, identificar uma informação oculta ou compreender alguma condição necessária para obter o resultado esperado.

Como o arquivo disponibilizado está escrito em Python, podemos analisar diretamente seu código-fonte, observando suas funções, variáveis e operações.

Dessa forma, a estratégia foi analisar o funcionamento do programa e procurar possíveis funções ou informações que não fossem utilizadas durante sua execução normal.

## Resolução

### Etapa 1: Análise do arquivo

Após realizar o download do arquivo `crackme.py`, comecei a investigação utilizando o comando:

```bash
cat crackme_gen.py
```

O comando `cat` permite visualizar o conteúdo de arquivos diretamente no terminal.

<img width="812" height="830" alt="image" src="https://github.com/user-attachments/assets/42c6e38d-d953-401b-9c70-8961ddf13ed2" />
<img width="1162" height="232" alt="image" src="https://github.com/user-attachments/assets/f9a7f53d-71c3-40bf-bc71-e5956024a38f" />




Ao analisar o código, foi possível identificar uma variável chamada `bezos_cc_secret`, que armazenava uma sequência de caracteres aparentemente sem significado.

Além disso, duas funções chamaram a atenção:

- `choose_greatest()`: responsável por comparar dois números.
- `decode_secret()`: responsável por decodificar uma sequência de caracteres.

A presença de uma função de decodificação indicava que poderia existir alguma informação escondida dentro do programa.

### Etapa 2: Executando o programa

Para entender melhor seu funcionamento, executei:

```bash
python crackme_gen.py
```


<img width="395" height="110" alt="image" src="https://github.com/user-attachments/assets/a67d3c88-bc49-41b0-8f28-d0a06319f399" />


O programa solicitava dois números e informava qual deles era o maior.

Entretanto, esse comportamento não parecia estar relacionado ao objetivo principal do desafio.

Ao observar o código novamente, percebi que a função `choose_greatest()` era executada normalmente, enquanto a função `decode_secret()` não era chamada.

Isso indicava que seria necessário investigar a função de decodificação.

### Etapa 3: Analisando a função decode_secret()

Ao analisar a função, encontrei o seguinte trecho:

```python
def decode_secret(secret):
    rotate_const = 47
    decoded = ""

    for c in secret:
        index = alphabet.find(c)
        original_index = (index + rotate_const) % len(alphabet)
        decoded = decoded + alphabet[original_index]

    print(decoded)
```

Essa função utiliza uma técnica de substituição de caracteres conhecida como **ROT47**.

O ROT47 funciona deslocando cada caractere em 47 posições dentro de um conjunto de 94 caracteres ASCII imprimíveis.

Portanto, a própria função já possuía a lógica necessária para recuperar a mensagem original.

### Etapa 4: Executando a função de decodificação

Após compreender o funcionamento do código, percebi que não seria necessário desenvolver outro algoritmo para descobrir a mensagem.

Bastava executar a função `decode_secret()` utilizando como argumento a variável que armazenava a mensagem codificada.

Para isso, adicionei a seguinte linha ao final do programa:

```python
decode_secret(bezos_cc_secret)
```

Essa instrução faz com que a função receba a mensagem codificada e aplique o processo de decodificação.

Em seguida, executei novamente:

```bash
python crackme_gen.py
```

**Resultado:**

<img width="297" height="18" alt="image" src="https://github.com/user-attachments/assets/ffcc986f-1990-4627-8358-9de114768fda" />

Após a execução, o programa exibiu a mensagem decodificada, revelando a flag do desafio.

## 5. Conclusão

O desafio *Crackme.py* demonstrou a importância de analisar o funcionamento de um programa antes de tentar descobrir uma senha ou quebrar uma codificação.

Inicialmente, o programa aparentava realizar apenas uma comparação entre dois números. Entretanto, ao investigar seu código-fonte, foi possível identificar uma função de decodificação que não era utilizada durante a execução normal.

Durante a resolução, foram utilizados os seguintes conhecimentos e ferramentas:

- **Python:** para compreender o funcionamento e modificar a execução do programa.
- **Cat:** para visualizar o conteúdo do arquivo no terminal.
- **Engenharia reversa:** para investigar as funções e identificar informações relevantes.

O principal aprendizado foi que nem todas as funções de um programa são executadas automaticamente e que informações importantes podem estar presentes em partes do código que inicialmente parecem não ter utilidade.

Além disso, o desafio mostrou que, em determinadas situações, a solução já pode estar presente no próprio programa, sendo necessário apenas compreender como utilizá-la.
