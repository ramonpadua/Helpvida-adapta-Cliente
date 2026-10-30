# CLAUDE — Help Vida

Siga `AGENTS.md`. A unidade de execução é uma task da Fase 1 vinculada a exatamente uma SPEC.

Antes de alterar qualquer coisa:

1. confirme que a task está autorizada e elegível;
2. leia critérios, pré-condições, ponto de parada e TDD da SPEC;
3. interrompa diante de bloqueio não resolvido;
4. mantenha dado real, IA externa e scraping desativados sem os respectivos gates.


## Retomada guiada após alinhamento SES

Ao receber “vamos continuar o projeto”, leia `GUIA-CONTINUAR-PROJETO.md`, `STATUS.md` e a SPEC da próxima task. Explique o que já existe, o que falta, a correção exata e como Fernando fará o teste em tela. Começar pela candidata T11; não refazer T01 nem criar agente duplicado. Fluxo SES entregue incorporado, não cobrar novamente. Não prometer visão/OCR comprovados só porque existe agente. Uma autorização e um teste humano por task.

Repo operacional: https://github.com/ramonpadua/Helpvida-adapta-Cliente
Código do sistema: https://github.com/FernandoHelpVida/Prescri-o-SES (submódulo `07-sistemas/Prescri-o-SES`).

## Contexto do sistema (repo operacional e builder)

- **Repositório operacional (raiz):** https://github.com/ramonpadua/Helpvida-adapta-Cliente
- **Repositório do código (cliente):** https://github.com/FernandoHelpVida/Prescri-o-SES — submódulo em `07-sistemas/Prescri-o-SES`
- **Builder (Skip):** https://novo-projeto-f88ac--preview.goskip.app — projeto 56877, organização da Soraya
- **Pasta do sistema no Drive:** `07-sistemas/Prescri-o-SES` (registro documental do vínculo)
- **Consulta do código:** buscar/atualizar o submódulo antes de avaliar o que o cliente construiu; o ponteiro fixa o commit, não acompanha sozinho.
