# Testes de contrato

Validam `specs/*/contracts/` — o que atravessa uma fronteira: formato,
campos obrigatórios, códigos de erro, compatibilidade.

O contrato manda (Constituição, Art. 6): quando o teste falha, a suspeita
recai sobre a implementação, não sobre o contrato. Mudar o contrato para o
teste passar é mudar a spec — passa pelo fluxo completo.

Estes testes vêm **antes** da implementação e precisam falhar primeiro.
