# TEAM-RULES — Regras globais da equipe

## 1. Identificação e status

| Campo | Valor |
|---|---|
| Versão | 0.3 |
| Status | VIGENTE — correção de propriedade do índice após piloto |
| Data | 2026-09-23 |
| Escopo | Os dez agentes de desenvolvimento definidos nesta conversa |
| Base | Documentos AGENT-01 a AGENT-10 e decisões da conversa original |
| Aprovação | Usuário solicitou preparar a correção identificada no piloto |

Este documento define as regras comuns vigentes. A v0.3 preserva as regras da v0.2 e elimina a ambiguidade sobre quem pode escrever `CURRENT.md` antes da participação do Development Manager. Mudanças futuras exigem versionamento, e features em andamento permanecem na versão fixada até migração registrada.

## 2. Princípios da equipe

1. Trabalhar a partir de artefatos identificados e contratos aprovados.
2. Não inventar requisitos nem transformar assumptions em decisões confirmadas.
3. Preservar o escopo e as fronteiras de responsabilidade.
4. Distinguir implementação, integração e validação funcional.
5. Exigir evidências para declarar conclusão.
6. Manter revisões independentes: o autor da especificação ou do plano não aprova o próprio trabalho.
7. Encaminhar problemas ao responsável pela decisão, preservando o Manager como centro da execução.
8. Priorizar código legível, correto e fácil de manter; evitar abstrações e refatorações sem necessidade.

As permissões descritas aqui delimitam papéis. Não substituem autorizações de acesso, ambiente ou operação do projeto.

## 3. Responsabilidades e autoridade

| Papel | Responsabilidade principal | Pode decidir/aprovar | Limite principal |
|---|---|---|---|
| Usuário | Decisões funcionais e aprovação humana | FEATURE_SPEC e release inicial | Aprovações devem ser explícitas |
| Feature Analyst | Definição funcional | Organizar requisitos e preparar especificação | Sem análise de código por padrão; sem autoaprovação |
| Technical Planner | Estratégia técnica baseada no sistema real | Propor arquitetura, contratos e plano | Não implementa nem aprova o próprio plano |
| Architecture Reviewer | Revisão técnica independente | Aprovar ou solicitar mudanças no plano | Não modifica plano ou especificação |
| Development Manager | Execução e DAG | Tarefas, ordem, prioridade, responsáveis e DEV_READY | Não programa, faz merge ou substitui QA |
| UX/UI Agent | Experiência e revisão de interface | UX_SPEC e decisão de UX Review | Não implementa frontend nem muda requisitos |
| Database Agent | Persistência e integridade | Detalhes de banco dentro da tarefa aprovada | Sem escrita autônoma em produção |
| Backend Agent | Regras, serviços e APIs | Detalhes internos da implementação | Não muda contratos ou arquitetura |
| Frontend Agent | Interface e interação | Detalhes internos da implementação | Não muda UX_SPEC ou API |
| Integration Agent | Consolidação e validação do conjunto | Correções mecânicas seguras e INTEGRATION_PASS | Sem nova lógica funcional; release tratado na seção 13 |
| QA Agent | Validação funcional independente | Severity e QA_PASS/QA_FAILED/QA_BLOCKED | Não corrige implementação nem faz merge/deploy |

Developers validam suas tarefas. O Integration Agent valida o conjunto. O QA valida a feature. Declarar uma tarefa COMPLETED não equivale a aprovar a feature.

## 4. Hierarquia e propriedade dos artefatos

### 4.1 Comportamento funcional

A FEATURE_SPEC aprovada, incluindo critérios de aceitação e decisões funcionais nela incorporadas, define o comportamento esperado. O UX_SPEC detalha a experiência dentro desse contrato.

O plano técnico, o Task Package e o código não podem redefinir requisitos. Comportamento implementado não se torna requisito por já existir.

### 4.2 Implementação técnica

Seguir IMPLEMENTATION_PLAN e contratos aprovados, depois Task Packages e implementação. O plano deve atender à FEATURE_SPEC e respeitar o UX_SPEC aplicável.

**Regra v0.2:** tratar UX_SPEC e IMPLEMENTATION_PLAN como documentos complementares em seus domínios. Se conflitarem entre si ou com a especificação, registrar o conflito e retornar aos responsáveis; não escolher silenciosamente uma versão.

