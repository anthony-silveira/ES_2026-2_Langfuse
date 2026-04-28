# Plano de Melhoria

## 1. Introdução

A partir da auditoria realizada no ecossistema baseado no Langfuse, observou-se que o sistema apresenta alto nível de maturidade técnica, especialmente nos aspectos arquiteturais, de verificação e validação e na utilização de práticas modernas de desenvolvimento colaborativo.

Entretanto, foram identificadas lacunas relacionadas à formalização e padronização de processos, principalmente nos eixos de Gerência de Projetos (GP), Gerência de Requisitos (GR) e Gestão de Riscos. Essas lacunas não indicam ausência de práticas, mas sim execução parcialmente estruturada, comum em ambientes ágeis e open-source.

A análise da modelagem UML e da arquitetura evidenciou um sistema complexo, caracterizado por:

- Centralidade da entidade Project  
- Fluxos críticos de observabilidade (Trace → Observation → Score)  
- Forte dependência de serviços externos  
- Complexidade concentrada na camada de LLM  

Esse cenário reforça a necessidade de fortalecimento dos processos formais, garantindo maior previsibilidade, controle e evolução sustentável do sistema.

---

## 2. Priorização dos Problemas

### Tabela de Problemas Identificados

| ID  | Problema                                   | Evidência                         | Processo Afetado                  | Impacto                     |
|-----|--------------------------------------------|----------------------------------|----------------------------------|-----------------------------|
| P1  | Ausência de formalização do planejamento   | Planejamento implícito via Issues | Gerência de Projetos (GP)         | Baixa previsibilidade       |
| P2  | Informalidade na gestão de requisitos      | PRs sem Issues vinculadas        | Gerência de Requisitos (GR)       | Lacunas de rastreabilidade  |
| P3  | Complexidade elevada na camada de LLM      | Centralização de lógica crítica  | Arquitetura / Qualidade           | Risco sistêmico             |
| P4  | Forte dependência de serviços externos     | Uso de múltiplas APIs            | Gerência de Projetos (Riscos)     | Baixa resiliência           |
| P5  | Ausência de gestão formal de riscos        | Mitigações não documentadas      | Gerência de Projetos (GP)         | Instabilidade operacional   |

---

## 3. Relação entre Problemas e Prioridade

A priorização foi definida com base no impacto identificado:

- P1 (Planejamento) → **Prioridade Alta**  
- P2 (Requisitos) → **Prioridade Alta**  
- P3 e P4 (Arquitetura e dependências) → **Prioridade Média**  
- P5 (Riscos) → **Prioridade Alta**  

Observa-se que os problemas mais críticos estão relacionados à estruturação dos processos, e não à qualidade técnica do sistema.

---

## 4. Ações de Melhoria

### 4.1 Implantação de Gerência de Projetos (GP)

**Problemas relacionados:**
- P1 — Falta de formalização do planejamento  
- P4 — Dependência de serviços externos  
- P5 — Ausência de gestão de riscos  

**Justificativa**

A auditoria demonstrou que o projeto utiliza práticas ágeis e evidências digitais (Issues, PRs e CI/CD), porém sem formalização explícita de planejamento e controle.

Essa lacuna torna-se crítica devido a:

- Alta dependência de serviços externos (APIs de LLM)  
- Complexidade da arquitetura  
- Necessidade de previsibilidade em releases  

**Ação proposta**

- Planejamento iterativo (Scrum ou Kanban)  
- Definição clara de tarefas e responsáveis  
- Uso de métricas (lead time, cycle time)  
- Monitoramento contínuo via dashboards  
- Gestão formal de riscos (registro, análise e mitigação)  

**Impacto esperado**

- Aumento da previsibilidade  
- Redução de falhas operacionais  
- Melhor controle da evolução do sistema  

---

### 4.2 Implantação de Gerência de Requisitos (GR)

**Problema relacionado:**
- P2 — Informalidade na gestão de requisitos  

**Justificativa**

O sistema já apresenta práticas avançadas de requisitos, como:

- Uso de Discussions (RFCs)  
- Rastreabilidade via Pull Requests  
- Validação assistida por IA  

No entanto, existem lacunas em:

- PRs sem vínculo com Issues  
- Falta de critérios de aceitação  
- Dependência de conhecimento tácito  

**Ação proposta**

- Obrigatoriedade de Issues para mudanças funcionais  
- Definição de critérios de aceitação  
- Padronização de templates  
- Rastreabilidade Issue → PR → Código  
- Controle formal de mudanças  

**Impacto esperado**

- Maior clareza no desenvolvimento  
- Redução de ambiguidades  
- Melhor rastreabilidade  

---

### 4.3 Melhoria da Gestão de Riscos em Sistemas LLM

**Problemas relacionados:**
- P4 — Dependência de serviços externos  
- P5 — Falta de formalização de riscos  

**Justificativa**

Riscos identificados:

- Volatilidade de APIs (OpenAI, Anthropic)  
- Falhas de integração  
- Custos variáveis  
- Prompt injection  

**Ação proposta**

- Registro de riscos (risk log)  
- Estratégias de fallback  
- Versionamento de prompts  
- Monitoramento de custos  
- Plano de contingência  

**Impacto esperado**

- Maior resiliência  
- Redução de impactos operacionais  
- Melhor controle de custos  

---

### 4.4 Redução da Complexidade da Camada de LLM

**Problema relacionado:**
- P3 — Complexidade da camada de LLM  

**Justificativa**

A centralização da lógica cria um ponto crítico de risco e alta complexidade.

**Ação proposta**

- Modularização da camada  
- Testes por provedor  
- Monitoramento de performance  
- Separação de responsabilidades  

**Impacto esperado**

- Redução de acoplamento  
- Maior manutenibilidade  
- Menor risco sistêmico  

---

## 5. Alinhamento com Modelos de Maturidade

As melhorias propostas estão alinhadas com:

### CMMI
- Project Planning (PP)  
- Requirements Management (REQM)  
- Process and Product Quality Assurance (PPQA)  

### MPS.BR
- Gerência de Projetos (GP)  
- Gerência de Requisitos (GR)  
- Garantia da Qualidade (GQA)  

Esses processos são fundamentais para evolução do sistema no nível G (Iniciado) e níveis superiores.

---

## 6. Conclusão do Plano de Melhoria

A análise integrada demonstrou que o sistema possui alta maturidade técnica, porém apresenta lacunas na formalização dos processos.

As ações propostas focam em:

- Estruturação do planejamento  
- Fortalecimento da gestão de requisitos  
- Formalização da gestão de riscos  
- Redução de complexidade técnica  

A implementação dessas melhorias permitirá elevar o nível de maturidade do sistema, garantindo maior controle, previsibilidade e sustentabilidade.

---

## 7. Considerações Finais

O sistema analisado apresenta uma base arquitetural sólida, com forte aderência às práticas modernas de desenvolvimento de software, especialmente no contexto de aplicações baseadas em LLM.

Entretanto, sua evolução sustentável depende da formalização dos processos, reduzindo a dependência de práticas informais.

Dessa forma, o plano de melhoria representa um passo essencial para a transição para um modelo mais maduro, alinhado às boas práticas da Engenharia de Software e aos modelos CMMI e MPS.BR.