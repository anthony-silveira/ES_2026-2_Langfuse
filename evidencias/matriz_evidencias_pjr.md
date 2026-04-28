# Matriz de evidências - PJR

## Objetivo

Relacionar cada conclusão do eixo PJR às evidências observadas no repositório do Langfuse, de forma que a análise possa ser auditada e reproduzida.

| Achado | Evidência no repositório | Interpretação |
| --- | --- | --- |
| Arquitetura em camadas | `.agents/AGENTS.md` | O guia raiz descreve a separação entre `web`, `worker`, `packages/shared` e `ee`, reforçando fronteiras e responsabilidades. |
| Monorepo modular | Estrutura do repositório e `turbo.json` | O projeto está organizado em módulos com responsabilidades distintas e fluxo coordenado por workspace/monorepo. |
| Separação entre interface e domínio | `web/src/server/api/root.ts` e `packages/shared/src/server/repositories/*` | A entrada HTTP compõe routers, enquanto acesso a dados e lógica compartilhada ficam concentrados em camadas próprias. |
| Backend síncrono e assíncrono desacoplados | `web/src/pages/api/*`, `worker/src/app.ts`, `worker/src/queues/workerManager.ts` | A API recebe e valida requisições; os workers executam processamento em segundo plano. |
| Camada LLM centralizada | `packages/shared/src/server/llm/*` | Integrações com provedores de IA ficam em uma camada única, reduzindo duplicação e melhorando consistência. |
| Uso de Adapter/Strategy | `packages/shared/src/server/llm/types.ts`, `fetchLLMCompletion.ts` | A existência de abstrações como `LLMAdapter` evidencia adaptação entre provedores distintos. |
| Uso de Factory | `packages/shared/src/server/services/StorageService.ts` | `StorageServiceFactory` seleciona dinamicamente a implementação de storage conforme o provedor configurado. |
| Uso de Repository | `packages/shared/src/server/repositories/*` | O acesso a dados é encapsulado em repositórios, reduzindo acoplamento com a infraestrutura. |
| Núcleo de domínio bem definido | `packages/shared/prisma/schema.prisma` | O schema centraliza entidades como `Project`, `Trace`, `Observation`, `Score`, `Dataset` e `Prompt`. |
| Modelagem multi-tenant | `Organization`, `Project`, `OrganizationMembership` e `ProjectMembership` em `schema.prisma` | O sistema separa contexto organizacional, projetos e permissões de acesso. |
| Observabilidade orientada a entidades | `LegacyPrismaTrace`, `LegacyPrismaObservation`, `LegacyPrismaScore` em `schema.prisma` e contratos em `packages/shared/src/domain/*` | O domínio evidencia um fluxo principal de rastreamento, observação e avaliação. |
| Experimentação estruturada | `Dataset`, `DatasetItem`, `DatasetRuns`, `DatasetRunItems` em `schema.prisma` | O produto suporta avaliação reprodutível baseada em datasets e execuções controladas. |
| Governança de prompts | `Prompt`, `PromptDependency`, `PromptProtectedLabels` em `schema.prisma` | O Langfuse trata prompts como ativos versionados e relacionados entre si. |
| Dependência de serviços externos | `README.md`, `.env*.example`, serviços de storage, Redis, ClickHouse e LLM | A arquitetura depende de múltiplos componentes externos, o que aumenta criticidade operacional. |

## Síntese

As evidências mostram que a análise de PJR não foi baseada em opinião isolada, mas em artefatos verificáveis do próprio repositório. Os principais achados decorrem da combinação entre:

- estrutura do monorepo
- guias arquiteturais internos
- schema Prisma
- contratos de domínio
- serviços compartilhados
- camada de filas e workers
- camada de integração com LLM
