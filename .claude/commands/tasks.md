---
description: Quebra um plano aprovado em tasks atômicas, ordenadas e verificáveis
argument-hint: [NNNN-slug] (opcional — usa a feature mais recente se omitido)
---

# /tasks

Feature alvo: $ARGUMENTS

Se nada foi informado, use a feature mais recente em `specs/` — e diga qual
escolheu.

Você vai produzir **apenas** `tasks.md`. Nenhum código.

## Portão de entrada

Pare e avise se: não existir `plan.md`, ou ele não estiver aprovado, ou a
checagem constitucional dele estiver em branco.

## Ao quebrar em tasks

Leia `spec.md`, `plan.md`, `data-model.md` e `contracts/` inteiros antes de
escrever a primeira task.

Regras de formação:

1. **Ordem obrigatória** (Art. 5): preparação → contratos → testes que falham
   → implementação → fechamento. Nenhuma task de implementação aparece antes
   do teste que ela faz passar.
2. **Atômica** (Art. 9): dono único, arquivos previstos, e um "pronto quando"
   objetivo — um comando que roda, um teste que passa, um arquivo que existe
   com determinado conteúdo. Se não dá para verificar sozinha, quebre.
3. **`[P]` só quando é verdade**: duas tasks são paralelas apenas se não
   tocam o mesmo arquivo e nenhuma depende do resultado da outra.
4. **`Depende de:` em todas.** Um traço quando não há dependência.
5. **Cada task de implementação cita o requisito** (RF/RN) que atende.
6. **Fechamento sempre inclui**: suíte completa verde, glossário atualizado
   (Art. 7) e a spec marcada como `implementada`.
7. **Preencha a tabela de cobertura** ao final: todo requisito da spec
   aparece em pelo menos uma task. Requisito sem task é bug de planejamento —
   volte e corrija antes de entregar.

Numere `T001`, `T010`, `T020`... com folga entre blocos, para caber inserção
depois sem renumerar tudo.

## Ao terminar

Responda com: quantidade de tasks por bloco, quais podem rodar em paralelo,
o caminho crítico, e qualquer requisito que você não conseguiu cobrir (e por
quê). Próximo passo: `/implement`.
