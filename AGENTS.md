# Fluxograma de Workflow de Desenvolvimento de Software

## Contexto e Finalidade

Este fluxograma define o processo de desenvolvimento de software adotado pelo time, estabelecendo uma estrutura clara de comunicação, revisão e entrega entre desenvolvedores e revisadores (Tech Leads/Revisadores). O objetivo é garantir qualidade, alinhamento com padrões e mitigação de riscos técnicos desde as fases iniciais do desenvolvimento.

## Estrutura Principal

O diagrama é dividido em **4 fluxos principais**:

### 1. **Iniciar o dia e ver as pendências do dia** (Lado Esquerdo)
Este é o ponto de partida para o revisador/Tech Lead no início do dia.

**Decisões principais:**
- **Há tarefas para revisar?** - Verifica se existem PRs ou tarefas aguardando revisão
  - **Se SIM**: Procede para análise de prioridades
  - **Se NÃO**: Move para verificação de acompanhamento diário

**Avaliações de prioridade:**
- **Carga cognitiva alta**: Tarefas com lógicas complexas, aprendizado envolvido → **prioridade máxima**
- **Pré-review inadequado**: Tarefas que não tiveram acompanhamento adequado durante desenvolvimento → **prioridade alta**
- **Acompanhamento diário**: Verifica se recebeu follow-ups regulares
  - **Sem acompanhamento**: Agenda pré-review com o desenvolvedor (preferentemente entre 10h-17h)
  - **Com acompanhamento**: Prossegue conforme prioridade

**Consideração especial - Tech Lead de equipe:**
- Se for segunda-feira E for Tech Lead de algum time → Fazer reunião com PO para definir metas

---

### 2. **Passar uma nova tarefa** (Topo Central)
Quando um desenvolvedor fica sem tarefas ou quando é necessário distribuir novo trabalho.

**Decisão 1: Qual o nível de experiência do programador?**

**Para Desenvolvedores Júnior:**

Primeiro, verifique: **A tarefa envolve pesquisa ou aprendizado significativo?**

- **SIM** → Procure outra tarefa sem essa barreira ou escale a decisão
  - Não travar o júnior com pesquisa/aprendizado mantém velocidade de entrega
  - Pode alocar para pleno/sênior se viável, ou deixar para quando houver tempo dedicado a mentoria

- **NÃO** → Delegue uma tarefa com critérios específicos:
  - Esforço máximo de **1 dia** (estimativa do seu ponto de vista)
  - Sem dependências de outras tasks
  - Critérios de aceite **claros e explícitos**
  - Mockup visual (se houver componentes de front-end)
  - Baseada em conhecimento que o júnior já possui

---

### 3. **Fazer pré-review** (Lado Central)
Este é o processo de revisão antes da revisão final. Responsabilidade do revisador.

**Passos:**
1. **Responder dúvidas iniciais** do desenvolvedor (com tempo limitado)
   - Júnior: **1 hora** disponível
   - Pleno/Sênior: **30 minutos** disponível
2. **Revisar o PR/código:**
   - Abrir a lista de arquivos alterados no GitHub/IDE
   - Revisar um arquivo por vez
   - Marcar checkbox de "revisado" para cada arquivo
   - Priorizar revisão do conteúdo mais difícil primeiro

3. **Fornecer feedback ao desenvolvedor**
   - Solicitação de mudanças pequenas (1-3 min): **Executar imediatamente**
   - Solicitação de mudanças médias/grandes (+3 min): **Registrar na lista de pendências**

**Critério de mudanças solicitadas:**

O fluxo de decisão segue uma hierarquia clara baseada na **filosofia de máxima entrega sem travar desenvolvedores**:

1. **Tipo de motivo (Fatores técnicos críticos - Não se negocia):**
   - **Padrão já estabelecido foi violado** → **SEMPRE Solicite a alteração**
     - Manter consistência arquitetural é crítico para o projeto
     - Aplicável a todos os níveis de experiência

   - **Problema de segurança** → **SEMPRE Solicite a alteração**
     - Riscos de segurança não podem ser adiados
     - Prioridade máxima antes de qualquer deploy
     - Aplicável a todos os níveis de experiência

