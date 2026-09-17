# Artifact Storage Rules

Versão: 0.2
Status: estrutura aprovada pelo usuário nesta conversa.

## Localização

Definições centrais: C:\Users\gusta\Documents\Agent-Team.
Registros de execução: agent-records/ na raiz de cada projeto.

## Estrutura por projeto

```text
agent-records/
├── README.md
├── rules/
│   └── v0.2-<team-commit>/
│       ├── TEAM-RULES.md
│       ├── ARTIFACT-STORAGE-RULES.md
│       └── AGENT-01...AGENT-10.md
└── features/
    └── FEATURE-014-importacao-de-compras/
        ├── FEATURE.md
        ├── CURRENT.md
        └── 01-feature-analyst/
            └── 20260917T143025Z-run-001/
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
- Registrar team_version e team_commit imutável. O snapshot inclui agentes, regras e templates; usar caminhos relativos ao projeto nos handoffs.
- Registros de preparação de dependências também devem ser preservados. Na integração, conservar a união dos registros das branches; conflitos em CURRENT.md são resolvidos pelo Manager a partir dos eventos, sem descartar execuções.
- Git não substitui backup independente. A política exige preservação; o operador do projeto deve prover backup, cuja implementação não faz parte desta revisão.
