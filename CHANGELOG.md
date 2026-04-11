# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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
