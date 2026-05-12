---
description: Identificar áreas subespecificadas na spec da feature ativa, fazendo até 5 perguntas de clarificação direcionadas e codificando as respostas de volta na spec.
strategy: wrap
handoffs:
  - label: Criar Plano Técnico
    agent: speckit.plan
    prompt: Criar um plano para a spec. Estou construindo com...
---

<!-- PRESET pt-BR — strategy: wrap -->
<!-- Este wrapper envelopa o command core clarify do Spec Kit. -->
<!-- O frontmatter acima (description, handoffs em pt-BR) vence sobre o upstream. -->
<!-- scripts e agent_scripts são herdados automaticamente do command core. -->

<!-- markdownlint-disable MD041 MD031 MD032 MD040 -->

## Diretiva de Idioma — Português Brasileiro (pt-BR)

**INSTRUÇÃO OBRIGATÓRIA**: Todo output gerado por este command DEVE ser em **Português Brasileiro (pt-BR)**.
Identificadores de código, nomes de variáveis e palavras-chave técnicas permanecem em inglês.

**Mapeamento de termos aplicáveis ao command clarify**:

| Original | pt-BR |
| -------- | ----- |
| Clarifications | Clarificações |
| Session | Sessão |
| Resolved | Resolvido |
| Deferred | Adiado |
| Clear | Claro |
| Outstanding | Pendente |
| Functional Requirements | Requisitos Funcionais |
| Success Criteria | Critérios de Sucesso |
| Edge Cases | Casos de Borda |
| Coverage summary | Resumo de cobertura |
| Sections touched | Seções alteradas |

## Override de Interação — vscode_askQuestions

**INSTRUÇÃO DE OVERRIDE**: O command abaixo instrui a apresentar perguntas de clarificação ao usuário **uma por vez** usando tabelas markdown (`| Option | Description |`) com `**Recommended:**` e aguardar resposta via texto livre. Você **DEVE IGNORAR** essa instrução e **SUBSTITUIR** por chamadas à ferramenta `vscode_askQuestions`.

**Regras de substituição**:

1. **UMA pergunta por vez** — manter o loop sequencial do clarify, mas usar `vscode_askQuestions` com um único item no array `questions` em cada chamada.

2. Para cada pergunta, construir a chamada `vscode_askQuestions`:
   - `header`: Tópico curto (ex.: "Política de Retenção de Dados")
   - `question`: Iniciar com `**Recomendado: [Opção]** — [1-2 frases de raciocínio].\n\n[Pergunta específica]`
   - `options`: Array de 2-5 opções. Cada uma com:
     - `label`: Resposta curta e descritiva
     - `description`: Implicações para a feature
     - `recommended: true` na melhor opção
   - `allowFreeformInput`: `true`

3. Exemplo de chamada:
   ```json
   {
     "questions": [{
       "header": "Política de Retenção de Dados",
       "question": "**Recomendado: 1 ano** — equilibra necessidades de analytics com custos de armazenamento e conformidade LGPD.\n\nPor quanto tempo os dados do usuário devem ser retidos?",
       "options": [
         {"label": "90 dias", "description": "Armazenamento mínimo, capacidade limitada de analytics"},
         {"label": "1 ano", "description": "Bom equilíbrio para analytics e trilhas de auditoria", "recommended": true},
         {"label": "Indefinido", "description": "Nunca deletado. Requer justificativa LGPD/GDPR"}
       ],
       "allowFreeformInput": true
     }]
   }
   ```

4. Para perguntas de resposta curta (sem opções discretas significativas):
   - `header`: Tópico da pergunta
   - `question`: `**Sugerido: [resposta proposta]** — [raciocínio breve].\n\nForneça sua resposta (máx 5 palavras) ou aceite a sugestão.`
   - Sem `options` — deixar usuário digitar livremente
   - `allowFreeformInput`: `true`

5. Processar respostas:
   - Opção selecionada → usar label da opção
   - Texto freeform → usar como resposta (validar <=5 palavras para short-answer)
   - Pergunta pulada / sem resposta → aceitar recomendação/sugestão
   - Sinais de término ("done", "pronto", "sem mais") → parar loop sem registrar resposta da pergunta atual

---

{CORE_TEMPLATE}

---

<!-- REFORÇO: (1) Todo output DEVE estar em pt-BR. (2) Cada pergunta de clarificação DEVE usar vscode_askQuestions com UM item por vez, NUNCA tabelas markdown inline. (3) Respeitar máximo de 5 perguntas. -->
