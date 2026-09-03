# Constituição do Projeto

Regras invioláveis do Bora Estudar 2.0. Valem para pessoas e para agentes.

Um plano que viole um artigo daqui **não é aprovado** — ou o plano muda, ou a
constituição é emendada primeiro, explicitamente, com justificativa registrada
no histórico deste arquivo.

Versão: 1.1.0 · Ratificada em: 2026-09-02 · Última emenda: 2026-09-02

---

## Art. 1 — A spec é a fonte da verdade

Toda mudança de comportamento nasce em `specs/NNNN-slug/spec.md`. Código sem
spec correspondente é dívida, não entrega.

Quando código e spec divergem, a spec está certa até que alguém a corrija de
propósito. Corrigir a spec é uma alteração legítima; ignorá-la não é.

## Art. 2 — Spec não fala de tecnologia

`spec.md` descreve **o quê** e **por quê**, na linguagem do domínio. Nomes de
framework, banco, biblioteca, formato de arquivo ou nome de classe só aparecem
a partir do `plan.md`.

Teste prático: se a spec continuaria válida caso o produto fosse reescrito em
outra linguagem, ela está no nível certo.

## Art. 3 — Ambiguidade é explícita

O que não estiver decidido vira `[PRECISA ESCLARECER: pergunta objetiva]` no
documento. É proibido preencher lacuna com suposição silenciosa.

Nenhuma feature avança para `/plan` com marcadores `[PRECISA ESCLARECER]`
pendentes.

## Art. 4 — Todo requisito é verificável

Cada requisito funcional tem pelo menos um critério de aceite observável:
entrada, ação, resultado esperado. "Rápido", "intuitivo" e "robusto" não são
critérios — vire número, prazo ou comportamento observável.

## Art. 5 — Teste antes do código

A ordem é: contrato → teste que falha → implementação → teste que passa.

Nenhuma task de implementação é dada como concluída sem um teste que falharia
sem ela. Testes que nunca falharam não provam nada.

## Art. 6 — O contrato manda na integração

Toda fronteira (API, mensagem, formato persistido, protocolo entre módulos)
é descrita em `specs/NNNN-slug/contracts/` antes de ser implementada, e tem
teste em `tests/contract/`.

Mudança de contrato é mudança de spec: passa pelo mesmo fluxo, nunca "só um
campinho a mais".

## Art. 7 — Uma linguagem só

Os termos do domínio são os de `docs/glossary.md` — no código, no banco, na
interface e nas conversas. Termo novo entra no glossário na mesma entrega em
que aparece no código. Sinônimo não é permitido.

## Art. 8 — Decisão arquitetural vira ADR

Escolha estrutural durável — banco, runtime, hospedagem, fronteira entre
módulos, formato de autenticação — vira um arquivo em `docs/adr/`, com as
alternativas descartadas e o motivo. Sem ADR, a decisão não existe: será
reaberta na próxima dúvida.

## Art. 9 — Tasks são atômicas e verificáveis

Uma task tem dono único, arquivo(s) previsto(s) e uma forma objetiva de dizer
"pronto". Se não cabe em uma sessão de trabalho ou não dá para verificar
sozinha, ela é grande demais: quebre.

## Art. 10 — Simplicidade tem precedência

Diante de duas soluções que atendem à spec, vence a mais simples de entender
e de apagar. Abstração se conquista com o terceiro caso concreto, não com o
primeiro previsto.

Nada de infraestrutura "para quando crescer" sem requisito escrito que a
exija.

## Art. 11 — Nada quebrado no `main`

`main` sempre passa nas checagens do projeto. Entrega incompleta vive atrás
de um limite (branch, flag), nunca num `main` vermelho.

---

## Regras de stack

Cada escolha entra aqui **depois** de virar um ADR em `docs/adr/`, resumida
em uma linha com link para o ADR que a decidiu.

| Decisão | ADR |
|---|---|
| O backend é o **Supabase**. Não há servidor de aplicação próprio. | [0001](../docs/adr/0001-supabase-como-backend.md) |
| **Autorização é RLS**, no banco. Regra que não está em RLS não existe. | [0001](../docs/adr/0001-supabase-como-backend.md) |
| Schema só muda por **migration versionada**; tabela nova nasce com política. | [0001](../docs/adr/0001-supabase-como-backend.md) |
| Frontend é **SPA React com Vite**. Sem SSR, sem meta-framework, sem segredo no cliente. | [0002](../docs/adr/0002-spa-react-com-vite.md) |
| Todo o código é **TypeScript `strict`**; tipos do banco são gerados e versionados. | [0003](../docs/adr/0003-typescript-em-todo-o-codigo.md) |
| Testes em **Vitest**; ponta a ponta em **Playwright**; contrato e RLS contra o banco real. | [0004](../docs/adr/0004-vitest-e-playwright.md) |

Ainda **não** decididos, e portanto ainda livres: hospedagem, roteamento da
SPA, integração contínua, gerenciador de pacotes.

---

## Emendas

| Versão | Data | O que mudou | Por quê |
|---|---|---|---|
| 1.0.0 | 2026-09-02 | Ratificação inicial | Início do projeto em SDD |
| 1.1.0 | 2026-09-02 | Regras de stack preenchidas a partir dos ADRs 0001–0004 | Definição da stack: Supabase, React/Vite, TypeScript, Vitest/Playwright |
