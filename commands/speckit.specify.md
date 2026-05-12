---
description: Criar ou atualizar a especificação de feature a partir de uma descrição em linguagem natural.
strategy: wrap
handoffs:
  - label: Criar Plano Técnico
    agent: speckit.plan
    prompt: Criar um plano para a spec. Estou construindo com...
  - label: Clarificar Requisitos da Spec
    agent: speckit.clarify
    prompt: Clarificar os requisitos da especificação
    send: true
---

<!-- PRESET pt-BR — strategy: wrap -->
<!-- Este wrapper envelopa o command core specify do Spec Kit. -->
<!-- O frontmatter acima (description, handoffs em pt-BR) vence sobre o upstream. -->
<!-- scripts e agent_scripts são herdados automaticamente do command core. -->

<!-- markdownlint-disable MD041 MD031 MD032 MD040 -->

## Diretiva de Idioma — Português Brasileiro (pt-BR)

**INSTRUÇÃO OBRIGATÓRIA**: Todo output gerado por este command DEVE ser em **Português Brasileiro (pt-BR)**.
Identificadores de código, nomes de variáveis e palavras-chave técnicas permanecem em inglês.

**Mapeamento de termos aplicáveis ao command specify**:

| Original | pt-BR |
| -------- | ----- |
| Feature Specification | Especificação de Feature |
| User Story | História de Usuário |
| FR-### | RF-### |
| SC-### | CS-### |
| `[NEEDS CLARIFICATION: ...]` | `[NECESSITA CLARIFICAÇÃO: ...]` |
| Given / When / Then | Dado / Quando / Então |
| Acceptance Scenarios | Cenários de Aceite |
| Edge Cases | Casos de Borda |
| Functional Requirements | Requisitos Funcionais |
| Success Criteria | Critérios de Sucesso |
| Measurable Outcomes | Resultados Mensuráveis |
| Assumptions | Premissas |
| Key Entities | Entidades Principais |
| mandatory | obrigatório |

## Override de Interação — vscode_askQuestions

**INSTRUÇÃO DE OVERRIDE**: O command abaixo instrui a apresentar perguntas de clarificação ao usuário usando tabelas markdown inline (`| Option | Answer | Implications |`) e aguardar resposta via texto. Você **DEVE IGNORAR** essa instrução e **SUBSTITUIR** por chamadas à ferramenta `vscode_askQuestions`.

**Quando encontrar** `[NEEDS CLARIFICATION]` / `[NECESSITA CLARIFICAÇÃO]` markers e o command instruir a apresentar perguntas em tabela markdown:

1. Para cada clarificação (max 3), construa um item no array `questions` de `vscode_askQuestions`:
   - `header`: `"Q[N]: [Tópico]"` — identificador curto
   - `question`: Combine o contexto (citando a seção relevante da spec) com a pergunta específica do marker
   - `options`: Array de 2-5 opções. Cada opção deve ter:
     - `label`: Resposta curta (ex.: "OAuth2/SSO", "90 dias")
     - `description`: Implicações para a feature
     - Marque a opção mais adequada com `recommended: true`
   - `allowFreeformInput`: `true`

2. Exemplo de chamada:
   ```json
   {
     "questions": [
       {
         "header": "Q1: Método de Autenticação",
         "question": "A spec menciona 'login seguro' sem especificar o método. Qual abordagem de autenticação usar?",
         "options": [
           {"label": "OAuth2/SSO", "description": "Enterprise-grade, requer identity provider. Ideal para apps B2B.", "recommended": true},
           {"label": "Email/Senha + MFA", "description": "Abordagem tradicional com multi-fator. Setup mais simples."},
           {"label": "API Keys", "description": "Apenas serviço-a-serviço. Não adequado para usuários finais."}
         ],
         "allowFreeformInput": true
       }
     ]
   }
   ```

3. Processar respostas: usar label da opção selecionada ou texto freeform como resposta.

4. **Apresentar TODAS as clarificações de uma vez** via um único `vscode_askQuestions` com múltiplas questions (não sequencial).

---

{CORE_TEMPLATE}

---

<!-- REFORÇO: (1) Todo output DEVE estar em pt-BR. (2) Perguntas de clarificação DEVEM usar vscode_askQuestions, NUNCA tabelas markdown inline. -->
