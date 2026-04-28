# Auditoria de Processo (Eixo IV - GRE, V&V e GQA)

## Diagnóstico do Eixo GRE (Gerência de Requisitos)

Este diagnóstico foi elaborado com base na auditoria técnica realizada no repositório :contentReference[oaicite:0]{index=0}, sendo alinhado às práticas de:

- :contentReference[oaicite:1]{index=1} (Gerência de Requisitos – GRE)  
- :contentReference[oaicite:2]{index=2} (Requirements Management – REQM)  

O foco da análise está na capacidade do projeto em:

- Elicitar requisitos  
- Validar necessidades dos usuários  
- Garantir rastreabilidade até o código final  

---

## Diagnóstico Geral

O projeto apresenta **elevado nível de maturidade em gestão de requisitos**, destacando-se por:

- Transparência no processo  
- Forte uso de automação  
- Integração com ferramentas do GitHub  

O uso de discussões abertas para elicitação e validação assistida por inteligência artificial contribui para garantir que os requisitos sejam compreendidos antes da implementação.

Entretanto, observa-se **informalidade pontual em mudanças menores**, típica de projetos ágeis open source.

---

## 1. Indicadores Positivos

### 1.1 Elicitação via Processos de RFC (Discussions)

O projeto utiliza a aba *Discussions* (categoria *Ideas*) como um repositório de RFC (*Request for Comments*).

**Evidências:**
- Funcionalidades relevantes passam por debate público  
- Discussões estruturadas antes da implementação  

**Alinhamento:**
- Atende à prática de elicitação e validação de requisitos  
- Define o *“o quê”* antes do *“como”*  

---

### 1.2 Rastreabilidade Bidirecional Automatizada

A rastreabilidade entre requisito e implementação é mantida por meio de metadados do GitHub.

**Evidência técnica:**
- Uso de comandos como `Fixes #ID`  
- Links diretos entre Issues, Discussions e PRs  

**Impacto:**
- Permite auditoria completa do ciclo de desenvolvimento  
- Atende aos requisitos do nível G do MPS.BR  

---

### 1.3 Validação Assistida por IA

O projeto utiliza bots de revisão automatizada para validar implementações.

**Funcionamento:**
- A IA analisa se o código atende ao objetivo do requisito  
- Identifica inconsistências entre proposta e implementação  

**Vantagem:**
- Atua como camada adicional de qualidade  
- Reduz risco de desvios funcionais  

---

### 1.4 Padronização de Commits

O projeto adota o padrão **Conventional Commits**:

- `feat:` → novas funcionalidades  
- `fix:` → correções  
- `chore:` → manutenção  

**Benefícios:**
- Organização do histórico  
- Geração automática de changelog  
- Apoio à gerência de configuração  

---

## 2. Pontos de Atenção

### 2.1 Existência de PRs Diretos

Foram identificados Pull Requests sem vínculo com Issues ou Discussions.

**Risco:**
- Quebra da rastreabilidade  
- Dificuldade de auditoria da origem do requisito  

**Ação sugerida:**
- Tornar obrigatória a criação de Issues para mudanças funcionais  

---

### 2.2 Dependência de Conhecimento Tácito

A especificação de requisitos nem sempre está formalizada.

**Problema:**
- Critérios de aceitação não documentados  
- Dependência do conhecimento dos mantenedores  

**Risco:**
- Ambiguidade na validação  
- Dificuldade para novos contribuidores  

---

## 3. Diagnóstico por Leitura Crítica

### 3.1 Projeto (Elicitação)

O projeto demonstra proatividade na coleta de requisitos, utilizando ferramentas colaborativas modernas.

---

### 3.2 Justificativa (Gestão)

A vinculação entre Discussions, Issues e PRs fornece base consistente para decisões técnicas.

---

### 3.3 Resultado (Rastreabilidade)

O sistema permite rastrear:

- Origem do requisito  
- Implementação  
- Validação  

Garantindo transparência e controle do ciclo de vida.

---

## 4. Integração com V&V e GQA

### Verificação e Validação (V&V)

- Uso de CI/CD via GitHub Actions  
- Execução automática de testes  
- Validação contínua de código  

### Garantia da Qualidade (GQA)

- Revisões por pares (code review)  
- Uso de bots de análise  
- Padronização de commits  
- Controle de contribuição (CLA, CONTRIBUTING.md)  

---

## 5. Fechamento Prático

**Diagnóstico final:**

✔ Processo de RFC bem estabelecido  
✔ Rastreabilidade automatizada  
✔ Uso de IA na validação  
✔ Forte integração com práticas de qualidade  

Ponto crítico:
- PRs sem vínculo formal com requisitos  

---

## Conclusão

O projeto :contentReference[oaicite:3]{index=3} apresenta um nível de maturidade em Engenharia de Requisitos superior à média de projetos open source.

Suas práticas demonstram forte aderência aos modelos:

- :contentReference[oaicite:4]{index=4}  
- :contentReference[oaicite:5]{index=5}  

A principal oportunidade de melhoria está na formalização completa da rastreabilidade em todos os Pull Requests.

De forma geral, o projeto possui características que viabilizam sua evolução para uma certificação no nível G do MPS.BR.


