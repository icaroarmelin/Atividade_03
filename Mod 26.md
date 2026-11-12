
# Mod 26

**Categoria:** Criptografia  
**Plataforma:** CyLab  
**Dificuldade:** Fácil

## 1. Introdução

Este write-up apresenta a resolução do desafio *Mod 26*, disponibilizado na plataforma CyLab como exercício prático de criptografia.

O desafio consiste em decodificar uma mensagem utilizando uma técnica de substituição de caracteres conhecida como ROT13.

Seu principal objetivo é introduzir conceitos básicos de criptografia, especialmente as cifras de substituição e o funcionamento da aritmética modular.

## 2. Enunciado

O desafio apresenta a seguinte descrição:

> "Cryptography can be easy, do you know what ROT13 is?"

Além do enunciado, é disponibilizada uma sequência de caracteres codificados, que devemos decifrar para encontrar a flag.

## 3. Interpretação do desafio

O enunciado fornece uma dica importante ao mencionar diretamente o ROT13.

O ROT13 é uma variação da cifra de César, um método de substituição no qual cada letra é substituída por outra localizada a uma quantidade fixa de posições à frente no alfabeto.

No caso do ROT13, esse deslocamento é de 13 posições.

Como o alfabeto utilizado possui 26 letras, podemos representar matematicamente a transformação por:

\[
f(x) = (x + 13) \bmod 26
\]

Onde:

- `x` representa a posição da letra no alfabeto, começando em 0.
- `13` representa a quantidade de posições deslocadas.
- `mod 26` representa o resto da divisão por 26, permitindo que a contagem retorne ao início do alfabeto.

Por exemplo, a letra `A` se transforma em `N`, enquanto a letra `N` se transforma em `A`.

Dessa forma, aplicar o ROT13 duas vezes retorna à mensagem original.

A partir dessa interpretação, a estratégia foi utilizar o terminal Linux para substituir os caracteres da mensagem e recuperar a flag.

## 4. Resolução

### Etapa 1 — Análise da mensagem codificada

Ao iniciar o desafio, recebemos uma sequência de caracteres semelhante a:

```text
cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_...}
```

**Resultado:**

<!-- Inserir print do enunciado e da mensagem original -->

Ao observar a sequência, percebemos que ela possui uma estrutura semelhante ao formato das flags utilizadas no CyLab:

```text
picoCTF{...}
```

Entretanto, os caracteres aparecem substituídos por outras letras.

Como o enunciado menciona o ROT13, podemos testar esse método de decodificação.

### Etapa 2 — Entendendo o ROT13

Antes de realizar a decodificação, é importante compreender como funciona o deslocamento das letras.

No ROT13, cada letra é substituída por outra localizada 13 posições à frente no alfabeto.

Por exemplo:

```text
Original: ABCDEFGHIJKLMNOPQRSTUVWXYZ
ROT13:    NOPQRSTUVWXYZABCDEFGHIJKLM
```

Assim:

- `A` se transforma em `N`.
- `B` se transforma em `O`.
- `C` se transforma em `P`.
- `N` se transforma em `A`.
- `O` se transforma em `B`.
- `P` se transforma em `C`.

Esse processo também funciona com letras minúsculas.

Caracteres como números, espaços, chaves e símbolos não são alterados pelo ROT13.

Uma característica importante dessa cifra é que o próprio ROT13 pode ser utilizado tanto para codificar quanto para decodificar uma mensagem.

### Etapa 3 — Decodificando com o terminal Linux

Para resolver o desafio, podemos utilizar o comando `tr`, disponível em sistemas Linux.

Esse comando permite substituir caracteres de uma entrada por outros caracteres definidos pelo usuário.

A estrutura utilizada foi:

```bash
echo "MENSAGEM_CODIFICADA" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

Podemos dividir o comando em algumas partes:

- `echo`: exibe a mensagem informada.
- `|`: encaminha a saída de um comando para a entrada de outro.
- `tr`: realiza a substituição dos caracteres.
- `'A-Za-z'`: representa o alfabeto original, incluindo letras maiúsculas e minúsculas.
- `'N-ZA-Mn-za-m'`: representa o alfabeto com deslocamento de 13 posições.

Dessa forma, o comando realiza automaticamente a substituição necessária para aplicar o ROT13.

### Etapa 4 — Obtendo a flag

Após compreender o funcionamento do comando, basta substituir `MENSAGEM_CODIFICADA` pela sequência fornecida no desafio.

Por exemplo, podemos testar:

```bash
echo "cvpbPGS" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

**Resultado:**

```text
picoCTF
```

Isso confirma que o método utilizado está correto.

Em seguida, aplicamos a mesma substituição à mensagem completa.

**Resultado:**

<!-- Inserir print do comando utilizado e da flag decodificada -->

Após a execução, a sequência original é transformada em uma mensagem legível, revelando a flag.

O resultado apresenta a estrutura:

```text
picoCTF{next_time_I'll_try_2_rounds_of_rot13_...}
```

Com isso, o desafio foi concluído.

## 5. Conclusão

O desafio *Mod 26* demonstrou o funcionamento de uma cifra de substituição simples, conhecida como ROT13.

Inicialmente, a mensagem apresentada parecia ser apenas uma sequência de caracteres sem significado. Entretanto, ao interpretar o enunciado e compreender a técnica mencionada, foi possível identificar o método de codificação utilizado.

Durante a resolução, foram utilizados os seguintes conhecimentos e ferramentas:

- **ROT13:** para compreender a substituição de caracteres por meio de um deslocamento de 13 posições.
- **Cifra de César:** para entender o conceito de deslocamento fixo dentro de um alfabeto.
- **Aritmética modular:** para compreender como os deslocamentos retornam ao início do alfabeto.
- **Echo:** para enviar a mensagem codificada pelo terminal.
- **Tr:** para realizar a substituição automática dos caracteres.

O principal aprendizado foi compreender que o ROT13 é uma técnica de substituição reversível, na qual a mesma operação pode ser utilizada tanto para codificar quanto para decodificar uma mensagem.

Além disso, o desafio mostrou como ferramentas simples do terminal Linux podem ser utilizadas para resolver problemas básicos de criptografia, sem a necessidade de desenvolver programas mais complexos.


Além disso, o desafio mostrou como ferramentas simples do terminal Linux podem ser utilizadas para resolver problemas básicos de criptografia, sem a necessidade de desenvolver programas mais complexos.
