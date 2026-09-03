# 0003 — TypeScript em todo o código

- **Status:** aceito
- **Data:** 2026-09-02
- **Decisores:** Victor Almeida
- **Feature de origem:** transversal

## Contexto

O [ADR 0001](./0001-supabase-como-backend.md) põe o frontend falando direto
com o banco. Isso remove uma camada intermediária — e, com ela, o lugar onde
normalmente se percebe que uma coluna mudou de nome.

O CLI do Supabase gera tipos a partir do schema do banco. Esses tipos só
valem alguma coisa se houver quem os verifique.

A Constituição, no Art. 6, diz que o contrato manda na integração. Um
contrato que ninguém checa é documentação.

## Decisão

**Todo o código do repositório é TypeScript, em modo `strict`.**

- Os tipos do banco são gerados pelo CLI do Supabase e **versionados**.
- Toda migration é seguida da regeneração dos tipos, na mesma entrega.
- O passo de checagem de tipos entra nas checagens obrigatórias do projeto
  (Art. 11): `main` com erro de tipo é `main` quebrado.

## Alternativas consideradas

### TypeScript com `strict` — **escolhida**

- A favor: uma migration que quebra o contrato aparece na compilação, não em
  produção; os tipos gerados do schema tornam o banco a fonte da verdade
  também no frontend; refatoração deixa de ser aposta.
- Contra: passo de build a mais; curva para quem não escreve TS; tipagem de
  biblioteca de terceiro às vezes atrapalha.

### JavaScript — descartada

- A favor: nenhuma cerimônia, nenhum passo de build de tipos.
- Contra: os tipos gerados pelo Supabase viram enfeite; toda checagem de
  contrato passa a depender exclusivamente de teste escrito à mão.
- Motivo do descarte: joga fora a maior vantagem prática do ADR 0001.

### TypeScript sem `strict` — descartada

- A favor: adoção mais suave, menos atrito no começo.
- Contra: `null` e `undefined` continuam invisíveis — que é justamente a
  classe de bug que mais aparece em dado vindo do banco.
- Motivo do descarte: paga o custo do TypeScript sem receber o benefício.

## Consequências

**Boas:**

- Contrato do banco verificado a cada compilação, sem escrever teste para
  isso.
- Editor com autocomplete real sobre o schema.
- Erro de renomeação de coluna aparece em segundos, não em produção.

**Ruins — o preço que aceitamos pagar:**

- Migration e regeneração de tipos viram um par indissociável; esquecer o
  segundo passo produz um erro confuso.
- Alguma fricção com bibliotecas mal tipadas.

**O que passa a ser proibido por causa disto:**

- Editar à mão o arquivo de tipos gerado do schema.
- Usar `any` sem um comentário na linha anterior explicando por quê.
- Silenciar erro de tipo com `@ts-ignore` — quando for inevitável, use
  `@ts-expect-error` com justificativa.
- Abrir PR com erro de tipo, ainda que os testes passem.

## Quando revisitar

Não se prevê revisão. Reverter para JavaScript significaria abandonar a
verificação de contrato descrita no Art. 6.
