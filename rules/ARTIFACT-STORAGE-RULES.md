# Artifact Storage Rules

Versão: 0.1
Status: estrutura aprovada pelo usuário nesta conversa.

## Localização

Definições centrais: C:\Users\gusta\Documents\Agent-Team.
Registros de execução: agent-records/ na raiz de cada projeto.

## Estrutura por projeto

```text
agent-records/
├── README.md
├── rules/
│   └── v0.1/
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
4. Usar horário UTC no formato YYYYMMDDTHHMMSSZ e sequência run-NNN para distinguir execuções.
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
