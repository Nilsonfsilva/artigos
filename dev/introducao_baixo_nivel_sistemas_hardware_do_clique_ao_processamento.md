# Introdução ao Baixo Nível e Sistemas de Hardware: Do Clique ao Processamento

A programação em baixo nível, como Assembly, envolve entender como o hardware e 
o software interagem diretamente. Este artigo pretende explicar esse processo 
passo a passo, ilustrando como um computador executa um programa, desde o clique 
no ícone até a manipulação de dados pelos registradores da CPU. Para isso, vamos 
explorar como os componentes do sistema interagem, o papel da memória física e 
virtual, e a importância da arquitetura de Von Neumann.

A **Arquitetura de Von Neumann** é o modelo básico que descreve como os 
computadores modernos funcionam. Esse modelo tem a característica de usar uma 
**memória unificada** para armazenar tanto as **instruções** do programa quanto 
os **dados** que o programa manipula. Em outras palavras, a CPU lê instruções e 
dados da mesma memória. 

Essa arquitetura simples, no entanto, cria o que chamamos de **gargalo de Von 
Neumann**, onde a CPU pode ficar esperando por dados ou instruções, já que o 
barramento que conecta a memória e o processador tem largura limitada. No 
entanto, essa arquitetura é amplamente utilizada por ser eficiente e fácil de 
implementar, e continua a ser o padrão para a maioria dos sistemas 
computacionais.

---

## 1. Introdução ao Processamento em Baixo Nível

Quando falamos de programação em baixo nível, estamos nos referindo à escrita de 
códigos que interagem diretamente com o hardware, sem passar por muitas camadas 
de abstração, como acontece em linguagens de alto nível (C, Python, Java, etc.). 
Nesse nível, é fundamental entender o funcionamento da **CPU**, das **memórias** 
e do **sistema operacional**.

- A **CPU** é responsável por executar instruções diretamente, manipulando dados 
e realizando cálculos.
- As **memórias** (RAM e disco) são responsáveis por armazenar dados e 
instruções. A diferença entre memória **volátil** (RAM) e **não volátil** 
(HD/SSD) é fundamental: a RAM é mais rápida e temporária, enquanto o disco é 
mais lento, mas armazena dados permanentemente.
- O **sistema operacional** é a ponte entre o hardware e o software, gerenciando 
o uso de recursos como memória e CPU.

## 2. O Papel do Sistema Operacional no Controle de Recursos

O sistema operacional (SO) tem um papel essencial na gestão dos recursos do 
computador, como a **memória**, a **CPU**, e os **dispositivos de entrada/saída** 
(E/S). Ele faz isso por meio de funções como:

- **Gerenciamento de memória**: O SO aloca espaço na memória para programas em 
execução e dados que estão sendo manipulados.
- **Gerenciamento de processos**: Ele controla quais programas estão rodando, 
garantindo que cada um tenha tempo suficiente na CPU.
- **Gerenciamento de dispositivos de E/S**: Cuida da comunicação entre o hardware 
e os dispositivos como teclado, mouse, impressora, etc.

Em sistemas modernos, o sistema operacional oferece uma camada de abstração 
entre o hardware e o software, facilitando o desenvolvimento de programas sem 
que os desenvolvedores precisem se preocupar com detalhes técnicos de baixo 
nível. No entanto, ao programar em Assembly, ou em outros níveis de baixo nível, 
é crucial entender essa dinâmica interna para otimizar o desempenho e os 
recursos.

## 3. Componentes Básicos de um Sistema de Computador

Um computador típico possui vários componentes que trabalham juntos para 
executar programas. Os principais são:

- **CPU (Unidade Central de Processamento)**: Onde os cálculos e operações 
lógicas são realizados.
- **Memória**: Aqui, distinguimos entre:
  - **Memória RAM (Memória de Acesso Aleatório)**: Usada para armazenar dados 
temporários que o processador precisa acessar rapidamente.
  - **Memória de armazenamento (HD ou SSD)**: Armazena os dados permanentemente, 
até que o usuário ou sistema os modifique ou remova.
- **Barramentos**: São caminhos que ligam a CPU à memória e a outros 
dispositivos. Eles transportam dados, endereços de memória e sinais de controle.

## 4. O Ciclo de Execução: Do Clique ao Processamento

Agora que temos uma visão geral do sistema, vamos seguir com um exemplo prático 
para entender o que acontece desde o momento em que você clica para abrir um 
programa até o processamento final pela CPU.

### 4.1. Clicando no Ícone: O Programa no Armazenamento Permanente (HD/SSD)

