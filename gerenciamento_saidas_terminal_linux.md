
# Gerenciamento de Saídas no Terminal Linux

O terminal Linux é uma interface poderosa que permite a interação direta com o
sistema operacional, por meio da execução de comandos. Ao realizar operações no
terminal, três fluxos principais gerenciam a entrada e saída de dados:

- **stdin** (entrada padrão): Responsável por receber a entrada de dados,
 geralmente do teclado.
- **stdout** (saída padrão): Onde os resultados bem-sucedidos dos comandos
são exibidos, normalmente o terminal.
- **stderr** (saída de erro): Usado para exibir mensagens de erro.

Neste artigo, vamos explorar como esses fluxos funcionam, como os códigos de
saída são utilizados para indicar sucesso ou falha, e como redirecionar essas
saídas para outras fontes.

## 1. Fluxos de Entrada e Saída no Linux

Quando você executa um comando no terminal, ele se comunica com o sistema
operacional através de três fluxos principais:

- **stdin**: Este é o fluxo de entrada padrão, onde o comando lê as informações
fornecidas pelo usuário. Geralmente, é o teclado, mas pode ser redirecionado de
um arquivo ou outro comando.

- **stdout**: Este é o fluxo de saída padrão, onde o comando envia suas saídas 
bem-sucedidas. Normalmente, essas saídas são exibidas no terminal.

- **stderr**: É o fluxo utilizado para mensagens de erro. Ao invés de enviar as
mensagens de erro para o stdout (misturando-se com as saídas regulares), elas
são separadas neste fluxo dedicado.

Esses três fluxos são representados internamente por descritores de arquivo:

- `0`: stdin
- `1`: stdout
- `2`: stderr

## 2. Redirecionando Saídas

Em muitos casos, pode ser útil redirecionar a saída de um comando para um arquivo
ou para outro comando. Isso pode ser feito utilizando operadores de redirecionamento:

- `>`: Redireciona a **stdout** para um arquivo (substitui o conteúdo do arquivo).
- `>>`: Redireciona a **stdout** para um arquivo (anexa ao conteúdo existente).
- `2>`: Redireciona a **stderr** para um arquivo.
- `&>`: Redireciona tanto a **stdout** quanto a **stderr** para um arquivo.

### Exemplo:

```bash
comando > saida.txt  # Redireciona a saída padrão para um arquivo
comando 2> erro.txt  # Redireciona os erros para um arquivo separado
```

Se você quiser descartar erros, pode redirecionar o stderr para `/dev/null`, que
é um "buraco negro" que descarta tudo o que é enviado para ele:

```bash
comando 2> /dev/null  # Ignora todas as mensagens de erro
```

## 3. Combinando Saídas

Se for necessário combinar stdout e stderr em um único arquivo, você pode usar
a seguinte sintaxe:

```bash
comando > arquivo.txt 2>&1
```

Aqui, o `2>&1` significa que o **stderr** (2) será redirecionado para o mesmo
destino que o **stdout** (1), resultando em ambas as saídas combinadas em `arquivo.txt`.

## 4. Códigos de Saída

Cada comando no Linux retorna um código de saída após sua execução. Esse código
é um número que indica o status do comando:

- **0**: O comando foi executado com sucesso.
- **1** (ou outro valor diferente de zero): Ocorreu um erro.

Você pode visualizar o código de saída do último comando executado usando o
comando `echo $?`. Por exemplo:

```bash
ls /algum/diretorio
echo $?  # Exibe o código de saída do último comando
```

## 5. Quem Gerencia as Saídas?

O gerenciamento das saídas e do código de retorno é uma responsabilidade conjunta
do programa e do sistema operacional:

- **Programa**: Cada programa é projetado para enviar suas saídas para stdout ou
stderr conforme apropriado. Além disso, o programa define o código de saída que
será retornado após sua execução.
- **Sistema Operacional**: O kernel do Linux é responsável por gerenciar os
descritores de arquivo (stdin, stdout e stderr) e fornecer ao programa uma
maneira de interagir com eles. Também é o kernel que, após a finalização do
programa, coleta o código de saída e o disponibiliza para outros programas ou scripts.

Quando um programa termina, ele devolve um código de saída ao sistema operacional,
que pode ser verificado e utilizado para tomar decisões em scripts ou processos
automáticos.

## 6. Interrupções e Manipulação de Sinais

Interrupções de execução, como `Ctrl+C`, são tratadas por meio de **sinais** no Linux.
Esses sinais são uma forma de comunicação entre o sistema e os processos, indicando
que alguma ação deve ser tomada.