2. **Outras razões (performance, qualidade, refatoração, otimização):**

   A decisão depende do **nível de experiência do desenvolvedor**:

   - **Desenvolvedor Júnior** → **SEMPRE Adicione ao backlog**
     - **Nunca travar com aprendizado** é a regra
     - Se a mudança envolve aprendizado significativo, não é obrigatória
     - Foco em manter velocidade: código que funciona > código perfeito
     - O júnior construi experiência com padrões, não em edge cases

   - **Desenvolvedor Pleno/Sênior** → Use as **Perguntas de Contexto** para decidir:

     **Perguntas de Contexto** (aplique em ordem para avaliar prioridade):

     1. **"Se eu subir isso hoje, alguém será beneficiado?"**
        - Entender o impacto real: é performance percebida pelos usuários? É arquitetura que impacta manutenção futura?
        - **NÃO**: Provavelmente é detalhe técnico ou edge case → Adicione ao backlog
        - **SIM**: Prossiga para próxima pergunta

     2. **"Esse problema vai piorar significativamente se não for corrigido nos próximos sprints?"**
        - Avaliar criticidade temporal: é débito técnico que cresce exponencialmente ou é estável?
        - **SIM** (crescimento acelerado, impacto futuro): Pode justificar solicitar alteração
        - **NÃO** (problema controlado, não cresce): Adicione ao backlog para sprint de débito técnico

     3. **"Quanto tempo vai levar para corrigir AGORA vs. deixar para depois?"**
        - Estimar custo relativo: é rápido agora? Ficará mais caro depois?
        - **AGORA < 30 min** E respostas anteriores apontam benefício: **Solicite a alteração**
        - **AGORA >= 30 min**: Considere deixar para backlog, mesmo com benefício potencial
        - **Muito mais caro depois** (ex: refatoração de base de dados que será pior depois): Solicite a alteração se AGORA < 1 hora

     4. **"Essa mudança depende de outras alterações ou contexto que ainda não está pronto?"**
        - Avaliar bloqueadores: a correção faz sentido isoladamente ou é parte de refatoração maior?
        - **SIM (precisa de contexto maior)**: Adicione ao backlog como parte de épica/feature maior
        - **NÃO (pode ser corrigido isoladamente)**: Considere a próxima pergunta

     5. **"Qual é o impacto na manutenibilidade futura do projeto?"**
        - Avaliar débito técnico: vai dificultar implementações futuras? Cria precedente ruim?
        - **Alto impacto** (violação de padrão não-crítico, código confuso, duplicação sistemática): Solicite se custo <= 30 min
        - **Baixo impacto** (detalhe isolado, edge case, padrão emergente): Adicione ao backlog

     **Perguntas adicionais para performance/arquitetura** (idempotentes e stateless; use-as quando houver suspeita de custo alto):
     6. **"A degradação é observável agora (métricas, p95/p99, CPU/memória) ou é apenas hipótese?"**
        - Observável com dado concreto → Inclina a solicitar se o custo for baixo ou risco crescer rápido
        - Apenas hipótese sem evidência → Inclina a backlog até medir
     7. **"Há risco de saturação em curto prazo (picos previstos, datas de alta demanda, limites de infraestrutura)?"**
        - Saturação provável em breve → Solicitar se correção couber no limite de tempo aceitável
        - Sem risco imediato → Backlog ou correção planejada
     8. **"Esse ponto viola um padrão arquitetural já estabelecido (contrato de módulo, fronteira de contexto, forma de injeção, observabilidade obrigatória)?"**
        - Violação de padrão conhecido → Solicitar (mesmo que não seja segurança), pois fere consistência
        - Alinhado ao padrão → Trate como otimização/performance normal
     9. **"A correção tem escopo local e baixo risco de regressão ou exige refatoração estrutural ampla?"**
        - Escopo local e reversível → Pode solicitar agora se custo <= 30-60 min
        - Refatoração ampla sem urgência → Backlog para épica/débito técnico
     10. **"Existe alternativa rápida de mitigação (feature flag, configuração, limite) que evita impacto até a solução completa?"**
         - Mitigação rápida disponível → Solicitar mitigação agora + backlog para solução completa
         - Sem mitigação e risco alto → Solicitar solução agora se custo comportar; caso contrário, escalar prioridade

     **Resumo da Decisão:**
     - **Se NÃO vai atrasar significativamente** (< 30 min) E há benefício claro → **Solicite a alteração**
       - Desenvolvedor já domina os fundamentos
       - Feedback sobre sutilezas é bem absorvido
       - O projeto sai beneficiado sem custo de tempo

     - **Se VAI atrasar significativamente** (>= 30 min) OU é detalhe isolado → **Adicione ao backlog**
       - Melhorias não-críticas podem ser adicionadas em sprints de refatoração
       - Evita bloqueio desnecessário
       - Mantém momentum de entrega da feature

---

### 4. **Minha tarefa será pré-revisada** (Lado Direito)
Fluxo do ponto de vista do desenvolvedor que submete sua tarefa para pré-review.

**Preparação:**
1. Verificar se é o **primeiro contato do revisador** com essa tarefa
   - **SIM**: Contextualizar o revisador adequadamente (explicar background, decisões, desafios)
   - **NÃO**: Entrega resumida das alterações

2. **Entregar ao revisador:**
   - Resumo das alterações desde o último pré-review
   - Lista de pendências para conclusão da tarefa

3. **Durante o desenvolvimento:**
   - Identificar **riscos técnicos** percebidos
   - Registrar na lista de pendências para discussão com revisador
   - Exemplos:
     - "O campo X pode precisar de índice, mas ainda não validei"
     - "A abordagem que escolhi não segue o padrão do time para services/usecases. O que você acha?"

