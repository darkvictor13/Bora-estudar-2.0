---
description: Cria a spec de uma feature nova (o quê e por quê, sem tecnologia)
argument-hint: <descrição da feature em uma ou duas frases>
---

# /specify

Descrição da feature dada pelo usuário:

> $ARGUMENTS

Você vai produzir **apenas** a `spec.md` de uma feature nova. Nada de código,
nada de escolha técnica, nada de arquivo fora da pasta da feature.

## Antes de escrever

1. Leia `specs/constitution.md` — em especial os Art. 2, 3, 4 e 7.
2. Leia `docs/vision.md` e `docs/glossary.md`. A spec usa os termos do
   glossário; se a feature exige um termo novo, ele é definido na spec e
   anotado para entrar no glossário.
3. Liste `specs/` e descubra o maior número de feature já usado. O número
   desta é o próximo, com quatro dígitos (`0001`, `0002`, ...).
4. Confira se já existe spec cobrindo o mesmo problema. Se existir, diga isso
   ao usuário e pergunte se é para estender a existente em vez de criar outra.

## Ao escrever

1. Crie `specs/NNNN-slug/` — `slug` curto, em português, com hífens
   (ex.: `0001-cadastro-usuario`).
2. Copie `specs/_template/spec.md` para lá e preencha **todas** as seções.
3. Regras que não se negociam:
   - **Sem tecnologia.** Nenhum framework, banco, biblioteca, endpoint, nome
     de classe ou de tabela. Se a frase deixaria de fazer sentido caso o
     produto fosse reescrito em outra linguagem, ela não pertence à spec.
   - **Todo requisito verificável.** Cada RF tem critério de aceite com
     entrada, ação e resultado observável. "Rápido" vira número.
   - **Ambiguidade é explícita.** Tudo que a descrição do usuário não decidiu
     vira `[PRECISA ESCLARECER: pergunta objetiva]`. É proibido escolher por
     conta própria e seguir em silêncio. Áreas que costumam esconder lacuna:
     quem pode fazer, o que acontece no caminho de erro, o que acontece com
     dado já existente, limites e volumes, o que é proibido.
   - **Fora de escopo é obrigatório.** Diga o que esta feature não faz.
4. Não crie `plan.md`, `tasks.md`, `data-model.md` nem `contracts/` — cada um
   tem seu comando.

## Ao terminar

Responda ao usuário com, nesta ordem:

1. O caminho da spec criada.
2. Os cenários e requisitos, em uma linha cada.
3. **A lista dos `[PRECISA ESCLARECER]`, como perguntas diretas.** Se houver
   algum, diga claramente que a feature não avança para `/plan` enquanto
   estiverem abertos (Art. 3).
4. O próximo passo: responder as perguntas, revisar a spec, e então `/plan`.