Por exemplo, o sinal **SIGINT** (geralmente enviado ao pressionar `Ctrl+C`) interrompe
um processo em execução. Quando um processo é interrompido por um sinal, ele normalmente
retorna um código de saída correspondente ao sinal recebido.

### Exemplo de sinais comuns:

- `SIGINT` (2): Interrupção do programa (geralmente enviada por `Ctrl+C`).
- `SIGKILL` (9): Finalização forçada de um processo.
- `SIGTERM` (15): Solicitação de término de um processo.

A relação entre sinais e códigos de saída é direta: quando um programa é
encerrado por um sinal, o código de saída normalmente reflete o número do sinal.

### Exemplo:

```bash
sleep 100
# Pressione Ctrl+C para interromper
echo $?  # O código de saída será 130 (128 + número do sinal 2 para SIGINT)
```

## 7. Visualizando Códigos de Saída e Erros

Nem todos os códigos de saída podem ser conhecidos diretamente por um único
comando, mas existem formas de visualizar e entender os códigos retornados
pelos comandos e programas.

### 7.1. Códigos de Saída Padrão

O sistema Linux adota códigos de saída padronizados para representar o sucesso
ou falha de uma operação. Aqui estão alguns exemplos comuns:

- **0**: Sucesso (sem erros).
- **1**: Erro genérico.
- **2**: Uso incorreto de comando (erro de sintaxe).
- **126**: O comando não pode ser executado.
- **127**: Comando não encontrado.
- **128**: Argumento inválido para um sinal de encerramento.
- **130**: Interrompido por `Ctrl+C` (SIGINT).
- **137**: Comando terminado por `SIGKILL`.
- **255**: Erro de retorno fora do intervalo permitido.

Cada programa pode definir seus próprios códigos de saída, mas muitos seguem esses padrões.

### 7.2. Obtendo Códigos de Saída de Comandos

Se você quer visualizar o código de saída de um comando específico, pode usar o comando
especial `echo $?` após a execução do comando. Por exemplo:

```bash
ls /nonexistent
echo $?  # Exibe o código de saída do último comando
```

Aqui, o código de saída indica se o comando foi executado com sucesso ou se houve algum erro.

### 7.3. Definindo Códigos de Saída em Scripts

Se estiver escrevendo um script, você pode definir códigos de saída personalizados com o
comando `exit`. Isso é útil para indicar se a execução do script foi bem-sucedida ou se
ocorreu algum erro:

```bash
#!/bin/bash
if [ "$1" == "ok" ]; then
    echo "Executado com sucesso"
    exit 0
else
    echo "Ocorreu um erro"
    exit 1
fi
```

### 7.4. Listando Sinais e Códigos de Erro

No Linux, você pode usar o comando `kill -l` para listar os sinais que podem ser enviados
aos processos. Cada um desses sinais pode causar a terminação de um processo com um
código de saída específico:

```bash
kill -l
```

Isso mostrará uma lista de sinais como SIGINT, SIGTERM, SIGKILL, entre outros, que têm
associações com determinados códigos de saída.

Esses códigos de saída permitem que você gerencie melhor o comportamento dos seus
programas e scripts no Linux, seja para depuração ou automação de tarefas.

## Conclusão

O gerenciamento de fluxos de entrada e saída no terminal Linux é fundamental para o
controle eficiente de processos e comandos. Com a separação entre stdin, stdout, e
stderr, o sistema operacional e os programas têm uma forma estruturada de lidar com
informações, sucessos e falhas. Entender como redirecionar essas saídas, utilizar
corretamente os códigos de saída, e interpretar sinais ajuda tanto na criação de
scripts robustos quanto na depuração de programas.

Por fim, dominar esses conceitos não só torna o uso do terminal mais produtivo,
como também possibilita uma automação mais eficiente das tarefas, resultando em
um ambiente de trabalho mais controlado e previsível. A flexibilidade e o poder
do Linux estão, em grande parte, na maneira como ele gerencia esses fluxos,
permitindo ao usuário configurar e otimizar o sistema conforme suas necessidades.


Referência:

1. https://www.certificacaolinux.com.br/comando-linux-condutores/
2. https://www.youtube.com/watch?v=H9J_JG9oxl4
3. https://wiki.unicentro.br/Redirecionamento_de_entrada_e_sa%C3%ADda
4. https://www.ibm.com/docs/pt-br/i/7.5?topic=functions-signal-handle-interrupt-signals
5. https://www.ibm.com/docs/pt-br/psfa/7.1.0?topic=system-stop-errant-processes
