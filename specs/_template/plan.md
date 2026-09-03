# Plano Técnico — [Nome da feature]

- **Spec:** [`spec.md`](./spec.md)
- **Status:** rascunho | aprovado
- **Data:** AAAA-MM-DD

> `plan.md` responde **como**. Ele traduz a spec em arquitetura, sem inventar
> requisito novo: tudo aqui rastreia até um RF/RNF/RN da spec.

## Resumo da abordagem

[Um parágrafo: a forma da solução, em alto nível. Alguém que leia só isto
deve conseguir explicar a estratégia.]

## Checagem constitucional

Preencher antes de aprovar. Violação = plano reprovado (ou emenda explícita).

| Artigo | Como este plano cumpre |
|---|---|
| Art. 5 — Teste antes do código | [...] |
| Art. 6 — Contrato manda na integração | [...] |
| Art. 7 — Uma linguagem só | [...] |
| Art. 8 — Decisão vira ADR | [ADRs criados/afetados, ou "nenhuma decisão nova"] |
| Art. 10 — Simplicidade | [o que foi deliberadamente deixado de fora] |

## Stack e ferramentas

Só o que esta feature usa, com o motivo. Escolha durável → abrir ADR (Art. 8).

| Escolha | Motivo | ADR |
|---|---|---|
| [...] | [...] | [`docs/adr/NNNN-....md`] |

## Arquitetura

[Componentes envolvidos e como conversam. Diagrama em texto quando ajudar.]

```
[cliente] ──▶ [componente A] ──▶ [componente B]
```

### Componentes tocados

| Componente | Novo ou existente | Responsabilidade nesta feature |
|---|---|---|
| [...] | [...] | [...] |

## Modelo de dados

Detalhado em [`data-model.md`](./data-model.md). Resumo:

- [entidade nova/alterada e o porquê]

## Contratos

Detalhados em [`contracts/`](./contracts/). Resumo:

| Fronteira | Contrato | Teste |
|---|---|---|
| [ex.: API pública] | `contracts/openapi.yaml` | `tests/contract/[...]` |

## Estratégia de testes

| Camada | O que cobre aqui | Onde |
|---|---|---|
| Contrato | [...] | `tests/contract/` |
| Integração | [...] | `tests/integration/` |
| Unidade | [...] | `tests/unit/` |

## Rastreabilidade

Todo requisito da spec tem destino técnico. Nenhuma linha sem origem.

| Requisito | Onde é atendido |
|---|---|
| RF-01 | [componente / contrato / função] |

## Riscos e mitigações

| Risco | Impacto | Mitigação |
|---|---|---|
| [...] | [...] | [...] |

## Alternativas consideradas

Investigação completa em [`research.md`](./research.md). Resumo do descarte:

- **[Alternativa]** — descartada porque [...]
