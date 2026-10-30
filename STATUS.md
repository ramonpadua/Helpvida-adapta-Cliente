# STATUS — Help Vida

- **Fase:** F1 — captura e conferência SES; emenda E-F1-20261030-02.
- **Concluída:** F1-T01, teste humano aprovado 30/10 11:57. Preservado, sem reabrir.
- **Tasks:** 1 aceita, 12 abertas (inclui implementações parciais), 2 suspensas T09/T10; total 15. Suspensa não equivale a concluída.
- **Próxima candidata:** F1-T11, corrigir falso sucesso da leitura; aguarda autorização e teste humano próprios. Nenhuma task de código executada nesta atualização documental.
- **Já construído:** tela/tema, paciente antes, cadastro, upload de arquivo único, fila, cards, agente e hooks (v0.0.10). Reusar; não reconstruir.
- **Bloqueio crítico:** hook manda só filename/cadastro e inventa valores em fallback; leitura de imagem/PDF NÃO provada.
- **Sequência principal:** T11 → T02 → T03 → T04 → T05; depois provas externas T12/T14 e integrações T13/T15 conforme gates; T06 visão condicionada; T07→T08 saída SES/medição com modo manual homologado possível. Uma por vez.
- **Pendências cliente:** fluxo SES recebido; formato final a homologar; limites completos de arquivo/lote; autorização/política de dados; destino/perfis/retencão SharePoint; documentação/autenticação da API de consulta e regras por autorização de paciente para fase posterior. Não perguntar de novo o que call já respondeu.
- **Gates:** sem dado real antes B-DADOS-01; sem visão externa sem decisão; local só estudo; sync 03h só foi relatado no outro app. Check-escopo/check-cliente 08/09 estão APROVADOS (corrige relato anterior de pendente).
- **Fontes:** call 30/10; raiz 8fe6477; código 41df705; prompts do dia como intenção. Existência de migration/agente ou build passando não aprova task.


## Fluxo SES recebido em 30/10 — fonte incorporada

Fonte: `FLUXO_ADAPTA_SES.docx`, Drive ID `1gJyymfrmYRe16tcogQfdjK4JCWvWse5_` (contexto), lido integralmente. **A entrega do fluxo pelas meninas está cumprida: não voltar a cobrá-lo.**
O documento confirma faturamento por pacote, auditoria de prescrições/evoluções manuscritas, carimbo/assinatura/legibilidade/rasuras, relatórios mensais por terapia e confronto com o **SpinCare**. Corrige a transcrição “Skin Care”: nome do sistema confirmado documentalmente como SpinCare; documentação/endpoints/autenticação da API ainda não foram entregues/provados.
Categorias incluem medicina, enfermagem, fisioterapia, fonoterapia, nutrição, serviço social, psicologia e relatórios de técnicos. Presença/legibilidade são conferidas sem atribuir identidade por rubrica.
Referência de pacote: baixa 6h técnico/fisio 3 por semana/fono 1; média 12h/3/1; alta sem ventilação 24h/5/2; alta com ventilação 24h/7/2. Visitas médica e enfermagem semanais; nutrição, serviço social e psicologia mensais. **Prevalece sempre autorização individual/vigência**, não aplicar frequência global nem automatizar cobrança/diagnóstico. Regras e confronto gerencial para etapa própria, não extrair narrativa clínica nesta correção.
O fluxo descreve processo institucional atual; fotos semanais antecipam preparação, não substituem automaticamente prontuário físico/relatórios assinados nem liberam faturamento. T07 já tem insumo de fluxo; formato de saída versionado e aceite operacional ainda precisam ser homologados, sem pedir ao cliente que entregue o mesmo fluxo novamente.

**Retomada:** siga `GUIA-CONTINUAR-PROJETO.md`; teste humano descrito em linguagem operacional e T01 preservada.
