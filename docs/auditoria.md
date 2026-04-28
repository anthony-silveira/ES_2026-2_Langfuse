# Processo de Desenvolvimento (Eixo I – GPR)

## 1. Ciclo de Vida e Frequência de Releases

Diferente do modelo Cascata, caracterizado pela rigidez e execução sequencial de fases, o projeto analisado adota um **Ciclo de Vida Ágil (Iterativo e Incremental)**. Esse modelo prioriza ciclos curtos de desenvolvimento, feedback contínuo e entrega frequente de valor.

### 1.1 Tabela de Periodicidade de Releases

| Versão  | Data de Publicação | Intervalo (dias) | Natureza da Alteração |
|:-------:|:-----------------:|:----------------:|:---------------------|
| v4.5.1 | 24/04/2026 | 3  | Correção de Bug (Patch) |
| v4.5.0 | 21/04/2026 | 11 | Melhoria de Funcionalidade |
| v4.2.0 | 10/04/2026 | 9  | Atualização de Atributos |
| v3.14.6| 01/04/2026 | 22 | Manutenção de Versão Anterior |
| v4.0.0 | 10/03/2026 | -  | Mudança Arquitetural (Major) |

### Análise do Padrão

Observa-se um padrão de releases frequentes e adaptáveis, com intervalos predominantemente inferiores a 15 dias. Esse comportamento evidencia:

- Entregas incrementais contínuas  
- Correções rápidas (patches)  
- Evolução progressiva do sistema  

Esse padrão é característico de ambientes ágeis baseados em **Working Software e Quick Feedback Cycles**.

---

## 2. Roadmap e Planejamento Incremental

A Gerência de Projetos (GPR), no contexto open source, baseia-se em evidências digitais disponíveis no repositório.

### Estrutura do Roadmap

O planejamento do projeto é realizado por meio de:

- **Milestones** → agrupamento de funcionalidades por versão  
- **Issues** → representação de requisitos e tarefas  
- **Pull Requests (PRs)** → implementação e validação  

### Evidências de Planejamento

- Uso de **labels** (ex: `high priority`, `enhancement`)  
- Organização de backlog via GitHub  
- Associação entre Issue → PR → Código  

Esse fluxo cria uma **rastreabilidade implícita**, conectando planejamento, execução e entrega.

### Alinhamento Estratégico

O roadmap funciona como um "fio condutor" do desenvolvimento, permitindo:

- Visualizar prioridades  
- Monitorar progresso  
- Organizar entregas incrementais  

---

## 3. Gerência de Riscos em Sistemas Baseados em LLM

Sistemas baseados em LLM apresentam riscos específicos, principalmente devido à dependência de serviços externos e comportamento não determinístico.

### Principais Riscos Identificados

- **Mudanças em APIs externas**  
  Dependência de provedores como OpenAI e Anthropic  

- **Alucinações de modelos**  
  Respostas inconsistentes ou incorretas  

- **Prompt Injection**  
  Manipulação de entrada maliciosa  

- **Custos variáveis**  
  Uso de tokens e consumo de API  

### Estratégias de Mitigação Observadas

- Uso de **LLM Evals**  
- Aplicação de **datasets de validação (Gold Standard)**  
- Monitoramento de execução e respostas  
- Controle de uso via métricas  

---

## 4. Análise Crítica de Maturidade (MPS.BR – Nível G)

O nível G do MPS.BR enfatiza dois processos principais:

- Gerência de Projetos (GPR)  
- Gerência de Requisitos (GRE)  

### 4.1 Pontos Fortes

- **Aderência ao processo**
  - Uso consistente do `CONTRIBUTING.md`  
  - Templates padronizados  

- **Verificação e Validação (V&V)**
  - Integração com GitHub Actions  
  - Execução automática de testes e lint  

- **Rastreabilidade**
  - Relação entre Issue → PR → Código  
  - Evidência de fluxo estruturado de desenvolvimento  

---

### 4.2 Lacunas Identificadas

- **Ausência de estimativas formais**
  - Não há métricas explícitas de esforço (ex: pontos de função)  

- **Falta de formalização de planos de contingência**
  - Ausência de políticas claras de rollback  
  - Falta de documentação de recuperação de falhas  

---

## 5. Conclusão

O projeto apresenta um nível elevado de organização e aderência às práticas modernas de desenvolvimento ágil, especialmente no contexto open source.

A frequência de releases, o uso de backlog estruturado e a integração com ferramentas de CI/CD demonstram maturidade técnica significativa.

No entanto, sob a perspectiva do MPS.BR Nível G, ainda existem lacunas relacionadas à formalização de processos, especialmente em:

- Planejamento estruturado  
- Estimativas de esforço  
- Gestão formal de riscos  

Como recomendação, a adoção de práticas mais formais de planejamento e controle contribuiria para elevar o nível de maturidade do projeto, tornando-o mais previsível, controlado e alinhado às boas práticas da Engenharia de Software.