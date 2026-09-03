# Bora Estudar 2.0

Projeto conduzido em **Spec Driven Development**: a especificação é a fonte
da verdade, e o código é a consequência dela.

A visão do produto está em [`docs/vision.md`](docs/vision.md). As regras
invioláveis, em [`specs/constitution.md`](specs/constitution.md).

## O fluxo

Quatro comandos, sempre nesta ordem. Cada um só começa quando o anterior
está escrito e revisado.

| Comando | Produz | Responde |
|---|---|---|
| `/specify` | `specs/NNNN-slug/spec.md` | O quê e por quê — sem tecnologia |
| `/plan` | `plan.md`, `research.md`, `data-model.md`, `contracts/` | Como |
| `/tasks` | `tasks.md` | Em que passos, verificáveis |
| `/implement` | `src/`, `tests/` | O código, com teste antes |

Entre `/specify` e `/plan` existe um portão: enquanto houver
`[PRECISA ESCLARECER]` na spec, a feature não avança.

## Estrutura

```
CLAUDE.md              contexto sempre carregado — o mapa curto
.claude/
  commands/            /specify, /plan, /tasks, /implement
  skills/              procedimentos próprios do projeto
  settings.json
specs/
  constitution.md      regras invioláveis
  _template/           esqueleto copiado a cada feature nova
  NNNN-slug/           uma pasta por feature
docs/
  vision.md            produto, personas, escopo macro
  glossary.md          linguagem ubíqua — um conceito, um nome
  adr/                 decisões arquiteturais duradouras
src/                   código de produção
tests/
  contract/            valida specs/*/contracts/
  integration/         fluxos entre componentes
  unit/                unidades isoladas
```

## Começando uma feature

```bash
# 1. descreva a feature — a spec nasce numerada, com as lacunas explícitas
/specify cadastro de usuário com e-mail e senha

# 2. responda os [PRECISA ESCLARECER] e revise a spec
# 3. traduza em arquitetura
/plan

# 4. quebre em passos atômicos
/tasks

# 5. execute — teste antes do código
/implement
```

## Stack

| Camada | Escolha | ADR |
|---|---|---|
| Backend | Supabase — Postgres, Auth, Storage; sem servidor próprio | [0001](docs/adr/0001-supabase-como-backend.md) |
| Autorização | Row Level Security, no banco | [0001](docs/adr/0001-supabase-como-backend.md) |
| Frontend | SPA React com Vite, sem SSR | [0002](docs/adr/0002-spa-react-com-vite.md) |
| Linguagem | TypeScript `strict` | [0003](docs/adr/0003-typescript-em-todo-o-codigo.md) |
| Testes | Vitest · Playwright | [0004](docs/adr/0004-vitest-e-playwright.md) |

Hospedagem, roteamento, CI e gerenciador de pacotes seguem em aberto — cada
um vira ADR quando um requisito escrito exigir.

## Estado atual

Estrutura montada e stack decidida. Nenhuma feature especificada, nenhum
código escrito — o projeto ainda não foi inicializado (sem `package.json`,
sem Vite, sem Supabase local).

Antes da primeira `/specify`, preencha [`docs/vision.md`](docs/vision.md) —
é dele que sai o critério para dizer se uma feature pertence ao produto.

Identificadores em inglês, no código e no banco. Comentários, documentação e
texto de interface em português.