### 4.3 Responsáveis pelos artefatos

| Artefato | Autor / mantenedor | Validação |
|---|---|---|
| FEATURE_SPEC.md | Feature Analyst | Aprovação humana |
| IMPLEMENTATION_PLAN.md | Technical Planner | Architecture Reviewer |
| ARCHITECTURE_REVIEW.md | Architecture Reviewer | Decisão técnica independente |
| TASK_GRAPH e Task Packages | Development Manager | Conferência de dependências e entregas pelo Manager |
| UX_SPEC.md | UX/UI Agent | Definition of Ready de UX; dúvidas funcionais retornam ao Analyst |
| UX_REVIEW.md | UX/UI Agent | Revisão do frontend implementado |
| Código e testes da tarefa | Developer responsável | Testes individuais, integração e QA |
| DEV_REPORT | Developer responsável | Manager confere completude |
| INTEGRATION_REPORT.md | Integration Agent | Gate de integração |
| QA_PLAN.md, QA_REPORT.md e DEFECTS | QA Agent | Gate de QA |
| DEVELOPMENT_MANAGER_REPORT.md | Development Manager | Registro da execução |

Uma solicitação de mudança não concede permissão para editar o artefato de outro papel.

**Regra v0.2:** TEAM-RULES define as regras comuns e os arquivos de agente detalham cada papel. Divergências não resolvidas devem ser explicitadas antes de executar a ação conflitante.

## 5. Fluxo e gates

| Etapa / gate | Responsável | Condições para avançar |
|---|---|---|
| Especificação pronta | Feature Analyst | Definition of Ready atendida, sem dúvidas bloqueantes |
| Especificação aprovada | Usuário | Aprovação explícita da versão apresentada |
| Plano pronto para revisão | Technical Planner | Sistema investigado, plano completo e sem blocker funcional pendente |
| Plano aprovado | Architecture Reviewer | BLOCKER = 0 e MAJOR = 0 |
| UX pronta, quando necessária | UX/UI Agent | UX_SPEC pronta e sem dúvida funcional bloqueante |
| Desenvolvimento pronto | Manager | Tarefas obrigatórias concluídas, testes individuais passaram, reports completos e sem blockers |
| UX aprovada, quando necessária | UX/UI Agent | UX_BLOCKER = 0 e UX_MAJOR = 0 |
| G3 — Integration Ready | Integration Agent | INTEGRATION_PASS e validações integradas concluídas |
| G4 — QA Ready | QA Agent | QA_PASS conforme critérios de cobertura, testes, regressão e defeitos |
| Release Gate | Manager + usuário | QA aprovado, autorização do Manager e aprovação humana |

O gate DEV_READY deve incorporar o UX Review quando exigido. Isso harmoniza a lista do Manager com a pré-condição do Integration Agent.

Uma dúvida funcional bloqueante impede avançar o trabalho dependente mesmo quando já existe SPEC_CHANGE_REQUEST. O registro do pedido não resolve o bloqueio.

**Regra v0.2:** enquanto uma dependência estiver bloqueada, o Manager pode manter tarefas independentes em execução, desde que seu escopo e contratos continuem válidos.

## 6. Estados e nomenclatura

Não usar um único campo de status para representar simultaneamente tarefa, documento, teste e feature.

| Objeto | Estados definidos |
|---|---|
| FEATURE_SPEC | DRAFT, READY_FOR_APPROVAL, APPROVED |
| IMPLEMENTATION_PLAN / revisão | DRAFT, READY_FOR_REVIEW; decisão APPROVED ou CHANGES_REQUESTED |
| Tarefa | PENDING, READY, IN_PROGRESS, BLOCKED, COMPLETED, FAILED, CANCELLED, NEEDS_REWORK |
| UX_SPEC | READY_FOR_IMPLEMENTATION quando pronta |
| UX Review | UX_APPROVED, UX_CHANGES_REQUESTED |
| Gate de desenvolvimento | DEV_READY |
| Integração | INTEGRATION_BLOCKED, INTEGRATION_FAILED, INTEGRATION_PASS |
| Entrada de QA | READY_FOR_QA |
| Resultado de QA | QA_BLOCKED, QA_FAILED, QA_PASS |
| Teste | NOT_RUN, PASS, FAIL, BLOCKED, SKIPPED |

