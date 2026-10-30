# Estado atual — Adapta Cliente

- task_id: F1-T11
- champion: Fernando/TI
- spec: 04-fase-atual/specs/spec-1-006-integridade-da-extracao.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada + 2026-10-30T15:37-03:00; trecho: "Pode corrigir agora"
- teste_humano: pendente
- verificacao_automatica: passou + Skip v0.0.13; QA setup/análise estática/build/integrações OK; prova negativa local 13/13 (foto→indisponível, PDF escaneado→indisponível, agente fora do ar→indisponível, resposta não-JSON→indisponível, resultado sem origem→recusado, sugestão com origem→aceita, conferente→403)
- aprendizado: pendente
- ultima_acao: hook de extração reescrito sem fallback inventado; telas sem default true de carimbo/assinatura; build v0.0.13 publicado na prévia
- proxima_acao: executar teste humano da F1-T11 e informar se funcionou
- atualizado_em: 2026-10-30T16:05:00-03:00

## Continuidade documental — E-F1-20261030-02

- F1-T01 permanece concluída; trecho de aceite preservado.
- F1-T11 implementada nesta data; NÃO aceita ainda — aguarda teste humano.
- Agente verificado no ambiente: migration `0005_leitor_prontuarios_helpvida` applied; slugs `leitor-prontuarios-helpvida` e `prontuario-extractor` existem (tier fast).
- Limite de plataforma confirmado na documentação Skip: gateway de IA aceita somente texto; não há entrada de imagem/visão. Leitura de foto fica para T06.
- Em seguida: T02 → T03 → T04 → T05; integrações guarda/pacientes e PoC condicionais conforme fase.md.
