# Plano de Melhoria

## Introdução
Como resultado da auditoria realizada no sistema baseado no Langfuse, foram identificados diversos problemas relacionados à ausência de formalização de processos, apesar da elevada maturidade arquitetural observada.

A tabela de problemas identificados evidenciou lacunas principalmente nas áreas de planejamento, controle de requisitos e gestão de riscos. Já a priorização destacou como críticos os problemas P1 (ausência de planejamento) e P2 (falta de gestão de requisitos), ambos classificados com prioridade alta.

Além disso, a análise da modelagem UML e do diagnóstico arquitetural revelou um sistema com alta complexidade, caracterizado por:

- Centralidade da entidade **Project**
- Múltiplos fluxos críticos (Trace → Observation → Score)
- Forte dependência de serviços externos
- Complexidade concentrada na camada de LLM

Esse cenário reforça a necessidade de processos bem definidos para garantir controle e evolução do sistema.

---

## Priorização dos Problemas

| ID | Problema | Evidência | Processo Afetado | Impacto |
|----|---------|----------|------------------|--------|
| P1 | Ausência de planejamento formal | Não há controle explícito de atividades | Gerência de Projetos (GP) | Baixa previsibilidade |
| P2 | Falta de gestão de requisitos | Não há rastreabilidade clara | Gerência de Requisitos (GR) | Dificuldade de evolução |
| P3 | Alta complexidade na camada de LLM | Camada central concentra múltiplas responsabilidades | Qualidade / Arquitetura | Risco de falhas sistêmicas |
| P4 | Dependência de serviços externos | Uso de múltiplos serviços (Redis, APIs, etc.) | Gerência de Projetos (com foco em riscos) | Baixa resiliência |
| P5 | Falta de controle formal de riscos | Não há evidência de mitigação estruturada | Gerência de Projetos (GP) | Instabilidade |

---

## Relação entre Problemas e Prioridade

Com base na análise realizada:

- **P1 (Planejamento)** → Prioridade Alta → Impacta a organização do projeto  
- **P2 (Requisitos)** → Prioridade Alta → Impacta a evolução do sistema  
- **P3 e P4** → Prioridade Média → Representam riscos operacionais  

A priorização orientou a definição das ações de melhoria, focando nos problemas de maior impacto.

---

## 1. Implantação de Gerência de Projetos (GP)

### Problemas relacionados
- P1 — Ausência de planejamento formal  
- P4 — Dependência de serviços externos  
- P5 — Falta de gestão de riscos  

### Justificativa
Apesar da arquitetura bem definida, não foram identificadas evidências de:
- Planejamento estruturado  
- Controle formal de atividades  
- Gestão de riscos  

Essa lacuna é crítica considerando:
- A dependência de serviços externos  
- A complexidade da camada de LLM  
- A quantidade de componentes interligados  

### Ação proposta
Implementar um processo estruturado de Gerência de Projetos, incluindo:
- Planejamento de atividades (Kanban ou Scrum)  
- Definição de tarefas e responsáveis  
- Monitoramento contínuo  
- Gestão de riscos  

### Impacto esperado
- Maior organização  
- Redução de riscos  
- Melhor controle da evolução do sistema  

---

## 2. Implantação de Gerência de Requisitos (GR)

### Problemas relacionados
- P2 — Falta de requisitos definidos  
- P3 — Falta de rastreabilidade  

### Justificativa
A modelagem UML evidencia a existência de múltiplos fluxos:
- Observabilidade (Trace → Observation → Score)  
- Experimentação (Dataset → DatasetRun)  
- Prompt Engineering  

No entanto, não há evidências de:
- Controle formal de requisitos  
- Rastreabilidade entre requisitos e código  
- Gestão de mudanças  

### Ação proposta
Estabelecer um processo de Gerência de Requisitos com:
- Criação de backlog estruturado (GitHub Issues)  
- Definição de requisitos funcionais e não funcionais  
- Rastreabilidade entre requisitos e componentes  
- Controle de mudanças  

### Impacto esperado
- Clareza no desenvolvimento  
- Redução de retrabalho  
- Melhor manutenção  

---

## 3. Alinhamento com Modelos de Maturidade

As melhorias propostas estão alinhadas com:

- :contentReference[oaicite:0]{index=0}  
  - Project Planning (PP)  
  - Requirements Management (REQM)  

- :contentReference[oaicite:1]{index=1}  
  - Gerência de Projetos (GP)  
  - Gerência de Requisitos (GR)  

Esses processos são fundamentais no nível G, garantindo controle básico do projeto.

---

## 4. Conclusão do Plano de Melhoria

A integração entre problemas, priorização e análise arquitetural permitiu identificar claramente os gaps de maturidade.

Embora o sistema apresente alta qualidade técnica, a ausência de processos formais limita sua evolução.

A implementação das práticas propostas permitirá:
- Redução de riscos  
- Aumento da previsibilidade  
- Evolução do nível de maturidade  

---

## 5. Considerações Finais

A análise evidenciou que o sistema possui:

- Alta maturidade arquitetural  
- Baixa maturidade de processo  

Apesar da base técnica sólida, sua evolução depende diretamente da adoção de processos formais.

As melhorias propostas demonstram forte aderência aos modelos CMMI e MPS.BR e representam um passo essencial para a transição de um processo informal para um modelo estruturado de Engenharia de Software.