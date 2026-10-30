# SPEC-1-004 — Template pré-preenchido, aprovação interna e medição

**Fase:** 1  
**Status:** planejada; template nominal bloqueado  
**Dono:** Fernando/TI; homologação por Milene + Auditoria/Faturamento + Gestão  
**Origem no escopo:** DH-02, DH-06, DH-10; Fase 1 — template e baseline  
**Degrau da solução:** reuso — preencher o template operacional homologado pela Help Vida sem redesenhá-lo nem criar regra de cobrança.

## Contexto e decisões fechadas

- **Estado atual:** preenchimento manual e custo/tempo sem série comparável consolidada.
- **Estado desejado:** dados conferidos geram versão pré-preenchida do template com prova de origem; execução paralela mede manual versus sistema na mesma coorte.
- **Decisões fechadas:** somente completude/formato; fim do MVP em aprovação interna; métrica norte é tempo mediano origem→aprovação interna; hipótese 14→10 não é meta.
- **Bloqueios:** `B-TEMPLATE-01` arquivo/versão/campos e regras de formato homologados; `B-PILOTO-01`; `B-METRICA-01` responsável, relógios, fonte do tempo/custo manual e janela de comparação.

## Resultado observável

Uma ocorrência integralmente conferida gera um template marcado como pré-preenchido, com versão e rastreabilidade de cada campo; nenhum documento incompleto é liberado. Um painel/relatório compara a mesma coorte manual e sistema sem misturar volume ou período.

## Limites e dependências

- **Inclui:** mapeamento campo→template; versão; validação de presença/formato; prévia; regeneração versionada; aprovação interna; exportação apenas de fixture sintética para destino autorizado da sessão de teste, com ator/instante registrados e marca `NÃO ENVIADO`; eventos e métricas. Dado real não pode ser exportado na Fase 1 sem política e autorização específica do canal/destino.
- **Fora:** envio/e-mail/portal/XML/TISS, aceite da operadora, cálculo de cobrança, glosa, regra clínica, impressão automática.
- **Entradas:** campos conferidos da SPEC-1-003; template homologado; relógios da coorte.
- **Saídas:** template pré-preenchido; manifesto de campos/origens; relatório de baseline e resultado.
- **Superfícies/arquivos/configurações afetadas:** gerador de template, manifesto, tela de aprovação interna, instrumentação/relatório e testes; caminhos físicos ficam bloqueados até `B-ENV-01`.
- **Risco e plano B:** template muda → bloquear nova geração, manter versão anterior identificada e voltar ao preenchimento manual.
- **Rollback:** invalidar versão gerada sem apagar trilha; regenerar somente após nova homologação.

## Dados e métricas

| Métrica | Início | Fim | Agregação | Regra |
|---|---|---|---|---|
| tempo mediano | disponibilidade registrada da origem | aprovação interna | mediana por coorte | manual e sistema na mesma modalidade/documento |
| correção de campos | sugestão inicial | valor final | % por campo | excluir campos sem sugestão do denominador e reportá-los à parte |
| retrabalho | retorno a `corrigir` | nova conferência | taxa por ocorrência | motivo obrigatório |
| primeira conferência | abertura da conferência | aprovado sem retorno | proporção | mesma coorte |
| custo de coleta | ocorrência | entrega da origem | unidade monetária e composição definidas em `B-METRICA-01` | fonte e responsável registrados; não misturar unidades |

| Regra | Condição | Resultado |
|---|---|---|
| RN-401 | obrigatório não conferido | não gerar versão liberável |
| RN-402 | template/versão divergente | bloquear e solicitar homologação |
| RN-403 | regeneração após correção | criar nova versão; preservar anterior como substituída |
| RN-404 | coortes/períodos diferentes | relatório sinaliza incomparável; não calcula ganho conclusivo |
| RN-405 | documento aprovado internamente | marcar explicitamente `NÃO ENVIADO À OPERADORA` |

## Fluxo

1. Conferente conclui a revisão da SPEC-1-003.
2. Sistema valida completude/formato contra versão homologada.
3. Gera prévia + manifesto de origem.
4. Conferente compara e aprova internamente ou devolve a `corrigir`.
5. Sistema fecha relógios e atualiza relatório comparável.
6. Demonstração deixa claro que não houve envio/aceite externo.

