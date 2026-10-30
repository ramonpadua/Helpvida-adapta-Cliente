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
| F1-T14 | Comprovar API de consulta do sistema de cadastro de pacientes | Fernando/TI; aceite Auditoria/Faturamento | SPEC-1-008 | CA-HV-059..060 | Contrato de prova read-only; TDD | Fernando confirma produto/fornecedor grafado Skin Care na call, documentação e auth; consulta sintética/autorizada para nome+convênio | contrato endpoint→campos + teste de leitura + paginação + limites; sem valores de chaves | T02 aceita; API/documentação/permissão fornecidas pelo cliente | não copiar integração do outro projeto nem inventar endpoint; só leitura | contrato de consulta provado ou bloqueio descrito | 7 | Bloqueada — SpinCare confirmado; documentação e autenticação pendentes |
| F1-T15 | Reaproveitar pacientes do sistema de origem sem duplicar cadastro | Fernando/TI; aceite Auditoria/Faturamento | SPEC-1-008 | CA-HV-061..063 | Contrato de importação; TDD | Após prova, sincronizar nome+convênio por chave estável; tratar paginação/homônimos/falha e preservar seleção manual | teste de reconciliação + log sanitizado + aceite Fernando | T14 e T03 aceitas; chave/frequência homologadas | não ativar cron 03h por cópia da fala do outro app; sem escrita na origem | paciente selecionável com origem preservada e fallback manual | 9 | Bloqueada — depende T14; cadastro manual continua válido |

### Gate de detalhamento T15
O recibo T14 complementa esta SPEC com produto/fornecedor confirmados, URL/endpoint documentados, parâmetros, autenticação, chave única, schema mínimo, paginação/limites, frequência aprovada e arquivos afetados. Sem esse contrato revisado pelo consultor, T15 segue bloqueada; não deixar decisões estruturais ao executor.


## Fluxo SES recebido em 30/10 — fonte incorporada

Fonte: `FLUXO_ADAPTA_SES.docx`, Drive ID `1gJyymfrmYRe16tcogQfdjK4JCWvWse5_` (contexto), lido integralmente. **A entrega do fluxo pelas meninas está cumprida: não voltar a cobrá-lo.**
O documento confirma faturamento por pacote, auditoria de prescrições/evoluções manuscritas, carimbo/assinatura/legibilidade/rasuras, relatórios mensais por terapia e confronto com o **SpinCare**. Corrige a transcrição “Skin Care”: nome do sistema confirmado documentalmente como SpinCare; documentação/endpoints/autenticação da API ainda não foram entregues/provados.
Categorias incluem medicina, enfermagem, fisioterapia, fonoterapia, nutrição, serviço social, psicologia e relatórios de técnicos. Presença/legibilidade são conferidas sem atribuir identidade por rubrica.
Referência de pacote: baixa 6h técnico/fisio 3 por semana/fono 1; média 12h/3/1; alta sem ventilação 24h/5/2; alta com ventilação 24h/7/2. Visitas médica e enfermagem semanais; nutrição, serviço social e psicologia mensais. **Prevalece sempre autorização individual/vigência**, não aplicar frequência global nem automatizar cobrança/diagnóstico. Regras e confronto gerencial para etapa própria, não extrair narrativa clínica nesta correção.
O fluxo descreve processo institucional atual; fotos semanais antecipam preparação, não substituem automaticamente prontuário físico/relatórios assinados nem liberam faturamento. T07 já tem insumo de fluxo; formato de saída versionado e aceite operacional ainda precisam ser homologados, sem pedir ao cliente que entregue o mesmo fluxo novamente.

**Retomada:** siga `GUIA-CONTINUAR-PROJETO.md`; teste humano descrito em linguagem operacional e T01 preservada.
