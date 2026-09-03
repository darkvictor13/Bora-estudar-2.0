# 0004 — Vitest e Playwright como ferramentas de teste

- **Status:** aceito
- **Data:** 2026-09-02
- **Decisores:** Victor Almeida
- **Feature de origem:** transversal

## Contexto

O Art. 5 da Constituição exige teste antes do código, e o Art. 6 exige teste
de contrato para toda fronteira. As pastas `tests/contract`,
`tests/integration` e `tests/unit` existem desde o primeiro dia.

Isso deixa de ser detalhe de implementação: sem ferramenta de teste, o fluxo
inteiro trava na primeira feature.

Duas fronteiras precisam de cobertura, e são de naturezas diferentes: a API
gerada pelo Supabase, incluindo as políticas de RLS (ADR 0001), e a interface
da SPA (ADR 0002).

## Decisão

- **Vitest** para `tests/unit`, `tests/integration` e `tests/contract`.
- **Playwright** para o fluxo ponta a ponta, num navegador de verdade.
- Os testes de contrato e de integração rodam contra o **Supabase local**,
  não contra dublês. Política de RLS só se prova contra o banco.
- **Toda tabela tem teste de RLS**: o que o dono pode ver, e o que outra
  pessoa **não** pode.

## Alternativas consideradas

### Vitest + Playwright — **escolhida**

- A favor: o Vitest compartilha a configuração do Vite (ADR 0002) — um
  arquivo de config, um resolvedor de módulos, sem duplicação; entende
  TypeScript sem transpiler extra (ADR 0003); o Playwright cobre a camada de
  interface, onde os bugs que escapam da unidade se escondem.
- Contra: duas ferramentas para conhecer; o Playwright pesa na integração
  contínua e precisa de navegador instalado.

### Jest + Testing Library — descartada

- A favor: ecossistema maduro e amplamente conhecido.
- Contra: exige configuração própria fora do Vite, com transformação de
  TypeScript à parte; suíte mais lenta.
- Motivo do descarte: paga configuração duplicada para chegar ao mesmo
  lugar.

### Só Vitest, sem navegador — descartada

- A favor: uma ferramenta a menos.
- Contra: deixa a camada de interface e de fluxo sem cobertura — exatamente
  onde os cenários da spec vivem.
- Motivo do descarte: o Art. 4 exige critério de aceite observável; boa parte
  deles só é observável na tela.

### Cypress — descartada

- A favor: boa experiência de desenvolvimento.
- Contra: mais lento, e o modelo de execução dentro do navegador complica
  cenários com várias sessões — como aluno e professor ao mesmo tempo.
- Motivo do descarte: o Playwright resolve melhor o caso multiusuário, que
  este produto vai ter.

## Consequências

**Boas:**

- Uma configuração só entre build e teste unitário.
- Teste de contrato contra banco real prova a RLS, não a nossa opinião sobre
  ela.
- Cenário "Dado que / Quando / Então" da spec tem tradução direta em teste.

**Ruins — o preço que aceitamos pagar:**

- O ambiente de teste depende do Supabase local em execução — e, portanto,
  de Docker.
- A suíte ponta a ponta é a mais lenta e a mais frágil do repositório;
  precisa de cuidado para não virar ruído.

**O que passa a ser proibido por causa disto:**

- Dar task de implementação como concluída sem um teste que falhou antes
  dela (Art. 5).
- Substituir teste de contrato por teste ponta a ponta: o e2e cobre fluxo,
  não formato de fronteira.
- Dublar o banco em teste de contrato ou de RLS.
- Tabela nova sem teste de política de acesso.

## Quando revisitar

- Se a suíte ponta a ponta ficar lenta ou instável a ponto de as pessoas
  passarem a ignorá-la.
- Se o Supabase local deixar de ser viável como dependência de teste.