## Checklist de execução

- [ ] Template e mapeamento assinados por Auditoria/Faturamento.
- [ ] Versão exibida no documento e manifesto.
- [ ] Incompleto, formato inválido e mudança de versão testados.
- [ ] Relógios manual/sistema definidos e reconciliados.
- [ ] Aviso `NÃO ENVIADO` visível.
- [ ] Relatório não contém hipótese 14→10 como resultado.

## Critérios de aceite

- [ ] **CA-1-019:** somente campos conferidos alimentam o template.
- [ ] **CA-1-020:** cada campo do template rastreia valor final e origem.
- [ ] **CA-1-021:** incompletude/formato inválido bloqueiam aprovação interna.
- [ ] **CA-1-022:** versão/regeneração são rastreáveis e reversíveis.
- [ ] **CA-1-023:** saída distingue pré-preenchido/aprovado internamente de enviado/aceito externamente.
- [ ] **CA-1-024:** relatório compara coorte e janela equivalentes e apresenta baseline, resultado, volume e limitações.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | template não mapeado | gerar com fixture conferida | ausência/mapeamento errado é detectado | diff RED |
| GREEN | geração homologada | gerar nominal e comparar campo a campo | template/manifesto corretos; aprovação interna possível | diff + versão + aceite |
| REFACTOR/REGRESSÃO | incompleto/versão/coorte | remover obrigatório, trocar versão e misturar períodos | bloqueios explícitos; ganho não calculado indevidamente | suíte/roteiro + relatório |

**Dados/fixtures:** FIX-01 e FIX-03 do índice, enriquecidas apenas pelo mapeamento do template homologado; preservar os IDs ponta a ponta.  
**Evidência exigida:** diff esperado×gerado, manifesto, relatório comparativo e aceite humano.

## Handoff e operação

- **Como demonstrar:** gerar, devolver para correção, regenerar e mostrar relatório.
- **Como operar:** Auditoria/Faturamento homologa template e aprova; Gestão valida comparação.
- **Como monitorar:** tempo mediano, correção, retrabalho, primeira conferência e custo de coleta.
- **Pendência:** valores nominais dependem de `B-PILOTO-01`, `B-TEMPLATE-01` e `B-METRICA-01`.

## Instruções de execução para o Ethos

1. **Ler antes:** SPEC-1-003 aceita, template/versionamento e contrato `B-METRICA-01`.
2. **Alterar somente:** mapeamento, gerador, manifesto, aprovação interna, relógios e relatório.
3. **Não alterar:** conteúdo do template homologado, regras de cobrança, canais externos ou status de aceite da operadora.
4. **Ordem:** RED de mapeamento → geração nominal → bloqueios → versionamento → comparação de coorte.
5. **Parar:** template sem versão, campo sem origem, coortes incomparáveis ou destino de exportação não autorizado.
6. **Estado válido ao parar:** versão anterior preservada; preenchimento manual disponível; artefato marcado `NÃO ENVIADO`.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Subseção exata | Recorte da prova | Evidência esperada | Pré-condições | Ponto de parada | Estado final | Leva | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| F1-T07 | Homologar a ficha SES e gerar a saída conferida sem envio externo | Fernando/TI; aceite Auditoria/Faturamento | SPEC-1-004 | CA-1-019..023; CA-HV-053 | Emenda E-F1-20261030 — saída SES; TDD | Reusar fluxo SES recebido em 30/10; aprovar formato com auditoria; gerar por paciente/período com evoluções validadas, sem dupla contagem | modelo SES versionado + comparação campo a campo + manifesto NÃO ENVIADO | T05 aceita; B-TEMPLATE-01 SES e B-PILOTO-01 resolvidos; manual possível | não usar template Unimed por padrão; não decidir cobrança/pagamento | saída SES aprovada internamente; modo manual independente da PoC | 11 | Bloqueada — fluxo SES recebido; modelo/aceite ainda a homologar; não recriar modelo por suposição |
| F1-T08 | Comparar tempo e retrabalho do piloto SES com o processo manual | Fernando/TI; aceite Auditoria/Faturamento | SPEC-1-004 | CA-1-024 | Dados e métricas; Emenda E-F1-20261030; TDD | Comparar mesma coorte/janela e origem→aprovação; separar manual/automático e volume por página/evolução | baseline + resultado + volume + limitações + decisão de expansão | T07 aceita; B-METRICA-01 homologado; real só após política | não converter desejo 14→10 em meta nem prometer novo prazo sem capacidade | ganho auditável ou ausência de ganho explicitada | 12 | Aberta — depende de T07 e baseline |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|

