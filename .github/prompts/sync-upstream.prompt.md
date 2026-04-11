---
description: "Sincronizar o preset pt-BR com a versão mais recente do Spec Kit upstream. Baixa templates e commands do repositório oficial, compara com os locais, identifica diferenças e aplica as atualizações preservando traduções e integrações customizadas."
name: "Sync Upstream Spec Kit"
argument-hint: "Versão do Spec Kit (ex: 0.7.0) ou deixe vazio para usar main"
agent: "agent"
tools:
  - fetch_webpage
  - run_in_terminal
  - read_file
  - replace_string_in_file
  - create_file
  - vscode_askQuestions
---

# Sincronizar Preset pt-BR com Upstream Spec Kit

Você é um agente de manutenção para o preset `spec-kit-preset-pt-br`. Sua missão é comparar os arquivos locais do preset com a versão mais recente do upstream (github/spec-kit) e aplicar as atualizações necessárias preservando as customizações.

## Contexto do Preset

Este preset possui dois tipos de arquivo com estratégias de merge diferentes:

### Templates (6 arquivos) — Estratégia: TRADUZIR NOVIDADES
Arquivos que são **traduções completas** dos templates upstream. Headings e todo o conteúdo estão em pt-BR.

| Local | Upstream |
|-------|----------|
| `templates/spec-template.md` | `templates/spec-template.md` |
| `templates/plan-template.md` | `templates/plan-template.md` |
| `templates/tasks-template.md` | `templates/tasks-template.md` |
| `templates/checklist-template.md` | `templates/checklist-template.md` |
| `templates/constitution-template.md` | `templates/constitution-template.md` |
| `templates/agent-file-template.md` | `templates/agent-file-template.md` |

**Regra de merge**: Toda nova seção ou placeholder adicionado upstream deve ser traduzido para pt-BR e inserido na posição correta. Seções existentes traduzidas devem ser preservadas. Identificadores de código, nomes de variáveis e palavras-chave técnicas permanecem em inglês.

### Commands (2 arquivos) — Estratégia: MERGE CIRÚRGICO
Arquivos que são **cópias do upstream com modificação pontual** no formato de perguntas ao usuário (markdown tables → `vscode_askQuestions`).

| Local | Upstream |
|-------|----------|
| `commands/speckit.specify.md` | `templates/commands/specify.md` |
| `commands/speckit.clarify.md` | `templates/commands/clarify.md` |

**Regra de merge**: A lógica upstream (hooks, validação, scripts, checklists) deve ser atualizada fielmente. As seções que usam `vscode_askQuestions` em vez de markdown tables devem ser PRESERVADAS — são as customizações deste preset. O frontmatter (description, handoffs) deve permanecer traduzido para pt-BR.

## Instruções de Execução

### Passo 1: Determinar versão alvo

Se o usuário forneceu uma versão (ex: `0.7.0`), use a tag `v{versão}` para o download.
Se vazio, use `main`.

Defina a base URL:
- Com tag: `https://raw.githubusercontent.com/github/spec-kit/v{versão}/`
- Sem tag: `https://raw.githubusercontent.com/github/spec-kit/main/`

### Passo 2: Baixar CHANGELOG upstream

Baixe `{BASE_URL}CHANGELOG.md` e identifique as mudanças desde a última versão sincronizada deste preset.

A última versão sincronizada está registrada no `CHANGELOG.md` local — procure por referências ao Spec Kit (ex: "upstream 0.6.1").

Resuma para o usuário:
- Versões lançadas desde a última sync
- Mudanças relevantes para templates e commands
- Novos templates adicionados (se houver)

Use `vscode_askQuestions` para confirmar se o usuário quer prosseguir:
```json
{
  "questions": [{
    "header": "Confirmar sync",
    "question": "Encontrei N mudanças relevantes desde a versão X.Y.Z. Deseja prosseguir com a sincronização?",
    "options": [
      {"label": "Sim, prosseguir", "recommended": true},
      {"label": "Não, cancelar"}
    ]
  }]
}
```

### Passo 3: Baixar arquivos upstream

Baixe todos os 8 arquivos upstream usando `fetch_webpage`:

**Templates** (da pasta `templates/`):
- `spec-template.md`
- `plan-template.md`
- `tasks-template.md`
- `checklist-template.md`
- `constitution-template.md`
- `agent-file-template.md`

**Commands** (da pasta `templates/commands/`):
- `specify.md`
- `clarify.md`

