##                    Entendendo o Processo de Endurecimento na Compilação de Programas


## 1. Etapas no processo de compilação:

   1.1 Escrever código-fonte num  bloco de notas e/ou IDE.
   Esta é a fase onde o programador escreve o código em uma linguagem de alto nível, como C por exemplo.
   Esse código (arquivo de texto) é  dividido em várias seções:
      * Seção de código (funções e lógica),
      * Declaração de variáveis,Constantes,
      * Chamada de bibliotecas externas (através de #include para cabeçalhos ou
   chamadas dinâmicas como dlls no Windows ou so no Linux).

## 2. Compilação (geração do código objeto):

   2.1 Análise léxica: O compilador lê o código-fonte e converte-o em **tokens**
   (elementos básicos como palavras-chave, identificadores, operadores).

   2.2  Análise sintática: O compilador verifica se a estrutura do código está
   de acordo com as regras da linguagem (sintaxe).

   2.3  nálise semântica: Valida se as operações fazem sentido, como tipos de dados compatíveis.

   2.4 Geração do código intermediário: O compilador converte o código-fonte em uma forma intermediária
   mais próxima do código de máquina.

   2.5 Otimização: O compilador pode otimizar o código intermediário para melhorar o desempenho.

   2.6 Geração de código objeto: O código intermediário é traduzido para código objeto,
   que é código de máquina incompleto, com referências a bibliotecas externas ou funções
   que ainda precisam ser resolvidas.
   Aqui, o processo de ligação com DLLs (ou bibliotecas dinâmicas) não ocorre ainda.
   A linguagem com as bibliotecas externas é resolvida apenas na próxima etapa, que é o
   **link-editing**(ligação).

## 3. Linkagem (link editing):
   Ligação: O linker (ou ligador) toma os arquivos objeto gerados na etapa de compilação
   e resolve as referências a bibliotecas externas (como funções declaradas em outros
   **arquivos .o,bibliotecas estáticas .a, ou dinâmicas .dll ou .so).**

   3.1  Linkagem estática: O linker incorpora as bibliotecas diretamente no binário final.

   3.2  Linkagem dinâmica: O linker cria referências para que o binário carregue as bibliotecas
   dinâmicas apenas no momento da execução.

   3.3  Geração do executável: Após a resolução das dependências, o linker gera o código de máquina
   final, criando o arquivo binário que pode ser executado diretamente pelo sistema operacional.

   A escrita do código-fonte: Divisão em seções (funções, variáveis, etc.).
   Compilação: Verificação do código, análise léxica/sintática/semântica, geração de código objeto.
   Linkagem: Resolver chamadas de bibliotecas e gerar o executável.
   Obs: A ligação com DLLs/bibliotecas ocorre durante a linkagem, não na etapa de compilação.


