---
description: Traduz uma spec aprovada em plano técnico, pesquisa, modelo de dados e contratos
argument-hint: [NNNN-slug] (opcional — usa a spec mais recente se omitido)
---

# /plan

Feature alvo: $ARGUMENTS

Se nada foi informado, use a spec mais recente em `specs/` — e diga ao
usuário qual escolheu, antes de trabalhar.

Você vai produzir `plan.md`, `research.md`, `data-model.md` e `contracts/`.
**Nenhum código de produção e nenhum teste ainda.**

## Portão de entrada

Antes de qualquer coisa, verifique — e **pare** se falhar:

1. `spec.md` existe e está marcada como `aprovada` ou `em revisão`.
2. Não sobrou nenhum `[PRECISA ESCLARECER]`. Se sobrou, liste os marcadores,
   explique que o Art. 3 bloqueia o avanço, e encerre sem escrever nada.
3. `specs/constitution.md` foi lido nesta sessão. Ele manda no plano.

## Ao planejar

1. **Pesquise antes de decidir.** Toda escolha não óbvia — biblioteca,
   formato, estratégia — passa por `research.md`: pergunta, o que foi
   verificado, resposta, e as alternativas descartadas com o motivo. Prefira
   verificar (docs, código do repo, experimento) a lembrar.
2. **Preencha a checagem constitucional** do `plan.md` artigo por artigo. Se
   o plano viola um artigo, você tem duas saídas legítimas: mudar o plano, ou
   propor emenda explícita ao usuário. Seguir em frente não é uma delas.
3. **Modele os dados** em `data-model.md`: entidades, campos, tipos e, acima
   de tudo, **invariantes** — cada uma rastreando até uma regra de negócio da
   spec. Nomes em inglês, descrições em português.
4. **Escreva os contratos** de toda fronteira em `contracts/` (Art. 6). O
   contrato vem antes da implementação, sempre. Cada operação aponta qual
   requisito da spec atende.
5. **Abra ADR** para toda decisão arquitetural durável — banco, runtime,
   hospedagem, autenticação, fronteira entre módulos (Art. 8). Crie o arquivo
   em `docs/adr/` a partir de `docs/adr/_template.md` e registre a escolha na
   tabela "Regras de stack" da constituição.
6. **Preencha a rastreabilidade.** Todo RF/RNF/RN da spec tem destino técnico
   na tabela. Nada de item órfão nos dois sentidos: requisito sem destino é
   esquecimento; componente sem requisito é escopo inventado.
7. **Escolha o simples** (Art. 10). Registre no plano o que você deixou de
   fora de propósito.

## Ao terminar

Responda com:

1. Os arquivos criados.
2. A abordagem em três a cinco linhas.
3. Os ADRs abertos, se houver.
4. As decisões que ainda dependem do usuário — sem enterrá-las no documento.
5. O próximo passo: revisar o plano e rodar `/tasks`.
