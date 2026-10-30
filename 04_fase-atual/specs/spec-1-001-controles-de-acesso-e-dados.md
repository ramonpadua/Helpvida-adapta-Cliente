# SPEC-1-001 — Controles de acesso, dados e trilha do piloto

**Fase:** 1  
**Status:** planejada com uso real bloqueado  
**Dono:** Fernando/TI; homologação por TI + jurídico/DPO + Auditoria/Faturamento  
**Origem no escopo:** DC-01, DH-03, DH-04; Fase 1 — Dados; critérios globais 2, 4, 5 e 6  
**Degrau da solução:** recurso nativo da plataforma — autenticação, autorização, armazenamento protegido e auditoria devem usar os recursos nativos do ambiente que for formalmente selecionado; nenhuma plataforma é presumida nesta SPEC.

## Contexto e decisões fechadas

- **Estado atual:** não há ambiente/repositório formalmente selecionado nem política aprovada para dados reais. A operação existente manipula documentos de saúde; a alegação “não guardar dados” foi rejeitada como premissa segura pelo escopo definitivo.
- **Estado desejado:** existe um limite técnico demonstrável que separa operador de campo, conferente e administrador; registra acesso e mudança de estado sem expor conteúdo sensível em logs; permite apagar/expirar massa de teste.
- **Decisões fechadas:** menor privilégio; conferência humana obrigatória; estados `recebido → extraído → em conferência → corrigir → aprovado internamente`; uso real somente após política.
- **Bloqueios:** `B-ENV-01` seleção/autorização de ambiente e repositório; `B-DADOS-01` política de finalidade, base aplicável, perfis, retenção, exclusão, processamento externo e incidente. Massa sintética pode ser usada antes de `B-DADOS-01`.

## Resultado observável

Em ambiente autorizado, três contas de teste demonstram que cada papel vê e altera apenas o permitido; tentativa indevida é negada e auditada; uma ocorrência sintética pode ser criada, avançada e excluída/expirada sem dado de paciente.

## Limites e dependências

- **Inclui:** papéis de teste; matriz mínima de permissões; identificador opaco de ocorrência; timestamps; autor da alteração; motivo de correção; retenção configurável; trilha sem conteúdo clínico.
- **Fora de escopo:** SSO, acesso de operadora, dado real, regra clínica/faturamento, envio externo, decisão por IA.
- **Entradas:** ambiente autorizado; matriz abaixo; fixture sintética; política aprovada apenas para migrar a dado real.
- **Saídas:** configuração de acesso; esquema lógico; testes de permissão; evidência de auditoria e exclusão.
- **Superfícies afetadas:** módulo de autenticação/autorização, persistência de ocorrências e eventos, tela/fila mínima de teste; caminhos físicos só serão definidos após `B-ENV-01`.
- **Risco e plano B:** se o ambiente não oferecer RBAC/auditoria suficientes, parar; não construir autorização improvisada.
- **Rollback:** desativar contas de teste, remover fixture e reverter configuração/migração da task sem afetar outros ambientes.

## Dados e permissões

| Entidade | Campos mínimos | Regra de qualidade | Retenção |
|---|---|---|---|
| ocorrência | id opaco, competência fictícia, tipo documental, casa fictícia, status, created_at | sem nome/CPF/cartão/prontuário real | configurável |
| evento_auditoria | occurrence_id, ator, papel, ação, estado anterior/novo, timestamp, motivo | sem imagem/texto clínico/token/segredo | conforme política; teste removível |
| artefato_teste | id, tipo, hash, origem sintética, qualidade | conteúdo exclusivamente sintético | expira ao encerrar a prova; Fernando/TI executa e demonstra a remoção no mesmo ciclo |

| Papel | Criar/capturar | Ver conteúdo | Corrigir | Aprovar internamente | Administrar acesso |
|---|---:|---:|---:|---:|---:|
| Operador de campo | sim | apenas próprias ocorrências necessárias | não | não | não |
| Conferente | não | fila atribuída | sim, com motivo | sim | não |
| Fernando/TI administrador | suporte técnico; sem uso operacional | somente suporte autorizado e auditado | não como conferente | não | sim |

## Fluxo e regras

