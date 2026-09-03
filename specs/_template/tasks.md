# Tasks — [Nome da feature]

- **Spec:** [`spec.md`](./spec.md) · **Plano:** [`plan.md`](./plan.md)
- **Status:** rascunho | aprovado | em execução | concluído

> Toda task é atômica, tem arquivo previsto e uma forma objetiva de dizer
> "pronto" (Art. 9). A ordem respeita teste antes do código (Art. 5).

## Legenda

- `[ ]` pendente · `[x]` concluída
- `[P]` pode rodar em paralelo com as outras `[P]` do mesmo bloco
- **Depende de:** tasks que precisam estar concluídas antes desta

## Bloco 1 — Preparação

- [ ] **T001** — [Preparar estrutura / dependências]
  - Arquivos: `[caminho]`
  - Pronto quando: `[comando ou verificação objetiva]`
  - Depende de: —

## Bloco 2 — Contratos e testes que falham

Nenhuma implementação neste bloco. Ao final, os testes existem e **falham**.

- [ ] **T010 [P]** — Escrever contrato de [fronteira]
  - Arquivos: `specs/NNNN-slug/contracts/[...]`
  - Pronto quando: contrato descreve todos os campos do `data-model.md`
  - Depende de: T001

- [ ] **T011 [P]** — Teste de contrato de [fronteira]
  - Arquivos: `tests/contract/[...]`
  - Pronto quando: o teste roda e **falha** pela ausência da implementação
  - Depende de: T010

- [ ] **T012 [P]** — Teste de integração do cenário 1 da spec
  - Arquivos: `tests/integration/[...]`
  - Pronto quando: o teste roda e **falha**
  - Depende de: T001

## Bloco 3 — Implementação

Cada task aqui faz um teste do Bloco 2 passar. Nada além disso.

- [ ] **T020** — Implementar [unidade]
  - Arquivos: `src/[...]`
  - Pronto quando: T011 passa
  - Requisito: RF-01
  - Depende de: T011

- [ ] **T021** — Implementar [unidade]
  - Arquivos: `src/[...]`
  - Pronto quando: T012 passa
  - Requisito: RF-02
  - Depende de: T012

## Bloco 4 — Fechamento

- [ ] **T090** — Rodar a suíte completa e as checagens do projeto
  - Pronto quando: tudo verde, `main` continua íntegro (Art. 11)
  - Depende de: todas as anteriores

- [ ] **T091** — Atualizar `docs/glossary.md` com os termos novos
  - Pronto quando: todo termo de domínio da spec está no glossário (Art. 7)

- [ ] **T092** — Marcar a spec como `implementada`
  - Arquivos: `specs/NNNN-slug/spec.md`

## Cobertura dos requisitos

Nenhum requisito da spec fica sem task.

| Requisito | Tasks |
|---|---|
| RF-01 | T011, T020 |
| RF-02 | T012, T021 |
