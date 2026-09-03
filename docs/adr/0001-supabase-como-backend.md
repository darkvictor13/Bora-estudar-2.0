# 0001 — Supabase como backend

- **Status:** aceito
- **Data:** 2026-09-02
- **Decisores:** Victor Almeida
- **Feature de origem:** transversal

## Contexto

O produto precisa de banco relacional, autenticação, armazenamento de
arquivos e uma API para o frontend consumir. Nenhuma dessas peças é o
diferencial do Bora Estudar — são infraestrutura obrigatória.

A equipe é pequena. Todo dia gasto mantendo servidor de aplicação, camada de
autenticação e CRUD é um dia não gasto no produto.

## Decisão

**O Supabase é o backend.** Não haverá servidor de aplicação próprio.

Concretamente:

- Os dados vivem no Postgres gerenciado pelo Supabase.
- A autenticação e as sessões são do Supabase Auth.
- O frontend fala com o banco pela API gerada (PostgREST), através do
  cliente oficial.
- **A autorização é feita por Row Level Security**, no banco. RLS é a
  fronteira de segurança do produto, não um complemento dela.
- Regra de negócio que precisa de servidor vive em Postgres (constraint,
  trigger, função) ou em Edge Function — nessa ordem de preferência.
- O schema é versionado em migrations; o ambiente local sobe pelo CLI do
  Supabase.

## Alternativas consideradas

### Supabase — **escolhida**

- A favor: Postgres de verdade (SQL, constraints, transações), auth e
  storage já resolvidos, ambiente local fiel ao de produção, tipos gerados a
  partir do schema, RLS como autorização declarativa e testável.
- Contra: acoplamento a um fornecedor; RLS exige disciplina — política mal
  escrita é vazamento de dados; processamento pesado não tem lugar natural.

### Backend próprio (Node, Laravel ou similar) — descartada

- A favor: controle total; nenhum limite de fornecedor.
- Contra: reintroduz tudo o que queremos evitar — deploy, escalonamento,
  autenticação, camada de acesso a dados, e o CRUD inteiro escrito à mão.
- Motivo do descarte: custo permanente de manutenção sem ganho de produto.

### Firebase — descartada

- A favor: maturidade, tempo real, ecossistema.
- Contra: banco de documentos. O domínio é fortemente relacional; consultas
  agregadas viram trabalho manual e duplicação de dados.
- Motivo do descarte: o modelo de dados não combina com o domínio.

### Postgres puro + API própria — descartada

- A favor: nenhum acoplamento; Postgres é Postgres.
- Contra: auth, storage e API passam a ser nosso problema.
- Motivo do descarte: é o backend próprio, com passos extras.

## Consequências

**Boas:**

- Autenticação, storage e API funcionando desde o primeiro dia.
- Postgres permite pôr invariante no banco — o `data-model.md` de cada
  feature vira constraint de verdade, não convenção.
- O schema gera tipos, o que dá checagem de contrato de graça (ver
  [0003](./0003-typescript-em-todo-o-codigo.md)).
- Ambiente local sobe por comando; teste de integração roda contra um banco
  real.

**Ruins — o preço que aceitamos pagar:**

- Sair do Supabase depois custa caro: auth e storage teriam de ser
  reescritos (o Postgres em si é portável).
- RLS mal escrita vaza dados de um aluno para outro. Toda política precisa
  de teste — não é opcional.
- Processamento longo ou pesado não cabe em Edge Function; se surgir,
  precisará de outra decisão.

**O que passa a ser proibido por causa disto:**

- Usar a chave `service_role` no frontend, em qualquer circunstância.
- Tratar autorização apenas na interface: se a regra não está em RLS, ela
  não existe.
- Alterar o schema fora de uma migration versionada.
- Tabela nova sem política de RLS explícita.

## Quando revisitar

- Quando aparecer requisito escrito de processamento que Edge Functions não
  sustentem (relatório pesado, fila longa, job de horas).
- Quando o custo do plano passar a competir com o de operar infraestrutura
  própria.