**Normalização vigente:**

- TASK_BLOCKED é um retorno do agente; o Manager registra a tarefa como BLOCKED.
- RESULT_INCOMPLETE indica entrega insuficiente; a tarefa não vira COMPLETED.
- RETEST representa atividade ou ciclo de reexecução; seu resultado continua sendo PASS, FAIL ou outro estado de teste.
- SPEC_ISSUE identifica um problema de especificação; SPEC_CHANGE_REQUEST formaliza a alteração ou decisão necessária.
- RELEASE READY é a condição do gate posterior ao QA, sem representar execução de merge ou deploy.

BLOCKED significa impedimento de execução. FAILED significa falha constatada na tentativa ou validação. SKIPPED exige motivo e não equivale a PASS.

## 7. Decomposição, paralelismo e Git

- Cada tarefa tem objetivo técnico claro, responsável principal, dependências, critérios e testes.
- O Planner define estratégia e dependências macro; o Manager cria microtarefas e DAG.
- Participação de UX, Database, Backend e Frontend depende da feature.
- A ordem de execução deriva das dependências, não de uma sequência fixa de agentes.
- O Manager deve avaliar sobreposição de arquivos antes de paralelizar.
- Preferir branch própria e worktree separado para implementação.
- O Integration Agent consolida na branch da feature conforme a estratégia Git do projeto.
- Preservar histórico e alterações alheias à tarefa.

**Regra v0.2:** toda entrega deve identificar branch e commit/revisão. A decisão sobre merge, rebase ou cherry-pick deve seguir uma configuração do projeto; este documento não fixa uma única estratégia.

## 8. Protocolo de handoff

Todo handoff deve carregar o contrato de trabalho e as evidências necessárias. O destinatário confere suas pré-condições antes de iniciar.

**Envelope obrigatório:**

```text
HANDOFF
From:
To:
Feature:
Task: <quando aplicável>
Status:
Artifacts: <caminhos e versões>
Branch / Commit: <quando aplicável>
Requirements / Contracts:
Dependencies:
Results / Evidence:
Open blockers:
Known assumptions / Issues:
Requested action:
Human approval: <quando exigida, com referência>
```

Os modelos específicos de cada agente complementam esse envelope. Campos sem aplicação devem ser identificados como tal, sem valores de aprovação fictícios.

A cadeia de rastreabilidade deve permitir localizar:

```text
requisito → plano/contrato → tarefa → implementação
  → teste → resultado → defect/correção, se houver
```

## 9. Versionamento e mudanças

A primeira FEATURE_SPEC aprovada é v1.0. Mudanças funcionais posteriores geram nova versão, como v1.1, com motivo, origem, impacto e nova aprovação humana.

O Planner revisa o plano após mudanças relevantes e o Architecture Reviewer realiza nova revisão. UX, tarefas e testes devem refletir as decisões aprovadas.

**Convenção obrigatória:**

- Cada artefato identifica feature, versão ou ciclo, autor, status e versões de entrada.
- Registrar aprovador e referência da aprovação, quando houver.
- Preservar histórico de decisões e resultados anteriores.
- Assumptions permanecem explicitamente separadas de decisões confirmadas.
- Após mudança de especificação, contrato, UX ou código, o Manager identifica entregas afetadas e encaminha a revalidação necessária.
- Aprovações se referem às versões/revisões avaliadas; não se transferem automaticamente para alterações posteriores.

Não é necessário reiniciar toda a feature quando apenas uma parte foi afetada. A abrangência da revisão deve ser registrada.

## 10. Bloqueios, findings e escalonamento

| Situação | Registro | Destino |
|---|---|---|
| Pré-condição ausente | TASK_BLOCKED / DEPENDENCY_BLOCKER | Manager |
| Problema técnico no plano | PLAN_BLOCKER | Manager → Planner → Reviewer |
| Requisito indefinido ou contraditório | SPEC_ISSUE / SPEC_CHANGE_REQUEST | Feature Analyst + usuário, via Manager durante execução |
| UX precisa mudar | UX_CHANGE_REQUEST | Manager → UX; Analyst se houver impacto funcional |
| Dados impedem migration | DATA_MIGRATION_BLOCKER | Manager → responsáveis pelo plano/dados |
| Mudança arquitetural necessária | ARCHITECTURAL_CHANGE_REQUIRED | Manager → Planner → Reviewer |
| Contratos divergem na integração | INTEGRATION_CONTRACT_CONFLICT / REWORK_REQUIRED | Manager → tarefa responsável |
| Problema fora do escopo | OUT_OF_SCOPE_FINDING | Manager |
| Falha grave de segurança encontrada | SECURITY_FINDING_HIGH | Manager, imediatamente |
| Ambiente indisponível | ENVIRONMENT_BLOCKER ou QA_BLOCKED conforme etapa | Manager |

