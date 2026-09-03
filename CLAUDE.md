# Bora Estudar 2.0

Projeto desenvolvido em **Spec Driven Development (SDD)**: a especificação é a
fonte da verdade; o código é a consequência dela.

## Regra de ouro

**Nenhuma linha de código sem uma spec aprovada.** Se a tarefa não tem spec,
o primeiro passo é `/specify` — nunca abrir o editor direto.

## O ciclo

```
/specify  →  specs/NNNN-slug/spec.md        O QUÊ e POR QUÊ (sem tecnologia)
/plan     →  plan.md + research.md          COMO (arquitetura, stack, decisões)
             + data-model.md + contracts/
/tasks    →  tasks.md                       passos atômicos e verificáveis
/implement→  src/ + tests/                  executa as tasks, em ordem, com TDD
```

Cada etapa só começa quando a anterior está escrita e revisada. Pular etapa é
o erro mais caro do fluxo.

## Onde as coisas moram

| Caminho | O que é |
|---|---|
| `specs/constitution.md` | Regras invioláveis. **Leia antes de planejar.** |
| `specs/NNNN-slug/` | Uma pasta por feature, numerada em sequência |
| `specs/_template/` | Esqueleto copiado a cada feature nova |
| `docs/vision.md` | Produto, personas, escopo macro |
| `docs/glossary.md` | Linguagem ubíqua — os termos do domínio |
| `docs/adr/` | Decisões arquiteturais duradouras, uma por arquivo |
| `src/` | Código de produção |
| `tests/contract/` | Valida `specs/*/contracts/` |
| `tests/integration/` | Fluxos entre componentes |
| `tests/unit/` | Unidades isoladas |

## Stack

Decidida nos ADRs [0001–0004](docs/adr/). Detalhes e proibições lá; aqui, o
essencial:

| Camada | Escolha |
|---|---|
| Backend | Supabase — Postgres, Auth, Storage. **Sem servidor próprio.** |
| Autorização | Row Level Security, no banco |
| Frontend | SPA React com Vite. Sem SSR, sem meta-framework |
| Linguagem | TypeScript `strict`; tipos do banco gerados e versionados |
| Testes | Vitest (unit, integração, contrato) · Playwright (e2e) |

Quatro coisas que a stack proíbe: `service_role` no cliente, autorização só
na interface, mudança de schema fora de migration, e tabela sem política de
RLS.

Hospedagem, roteamento, CI e gerenciador de pacotes **ainda não foram
decididos** — não presuma; abra ADR.

## Convenções

- Identificadores (código, banco, arquivos) em **inglês**.
- Comentários, documentação, specs e texto de interface em **português**.
- Termos de domínio: sempre os do `docs/glossary.md`, nunca sinônimos.
- Ambiguidade numa spec vira marcador `[PRECISA ESCLARECER: pergunta]` —
  nunca um palpite silencioso.
