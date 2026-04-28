# Contexto de pesquisa - PJR

## Propósito

Este documento registra como a análise do eixo PJR foi conduzida, quais fontes foram consultadas, qual lógica orientou a leitura do repositório e por que determinadas evidências foram selecionadas como base para o diagnóstico final.

O objetivo principal foi garantir que a análise não se apoiasse apenas em impressões subjetivas sobre o projeto, mas em artefatos técnicos verificáveis do próprio Langfuse, permitindo rastreabilidade e replicação por outros integrantes da equipe ou pelo professor.

## Pergunta orientadora

Como o Langfuse organiza sua arquitetura e sua modelagem de domínio para sustentar observabilidade, avaliação, integração com aplicações baseadas em LLM e evolução modular do sistema?

## Recorte do eixo PJR

Como o enunciado da atividade não apresenta uma definição operacional rígida para o eixo PJR, o recorte adotado nesta análise foi alinhado às dimensões de Projeto e Construção, com foco em:

- decomposição arquitetural do sistema
- organização dos módulos e responsabilidades
- modelagem das entidades centrais do domínio
- evidências de desacoplamento entre camadas
- padrões arquiteturais empregados
- pontos de risco associados à estrutura técnica

Em outras palavras, a análise não teve como foco principal requisitos funcionais detalhados, testes automatizados ou métricas de performance isoladas, mas sim a forma como o sistema foi projetado e estruturado para sustentar crescimento e manutenção.

## Estratégia de pesquisa adotada

A pesquisa foi conduzida por leitura técnica orientada a evidências internas do repositório. O procedimento seguiu uma lógica progressiva, indo do nível mais amplo da arquitetura até o nível mais específico da modelagem de domínio.

O objetivo não foi reproduzir todo o código do projeto, mas identificar os artefatos que melhor revelam:

- a decomposição arquitetural do sistema
- a separação entre módulos e responsabilidades
- a organização do domínio de negócio
- os padrões arquiteturais empregados
- os pontos de risco e criticidade

## Etapas da investigação

### 1. Leitura de documentação e guias internos

Na primeira etapa, foram analisados os arquivos de documentação e orientação do repositório para compreender a estrutura oficial do projeto, seus módulos e as fronteiras de responsabilidade entre pacotes.

Essa etapa foi importante porque evitou interpretações apressadas baseadas apenas em nomes de pastas. Em vez disso, a análise partiu da visão arquitetural declarada pelo próprio projeto.

### 2. Mapeamento da estrutura do monorepo

Na segunda etapa, foi realizado o levantamento da estrutura macro do Langfuse, com atenção especial aos diretórios:

- `web`
- `worker`
- `packages/shared`
- `ee`

Esse mapeamento permitiu identificar a escolha por monólito modular e verificar a separação entre interface, backend síncrono, backend assíncrono e contratos compartilhados.

### 3. Leitura da camada de entrada e execução

Na terceira etapa, foram observados arquivos responsáveis por entrada, orquestração e execução, como routers, endpoints e workers. O objetivo foi verificar se a lógica de negócio estava concentrada nessas camadas ou se havia delegação adequada para serviços e repositórios.

### 4. Leitura da modelagem de domínio

Na quarta etapa, a análise se concentrou no schema Prisma e nos contratos de domínio do pacote compartilhado. Esse momento foi decisivo para entender:

- quais são as entidades nucleares do sistema
- como elas se relacionam
- quais objetos sustentam observabilidade, avaliação, experimentação e governança de prompts

Foi nessa etapa que se consolidou o núcleo da modelagem usado depois no UML.

### 5. Leitura da infraestrutura compartilhada

Na quinta etapa, foram analisados componentes de infraestrutura e integração, com foco em:

- repositórios
- storage
- camada de LLM
- organização de serviços compartilhados

Essa etapa ajudou a identificar padrões arquiteturais e pontos de centralização crítica.

## Principais fontes analisadas

### Documentação e guias

- `README.md`
- `CONTRIBUTING.md`
- `.agents/AGENTS.md`
- `packages/shared/AGENTS.md`

### Estrutura arquitetural

- `turbo.json`
- `package.json`
- estrutura dos diretórios `web`, `worker`, `packages/shared` e `ee`

### Backend e execução

- `web/src/server/api/root.ts`
- `web/src/pages/api/public/*`
- `worker/src/app.ts`
- `worker/src/queues/workerManager.ts`

