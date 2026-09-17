# Agent Team — v0.2

Equipe de dez agentes de desenvolvimento e suas regras operacionais.

## Conteúdo

- agents/: definições v0.2 dos dez agentes.
- rules/TEAM-RULES.md: regras comuns vigentes e precedência.
- rules/ARTIFACT-STORAGE-RULES.md: armazenamento, execuções imutáveis e índices.
- templates/: modelos obrigatórios de registro, handoff, feature, estado atual, tarefa e aprovação.
- CHANGELOG.md: histórico das revisões.

## Uso

Carregar as duas regras comuns e o documento do agente antes de executá-lo. Fixar versão e commit deste repositório no projeto consumidor; preservar snapshot das definições e modelos em agent-records/rules/. Uma atualização central não migra features em andamento automaticamente.

Repositório: https://github.com/GustavoWachholz/Dev-agent-team

Os Markdown definem o processo; não instalam um executor. Backup externo, proteção de branch e processo de deploy não foram configurados por esta revisão.

A v0.2 implementa as correções autorizadas pelo usuário. A revisão aprofundada de cada papel e um piloto devem validar sua aplicação prática.
