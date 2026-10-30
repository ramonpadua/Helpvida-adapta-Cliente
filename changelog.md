# Changelog — Help Vida

## 2026-10-30

- 2026-10-30 · Fernando/TI · **F1-T11 implementada (aguarda teste humano)**: hook `hv_extrair_prontuario.js` reescrito sem fallback inventado — removeu o bloco que criava nome/data/profissional fixos com confiança alta em falha ou JSON inválido; passou a devolver `leitura_disponivel: false` com motivo explícito, sem marcar `extraido` e sem tocar campos revisados. `AnexarProntuario.tsx` e `ConferenciaDetalhe.tsx` não iniciam mais carimbo/assinatura como `true` (agora `null` = não verificado); origem e confiança só aparecem quando há sugestão real. Guard de papel na rota (operador dono do envio ou admin). Skip v0.0.10 → v0.0.13, QA passou em setup, análise estática, build e integrações. Prova negativa local 13/13.
- 2026-10-30 · Fernando/TI · **Limite de plataforma documentado**: o gateway de IA do Skip (`$ai.agent`/`$ai.chat`) recebe somente texto — não há entrada de imagem/visão; `$documents.toMarkdown` só lê PDF/DOC com camada de texto e falha em escaneado com 422 "OCR is required". Consequência: leitura de foto de prontuário permanece indisponível (T06); PDF digital é o único caminho de leitura real nesta versão.
- 30/10 · Consultor · Fluxo FLUXO_ADAPTA_SES.docx recebido e incorporado; nome SpinCare confirmado e cobrança do fluxo encerrada. Guia de retomada/teste leigo incluído em AGENTS/CLAUDE/README e GUIA-CONTINUAR-PROJETO.md. T11 orienta verificar agente no ambiente, corrigir fallback sem prometer visão e explicar testes por botões/papéis. T01/aceites preservados; app não alterado.
- 2026-10-30 · Consultor (pedido Ramon) · E-F1-20261030-02: continuidade pós-call e prompts aplicada SOMENTE em documentação. T01/aceite preservados; tarefas abertas reaproveitam tela/agente/fila existentes. T11 correção de falso sucesso priorizada; T12/T13 guarda SharePoint e T14/T15 API consulta condicionais. T09/T10 scraping suspensas, sem conclusão. SES semanal, capacidade de lote >=20 fotos (não máximo), múltiplas evoluções e revisão humana; regras/custos posteriores. Check 08/09 confirmado aprovado. Sem alteração do app, deploy ou serviço externo.
- 2026-10-30 · Consultor · Vínculo do sistema: criado submódulo Git real `07-sistemas/Prescri-o-SES` (gitlink `160000`, commit `41df705`) apontando para o repositório do cliente `FernandoHelpVida/Prescri-o-SES`. `.gitmodules` publicado com URL limpa (sem credencial); registro em `07-sistemas/Prescri-o-SES-vinculo.md`. Nenhuma fase, task, SPEC ou aceite alterado.
- 2026-10-30 · Fernando/TI · Task F1-T01 concluída: teste humano aprovado pelo champion ("está tudo de acordo"); revalidação independente confirmou migrações 0001/0002 aplicadas, regras de acesso e hooks de RBAC/auditoria intactos e prévia renderizando login (v0.0.7). Evidências: painel admin + logs do projeto Skip "Novo Projeto" (56877).
- 2026-10-30 · Fernando/TI · Paleta da marca Help Vida aplicada ao tema (v0.0.8): tokens em `src/main.css` e `tailwind.config.ts` reancorados na logo oficial (verde escuro #06301F, teal #128A68, verde claro #6FC7AE, amarelo #D3B308, fundo #F4F6F5); QA passou em setup, análise estática, build e integrações; prévia confere as cores na tela de login. Sem alteração de regra, dado ou hook.
- 2026-10-30 · Fernando/TI · Emenda E-1 proposta na SPEC-1-002: contrato `B-ARQ-01` passa a modelar lote de N páginas por ocorrência (mínimo proposto de 20), com página indexada, hash e qualidade próprios. **Aguardando homologação de Fernando/TI** — nenhum valor implementado.
- 2026-10-30 · Fernando/TI · Ambiente Skip verificado: migration `0005_leitor_prontuarios_helpvida` **applied**; agentes `leitor-prontuarios-helpvida` (id mkebr90cetvr01z) e `prontuario-extractor` existem com tier fast e prompt de transcrição fiel. A pendência registrada no guia ("não confirmado em execução") está resolvida.

## 2026-09-15

- 2026-09-15 · Fernando/TI · F1-T01: implementação restrita concluída no projeto Skip "Novo Projeto" (versão 0.0.5); migrações `0001_hv_access_control` e `0002_hv_harden_user_access` aplicadas; QA oficial passou em setup, análise estática, build, integrações e teste; teste humano ainda pendente.
- 2026-09-15 · Fernando/TI · DEBUG task F1-T01: app ficou em branco na prévia v0.0.4 → causa raiz `ReferenceError` na montagem de `Index.tsx` (bloco de provas inserido em `Login`, fora do escopo de `user`, `proofOccurrence` e `runProof`) → corrigido na v0.0.5.

## 2026-09-08

- Workspace externo da Fase 1 preparado a partir do handoff validado.
- Incluídas cinco SPECs e F1-T01..F1-T10.
- Ata de corte de 03/09 incluída sem transcrição bruta.
- Nenhuma implementação, integração, conta, repositório ou conector criado.