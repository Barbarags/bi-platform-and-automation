# Standards in use / Padrões em uso

## Naming / Nomenclatura

| Prefix / Prefixo | EN | PT |
|---|---|---|
| `0_` | Dimensions, estimates, reference tables | Dimensões, estimativas, tabelas de referência |
| `1_` | Origin (extracted facts, split by year) | Origem (fatos extraídos, divididos por ano) |
| `2_` | Detail and aggregation of the origin | Detalhe e agregação da origem |
| `6_` | Finalized internal processes | Processos internos finalizados |
| `x_` | Retired, pending removal | Aposentado, aguardando remoção |
| `TEST_` / `TESTE_` | Work in progress, not production | Em desenvolvimento, fora de produção |

## Practices / Práticas

1. **Layering** – source-specific logic in the flow workspace; models consume, never extract.
2. **Environments** – separate gateway connections for development and production.
3. **Access by group** – administrators and the data team; no individual grants.
4. **Incremental Refresh** on large entities (two years stored, recent months refreshed, change detection).
5. **Config tables** for rule parameters (tolerances, versions) read through a function.
6. **Endorsement** – *Certified* for dataflows and apps that the business depends on.
7. **Documentation** – data dictionary (table, alias, behavior, rule, business meaning) and written metric definitions ship with each model.
8. **Monitoring** – scheduled refreshes reviewed in the monitoring hub; failures investigated by the owner.
