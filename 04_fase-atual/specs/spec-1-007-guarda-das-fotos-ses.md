# SPEC-1-007 — Guarda das fotos SES e consulta autenticada

**Fase:** 1 / emenda E-F1-20261030-02
**Dono:** Fernando/TI; aceite operacional Auditoria/Faturamento
**Status:** planejada conforme bloqueios das tasks; código não alterado
**Degrau:** reuso do aplicativo e recursos existentes; integração nova somente após prova contratual.
**Fontes:** 3°_call.md 30/10 e código 41df705; prompts enviados pelo consultor são intenção, não prova.

## Estado atual
Arquivo está no file field PocketBase por ocorrência; SharePoint e servidor local NÃO têm integração no repo.
## Resultado e governança
Call 25:25–27:46 exige retenção para consulta/prova, cita SharePoint/OneDrive e cogita servidor local. SharePoint é direção inicial; endereço, autorização, política e implantação NÃO foram demonstrados. Servidor local e transferência recorrente são estudo condicionado, não promessa nem automação criada.
## Contrato de guarda
Fernando/TI indica tenant/site/biblioteca/pasta autorizados, owner, escopos de acesso, retenção, base/finalidade, usuários e recuperação. Secret só em Secrets do ambiente cliente; nenhum token no chat/repo. Conteúdo saúde: sintético até B-DADOS-01. Permissão mínima; usuário sem escopo não baixa original nem por URL direta.
Páginas mantêm hash/índice/protocolo, origem e identificador estável do objeto; URL temporária não é referência única. Metadados ficam no app. Falha de upload remoto mantém página pendente e original preservado; retry idempotente e checagem de hash. Não marcar arquivado antes da confirmação.
T12 prova acesso com arquivo sintético autorizado e homologa contrato de guarda; não implementa integração completa. T13 só implementa contrato provado. Não mover/apagar original nem ativar cópia local automaticamente. Qualquer expiração de temporário depende de política e prova em teste; NUNCA apagar nada do Drive do Ramon.
## Critérios
CA-HV-054: owner define destino/perfis/retencão e decisão sobre local fica explícita. CA-HV-055: prova sintética autenticada de leitura/escrita, escopo restrito e credencial não exposta.
CA-HV-056: página remota é recuperada por usuário autorizado mantendo hash e vínculo durável. CA-HV-057: timeout/retry sem duplicação silenciosa/perda e alerta visível. CA-HV-058: acesso indevido negado e rollback para captura sintética/manual sem destruir arquivos.
## TDD
T12 RED sem permissão → negado; GREEN objeto sintético criado/consultado; REGRESSÃO usuário fora do escopo e segredo fora de log. T13 RED falha de rede; GREEN guardar/recuperar lote; REGRESSÃO troca de URL, retry e hash. Evidência sanitizada + teste de TI. Não executar contra SharePoint não autorizado.
## Parada e rollback
Sem contrato/prova/política não há real; bloqueio externo não paralisa T03–T05 sintéticos. Destino local depende de prova de conectividade e decisão humana futura; não criar webhook/cron como substituto silencioso.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Subseção exata | Recorte da prova | Evidência esperada | Pré-condições | Ponto de parada | Estado final | Leva | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| F1-T12 | Definir e provar onde as fotos SES serão guardadas | Fernando/TI; aceite Auditoria/Faturamento | SPEC-1-007 | CA-HV-054..055 | Contrato de guarda; TDD da prova | Fernando indica site/biblioteca autorizados, perfis, retenção e serviço; provar leitura/escrita de arquivo sintético e consulta pelo app | matriz de acesso + prova sintética + decisão de retenção; sem segredos em chat | T02 aceita; autorização do dono de SharePoint; sem dado real | parar sem site/conta/permissão; servidor local é estudo, não promessa | contrato de armazenamento definido antes de integração | 7 | Bloqueada por acesso/contrato externo; não bloqueia testes sintéticos T03–T05 |
| F1-T13 | Integrar guarda SharePoint sem perder o vínculo com as páginas | Fernando/TI; aceite Auditoria/Faturamento | SPEC-1-007 | CA-HV-056..058 | Contrato de integração; TDD da implementação | Reusar lotes T03; upload autorizado, identificador durável e consulta autenticada; falha/retry sem perder original; estudo local separado | teste de falha e consulta + hashes + autorização + aceite de TI | T12 e T04 aceitas; contrato e política antes de real | não apagar/mover originais nem sincronizar servidor local sem novo gate | guarda consultável; metadados no app, cópia temporária conforme política | 8 | Bloqueada — depende da prova T12; integração NÃO existe no código |

### Gate de detalhamento T13
O recibo T12 deve incorporar à SPEC endpoints documentados, fluxo de autorização, permissões, payloads/respostas, chave de reconciliação, limites e caminhos físicos de hook/migration a alterar no app. Sem esse detalhamento revisado pelo consultor, T13 não está liberada para implementação. Bibliotecas/provedores não são escolhidos pelo executor.
