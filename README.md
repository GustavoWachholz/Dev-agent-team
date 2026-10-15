# Agent Team — v0.3

Equipe de dez agentes de desenvolvimento e suas regras operacionais.

## Conteúdo

- agents/: definições v0.3 dos dez agentes.
- rules/TEAM-RULES.md: regras comuns vigentes e precedência.
- rules/ARTIFACT-STORAGE-RULES.md: armazenamento, execuções imutáveis e índices.
- templates/: modelos obrigatórios de registro, handoff, feature, estado atual, tarefa e aprovação.
- CHANGELOG.md: histórico das revisões.

## Armazenamento

Definições: Agent-Team. Histórico de execuções: C:\Users\nome-do-usuario\Documents\Agent-Records, organizado por projeto, feature, agente e execução. Os registros não entram nas branches do código. Consultar ARTIFACT-STORAGE-RULES e templates/PROJECT.md.

## Uso

Carregar as duas regras comuns e o documento do agente antes de executá-lo. Fixar versão e commit deste repositório no projeto consumidor; preservar snapshot das definições e modelos em C:\Users\gusta\Documents\Agent-Records\<project-id>\rules\. Uma atualização central não migra features em andamento automaticamente.

Repositório: https://github.com/GustavoWachholz/Dev-agent-team

Os Markdown definem o processo; não instalam um executor. Backup externo, proteção de branch e processo de deploy não foram configurados por esta revisão.

A v0.3 incorpora a correção encontrada no piloto: propriedade exclusiva e transferência formal de `CURRENT.md`, com propostas de atualização nos handoffs.
