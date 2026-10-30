# Instruções do agente — Help Vida

Você apoia a TI da Help Vida na execução controlada da Fase 1.

- Fonte de trabalho: `04_fase-atual/fase.md` e a SPEC vinculada em `04_fase-atual/specs/`.
- Execute somente uma task por vez e somente após autorização humana.
- Nunca invente campo, regra, permissão, integração, arquitetura ou critério de aceite.
- Use massa sintética enquanto a política de dados reais não estiver aprovada.
- Rode o TDD da SPEC e preserve evidências sanitizadas.
- Após a task, peça teste humano e aguarde autorização antes de avançar.
- Falha mantém a task aberta; diagnostique sem ampliar o escopo.
- Não faça push, publique, crie repo, conta, conector ou segredo sem confirmação explícita.


## Retomada guiada após alinhamento SES

Ao receber “vamos continuar o projeto”, leia `GUIA-CONTINUAR-PROJETO.md`, `STATUS.md` e a SPEC da próxima task. Explique o que já existe, o que falta, a correção exata e como Fernando fará o teste em tela. Começar pela candidata T11; não refazer T01 nem criar agente duplicado. Fluxo SES entregue incorporado, não cobrar novamente. Não prometer visão/OCR comprovados só porque existe agente. Uma autorização e um teste humano por task.

## Contexto do sistema (repo operacional e builder)

- **Repositório operacional (raiz):** https://github.com/ramonpadua/Helpvida-adapta-Cliente
- **Repositório do código (cliente):** https://github.com/FernandoHelpVida/Prescri-o-SES — submódulo em `07-sistemas/Prescri-o-SES`
- **Builder (Skip):** https://novo-projeto-f88ac--preview.goskip.app — projeto 56877, organização da Soraya
- **Pasta do sistema no Drive:** `07-sistemas/Prescri-o-SES` (registro documental do vínculo)
- **Consulta do código:** buscar/atualizar o submódulo antes de avaliar o que o cliente construiu; o ponteiro fixa o commit, não acompanha sozinho.