## Emenda E-F1-20261030-02 — continuidade a partir do código

**Origem:** 3°_call.md (30/10), prompts do consultor aplicados diretamente no Skip e pedido expresso de ajustar as tarefas. Esta seção prevalece apenas nos pontos conflitantes do contrato anterior; preserva histórico, aceites e IDs.
**Degrau:** reuso do app React/PocketBase existente; não recriar o sistema nem assumir que publicar agente comprova OCR.
### Emenda E-F1-20261030 — saída SES
O recorte prioritário é SES/Secretaria de Estado de Saúde, não formulário Unimed (04:58–06:44;56:35–01:00:12). Fonte de entrada é foto/lote, não scraping obrigatório.
**CA-HV-053:** Auditoria homologa formato SES versionado a partir do fluxo corrigido prometido na call; a saída relaciona paciente, período e evoluções efetivamente conferidas com data/profissional/categoria e origem. Contagem é de registros de evolução validados, NÃO de fotos; não tratar contagem como terapia paga ou falta clínica automaticamente. Não inventar formato oficial SES nem converter o modelo Unimed em aceite.
T07 reusa campos e fila; fluxo corrigido/modelo são B-TEMPLATE-01. Testar duas evoluções/página, mesma evolução reapresentada sem dupla contagem conforme chave homologada e origem ausente impedindo confirmação.
As regras de frequência variam por autorização/paciente (48:37–50:24); colher com auditoria durante homologação os exemplos, vigência, frequência/unidade, exceções e quem valida, para a F2. Não aplicar mínimo global de fisio/fono nem implementar motor de pendências nesta F1. Faturamento SES em pacote não elimina validação humana. Pagamento/custos individuais ficam F3.
T08 compara coorte/prazo/volume equivalentes no manual e sistema; se modo manual for validado, medir e declarar explicitamente que leitura automática continua bloqueada. Real só com política/guarda aprovadas. Sem promessa automática de reduzir equipe ou concluir em 2 meses.



## Fluxo SES recebido em 30/10 — fonte incorporada

Fonte: `FLUXO_ADAPTA_SES.docx`, Drive ID `1gJyymfrmYRe16tcogQfdjK4JCWvWse5_` (contexto), lido integralmente. **A entrega do fluxo pelas meninas está cumprida: não voltar a cobrá-lo.**
O documento confirma faturamento por pacote, auditoria de prescrições/evoluções manuscritas, carimbo/assinatura/legibilidade/rasuras, relatórios mensais por terapia e confronto com o **SpinCare**. Corrige a transcrição “Skin Care”: nome do sistema confirmado documentalmente como SpinCare; documentação/endpoints/autenticação da API ainda não foram entregues/provados.
Categorias incluem medicina, enfermagem, fisioterapia, fonoterapia, nutrição, serviço social, psicologia e relatórios de técnicos. Presença/legibilidade são conferidas sem atribuir identidade por rubrica.
Referência de pacote: baixa 6h técnico/fisio 3 por semana/fono 1; média 12h/3/1; alta sem ventilação 24h/5/2; alta com ventilação 24h/7/2. Visitas médica e enfermagem semanais; nutrição, serviço social e psicologia mensais. **Prevalece sempre autorização individual/vigência**, não aplicar frequência global nem automatizar cobrança/diagnóstico. Regras e confronto gerencial para etapa própria, não extrair narrativa clínica nesta correção.
O fluxo descreve processo institucional atual; fotos semanais antecipam preparação, não substituem automaticamente prontuário físico/relatórios assinados nem liberam faturamento. T07 já tem insumo de fluxo; formato de saída versionado e aceite operacional ainda precisam ser homologados, sem pedir ao cliente que entregue o mesmo fluxo novamente.

**Retomada:** siga `GUIA-CONTINUAR-PROJETO.md`; teste humano descrito em linguagem operacional e T01 preservada.