1. Administrador cria contas de teste com um papel cada.
2. Operador cria ocorrência sintética em `recebido`.
3. Sistema registra evento sem conteúdo do documento.
4. Conferente avança estados, corrige com motivo e aprova internamente.
5. Operador tenta aprovar e recebe negação sem mudança de estado.
6. Administrador executa expiração/exclusão da fixture e preserva somente evidência permitida.

| Regra | Condição | Resultado | Exceção |
|---|---|---|---|
| RN-101 | papel sem permissão | negar por padrão e auditar | nenhuma concessão implícita |
| RN-102 | mudança para `corrigir` | motivo obrigatório | rejeitar se vazio |
| RN-103 | dado real sem política aprovada | impedir ingestão | usar sintético/desidentificado |
| RN-104 | log contém imagem, texto clínico ou segredo | teste falha | mascarar/remover antes de prosseguir |
| RN-105 | administrador solicita acesso de suporte a conteúdo | negar sem autorização temporal, justificativa e evento auditado | revogar ao encerrar o suporte |

## Checklist de execução

- [ ] `B-ENV-01` resolvido antes de alterar ambiente.
- [ ] Fixture revisada para ausência de dado real.
- [ ] Papéis e negação por padrão configurados.
- [ ] Transições e motivo auditados.
- [ ] Logs inspecionados para conteúdo sensível/segredo.
- [ ] Exclusão/expiração exercitada.
- [ ] Evidências anexadas sem dado pessoal.

## Critérios de aceite

- [ ] **CA-1-001:** operador não consegue aprovar internamente nem administrar acesso.
- [ ] **CA-1-002:** conferente consegue corrigir somente com motivo e aprovar ocorrência sintética atribuída.
- [ ] **CA-1-003:** cada transição registra ator, papel, instante e estado anterior/novo.
- [ ] **CA-1-004:** logs e evidências não contêm imagem/texto clínico, credencial ou segredo; acesso administrativo de suporte a conteúdo é negado sem autorização temporal e, quando autorizado, registra justificativa, ator, início e revogação.
- [ ] **CA-1-005:** fixture pode ser expirada/excluída de forma demonstrável.
- [ ] **CA-1-006:** dado real permanece tecnicamente/operacionalmente bloqueado até `B-DADOS-01`.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | matriz não aplicada | testes de autorização com três papéis | ao menos uma ação indevida é possível antes da configuração | relatório RED sem dado real |
| GREEN | autorização e auditoria | repetir suíte: criar, ver, corrigir, aprovar, administrar | somente ações da matriz passam; eventos completos | log sanitizado + resultado da suíte |
| REFACTOR/REGRESSÃO | negação/segredo/retenção | varrer logs, tentar acesso cruzado e expirar fixture | zero vazamento; zero escalada; remoção confirmada | checklist e captura sanitizada |

**Dados/fixtures:** uma casa, pessoa e operadora totalmente fictícias; documento gerado para teste, marcado `SINTÉTICO — NÃO USAR`.  
**Caminhos de erro obrigatórios:** sessão expirada, papel ausente, ocorrência não atribuída, motivo vazio, tentativa de dado real.  
**Evidência exigida:** resultado de testes, matriz assinada por TI e demonstração a Auditoria/Faturamento.

## Handoff e operação

- **Como demonstrar:** três logins; fluxo permitido e duas tentativas negadas; inspeção do evento; exclusão da fixture.
- **Como operar depois:** Fernando/TI administra acesso; Auditoria/Faturamento não administra perfis.
- **Como monitorar:** revisão de acessos e eventos de negação; incidente conforme política.
- **Pendência conhecida:** uso real continua bloqueado por `B-DADOS-01`.

## Instruções de execução para o Ethos

