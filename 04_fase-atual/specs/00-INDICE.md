# Índice de SPECs — Fase 1 | Help Vida

**Fase:** Sistema de origem, extração e pré-preenchimento  
**Estado:** SPECs geradas em onda; nenhuma task/implementação autorizada  
**Gate de escopo:** `check-escopo` aprovado (Drive ID `1GGD4pIxbcgTdLYUnbm6qsEoiwY2ZpYqR`) e `check-cliente` aprovado (Drive ID `1R3rW4AwDKJjWL5BNqoiX3n_aAEfibkVe`) em 08/09/2026  
**Runtime:** SkillMind → gerar-specs; fallback `ethos-legacy` por contratos globais ausentes

## Resultado da fase

Provar, no recorte controlado de cinco casas, uma cadeia rastreável de entrada, extração assistida, conferência humana e template pré-preenchido, comparando tempo/custo manual e sistema. Uso real, provedor de IA e scraping permanecem condicionados aos gates próprios.

## Onda atual

| SPEC | Resultado observável | Estado | Gate principal |
|---|---|---|---|
| SPEC-1-001 | papéis, negação, auditoria e expiração com fixture | planejada; real bloqueado | ambiente + política para real |
| SPEC-1-002 | captura/upload com protocolo e fila | planejada | ambiente + recorte nominal |
| SPEC-1-003 | sugestão por campo e conferência humana | planejada; provedor bloqueado | provedor/contrato + dicionário |
| SPEC-1-004 | template versionado e comparação manual×sistema | planejada; template bloqueado | template + métrica + recorte |
| SPEC-1-005 | scraping detectável com fallback/reconciliação | bloqueada | permissão + contrato + segredo |

## Ordem lógica e independência

1. SPEC-1-001 cria o limite de acesso/auditoria no ambiente autorizado.
2. SPEC-1-002 entrega valor visível com massa sintética mesmo sem scraping.
3. SPEC-1-003 pode começar com fixture e motor aprovado; modo manual permanece funcional.
4. SPEC-1-004 fecha o incremento demonstrável e a medição.
5. SPEC-1-005 é integração separada e não bloqueia o fallback operacional.

## Bloqueios consolidados

- `B-ENV-01`: plataforma, ambiente e repositório autorizados.
- `B-DADOS-01`: política de dados/acesso/retention/processamento/incidente.
- `B-PILOTO-01`: cinco casas, operadora, modalidade, documento, operadores e owners.
- `B-ARQ-01`: tipos, tamanho, resolução e quantidade de arquivos homologados.
- `B-TEMPLATE-01`: template/versão/campos homologados.
- `B-METRICA-01`: relógios, fontes, coorte e responsável pelo baseline.
- `B-IA-01`: provedor/modelo/contrato/retenção/custo/autorização.
- `B-SCRAPE-01/02`: permissão e contrato técnico da fonte.
- `B-SECRET-01`: cofre, acesso e rotação.

## Revisão do painel gerar-specs

- **Analista de SPEC:** cobertura vertical preservada; cada mudança de permissão, dado e integração tem contrato próprio.
- **Risco:** dados de saúde, credenciais, IA e scraping têm gates e fallback explícitos.
- **TDD:** todas as SPECs possuem RED/GREEN/REGRESSÃO e caminhos de erro. SPEC-1-001/002 são prováveis primeiro com fixture; SPEC-1-003 tem Estágio A simulado e Estágio B condicionado; SPEC-1-004 depende de template/métrica; SPEC-1-005 permanece bloqueada.
- **Coerência:** fase termina em pré-preenchimento e aprovação interna; central/custos/envio permanecem fora.

## Fixtures compartilhadas

| ID | Conteúdo sintético | Uso |
|---|---|---|
| FIX-01 | documento legível completo | SPEC-1-002→003→004, fluxo nominal |
| FIX-02 | mesmo documento desfocado/cortado | SPEC-1-002/003, baixa qualidade |
| FIX-03 | documento incompleto com obrigatório ausente | SPEC-1-003/004, bloqueio |
| FIX-04 | arquivo inválido/acima do contrato | SPEC-1-002, rejeição |
| FIX-05 | duplicata binária de FIX-01 | SPEC-1-002/005, idempotência |
| FIX-06 | resposta simulada determinística campo→valor→origem→confiança | SPEC-1-003 Estágio A |

## Gate seguinte

Revisão e aceite humano destas SPECs. Somente depois, `gerar-tasks`. A primeira task futura deve ser escolhida individualmente; nenhuma implementação foi iniciada.

## Emenda E-F1-20261030-02 vigente

F1-T01 aceita; demais conforme tabela operacional atual. Esta seção substitui a narrativa inicial de nenhuma implementação. SPECs 001–005 preservadas com emendas; SPECs 006 integridade/T11, 007 guarda/T12–13, 008 consulta/T14–15 adicionadas. Oito SPECs justificadas por separar permissões, dado e duas integrações com provas/owners diferentes; não são oito frentes simultâneas. Scraping 005 está suspenso, não concluído.



1. Próxima candidata: **F1-T11**, retirar resultados inventados sem desfazer o visual.
2. Depois: **T02 → T03 → T04 → T05**. Só sintético enquanto a política não estiver aprovada.
3. **T12 → T13** resolve guarda SharePoint para uso real. **T14 → T15** consulta pacientes se o contrato de API for provado. Essas frentes externas não bloqueiam a conferência sintética/manual; não executar várias ao mesmo tempo.
4. **T06** é PoC de visão condicionada. Se não viável, manter manual; não declarar leitura funcionando. **T07 → T08** podem fechar saída/medição do fluxo manual se homologado, sem inventar aceite da T06.
5. T09/T10 suspensas, não encerradas nem substituídas silenciosamente; eventual retomada exige decisão explícita.



Fixtures devem contemplar 20 páginas, duas evoluções/página, paciente divergente, carimbo ilegível, ausência desconhecida, PDF digital/scan, JSON inválido e API indisponível. Nunca usar nome real de amostra como fixture.
