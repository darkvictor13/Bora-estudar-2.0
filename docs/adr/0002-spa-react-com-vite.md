# 0002 — SPA em React com Vite, sem meta-framework

- **Status:** aceito
- **Data:** 2026-09-02
- **Decisores:** Victor Almeida
- **Feature de origem:** transversal

## Contexto

O frontend é React, por decisão do time. Resta definir **o que roda em volta
dele**: um meta-framework com renderização no servidor, ou uma SPA compilada
para arquivos estáticos.

O produto é uma aplicação autenticada — painéis atrás de login. Não é um site
de conteúdo: não há página pública que dependa de indexação em buscador nem
de renderização no servidor para ser útil.

O [ADR 0001](./0001-supabase-como-backend.md) já decidiu que não existe
servidor de aplicação próprio. Um meta-framework traria um de volta.

## Decisão

**SPA em React, compilada com Vite. Sem SSR e sem meta-framework.**

A saída do build é um conjunto de arquivos estáticos. O frontend fala direto
com o Supabase.

## Alternativas consideradas

### React + Vite (SPA) — **escolhida**

- A favor: build estático, hospedagem trivial; servidor de desenvolvimento
  rápido; sem camada de servidor para manter; config compartilhada com o
  Vitest (ver [0004](./0004-vitest-e-playwright.md)).
- Contra: sem renderização no servidor; o primeiro carregamento depende do
  tamanho do pacote; SEO exigiria outra solução.

### Next.js — descartada

- A favor: SSR, roteamento por arquivo, ecossistema grande.
- Contra: reintroduz um servidor Node para manter e hospedar, contrariando
  o ADR 0001; boa parte do que oferece (rotas de API, server actions) é
  redundante com o Supabase.
- Motivo do descarte: decisão explícita do time, coerente com o ADR 0001 —
  não há requisito de SSR ou SEO que justifique o custo.

### React Router em modo framework / Remix — descartada

- A favor: menos servidor que o Next, bom modelo de dados por rota.
- Contra: ainda assume um servidor para render; o ganho é pequeno num app
  todo atrás de login.
- Motivo do descarte: mesma objeção do Next, em escala menor.

### Create React App — descartada

- A favor: era o caminho padrão.
- Contra: descontinuado.
- Motivo do descarte: não é opção viável hoje.

## Consequências

**Boas:**

- Um artefato só: arquivos estáticos, sem processo de servidor no frontend.
- Ciclo de desenvolvimento rápido.
- A fronteira fica óbvia: tudo que é regra vive no banco (ADR 0001), tudo que
  é interface vive aqui.

**Ruins — o preço que aceitamos pagar:**

- Nada de SEO server-side. Se um dia houver página pública que precise ser
  indexada, ela não caberá nesta arquitetura.
- O tamanho do pacote é responsabilidade nossa, e cresce em silêncio.
- Sem servidor, não há lugar para segredo no frontend — tudo que chega ao
  navegador é público.

**O que passa a ser proibido por causa disto:**

- Introduzir SSR, rota de servidor ou server action no frontend.
- Guardar qualquer segredo no código do cliente.
- Depender de um processo Node em execução para a aplicação funcionar.

## Quando revisitar

- Quando existir requisito **escrito** de indexação de página pública em
  buscador.
- Quando o tempo do primeiro carregamento virar métrica de produto violada
  de forma consistente.