1. **Ler antes:** escopo definitivo, checks, matriz de papéis desta SPEC e definição de `B-ENV-01`.
2. **Alterar somente:** autorização, ocorrência/evento sintéticos, expiração e testes desta SPEC.
3. **Não alterar:** integrações, IA, template, dado real ou papéis além da matriz.
4. **Ordem:** provar RED → configurar menor privilégio/auditoria → provar GREEN → inspecionar logs/expirar fixture.
5. **Parar:** ambiente não autorizado, acesso administrativo não justificado ou indício de dado real.
6. **Estado válido ao parar:** nenhuma permissão ampliada; fixture removível; configuração anterior reversível.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Subseção exata | Recorte da prova | Evidência esperada | Pré-condições | Ponto de parada | Estado final | Leva | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| F1-T01 | Configurar papéis, negação por padrão e trilha sintética | Fernando/TI | SPEC-1-001 | CA-1-001..004 | Dados e permissões; Fluxo e regras; TDD RED→GREEN | Executar primeiro o RED da matriz não aplicada; depois aplicar a matriz com Operador, Conferente e Admin e provar ações permitidas/negadas e eventos sanitizados | resultado da suíte + log sanitizado + matriz aplicada | B-ENV-01 resolvido; ambiente/repositório autorizados; FIX sintética revisada | parar antes de dado real, permissão fora da matriz ou acesso de suporte sem autorização temporal | RBAC e auditoria funcionais com fixture; nenhuma permissão implícita | 1 | Concluída — 2026-10-30 (teste humano aprovado) |
| F1-T02 | Ajustar e provar acesso seguro, expiração de testes e bloqueio de dado real no fluxo novo | Fernando/TI; aceite Auditoria/Faturamento | SPEC-1-001 | CA-1-005..006; CA-HV-045..047 | Emenda E-F1-20261030 — T02; TDD | Tentar leitura/alteração direta e via hook com operador/conferente/suporte sem escopo; tentar confirmar vazio e sobrescrever revisão; expirar fixture sintética | matriz de negações + regressão RBAC + prova de expiração em ambiente de teste | T11 aceita; autorização; fixture aprovada | parar se acesso indevido persistir ou houver dado real; nunca apagar arquivos do Drive | novas coleções protegidas sem desfazer T01 | 3 | Aberta — depende de T11; não repetir implementação da T01 |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|

## Emenda E-F1-20261030-02 — continuidade a partir do código

**Origem:** 3°_call.md (30/10), prompts do consultor aplicados diretamente no Skip e pedido expresso de ajustar as tarefas. Esta seção prevalece apenas nos pontos conflitantes do contrato anterior; preserva histórico, aceites e IDs.
**Degrau:** reuso do app React/PocketBase existente; não recriar o sistema nem assumir que publicar agente comprova OCR.
### Emenda E-F1-20261030 — T02
T01 está aceita em 30/10 11:57 (fonte raiz commit 6c11af2..b1cee1c). Não reabrir T01. Migração 0003 criou coleções novas com leitura ampla e update autenticado; essa superfície NÃO está homologada pelo aceite anterior.
T02 mantém CA-1-005/006 e cobre as novas coleções `clientes`, `ocorrencias`, `extracoes`, os arquivos protegidos e os hooks `hv_extrair_prontuario`/`hv_confirmar_dados`.
- **CA-HV-045:** negação por padrão também na API direta/arquivo; operador só cria no escopo permitido e não altera status, campos finais, responsável ou extrações. Conferente só consulta e confirma itens do escopo autorizado. Admin gerencia conforme matriz; suporte somente com concessão temporal existente.
- **CA-HV-046:** confirmar requer estado válido, obrigatórios revisados e trilha; nova tentativa não sobrescreve silenciosamente uma revisão aprovada; o operador não burla UI via CRUD/hook.
- **CA-HV-047:** guards sintéticos e expiração verificáveis no fluxo novo; nunca excluir arquivo do Drive. Provas de descarte somente fixtures no ambiente de teste autorizado.
**TDD adicional:** RED por perfis em API e hook; GREEN negar fora da matriz; REGRESSÃO expiração e revogação de suporte sem mudar T01. Guardar resultados sanitizados, não token/conteúdo clínico. Falha mantém T02 aberta.


### Recorte de implementação T02
Reusar papéis e concessões temporais da 0001/0002. Introduzir migração corretiva não destrutiva para 0003; não editar migração aplicada nem excluir registros. Bloquear update direto de status/campos finais/responsável pelo operador; confirmação via hook verificado por papel e escopo; arquivos protegidos com autorização equivalente à ocorrência. Criar/read/update de clientes conforme matriz (admin gerencia; operador consulta e cria para captura autorizada; conferente consulta somente o necessário; suporte só concessão temporal). Definir escopo nominal do piloto com Fernando antes de ampliar para real; até lá fixture isolada. Não redefinir o aceite T01. Rodar provas de CRUD direto e hooks com usuários sintéticos de cada papel.
