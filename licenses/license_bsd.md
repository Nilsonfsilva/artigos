
# Licença BSD: Explicação Completa e Diferenças entre as Versões de 2 e 3 Cláusulas

A licença BSD (Berkeley Software Distribution) é uma licença de software
permissiva, o que significa que permite o uso, modificação e redistribuição de
software com poucas restrições. Ela é amplamente utilizada em projetos de
código aberto e software livre, e, devido à sua flexibilidade, também pode
ser integrada em softwares proprietários. Existem diferentes variantes da
licença BSD, sendo as mais comuns a BSD de 2 cláusulas e a BSD de 3 cláusulas.
Neste artigo, explicaremos cada uma dessas licenças, suas diferenças e como
aplicá-las, com exemplos para cada situação.

---

## 1. Visão Geral da Licença BSD

A licença BSD foi criada para facilitar a distribuição de software desenvolvido
pela Universidade da Califórnia em Berkeley e é reconhecida pela sua
simplicidade. Ela permite que qualquer pessoa use o código licenciado de
forma bastante livre, inclusive para fins comerciais, exigindo apenas que o
aviso de copyright original e o texto da licença sejam mantidos em
redistribuições.

Essa licença não impõe restrições de copyleft, o que significa que o
software licenciado sob BSD pode ser integrado a qualquer tipo de software,
incluindo software proprietário. Isso a torna uma das licenças mais
permissivas e uma escolha popular para projetos de código aberto.

---

## 2. BSD de 3 Cláusulas: Explicação e Exemplo

A licença BSD de 3 cláusulas, também conhecida como "New BSD License" ou
"BSD Revisada", possui três cláusulas principais:

- **Cláusula de Copyright**: Especifica que o código pode ser usado e
  distribuído desde que o aviso de copyright e o texto da licença estejam
  presentes em todas as cópias e redistribuições, seja em formato original ou
  modificado.

- **Cláusula de Redistribuição**: Estabelece que, se o código for modificado
  e redistribuído, o aviso original deve ser incluído e atribuído ao autor
  original.

- **Cláusula de Endosso**: Impede que o nome do autor original ou da
  organização (por exemplo, a Universidade da Califórnia) seja utilizado para
  promover produtos derivados do software sem permissão explícita. Essa
  cláusula protege a reputação do autor ou da instituição original contra
  associações indesejadas.

**Exemplo de Aplicação da BSD de 3 Cláusulas**:

Imagine que você desenvolva um software chamado `MeuSoftware` baseado em
código sob licença BSD de 3 cláusulas. Ao redistribuir `MeuSoftware`
(modificado ou não), você precisaria incluir o seguinte aviso:

```plaintext
Copyright © [Ano] [Nome do autor ou instituição]
Todos os direitos reservados.

Redistribuição e uso nas formas de código-fonte e binário, com ou sem
modificações, são permitidos desde que as seguintes condições sejam
atendidas:
1. O aviso de copyright original e este aviso de permissão devem ser
   mantidos em todas as cópias ou redistribuições.
2. A documentação incluída deve reconhecer o autor original.
3. O nome do autor ou da instituição original não pode ser usado para
   promover produtos derivados sem autorização prévia.
```

Essa estrutura garante que os direitos de uso sejam amplos, mas respeita a
autoria original e previne associações indevidas com o autor original.

---

## 3. BSD de 2 Cláusulas: Explicação e Exemplo

A licença BSD de 2 cláusulas, também chamada de "Simplified BSD License" ou
"FreeBSD License", é uma versão simplificada da licença de 3 cláusulas, onde
a cláusula de endosso é removida. A licença de 2 cláusulas contém apenas:

- **Cláusula de Copyright**: Igual à licença de 3 cláusulas, que exige que o
  aviso de copyright e o texto da licença estejam presentes em todas as
  cópias redistribuídas.

- **Cláusula de Redistribuição**: Exige que a licença BSD original seja
  incluída em qualquer redistribuição, garantindo que o autor original seja
  mencionado.

A remoção da cláusula de endosso torna a licença BSD de 2 cláusulas mais
permissiva e simples, sendo ideal para projetos que não têm preocupações com
a associação de nomes de seus autores.

**Exemplo de Aplicação da BSD de 2 Cláusulas**:

No exemplo do `MeuSoftware`, se o código fosse licenciado sob a BSD de 2
cláusulas, você precisaria apenas garantir que o aviso de copyright e o texto
da licença fossem mantidos, sem restrições sobre o uso do nome do autor para
promoção.

```plaintext
Copyright © [Ano] [Nome do autor ou instituição]
Todos os direitos reservados.

Redistribuição e uso nas formas de código-fonte e binário, com ou sem
modificações, são permitidos desde que as seguintes condições sejam
atendidas:
1. O aviso de copyright original e este aviso de permissão devem ser
   mantidos em todas as cópias ou redistribuições.
```

---

## 4. Diferença Principal entre BSD de 2 Cláusulas e BSD de 3 Cláusulas

A principal diferença entre essas duas versões é a **Cláusula de Endosso** na
licença BSD de 3 cláusulas. Essa cláusula adiciona uma camada extra de
proteção à imagem do autor ou da instituição, impedindo que o nome deles
seja usado para promover derivados do software sem autorização.

| Licença BSD de 2 Cláusulas  | Licença BSD de 3 Cláusulas      |
|-----------------------------|---------------------------------|
| Simples e direta            | Inclui cláusula de endosso      |
| Menos restritiva            | Protege a imagem do autor       |
| Ideal para projetos abertos e proprietários | Requer autorização para uso do nome original em promoção |

---

## 5. Redistribuição de Código Derivado: Posso Usar Outra Licença?

Sim, uma das características permissivas da licença BSD é que ela permite a
redistribuição de código derivado com qualquer licença, desde que os
requisitos da licença original sejam cumpridos.

### Como Funciona?

1. **Escolha da Licença para o Código Derivado**: Quando você cria uma
   versão derivada do código licenciado sob BSD, você pode escolher
   licenciá-lo sob BSD ou sob outra licença, inclusive uma licença
   proprietária.

2. **Requisitos da Licença Original**: Independentemente de qual licença
   você escolher para o código derivado, a licença BSD exige que o texto da
   licença original e os avisos de copyright estejam incluídos na
   redistribuição. Isso garante que o autor original receba o devido crédito.

**Exemplo Prático**

Se você cria um software derivado, chamado `MeuSoftwarePro`, baseado em
`MeuSoftware` licenciado sob BSD, você pode:
- Redistribuir `MeuSoftwarePro` sob uma licença proprietária, mantendo o
  aviso original da BSD e o copyright.
- Ou, redistribuir `MeuSoftwarePro` sob uma licença aberta (como MIT), também
  mantendo o aviso original da BSD.

### Resumo

A licença BSD oferece uma grande flexibilidade para uso e redistribuição de
software, com duas variações principais:

- **BSD de 2 cláusulas**: Simples e permissiva, exigindo apenas que o aviso
  de copyright e o texto da licença original estejam presentes.
- **BSD de 3 cláusulas**: Igual à de 2 cláusulas, mas com uma cláusula
  adicional de endosso que protege o nome do autor contra associações
  indesejadas.

Essa flexibilidade permite que desenvolvedores usem o código BSD em uma
ampla variedade de projetos, incluindo comerciais, desde que respeitem as
poucas exigências da licença.
