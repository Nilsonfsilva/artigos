
# O papel do loader na execução de programas

Aqui está uma visão reorganizada e detalhada do funcionamento do **loader** no 
processo de carregamento de um programa na memória:

### O que acontece quando clicamos para executar um programa?

Quando você clica em um ícone ou executa um comando para iniciar um programa, 
uma série de eventos são acionados no sistema. Vamos detalhar o que acontece 
nesse processo, desde o clique até o carregamento na memória e a execução do 
programa.

#### 1. Quem chama o loader?
O **mouse**, por si só, não tem a capacidade de chamar o loader ou realizar 
qualquer operação de sistema. Ele apenas gera um **evento de entrada** (um 
clique) que é capturado pelo **sistema operacional**.

Esse evento é enviado ao sistema, que interpreta o clique como uma solicitação 
para executar um programa. O **sistema operacional** então inicia o processo de 
execução do programa. É nesse ponto que o **loader**, uma parte crucial do 
sistema operacional, entra em ação. O loader é o responsável por carregar o 
programa na memória para que ele possa ser executado pelo processador.

#### 2. Como o loader carrega o programa na memória?
O **loader** não carrega todo o programa na RAM (memória física) de uma vez. Isso 
seria ineficiente, especialmente para programas grandes. Em vez disso, o loader 
utiliza a **memória virtual**, que é uma abstração fornecida pelo sistema 
operacional.

##### Memória Virtual vs. Memória Física
- **Memória virtual**: Essa é uma área de memória que dá a impressão ao programa 
de que ele tem acesso a um grande espaço contínuo de memória. Cada programa tem 
seu próprio espaço de memória virtual, independente de quanta RAM física está 
disponível no sistema. A memória virtual é gerenciada pelo sistema operacional e 
geralmente está localizada no disco rígido (HD, SSD) quando não há RAM 
suficiente.

- **Memória física (RAM)**: Esta é a memória de alta velocidade onde os dados 
realmente são processados pelo processador. Como a RAM é limitada, nem sempre é 
possível carregar todo o programa na memória física de uma vez.

##### Processo de Carregamento
Quando o loader recebe a solicitação para carregar um programa, ele segue os 
seguintes passos:
1. **Mapeamento na Memória Virtual**: O loader mapeia todo o programa na memória 
virtual. Isso significa que o sistema operacional reserva um espaço de 
endereçamento na memória virtual para o programa. Ele organiza o programa em 
partes chamadas de **páginas**, que podem ser carregadas na RAM conforme 
necessário. Essas páginas são atribuídas a **offsets** (deslocamentos) que dão a 
impressão de que o programa está ocupando toda a memória de forma contínua, mesmo 
que fisicamente ele não esteja todo carregado.

2. **Carregamento na Memória Física (RAM)**: Inicialmente, o loader carrega 
apenas as partes essenciais do programa que são necessárias para iniciar sua 
execução. Isso pode incluir o código principal do programa e qualquer recurso 
inicial obrigatório. As outras partes do programa permanecem na memória virtual, 
no disco rígido.

#### 3. Como o loader sabe o que carregar?
O **loader** não precisa calcular o tamanho de todo o programa para determinar o 
que carregar. Em vez disso, ele segue instruções e metadados fornecidos no 
**arquivo executável** do programa. Esses dados informam ao loader quais partes 
são necessárias para a execução inicial.

Se o programa precisar de mais recursos ao longo do tempo (como abrir novos 
arquivos ou executar novas funcionalidades), o sistema operacional e o loader 
podem buscar e carregar as partes relevantes na memória física sob demanda. Isso 
é feito por um processo conhecido como **paginação sob demanda**.

#### 4. Quem gerencia a memória virtual?
A criação e o gerenciamento da **memória virtual** são tarefas do **sistema 
operacional**, e não diretamente do loader. O sistema operacional define como a 
memória é distribuída, cria o espaço de endereçamento virtual, e decide quais 
partes do programa (quais páginas) serão carregadas na RAM de acordo com as 
necessidades.

O loader atua em coordenação com o sistema operacional para carregar o programa 
inicialmente na memória virtual e, conforme necessário, mover partes para a 
memória física. Quando uma parte do programa não está na RAM mas é solicitada, o 
sistema operacional faz a **paginação** para trazê-la da memória virtual (disco) 
para a RAM, permitindo sua execução.

### Fluxo de Carregamento de um Programa

1. **Clique no programa**: O usuário clica em um ícone ou executa um comando. O 
sistema operacional detecta esse evento.

2. **Início do carregamento**: O sistema operacional invoca o loader, que começa 
a preparar o programa para a execução, mapeando-o na memória virtual.

3. **Memória Virtual**: Todo o programa é mapeado na memória virtual, dividindo-o 
em várias páginas. O sistema operacional cria esse mapeamento para que o programa 
tenha acesso ao seu espaço de memória, mesmo que não todo o programa esteja ainda 
na memória física.

4. **Carregamento Inicial na RAM**: Apenas as partes essenciais do programa são 
carregadas inicialmente na memória física (RAM). As outras partes permanecem na 
memória virtual.

5. **Paginação Sob Demanda**: Conforme o usuário interage com o programa e 
solicita novos recursos (como abrir novos arquivos ou utilizar funcionalidades 
adicionais), o sistema operacional carrega as partes necessárias na RAM a partir 
da memória virtual.

6. **Execução**: O programa começa a ser executado e interage com o processador. 
À medida que novas funções são requisitadas e dados são processados, as partes do 
programa são carregadas da memória virtual para a RAM conforme necessário.

### Conclusão
O processo de carregamento de um programa envolve uma série de componentes 
trabalhando juntos, desde o clique até a execução. O **loader** e o **sistema 
operacional** têm papéis fundamentais no gerenciamento da memória, garantindo que 
o programa possa funcionar com eficiência, utilizando a **memória virtual** para 
garantir que todo o programa seja acessível, e a **memória física** (RAM) para 
carregar e executar apenas as partes essenciais no momento. Essa gestão 
inteligente permite que programas grandes funcionem mesmo em sistemas com RAM 
limitada, otimizando o uso dos recursos de hardware.

Referência:

1. https://www.dcce.ibilce.unesp.br/~aleardo/cursos/fsc/cap12.php
2. https://www.inf.unioeste.br/~marcio/SO/Aula8MemoriaVirtual.pdf
3. https://blog.4linux.com.br/conhecendo-o-kernel-linux-pelo-proc-parte-4-comportamentos-da-memoria-virtual/
4. https://escolalbk.com.br/glossario/o-que-e-memoria-virtual/

