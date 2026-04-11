# Constituição: [NOME_DO_PROJETO]
<!-- Exemplo: Constituição do Spec, Constituição do TaskFlow, etc. -->

## Princípios Fundamentais

### [NOME_PRINCÍPIO_1]
<!-- Exemplo: I. Biblioteca em Primeiro Lugar -->
[DESCRIÇÃO_PRINCÍPIO_1]
<!-- Exemplo: Toda feature começa como biblioteca independente; Bibliotecas devem ser autocontidas, testáveis isoladamente e documentadas; Propósito claro obrigatório — sem bibliotecas apenas organizacionais -->

### [NOME_PRINCÍPIO_2]
<!-- Exemplo: II. Interface de Linha de Comando -->
[DESCRIÇÃO_PRINCÍPIO_2]
<!-- Exemplo: Toda biblioteca expõe funcionalidade via CLI; Protocolo texto entrada/saída: stdin/args → stdout, erros → stderr; Suporte a formatos JSON + legível por humanos -->

### [NOME_PRINCÍPIO_3]
<!-- Exemplo: III. Test-First (NÃO NEGOCIÁVEL) -->
[DESCRIÇÃO_PRINCÍPIO_3]
<!-- Exemplo: TDD obrigatório: Testes escritos → Aprovados pelo usuário → Testes falham → Então implementar; Ciclo Red-Green-Refactor rigorosamente aplicado -->

### [NOME_PRINCÍPIO_4]
<!-- Exemplo: IV. Testes de Integração -->
[DESCRIÇÃO_PRINCÍPIO_4]
<!-- Exemplo: Áreas que exigem testes de integração: Contratos de novas bibliotecas, Mudanças de contrato, Comunicação entre serviços, Schemas compartilhados -->

### [NOME_PRINCÍPIO_5]
<!-- Exemplo: V. Observabilidade, VI. Versionamento e Breaking Changes, VII. Simplicidade -->
[DESCRIÇÃO_PRINCÍPIO_5]
<!-- Exemplo: I/O textual garante depurabilidade; logging estruturado obrigatório; Ou: formato MAJOR.MINOR.BUILD; Ou: Começar simples, princípios YAGNI -->

## [NOME_SEÇÃO_2]
<!-- Exemplo: Restrições Adicionais, Requisitos de Segurança, Padrões de Desempenho, etc. -->

[CONTEÚDO_SEÇÃO_2]
<!-- Exemplo: Requisitos de stack tecnológico, padrões de conformidade, políticas de deploy, etc. -->

## [NOME_SEÇÃO_3]
<!-- Exemplo: Fluxo de Desenvolvimento, Processo de Revisão, Quality Gates, etc. -->

[CONTEÚDO_SEÇÃO_3]
<!-- Exemplo: Requisitos de code review, quality gates de testes, processo de aprovação de deploy, etc. -->

## Governança
<!-- Exemplo: A Constituição prevalece sobre todas as outras práticas; Alterações exigem documentação, aprovação e plano de migração -->

[REGRAS_DE_GOVERNANÇA]
<!-- Exemplo: Todos os PRs/revisões devem verificar conformidade; Complexidade deve ser justificada; Use [ARQUIVO_DE_ORIENTAÇÃO] como guia de desenvolvimento em runtime -->

**Versão**: [VERSÃO_CONSTITUIÇÃO] | **Ratificada em**: [DATA_RATIFICAÇÃO] | **Última Alteração**: [DATA_ÚLTIMA_ALTERAÇÃO]
<!-- Exemplo: Versão: 2.1.1 | Ratificada em: 2025-06-13 | Última Alteração: 2025-07-16 -->