# Notas de versão — pagamentos 2.4.0

Data de lançamento: 2026-11-06

Dados fictícios para demonstração.

## Novidades

- Adicionada a exportação de pagamentos em CSV, sem adaptação obrigatória. ([PAY-101](https://example.com/demo/PAY-101))

## Correções

- Corrigida a exportação que retornava somente a primeira página de pagamentos; agora inclui os registros das páginas seguintes. ([PAY-102](https://example.com/demo/PAY-102))

## Mudanças incompatíveis

- O campo de API `name` foi renomeado para `full_name`. Para migrar, substitua `name` por `full_name` na integração. ([PAY-103](https://example.com/demo/PAY-103))

## Informações pendentes

Nenhuma.