# Auditoria de Processo  
## Eixo de Análise: Verificação e Validação (V&V)

---

## 1. Validação vs. Verificação

No contexto da Engenharia de Software, a distinção entre verificação e validação é fundamental:

- **Verificação:** avalia se o software está sendo desenvolvido corretamente, de acordo com especificações, padrões e requisitos definidos.
- **Validação:** avalia se o software atende às necessidades reais do usuário.

No sistema analisado, a verificação foi conduzida por meio da análise de código, workflows, testes automatizados e revisões de Pull Requests. Já a validação foi analisada a partir do comportamento real do sistema em execução, especialmente considerando a interação com modelos de linguagem (LLMs).

---

## 2. Análise da Pasta Workflows

Os workflows do projeto estão organizados na pasta:
- .github/workflows

### Principais workflows analisados:

- `ci.yml.template`
- `pipeline.yml`
- `claude-review-maintainer-prs.yml`

---

## 3. Execução das Verificações

### 3.1 Integração Contínua (CI)

O arquivo `ci.yml.template` executa o seguinte comando:
- pnpm turbo build lint type-check

Funções principais:

- **Build:** verifica se o código é compilável
- **Lint:** garante padrões e boas práticas
- **Type-check:** valida tipagem no TypeScript

Classificação: **Verificação**

---

### 3.2 Pipeline de Testes

O `pipeline.yml` executa múltiplas verificações automatizadas:

- Testes de backend (Jest)
- Testes em diferentes versões de PostgreSQL
- Testes de worker (lógica interna)
- Verificação de lint e formatação

Essas práticas demonstram rigor técnico e controle de qualidade no desenvolvimento.

Classificação: **Verificação**

---

## 4. Execução das Validações

### 4.1 Testes com Integração de LLM

O sistema executa testes com APIs reais de IA:

- OpenAI  
- Anthropic  
- Azure  
- VertexAI  

Comando utilizado:
- pnpm --filter=worker run test:llm-connections-only

Esses testes validam se as respostas das LLMs atendem aos critérios esperados.

Classificação: **Validação**

---

### 4.2 Testes End-to-End (E2E)

Utilizando Playwright, o sistema simula o comportamento do usuário:
- pnpm --filter=web run test:e2e

Esses testes validam:

- Fluxo completo da aplicação  
- Entrega de valor ao usuário final  

Classificação: **Validação**

---

### 4.3 Validação Assistida por Inteligência Artificial

O workflow `claude-review-maintainer-prs.yml` automatiza o processo de revisão:

- A IA analisa Pull Requests  
- Verifica consistência lógica  
- Identifica possíveis falhas  

Essa abordagem combina verificação técnica com validação semântica.

---

## 5. Sistema de Avaliação Interno

O sistema de avaliação do software atua como mecanismo de validação qualitativa.

### 5.1 Validação de Dados (Zod)

Funções como `applyScoreValidation` garantem:

- Integridade dos dados  
- Associação correta entre métricas e entidades  

### 5.2 Rastreabilidade

O sistema permite:

- Identificar origem das métricas  
- Diferenciar avaliações humanas e automatizadas  

Isso possibilita auditorias detalhadas do comportamento do sistema.

---

## 6. Processo de Peer Review

O fluxo identificado no repositório segue o padrão:

Issue → Pull Request → Código Final

Características observadas:

- Uso de prefixos (`feat`, `fix`)
- Discussões técnicas nos PRs
- Vínculo com issues da comunidade

### Diferencial: Revisão por IA

A utilização de revisão automatizada por IA:

- Identifica falhas complexas  
- Complementa testes automatizados  
- Aumenta a confiabilidade do código  

---

## 7. Tabela de Verificação e Validação

| Atividade | Categoria | Justificativa |
|----------|--------|-------------|
| Lint e Type-check | Verificação | Garante padrão e tipagem |
| Testes Unitários | Verificação | Valida funções internas |
| Validação com Zod | Verificação | Garante integridade dos dados |
| Revisão por IA | Verificação | Analisa lógica do código |
| Testes com LLM | Validação | Verifica comportamento real |
| Testes E2E | Validação | Simula uso real |
| Sistema de Scores | Validação | Avalia qualidade da saída |

---

## 8. Diagnóstico Final

Com base na auditoria realizada, o processo de Verificação e Validação apresenta:

### Nível de Maturidade: **Alto**

### Pontos Fortes:

- Forte automação via CI/CD  
- Testes em múltiplos ambientes  
- Validação com APIs reais  
- Uso inovador de IA no processo de revisão  

### Ponto de Atenção:

- Dependência de serviços externos (LLMs), que pode impactar estabilidade  

---

## 9. Conclusão

O processo de Verificação e Validação demonstra elevada maturidade e forte alinhamento com boas práticas da Engenharia de Software.

A combinação de:

- Testes automatizados  
- Validação com dados reais  
- Revisão assistida por inteligência artificial  

posiciona o projeto em um nível avançado de qualidade, compatível com modelos como CMMI e MPS.BR.

A principal oportunidade de melhoria está na mitigação de riscos associados à dependência de serviços externos.