Quando você clica em um programa, como a **Calculadora**, o **executável** do 
programa, que está armazenado no **HD ou SSD**, é carregado. Esse executável é 
um arquivo binário que contém o código que a CPU precisará executar.

O **HD ou SSD** é mais lento em comparação à memória RAM, mas é o local onde os 
dados ficam armazenados de forma **permanente**. No entanto, o programa não é 
executado diretamente a partir do HD/SSD. Ele primeiro precisa ser **carregado 
na memória RAM**.

### 4.2. Carregamento na Memória Física e Memória Virtual

Aqui, a distinção entre **memória física** e **memória virtual** entra em jogo.

- A **memória física** refere-se à quantidade de RAM física instalada no 
sistema.
- A **memória virtual** é uma abstração criada pelo sistema operacional. Ela faz 
o programa "pensar" que tem acesso a toda a memória, mesmo que parte dela não 
esteja fisicamente disponível. Isso é feito por meio de **endereços virtuais**.

O sistema operacional usa uma técnica chamada de **paginação**, onde o espaço de 
endereçamento é dividido em **páginas**. Essas páginas são **mapeadas** da 
memória virtual para a memória física conforme necessário. Cada programa tem a 
impressão de estar ocupando toda a memória, mas na verdade só as partes que estão 
sendo usadas naquele momento são carregadas na memória física. Esse mapeamento é 
gerenciado por uma tabela de **offsets**, que traduz os endereços virtuais para 
físicos.

Isso é importante para o funcionamento eficiente de sistemas multitarefa e para 
garantir que o programa tenha acesso apenas ao que realmente precisa. Quando o 
**loader** carrega o programa, ele o coloca na memória virtual, e conforme o 
programa roda, as páginas são trazidas para a memória física conforme necessário.

### 4.3. Reconhecimento pelo Processador

Agora que o programa está na **memória (RAM)**, o **processador (CPU)** começa a 
trabalhar. Ele lê as instruções do programa diretamente da RAM e as executa.

A **CPU** acessa essas instruções usando **endereços de memória virtual**, que 
são convertidos para endereços físicos conforme o necessário pelo sistema 
operacional.

### 4.4. O Papel dos Registradores

Dentro da CPU, os **registradores** são pequenos espaços de armazenamento ultra 
rápidos que guardam dados temporários durante o processamento. São esses 
registradores que a CPU usa para realizar operações matemáticas e lógicas.

Por exemplo, ao somar dois números, a CPU vai primeiro buscar os valores na RAM, 
carregá-los em dois registradores (por exemplo, **R1** e **R2**), somá-los e 
armazenar o resultado em um terceiro registrador (por exemplo, **R3**). O valor 
resultante pode ser então armazenado de volta na RAM ou ser enviado diretamente 
para um dispositivo de saída, como a tela.

#### Exemplo Prático: Soma de Dois Números

Vamos imaginar que você quer somar **5 + 3** no programa Calculadora:

1. **Entrada de Dados**: Você digita "5" e "3". Esses números são 
temporariamente armazenados na **memória RAM**.
2. **Processamento**:
   - A CPU carrega o número **5** em um registrador, digamos, **R1**.
   - Carrega o número **3** em outro registrador, **R2**.
   - A CPU soma os valores de **R1** e **R2** e armazena o resultado, **8**, em 
um terceiro registrador, **R3**.
3. **Resultado**: O valor **8** é movido de volta para a RAM e depois enviado 
para o dispositivo de saída (a tela), onde você vê o resultado final na 
interface da calculadora.

Essa interação entre memória, CPU e registradores é o coração do processamento 
em baixo nível.

---

## Conclusão

Neste artigo, exploramos o processo de execução de um programa, desde o clique 
até o processamento, detalhando como o sistema operacional gerencia a **memória 
física e virtual**, o papel da **CPU** e dos **registradores**, e como a 
**Arquitetura de Von Neumann** organiza o funcionamento dos computadores 
modernos. Entender esses conceitos é fundamental para quem deseja programar em 
baixo nível, pois permite otimizar o desempenho e o uso de recursos do sistema.


Referência:
1. https://www.facom.ufu.br/~claudio/Cursos/Antigos/ICC/Resources/Modulo01/Intr_Hardware.pdf

2. https://www.dcce.ibilce.unesp.br/~aleardo/cursos/fsc/cap12.php

3. https://edisciplinas.usp.br/pluginfile.php/7596147/mod_folder/content/0/10-OrganizacaoRegistradores.pdf

4. https://mentebinaria.gitbook.io/engenharia-reversa/assembly/registradores

