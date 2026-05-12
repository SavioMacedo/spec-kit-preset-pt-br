# spec-kit-preset-pt-br

Preset para o [Spec Kit](https://github.com/github/spec-kit) que traduz todos os artefatos e interações do workflow Spec-Driven Development para **Português Brasileiro (pt-BR)**.

## Estratégia central — Composição via `wrap`

Desde a v2.0.0, este preset usa `strategy: "wrap"` (composição) em vez de substituição (`replace`). Cada arquivo contém:

1. **Diretiva de idioma** — instrui o AI a gerar todo output em pt-BR
2. **Tabela de mapeamento de termos** — headings, prefixos e placeholders traduzidos
3. **`{CORE_TEMPLATE}`** — placeholder substituído em runtime pelo conteúdo upstream completo
4. **Reforço** — comentário final reiterando as regras de tradução

O Spec Kit resolve `{CORE_TEMPLATE}` em runtime (bottom-up), inserindo o conteúdo do template core completo. Isso significa que **atualizações upstream fluem automaticamente** — sem necessidade de re-sync manual.

### Templates envelopados (wrap)

- `constitution-template.md` — mapeamentos de termos de constituição
- `spec-template.md` — mapeamentos de headings + prefixos (FR→RF, SC→CS, US→HU)
- `plan-template.md` — mapeamentos de termos técnicos e labels
- `tasks-template.md` — mapeamentos de fases e prefixos (US→HU)
- `checklist-template.md` — mapeamentos de termos de checklist

### Commands envelopados (wrap)

Os commands `speckit.specify` e `speckit.clarify` usam wrap com dois propósitos:

1. **Frontmatter em pt-BR** (description, handoffs) — vence sobre o upstream
2. **Override comportamental** — instrui o AI a usar `vscode_askQuestions` em vez de tabelas markdown inline
3. **Scripts herdados** — `scripts` e `agent_scripts` são omitidos do wrapper, sendo herdados automaticamente do command core upstream

Os demais commands core (`speckit.plan`, `speckit.tasks`, etc.) **não precisam de wrapper** — carregam os templates em runtime, e como os templates do preset têm prioridade maior, os artefatos gerados saem em pt-BR automaticamente.

## Manutenção ao atualizar o Spec Kit

Com a estratégia `wrap`, atualizações do Spec Kit **fluem automaticamente** via `{CORE_TEMPLATE}`. Manutenção é necessária apenas quando:

1. O upstream adiciona **novos templates** que precisam de cobertura pt-BR (criar novo wrapper)
2. O upstream muda **headings ou prefixos** que afetam as tabelas de mapeamento (ajustar mapeamentos)
3. Os commands `specify`/`clarify` mudam a **mecânica de interação** (ajustar override de `vscode_askQuestions`)

Monitorar o [CHANGELOG do spec-kit](https://github.com/github/spec-kit/blob/main/CHANGELOG.md) para estas situações.

## Estrutura do repositório

```text
spec-kit-preset-pt-br/
├── .github/
│   └── copilot-instructions.md   # este arquivo
├── commands/
│   ├── speckit.specify.md         # wrap: frontmatter pt-BR + vscode_askQuestions
│   └── speckit.clarify.md         # wrap: frontmatter pt-BR + vscode_askQuestions
├── templates/
│   ├── constitution-template.md  # wrap: diretiva pt-BR + {CORE_TEMPLATE}
│   ├── spec-template.md          # wrap: diretiva pt-BR + {CORE_TEMPLATE}
│   ├── plan-template.md          # wrap: diretiva pt-BR + {CORE_TEMPLATE}
│   ├── tasks-template.md         # wrap: diretiva pt-BR + {CORE_TEMPLATE}
│   └── checklist-template.md     # wrap: diretiva pt-BR + {CORE_TEMPLATE}
├── preset.yml                    # manifesto do preset (id: "pt-br", strategy: wrap)
├── catalog.json                  # catálogo para instalação via registry
├── README.md
├── LICENSE
└── CHANGELOG.md
```

## Como o preset funciona (composição em runtime)

Resolução de templates em runtime (bottom-up, composição):

1. `.specify/templates/` — core do Spec Kit (base)
2. `.specify/extensions/<id>/templates/` — extensões
3. `.specify/presets/pt-br/templates/` ← **este preset atua aqui** (wrap sobre a base)
4. `.specify/templates/overrides/` — overrides locais do projeto

O `resolve_content()` do Spec Kit busca o `strategy` no frontmatter de cada layer. Com `wrap`, o conteúdo do layer inferior (base) é inserido no lugar de `{CORE_TEMPLATE}`. Frontmatter do layer mais prioritário vence.

## Convenções de desenvolvimento

- O `preset.yml` deve declarar `speckit_version: ">=0.8.0"` — composição via `wrap` requer v0.8.0+.
- O `id` no `preset.yml` deve ser `pt-br` (corresponde ao nome do repositório após `spec-kit-preset-`).
- Todos os arquivos devem ter `strategy: wrap` no frontmatter ou no `preset.yml`.
- Versionar com SemVer: `PATCH` para correções de texto, `MINOR` para novos wrappers, `MAJOR` para mudanças de estratégia.
- Monitorar o [CHANGELOG do spec-kit](https://github.com/github/spec-kit/blob/main/CHANGELOG.md) para novos templates ou mudanças de headings.

## Como testar localmente

```bash
# Num projeto já inicializado com specify init
specify preset add --dev /caminho/para/spec-kit-preset-pt-br

# Verificar que o spec-template resolve com wrap do preset
specify preset resolve spec-template

# Remover ao terminar
specify preset remove pt-br
```

## O que não fazer

- Não usar `strategy: replace` — manter `wrap` para todos os arquivos.
- Não adicionar `scripts` ou `agent_scripts` nos commands — devem ser herdados do upstream.
- Não envelopar commands além de `speckit.specify` e `speckit.clarify` — os demais não fazem perguntas interativas.
- Não renomear identificadores de código, nomes de variáveis ou palavras-chave técnicas nos templates — manter em inglês.