Salve os conteúdos upstream em uma pasta temporária `_upstream_sync/` na raiz do projeto.

### Passo 4: Comparar templates

Para cada template, compare o upstream com o local:

1. **Identificar seções novas**: Headings (##, ###) presentes no upstream mas ausentes no local
2. **Identificar seções removidas**: Headings no local que não existem mais no upstream
3. **Identificar mudanças em seções existentes**: Diferenças no conteúdo de placeholders ou instruções

Produza um relatório por template:
```
### spec-template.md
- ✅ Sem mudanças
  OU
- ⚠️ Nova seção: "## Security Considerations" (após "## Assumptions")
- ⚠️ Seção removida: "## Legacy Notes"
- ⚠️ Seção modificada: "## Success Criteria" — novo placeholder adicionado
```

### Passo 5: Comparar commands

Para cada command, faça um diff focado:

1. **Ignorar diferenças conhecidas**: Trechos que usam `vscode_askQuestions` no local vs markdown tables no upstream — estas são as customizações do preset
2. **Identificar mudanças na lógica**: Alterações em Pre-Execution Checks, hook handling, validation loops, script execution, checklist generation
3. **Identificar mudanças no frontmatter**: Novos handoffs, scripts, ou campos

Produza um relatório:
```
### speckit.specify.md
- ✅ Lógica de hooks: sem mudanças
- ⚠️ Passo 7c: nova validação adicionada antes do checklist
- ✅ Formato de perguntas: diferença esperada (askQuestions vs tables)
- ⚠️ Frontmatter: novo handoff adicionado
```

### Passo 6: Apresentar plano de ação

Use `vscode_askQuestions` para apresentar o plano completo ao usuário:

Para cada arquivo com mudanças, pergunte:
```json
{
  "questions": [{
    "header": "spec-template.md",
    "question": "Nova seção '## Security Considerations' encontrada no upstream. Traduzir e adicionar?",
    "options": [
      {"label": "Sim, traduzir e adicionar", "recommended": true},
      {"label": "Pular esta mudança"},
      {"label": "Revisar manualmente depois"}
    ]
  }]
}
```

### Passo 7: Aplicar mudanças aprovadas

**Para templates**:
- Traduza novas seções para pt-BR (headings, instruções, placeholders descritivos)
- Mantenha em inglês: nomes de variáveis, `[PLACEHOLDER_NAMES]`, termos técnicos
- Insira na posição correta (mesma ordem do upstream)
- Use `replace_string_in_file` para edições cirúrgicas

**Para commands**:
- Copie mudanças de lógica upstream fielmente
- PRESERVE as seções que usam `vscode_askQuestions`
- Atualize o frontmatter traduzido se houver novos campos
- Use `replace_string_in_file` para edições cirúrgicas

### Passo 8: Atualizar metadados

1. Bump a versão no `preset.yml` (MINOR para novas seções, PATCH para ajustes)
2. Adicione entrada no `CHANGELOG.md` com:
   - Versão upstream sincronizada
   - Lista de mudanças aplicadas por arquivo
   - Mudanças ignoradas/adiadas (se houver)

### Passo 9: Validação final

1. Verifique que todos os arquivos têm encoding UTF-8 limpo (sem BOM, emojis corretos)
2. Confirme que nenhuma seção do upstream ficou sem tradução nos templates
3. Confirme que as seções `vscode_askQuestions` nos commands estão intactas
4. Liste a estrutura final do preset

### Passo 10: Limpeza

Remova a pasta `_upstream_sync/` e apresente o resumo final:

```
## Sincronização Concluída

- **Versão upstream**: X.Y.Z
- **Versão preset**: A.B.C → D.E.F
- **Templates atualizados**: N de 6
- **Commands atualizados**: N de 2
- **Novas seções traduzidas**: lista
- **Próximo passo**: `git add -A && git commit -m "sync: upstream vX.Y.Z"` e `git tag vD.E.F`
```

## Regras Importantes

- **NUNCA** remova ou altere seções que usam `vscode_askQuestions` nos commands
- **NUNCA** deixe headings em inglês nos templates (exceto termos técnicos universais)
- **NUNCA** altere o `id` do preset no `preset.yml`
- **SEMPRE** preserve a ordem de seções do upstream
- **SEMPRE** confirme com o usuário antes de aplicar mudanças destrutivas
- **SEMPRE** mantenha identificadores de código e nomes de variáveis em inglês
- Se um novo template aparecer no upstream que não existia antes, crie-o traduzido e adicione ao `preset.yml`
