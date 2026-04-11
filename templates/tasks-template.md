---
description: "Template de lista de tarefas para implementação de feature"
---

# Tarefas: [NOME DA FEATURE]

**Entrada**: Documentos de design de `/specs/[###-feature-name]/`
**Pré-requisitos**: plan.md (obrigatório), spec.md (obrigatório para histórias de usuário), research.md, data-model.md, contracts/

**Testes**: Os exemplos abaixo incluem tarefas de teste. Testes são OPCIONAIS — inclua-os apenas se explicitamente solicitado na especificação da feature.

**Organização**: As tarefas são agrupadas por história de usuário para permitir implementação e teste independentes de cada história.

## Formato: `[ID] [P?] [História] Descrição`

- **[P]**: Pode rodar em paralelo (arquivos diferentes, sem dependências)
- **[História]**: A qual história de usuário esta tarefa pertence (ex.: HU1, HU2, HU3)
- Inclua caminhos de arquivo exatos nas descrições

## Convenções de Caminhos

- **Projeto único**: `src/`, `tests/` na raiz do repositório
- **Aplicação web**: `backend/src/`, `frontend/src/`
- **Mobile**: `api/src/`, `ios/src/` ou `android/src/`
- Os caminhos abaixo assumem projeto único — ajuste com base na estrutura do plan.md

<!--
  ============================================================================
  IMPORTANTE: As tarefas abaixo são TAREFAS DE EXEMPLO apenas para fins ilustrativos.

  O comando /speckit.tasks DEVE substituí-las por tarefas reais baseadas em:
  - Histórias de usuário do spec.md (com suas prioridades P1, P2, P3...)
  - Requisitos de feature do plan.md
  - Entidades do data-model.md
  - Endpoints dos contracts/

  As tarefas DEVEM ser organizadas por história de usuário para que cada história possa ser:
  - Implementada independentemente
  - Testada independentemente
  - Entregue como incremento de MVP

  NÃO mantenha estas tarefas de exemplo no arquivo tasks.md gerado.
  ============================================================================
-->

## Fase 1: Setup (Infraestrutura Compartilhada)

**Objetivo**: Inicialização do projeto e estrutura básica

- [ ] T001 Criar estrutura de projeto conforme plano de implementação
- [ ] T002 Inicializar projeto [linguagem] com dependências do [framework]
- [ ] T003 [P] Configurar ferramentas de linting e formatação

---

## Fase 2: Fundacional (Pré-requisitos Bloqueantes)

**Objetivo**: Infraestrutura central que DEVE estar completa antes de qualquer história de usuário

**⚠️ CRÍTICO**: Nenhum trabalho de história de usuário pode começar até que esta fase esteja completa

Exemplos de tarefas fundacionais (ajuste conforme seu projeto):

- [ ] T004 Configurar schema do banco de dados e framework de migrações
- [ ] T005 [P] Implementar framework de autenticação/autorização
- [ ] T006 [P] Configurar roteamento de API e estrutura de middleware
- [ ] T007 Criar modelos/entidades base dos quais todas as histórias dependem
- [ ] T008 Configurar tratamento de erros e infraestrutura de logging
- [ ] T009 Configurar gerenciamento de configurações de ambiente

**Checkpoint**: Fundação pronta — implementação das histórias de usuário pode começar em paralelo

---

## Fase 3: História de Usuário 1 — [Título] (Prioridade: P1) 🎯 MVP

**Objetivo**: [Breve descrição do que esta história entrega]

**Teste Independente**: [Como verificar que esta história funciona por conta própria]

### Testes da História de Usuário 1 (OPCIONAL — apenas se testes forem solicitados) ⚠️

> **NOTA: Escreva estes testes PRIMEIRO e certifique-se de que FALHAM antes da implementação**

- [ ] T010 [P] [HU1] Teste de contrato para [endpoint] em tests/contract/test_[nome].py
- [ ] T011 [P] [HU1] Teste de integração para [jornada do usuário] em tests/integration/test_[nome].py

### Implementação da História de Usuário 1

- [ ] T012 [P] [HU1] Criar modelo [Entidade1] em src/models/[entidade1].py
- [ ] T013 [P] [HU1] Criar modelo [Entidade2] em src/models/[entidade2].py
- [ ] T014 [HU1] Implementar [Serviço] em src/services/[servico].py (depende de T012, T013)
- [ ] T015 [HU1] Implementar [endpoint/feature] em src/[local]/[arquivo].py
- [ ] T016 [HU1] Adicionar validação e tratamento de erros
- [ ] T017 [HU1] Adicionar logging para operações da história de usuário 1

**Checkpoint**: Neste ponto, a História de Usuário 1 deve ser totalmente funcional e testável de forma independente

---

## Fase 4: História de Usuário 2 — [Título] (Prioridade: P2)

**Objetivo**: [Breve descrição do que esta história entrega]

**Teste Independente**: [Como verificar que esta história funciona por conta própria]

### Testes da História de Usuário 2 (OPCIONAL — apenas se testes forem solicitados) ⚠️

- [ ] T018 [P] [HU2] Teste de contrato para [endpoint] em tests/contract/test_[nome].py
- [ ] T019 [P] [HU2] Teste de integração para [jornada do usuário] em tests/integration/test_[nome].py

### Implementação da História de Usuário 2

- [ ] T020 [P] [HU2] Criar modelo [Entidade] em src/models/[entidade].py
- [ ] T021 [HU2] Implementar [Serviço] em src/services/[servico].py
- [ ] T022 [HU2] Implementar [endpoint/feature] em src/[local]/[arquivo].py
- [ ] T023 [HU2] Integrar com componentes da História de Usuário 1 (se necessário)

**Checkpoint**: Neste ponto, as Histórias de Usuário 1 E 2 devem funcionar de forma independente

