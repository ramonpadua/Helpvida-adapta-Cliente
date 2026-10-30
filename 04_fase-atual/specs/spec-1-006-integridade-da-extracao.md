# SPEC-1-006 — Integridade da leitura e fallback manual sem invenção

**Fase:** 1 / emenda E-F1-20261030-02
**Dono:** Fernando/TI; aceite operacional Auditoria/Faturamento
**Status:** planejada conforme bloqueios das tasks; código não alterado
**Degrau:** reuso do aplicativo e recursos existentes; integração nova somente após prova contratual.
**Fontes:** 3°_call.md 30/10 e código 41df705; prompts enviados pelo consultor são intenção, não prova.

## Estado atual e evidência
`hv_extrair_prontuario.js` em 41df705 constrói mensagem com filename/cadastro, não envia bytes; após erro/JSON inválido cria nome/data/profissional/registro fixos e confiança alta. `AnexarProntuario` usa true como default de presença. Isso é demonstração enganosa, não extração. Agente existe na migration 0005; 0006 é no-op.
## Resultado observável
Sem leitura comprovada, sistema mostra leitura indisponível e abre conferência manual com sugestões vazias/null; nunca gera sucesso da IA.
## Contrato de integridade
- T11 altera só fallback/erro/validação de resposta e rótulos dessa superfície, sem remover tela/registro/cadastro/agente já existentes.
- Valores do cadastro servem para comparação; nunca como transcrição. Remover defaults de profissional/data/assinatura/carimbo.
- Não gravar sugestões em campos finais antes de revisão; preservar existentes auditados, sem apagar dados nem reprocessar silenciosamente.
- JSON inválido, timeout, visão não suportada ou resultado sem origem → estado recuperável com modo manual, sem trocar para extraído com sucesso.
- Fixtures simuladas somente em caminho explícito rotulado SIMULAÇÃO, separado de qualquer botão de extração operacional.
## Critérios e TDD
- CA-HV-041: falha do agente não retorna valores de exemplo nem alta confiança.
- CA-HV-042: nenhuma imagem enviada ao motor implica leitura indisponível, sem alegação de análise.
- CA-HV-043: campos ausentes/desconhecidos permanecem null e visíveis para conferência; texto de erro não expõe dado sensível.
- CA-HV-044: foto/protocolo e modo manual seguem acessíveis; UI não mostra presença=true por default nem sobrescreve final revisado.
RED: testar gateway que falha/JSON inválido/sem conteúdo; registrar comportamento atual em fixture. GREEN: retirar fallback inventado e verificar CA041..044. REGRESSÃO: fluxo de upload e conferência manual, visual e autenticação legados sem regressão T01.
Comandos: lint/build do package atual; `npm test` é placeholder e NÃO conta como prova. Criar testes focados de integração com mocks, sem dados reais/conta produção. Teste humano: Fernando provoca indisponibilidade controlada e confirma que nenhum campo foi inventado; auditoria confere modo manual.
## Limites, rollback e ponto de parada
Nenhuma chamada de visão/serviço novo, publicação ou dado real. Se correção exigir ampliar arquitetura, parar e registrar. Rollback desliga extração automática, não volta à geração de valores falsos. Sem exclusão em Drive.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Subseção exata | Recorte da prova | Evidência esperada | Pré-condições | Ponto de parada | Estado final | Leva | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| F1-T11 | Corrigir a leitura que inventa resultados e deixar o modo manual honesto | Fernando/TI; aceite Auditoria/Faturamento | SPEC-1-006 | CA-HV-041..044 | Contrato de integridade; TDD | Forçar erro/JSON inválido e trocar imagem sem mudar cadastro; saída nunca usa nome/data/profissional de exemplo | testes negativos + diff sanitizado + teste humano | T01 concluída; autorização desta task; só sintético | parar antes de serviço externo, dado real ou qualquer resultado sem origem | sem falso sucesso; indisponibilidade visível; foto e conferência preservadas | 2 | Próxima candidata — aguarda autorização; correção ainda NÃO executada |

## Permissões desta correção
Não ampliar acesso atual durante T11: limitar prova a fixture isolada, aplicação só após autorização. Guard mínimo da rota exige papel e escopo autorizado na ocorrência; se isso exigir migração da matriz, desligar extração automática e encaminhar a T02 antes de reativar. Regressão das novas coleções fica T02, não reabre T01.