## 4. O que  endurecimento ou herdening num processo de compilação?
   O conceito de endurecimento ("hardening") na compilação de programas refere-se a um conjunto de
   técnicas usadas para tornar o programa mais seguro contra ataques comuns, como buffer overflows
   e execução arbitrária de código. Essas variáveis que você mencionou (como o ** _FORTIFY_SOURCE**)
   ajustam o comportamento do compilador e do linker, garantindo que o código final tenha proteções
   adicionais.

   No processo de compilação de programas em linguagens como C e C++, existem diversas vulnerabilidades
   conhecidas que podem ser exploradas por invasores. O endurecimento visa impedir ou, pelo menos,
   dificultar essas explorações. 

   Por exemplo:
   * **_FORTIFY_SOURCE**: Fortalece funções de manipulação de memória, como strcpy e sprintf, para que
   realizem verificações extras em busca de possíveis vulnerabilidades.

   * PIE (Position Independent Executable): Garante que o programa seja carregado em diferentes
   endereços de memória a cada execução, dificultando ataques baseados na localização fixa do código.

   * Stack Canaries: Inserem um valor especial ("canário") no início da pilha de execução.
   Se um invasor tentar realizar um buffer overflow, o valor do canário será corrompido,
   alertando o sistema sobre o ataque.
 
   * RELRO (Relocation Read-Only): Torna certas partes da memória somente leitura depois que
   o programa é inicializado, evitando que sejam alteradas durante a execução.

   A fim de entender esse processo, imagine que seu programa é uma casa. Um programa sem
   endurecimento seria uma casa com portas e janelas normais, que podem ser forçadas com
   relativa facilidade. Com o endurecimento, você está instalando portas blindadas, janelas
   de segurança, e um alarme que detecta qualquer tentativa de invasão.
 
   O 'Stack Canaries' é como um alarme que avisa se alguém está tentando mexer
   na pilha (como se alguém estivesse tentando mexer no telhado da casa).
   O 'PIE' é como mudar a localização dos cômodos da casa cada vez que alguém
   tenta entrar — o invasor nunca sabe onde as coisas estarão.
   O 'RELRO' é como colocar trancas extras em certos cômodos que nunca devem
   ser alterados depois que você fechou as portas.
 
   Assim, essas variáveis e técnicas tornam seu programa mais resistente a ataques,
   adicionando diversas "camadas de proteção".
   Logo quando as variáveis são setadas, elas  instruem o compilador a gerar o código
   com essas proteções extras, mas o processo vai além disso.

##   5.  Qual o papel do compilador e sistema operaconal no precesso de compilação e endurecimento:

   **5.1 Compilação e Linkagem**
   O endurecimento começa quando o código-fonte é compilado e transformado em código de
   máquina. Durante esse processo, o compilador injeta as proteções, conforme especificado
   pelas flags (como **_FORTIFY_SOURCE**, -fstack-protector, etc.).
 
   Além disso, o linker (que une o código e as bibliotecas) também pode adicionar proteções,
   como marcar certas áreas da memória como somente leitura. Ele também pode configurar o
   código para ser independente de posição (PIE), o que permitirá que o loader aloque o
   programa em diferentes regiões da memória.

   5.2. Execução pelo Loader
   Quando o programa é executado, o loader do sistema operacional carrega o programa na memória.
   Ele segue as instruções de proteção que foram configuradas durante a compilação. Por exemplo:

   Randomização de Endereço: Se o programa foi compilado com PIE, o loader aloca o código e os
   dados do programa em locais aleatórios na memória, tornando difícil para um invasor prever
   onde estão as partes vulneráveis.

   Proteção da Pilha: Se o compilador adicionou Stack Canaries, o loader garantirá que o
   código de proteção da pilha seja ativado durante a execução.

   Proteção de Segmentos de Memória: Com o RELRO, o loader marca certas regiões da memória
   como somente leitura, prevenindo ataques que tentem sobrescrever dados sensíveis.

   5.3 O Papel do Kernel:
   O kernel do sistema operacional orquestra todo esse processo, garantindo que as proteções
   que foram inseridas no código durante a compilação sejam respeitadas durante a execução.

   O kernel é responsável por:
    * Configurar a randomização da memória (ASLR),
    * Garantir que as permissões de memória (leitura, escrita, execução) estejam corretas,
    * Ativar a proteção da pilha e as outras proteções como as verificações do _FORTIFY_SOURCE.


   6.0 Então quer dizer que, ao compilar um programa, ou seja, na geração do objeto e na linkagem,
   eu tenho que pedir ao compilador que o programa seja compilado com essas precauções.
   O loader, por sua vez, quando for carregar o programa na memória, já sabe como fazer,
   uma vez que ele foi compilado com flags que cuidam dessas possíveis tentativas de ataque?

   Durante o processo de compilação e linkagem, o compilador e o linker seguem as instruções
   fornecidas pelas flags de endurecimento (como _FORTIFY_SOURCE, PIE, Stack Canaries, RELRO). 
   Isso gera um código binário que já inclui as proteções contra possíveis ataques.

   Quando o programa é executado, o loader (gerenciador de carregamento do sistema operacional)
   entende que o binário foi preparado com essas proteções e segue as instruções de segurança impostas
   durante a compilação. Ou seja, o loader já sabe que o programa requer certas medidas de proteção
   durante sua execução, como:
    * Alocar partes do código e dados em locais de memória aleatórios (no caso de PIE);
    * Proteger partes específicas da memória (como com RELRO, marcando-as como somente leitura);
    * Verificar integridade da pilha (usando Stack Canaries para detectar alterações).

