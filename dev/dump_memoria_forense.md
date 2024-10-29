# Dump de Memória em Equipamentos Apreendidos e Ferramentas Forenses em Sistemas Unix-Like

A prática de dump de memória é uma técnica comum em investigações forenses digitais,
especialmente quando um dispositivo é apreendido pelas autoridades policiais. 
Nesse contexto, várias perguntas surgem sobre o processo, as ferramentas usadas e a
análise posterior dos dados capturados. Este artigo explora esses tópicos de forma coesa,
detalhando a captura e análise de dados voláteis em sistemas Unix-like.

## 1. O Que é um Dump de Memória?

Quando um equipamento é apreendido enquanto ainda está ligado, é comum realizar um
**dump da memória RAM**. A memória RAM armazena dados voláteis, que são perdidos assim
queo dispositivo é desligado. A captura desses dados é essencial para preservar informações
cruciais para a investigação, como processos em execução, chaves de criptografia, dados de
navegação, e até mesmo o conteúdo da área de transferência (clipboard).

O objetivo do dump de memória é capturar o estado do sistema no momento da apreensão,
garantindo que todas as informações temporárias sejam preservadas antes de o sistema
ser desligado, o que tornaria esses dados inacessíveis.

## 2. Quais Regiões da Memória São Capturadas?

Durante um dump de memória, os peritos buscam capturar o máximo possível de dados relevantes,
e isso geralmente significa realizar um **dump completo da RAM**, abrangendo todas as regiões
da memória. Isso inclui:

1. **Memória do processo do usuário**: Dados temporários de programas em execução, como arquivos abertos e sessões de navegação.
2. **Memória do sistema operacional**: Buffers e caches mantidos pelo kernel.
3. **Área de transferência (clipboard)**: Informações copiadas para serem coladas podem ser extremamente relevantes.
4. **Memória de rede**: Pacotes temporariamente armazenados que podem revelar atividades de rede em andamento.

O dump pode ser total ou parcial, dependendo das necessidades da investigação e da situação no
momento da apreensão. No entanto, é comum que os peritos capturem **toda a memória**, já que
muitas informações críticas podem estar espalhadas em diferentes regiões da RAM.

## 3. Ferramentas Usadas em Sistemas Unix-Like para Capturar Memória

Em sistemas baseados em Unix, como Linux e macOS, existem várias ferramentas especializadas que
podem ser usadas para capturar o conteúdo da RAM. Como em uma investigação forense
**não se pode instalar softwares no dispositivo apreendido** (para evitar comprometer o estado
da evidência), as ferramentas são geralmente executadas a partir de dispositivos externos,
como pen-drives.

### 3.1 Algumas das ferramentas mais comuns incluem:

- **LiME (Linux Memory Extractor)**: Uma ferramenta de código aberto que permite capturar a
memória em sistemas Linux. Ela é carregada como um módulo do kernel e pode salvar o conteúdo da
RAM em um arquivo externo sem modificar significativamente o sistema.
 
- **DD (Data Dump)**: Uma ferramenta nativa de Unix-like que pode ser usada para copiar o conteúdo
da memória a partir de dispositivos especiais, como `/dev/mem`. No entanto, o acesso direto a essa
interface é restrito em versões mais recentes do Linux por razões de segurança.

- **Fmem**: Outra ferramenta projetada para capturar a memória física de sistemas Linux, atuando
como um driver de kernel que permite a extração da RAM.

- **AVML (Azure Virtual Memory forensics Library)**: Ferramenta da Microsoft para capturar memória
de sistemas Linux de forma rápida e eficiente.

Essas ferramentas são executadas diretamente do pen-drive ou outra mídia externa, garantindo que
**nenhuma modificação permanente** seja feita no sistema apreendido, preservando a integridade
da evidência.

## 4. Análise Posterior com Ferramentas Robustas como o Volatility

Após a captura do dump de memória, os dados são levados para um **laboratório forense** para
análise detalhada. Ferramentas como o **Volatility** são amplamente utilizadas para analisar
dumps de memória devido à sua flexibilidade e capacidade de extrair informações valiosas de
diferentes sistemas operacionais.
O **Volatility** é uma ferramenta de análise de memória volátil que permite dissecar o
conteúdo do dump em busca de:
- **Processos em execução** no momento da captura.
- **Conexões de rede** ativas.
- **Chaves de criptografia** temporárias.
- **Dados do usuário**, como documentos abertos e navegação na internet.
- **Dados maliciosos**, como malware ou exploits ativos.

A vantagem do Volatility é que ele é **não intrusivo** — ele não precisa ser instalado no sistema
original e pode ser executado em uma estação de análise separada. Isso garante que a integridade
do sistema apreendido seja mantida enquanto uma análise profunda é realizada.

## 5. Por Que Usar Ferramentas Externas para Captura e Análise?

A principal razão para usar **ferramentas externas** para capturar a memória e **ferramentas robustas**
para análise posterior é evitar qualquer alteração no dispositivo apreendido. Em uma investigação
forense, é fundamental preservar a integridade dos dados, pois qualquer modificação no sistema original
pode comprometer a validade das evidências.

1. **Captura no local**: Durante a apreensão, os peritos utilizam **dispositivos externos**, como
pen-drives, contendo ferramentas especializadas para capturar a memória sem modificar o sistema.
Isso garante que a evidência permaneça intacta.

2. **Análise em laboratório**: Uma vez que os dados foram capturados, eles são levados para um
laboratório forense, onde ferramentas como o Volatility são usadas para uma análise mais
aprofundada. O ambiente controlado do laboratório permite uma investigação detalhada, sem
pressões de tempo ou risco de comprometimento das evidências.

## Conclusão

O dump de memória é uma técnica essencial em investigações forenses, especialmente em sistemas
Unix-like, onde os dados voláteis podem conter informações críticas para o caso. Ferramentas como
**LiME**, **Fmem**, e **DD** são usadas para capturar a RAM de forma segura e eficiente, enquanto
o **Volatility** desempenha um papel central na análise posterior em laboratório.

O processo de apreensão e análise segue uma abordagem cuidadosa para garantir que os dados sejam
preservados e analisados sem comprometer o sistema original. Isso é fundamental para que as
provas obtidas sejam aceitas em processos judiciais e possam ser usadas para construir um caso
sólido.


Referência:

1. https://www.varonis.com/pt-br/blog/entenda-o-que-e-a-pericia-de-memoria-para-casos-de-resposta-a-incidentes
2. https://repositorio.ucb.br:9443/jspui/bitstream/123456789/11018/1/DiegoBatistaMunizTCCLatoSensu2016.pdf
3. https://mundonet.quora.com/O-que-%C3%A9-um-dump-de-mem%C3%B3ria-Especialmente-em-C