### Camada de dados e domínio

- `packages/shared/prisma/schema.prisma`
- `packages/shared/src/domain/traces.ts`
- `packages/shared/src/domain/observations.ts`
- `packages/shared/src/domain/scores.ts`
- `packages/shared/src/domain/prompts.ts`
- `packages/shared/src/domain/dataset-items.ts`
- `packages/shared/src/domain/dataset-run-items.ts`
- `packages/shared/src/domain/score-configs.ts`

### Infraestrutura e integração

- `packages/shared/src/server/repositories/*`
- `packages/shared/src/server/services/StorageService.ts`
- `packages/shared/src/server/llm/*`

## Critério de seleção das evidências

Nem todo arquivo do repositório foi usado como evidência formal. Foram priorizados os artefatos que:

- descrevem responsabilidades arquiteturais
- materializam relações entre módulos
- revelam contratos e entidades do domínio
- demonstram desacoplamento entre camadas
- evidenciam padrões como Repository, Factory, Adapter/Strategy e processamento assíncrono
- ajudam a explicar o funcionamento do sistema sem depender de inferência excessiva

Também foi evitado usar como evidência principal arquivos excessivamente periféricos, scripts muito específicos ou trechos isolados que não representassem o desenho estrutural do produto.

## Critério para construção do diagnóstico

O diagnóstico foi produzido a partir do cruzamento entre:

- documentação declarada pelo projeto
- organização física do monorepo
- contratos de domínio
- schema de dados
- serviços de integração e infraestrutura

Com isso, cada conclusão do PJR foi sustentada por mais de um tipo de evidência sempre que possível. Por exemplo:

- a conclusão sobre monólito modular não veio apenas da estrutura de pastas, mas também da organização descrita em `AGENTS.md`
- a conclusão sobre centralização da camada LLM não veio apenas do nome da pasta, mas da leitura dos arquivos de contrato e execução em `packages/shared/src/server/llm/*`
- a conclusão sobre modelagem multi-tenant decorreu da combinação entre entidades como `Organization`, `Project`, `OrganizationMembership` e `ProjectMembership`

## Justificativa do recorte do UML

O diagrama UML produzido para o PJR não tenta modelar todas as classes, tabelas, serviços e integrações do Langfuse. O recorte foi feito sobre as entidades e relações mais importantes porque isso aumenta a clareza analítica e torna o diagrama mais adequado para leitura acadêmica.

Se todo o sistema fosse representado em um único diagrama, haveria perda de legibilidade e de valor explicativo. Em vez de facilitar a compreensão, o excesso de elementos dificultaria a identificação do núcleo arquitetural do produto.

Por isso, o foco foi colocado em:

- multi-tenant: organização, projeto e memberships
- observabilidade: trace, observation, score e session
- experimentação: dataset e runs
- prompt engineering: prompt e dependências
- anexos e evidências: media e relações associadas

Esse recorte foi suficiente para demonstrar:

- o centro do domínio do Langfuse
- o fluxo principal de observabilidade e avaliação
- a relação entre projeto, execução, avaliação e experimentação
- a estrutura de governança de prompts e dados

## Limites da análise

Esta pesquisa não teve como objetivo:

- auditar exaustivamente todas as features do produto
- documentar todos os arquivos do repositório
- reproduzir cada fluxo de execução em ambiente rodando
- medir quantitativamente cobertura de testes, desempenho ou qualidade de código linha a linha

Esses temas podem aparecer em outros eixos da disciplina, mas para o PJR o foco principal foi a qualidade da organização arquitetural e da modelagem.

## Artefatos gerados a partir da pesquisa

Como resultado da investigação, foram produzidos os seguintes artefatos para a parte de PJR:

- relatório de modelagem e arquitetura
- diagrama UML em imagem
- fonte textual do diagrama em Mermaid
- matriz de evidências relacionando achados a arquivos do repositório
- texto explicativo sobre o recorte metodológico adotado

## Resultado metodológico

Com esse processo, a análise de PJR se manteve:

- rastreável, porque cada conclusão aponta para artefatos reais
- auditável, porque outras pessoas podem verificar os mesmos arquivos
- sintética, porque o recorte privilegia os elementos mais explicativos
- replicável, porque os caminhos analisados foram registrados
- defensável, porque o relatório explica não apenas o resultado, mas também o caminho percorrido para chegar a ele
