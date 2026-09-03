# Decisões Arquiteturais (ADR)

Uma decisão durável por arquivo, numerada em sequência e **imutável**: ADR
aceito não se edita. Mudou de ideia? Escreve-se um novo, e o antigo passa a
`substituído por NNNN`.

Copie `_template.md` para `NNNN-titulo-em-kebab-case.md`.

O que merece ADR (Constituição, Art. 8): banco, runtime, hospedagem,
autenticação, fronteira entre módulos, formato persistido, dependência
difícil de remover.

O que **não** merece: escolha reversível numa tarde. Essa vive no `plan.md`
da feature.

| ADR | Decisão | Status |
|---|---|---|
| [0001](0001-supabase-como-backend.md) | Supabase é o backend; autorização por RLS | aceito |
| [0002](0002-spa-react-com-vite.md) | SPA React com Vite, sem meta-framework | aceito |
| [0003](0003-typescript-em-todo-o-codigo.md) | TypeScript `strict` em todo o código | aceito |
| [0004](0004-vitest-e-playwright.md) | Vitest para unit/integração/contrato, Playwright para e2e | aceito |

## Decisões ainda em aberto

Sem ADR até que um requisito escrito as force:

- Hospedagem do frontend estático
- Roteamento da SPA
- Integração contínua
- Gerenciador de pacotes
