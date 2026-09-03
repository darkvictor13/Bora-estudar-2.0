# Modelo de Dados — [Nome da feature]

- **Spec:** [`spec.md`](./spec.md) · **Plano:** [`plan.md`](./plan.md)

> Entidades, campos e **invariantes**. Nomes de entidade e campo em inglês;
> descrições em português. Todo termo aqui existe em `docs/glossary.md`
> (Art. 7).

## Entidades

### `EntityName`

[Uma frase: o que esta entidade representa no domínio.]

| Campo | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | [tipo] | sim | Identificador |
| `[field]` | [tipo] | [sim/não] | [...] |
| `created_at` | timestamp | sim | Criação |

**Invariantes** — verdades que nunca podem ser violadas, em nenhum caminho:

| ID | Invariante | Origem |
|---|---|---|
| INV-01 | [ex.: `[field]` é único entre registros ativos] | RN-01 |

**Estados** (se a entidade tiver ciclo de vida):

```
[rascunho] ──▶ [ativo] ──▶ [encerrado]
```

| Transição | Quando ocorre | Quem pode |
|---|---|---|
| rascunho → ativo | [...] | [...] |

## Relações

| De | Para | Cardinalidade | Regra |
|---|---|---|---|
| `EntityA` | `EntityB` | 1:N | [ex.: apagar A apaga os B] |

## Volumetria esperada

| Entidade | Volume estimado | Crescimento |
|---|---|---|
| `EntityName` | [...] | [...] |

## Migração

- [O que precisa acontecer com dados existentes; "nada, entidade nova" também
  é resposta válida.]