---

## 4. **Estou desenvolvendo a minha tarefa** (Lado Extremo Direito)
Fluxo do desenvolvedor durante a implementação.

**Acompanhamento contínuo:**
- Revisar código que está sendo desenvolvido
- Identificar riscos técnicos (performance, segurança, padrões)
- **Registrar na lista de pendências** qualquer risco ou dúvida para discussão posterior com o revisador

**Feedback loop:**
- Após pré-review, receber solicitações de mudanças
- Classificar por tamanho e executar conforme prioridade

---

## Princípios-Chave do Processo

1. **Comunicação Early**: Pré-reviews acontecem durante o desenvolvimento, não apenas ao final
2. **Priorização de Risco**: Tarefas com alta complexidade recebem mais atenção e tempo de review
3. **Diferenciação por Senioridade**: Tempo, critérios de alocação e feedback variam conforme experiência
4. **Nunca Travar com Aprendizado**: Juniores não devem ser bloqueados por barreiras de pesquisa/aprendizado
5. **Máxima Entrega**: Código que funciona correto é melhor que código perfeito mas atrasado
6. **Riscos Críticos**: Padrões violados e segurança são não-negociáveis em qualquer nível
7. **Impacto no Projeto**: Para desenvolvedores sênior, considere o custo de tempo vs. benefício
8. **Documentação Contínua**: Manutenção de listas de pendências e contextualizações
9. **Feedback Contextual**: Mudanças pequenas são resolvidas na hora; maiores são registradas conforme prioridade

## Exemplos Práticos de Aplicação

### Cenário 1: Violação de Padrão Arquitetural
**Situação**: Um desenvolvedor (qualquer nível) criou um serviço que não segue o padrão de injeção de dependência do time

**Decisão**: Solicite a alteração (independente do nível)
- É um padrão estabelecido que garante consistência
- Todos devem seguir, independente de experiência
- Risco técnico crítico que impacta o projeto como um todo

### Cenário 2: Vulnerabilidade de Segurança
**Situação**: SQL injection potencial no código de acesso a dados

**Decisão**: Solicite a alteração (independente do nível)
- Segurança é crítica e não pode ser adiada
- Deve ser corrigido antes de qualquer deploy
- Risco existencial do projeto

### Cenário 3: Sugestão de Otimização de Performance para Júnior
**Situação**: Um desenvolvedor júnior fez uma query que poderia ter um índice para melhorar performance

**Decisão**: Adicione ao backlog
- **Não travar com aprendizado**: otimização de índices envolve pesquisa/aprendizado
- O código já funciona corretamente
- Pode ser feita em sprint de otimização futura
- Mantém o júnior produtivo sem bloqueios

### Cenário 4: Sugestão de Melhoria Simples para Sênior
**Situação**: Um desenvolvedor sênior poderia melhorar a legibilidade de uma função complexa com poucos minutos de trabalho

**Decisão**: Solicite a alteração
- Não vai atrasar significativamente
- Sênior já domina a abordagem
- Benefício de qualidade justifica o pequeno custo

### Cenário 5: Refatoração Grande para Sênior
**Situação**: Um desenvolvedor sênior poderia refatorar toda uma camada de serviços para melhor organização (~2-3 horas)

**Decisão**: Adicione ao backlog
- Vai atrasar significativamente a entrega atual
- Refatoração é melhoria, não crítico
- Pode ser feita em sprint dedicado a débito técnico
- Mantém momentum de entrega da feature

### Cenário 6: Alocação de Tarefa com Aprendizado
**Situação**: Precisa integrar uma nova biblioteca que ninguém do time conhece

**Opção A - Júnior está disponível:**
- **Não alocar para o júnior**
- Procure outra tarefa para ele
- Aloque para pleno/sênior ou deixe para quando tiver tempo de mentoria dedicado

**Opção B - Apenas júnior disponível:**
- Escale a decisão
- Considere se vale a pena o tempo de aprendizado vs. urgência
- Se alocar, deve ser com suporte próximo (pair programming)

## Benefícios

- **Máxima entrega**: Não travar desenvolvedores com barreiras mantém velocidade
- **Reduz riscos críticos**: Padrões e segurança são verificados; edge cases podem esperar
- **Acelera desenvolvimento**: Clareza total sobre quando solicitar mudança vs. adicionar ao backlog
- **Aproveita expertise**: Juniores em tarefas que dominam, sênior em tarefas complexas
- **Evita burnout**: Juniores não travados com aprendizado, sênior não sobrecarregado com feedback
- **Padronização onde importa**: Padrões críticos são enforçados; melhorias são adicionadas iterativamente
- **Mentoria natural**: Juniores aprendem pelos padrões que precisam seguir, não por feedback detalhado
- **Débito técnico controlado**: Melhorias vão para backlog (rastreado), não são perdidas
- **Equilíbrio qualidade-velocidade**: Código correto e funcional agora > código perfeito mas atrasado
