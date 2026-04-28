# Modelagem e Arquitetura - Eixo PJR

## Nota de escopo

O repositório do Langfuse não define explicitamente o significado do eixo PJR. Por isso, esta análise foi construída com base nas evidências técnicas observadas no código-fonte, na estrutura do monorepo e na documentação interna do projeto, sendo alinhada às práticas de Solução Técnica (CMMI-DEV) e Projeto e Construção (MPS.BR).

## Diagnóstico geral

O Langfuse apresenta elevado nível de maturidade arquitetural para os critérios avaliados neste eixo. Observa-se separação clara entre interface, orquestração, domínio e infraestrutura, com uso consistente de contratos tipados, modularização por feature e serviços compartilhados.

Na prática, o sistema evita concentrar lógica de negócio nas camadas de entrada, como HTTP e filas. Routers, handlers e processors permanecem mais enxutos, enquanto services, repositories e contratos compartilhados concentram regras de negócio, acesso a dados e integração com serviços externos. Esse desenho reduz acoplamento, favorece manutenção, melhora rastreabilidade e facilita evolução incremental.

## 1. Classes principais levantadas

Para complementar a leitura do UML, também foi feito um levantamento das classes mais relevantes para a explicação arquitetural do sistema. O critério adotado não foi listar toda e qualquer classe do repositório, mas selecionar aquelas que concentram responsabilidades estruturais, como autenticação, rate limit, fachada de API, serviços compartilhados, execução assíncrona e integração com infraestrutura.

| Classe | Responsabilidade principal | Arquivo base |
| --- | --- | --- |
| ApiAuthService | Verifica auth headers, resolve escopo de acesso e invalida cache de API keys | `web/src/features/public-api/server/apiAuth.ts` |
| RateLimitService | Calcula e aplica limites por org/plano/recurso | `web/src/features/public-api/server/RateLimitService.ts` |
| RateLimitHelper | Encapsula o resultado do rate limit e emite a resposta 429 | `web/src/features/public-api/server/RateLimitService.ts` |
| ScoresApiService | Fachada versionada da API pública de scores | `web/src/features/public-api/server/scores-api-service.ts` |
| TableViewService | CRUD e permalink de saved views | `packages/shared/src/server/services/TableViewService/TableViewService.ts` |
| DefaultEvalModelService | Valida e persiste configuração padrão de modelo de avaliação | `packages/shared/src/server/services/DefaultEvaluationModelService/DefaultEvalModelService.ts` |
| WorkerManager | Registra workers BullMQ, mede fila e trata falhas | `worker/src/queues/workerManager.ts` |
| ClickHouseClientManager | Singleton que gerencia clients ClickHouse por configuração | `packages/shared/src/server/clickhouse/client.ts` |
| StorageServiceFactory | Factory que escolhe a implementação de storage | `packages/shared/src/server/services/StorageService.ts` |

Esse conjunto foi utilizado como apoio analítico porque representa classes que ajudam a demonstrar separação de responsabilidades, uso de padrões arquiteturais e desacoplamento entre camadas.

## 2. Diagrama UML

![Diagrama UML do Langfuse](../diagramas/diagrama_de_classe.png)

O diagrama UML foi incluído como apoio visual para a leitura da arquitetura e da modelagem central do Langfuse. Em vez de tentar representar todo o sistema em um único desenho, o recorte foi direcionado às entidades e relações mais importantes para a compreensão estrutural do produto.

Essa escolha foi intencional. O Langfuse é um sistema amplo, organizado em monorepo, com múltiplos módulos, integrações externas e componentes de suporte. Caso todo o sistema fosse detalhado em um único UML, o resultado tenderia a ficar excessivamente poluído, difícil de interpretar e pouco útil para análise acadêmica. Em arquitetura de software, um diagrama eficaz não é o que mostra tudo, mas o que evidencia, com clareza, os elementos que melhor explicam o domínio e suas relações principais.

Por isso, o UML prioriza:

- multi-tenant e controle de contexto: `Organization`, `Project`, `User` e memberships
- observabilidade principal: `Trace`, `Observation`, `Score` e `TraceSession`
- avaliação e governança: `ScoreConfig`
- experimentação: `Dataset`, `DatasetItem`, `DatasetRun` e `DatasetRunItem`
- engenharia de prompts: `Prompt` e `PromptDependency`
- associação de arquivos e evidências: `Media`, `TraceMedia` e `ObservationMedia`

