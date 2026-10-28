# Plataforma de BI e Automação

🇬🇧 [Read in English](README.md)

A plataforma por trás das análises: um ambiente em camadas **Microsoft Fabric / Power BI** (workspaces, dataflows, modelos semânticos, apps, gateway local) mais fluxos de **Power Automate** que enviam insights diários ao Microsoft Teams, com os padrões que mantêm tudo sustentável.

> Tudo aqui é **sanitizado**. Nenhum tenant, servidor, id de workspace, usuário, empresa ou parceiro aparece neste repositório.

## Arquitetura

Diagrama no [README em inglês](README.md#architecture).

- **Dois tipos de workspace** – workspaces de *fluxo* cuidam da ingestão e da transformação (dataflows); workspaces de *domínio* cuidam de modelos semânticos, relatórios e do App entregue a cada público. Um modelo pesado não trava um leve, e uma mudança de fonte toca um único lugar.
- **Gateway local** – um cluster de gateway atende conexões de SQL Server, SharePoint e dataflows. Desenvolvimento e produção usam conexões separadas, e o acesso é dado a grupos (administradores e time de dados), não a pessoas.
- **Dataflows com Atualização Incremental** – entidades grandes guardam dois anos de histórico e atualizam só os meses mais recentes, por detecção de mudança.
- **Endosso** – dataflows críticos de produção e o app de operações levam o selo *Certificado*, para o consumidor saber no que confiar.
- **Monitoramento** – o hub de monitoramento acompanha atualizações agendadas, duração e falhas em todos os workspaces.
- **Caminho de migração** – a camada de conciliação foi reconstruída em Dataflow Gen2 em workspace de testes, enquanto a produção segue em Gen1; as regras foram para uma tabela de configuração para poderem ser versionadas.

## Insights diários no Teams (Power Automate)

Dois fluxos agendados transformam os modelos semânticos em mensagens que as pessoas de fato leem. Detalhes em [`docs/power-automate-flows.md`](docs/power-automate-flows.md).

## Padrões em uso

Convenções que mantêm ~70 dataflows e dezenas de modelos navegáveis. Detalhes em [`docs/standards.md`](docs/standards.md).

- Prefixos numéricos por camada (`0_` dimensões e estimativas, `1_` origem, `2_` detalhe, `6_` processos finalizados).
- `x_` marca itens aposentados antes da remoção; `TESTE_` marca trabalho em andamento.
- Parâmetros em tabelas de configuração, não escondidos nas consultas.
- Dicionário de dados e definição de métricas documentados por modelo.
- Atualização Incremental em entidades grandes; certificação nas críticas.

<!-- RESULTADOS: incluir depois (tempo de refresh antes/depois, falhas evitadas, usuários, horas economizadas com automação). -->

## Autoria

Construído e mantido por [Bárbara Gomes](https://github.com/Barbarags) – Coordenadora de Dados e BI.
