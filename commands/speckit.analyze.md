---
description: Realizar uma análise não-destrutiva de consistência e qualidade entre os artefatos spec.md, plan.md e tasks.md após a geração das tarefas.
strategy: wrap
---

<!-- PRESET pt-BR — strategy: wrap -->
<!-- Este wrapper envelopa o command core analyze do Spec Kit. -->
<!-- O frontmatter acima (description em pt-BR) vence sobre o upstream. -->
<!-- scripts e agent_scripts são herdados automaticamente do command core. -->
<!-- Este é um wrapper de IDIOMA apenas — NÃO altera o comportamento do command. -->
<!-- O analyze é read-only e não faz perguntas em tabela markdown, logo NÃO usa vscode_askQuestions. -->

<!-- markdownlint-disable MD041 MD031 MD032 MD040 -->

## Diretiva de Idioma — Português Brasileiro (pt-BR)

**INSTRUÇÃO OBRIGATÓRIA**: Todo output gerado por este command DEVE ser em **Português Brasileiro (pt-BR)**.
Identificadores de código, nomes de variáveis, IDs de findings e palavras-chave técnicas permanecem inalterados; headings, categorias, resumos, recomendações e demais textos saem em pt-BR.

**Mapeamento de termos aplicáveis ao command analyze**:

| Original | pt-BR |
| -------- | ----- |
| Specification Analysis Report | Relatório de Análise da Especificação |
| Category | Categoria |
| Severity | Severidade |
| Location(s) | Localização(ões) |
| Summary | Resumo |
| Recommendation | Recomendação |
| Coverage Summary Table | Tabela de Resumo de Cobertura |
| Requirement Key | Chave do Requisito |
| Has Task? | Tem Tarefa? |
| Task IDs | IDs de Tarefa |
| Notes | Notas |
| Constitution Alignment Issues | Problemas de Alinhamento com a Constituição |
| Unmapped Tasks | Tarefas Não Mapeadas |
| Metrics | Métricas |
| Next Actions | Próximas Ações |
| Total Requirements | Total de Requisitos |
| Total Tasks | Total de Tarefas |
| Coverage % | % de Cobertura |
| Ambiguity Count | Contagem de Ambiguidades |
| Duplication Count | Contagem de Duplicações |
| Critical Issues Count | Contagem de Problemas Críticos |
| Duplication | Duplicação |
| Ambiguity | Ambiguidade |
| Underspecification | Subespecificação |
| Coverage Gaps | Lacunas de Cobertura |
| Inconsistency | Inconsistência |
| Constitution Alignment | Alinhamento com a Constituição |
| CRITICAL / HIGH / MEDIUM / LOW | CRÍTICA / ALTA / MÉDIA / BAIXA |

**Mapeamento de prefixos de IDs** (mesmos das specs pt-BR):

| Original | pt-BR |
| -------- | ----- |
| FR-### | RF-### |
| SC-### | CS-### |

**Instruções adicionais**:

- Os IDs de findings (ex.: `A1`, `C2`) mantêm o formato; apenas o texto de categoria/resumo/recomendação sai em pt-BR.
- A pergunta de remediação ("Would you like me to suggest concrete remediation edits...") DEVE ser feita em pt-BR.
- O bloco de Próximas Ações e as sugestões de comando saem em pt-BR.

---

{CORE_TEMPLATE}

---

<!-- REFORÇO: Todo o output (relatório de análise, tabelas, severidades, métricas, próximas ações e a pergunta de remediação) DEVE estar em Português Brasileiro (pt-BR). -->
