 # Entendendo Makefile, Makefile.in, configure e configure.ac no Desenvolvimento de Software

No desenvolvimento de software, especialmente em projetos escritos em C ou utilizando scripts Shell,
encontramos arquivos fundamentais para a compilação e configuração do programa: Makefile, Makefile.in,
configure, e configure.ac. Cada um desses arquivos tem um papel específico no processo de adaptação e
construção do software em diferentes ambientes. Vamos explorar cada um deles de maneira didática.

## 1. Makefile

O Makefile é essencial para o uso da ferramenta `make`. Ele define as regras de compilação, especificando
como os arquivos fonte devem ser compilados, quais diretórios serão usados para instalação e quais são os
parâmetros do compilador.

### Uso Simples do Makefile

Em projetos simples, onde não é necessário ajustar o código ao ambiente, o Makefile pode ser usado 
diretamente. Basta o usuário rodar o comando `make` para compilar o projeto.

#### Exemplo de Makefile:

```makefile
CC = gcc
CFLAGS = -Wall -O2
TARGET = meu_programa

all:
    $(CC) $(CFLAGS) -o \$(TARGET) main.c


2. Makefile.in e configure

Quando um projeto precisa se adaptar ao ambiente em que será compilado, os arquivos Makefile.in
e configure entram em cena. Função do Makefile.in e Configure

  Makefile.in: Um modelo do Makefile, contendo variáveis e espaços reservados que serão
  preenchidos automaticamente.

  Configure: Um script gerado pela ferramenta Autoconf, que processa o Makefile.in para
   criar um Makefile final adaptado ao ambiente.

O usuário deve rodar o script configure antes de usar o make, garantindo que o Makefile gerado
esteja configurado corretamente para o sistema em que o programa será compilado.
Passos:

    Executar ./configure.
    Depois, rodar make.


3. configure.ac (ou configure.in)

O arquivo configure.ac é usado durante o desenvolvimento do projeto e define as verificações que
o script configure irá fazer. Ele é processado pelo Autoconf para gerar o script configure.
Função do Configure.ac

    * Define as condições e parâmetros que serão testados pelo configure.

    * Permite verificar a presença de bibliotecas, funções e outros recursos necessários.

Processo:

    1. O desenvolvedor escreve o configure.ac.
    2. Usa o comando autoconf para gerar o configure.
    3. O configure é executado para gerar o Makefile adaptado.


4. config.h

O config.h é um arquivo de cabeçalho gerado automaticamente pelo configure. Ele contém definições
de macros baseadas nos testes realizados no sistema, ajudando o código a se adaptar ao ambiente.
Exemplo de Uso no Código C:

#include "config.h"

#ifdef HAVE_LIBM
#include <math.h>
#endif

int main() {
#ifdef HAVE_SQRT
    printf("sqrt está disponível.\n");
#else
    printf("sqrt não está disponível.\n");
#endif
    return 0;
}

Resumo dos Cenários
Apenas o Makefile:

    Projeto simples, sem necessidade de ajustes.
    Usuário roda make diretamente.

Makefile.in + configure:

    Projeto precisa de ajustes automáticos.
    Usuário roda ./configure e depois make.

configure.ac → autoconf → configure → Makefile.in → Makefile:

    Desenvolvedor usa configure.ac para gerar o configure.
    Usuário executa o configure para obter o Makefile final.

Parâmetros Específicos nos Arquivos

Os arquivos Makefile.in e configure.ac precisam ser adaptados às necessidades de cada projeto. 
Eles contêm parâmetros que variam conforme as dependências, diretórios de instalação e
configurações específicas do sistema.

    1. Makefile.in: Usa variáveis como @CC@, @CFLAGS@ que serão substituídas pelo configure.

    2. configure.ac: Usa macros do Autoconf como AC_INIT, AC_PROG_CC, entre outras.


Processo Completo de Compilação com configure.ac → autoconf → configure → Makefile.in → Makefile

Para compilar um projeto que segue o fluxo configure.ac → autoconf → configure → Makefile.in → Makefile,
o processo envolve várias etapas, desde a preparação dos scripts de configuração até a compilação
final do software. 

Vamos detalhar cada passo:

1. configure.ac → autoconf → configure

    configure.ac: Este arquivo contém as macros do Autoconf que especificam os testes e configurações
                  necessários para o projeto. Ele define, por exemplo, o nome do pacote, versão, e os
                  testes para bibliotecas e funções específicas.

    autoconf: É a ferramenta que lê o configure.ac e gera o script configure. O comando é:

    autoconf  (Este comando cria um arquivo configure a partir do configure.ac.)



2. configure → Makefile.in → Makefile

    configure: Este script é executado pelo usuário para configurar o projeto de acordo com o ambiente
               do sistema. Ele realiza testes no sistema (como verificar se certas bibliotecas ou
               cabeçalhos estão presentes) e usa o Makefile.in para gerar o Makefile final. O comando é:

    ./configure

    Durante a execução, o configure substitui placeholders no Makefile.in com os valores apropriados
     para o ambiente do usuário e cria o Makefile.



3. Makefile e Compilação

    Makefile: Depois de gerado pelo configure, o Makefile contém todas as instruções necessárias
              para compilar o software. O usuário executa o make para iniciar o processo de 
              compilação, conforme definido no Makefile.

    make   (Esse comando compila os arquivos fonte e cria os binários do programa.)



4.Etapas Completas:

    a) Geração do configure:

        Criar o configure a partir do configure.ac com autoconf:
        autoconf


    b) Configuração do Ambiente:

    Executar o script configure para adaptar o Makefile.in ao ambiente:
    ./configure


    c) Compilação:

    Rodar make para compilar o projeto usando o Makefile gerado:

    make

(Opcional) Instalação:

    Instalar os binários no sistema (geralmente como superusuário):

        make install


Conclusão

O uso de Makefile, Makefile.in, configure, e configure.ac é uma prática que garante a
flexibilidade e portabilidade dos projetos de software. Dependendo da complexidade e 
dos requisitos do ambiente de execução, o desenvolvedor pode escolher a melhor combinação
desses arquivos para facilitar a instalação e compilação do programa.

Entender o papel de cada um desses arquivos permite criar sistemas mais robustos e adaptáveis,
garantindo que o software funcione corretamente em uma ampla gama de sistemas e ambientes.
