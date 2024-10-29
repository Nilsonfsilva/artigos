
# Licenças GPLv2, GPLv3 e AGPL: Entendendo as Diferenças e a Polêmica do ASP Loophole

As licenças **GPL** (GNU General Public License) são amplamente conhecidas no 
mundo do software livre e foram criadas pela Free Software Foundation (**FSF**) 
para garantir que o software possa ser usado, estudado, modificado e 
redistribuído de forma livre. Com o tempo, novas versões surgiram para atender 
a desafios específicos, como o uso de software em servidores e na nuvem. Neste 
artigo, exploramos as diferenças entre as versões **GPLv2**, **GPLv3** e 
**AGPL** e entendemos a polêmica do *ASP loophole*.

## 1. Entendendo a GPLv2

A **GPLv2** foi criada para assegurar que o software livre permanecesse livre em 
todas as suas versões e redistribuições. Ela define que qualquer modificação 
feita em um software sob GPLv2 deve ser disponibilizada com o mesmo tipo de 
licença, desde que o software seja distribuído.

**Principais características da GPLv2:**

- **Compartilhamento obrigatório do código:** Qualquer pessoa que distribua um 
  software modificado sob GPLv2 deve fornecer o código-fonte dessas modificações.
- **Uso em servidores:** Se o software é utilizado apenas internamente, sem 
  distribuição, não é necessário compartilhar o código-fonte modificado.

Essa característica gera a “brecha” conhecida como **ASP loophole**, abordada a 
seguir.

## 2. O que é o ASP Loophole?

O **ASP loophole** (*Application Service Provider loophole*) refere-se à lacuna 
da GPLv2, que permite o uso de software em servidores sem a necessidade de 
distribuir o código-fonte modificado, desde que o software não seja distribuído 
diretamente para terceiros. Com o crescimento da internet e do modelo **SaaS** 
(*Software as a Service*), empresas passaram a usar software GPLv2 modificado em 
servidores, oferecendo serviços aos usuários finais sem compartilhar o código.

## 3. A GPLv3: Fechando Lacunas, mas Ainda com Limitações

Para resolver limitações da GPLv2, a Free Software Foundation lançou a **GPLv3**, 
que trouxe proteções contra **tivoização** e problemas com **patentes**.

**O que é Tivoização?**  
A tivoização ocorre quando um dispositivo usa software livre, mas bloqueia 
modificações, impedindo que o usuário altere o software. A prática ficou 
conhecida pelo uso em dispositivos da empresa TiVo. A GPLv3 combate a 
tivoização, exigindo que dispositivos que utilizam software GPLv3 permitam 
modificações pelo usuário.

**Principais características da GPLv3:**

- **Proteção contra tivoização:** Dispositivos com software GPLv3 não podem 
  bloquear modificações, assegurando o direito do usuário de alterar o software.
- **Restrições de patentes:** A GPLv3 inclui cláusulas que evitam processos por 
  violação de patentes relacionadas ao software.
- **Distribuição:** Mantém a exigência de compartilhamento do código-fonte quando 
  distribuído a terceiros.

Embora a GPLv3 resolva várias questões, ainda permite o ASP loophole, 
possibilitando o uso e modificação do software em servidores sem a obrigação de 
compartilhar as modificações.

## 4. A AGPL: Fechando o ASP Loophole

Para resolver o ASP loophole, a FSF criou a **Affero General Public License** 
(**AGPL**), que garante que, mesmo quando o software é utilizado em servidores, 
o código-fonte modificado seja compartilhado com os usuários.

**Principais características da AGPL:**

- **Distribuição em rede:** Exige que qualquer modificação seja compartilhada 
  com os usuários, mesmo se o software estiver sendo oferecido apenas como 
  serviço online.
- **Objetivo:** Garante que usuários que interagem com o software na rede tenham 
  acesso ao código-fonte modificado, promovendo transparência.

A **AGPL** fecha a brecha do ASP loophole, impondo que qualquer modificação usada 
para oferecer serviços via rede seja compartilhada.

## 5. Resumo das Diferenças entre GPLv3 e AGPL

## Conclusão

A escolha entre **GPLv2**, **GPLv3** e **AGPL** depende dos objetivos do 
desenvolvedor e das necessidades dos usuários. A **GPLv2** ainda é popular e 
oferece flexibilidade para uso em servidores sem compartilhamento de 
modificações. A **GPLv3** trouxe avanços, protegendo contra tivoização e 
problemas de patentes, mas não cobre o uso em servidores. A **AGPL** é a mais 
restritiva, garantindo que modificações em serviços de rede sejam compartilhadas, 
promovendo transparência para os usuários.

Compreender essas licenças permite que desenvolvedores e empresas façam escolhas 
conscientes sobre o tipo de licença que melhor atende aos seus objetivos de 
compartilhamento e proteção do software livre.