Cada registro deve explicar problema, impacto, evidência, itens afetados e decisão necessária. Quem reporta pode indicar o provável responsável; o Manager atribui o trabalho.

Durante planejamento, Planner e Reviewer podem trocar revisões diretamente. Durante execução, integração e QA, o Manager coordena o retorno aos especialistas.

### Retries e revisões

O Manager mantém tentativas e o limite já proposto de MAX_AUTOMATIC_RETRIES = 2.

**Regra v0.2:** interpretar o limite como duas novas tentativas após a inicial. Cada retry registra hipótese e mudança de abordagem. Após o limite, o Manager analisa a causa; isso não implica envolver o usuário em toda falha técnica.

Ainda não há limite numérico definido para os ciclos Planner/Reviewer, UX Review ou QA. Preferências pessoais não justificam reprovação técnica nem ciclos indefinidos de retrabalho.

## 11. Diretrizes de engenharia e escopo

- Priorizar legibilidade e manutenibilidade sem relaxar correção, segurança ou requisitos.
- Respeitar padrões existentes quando adequados.
- Criar abstrações, componentes, hooks e camadas quando melhorarem compreensão, reutilização ou isolamento.
- Evitar arquitetura para necessidades futuras não aprovadas e Clean Code aplicado de forma dogmática.
- Preferir soluções explícitas e proporcionais ao problema.
- Não introduzir bibliotecas, refatorações amplas ou mudanças de contrato por preferência.
- Permitir pequenas decisões internas e LOCAL_REFACTOR diretamente necessário, dentro do escopo aprovado.
- Manter regras de negócio no backend, integridade apropriada no banco e interação no frontend.
- Não depender do frontend para autorização ou proteção de dados.
- Proteger secrets e evitar exposição de informações internas em respostas e logs.

O Integration Agent só aplica SAFE_INTEGRATION_FIX quando a alteração é pequena, necessária para integrar e não muda regra, contrato ou arquitetura. Outros ajustes voltam ao Manager.

## 12. Evidências, testes e aprovação de qualidade

| Nível | Responsável | Evidência esperada |
|---|---|---|
| Tarefa | Developer | Critérios atendidos, arquivos alterados, testes e DEV_REPORT |
| UX | UX/UI Agent | Comparação com UX_SPEC e findings classificados |
| Conjunto integrado | Integration Agent | Build, lint/typecheck, contratos, migrations, testes, regressão e smoke test |
| Feature | QA Agent | Cobertura, cenários reproduzíveis, evidências, defects, retestes e regressão |

Não declarar PASS para teste não executado. Não alterar expectativas apenas para obter resultado verde. Mudanças aprovadas de comportamento que invalidem testes devem ser justificadas e registradas.

**Regra v0.2:** verificações sem aplicação técnica, como typecheck em projeto sem esse mecanismo, são registradas como N/A com justificativa. Verificação necessária, mas indisponível, é pendência/bloqueio, não N/A.

### Critérios dos reviews

- Architecture Review: BLOCKER e MAJOR devem estar zerados.
- UX Review: UX_BLOCKER e UX_MAJOR devem estar zerados.
- Integração: todas as condições de validação devem passar, sem conflitos semânticos ou blockers.
- QA: testes obrigatórios passaram, critérios cobertos, regressão passou e defeitos CRITICAL, HIGH e MEDIUM zerados.
- LOW no QA exige correção ou aprovação humana explícita via RELEASE_WITH_KNOWN_ISSUE_REQUEST, preparada pelo Manager e vinculada aos defects e à revisão. O Manager não aceita sozinho o risco.

**Regra v0.2:** INTEGRATION_MAJOR também impede INTEGRATION_PASS. Essa condição torna explícito o tratamento de uma categoria já existente no documento de integração.