Esse recorte é suficiente para demonstrar:

- qual é o núcleo do domínio do produto
- como as execuções são registradas e avaliadas
- como prompts e datasets se relacionam com o ciclo de observabilidade
- como o sistema mantém separação por projeto e organização

Assim, a ausência de detalhamento completo de todas as classes não representa limitação da análise, mas sim uma decisão metodológica para preservar legibilidade, foco e valor explicativo.

## 3. Indicadores positivos

### 3.1 Arquitetura em camadas bem definida

O fluxo principal do sistema segue o padrão:

- entrada: tRPC, REST pública e filas BullMQ
- aplicação: services e routers com responsabilidade limitada
- domínio e dados: Prisma, ClickHouse e repositories
- infraestrutura: Redis, storage, observabilidade e workers

Esse desenho promove separação de responsabilidades e facilita a evolução incremental do sistema, além de tornar a arquitetura mais auditável e compreensível.

### 3.2 Camada de LLM centralizada

A integração com provedores de LLM está concentrada em `packages/shared/src/server/llm/*`.

Essa decisão arquitetural estabelece um ponto único de manutenção para:

- adaptação de provedores
- estrutura de mensagens
- tool calling
- validação de modelos

Esse centralismo reduz duplicação e evita inconsistências entre funcionalidades que dependem de IA. Além disso, a abstração por adaptadores, como `LLMAdapter`, reforça extensibilidade e desacoplamento.

### 3.3 Desacoplamento operacional

O sistema apresenta separação clara entre processamento síncrono e assíncrono:

- a API web cuida de entrada, autenticação, validação e exposição
- os workers executam processamento em background

Esse modelo reduz acoplamento entre camadas e melhora previsibilidade operacional.

### 3.4 Uso de interfaces e contratos bem definidos

O projeto faz uso consistente de contratos e interfaces entre componentes, principalmente na camada de infraestrutura e integração com serviços externos. Destaca-se:

- Strategy/Adapter na integração com provedores de LLM
- Factory em `StorageServiceFactory`
- Repository na camada de acesso a dados

Essa abordagem promove baixo acoplamento e alta coesão.

### 3.5 Decisão arquitetural: monólito modular

O Langfuse adota um modelo de monólito modular organizado em monorepo, com fronteiras bem definidas entre `web`, `worker`, `packages/shared` e `ee`.

Essa decisão reduz a complexidade inerente a arquiteturas distribuídas e, ao mesmo tempo, mantém isolamento lógico entre componentes.

## 4. Pontos de atenção

### 4.1 Complexidade concentrada na camada de LLM

A centralização da lógica de integração com LLM, embora positiva, cria um ponto de alta criticidade. Essa camada lida com múltiplos provedores, formatos de requisição e resposta, tool calls, structured outputs e diferentes formas de autenticação.

Como consequência, há risco de aumento de complexidade e de impacto sistêmico quando essa camada evolui.

### 4.2 Forte dependência de serviços externos

O sistema depende de múltiplos componentes externos:

- Postgres
- ClickHouse
- Redis
- serviços de armazenamento
- APIs de LLM

Esse cenário exige estratégias robustas de retry, fallback, monitoramento e isolamento de falhas.

## 5. Diagnóstico por leitura crítica

### 5.1 Projeto

O projeto apresenta estrutura sólida baseada em monorepo, com separação clara de responsabilidades entre módulos.

### 5.2 Justificativa

A divisão entre `web`, `worker` e `packages/shared` demonstra justificativa arquitetural consistente:

- features de produto ficam no `web`
- processamento intensivo é delegado ao `worker`
- contratos e integrações são centralizados no `shared`

### 5.3 Resultado

O resultado observado é um sistema com alta manutenibilidade arquitetural, especialmente considerando a complexidade do domínio de observabilidade e avaliação de aplicações baseadas em LLM.

## 6. Fechamento prático

Diagnóstico final:

- arquitetura consistente e bem estruturada
- desacoplamento elevado entre camadas
- uso adequado de padrões arquiteturais
- centralização eficiente da lógica compartilhada
- boa separação entre produto, domínio e infraestrutura
- risco concentrado principalmente em integrações externas e na camada de LLM

## Conclusão

O Langfuse demonstra alto nível de maturidade arquitetural, com decisões coerentes para sistemas modernos orientados à integração com IA. A solução atende de forma consistente aos objetivos do eixo PJR, evidenciando boas práticas de Projeto e Construção e Solução Técnica.
