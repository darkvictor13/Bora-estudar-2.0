---
description: Executa as tasks de uma feature, em ordem, com teste antes do código
argument-hint: [NNNN-slug] [ou uma task específica, ex.: T020]
---

# /implement

Alvo: $ARGUMENTS

Sem argumento: feature mais recente em `specs/`, a partir da primeira task
não concluída. Com um `TNNN`: só aquela task e as suas dependências.

## Portão de entrada

Pare e avise se `tasks.md` não existir, não estiver aprovado, ou tiver
requisito sem cobertura na tabela final.

Leia antes de tocar em qualquer arquivo: `specs/constitution.md`, e a
`spec.md`, `plan.md`, `data-model.md`, `contracts/` e `tasks.md` da feature.

## O laço de execução

Para cada task, na ordem, uma de cada vez:

1. **Leia a task inteira** — arquivos previstos, "pronto quando", dependências.
   Se alguma dependência não está `[x]`, não comece.
2. **Task de teste** (Bloco 2): escreva o teste e **rode-o**. Ele precisa
   **falhar**, pelo motivo certo. Teste que passa de primeira não está
   testando a feature — conserte o teste antes de seguir (Art. 5).
3. **Task de implementação** (Bloco 3): escreva o mínimo que faz o teste
   passar. Rode o teste. Nada além do que a task pede — melhoria fora de
   escopo é outra task, não um brinde.
4. **Verifique o "pronto quando"** de fato: rode o comando, não presuma.
5. **Marque `[x]`** em `tasks.md` assim que a verificação passar, uma task por
   vez. O arquivo é o estado da execução — mantenha-o honesto.
6. **Se travar**: pare, não improvise. Relate o que travou, o que você tentou
   e quais são as saídas. Contornar o plano em silêncio é o pior desfecho.

Tasks `[P]` do mesmo bloco podem ser feitas em sequência sem cerimônia; a
marcação existe para dizer que não há dependência entre elas.

## Limites

- **Não altere `spec.md`, `plan.md` nem `contracts/` durante a implementação.**
  Se a realidade contradiz o plano, pare e diga: a correção volta ao `/plan`
  (Art. 1 e Art. 6).
- Não pule o bloco de testes "porque é simples".
- Não deixe `main` quebrado (Art. 11).
- Termo de domínio novo entra em `docs/glossary.md` na mesma entrega (Art. 7).

## Ao terminar

Rode a suíte completa e as checagens do projeto. Depois responda com:

1. Tasks concluídas e tasks que sobraram.
2. Resultado real das checagens — **cole a saída se algo falhou**. Nunca
   relate verde o que não ficou verde.
3. Requisitos da spec agora atendidos, e os que ainda não.
4. Divergências entre plano e realidade que mereçam voltar ao `/plan`.
