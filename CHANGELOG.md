# Changelog

<!-- markdownlint-disable MD024 -->

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [2.0.0] — 2026-05-11

### Changed

- **BREAKING: Migração de `strategy: replace` para `strategy: wrap`** — todos os 7 arquivos do preset (5 templates + 2 commands) agora usam composição `wrap` com `{CORE_TEMPLATE}` em vez de substituir o conteúdo upstream inteiro.
- **Manutenção zero**: templates e commands upstream fluem automaticamente via `{CORE_TEMPLATE}`. Atualizações do Spec Kit não exigem mais re-sync manual dos 7 arquivos.
- `preset.yml` — `speckit_version` atualizado de `>=0.1.0` para `>=0.8.0` (composition strategies requerem v0.8.0+). Tag `composition` adicionada. Campo `replaces` removido (não necessário com `strategy: wrap`).
- `templates/constitution-template.md` — substituído por wrapper com diretiva de idioma pt-BR + tabela de mapeamento de termos + `{CORE_TEMPLATE}`.
- `templates/spec-template.md` — substituído por wrapper com mapeamentos de headings, prefixos (FR→RF, SC→CS, US→HU) e placeholders + `{CORE_TEMPLATE}`.
- `templates/plan-template.md` — substituído por wrapper com mapeamentos de termos técnicos e labels de estrutura + `{CORE_TEMPLATE}`.
- `templates/tasks-template.md` — substituído por wrapper com mapeamentos de fases, labels e prefixos (US→HU) + `{CORE_TEMPLATE}`.
- `templates/checklist-template.md` — substituído por wrapper com mapeamentos de termos de checklist + `{CORE_TEMPLATE}`.
- `commands/speckit.specify.md` — substituído por wrapper com frontmatter pt-BR (description, handoffs) + override de interação `vscode_askQuestions` + `{CORE_TEMPLATE}`. Scripts herdados automaticamente do upstream.
- `commands/speckit.clarify.md` — substituído por wrapper com frontmatter pt-BR + override sequencial `vscode_askQuestions` + `{CORE_TEMPLATE}`. Scripts herdados automaticamente do upstream.

### Notas da migração

- **Versão coberta**: upstream 0.8.8 (última disponível).
- **Redução de ~2000 linhas para ~250 linhas** mantidas no preset.
- **Composição**: o Spec Kit resolve `{CORE_TEMPLATE}` em runtime, inserindo o conteúdo upstream completo. O wrapper adiciona diretivas de tradução antes e reforço depois.
- **Frontmatter de commands**: o layer mais prioritário (preset) vence. `scripts` e `agent_scripts` são herdados do upstream automaticamente quando ausentes no wrapper.
- **Compatibilidade**: requer Spec Kit >=0.8.0 (composition strategies implementadas desde esta versão).

## [1.4.1] — 2026-04-28

### Changed

- **Sync upstream 0.8.1** — substituídas referências hardcoded a commands (`/speckit.*`) por tokens de placeholder (`__SPECKIT_COMMAND_*__`), alinhando ao PR upstream `fix: resolve command references per integration type (dot vs hyphen) (#2354)`.
- `templates/checklist-template.md` — `/speckit.checklist` → `__SPECKIT_COMMAND_CHECKLIST__`.
- `templates/plan-template.md` — `/speckit.plan` → `__SPECKIT_COMMAND_PLAN__`, `/speckit.tasks` → `__SPECKIT_COMMAND_TASKS__`.
- `templates/tasks-template.md` — `/speckit.tasks` → `__SPECKIT_COMMAND_TASKS__`.
- `commands/speckit.specify.md` — `/speckit.specify` → `__SPECKIT_COMMAND_SPECIFY__`, `/speckit.plan` → `__SPECKIT_COMMAND_PLAN__`, `/speckit.clarify` → `__SPECKIT_COMMAND_CLARIFY__`, `/speckit.tasks` → `__SPECKIT_COMMAND_TASKS__`.
- `commands/speckit.clarify.md` — `/speckit.plan` → `__SPECKIT_COMMAND_PLAN__`, `/speckit.specify` → `__SPECKIT_COMMAND_SPECIFY__`, `/speckit.clarify` → `__SPECKIT_COMMAND_CLARIFY__`.
- `catalog.json` — versão bumped para 1.4.1.

### Notas da sync

- **Versão coberta**: 0.8.1.
- **Única mudança**: introdução de tokens `__SPECKIT_COMMAND_*__` substituindo referências hardcoded a commands em todos os templates e commands.
- **Templates alterados** (3/5): `plan-template.md`, `tasks-template.md`, `checklist-template.md`. Templates `spec-template.md` e `constitution-template.md` inalterados.
- **Commands alterados** (2/2): `speckit.specify.md`, `speckit.clarify.md` — customizações `vscode_askQuestions` e frontmatter pt-BR preservados.

## [1.4.0] — 2026-04-23

### Changed

- **Sync upstream 0.8.0** — templates e commands com SHA idêntico ao 0.7.1; única mudança estrutural é a remoção de `agent-file-template.md` do upstream.
- `preset.yml` — removida entrada `agent-file-template` de `provides.templates`; versão bumped para 1.4.0.

### Removed

- `templates/agent-file-template.md` — template removido do upstream entre 0.7.1 e 0.8.0. Arquivo e referência no preset removidos para alinhar ao upstream.

### Notas da sync

- **Versões cobertas**: 0.7.2, 0.7.3, 0.7.4, 0.7.5, 0.8.0.
- **Templates inalterados** (5/5): `spec-template.md`, `plan-template.md`, `tasks-template.md`, `checklist-template.md`, `constitution-template.md` — SHA idêntico entre 0.7.1 e 0.8.0.
- **Commands inalterados** (2/2): `speckit.specify.md`, `speckit.clarify.md` — upstream `specify.md` e `clarify.md` com SHA idêntico; customizações `vscode_askQuestions` preservadas.
- **Mudança relevante no engine 0.8.0**: composition strategies (prepend, append, wrap) para presets — não requer alteração no preset.

## [1.3.3] — 2026-04-15

### Changed

- `commands/speckit.specify.md` — prompts de handoff traduzidos para pt-BR, mantendo a lógica do upstream `0.7.1` e a customização com `vscode_askQuestions`.
- `commands/speckit.clarify.md` — prompts de handoff traduzidos para pt-BR e loop interativo alinhado ao upstream `0.7.1`, preservando `vscode_askQuestions` e agora cobrindo explicitamente `skip` e sinais de término antecipado do usuário.
- `preset.yml` — versão bumped para `1.3.3` (PATCH: sync efetiva dos commands para distribuição e atualização em outros repositórios).

## [1.3.2] — 2026-04-15

### Changed

- **Sync upstream 0.7.1** — verificado que os 6 templates permanecem estruturalmente alinhados ao upstream e que `commands/speckit.specify.md` já contém o conteúdo do default preservando a customização com `vscode_askQuestions`.
- `commands/speckit.clarify.md` — divergência pontual no encerramento do loop de perguntas revisada durante a sync; mantido o comportamento local de `skip` por decisão explícita.
- `preset.yml` — versão bumped para 1.3.2 (PATCH: sync de upstream sem merge de conteúdo aplicado).
- Referência de upstream atualizada de 0.7.0 para 0.7.1.

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