---

## Fase 5: História de Usuário 3 — [Título] (Prioridade: P3)

**Objetivo**: [Breve descrição do que esta história entrega]

**Teste Independente**: [Como verificar que esta história funciona por conta própria]

### Testes da História de Usuário 3 (OPCIONAL — apenas se testes forem solicitados) ⚠️

- [ ] T024 [P] [HU3] Teste de contrato para [endpoint] em tests/contract/test_[nome].py
- [ ] T025 [P] [HU3] Teste de integração para [jornada do usuário] em tests/integration/test_[nome].py

### Implementação da História de Usuário 3

- [ ] T026 [P] [HU3] Criar modelo [Entidade] em src/models/[entidade].py
- [ ] T027 [HU3] Implementar [Serviço] em src/services/[servico].py
- [ ] T028 [HU3] Implementar [endpoint/feature] em src/[local]/[arquivo].py

**Checkpoint**: Todas as histórias de usuário devem agora ser funcionais de forma independente

---

[Adicione mais fases de histórias de usuário conforme necessário, seguindo o mesmo padrão]

---

## Fase N: Polimento e Aspectos Transversais

**Objetivo**: Melhorias que afetam múltiplas histórias de usuário

- [ ] TXXX [P] Atualizações de documentação em docs/
- [ ] TXXX Limpeza e refatoração de código
- [ ] TXXX Otimização de desempenho em todas as histórias
- [ ] TXXX [P] Testes unitários adicionais (se solicitado) em tests/unit/
- [ ] TXXX Fortalecimento de segurança
- [ ] TXXX Executar validação do quickstart.md

---

## Dependências e Ordem de Execução

### Dependências entre Fases

- **Setup (Fase 1)**: Sem dependências — pode começar imediatamente
- **Fundacional (Fase 2)**: Depende da conclusão do Setup — BLOQUEIA todas as histórias de usuário
- **Histórias de Usuário (Fase 3+)**: Todas dependem da conclusão da fase Fundacional
  - As histórias podem prosseguir em paralelo (se houver equipe suficiente)
  - Ou sequencialmente em ordem de prioridade (P1 → P2 → P3)
- **Polimento (Fase Final)**: Depende da conclusão de todas as histórias desejadas

### Dependências entre Histórias de Usuário

- **História de Usuário 1 (P1)**: Pode começar após Fundacional (Fase 2) — sem dependências de outras histórias
- **História de Usuário 2 (P2)**: Pode começar após Fundacional (Fase 2) — pode integrar com HU1 mas deve ser testável independentemente
- **História de Usuário 3 (P3)**: Pode começar após Fundacional (Fase 2) — pode integrar com HU1/HU2 mas deve ser testável independentemente

### Dentro de Cada História de Usuário

- Testes (se incluídos) DEVEM ser escritos e FALHAR antes da implementação
- Modelos antes de serviços
- Serviços antes de endpoints
- Implementação central antes da integração
- História completa antes de passar para a próxima prioridade

### Oportunidades de Paralelismo

- Todas as tarefas de Setup marcadas [P] podem rodar em paralelo
- Todas as tarefas Fundacionais marcadas [P] podem rodar em paralelo (dentro da Fase 2)
- Após a conclusão da fase Fundacional, todas as histórias podem começar em paralelo (se a equipe permitir)
- Todos os testes de uma história marcados [P] podem rodar em paralelo
- Modelos dentro de uma história marcados [P] podem rodar em paralelo
- Histórias diferentes podem ser trabalhadas em paralelo por membros diferentes da equipe

---

## Exemplo de Paralelismo: História de Usuário 1

```bash
# Iniciar todos os testes da HU1 juntos (se testes solicitados):
Tarefa: "Teste de contrato para [endpoint] em tests/contract/test_[nome].py"
Tarefa: "Teste de integração para [jornada do usuário] em tests/integration/test_[nome].py"

# Iniciar todos os modelos da HU1 juntos:
Tarefa: "Criar modelo [Entidade1] em src/models/[entidade1].py"
Tarefa: "Criar modelo [Entidade2] em src/models/[entidade2].py"
```

---

## Estratégia de Implementação

### MVP Primeiro (Apenas História de Usuário 1)

1. Concluir Fase 1: Setup
2. Concluir Fase 2: Fundacional (CRÍTICO — bloqueia todas as histórias)
3. Concluir Fase 3: História de Usuário 1
4. **PARAR e VALIDAR**: Testar a HU1 de forma independente
5. Fazer deploy/demo se estiver pronto

### Entrega Incremental

1. Concluir Setup + Fundacional → Fundação pronta
2. Adicionar HU1 → Testar independentemente → Deploy/Demo (MVP!)
3. Adicionar HU2 → Testar independentemente → Deploy/Demo
4. Adicionar HU3 → Testar independentemente → Deploy/Demo
5. Cada história adiciona valor sem quebrar as anteriores

### Estratégia para Equipes Paralelas

Com múltiplos desenvolvedores:

1. Equipe conclui Setup + Fundacional juntos
2. Após a Fundacional concluída:
   - Desenvolvedor A: História de Usuário 1
   - Desenvolvedor B: História de Usuário 2
   - Desenvolvedor C: História de Usuário 3
3. Histórias concluídas e integradas independentemente

---

## Notas

- Tarefas com [P] = arquivos diferentes, sem dependências
- Rótulo [História] mapeia tarefa para história específica para rastreabilidade
- Cada história de usuário deve ser independentemente concluível e testável
- Verificar se os testes falham antes de implementar
- Fazer commit após cada tarefa ou grupo lógico
- Parar em qualquer checkpoint para validar a história de forma independente
- Evitar: tarefas vagas, conflitos no mesmo arquivo, dependências cross-história que quebrem a independência