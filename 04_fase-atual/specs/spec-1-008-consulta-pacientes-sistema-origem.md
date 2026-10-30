# SPEC-1-008 — Consulta de pacientes ao sistema de origem

**Fase:** 1 / emenda E-F1-20261030-02
**Dono:** Fernando/TI; aceite operacional Auditoria/Faturamento
**Status:** planejada conforme bloqueios das tasks; código não alterado
**Degrau:** reuso do aplicativo e recursos existentes; integração nova somente após prova contratual.
**Fontes:** 3°_call.md 30/10 e código 41df705; prompts enviados pelo consultor são intenção, não prova.

## Estado atual e origem
50:56–52:05: Fernando informa API de consulta de pacientes/nome+convênio; produto transcrito “Skin Care”, nome exato a confirmar. 01:09:21 descreve cache/cron 03h em OUTRO app. O repo atual não comprova essa integração.
## Resultado observável
Paciente já cadastrado na origem pode ser selecionado no fluxo SES, sem nova digitação/duplicação e sem escrita no sistema mãe. Cadastro manual funciona enquanto API bloqueada.
## Contrato de prova e integração
T14 coleta documentação oficial/fornecedor, base URL, auth e escopo, endpoints reais, nome/convênio, chave estável, paginação, filtros, limites e ambiente de teste. Nenhum endpoint é inventado. Prova somente GET/consulta equivalente autorizada. Secrets no ambiente cliente; não pedir valores pelo chat.
T15 depende T14: reusar seletor existente, mapear chave externa por origem, atualizar cadastro sem confundir homônimos, preservar identificação manual revisada; falha parcial não desativa paciente nem apaga registro. Definir frequência/cache/SLA e botão de atualização COM Fernando; 03h é relato de outro app, não configuração autorizada aqui.
Dados mínimos nome+convênio e chave estável; não importar CPF/dados clínicos por padrão nem copiar código/credencial do outro projeto. Sem dado real antes da política.
## Critérios
CA-HV-059: produto/contrato de consulta verificados e ausência de escrita provada. CA-HV-060: autorização, paginação e limites testados com massa sintética/autorizada.
CA-HV-061: vínculo por chave da origem, homônimos separados e sem dupla criação. CA-HV-062: falha parcial preserva último estado e cadastro/seleção manual. CA-HV-063: consulta/atualização conforme frequência homologada, log sanitizado e aceites de TI/operação.
## TDD
T14 RED sem credencial autorizada → recusa; GREEN consulta mínima e paginação; REGRESSÃO limite/erro/auth. T15 RED paciente repetido/homônimo; GREEN seletor com origem e reconciliação; REGRESSÃO timeout/lote parcial e manual. Sem implementação antes do contrato; apenas leitura na origem.
## Limites, recuperação e parada
Sem documentação não adivinhar rota; parar e informar bloqueio. Não automatizar cron nem trocar canal por falta de integração. Rollback desliga consulta mantendo pacientes já homologados sem apagá-los. Este conector não cria regra clínica/comercial e não faz scraping.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Subseção exata | Recorte da prova | Evidência esperada | Pré-condições | Ponto de parada | Estado final | Leva | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| F1-T14 | Comprovar API de consulta do sistema de cadastro de pacientes | Fernando/TI; aceite Auditoria/Faturamento | SPEC-1-008 | CA-HV-059..060 | Contrato de prova read-only; TDD | Fernando confirma produto/fornecedor grafado Skin Care na call, documentação e auth; consulta sintética/autorizada para nome+convênio | contrato endpoint→campos + teste de leitura + paginação + limites; sem valores de chaves | T02 aceita; API/documentação/permissão fornecidas pelo cliente | não copiar integração do outro projeto nem inventar endpoint; só leitura | contrato de consulta provado ou bloqueio descrito | 7 | Bloqueada — nome exato, documentação e autenticação pendentes |
| F1-T15 | Reaproveitar pacientes do sistema de origem sem duplicar cadastro | Fernando/TI; aceite Auditoria/Faturamento | SPEC-1-008 | CA-HV-061..063 | Contrato de importação; TDD | Após prova, sincronizar nome+convênio por chave estável; tratar paginação/homônimos/falha e preservar seleção manual | teste de reconciliação + log sanitizado + aceite Fernando | T14 e T03 aceitas; chave/frequência homologadas | não ativar cron 03h por cópia da fala do outro app; sem escrita na origem | paciente selecionável com origem preservada e fallback manual | 9 | Bloqueada — depende T14; cadastro manual continua válido |

### Gate de detalhamento T15
O recibo T14 complementa esta SPEC com produto/fornecedor confirmados, URL/endpoint documentados, parâmetros, autenticação, chave única, schema mínimo, paginação/limites, frequência aprovada e arquivos afetados. Sem esse contrato revisado pelo consultor, T15 segue bloqueada; não deixar decisões estruturais ao executor.
