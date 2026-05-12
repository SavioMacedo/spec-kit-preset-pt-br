# spec-kit-preset-pt-br

Preset para o [Spec Kit](https://github.com/github/spec-kit) que traduz todos os artefatos e interações do workflow **Spec-Driven Development** para **Português Brasileiro (pt-BR)**.

## O que este preset faz

Após a instalação, todos os artefatos gerados pelo Spec Kit — especificações, planos, listas de tarefas, checklists e a constituição — são redigidos em Português Brasileiro. Identificadores de código, nomes de variáveis e palavras-chave técnicas permanecem em inglês.

Além disso, os commands **`/speckit.specify`** e **`/speckit.clarify`** são enriquecidos para que **todas as perguntas ao usuário** sejam feitas via `vscode_askQuestions` — a interface nativa de perguntas do VS Code — em vez de tabelas markdown inline.

## Arquitetura: Composição via `strategy: wrap`

Desde a v2.0.0, o preset usa **composição** em vez de substituição. Todos os 7 arquivos usam `strategy: "wrap"` com o placeholder `{CORE_TEMPLATE}`:

```text
[Diretiva de idioma pt-BR + mapeamentos de termos]

{CORE_TEMPLATE}  ← conteúdo upstream completo, inserido automaticamente

[Reforço de tradução]
```

### Vantagens sobre a abordagem anterior (replace)

| Aspecto | v1.x (replace) | v2.x (wrap) |
| ------- | -------------- | ----------- |
| Linhas mantidas no preset | ~2000 (7 cópias completas) | ~250 (7 wrappers) |
| Manutenção por update do Spec Kit | Diff manual de 7 arquivos | **Nenhuma** |
| Risco de dessincronia | Alto | **Zero** |
| Novas seções upstream | Invisíveis até re-sync | **Aparecem automaticamente** |

### Como funciona para commands

Para `speckit.specify` e `speckit.clarify`:

- **Frontmatter** (description, handoffs) em pt-BR → vence sobre o upstream
- **scripts/agent_scripts** → herdados automaticamente do command core
- **Override comportamental** → diretiva instrui o AI a usar `vscode_askQuestions` em vez de tabelas markdown
- **Lógica do command** → flui inteira via `{CORE_TEMPLATE}` (hooks, validação, branch creation, etc.)

## Instalação

```bash
# Adicionar o preset ao seu projeto
specify preset add https://github.com/SavioMacedo/spec-kit-preset-pt-br
```

### Instalação via catálogo customizado

Este repositório agora também expõe um catálogo de presets em `catalog.json`. Isso permite que um projeto consumidor adicione o catálogo uma vez e instale o preset pelo `id`:

```bash
# Adicionar este catálogo ao projeto consumidor
specify preset catalog add https://raw.githubusercontent.com/SavioMacedo/spec-kit-preset-pt-br/main/catalog.json --name savio-presets --install-allowed

# Verificar se o catálogo foi registrado
specify preset catalog list

# Procurar e instalar o preset pelo id
specify preset search pt-br
specify preset add pt-br

# Validar a resolução do template
specify preset resolve spec-template
```

### Desenvolvimento local

```bash
# Clonar o preset
git clone https://github.com/SavioMacedo/spec-kit-preset-pt-br

# Num projeto já inicializado com specify init
specify preset add --dev /caminho/para/spec-kit-preset-pt-br

# Verificar que o spec-template resolve do preset
specify preset resolve spec-template

# Remover ao terminar
specify preset remove pt-br
```

## Uso

Após instalar o preset, use o Spec Kit normalmente. Todos os artefatos serão gerados em pt-BR:

| Comando                 | Artefato gerado        |
| ----------------------- | ---------------------- |
| `/speckit.constitution` | Constituição em pt-BR  |
| `/speckit.specify`      | Especificação em pt-BR |
| `/speckit.plan`         | Plano técnico em pt-BR |
| `/speckit.tasks`        | Tarefas em pt-BR       |
| `/speckit.checklist`    | Checklist em pt-BR     |

## Templates incluídos

| Template                    | Strategy | Descrição                                    |
| --------------------------- | -------- | -------------------------------------------- |
| `constitution-template.md`  | wrap     | Wrapper pt-BR para constituição do projeto   |
| `spec-template.md`          | wrap     | Wrapper pt-BR para especificação de feature  |
| `plan-template.md`          | wrap     | Wrapper pt-BR para plano de implementação    |
| `tasks-template.md`         | wrap     | Wrapper pt-BR para lista de tarefas          |
| `checklist-template.md`     | wrap     | Wrapper pt-BR para checklist de qualidade    |

## Commands enriquecidos

| Command             | Strategy | Override                                            |
| ------------------- | -------- | --------------------------------------------------- |
| `speckit.specify`   | wrap     | Frontmatter pt-BR + `vscode_askQuestions`           |
| `speckit.clarify`   | wrap     | Frontmatter pt-BR + `vscode_askQuestions` sequencial |

> Os demais commands (`plan`, `tasks`, `checklist`, `implement`, etc.) usam os templates PT-BR automaticamente via composição — não precisam de wrapper.

## Este repositório como catálogo

O arquivo `catalog.json` na raiz é o ponto de entrada do catálogo. Hoje ele publica um único preset, `pt-br`, apontando para o artefato versionado `v2.0.0`.

Isso permite dois modos de consumo:

1. Instalação direta do preset por URL do repositório.
2. Instalação via catálogo customizado com `specify preset catalog add ...` seguida de `specify preset add pt-br`.

## Como evoluir para múltiplos presets

Se você quiser que este mesmo repositório hospede vários presets no futuro, as adaptações recomendadas são:

1. Adicionar uma entrada por preset dentro de `catalog.json`.
2. Manter cada preset com seu próprio `preset.yml`, templates, commands e README dedicado.
3. Se houver vários presets no mesmo repositório, reorganizar a estrutura para subpastas como `presets/<id>/` ou `<id>/`.
4. Publicar um ZIP versionado por preset em cada release. O `archive/refs/tags/...zip` do GitHub funciona bem para este repositório enquanto ele contém um único preset na raiz, mas não é o formato ideal para múltiplos presets no mesmo pacote.
5. Atualizar, em cada entrada do catálogo, os campos `version`, `download_url`, `documentation`, `created_at` e `updated_at`.
6. Validar no consumer com `specify preset catalog add`, `specify preset search`, `specify preset add <id>` e `specify preset resolve spec-template`.

## Compatibilidade

| Spec Kit  | Status                                        |
| --------- | --------------------------------------------- |
| `>=0.8.0` | ✅ Compatível (composition strategies)         |
| `<0.8.0`  | ❌ Não compatível (use preset v1.4.1 ou menor) |

## Contribuindo

1. Faça um fork do repositório
2. Crie uma branch: `git checkout -b minha-melhoria`
3. Faça suas alterações nos templates em `templates/`
4. Abra um Pull Request

Ao identificar novas seções adicionadas em releases do Spec Kit que precisem de cobertura, abra uma issue.

## Licença

[MIT](LICENSE)