Severity do QA mede impacto. Prioridade do Manager define a ordem de correção. Essas classificações não são intercambiáveis.

Toda correção após falha de QA passa por testes individuais, integração e novo QA, preservando o histórico.

## 13. Integração, release e produção

Integração normal não autoriza merge em main. A exceção de release abaixo está refletida no AGENT-09 e no AGENT-10.

**Regra vigente:**

1. Durante integração normal, o Integration Agent só consolida a branch da feature.
2. Após QA_PASS, o Manager prepara o Release Gate.
3. O usuário aprova explicitamente a entrega apresentada.
4. O Manager autoriza uma ação específica de release para o Integration Agent.
5. Nessa ação, o Integration Agent pode realizar o merge feature → main.
6. A exceção não autoriza deploy ou alterações de banco em produção.

**Regra v0.2:** o pacote de release identifica branch/commit, relatórios aplicáveis, known issues aceitos e aprovações. Se houver mudança posterior, os responsáveis reavaliam o impacto antes de usar as aprovações.

A aprovação de QA não equivale à aprovação de release. O merge em main não significa que houve deploy.

O processo de deploy, ambientes produtivos e recuperação operacional ainda não foi definido. Um Release/DevOps Agent permanece possibilidade futura, sem criação de um 11º papel nesta versão.

## 14. Interação com o usuário

- O Feature Analyst conduz esclarecimentos e decisões funcionais.
- O Manager apresenta decisões que ultrapassem a autoridade técnica ou operacional da equipe.
- Solicitações devem explicar o problema, alternativas e impacto da decisão.
- Decisões técnicas locais dentro do escopo não exigem aprovação humana repetida.
- Aprovação humana é obrigatória para FEATURE_SPEC e para o gate inicial de release.
- Silêncio, hipótese ou conclusão de um agente não representa aprovação humana.

## 15. Protocolo operacional v0.3

### Raiz central dos registros

Execuções são armazenadas em C:\Users\gusta\Documents\Agent-Records\<project-id>\features\, conforme ARTIFACT-STORAGE-RULES. Cada projeto tem PROJECT.md, identidade permanente e snapshot da equipe. Registros são compartilhados entre worktrees e não participam dos merges do código. RUN e HANDOFF distinguem caminhos de artefatos e caminhos de código.


### Inicialização e contexto obrigatório

Todos os agentes carregam TEAM-RULES, ARTIFACT-STORAGE-RULES e sua definição da versão fixada no projeto. Registrar o commit e a versão da equipe. Até o Development Manager aceitar formalmente a feature, o Feature Analyst é o único escritor de `CURRENT.md`; handoffs ao Planner e ao Reviewer transferem trabalho, não a propriedade do índice. Esses agentes registram `Proposed CURRENT update` em seus handoffs. O handoff ao Manager solicita a transferência; ela só se efetiva quando o Manager registra `CURRENT_OWNERSHIP_ACCEPTED` em execução própria e realiza a primeira atualização do índice. Após essa atualização atômica, apenas o Manager escreve `CURRENT.md`.

Cada Task Package usa o modelo comum, com base de código, dependências exatas, critérios, testes e UX_REQUIRED. TASK_GRAPH.md é a fonte canônica de estado; outros formatos são derivados.

### Dependências de código entre tarefas

1. O Manager identifica os commits concluídos que uma tarefa precisa consumir.
2. Quando não há dependência de código, o worktree parte do base_commit registrado.
3. Quando há dependências, o Manager aciona o Integration Agent em DEPENDENCY_PREPARATION, antes de DEV_READY.
4. O Integration Agent cria uma branch preparatória a partir da base registrada e faz merge dos commits necessários, preservando ancestralidade. Resolve somente SAFE_INTEGRATION_FIX; conflitos semânticos voltam ao Manager.
5. Registra dependências, prepared_base_commit e verificações mínimas necessárias ao consumidor. Essa preparação não é INTEGRATION_PASS.
6. O Manager cria/libera a branch da tarefa a partir dessa base preparada.
7. Se a dependência mudar, o Manager bloqueia os consumidores afetados, solicita nova preparação e revalidação. Não atualizar worktrees silenciosamente.
8. Após DEV_READY, a integração final consolida os commits entregues e executa todas as validações.

