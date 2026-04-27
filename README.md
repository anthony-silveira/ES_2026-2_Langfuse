# ES_2026-2_Langfuse
Repository created for academic activities

- IV. Eixos de Análise
Verificação e Validação (Foco: V&V):
  
Em resumo, a verificação focará na conformidade, ou seja, se o software está sendo desenvolvido de acordo com as especificações técnicas, padrões de códigos e requisitos definidos anteriormente.
No langfuse, por exemplo, analisamos a verificação olhando o código, documentos, diagramas e lógicas internas, por exemplo, analisando o workflows do repositório e os peer reviews nos pull requests.
Já a validação focará na necessidade do usuário, ou seja, no final de cada ciclo é necessário validar se a ferramenta realmente age como o usuário espera e resolva o problema dele. Para isso é necessário que olhemos o software em        execução e o comportamento da ia.
No langfuse, como ele age como uma ferramenta de validação para outros sistemas de ia, iremos verificar se as métricas que ele entrega aos usuários são precisas.

  Análise da pasta workflows:
Por padrão, a pasta workflows se encontra na pasta .github/workflows, então o projeto já segue essa convenção facilitando o acesso e entendimento.
São workflows desse projeto:
deploy_ecs_service.yml | ci.yml.template | cla-assistant.yml | claude-review-maintainer-prs.yml | codeql.yml | codespell.yml | dependabot-rebase-stale.yml | deploy.yml | licencecheck.yml | pipeline.yml | promote-main-to-production.yml | release.yml | sdk-api-spec.yml | snyk-web.yml | snyk-worker.yml | stale_issues.yml | validate-pr-title.yml | zizmor.yml

  Podemos citar três principais arquivos neste workflows:
ci.yml.template:
É um template utilizado para gerar o ci (continuos integration) final, tem como principal objetivo a verificação. 
Principal linha de comando: run: pnpm turbo build lint type-check
Build verificará se o código é compilável, ou seja, se houver algum erro de sintaxe ou dependência faltando o código quebra.
Lint verificará estilo e boas práticas, por exemplo uso de variáveis não declaradas.
Type-check verificará se função está passando para a outra com o tipo correto.

Pipeline.yml:
No pipeline os testes estão divididos em pedaços, há alguns testes automatizados para verificação:
Testes de Backend (Jest): O job tests-web executa o comando npx jest --selectProjects server. Ele usa uma matriz para testar em diferentes versões do PostgreSQL (12 e 15), o que é uma excelente evidência de rigor técnico para o CMMI.
Testes de Worker: O job tests-worker roda o comando pnpm --filter=worker run test:exclude-llm-connections. Isso verifica a lógica interna do processamento de dados sem depender de IAs externas.
Lint e Tipagem: Os jobs lint e prettier-check garantem que o código segue o padrão estético e não possui erros de sintaxe TypeScript (pnpm run lint).
Há também alguns mecanismos para validação:
O job test-worker-llm-connections: Ele usa chaves reais (secrets) da OpenAI, Anthropic e Azure para rodar o comando test:llm-connections-only. testa se a integração com a IA externa está retornando o que deveria, ataca diretamente o risco de volatilidade das APIs de LLM mencionado no roteiro da atividade.
Os jobs e2e-tests e e2e-server-tests utilizam a ferramenta Playwright: Eles simulam um usuário real navegando no sistema (test:e2e), validando se o fluxo completo do software entrega o valor esperado ao usuário final.

claude-review-maintainer-prs.yml:
Nesse arquivo acontece uma verificação peer review, feito pela próprio claude. Sempre que um mantenedor abre um Pull Request (PR), o workflow dispara um comentário @claude review. Isso automatiza parte da Verificação técnica. Em vez de depender apenas de humanos, uma IA (Claude) valida se o código novo faz sentido antes de ele ser fundido ao projeto principal.

  Sistema de avaliação do Langfuse:
O sistema de avaliação é o componente mais crítico para a Validação qualitativa das saídas de IA. Nossa auditoria no código-fonte revelou:
Que o Langfuse utiliza a biblioteca Zod para garantir que nenhuma avaliação (score) entre no sistema sem cumprir regras rígidas de integridade:
Lógica de Exclusividade: A função applyScoreValidation exige que um score esteja vinculado a exatamente um identificador (traceId, sessionId ou datasetRunId). Isso evita inconsistências no banco de dados e garante que o feedback do usuário tenha um destino preciso.
Filtros de Segurança: Funções como filterAndValidateDbScoreConfigList verificam as configurações vindas do banco de dados (Prisma), descartando automaticamente dados corrompidos.
Que a estrutura definida em scoresTableCols mapeia diretamente a lógica técnica para a interface do usuário:
Rastreabilidade de Ponta a Ponta: Cada coluna (Trace ID, Session ID, Source, Data Type) permite que o usuário realize a Validação das métricas entregues.
Diferenciação de Fonte: O sistema distingue se o score veio de uma "IA" ou de um "Humano", permitindo auditorias cruzadas de qualidade.

  Análise de peer review e processo de revisão de código:
Para a verificação, selecionamos pull requests que apresentassem uma trilha clássica de evolução: issue > pull request > código final.
Percebemos que a boa parte dos prs que possuíam essa características tinham os prefixos feat e fix, estes possuíam discussões ativas na aba conversation e vínculo explícitos com issues reportados pela comunidade.
Como exemplo, citaremos a seguinte trilha de rastreabilidade:
Issue Original (#11529): Identificou uma falha na visibilidade do estado posterior ("after state") nos logs de auditoria de cargos organizacionais.
Pull Request de Correção: O PR implementou a migração de testes unitários para o Vitest e corrigiu a lógica de persistência de logs no roteiro de membros.
Código Final: As alterações foram consolidadas no arquivo membersRouter.ts, normalizando a identificação de recursos. 
Ou seja, A análise do processo de revisão do Langfuse revela um nível de maturidade elevado, caracterizado por um modelo híbrido que combina inteligência humana e automação.
Verificação Assistida por IA (Claude Review): O diferencial competitivo do projeto é o uso do workflow claude-review-maintainer-prs.yml. Este mecanismo automatiza o Peer Review, permitindo que uma IA (Claude) realize uma análise lógica profunda antes mesmo da intervenção humana.
Eficácia da Revisão: Durante a auditoria, observou-se que o revisor automatizado foi capaz de detectar falhas de condição de corrida (TOCTOU) e riscos de conformidade em logs de auditoria que não haviam sido capturados pelos testes automatizados convencionais.
Conformidade com CMMI/MPS.BR: O processo de revisão não se limita apenas à correção de sintaxe, mas valida a Solução Técnica (PJR) e a Gestão de Mudanças (GRE). A exigência de que os testes (conforme o job tests-web) passem antes do merge assegura que a Verificação seja uma barreira de qualidade intransponível no pipeline de CI/CD.






  
