# Entendendo o Processo de Compilação: Do Código de Alto Nível à Linguagem de Máquina

O processo de compilação é fundamental na transformação do código escrito em linguagens
de alto nível para um formato que os computadores possam entender, conhecido como linguagem de máquina.
Neste artigo, exploraremos cada etapa desse processo, utilizando um exemplo de código em C
e focando especialmente na tokenização e análise semântica.

## Exemplo de Código de Alto Nível

Para ilustrar o processo, consideremos o seguinte trecho de código escrito em C:

```c
int main() {
    int x = 10;
    int y = x + 20;
    return y;
}
```

## 1. Tokenização

A primeira etapa da compilação é a **tokenização**, na qual o compilador divide o código
em unidadessignificativas chamadas **tokens**. Cada token é uma representação estruturada
que inclui o tipo do token e, em alguns casos, o valor associado. Por exemplo, no código
acima, o símbolo `(` (parêntese esquerdo) é transformado em um token:

- **Token**: `LPAREN` (representa o parêntese esquerdo)
- **Tipo**: Símbolo (ou operador)
- **Valor**: `(`

Assim, a tokenização gera uma lista de tokens que representam os componentes do código-fonte,
como palavras-chave, identificadores, literais e operadores.

## 2. Análise Sintática

Após a tokenização, o compilador realiza a **análise sintática**. Nessa fase, os tokens são
organizados em uma estrutura hierárquica, como uma árvore de sintaxe, que reflete a estrutura
gramatical do código. No nosso exemplo, a árvore de sintaxe pode ser representada da seguinte
forma:

```
Function Declaration
    ├── Keyword: int
    ├── Identifier: main
    ├── LPAREN  // Aqui está o parêntese esquerdo
    ├── RPAREN
    └── Body
```

## 3. Análise Semântica
A fase seguinte é a **análise semântica**, onde o compilador verifica se a estrutura e o uso dos
tokens fazem sentido dentro do contexto da linguagem. Nesta etapa, o compilador assegura que:

- O `LPAREN` é corretamente emparelhado com um `RPAREN` (parêntese direito).
- As variáveis são utilizadas de acordo com seus tipos e escopos.

Por exemplo, no código `int y = "hello";`, o compilador detectaria um erro, pois a variável `y` 
foi declarada como `int`, mas está sendo atribuída uma string, que não é compatível.


## 4. Geração de Código Intermediário
Depois da análise semântica, o compilador gera **código intermediário**. Esta representação pode
ser usada para facilitar a tradução para a linguagem de máquina. A chamada da função `main` pode
ser representada em código intermediário, utilizando um marcador para os parênteses que indicam
o início e o fim dos argumentos.
#### Exemplo de Código Intermediário:
```plaintext
CALL main
```

## 5. Geração de Código de Máquina
Finalmente, na fase de **geração de código de máquina**, o compilador traduz o código intermediário
em instruções que a máquina pode entender. Embora o símbolo `(` não apareça diretamente na linguagem
de máquina, as operações associadas à chamada da função serão representadas. Um exemplo de código de
máquina para a chamada da função pode parecer com:
```plaintext
PUSH EBP
MOV EBP, ESP
CALL main
```

Aqui, as instruções refletem as operações realizadas pela função, mas o parêntese em si não é
explicitamente representado.

## Conclusão
O processo de compilação transforma o código de alto nível em instruções que a máquina pode executar.
Desde a tokenização, onde os símbolos são convertidos em tokens estruturados, até a geração de código
de máquina, cada fase desempenha um papel crucial em garantir que o código seja executado corretamente.
Este processo garante que o código seja organizado, verificado e traduzido de forma eficiente,
permitindo que programas escritos em linguagens de alto nível sejam executados em sistemas computacionais.

Referência:

1. https://johnidm.gitbooks.io/compiladores-para-humanos/content/part1/structure-of-a-compiler.html
2. https://professor.pucgoias.edu.br/SiteDocente/admin/arquivosUpload/17389/material/Aulao.pdf
3. http://www.inf.ufes.br/~tavares/labcomp2000/anasint.html