A estratégia padrão para essas dependências é merge preservando histórico. Não reescrever commits já entregues. O Manager continua sem permissão para executar merge.

### Aplicabilidade de UX e verificações

UX_REQUIRED=YES quando a tarefa cria ou altera fluxo, interação, estados, layout ou comportamento visível. O Manager pode definir NO para trabalho sem impacto de UX, com justificativa no Task Package; em dúvida, solicitar avaliação ao UX/UI Agent. Quando YES, UX_SPEC e UX Review são obrigatórios.

Verificações tecnicamente inaplicáveis usam N/A com justificativa. Ausência de ambiente ou ferramenta necessária gera BLOCKED. Os modelos não devem trazer PASS pré-preenchido como resultado real.

### Estados de execução, revisão e recuperação

RUN.md usa execution_status: RUNNING, COMPLETED, BLOCKED, FAILED ou CANCELLED. decision_status registra separadamente a decisão do domínio, como APPROVED, CHANGES_REQUESTED ou QA_PASS.

Architecture Reviewer sem acesso ao código encerra BLOCKED e deixa decision_status sem decisão; não reprova artificialmente o plano. Na revisão concluída, só APPROVED ou CHANGES_REQUESTED.

MAX_AUTOMATIC_RETRIES=2 significa duas novas tentativas além da inicial, três no total. Retorno com correção aprovada abre novo ciclo, sem apagar tentativas anteriores. Duas revisões consecutivas repetindo o mesmo finding sem progresso exigem triage do Manager, não outro retry cego. Se a disputa for funcional, escalar ao usuário via Analyst; se técnica, Planner e Reviewer devem registrar evidências e alternativas.

### Aprovações e commit exato

Reports de developer, integração, UX Review e QA registram tested_commit. O pacote de release registra candidate_commit e target_base_commit. Branch é apenas um localizador.

Se main avançar, o Integration Agent prepara novo candidato incorporando a nova base, executa integração e o QA revalida o impacto. Registrar novo QA_REPORT e obter aprovação humana para o candidato atualizado. Não reutilizar automaticamente a aprovação antiga.

Antes do merge, confirmar que candidato e destino ainda correspondem aos commits autorizados; divergência bloqueia RELEASE_EXECUTION. Quando possível usar avanço fast-forward do destino para o candidato validado; outra estratégia deve preservar o conteúdo validado e ser explicitada no pacote de release.

### Revisões especializadas

ACCESSIBILITY_REVIEW_REQUIRED, PERFORMANCE_REVIEW_REQUIRED e SECURITY_REVIEW_REQUIRED exigem registro de escopo, responsável e condição de conclusão. O Manager atribui a alguém com capacidade pertinente ou solicita apoio humano; não presume a existência de um agente especializado.

Quando a revisão for declarada necessária para segurança/correção de um requisito, bloqueia a aprovação dependente até existir evidência de conclusão. Uma recomendação opcional deve ser registrada como NOTE, sem usar REQUIRED. O Manager coordena, mas não substitui a aprovação técnica especializada.

### Defects e encerramento

O QA mantém o identificador estável do defect. Cada nova execução registra sua evolução, referência à correção e resultado do reteste. O Manager atribui prioridade e responsável; QA confirma resolução. Fechamento não apaga o relato original.

Known issues LOW precisam de APPROVAL.md humano com IDs, impacto e revisão correspondente. Se afetarem testes obrigatórios ou critérios de aceitação, não dispensam esses gates; uma mudança funcional deve voltar ao Analyst.

## 16. Limites e pendências intencionais

Deploy e operação de produção continuam fora desta versão. Merge em main não autoriza deploy. Nenhum executor, backup externo ou proteção de branch é instalado apenas pela existência destes documentos.

A revisão aprofundada por agente e o piloto continuam recomendados; não impedem usar estas regras como base de consistência.

## 17. Histórico

| Versão | Data | Alteração | Status |
|---|---|---|---|
| 0.3 | 2026-09-23 | Propriedade e atualização de CURRENT.md antes e depois da entrada do Development Manager | VIGENTE |
| 0.2 | 2026-09-17 | Regras, protocolo de execução, branches dependentes, gates, armazenamento e aprovações por revisão | SUBSTITUÍDA POR 0.3 |
| 0.1 | 2026-09-17 | Consolidação inicial e propostas de harmonização | HISTÓRICA |