##   6.1 Etapas de compilação e endurecimento:

   **6.1.1 Na compilação/linkagem:**
   As flags de endurecimento instruem o compilador/linker a preparar o código com proteções
   adicionais, gerando um binário mais seguro.

   **6.2.2 Na execução:**
   O loader carrega o binário com base nessas proteções, aplicando as técnicas apropriadas
   para garantir a segurança durante a execução.

   Esse processo em conjunto (compilação endurecida + carregamento seguro pelo loader) garante
   que o programa seja menos vulnerável a ataques comuns, como buffer overflows e explorações
   de memória.

##   7.0 Conceito de Endurecimento em Linguagens compiladas: 
   Cada compilador tem um processo fundamental na geração do binário.
   Ele é o reponsável em instruir o processo de compilação a aplicar as camadas de proteção
   com flags específicas. Muito embora dentro do mesmo conceito: "proteger a memória e evitar
   vulnerabilidades".

   **7.1  Exemplo de endurecimento em diferentes linguagens:**
   7.1.1 C/C++ (compiladores como GCC, Clang):
   Flags específicas:
   *_FORTIFY_SOURCE:* Garante verificações extras em funções de manipulação de memória.
   *-fstack-protector:* Insere Stack Canaries para detectar buffer overflows.
   *-fPIE/-pie:* Ativa executáveis independentes de posição (PIE).
   *-Wl,-z,relro e -Wl,-z,now:* Ativa RELRO, tornando partes da memória somente leitura.

   **7.2  Rust:**
   O compilador Rust também aplica muitas dessas técnicas de endurecimento por padrão,
   como proteção da pilha e PIE.
   Rust é conhecido por seu sistema de segurança de memória, que evita muitos problemas comuns
   de C/C++ de forma nativa, através de sua arquitetura de gerenciamento de memória e verificações
   de borrow-checking (garantindo que referências à memória são sempre válidas).

  **7.3. Go (Golang):**
   Em Go, o compilador também aplica proteções como a randomização de memória.
   O runtime de Go tem verificações automáticas de limite de array, evitando buffer overflows.
   O sistema de garbage collection reduz as chances de erros de memória, como double free ou
   memory leaks.

 ** 7.4. Fortran (compilado com GCC):**
   O compilador GCC para Fortran também pode aplicar proteções de pilha e outras flags de 
   endurecimento, semelhantes às de C/C++.

**7.5. Java:**
   Embora Java seja compilado em bytecode e executado em uma máquina virtual (JVM), a JVM
   pode ser configurada com opções de endurecimento. O JIT Compiler (Just-In-Time) que transforma
   o bytecode em código de máquina também pode aplicar proteções, como execução aleatória de
   código e verificações de integridade da memória.

##  Conclusão
   Cada linguagem tem suas próprias práticas e ferramentas para aplicar endurecimento, mas o conceito
   de proteger a memória e dificultar explorações de segurança é amplamente aplicado em todas elas.


Referência:

1. https://tsxvpsbr.dyndns.org/arquivos/UFFS/Compiladores%20-%20Princ%C3%ADpios%20T%C3%A9cnicas%20e%20Ferramentas.pdf
2. https://www.passeidireto.com/arquivo/142133133/processo-de-compilacao
3. https://geovanegriesang.wordpress.com/wp-content/uploads/2015/04/compiladores_04.pdf
4. https://repositorio.ufsc.br/bitstream/handle/123456789/183898/Gals.pdf?sequence=-

