# Artifact Storage Rules

Versão: 0.2
Status: estrutura aprovada pelo usuário nesta conversa.

## Localização

Definições centrais: C:\Users\gusta\Documents\Agent-Team.
Registros de execução: C:\Users\gusta\Documents\Agent-Records, fora dos repositórios de código.

## Estrutura por projeto

```text
Agent-Records/
├── README.md
└── PROJECT-<UUID>-nome-do-projeto/
    ├── PROJECT.md
    ├── rules/
    │   └── v0.2-<team-commit>/
    │       ├── agents/
    │       ├── rules/
    │       └── templates/
    └── features/
        └── FEATURE-014-importacao-de-compras/
            ├── FEATURE.md
            ├── CURRENT.md
            └── 01-feature-analyst/
                └── 20260917T143025Z-run-<UUID>/
                    ├── RUN.md
                    ├── FEATURE_SPEC.md
                    └── HANDOFF.md
```

## Regras

1. Cada feature recebe ID permanente e nome descritivo; o ID permanece mesmo se o título mudar.
2. Criar pastas de agentes conforme sua participação, usando número e nome do papel.
3. Cada pasta de execução reúne todos os artefatos produzidos naquela execução.
4. Usar horário UTC no formato YYYYMMDDTHHMMSSZ e run-<UUID> para distinguir execuções concorrentes.
5. Execuções encerradas são imutáveis. Correções geram nova execução com referência à anterior. Não apagar registros.
6. Versão de artefato e execução são distintas; um reteste pode usar a mesma especificação e produzir outro registro.
7. Registrar caminhos e versões exatos das entradas. O arquivo mais recente pode ser um rascunho reprovado.
8. FEATURE.md identifica objetivo e origem. CURRENT.md aponta para versões aprovadas e resultados vigentes.
9. CURRENT.md pode ser atualizado com histórico no Git; não substitui evidências e aprovações preservadas nas execuções.
10. Preservar a versão das regras e dos agentes utilizada pelo projeto. Atualizações centrais não se aplicam silenciosamente ao trabalho em andamento.
11. Código, migrations e testes do produto ficam nas pastas normais do projeto. Registrar referências aos commits em vez de duplicar todo o código.
12. Evidências podem ficar em evidence/ e defeitos em defects/ dentro da execução.
13. Preservação permanente requer Git e backup. Salvar evidências sem credenciais ou dados sensíveis desnecessários.

## Registro da execução

Usar o modelo RUN.md da pasta templates/ e referenciar handoffs e aprovações correspondentes. Registrar branch e commit testado quando aplicáveis.

## Protocolo de registro v0.2

- IDs de feature são alocados pelo Feature Analyst na criação; o Manager assume o registro após receber a feature.
- Manager é o único escritor de CURRENT.md após essa transferência. Agentes enviam propostas de atualização em seus handoffs.
- Cada execução usa YYYYMMDDTHHMMSSZ-run-<UUID>. A sequência numérica anterior é substituída por UUID para evitar colisões de instâncias paralelas. Registros antigos não são renomeados.
- Criar o diretório exclusivamente; se já existir, gerar outro UUID. Não usar overwrite.
- O agente cria RUN.md antes de trabalhar, registra entradas exatas e atualiza somente sua execução ainda aberta.
- Ao terminar, gravar resultados e manifesto de saídas com caminhos e hashes SHA-256 em RUN.md. Não incluir o próprio RUN.md no cálculo para evitar autorreferência.
- Encerrar com execution_status e finished_at. Após encerramento, nenhum arquivo da execução pode ser alterado.
- Aprovação recebida após encerramento gera novo registro APPROVAL.md em nova execução, referenciando o artefato aprovado.
- Se houver interrupção, o Manager registra em nova execução que a anterior foi interrompida/superada. Preserva o diretório anterior sem completar ou reescrever seus arquivos. A retomada recebe novo Run ID.
- CURRENT.md só aponta para entregas aceitas e versões aprovadas; atualizações são serializadas pelo responsável e commitadas no Git. O índice não concede aprovação.
- Registrar team_version e team_commit imutável. O snapshot inclui agentes, regras e templates; usar artifact_paths relativos à pasta de registros do projeto; code_paths são relativos à raiz do repositório de código. Nunca misturar essas duas bases.
- Registros de preparação de dependências também devem ser preservados. Os registros ficam fora das branches de código e não são transportados por merge. Todas as instâncias e worktrees do mesmo projeto usam a mesma pasta de registros. O Manager serializa atualizações de CURRENT.md, sem descartar execuções.
- Git não substitui backup independente. A política exige preservação; o operador do projeto deve prover backup, cuja implementação não faz parte desta revisão.

## Identidade do projeto e resolução de caminhos

Antes da primeira execução, o Feature Analyst ou Manager cadastra PROJECT.md a partir do modelo. Alocar project_id com UUID e manter o ID mesmo se o repositório mudar de nome ou local. Uma cópia/worktree do mesmo projeto reutiliza esse ID; um projeto independente recebe outro.

PROJECT.md registra URL do repositório sem credenciais, caminhos locais conhecidos, records_root, team_version e team_commit. Os caminhos locais servem para localizar o checkout; repository_url e commits identificam o código avaliado.

Cada RUN e HANDOFF inclui project_id e repository_url. artifact_paths são relativos à pasta PROJECT-<UUID>-nome; code_paths são relativos ao checkout. Não resolver caminhos de artefatos com base no diretório de trabalho do agente.

O snapshot em rules/ é criado a partir do commit fixado da equipe e inclui regras, agentes e modelos. Não apontar para arquivos centrais mutáveis como se fossem um snapshot.

O histórico central requer versionamento próprio e backup independente do repositório de código. Sua configuração não é implícita; registrar no README da raiz o estado real de Git/remoto/backup. Não enviar registros para o repositório Agent-Team.

Se houver registros legados em um projeto, preservá-los e registrar sua origem antes de uma migração explícita. Esta alteração não autoriza apagar históricos anteriores.
