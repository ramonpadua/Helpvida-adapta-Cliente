# STATUS — Help Vida

- **Fase:** F1 — captura e conferência SES; emenda E-F1-20261030-02.
- **Concluída:** F1-T01, teste humano aprovado 30/10 11:57. Preservado, sem reabrir.
- **Tasks:** 1 aceita, 12 abertas (inclui implementações parciais), 2 suspensas T09/T10; total 15. Suspensa não equivale a concluída.
- **Próxima candidata:** F1-T11, corrigir falso sucesso da leitura; aguarda autorização e teste humano próprios. Nenhuma task de código executada nesta atualização documental.
- **Já construído:** tela/tema, paciente antes, cadastro, upload de arquivo único, fila, cards, agente e hooks (v0.0.10). Reusar; não reconstruir.
- **Bloqueio crítico:** hook manda só filename/cadastro e inventa valores em fallback; leitura de imagem/PDF NÃO provada.
- **Sequência principal:** T11 → T02 → T03 → T04 → T05; depois provas externas T12/T14 e integrações T13/T15 conforme gates; T06 visão condicionada; T07→T08 saída SES/medição com modo manual homologado possível. Uma por vez.
- **Pendências cliente:** fluxo SES corrigido e formato final; limites completos de arquivo/lote; autorização/política de dados; destino/perfis/retencão SharePoint; documentação/autenticação da API de consulta e regras por autorização de paciente para fase posterior. Não perguntar de novo o que call já respondeu.
- **Gates:** sem dado real antes B-DADOS-01; sem visão externa sem decisão; local só estudo; sync 03h só foi relatado no outro app. Check-escopo/check-cliente 08/09 estão APROVADOS (corrige relato anterior de pendente).
- **Fontes:** call 30/10; raiz 8fe6477; código 41df705; prompts do dia como intenção. Existência de migration/agente ou build passando não aprova task.
