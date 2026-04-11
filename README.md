# spec-kit-preset-pt-br

Preset para o [Spec Kit](https://github.com/github/spec-kit) que traduz todos os artefatos e interações do workflow **Spec-Driven Development** para **Português Brasileiro (pt-BR)**.

## O que este preset faz

Após a instalação, todos os artefatos gerados pelo Spec Kit — especificações, planos, listas de tarefas, checklists, a constituição e o arquivo de diretrizes do agente — são redigidos em Português Brasileiro. Identificadores de código, nomes de variáveis e palavras-chave técnicas permanecem em inglês.

Além disso, os commands **`/speckit.specify`** e **`/speckit.clarify`** são sobrescritos para que **todas as perguntas ao usuário** sejam feitas via `vscode_askQuestions` — a interface nativa de perguntas do VS Code — em vez de tabelas markdown inline. Os demais commands core não são sobrescritos.

## Trade-off de manutenção

O sistema usa "first match wins" — sem merge de templates. Quando o Spec Kit adicionar seções novas a um template em uma versão futura, o usuário não verá essas seções até que o preset seja atualizado. Monitore o [CHANGELOG do spec-kit](https://github.com/github/spec-kit/blob/main/CHANGELOG.md) e publique uma nova versão do preset com as seções traduzidas quando necessário.

## Instalação

```bash
# Adicionar o preset ao seu projeto
specify preset add https://github.com/SavioMacedo/spec-kit-preset-pt-br
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

| Template                    | Descrição                                |
| --------------------------- | ---------------------------------------- |
| `constitution-template.md`  | Constituição do projeto                  |
| `spec-template.md`          | Especificação de feature                 |
| `plan-template.md`          | Plano de implementação                   |
| `tasks-template.md`         | Lista de tarefas                         |
| `checklist-template.md`     | Checklist de qualidade                   |
| `agent-file-template.md`    | Diretrizes de desenvolvimento do agente  |

## Commands sobrescritos

| Command           | Motivo do override                                     |
| ----------------- | ------------------------------------------------------ |
| `speckit.specify` | Perguntas de clarificação via `vscode_askQuestions`     |
| `speckit.clarify` | Loop de perguntas sequenciais via `vscode_askQuestions` |

> Os demais commands (`plan`, `tasks`, `checklist`, `implement`, etc.) **não são sobrescritos** — usam os templates PT-BR automaticamente via resolução "first match wins".

## Compatibilidade

| Spec Kit  | Status        |
| --------- | ------------- |
| `>=0.1.0` | ✅ Compatível |

## Contribuindo

1. Faça um fork do repositório
2. Crie uma branch: `git checkout -b minha-melhoria`
3. Faça suas alterações nos templates em `templates/`
4. Abra um Pull Request

Ao identificar novas seções adicionadas em releases do Spec Kit que precisem de cobertura, abra uma issue.

## Licença

[MIT](LICENSE)
