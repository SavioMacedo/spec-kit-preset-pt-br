# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.3.1] — 2026-04-15

### Changed

- **Sync upstream 0.7.0** — verificado que nenhum template ou command core foi alterado entre 0.6.1 e 0.7.0.
  Versões intermediárias (0.6.2, 0.7.0) contêm apenas mudanças em catálogo comunitário, workflow engine e CLI.
- `preset.yml` — versão bumped para 1.3.1 (PATCH: sync sem alterações de conteúdo).
- Referência de upstream atualizada de 0.6.1 para 0.7.0.

## [1.3.0] — 2026-04-11

### Changed

- **preset.yml** — reestruturado para conformidade com o padrão oficial de presets do Spec Kit:
  - `description` reduzida para ≤200 caracteres.
  - Commands movidos para `provides.templates` (lista unificada com `type: "command"`).
  - Nomes dos commands em dot notation: `speckit.specify`, `speckit.clarify`.
  - Caminhos dos commands atualizados para `commands/speckit.specify.md` e `commands/speckit.clarify.md`.
- **Estrutura de diretórios** — `templates/commands/` movido para `commands/` na raiz (padrão oficial).
- **Filenames dos commands** — renomeados de `specify.md`/`clarify.md` para `speckit.specify.md`/`speckit.clarify.md`.
- Versão bumped para 1.3.0.

## [1.2.0] — 2026-04-11

### Added

- `commands/speckit.specify.md` — override do command `/speckit.specify` que usa
  `vscode_askQuestions` para todas as perguntas de clarificação ao usuário (substituindo
  as tabelas markdown inline do upstream).
- `commands/speckit.clarify.md` — override do command `/speckit.clarify` que usa
  `vscode_askQuestions` para o loop sequencial de perguntas (até 5).

### Changed

- `preset.yml` — seção `commands` adicionada com os 2 overrides; versão bumped para 1.2.0.
- Frontmatter dos commands traduzido para PT-BR (description, handoff labels).

## [1.1.0] — 2026-04-11

### Added

- `templates/agent-file-template.md` — novo template de diretrizes de desenvolvimento do agente em PT-BR (adicionado no upstream a partir do Spec Kit 0.5.x).

### Fixed

- Corrigidos problemas de encoding UTF-8 (emojis corrompidos) em todos os templates.
- `tasks-template.md` — traduzidas 10+ linhas que haviam permanecido em inglês:
  headings de fases, seções de testes opcionais, notas de paralelismo e entrega incremental.
- `plan-template.md` — traduzido campo `**Structure Decision**` que ainda estava em
  inglês; corrigida tabela de Rastreamento de Complexidade que estava com separadores duplicados.
- `constitution-template.md` — traduzidos 2 comentários HTML de exemplo (princípios 2 e 3)
  que haviam ficado em inglês.

## [1.0.0] — 2026-04-05

### Added

- `templates/constitution-template.md` — constitution template com diretiva de idioma
  PT-BR embutida que propaga para todo o workflow do Spec Kit.
- `preset.yml` — manifesto do preset com id `pt-br`, compatível com `speckit_version >=0.1.0`.
- `README.md` — documentação de instalação, uso e decisões arquiteturais.
- `LICENSE` — licença MIT.
- `.github/copilot-instructions.md` — guia de desenvolvimento e convenções do projeto.
