# spec-kit-preset-pt-br

Preset para o [Spec Kit](https://github.com/github/spec-kit) que traduz todos os artefatos e interações do workflow Spec-Driven Development para **Português Brasileiro (pt-BR)**.

## Estratégia central

Este preset sobrescreve os **templates de conteúdo**: `constitution-template.md`, `spec-template.md`, `plan-template.md`, `tasks-template.md`, `checklist-template.md` e `agent-file-template.md`. Todos traduzidos para pt-BR.

Além disso, sobrescreve os **commands interativos** `speckit.specify` e `speckit.clarify` para que todas as perguntas ao usuário usem a ferramenta `vscode_askQuestions` (interface nativa do VS Code) em vez de tabelas markdown inline.

Os demais commands core (`speckit.plan`, `speckit.tasks`, etc.) **não são sobrescritos**:
- Commands do core contêm lógica complexa: extension hooks, branch numbering, quality validation loops, script execution, checklist generators e handoffs.
- Sobrescrever um command significa possuir toda essa lógica — bug fixes e melhorias do upstream nunca chegam.
- Os commands core carregam os templates em runtime. Como os templates do preset têm prioridade maior, os artefatos gerados saem em pt-BR sem precisar tocar nos commands.

### Manutenção dos commands sobrescritos

Os dois commands sobrescritos (`speckit.specify` e `speckit.clarify`) são baseados no upstream 0.7.0. Ao atualizar o Spec Kit, verificar se esses commands mudaram e incorporar as alterações mantendo a integração com `vscode_askQuestions`.

## Manutenção ao atualizar o Spec Kit

Quando uma nova versão do Spec Kit adicionar seções novas aos templates, o usuário **não verá essas seções** enquanto o preset não for atualizado, pois o sistema usa "first match wins" sem merge. Isso é um trade-off conhecido e aceito nesta abordagem.

Para manter o preset atualizado:
1. Monitorar o [CHANGELOG do spec-kit](https://github.com/github/spec-kit/blob/main/CHANGELOG.md)
2. Ao identificar mudanças nos templates, incorporar as novas seções nas versões pt-BR
3. Publicar nova versão do preset com SemVer (`PATCH` para ajustes de texto, `MINOR` para novas seções)

## Estrutura do repositório

```
spec-kit-preset-pt-br/
├── .github/
│   └── copilot-instructions.md   # este arquivo
├── commands/
│   ├── speckit.specify.md         # override: vscode_askQuestions
│   └── speckit.clarify.md         # override: vscode_askQuestions
├── templates/
│   ├── constitution-template.md  # constituição do projeto
│   ├── spec-template.md          # especificação de feature
│   ├── plan-template.md          # plano de implementação
│   ├── tasks-template.md         # lista de tarefas
│   ├── checklist-template.md     # checklist de qualidade
│   └── agent-file-template.md    # diretrizes de desenvolvimento do agente
├── preset.yml                    # manifesto do preset (id: "pt-br")
├── README.md
├── LICENSE
└── CHANGELOG.md
```

## Como o preset funciona (para referência)

Resolução de templates em runtime (top-down, primeiro match vence):

1. `.specify/templates/overrides/` — overrides locais do projeto
2. `.specify/presets/pt-br/templates/` ← **este preset atua aqui**
3. `.specify/extensions/<id>/templates/`
4. `.specify/templates/` — core do Spec Kit (atualizado por upgrades)

O upgrade do Spec Kit (`specify init --here --force`) atualiza apenas o core (nível 4). O preset em nível 2 nunca é tocado.

## Convenções de desenvolvimento

- O `preset.yml` deve declarar `speckit_version: ">=0.1.0"` com range amplo — nunca amarrar a uma versão exata.
- O `id` no `preset.yml` deve ser `pt-br` (corresponde ao nome do repositório após `spec-kit-preset-`).
- Versionar com SemVer: `PATCH` para correções de texto, `MINOR` para novas seções nos templates, `MAJOR` para mudanças que alterem o comportamento do preset.
- Monitorar o [CHANGELOG do spec-kit](https://github.com/github/spec-kit/blob/main/CHANGELOG.md) para identificar se novos templates foram adicionados em releases — avaliar se precisam de cobertura PT-BR.

## Como testar localmente

```bash
# Num projeto já inicializado com specify init
specify preset add --dev /caminho/para/spec-kit-preset-pt-br

# Verificar que o spec-template resolve do preset
specify preset resolve spec-template

# Remover ao terminar
specify preset remove pt-br
```

## O que não fazer

- Não sobrescrever commands além de `speckit.specify` e `speckit.clarify` — os demais não fazem perguntas interativas ao usuário.
- Não amarrar `speckit_version` a versão exata — usar `>=0.1.0`.
- Não renomear identificadores de código, nomes de variáveis ou palavras-chave técnicas nos templates — manter em inglês.
