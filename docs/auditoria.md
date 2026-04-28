# Processo de Desenvolvimento (Eixo I – GPR)

## 1. Ciclo de Vida e Frequência de Releases

Diferente do modelo Cascata, marcado pela rigidez e execução sequencial de fases, o projeto analisado adota um **Ciclo de Vida Ágil (Iterativo e Incremental)**. Esse modelo prioriza ciclos curtos de desenvolvimento, feedback contínuo e entrega frequente de valor.

### 1.1 Tabela de Periodicidade de Releases

| Versão     | Data de Publicação | Intervalo entre Releases | Natureza da Alteração |
|:----------:|:-----------------:|:------------------------:|:----------------------|
| v3.163.0   | 31/03/2026        | —                        | Minor — Nova funcionalidade / melhoria |
| v3.164.0   | 07/04/2026        | 7 dias                   | Minor — Nova funcionalidade / melhoria |
| v3.165.0   | 07/04/2026        | —                        | Minor — Nova funcionalidade / melhoria |
| v3.166.0   | 07/04/2026        | —                        | Minor — Nova funcionalidade / melhoria |
| v3.167.0   | 07/04/2026        | —                        | Minor — Nova funcionalidade / melhoria |
| v3.167.1   | 07/04/2026        | —                        | Patch — Correção de bugs |
| v3.167.2   | 07/04/2026        | —                        | Patch — Correção de bugs |
| v3.167.3   | 07/04/2026        | —                        | Patch — Correção de bugs |
| v3.167.4   | 07/04/2026        | —                        | Patch — Correção de bugs |
| v3.168.0   | 14/04/2026        | 7 dias                   | Minor — Nova funcionalidade / melhoria |
| v3.169.0   | 14/04/2026        | —                        | Minor — Nova funcionalidade / melhoria |
| v3.170.0-0 | 21/04/2026        | 7 dias                   | Release de teste (observabilidade) |
| v3.170.0   | 23/04/2026        | 2 dias                   | Minor — Nova funcionalidade / melhoria |
| v3.171.0   | 28/04/2026        | 5 dias                   | Minor — Nova funcionalidade / melhoria |

**Nota:**  
As datas foram estimadas com base nos intervalos relativos informados, considerando como referência 28/04/2026. A classificação segue o padrão de versionamento semântico (SemVer):
- Major: quebra de compatibilidade  
- Minor: nova funcionalidade  
- Patch: correção de bugs  

### Análise do Padrão

O repositório apresenta um comportamento altamente ágil e adaptativo. A predominância de intervalos curtos (inferiores a 15 dias) evidencia:

- Entregas incrementais contínuas  
- Correções rápidas  
- Evolução progressiva do sistema  

Esse padrão é característico de ambientes com integração contínua e ciclos rápidos de feedback.

---

## 2. Roadmap e Planejamento Incremental

A Gerência de Projetos (GPR), em ambientes open source, é conduzida por meio de evidências digitais disponíveis no repositório.

### Estrutura do Roadmap

O planejamento do projeto é realizado por meio de:

- Backlog de Issues  
- Pull Requests (PRs)  
- Labels de priorização  

### Evidências de Planejamento

- Uso de etiquetas (labels) como *High Priority* e *Enhancement*  
- Organização de tarefas via Issues  
- Associação entre Issue → PR → Código  

Esse fluxo permite uma rastreabilidade implícita entre planejamento e execução.

### Alinhamento Estratégico

O roadmap atua como um elemento organizador do desenvolvimento, conectando:

- Requisitos  
- Implementação  
- Validação  

---

## 3. Gerência de Riscos em Sistemas LLM

Sistemas baseados em modelos de linguagem (LLMs) apresentam riscos técnicos específicos, decorrentes de sua natureza não determinística e dependência de serviços externos.

### Principais Riscos Identificados

- Mudanças em APIs de terceiros  
- Alucinações e inconsistências do modelo  
- Vulnerabilidades de prompt injection  
- Custos variáveis de execução  

### Estratégias de Mitigação Observadas

- Uso de avaliações automatizadas (LLM Evals)  
- Aplicação de datasets de validação (Gold Standard)  
- Monitoramento de execução e respostas  
- Controle de uso e custos  

---

## 4. Análise Crítica de Maturidade (MPS.BR – Nível G)

O nível G do MPS.BR enfatiza:

- Gerência de Projetos (GPR)  
- Gerência de Requisitos (GRE)  

### 4.1 Pontos Fortes

- Aderência ao processo  
  - Uso do CONTRIBUTING.md  
  - Templates padronizados  

- Verificação e Validação (V&V)  
  - CI/CD com GitHub Actions  
  - Execução automática de testes e lint  

- Rastreabilidade  
  - Relação entre Issue → PR → Código  

---

### 4.2 Lacunas Identificadas

- Ausência de estimativas formais de esforço  
- Falta de formalização de planos de rollback  
- Ausência de documentação estruturada de riscos  

---

## 5. Conclusão

O projeto apresenta elevado nível de organização e aderência às práticas modernas de desenvolvimento ágil.

A frequência de releases, o uso de backlog estruturado e a integração com pipelines de CI/CD evidenciam maturidade técnica significativa.

No entanto, sob a perspectiva do MPS.BR nível G, ainda existem lacunas relacionadas à formalização de processos, especialmente em:

- Planejamento estruturado  
- Estimativas de esforço  
- Gestão formal de riscos  

A adoção dessas práticas contribuiria para elevar o nível de maturidade do projeto, tornando-o mais previsível, controlado e alinhado às boas práticas da Engenharia de Software.